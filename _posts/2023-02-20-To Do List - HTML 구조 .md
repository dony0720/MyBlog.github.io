---
layout: single
title: HTML정리!!
---

#  HTML구조 잡기 

## login 


```python
<div class="login">
    <form class="login_form">
    <input id="name" type="text" placeholder="이름을 적어주세요">
    <input id="submit" type="submit" value="login">
    </form>
    <h1 class="greeting" id="hidden"></h1>
    
    <div class="music">
    <div class="music-option">music</div>
    <div class="music-controll">
        <button class="music-btn on">On</button>
        <button class="music-btn pause">Pause</button>
        <button class="music-btn off">Off</button>
    </div>
    </div>
    <div class="volume">
        <div>volume</div>
        <input class="volume-controll" type="range" step="0.1"
            min="1" max="10" value="0.5">
    </div>
    <div class="backGround">
        <button class="changeBackgroud">배경바꾸기</button>
    </div>
</div>
```

### login_form 부분 

<p style = font-weight:bold> input의 유효성을 검사하기 위해서 form 태그를 사용 </p>

## clock


```python
 <div class="clock">
    <span id="day"></span>
    <span id="time"></span>
    <span id="weather"></span>
</div>
```

## calendar


```python
<div class="calendar">
    <div class="header">
    <div class="year-month"></div>
    <div class="nav">
        <button class="nav-btn go-pre">&lt;</button>
        <button class="nav-btn go-today">Today</button>
        <button class="nav-btn go-next">&gt;</button>
    </div>
</div>
    <div class="main">
        <div class="days">
            <div class="day">일</div>
            <div class="day">월</div>
            <div class="day">화</div>
            <div class="day">수</div>
            <div class="day">목</div>
            <div class="day">금</div>
            <div class="day">토</div>
        </div>
    </div>
    <div class="dates"></div>
</div>
```

### dates 부분 
<p style = font-weight:bold> js로 날짜를 대입하기 위해서 만들어 둠 </p>
