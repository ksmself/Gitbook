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

* **float를 사용하면서 레이아웃이 붕괴**되기 때문에, 이를 방지하기 위해 **pseudo-element**를 활용한다. 

```css
.tab-menu-item::after{
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

* 기타 디자인적 요소들을 추가해주고, 무엇보다 부모에게 자식의 요소를 찾아주는 '**overflow: hidden**;'을 빼먹어서는 안된다.  

```css
  .tab-menu{
    list-style-type: none;
    padding-left: 0;
    overflow: hidden;
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

### 완성된 css 파

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
    overflow: hidden;
    max-width: 540px;
    border-bottom: 1px solid #E5EAEF;
  }
  .tab-menu-item{
    float: left;
  }
  .tab-menu-item::after{
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

## 

