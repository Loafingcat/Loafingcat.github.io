---
title: PeriodicWeatherFetcher의 기능 설명
date: 2024-04-12 16:30:00 +0900
categories: [Information]
tags: [information]     # TAG names should always be lowercase
authors: [LoafingCat]
---

# 전체 코드

    import time
    from data_fetch import DataFetcher

    class PeriodicWeatherFetcher:
        def __init__(self, api_key, city, duration_h):
            self.api_key = api_key
            self.city = city
            self.duration_h = duration_h
            self.fetcher = DataFetcher(api_key, city)

        def process(self):
            end_time = time.time() + self.duration_h
            weather_dict = {'city': self.city, 'temp': []}
        
            while time.time() < end_time:
                weather_data = self.fetcher.fetch_weather()
                if weather_data:
                    temperature = weather_data.get('main', {}).get('temp')
                    if temperature:
                        weather_dict['temp'].append(temperature)
                        print(f"현재 온도: {temperature}")
                    else:
                        print("날씨 데이터를 가져오는데 실패했습니다.")
                else:
                    print("날씨 데이터를 가져오는데 실패했습니다.")
                time.sleep(10)
            
            # print(weather_dict)
            return weather_dict


일정 시간마다 주기적으로 날씨 데이터를 가져와서 딕셔너리에 저장하는 역할을 합니다. 각 도시별로 온도 데이터를 리스트에 저장하고, 딕셔너리 형태로 변환합니다.

각 반복에서 fetcher 객체의 fetch_weather 메서드를 호출해서 날씨 데이터를 가져옵니다. 가져온 데이터가 있으면 온도를 추출해서 weather_dict 딕셔너리의 temp에 키에 추가합니다.

반복문이 종료된 후에는 weather_dict를 반환합니다.