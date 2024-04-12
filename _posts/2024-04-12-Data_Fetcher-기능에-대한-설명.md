---
title: Data_Fetcher-기능에-대한-설명
date: 2024-04-12 16:30:00 +0900
categories: [Information]
tags: [information]     # TAG names should always be lowercase
authors: [LoafingCat]
---


# 전체코드

        # data_fetcher.py
        import requests

        class DataFetcher:
            def __init__(self, api_key, city):

                self.api_key = api_key
                self.city = city

            def fetch_weather(self):
                url = f'https://api.openweathermap.org/data/2.5/weather?q={self.city}&appid={self.api_key}'
                response = requests.get(url)

                if response.status_code == 200:
                    print(f"{self.city}의 날씨 정보를 성공적으로 가져왔습니다.")
                    return response.json()
        
                else:
                    print(f"날씨 데이터를 가져오는데 문제가 발생했습니다. 상태 코드: {response.status_code}")

# 설명

- import requests로 HTTP 요청을 보내고 받기 위해 **requests 모듈**을 가져옵니다. 

- __init__에 두 개의 인자(api_key, city)를 받습니다. 
**api_key**는 OpenWeatherMap API의 API 키이고, **city**는 날씨 정보를 가져올 도시입니다.

- self.api_key = api_key와 self.city = city:

    이 코드는 생성자 메서드 내부에서 api_key와 city를 인스턴스 변수로 설정합니다. 이렇게 해야 클래스 내의 다른 메서드에서 이 값을 사용할 수 있습니다.

- fetch_weather(self)는 OpenWeatherMap API를 사용하여 날씨 정보를 가져오는 역할을 합니다.

- url 부분은 API 요청을 보낼 URL을 생성하는 부분입니다. OpenWeatherMap API의 형식에 맞춰진 것으로, 도시와 API 키를 포함합니다.

- response = requests.get(url) 부분에서 requests 모듈을 사용해서 생성된 URL에 HTTP GET 요청을 보내어 OpenWeatherMap API의 날씨 정보를 받아옵니다.

- if response.status_code == 200은 HTTP 상태 코드가 200(성공)인지 확인하는 부분입니다.

- 이후 성공하면 성공 메시지를 출력하고, 만약 실패한 경우 실패한 상태 코드를 출력합니다.

