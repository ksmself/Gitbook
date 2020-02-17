---
description: 개념을 제대로 숙지하고 있는지 스스로 체크하기 위한 훈련
---

# Css

## HTML+CSS의 기본

아래와 같은 페이지를 만들려면 어떻게 해야할까?

![&#xD3EC;&#xC778;&#xD2B8;&#xB294; &#xB808;&#xC774;&#xC544;&#xC6C3;!](.gitbook/assets/368.png)

html 파일

```markup
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Kiwi</title>
  <link rel="stylesheet" href="kiwi.css">
</head>
<body>
  <div>
    <img src="images/kiwi.png">
    <h1>
      Kiwi
    </h1>
    <ul>
      <li>
        Orange
      </li>
      <li>
        Kiwi
      </li>
      <li>
        Strawberry
      </li>
    </ul>
  </div>
</body>
</html>
```

css 파일

```css
body{
  /* url() 주의 */
  background-image: url(images/kiwi-bg.jpg);
}

div{
  background-color: white;
  width:400px;
  
  /* padding은 내부에 생기는 공간, 총 가로 길이는 500이 된다 */
  padding: 30px 50px;

  /* 좌우가 auto라는 뜻은 화면 크기를 조정함에 따라 자동으로 조절됨을 의미 */
  margin: 30px auto 50px;
  border: 16px solid green;
  border-radius: 50px;
}

h1{
  color:green;
  border-bottom: 5px solid green;
  background-color: antiquewhite;
  /* width 먼저 정한 후 margin 조*/
  width: 69px;
  margin: 30px auto;

}

ul{
  background-color: antiquewhite;
  /* width를 먼저 정한 후, margin, padding 조절 */
  width: 100px;
  margin: 30px auto;
  padding-top: 30px;
  padding-bottom: 30px;
}

```

## position

### static과 relative

static과 relative는 함께 간다고 생각하면 된다. relative는 원래 static일 때 위치에서 설정한 값을 기준으로 이동하면 되는 것이고, static은 앞에 relative가 있다면 relative가 원래 있었어야 할 자리 다음 위치로 가게 된다.  

### fixed

fixed는 항상 브라우저가 기준이다. 화면이 바뀌더라도 브라우저를 기준으로 위치가 고정된다.

### absolute

absolute는 조상 엘리먼트를 기준으로 relative하다고 생각하면 된다. 

### fixed와 sticky의 

fixed는 보이는 화면을 기준으로 지정한 오프셋에 계속 고정되고, sticky는 스크롤을 내리다가 지정한 오프셋에 도달하면 계속 그 위치에 고정된다.  





