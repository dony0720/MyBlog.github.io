---
layout: single
title: JavaScript 정리(1)~
---
```python
<h1><a href="index.html">WEB</a></h1>
  <input id="night_day" type="button" value="night" onclick="
    var target = document.querySelector('body');
    if(this.value === 'night'){
      target.style.backgroundColor = 'black';
      target.style.color = 'white';
      this.value = 'day';
    } else {
      target.style.backgroundColor = 'white';
      target.style.color = 'black';
      this.value = 'night';
    }
  ">
```

input type ="button" value = "night"- input type ="button"으로 푸쉬 버튼을 생성하고<br>
value에 값을 지정해주어 버튼안에 night이 쓰여있는걸 볼 수 있다<br>
onclick = "" - click 했을때 아래의 코드가 실행 

```python
 if(this.value === 'night'){
      target.style.backgroundColor = 'black';
      target.style.color = 'white';
      this.value = 'day';
    } else {
      target.style.backgroundColor = 'white';
      target.style.color = 'black';
      this.value = 'night';
```

value = night인 버튼이 눌러졌을때<br>
background가 black, 문단 글씨가 white, 버튼의 value가 day로 바뀐다 <br>
<br>
value = day인 버튼이 눌러졌을때<br>
background가 white, 문단 글씨가 black, 버튼의 value가 night로 바뀐다 <br>
<br>
var target = document.querySelector('body') - body 태그를 선택하는 코드를 target에 선언 <br>
target.style = 'black' - body 태그에 속성을 설정한다.ed<br>
target.style.backgroundColor = 'black'- 배경을 black으로 지정 <br>
target.style.color = 'white' - 글씨 색을 white로 지정 
