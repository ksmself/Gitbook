---
description: 실전에 적용할 수 있도록 간단한 예제를 통해 훈련하는 과정.
---

# Html 훈련

## \(1\) Ad Banner

다음과 같은 배너는 어떻게 만들 수 있을까? 생각보다 어렵지 않다. 세 가지 부분으로 나눈다는 것을 인지하면 그 다음은 간단하다. 다음 배너는 크게 _제목/부연 설명/클릭, 이렇게 세 부분으로 나눌 수 있다_. 제목은 h1 태그를 사용해서, 부연 설명은 p 태그로, 클릭을 하면 어딘가로 넘어가기 때문에 a 태그를 사용해주면 된다. **스타일은 css 파일을 통해서 구현 가능하므로 신경쓰지 않고 코드를 짜면 된다!!!** 

![ad banner](../.gitbook/assets/365.png)

```markup
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Ad Banner</title>
  <link rel="stylesheet" href="./styles.css">
</head>
<body>
  <div class="modal">
    <h1>Unlimited downloads. <br/>
        Our best content. <br/>
        No attribution.
    </h1>
    <p>
      As low as $9/mo <br/>
      Buy subscription or credit packs
    </p>
    <!-- Join Pro를 누르면 다른 탭으로 넘어가게 하기 위해 target 사용 -->
    <a href="#" target="_blank">
      Join Pro
    </a>
  </div>
</body>
</html>
```

## \(2\) Google Search Result Item

구글에 무언가를 검색하면 아래와 같은 화면이 나타난다. 제목 / 링크 / 설명, 이렇게 세 부분으로 나눌 수 있다. 제목은 h1 태그를 사용하면 되는데, 주의할 점은 웹에서 _제목을 눌러도 사이트로 넘어가기 때문에_, **h1 태그 안에 a 태그를 사용**해서 제목과 링크 두 가지 기능을 하도록 해야한다. 링크는 a 태그를 사용해주면 되고, 설명은 p 태그를 사용해주면 되는데, 잘 보면 &lt;div&gt;, &lt;span&gt;이라는 단어가 있는데, 브라우저 입장에서는 이 단어를 태그로 이해할 수 있기 때문에, **&lt;과 &gt;를 각각 &lt;\(less than\)와 &gt;\(greater than\)로 작성**해주어야 한다. 

![](../.gitbook/assets/367.png)

```markup
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Google Search Result Item</title>
  <link rel="stylesheet" href="./styles2.css">
</head>
<body>
  <div class="google-search-result-item">
    <h1>
      <a
       href="https://www.w3schools.com/html/html5_semantic_elements.asp">
       HTML5 Semantic Elements - W3Schools
      </a>
    </h1>
    <a
     href="https://www.w3schools.com/html/html5_semantic_elements.asp">
     https://www.w3schools.com › html › html5_semantic_elements
    </a>
    <p>
      Oct 27, 2019 - Examples of non-<strong>semantic elements</strong>: 
      &lt;div&gt; and &lt;span&gt; - Tells nothing about its content. ... HTML5
       <strong>semantic elements</strong> are supported in all modern browsers. 
       ... So, on the Internet, you will find HTML pages with &lt;section&gt; 
       elements containing ...
    </p>
  </div>
</body>
</html>

```

## \(3\) Feature Box

웹사이트에서 종종 아래와 같은 화면을 볼 수 있다. 그 중, 첫번째 사진과 글에 대해 코드를 짜보려고 한다. 사진과 제목, 부연설명으로 이루어져 있어 간단하지만 주의해야 할 사항이 두 가지가 있다. 

1. img 태그에는 경로를 지정하는 src 외에, 이미지가 없을 경우를 대비한 대체 텍스트인 alt라는 attribute을 꼭 넣어주어야 한다. 설령, 뭐라고 적어야 할지 모르겠거나 딱히 설명이 필요한 부분이 아니더라도 alt=""로 비워두면 된다. 
2. html은 정보를 나타내기 위한 언어인데, 개발자에 따라서는 이미지를 정보의 영역이 아닌 디자인의 영역으로 생각하는 경우도 있다. 그럴 경우, img 태그 없이 div class에 no-image라는 attribute을 추가해 css에서 이미지 부분을 해결할 수도 있다. 

![](../.gitbook/assets/369-_li.jpg)

그러면 코드로 확인해보자. 

```markup
<!-- 이미지를 html에 포함시키는 경우 -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Feature Box</title>
  <link rel="stylesheet" href="./styles3.css">
</head>
<body>
  <div class="feature-box">
    <img src="https://wac-cdn.atlassian.com/dam/jcr:bc1f15f9-3b2e-4c30-9313-0ebd6175f18c/File%20Cabinet@2x.png?cdnVersion=676" alt="">
    <h1>
      Free unlimited private repositories
    </h1>
    <p>
      Free for small teams under 5 and priced to scale with Standard ($3/user/mo) or Premium ($6/user/mo) plans.
    </p>
  </div>
</body>
</html>

<!-- 이미지를 css에 포함시키는 경우 -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Feature Box</title>
  <link rel="stylesheet" href="./styles3.css">
</head>
<body>
  <div class="feature-box no-image">
    <!-- <img src="https://wac-cdn.atlassian.com/dam/jcr:bc1f15f9-3b2e-4c30-9313-0ebd6175f18c/File%20Cabinet@2x.png?cdnVersion=676" alt=""> -->
    <h1>
      Free unlimited private repositories
    </h1>
    <p>
      Free for small teams under 5 and priced to scale with Standard ($3/user/mo) or Premium ($6/user/mo) plans.
    </p>
  </div>
</body>
</html>
```

