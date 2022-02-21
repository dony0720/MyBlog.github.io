```python
<input id="night_day" type="button" value="night" onclick="
    var target = document.querySelector('body');
    if(this.value === 'night'){
      target.style.backgroundColor = 'black';
      target.style.color = 'white';
      this.value = 'day'; 

      var alist = document.querySelectorAll('a');
      var i = 0;
      while(i < alist.length){
        alist[i].style.color = 'powderblue';
        i = i + 1;
```

document.querySelector('a')는 a 태그를 한개만 가져온다. <br>
document.querySelectorAll('a') 를 사용해 a 태그 전체를 가져온다 ex) [a,a,a,a] <br>
<br>
alilst[0] = a href="index.html" <br>
alist[1] = a href="1.html"<br>
alist[2] = a href="2.html"<br>
alist[3] = a href="3.html"<br>
<br>
이렇게 반복문을 사용해 각각의 a 태그에 color를 바꿀 수 있다. 


```python
function nightDayHandler(self){
    var target = document.querySelector('body');
    if(self.value === 'night'){
      target.style.backgroundColor = 'black';
      target.style.color = 'white';
      self.value = 'day';
      var alist = document.querySelectorAll('a');
      var i = 0;
      while(i < alist.length){
        alist[i].style.color = 'powderblue';
        i = i + 1;
      }
    } else {
      target.style.backgroundColor = 'white';
      target.style.color = 'black';
      self.value = 'night';
      var alist = document.querySelectorAll('a');
      var i = 0;
      while(i < alist.length){
        alist[i].style.color = 'blue';
        i = i + 1;
      }
    }
  }
```

독립된 함수를 만들때<br>
<br>
this를 사용하게 되면 전역개체를 가르키게 되어 동작이 되지 않음 <br>
this를 대신 self라는(아무거나 상관없음) 매개변수를 사용<br>
함수를 호출할때는 nightDayHandler(this) 작성하면 된다 
