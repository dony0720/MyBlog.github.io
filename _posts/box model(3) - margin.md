# margin 속성

**`margin`에 대해서** 

1. **`margin`**은 **`border`**(테두리)와 이웃하는 요소 사이의 간격인 마진 영역의 크기를 결정한다 

2. **`margin`** 은 **`padding`** 과 달리 **`background-color`** 속성으로 설정하는 배경색의 영향을 받지 않는다 

3. **`css`** 를 사용해 **`margin`** 영역의 크기를 방향별로 지정할 수 있다. 

4. **`css`** 에서 제공하는 **`margin`** 속성은 다음과 같습니다. 

    1) **`margin-top`** 
    
    2) **`margin-right`**
    
    3) **`margin-bottom`** 
    
    4) **`margin-left`** 
      
5.  **`margin`** 의 값을 음수로 지정해 해당 요소를 다른 요소의 위에 겹치게 할 수 있습니다. 


```python
<style>
    .none{
        background-color: aqua;
    }

        
    .margin{
        background-color: red;
        margin-top: -5px;
        margin-left: 30px;
    }
</style>

<body>
    <div class="none">margin 속성 적용하지 않음</div>
    <div class="margin">margin 속성 적용</div>
</body>
```

**위에 코드를 실행하게 되면 `class=margin`에 `margin-top:-5px`을 할당해서 서로 겹치는걸 볼 수 있다** 


```python
<style>
    .none{
        background-color: aqua;
        height: 100px;
        width: 500px;
    }

    .margin{
        background-color: red;
        margin-top: -5px;
        margin-left: 30px;
        height: 100px;
        width: 500px;
    }

    .margin-inherit{
        background-color: beige;
        width: 50px;;
        margin-left: inherit;
    }
</style>

<body>
    <div class="none">margin 속성 적용하지 않음</div>
    <div class="margin">margin 속성 적용
        <div class="margin-inherit">inherit 속성 적용</div>
    </div>
</body>
```

**`class= margin-inherit`에 `inherit` 속성을 적용해 부모인 `class=margin`의 margin-left 속성을 물려받는다.**   

# margin의 개별 설정 

## 속성이 4개일때 


```python
<style>
    .margin{
        margin: 10px 20px 30px 40px
    }
</style>

<body>
    <div class="margin">margin 개별 설정</div>
</body>
```

**위 코드의 적용순서와 의미는 다음과 같다** 

1. margin-top: 10px

2. margin-right: 20px 

3. margin-bottom: 30px 

4. margint-left: 40px 

## 속성이 3개일때 


```python
<style>
    .margin{
        margin: 10px 20px 30px
    }
</style>

<body>
    <div class="margin">margin 개별 설정</div>
</body>
```

**위 코드의 적용순서와 의미는 다음과 같다** 

1. margin-top: 10px

2. margin-right: 20px 

3. margin-bottom: 30px 

4. margint-left: 20px 

## 속성이 2개일때 


```python
<style>
    .margin{
        margin: 10px 20px 
    }
</style>

<body>
    <div class="margin">margin 개별 설정</div>
</body>
```

**위 코드의 적용순서와 의미는 다음과 같다** 

1. margin-top: 10px

2. margin-right: 20px 

3. margin-bottom: 10px 

4. margint-left: 20px 

# margin: auto 

1. **`margin`** 에 **`auto`** 를 설정하게되면 웹 브라우저가 수평 방향 **`margin`** 값을 자돋으로 설정한다. 

2. 즉 HTML 요소의 왼쪽과 오른쪽 마진을 자동으로 설정해준다 

3. 해당 요소를 포함하는 부모 요소의 왼쪽과 오른쪽 마진을 자동으로 설정해준다.  


```python
<style>
    .margin{
        background-color: red;
        margin: auto;
        height: 100px;
        width: 500px;
    }

    .margin-inherit{
        background-color: beige;
        width: 200px;;
        height: 30px;
        margin: auto;
    }
</style>


<body>
    <div class="margin">margin 속성 적용
        <div class="margin-inherit">inherit 속성 적용</div>
    </div>
</body>
```

1. 위 코드 실행결과 `class = margin`은 부모가 `body`고 `class = margin-inherit`은 부모가 `margin` 이다. 

2. `class= margin`은 수평으로 왼쪽과 오른쪽 값이 같아 부모인 `body`의 정중앙에 위치한다. 

3. `class = margin-inherit`은 부모인 `class = margin`의 정중앙에 위치한다.

# outline

1. **`outline`** 속성은 **`HTML`** 요소의 가장 바깥 부분을 둘러싸고 있는 부분을 설정합니다. 

2. **`outline`** 속성은 **`border`** 와 달리 요소 전체의 크기에는 포함되지 않는다.  

3. **`outline`** 속성은 **`border`** 속성과 같이 **`style`,`width`, `color`** 속성을 가진다. 


```python
<style>

    .dotted {
        border: solid;
        outline: dotted 5px red;
        margin: 20px;
    }

    .dashed {
        border: solid;
        outline: dashed 5px red;
        margin: 20px;
    }

    .solid {
        border: solid;
        outline: solid 5px red;
        margin: 20px;
    }

    .double {
        border: solid ;
        outline: double 5px red;
        margin: 20px;
    }

    .groove {
        border: solid ;
        outline: groove 5px red;
        margin: 20px;
    }

    .ridge {
        border: solid ;
        outline: ridge 5px red;
        margin: 20px;
    }

    .inset {
        border: solid ;
        outline: inset 5px red;
        margin: 20px;
    }

    .outset {
        border: solid ;
        outline: outset 5px red;
        margin: 20px;
    }

    .none {
        border: solid ;
        outline: none 5px red;
        margin: 20px;
    }

    .hidden {
        border: solid ;
        outline: hidden 5px red;
        margin: 20px;
    }
    
</style>


<body>
    
    <div class="dotted"> outline: dotted</div>
    
    <div class="dashed"> outline: dashed</div>
    
    <div class="solid"> outline: solid</div>
    
    <div class="double"> outline: double</div>
    
    <div class="groove"> outline: groove</div>
    
    <div class="ridge"> outline: ridge</div>
    
    <div class="inset"> outline: inset</div>
    
    <div class="outset"> outline: outset</div>
    
    <div class="none"> outline: none</div>
    
    <div class="hidden"> outline: hidden</div>
        
</body>
```

# 사진 
