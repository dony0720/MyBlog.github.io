---
layout: single
title: To Do List (5) - 날씨 정보 가져오기 
---
# API를 이용해 날씨 정보 가져오기 

## 소스코드 


```python
const weather = document.querySelector("#weather");
const API_KEY = "4dd7add724570dbc3c2270897dd5257b";

function onGeoOk(position) {
    const lat = position.coords.latitude;
    const lon = position.coords.longitude;
    const url = `https://api.openweathermap.org/data/2.5/weather?lat=${lat}&lon=${lon}&appid=${API_KEY}&units=metric`;
    fetch(url)
        .then((response) => response.json())
        .then((data) => {
            weather.innerText = `${data.name} / ${data.weather[0].main} / ${data.main.temp} `;
        });
}

function onGeoError() {
    alert("Can't find you. No weather for you.");
}
navigator.geolocation.getCurrentPosition(onGeoOk, onGeoError);
// 장치의 현재 위치를 가져옴, 위치를 얻는데 성공지 onGeok 실행 실패시 onGeoError 실행  
```

1. **`navigator.geolocation.getCurrentPosition(onGeoOk, onGeoError);`** 

     1) 장치의 현재 위치를 가져오게 됩니다 

     2) 위치를 얻는데 성공하면 onGeok()함수를 실행하고 실패시 onGeoError() 함수를 실행 

## API 이용 

1. google에 openWeather -> API -> Current weather data에 접속

2. 로그인 진행 후 영문이름을 클릭하게 되면 MY API KEYS를 통해서 Key값을 확인 

## onGeoOk 함수 

1. onGeoOk() 함수의 인자는 GeolocationPosition 객체를 가져온다 

2. GeolocationPosition 객체의 position.coords 부분을 보게 되면 위도와 경도를 확인할 수 있다 

3. API 호출 예시를 보게 되면 https://api.openweathermap.org/data/2.5/weather?lat=${lat}&lon=${lon}&appid=${API_KEY} 되어 있다 

4. &units=metric 부분을 추가하게 되면 섭씨로된 온도를 확인할 수 있다 

## onGeoError 함수 

1. 장치의 현재 위치를 가져오는데 실패시 onGeoError 함수 실행 

2. Can't find you. No weather for you. 라는 메시지의 경고창이 뜸 
