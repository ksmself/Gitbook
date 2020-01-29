# 트위터 마크업 챌린지

## 올바른 Sectioning Elements 사용 방법 

먼저, **구조적으로 문서를 설계**한다는 것은 **글의 구조**가 쉽게 파악되도록 하는 것이다. 

이것이 중요한 이유는,  800페이지의 전공서를 읽는다고 했을 때, 무작정 읽는 것보다는 책의 개요를 파악하는 것이 좋다. 

* 몇 단원으로 구성되어 있는
* 각 단원의 제목은 무엇인지
* 소단원과 소단원의 주제는 무엇인지 

위의 요소들만 제대로 읽어도 글의 전개 흐름을 쉽게 파악할 수 있다. 또한 정보의 위계 질서도 파악할 수 있다. **브라우저**도 마찬가지로 **개요가 필요**하다. 이를 위해 사용하는 요소가 바로 **Sectioning Elements**이다. **Sectioning Elements**는 section, article, nav, aside로 총 4개다. sectioning elements는 일종의 **단원을 여는 것**이다. 단원에는 항상 주제, 제목이 있다. 그래서 Sectioning Elements 내에는 **반드시 heading 태그를 작성**해야 한다. 

```markup
<section>
  <h1>섹션의 제목</h1>
  <p>..............</p>
</section>

<nav>
  <h1>메뉴</h1>
  <ul>
    <li>
      <a href="#">링크</a>
    </li>
  </ul>
</nav>
```

## 페이지 구조 설계

'Html &gt; Html 훈련' 파트에서 UI Component의 코드를 짤때에는 최소한의 기능/의미를 갖는 가장 작은 단위로 쪼개보는 훈련을 했었다. 그 방식이 유효하긴 하지만, 앞으로는 조금 더 크게 구획으로 나눠볼 것이다. 논리적으로 긴밀하게 연결된 집합체끼리! 

![&#xC55E;&#xC73C;&#xB85C; &#xB9C8;&#xD06C;&#xC5C5; &#xD560; &#xD2B8;&#xC704;&#xD130;](../.gitbook/assets/382.png)

위의 트위터 페이지를 마크업하기 전에 먼저 구획을 나눠보자! 어떻게 나눌 수 있을까? 

![&#xB17C;&#xB9AC;&#xC801;&#xC73C;&#xB85C; &#xAE34;&#xBC00;&#xD558;&#xAC8C; &#xAD6C;&#xD68D;&#xC744; &#xB098;&#xB220;&#xBD04;. ](../.gitbook/assets/383.png)

상단부 또는 도입부 / 피드 작성 폼 / 피드 / 트렌드 순위 / 팔로우 추천 목록 / 사이트 정보 ••• 정도로 나눌 수 있을 것 같다. 하지만 이는 문서를 작성하는 사람의 관점에 따라 충분히 달라질 수 있다. 

## Header

어떤 페이지의 상단부, 도입부를 담당하는 것이 바로 header이다. header는 div와 비슷하지만, div보다는 어떤 section의 상단부, 도입부의 뉘앙스가 느껴질 때 사용한다. 아래의 경우, 트위터의 로고가 있다. 그러므로 이는 전체 페이지에서 가장 중요한 부분, 대제목과 같은 부분이라고 할 수 있다. 그래서 header라고 판단한 것이다. 

![&#xD2B8;&#xC704;&#xD130;&#xC758; Header](../.gitbook/assets/384.png)

우선, 트위터 로고 부분만 마크업해보겠다. 

```markup
<header>
  <!-- 트위터 로고가 페이지에서 가장 중요한 부분이라고 할 수 있으므로 h1 사용 -->
  <h1>
    <!-- 트위터 로고를 누르면 다시 트위터 메인으로 이동하므로 anchor 태그 사용 -->
    <a href="#">
      <!-- src는 그냥 생략하겠음 -->
      <img src="#" alt="Twitter">
    </a>
  </h1>
</header>
```

## Global Navigation

nav는 문서 페이지 간에 이동이 필요한 메뉴가 있는 경우 사용한다. 또한, nav는 sectioning elements에 포함되므로, 반드시 heading 태그를 포함해야 한다. 

![nav](../.gitbook/assets/385.png)

위의 nav를 간단히 마크업해보자. 

```markup
<nav>
  <!-- nav는 sectioning elements이므로 반드시 heading 태그 포함 -->
  <h1>Global Navigation Menu</h1>
  <ul>
    <li>
      <a href="#">
        <span>Current Page</span>
        <!-- Icon -->
        Home
      </a>
    </li>
    <li>
      <a href="#">
        <!-- Icon -->
        Explore
      </a>
    </li>
    <li>
      <a href="#">
        <strong aria-label="5 Unread notifications">5</strong>
        <!-- Icon -->
        Notifications
      </a>
    </li>
    <li>
      <a href="#">
        <!-- Icon -->
        Messages
      </a>
    </li>
    <li>
      <a href="#">
        <!-- Icon -->
        Bookmarks
      </a>
    </li>
    <li>
      <a href="#">
        <!-- Icon -->
        Lists
      </a>
    </li>
    <li>
      <a href="#">
        <!-- Icon -->
        Profile
      </a>
    </li>
    <li>
      <button type="button">
        <!-- Icon -->
        More
      </button>
      <!-- Dropdown Menu -->
    </li>
  </ul>
  <button type="button">
    Tweet
  </button>
</nav>
```



