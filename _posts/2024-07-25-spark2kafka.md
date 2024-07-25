---
title: spark에서 kafka로 steam user 정보 적재
date: 2024-06-30 16:30:00 +0900
categories: [PipeLine]
tags: [pipeline]     # TAG names should always be lowercase
authors: [LoafingCat]
---



## 수정 필요함


    from datetime import datetime
    from airflow.decorators import dag
    from airflow.operators.python import PythonOperator
    import requests
    import json
    from confluent_kafka import Producer, Consumer, KafkaError
    import pendulum

    # 상수 정의
    KAFKA_TOPIC = 'test_topic'
    KAFKA_BROKER = 'localhost:9092'  # Docker 환경에 맞게 수정
    API_KEY = '1D6B63E8C3375FDCE46BD38620595819'  # 발급받은 Steam API 키
    SPECIFIED_USER_ID = 76561197960434622  # 지정된 Steam 사용자 ID

    # Kafka Producer 설정
    def create_kafka_producer():
        return Producer({'bootstrap.servers': KAFKA_BROKER})

    def get_steam_players_data(**context):
        all_players = []
        user_id = SPECIFIED_USER_ID  # 지정된 ID 사용

        # Steam API에서 사용자 정보 요청
        url = f'http://api.steampowered.com/ISteamUser/GetPlayerSummaries/v0002/?key={API_KEY}&steamids={user_id}'
        print(f"Requesting URL: {url}")  # 요청 URL 출력
        res = requests.get(url)
        
        if res.status_code != 200:
            print(f"Failed to fetch player data for {user_id}: {res.status_code}, Response: {res.text}")  # 오류 발생 시 출력
            return  # 오류 발생 시 종료
        
        data = res.json()
        players = data.get('response', {}).get('players', [])  # 플레이어 리스트 추출
        
        if not players:  # 플레이어가 없으면 종료
            print(f"No player found for {user_id}. Stopping.")
            return
        
        all_players.extend(players)  # 모든 플레이어 정보를 리스트에 추가
        print(f"Fetched player data for {user_id}: {players}")  # 성공적으로 가져온 데이터 출력

        context['task_instance'].xcom_push(key='players_data', value=json.dumps(all_players))  # JSON 문자열로 저장

    def send_players_to_kafka(data, **context):
        # Kafka Producer 생성
        producer = create_kafka_producer()
        
        players = json.loads(data)  # XCom에서 가져온 JSON 문자열을 파싱

        for player in players:
            key = player['steamid']  # steamid를 키로 사용
            value = json.dumps(player)  # 각 플레이어 정보를 JSON 문자열로 변환
            
            # Kafka로 메시지 전송
            try:
                producer.produce(KAFKA_TOPIC, key=key, value=value)
                print(f"Sent player data to Kafka: {value}")  # 전송 성공 시 출력
            except Exception as e:
                print(f"Failed to send message to Kafka: {e}")  # 전송 실패 시 출력

        # 전송 완료 후 대기
        producer.flush()

        # Kafka 전송 결과를 XCom에 저장 (예: 전송 성공 메시지)
        context['task_instance'].xcom_push(key='kafka_send_status', value='Players data sent to Kafka successfully')

    def process_and_send_to_kafka(**context):
        # XCom에서 플레이어 데이터 가져오기
        players_data = context['task_instance'].xcom_pull(key='players_data', task_ids='get_steam_players_task')

        # Kafka로 데이터 전송
        if players_data:
            send_players_to_kafka(players_data, **context)
        else:
            print("No player data found to send to Kafka.")

    local_tz = pendulum.timezone("Asia/Seoul")

    @dag(
        start_date=datetime(2024, 7, 25, tzinfo=local_tz),
        schedule='*/5 * * * *',  # 매 5분마다 실행
        catchup=False
    )
    def steam_usrinfo_dag():
        get_steam_players_task = PythonOperator(
            task_id='get_steam_players_task',
            python_callable=get_steam_players_data,
            provide_context=True
        )

        process_and_send_task = PythonOperator(
            task_id='process_and_send_task',
            python_callable=process_and_send_to_kafka,
            provide_context=True
        )

        get_steam_players_task >> process_and_send_task

    steam_usrinfo_dag()