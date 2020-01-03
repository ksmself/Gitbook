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

