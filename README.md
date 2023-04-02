# momentum 

과제를  수행하면서, 기억해야할 key points. 

### 목차 
* [배경이미지 변경](#chapter-1)
* [실시간 시계](#chapter-2)
* [인사](#chapter-3)
* [todo 목록 추가하기](#chapter-4)
* [weather API 사용하기](#chapter-4)

<br><br>

## <a id="chapter-1">배경이미지 변경</a>

배열에 있는 값을 랜덤으로 가져오기 = 배열이름[Math.floor(Math.random() * 배열길이)]

## <a id="chapter-2">실시간 시계</a>

```
const time = new Date();
const hour = String(time.getHours()).padStart(2, "0");
```
시간을 가져온다음, string으로 바꾸고, padStart로 표현하기 

## <a id="chapter-3">인사</a>

새로 고침해도, 값이 저장되도록 하려면, localStorage를 사용해야함. 

localStorage.setItem("key", name);
key라는 이름으로 name값을 저장하기. 

localStorage.getItem("key");
: 값 꺼내오기. 


## <a id="chapter-4">todo 목록 추가하기</a>
새로 고침해도, 값이 저장되도록 하려면, localStorage를 사용해야 하는데, 배열로 저장하고 싶을 때! JSON사용!

```
localStorage.setItem("todo", JSON.stringify(toDos));
const savedToDos = localStorage.getItem("todo");

const parsedToDos = JSON.parse(savedToDos); //배열로 꺼내기!
```


## <a id="chapter5">weather api사용하기</a>

https://api.openweathermap.org 에 있는 API 사용하기

```
const API_KEY = "44e31e73aec402baf02f60ad8b75e464"
function onGeo(position){

  const lat = position.coords.latitude;
  const lon = position.coords.longitude;
  const url = `https://api.openweathermap.org/data/2.5/weather?lat=${lat}&lon=${lon}&appid=${API_KEY}&units=metric`;
 
  //fetch함수는 url을 브라우저가 대신 불러와주는 것. 
  fetch(url).then(Response => Response.json().then(data => {
    const weather = document.querySelector("#weather span:first-child");
    const city = document.querySelector("#weather span:last-child");
    city.innerText = data.name;
    weather.innerText = `${Math.floor(data.main.temp)}°C ${data.weather[0].main}`;
  }))
}

function onGeoError(){
  alert("can't find");
}

navigator.geolocation.getCurrentPosition(onGeo, onGeoError);
//navigator.geolocation.getCurrentPosition 라는 함수는 두개의 인자를 필수로 받음, 성공했을때와 실패했을때 
```
