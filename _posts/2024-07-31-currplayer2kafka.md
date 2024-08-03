---
title: steam 동접자 정보 to kafka
date: 2024-07-31 16:30:00 +0900
categories: [PipeLine]
tags: [pipeline]     # TAG names should always be lowercase
authors: [LoafingCat]
---



    from datetime import datetime
    from airflow.decorators import dag
    from airflow.operators.python import PythonOperator
    import requests
    import json
    from confluent_kafka import Producer
    import pendulum

    # 상수 정의
    KAFKA_TOPIC = 'topic_GetUserInfo'
    KAFKA_BROKER = '172.31.2.88:9092'  # Docker 환경에 맞게 수정

    # 게임의 Steam 앱 ID
    GAMES = {
        '몬스터 헌터 월드': '582010',
        '엘든 링': '1245620',
        '팰월드': '1801980'
    }

    # Kafka Producer 설정
    def create_kafka_producer():
        return Producer({
            'bootstrap.servers': KAFKA_BROKER
        })

    def get_current_players(game_id):
        url = f'http://api.steampowered.com/ISteamUserStats/GetNumberOfCurrentPlayers/v1/?appid={game_id}'
        res = requests.get(url)

        if res.status_code == 200:
            data = res.json()
            return data.get('response', {}).get('player_count', 0)
        return 0

    def get_steam_players_data(**context):
        producer = create_kafka_producer()

        for game_name, game_id in GAMES.items():
            player_count = get_current_players(game_id)
            key = game_name  # 게임 이름을 키로 사용
            value = json.dumps({'game': game_name, 'player_count': player_count})  # 게임 이름과 플레이어 수를 JSON으로 변환
            
            # Kafka로 메시지 전송
            try:
                producer.produce(KAFKA_TOPIC, key=key, value=value)
            except Exception as e:
                print(f"Kafka 전송 실패: {e}")  # 에러 출력

        # 전송 완료 후 대기
        producer.flush()

    local_tz = pendulum.timezone("Asia/Seoul")

    @dag(
        start_date=datetime(2024, 7, 30, tzinfo=local_tz),
        schedule='* * * * *',  # 매 분마다 실행
        catchup=False
    )
    def steam_current_player_dag():
        get_current_player_task = PythonOperator(
            task_id='get_current_player_task',
            python_callable=get_steam_players_data,
            # provide_context=True,  # Airflow 2.0 이상에서는 생략 가능
        )

        get_current_player_task  # DAG에 작업 추가

    # DAG 정의
    dag_instance = steam_current_player_dag()


usrinfo 추가예정