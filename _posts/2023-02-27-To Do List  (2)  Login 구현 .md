---
layout: single
title: To Do List (2) - Login 기능 구현
---
# login 기능 구현 

## 소스코드 

### JavaScript


```python
const login_form = document.querySelector("#login_form");
const login_input = document.querySelector("#login_form #name");
const login_button = document.querySelector("#login_form #submit");
const greeting = document.querySelector("#greeting");
const hidden = "hidden"

function onLogin(event){
    event.preventDefault();
    const username = login_input.value;
    login_form.classList.add(hidden);
    localStorage.setItem("username", username)
    paintGreetings(username)
}

function paintGreetings(username) {
    greeting.innerText = `Hello ${username}`;
    greeting.classList.remove(hidden);
  }

const savedUsername = localStorage.getItem("username");

if (savedUsername === null) {
    login_form.classList.remove(hidden);
    login_form.addEventListener("submit", onLogin);
} else {
  paintGreetings(savedUsername);
}
```

### style.css


```python
.hidden {
    display: none;
}
```


```python
const login_form = document.querySelector("#login_form");
const login_input = document.querySelector("#login_form #name");
const login_button = document.querySelector("#login_form #submit");
const greeting = document.querySelector("#greeting");
```

1. **document는 js가 html에 접근하기 위해서 사용되어짐**

2. **HTML 요소의 선택은 다음과 같습니다**

    1) **document.getElementsByTagName(태그이름):** <br>
       -> 해당 태그 이름의 요소를 모두 선택함.

    2) **document.getElementById(아이디):** <br>
        -> 해당 아이디의 요소를 선택함.

    3) **document.getElementsByClassName(클래스이름):** <br>
        -> 해당 클래스에 속한 요소를 모두 선택함.

    4) **document.getElementsByName(name속성값):** <br>
       -> 해당 name 속성값을 가지는 요소를 모두 선택함..

    5) **document.querySelectorAll(선택자):** <br>
       -> 해당 선택자로 선택되는 요소를 모두 선택함.

## onLogin 함수 


```python
function onLogin(event){
    event.preventDefault();
    const username = login_input.value;
    login_form.classList.add(hidden);
    localStorage.setItem("username", username);
    paintGreetings(username);
}
```

1. **event.preventDefault()**
   login_input.value의 값을 가져오기 위해서 <br>
   **form태그의 자동으로 submit되고 페이지를 재시작하는 event의 기본동작을 막는다** <br>   
  
2. login 되었을때 login_form 부분은 보이지 않게 하기위해 **classList를 사용해** <br>
   기존 클래스명을 유지한채 'hidden' 클래스명을 추가

3. input에 넣은 값을 저장하기위해 localStorage.setItem("username", username)을   
   사용함 개발자 도구에서 Application 메뉴로 이동해 Local Storage 항목을 선택해   
   확인할 수 있다. 

## paintGreetings 함수 


```python
function paintGreetings(username) {
    greeting.innerText = `Hello ${username}`;
    greeting.classList.remove(hidden);
}
```

1. **innerText를 사용해** id 값이 greeting인 h1 태그 안에 **`Hello ${username}`를 출력** 

<br>
<br>

```python
const savedUsername = localStorage.getItem("username");

if (savedUsername === null) {
    login_form.classList.remove(hidden);
    login_form.addEventListener("submit", onLogin);
} else {
  paintGreetings(savedUsername);
}
```

1. Local Storage에 저장된 username의 값이 없다면 login 부분의 class ="hidden"을 한다.

2. **login_form.addEventListener("submit", onLogin)** <br>
    1) login_form에서 submit 이벤트를 감지할때 onLogin 함수를 실행  
