# Css 훈련

## CSS 초보를 위한 꿀팁

* 노트를 준비한다.
* 현재 상태와 만들어야 할 디자인 시안을 비교한다.
* 현 상태와 디자인 시안의 차이점을 찾아 체크리스트로 작성한다. 
* 작성한 체크리스트를 하나하나 해결한다. 

## float 1

![&#xB514;&#xC790;&#xC778; &#xC2DC;&#xC548;.](../.gitbook/assets/479.png)

![&#xD604;&#xC7AC; &#xC0C1;&#xD0DC;.](../.gitbook/assets/480.png)

현재 상태에서 디자인 시안으로 가기 위해서는 여러 가지 변화가 필요해보인다. 

* 리스트 옆에 붙어 있는 도트와 공백을 제거하고, 저들을 가로로 배치해야 할 것이다. 

```css
.tab-menu{
    list-style-type: none;
    padding-left: 0;
 }
.tab-menu-item{
    float: left;
 }
```

* **float를 사용하면서 레이아웃이 붕괴**되기 때문에, 이를 방지하기 위해 **pseudo-element**를 활용한다. \(float로 인한 레이아웃 붕괴 문제를 해결하는 여러 방법이 있지만, overflow:hidden;을 부모에게 적용하듯 **pseudo-element**도 마찬가지로 **부모에게 적용**!!!\)

```css
.tab-menu::after{
    content: ' ';
    display: block;
    clear: left;
  }
```

* tab-menu-item의 텍스트만이 아니라 **여백을 클릭하더라도 이동 가능하도록** tab-menu-item **a에 padding을 준다**. **anchor는 inline**이라 padding 등이 적용 불가하므로 **display는 block 또는 inline-block으로 변경**해준다. tab-menu-item 사이의 간격이 16px인 것도 적용해준다. 

```css
  .tab-menu-item a{
    padding: 16px 20px;
    display: inline-block;
    margin-right: 16px;
  }
```

* 기타 디자인적 요소들을 추가해준다.

```css
  .tab-menu{
    list-style-type: none;
    padding-left: 0;
    max-width: 540px;
    border-bottom: 1px solid #E5EAEF;
  }
  .tab-menu-item.selected a{
    color: #2860E1;
    /* font-weight이 medium이므로 */
    font-weight: 500;
    border-bottom: 2px solid #2860E1;
  }
```

### 완성된 html 파일

```markup
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Float 1</title>
    <link href="https://fonts.googleapis.com/css?family=Roboto:400,500&display=swap" rel="stylesheet" />
    <link rel="stylesheet" href="./p-style.css" />
  </head>
  <body>
    <ul class="tab-menu">
      <li class="tab-menu-item">
        <a href="#">Summary</a>
      </li>
      <li class="tab-menu-item selected">
        <a href="#">Emails</a>
      </li>
      <li class="tab-menu-item">
        <a href="#">Files</a>
      </li>
      <li class="tab-menu-item">
        <a href="#">Mentions</a>
      </li>
    </ul>
  </body>
</html>
```

### 완성된 css 파일

```css
* {
    box-sizing: border-box;
    margin: 0;
  }
  
  body {
    font-family: "Roboto", sans-serif;
    letter-spacing: -0.02em;
  }
  
  a {
    font-size: 18px;
    line-height: 20px;
    color: #8492a6;
    text-decoration: none;
  }
  
  /* ▼ WHERE YOUR CODE BEGINS */
  .tab-menu{
    list-style-type: none;
    padding-left: 0;
    max-width: 540px;
    border-bottom: 1px solid #E5EAEF;
  }
  .tab-menu-item{
    float: left;
  }
  .tab-menu::after{
      content: ' ';
      display: block;
      clear: left;
  }
  .tab-menu-item a{
    padding: 16px 20px;
    display: inline-block;
    margin-right: 16px;
  }
  .tab-menu-item.selected a{
    color: #2860E1;
    /* font-weight이 medium이므로 */
    font-weight: 500;
    border-bottom: 2px solid #2860E1;
  }
```

## float 2 

![&#xB514;&#xC790;&#xC778; &#xC2DC;&#xC548;.](../.gitbook/assets/482.png)

![&#xD604;&#xC7AC; &#xC0C1;&#xD0DC;. ](../.gitbook/assets/483.png)

* 우선, 이미지의 모양을 둥글게 하고, width와 height 값을 조정해야 한다. 

```css
  .card-user{
    width: 44px;
    height: 44px;
    border-radius: 50%;
  }
```

* card-content 사이의 여백을 위해 h1과 strong에 margin-bottom을 주었다. 그런데, strong의 margin-bottom은 적용되지 않아 왜 그런가 봤더니 display가 inline이었다. 그래서 display를 block으로 변경해주었다. \*margin을 줄 때는 한 방향으로 통일하는 것이 좋음. 

```css
  .card-content h1{
    margin-bottom: 4px;
  }
  .card-content strong{
    margin-bottom: 12px;
    display: block;
  }
```

* 이제는 가로배치를 해야한다. card-user와 card-content 모두 float: left; 시키고, 둘 사이의 여백을 위해 margin-right을 사용하였다. 

```css
  .card-user{
    width: 44px;
    height: 44px;
    border-radius: 50%;
    margin-right: 20px;
  }
  .card-user,
  .card-content{
    float: left;
  }
```

* 레이아웃 붕괴를 위해 pseudo-element를 활용하지만, 이 속성이 한 번만 사용되지 않을 수 있기 때문에 clearfix라는 class를 만들어 clear: both;로 하고 언제든 사용할 수 있도록 했다. 또한, card 전부분에 필요한 padding을 주었다.  

```css
  .clearfix::after{
    content:'';
    display: block;
    clear: both;
  }
  .card{
    padding: 20px;
  }
```

### 완성된 html 파일

```markup
<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Float 2</title>
    <link href="https://fonts.googleapis.com/css?family=Noto+Sans+KR&display=swap" rel="stylesheet" />
    <link rel="stylesheet" href="./style.css" />
  </head>
  <body>
    <div class="card clearfix">
      <img src="./assets/user.jpg" alt="Customer support" class="card-user" />
      <div class="card-content">
        <h1>RE: 안녕하세요 배송 관련 문의드립니다</h1>
        <strong>
          customer support
        </strong>
        <p>
          안녕하세요 우현님. 문의 드린 사항에 대한 답변드립니다. 지난 12...
        </p>
      </div>
    </div>
  </body>
</html>
```

### 완성된 css 파일

```css
* {
    box-sizing: border-box;
    margin: 0;
  }
  
  body {
    font-family: "Noto Sans KR", sans-serif;
    letter-spacing: -0.02em;
  }
  
  h1 {
    font-size: 16px;
    font-weight: 400;
    color: #1f2d3d;
    line-height: 1.25;
  }
  
  strong {
    font-size: 14px;
    font-weight: 400;
    color: #afb3b9;
    line-height: 1.4285714286;
  }
  
  p {
    font-size: 16px;
    color: #79818b;
    line-height: 1.5;
  }
  
  /* ▼ WHERE YOUR CODE BEGINS */
  .clearfix::after{
    content:'';
    display: block;
    clear: both;
  }
  .card{
    padding: 20px;
  }
  .card-user{
    width: 44px;
    height: 44px;
    border-radius: 50%;
    margin-right: 20px;
  }
  .card-content h1{
    margin-bottom: 4px;
  }
  .card-content strong{
    margin-bottom: 12px;
    display: block;
  }
  .card-user,
  .card-content{
    float: left;
  }
```

## position 1 

![&#xB514;&#xC790;&#xC778; &#xC2DC;&#xC548;. ](../.gitbook/assets/485.png)

![&#xD604;&#xC7AC; &#xC0C1;&#xD0DC;.](../.gitbook/assets/486.png)

* 프로필 이미지와 user name을 담고 있는 user-card의 속성부터 정리한다. 

```css
  .user-card{
    width: 240px;
    height: 56px;
    background-color: #ffffff;
    border: 1px solid #E5EAEF;
    border-radius: 4px;
  }
```

* 이미지의 사이즈와 border-radius를 조정한다. 이때, 이미지는 **user-photo의 img**이므로 아래의 코드와 같이 표현한다. 

```css
  .user-photo img{
    display: block;
    width: 40px;
    height: 40px;
    border-radius: 50%;
  }
```

* 이미지와 user name의 가로 배치가 필요해보인다.  

```css
  .user-card::after{
    content: '';
    display: block;
    clear: left;
  }
  .user-photo,
  .user-name{
    float: left;
  }
```

* user-photo에 padding을 적용한다. 

```css
  .user-photo{
    padding: 8px 12px;
  }
```

* user-name도 수직으로 가운데 정렬을 위해 padding을 적용한다. 

```css
  .user-name{
    padding: 16px 0;
  }
```

* 마지막으로 초록 동그라미를 만들어낸다. 초록 동그라미는 원래 위치에서 완전히 떼내어, 원래의 맥락에서 완전히 벗어나서 위치를 옮겨야 하므로 position: aboslute;를 사용한다. 자연히 부모 요소는 relative가 되어야 하므로 user-photo의 position을 relative로 바꿔준다.

```css
  .user-status{
    position: absolute;
    right: 10px;
    bottom: 6px;
    display: block;
    box-sizing: content-box;
    width: 8px;
    height: 8px;
    border-radius: 50%;
    border: 2px solid #FFFFFF;
    background-color:#21D891;
  }
```

### 완성된 html 파일

```markup
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Position 1</title>
    <link href="https://fonts.googleapis.com/css?family=Lato&display=swap" rel="stylesheet" />
    <link rel="stylesheet" href="./style.css" />
  </head>
  <body>
    <div class="user-card">
      <div class="user-photo">
        <img src="./assets/user.jpg" alt="Kimbug" />
        <span class="user-status" aria-label="Active"></span>
      </div>
      <h1 class="user-name">
        Kimbug
      </h1>
    </div>
  </body>
</html>
```

### 완성된 css 파일

```css
* {
    box-sizing: border-box;
    margin: 0;
  }
  
  body {
    font-family: "Lato", sans-serif;
  }
  
  h1 {
    font-size: 16px;
    font-weight: 400;
    line-height: 1.5;
    color: #273444;
  }
  
  /* ▼ WHERE YOUR CODE BEGINS */
  .user-card{
    width: 240px;
    height: 56px;
    background-color: #ffffff;
    border: 1px solid #E5EAEF;
    border-radius: 4px;
  }
  .user-card::after{
    content: '';
    display: block;
    clear: left;
  }
  .user-photo,
  .user-name{
    float: left;
  }
  .user-photo{
    position: relative;
    padding: 8px 12px;
  }
  .user-photo img{
    display: block;
    width: 40px;
    height: 40px;
    border-radius: 50%;
  }
  .user-name{
    padding: 16px 0;
  }
  .user-status{
    position: absolute;
    right: 10px;
    bottom: 6px;
    display: block;
    box-sizing: content-box;
    width: 8px;
    height: 8px;
    border-radius: 50%;
    border: 2px solid #FFFFFF;
    background-color:#21D891;
  }
```

## 

