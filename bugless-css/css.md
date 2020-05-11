# Css 훈련

## TCSS 초보를 위한 꿀팁

* 노트를 준비한다.
* 현재 상태와 만들어야 할 디자인 시안을 비교한다.
* 현 상태와 디자인 시안의 차이점을 찾아 체크리스트로 작성한다. 
* 작성한 체크리스트를 하나하나 해결한다. 

## float 1

![&#xB514;&#xC790;&#xC778; &#xC2DC;&#xC548;.](../.gitbook/assets/479%20%281%29.png)

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

## position 2 

![&#xB514;&#xC790;&#xC778; &#xC2DC;&#xC548;.](../.gitbook/assets/487.png)

![&#xD604;&#xC7AC; &#xC0C1;&#xD0DC;.](../.gitbook/assets/488.png)

* 먼저, card의 사이즈부터 조정한다. 

```css
  .card{
    width: 400px;
    height: 354px;
  }
```

* card의 사이즈를 조정해도 이미지가 줄어들지 않으니, 이미지의 사이즈를 조정한다. 이때, 이미지는 inline인데, width와 height를 적용했으니 display를 block으로 바꿔준다. 

```css
  .card-carousel img{
    display: block;
    width: 100%;
    height: auto;
  }
```

* 화살표의 position을 조정해준다. top: 50%으로 하면, 50% 지점에서부터 시작되기 때문에, 화살표의 위치가 정중앙보다 내려오게 된다. 그래서 transform: translateY\(-50%\)을 사용해 그 위치로부터 50% 올라갈 수 있도록 조정해준다. 

```css
  .card-carousel{
    position: relative;
  }
  #prev, 
  #next{
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
  }
  #prev{
    left: 0;
  }
  #next{
    right: 0;
  }
```

* card-content 내부에 대한 정리다. 처음 혼자 실습을 해볼 때는 컨텐트 내부 요소 각각의 position을 조정했지만, 강의를 들어보니 그냥 padding을 주면 쉽게 positioning이 가능했다. card-content의 strong부분도 그냥 text-align을 right으로 주면 되었다. 

```css
  .card-content h1{
    margin-bottom: 2px;
  }
  .card-content strong{
    display: block;
    /* 일반적으로, margin은 한 방향으로 주는 것이 좋음 */
    margin-top: 8px;
    text-align: right;
  }
  .card-content{
    padding: 12px 16px;
  }
```

## position 3 

![&#xB514;&#xC790;&#xC778; &#xC2DC;&#xC548;.](../.gitbook/assets/492.png)

![&#xD604;&#xC7AC; &#xC0C1;&#xD0DC;.](../.gitbook/assets/491.png)

* 텍스트나 **인라인 요소를 블록 안에서 가운데 정렬하고 싶을 때** 사용하는 속성이, **text-align: center;**이다. 

```css
  .modal-title, 
  .modal-desc{
    text-align: center;
  }
  .modal-title{
    margin-bottom: 4px;
  }
  .modal-desc{
    width: 591px;
    margin: 0 auto 24px;
  }
```

* input과 버튼도 display가 inline-block이므로, 부모 요소인 block 'input'에 가운데 정렬 속성을 주면 된다. 그리고 버튼에 padding을 주면, 혹여나 글씨가 커지더라도 버튼이 꽉 차지 않고 일정 여백을 유지한 채 버튼의 사이즈가 커진다. 

```css
  .input-group{
    text-align: center;
  }
  .input-group input{
    border: none;
    width: 200px;
    height: 36px;
    padding: 0 16px;
    border-radius: 4px;
    background-color: #F6F8FA;
    margin-right: 8px;
  }
  .input-group button{
    border: none;
    height: 36px;
    padding: 8px 14px;
    border-radius: 4px;
    background-color: #2860E1;
    color: #fff;
  }
```

* modal은 display가 block인데, **block은 width 값을 따로 부여하지 않을 경우, 부모의 100%를 다 차지**한다. 근데 만약, **position: fixed를 주게 되면, width가 따로 선언되어 있지 않기 때문에, 가지고 있는 content 사이즈만큼 줄게 된다.** 

```css
  .modal{
    padding: 32px 40px;
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    border-radius: 4px;
  }
```

* close 버튼은 뷰포트와도 상관 없고, 원래 있던 자리에서 아예 똑 떼서 오른쪽 상단에 붙이고 싶은 것이므로 position: absolute를 사용한다. 부모인 modal도 이미 position이 fixed이므로 건드릴 필요가 없다. 

```css
  .close-button{
    position: absolute;
    top: 8px;
    right: 8px;
  }
```

## flexbox 1 

이미 float를 이용해서 가로 배치했던 코드를 지우고, flexbox를 이용해보려고 한다. 

![&#xB514;&#xC790;&#xC778; &#xC2DC;&#xC548;. ](../.gitbook/assets/479.png)

* flexbox를 이용할때는 가장 먼저 가로 배치하려고 하는 요소들을 감싸는 **부모에게 display: flex;**를 선언한다. 
* 그리고, flex-direction을 선언하는데, row일 경우는 이 값이 default이므로 따로 선언하지 않아도 된다. 
* 가로 배치할 아이들이 한 줄에 꼭 들어와야 한다면 flex-wrap을 nowrap으로 해주어야 하지만, 이 값도 default라서 따로 선언할 필요가 없다. 
* 위의 경우, justifiy-content는 flex-start로 해줘야 하지만, 이 값도 default! 
* align-items는 center로 선언해주면 된다.  

## flexbox 2 

float를 이용해서 가로 배치했던 코드를 지우고 float를 이용해보자. 

![&#xB514;&#xC790;&#xC778; &#xC2DC;&#xC548;. ](../.gitbook/assets/493.png)

* 이미지와 텍스트를 담고 있는 박스를 가로 배치하려고 한다. 이들을 감싸는 부모인 card에 display: flex;를 선언한다. 
* flex-direction은 row이므로 생략, flex-wrap도 nowrap이므로 생략. 
* justify-content는 space-between으로 준다. 둘 사이가 너무 멀어지지 않게 width값도 조정해준다. 
* align-items는 flex-start이므로 생략한다. 

## flexbox 3 

![&#xB514;&#xC790;&#xC778; &#xC2DC;&#xC548;.](../.gitbook/assets/495.png)

![&#xD604;&#xC7AC; &#xC0C1;&#xD0DC;. ](../.gitbook/assets/494.png)

* 이미지는 inline이다. 그래서 먼저 display를 block으로 바꿔준다. 

```css
 .profile-image{
    display: block;
    border-radius: 50%;
    width: 80px;
    height: 80px;
    margin-bottom: 16px;
 }
```

* flex를 이용해서 가운데 정렬을 해준다. 

```css
  .profile{
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 386px;
  }
  .profile-image{
    display: block;
    border-radius: 50%;
    width: 80px;
    height: 80px;
    margin-bottom: 16px;
 }

  .profile-name{
    margin-bottom: 4px;
 }

  .profile-detail{
    display: flex;
    justify-content: space-between;
 }
```

* 그런데 이렇게 하고 나면, profile-detail의 width 값이 작아진다. 간혹, flex를 이용해서 center로 정렬하고 나면 width값이 저절로 조정되는 경우가 있다고 한다.  그래서 profile-detail의 width를 100%로 조정해주면 좁혀진 width가 해결된다. 

```css
  .profile-detail{
    display: flex;
    justify-content: space-between;
    width: 100%;
 }
  .profile-detail-item{
    text-align: center;
 }
```

## media query 

만들어야 하는 여러 버전 중, 모바일부터 시작한다. 나머지 버전은 모바일과 다른 부분에 한해서만 코드를 작성해주면 된다. 

### mobile 

![&#xB514;&#xC790;&#xC778; &#xC2DC;&#xC548;. ](../.gitbook/assets/497.png)

width 값이 가장 작은 ipone5 기준으로 상태를 확인한다. ipone5에서 제대로 나타난다면, 다른 기기에서도 아무 문제 없기 때문이다. 

![&#xD604;&#xC7AC; &#xC0C1;&#xD0DC;.](../.gitbook/assets/498.png)

* 가장 먼저 노란색 배너를 아래에 위치시킨다. 뷰포트를 기준으로 가장 하단에 배치되기를 원하기 때문에 **position: fixed**를 사용해준다. 또, 배너가 화면에서 전체 가로 길이만큼 차지하기 바라므로 **width는 100%**로 해준다. / 앵커 영역이 배너 전체가 되기를 바라므로, **height를 배너의 높이만큼** 준다. 이때, display를 변경해줘야 하는데, **앵커 안의 텍스트가 가운데 정렬**되기 바라므로 **텍스트의 부모인 앵커에 flex를** 준다. 

```css
  .banner{
    position: fixed;
    bottom: 0;
    left: 0; 
    width: 100%;
    background-color: #FFC82C;
  }

  .banner-title a{
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%; 
    height: 64px;
    font-size: 18px;
  }
```

* landing의 height가 애매하게 끊어져 있으므로, height를 100vh로 조정해준다. 왼쪽, 오른쪽으로 부터 20px씩 padding을 준다. landing-title은 세로로 가운데, 가로로는 끝에 붙어 있다. landing에 display: flex를 준다. 텍스트가 오른쪽 정렬되어 있으므로 text-align: right을 준다. 

```css
  .landing{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: flex-end;
    height: 100vh;
    padding: 0 20px;
  }

  .landing-title{
    margin-bottom: 24px;
    text-align: right;
    font-size: 32px;
  }
```

* laning-link 역시 텍스트가 가운데 정렬되어야 하므로, 부모인 landing-link에 flex를 준다. 

```css
  .landing-link{
    display: flex;
    justify-content: center;
    align-items: center;
    width: 160px;
    height: 52px;
    background-color: rgba(0, 0, 0, 0.5);
    border: 2px solid #FFFFFF;
    border-radius: 16px;
    font-size: 15px;
  }
```

### desktop

데스크탑은 모바일 버전에서 수정하면 된다. 

![&#xB514;&#xC790;&#xC778; &#xC2DC;&#xC548;. ](../.gitbook/assets/496.png)

![&#xD604;&#xC7AC; &#xC0C1;&#xD0DC;. ](../.gitbook/assets/499.png)

* 배너를 상단으로 옮겨줘야 하는데, 모바일에서 정해둔 bottom 값을 해제해야 한다. bottom: auto로! 

```css
  @media screen and (min-width: 768px){
    .banner{
      bottom: auto;
      top: 0;
    }

    .banner-title a{
      height: 80px;
    }
  }
```

* landing 부분도 달라진 부분만 수정해준다. 

```css
    .landing{
      align-items: center;
    }

    .landing-title{
      margin-bottom: 32px;
      text-align: center;
      font-size: 50px;
    }

    .landing-link{
      width: 180px;
      height: 56px;
      font-size: 18px;
    }
```

## Typography Library 제작 

디자이너가 아래의 typography 위주로 사용하겠다고 시안을 준다면, 개발자는 이 typography library를 제작하여 활용하면 된다. 

![typography.](../.gitbook/assets/502.png)

* font-size는 font-size, line-height, letter-spacing을 함께 묶어 클래스로 만들어주는데, 주어진 **line-height**는 font-size로 나누어 표시하고, **em은 생략**한다. **letter-spacing은 em**이 필요하다.  

아래와 같이 Typography Library 제작! 

```css
/* ▼ WHERE YOUR CODE BEGINS */
body{
    font-family: 'Noto Sans KR', sans-serif;
    letter-spacing: -0.015em;
}

/* Font Size */
.fs-tiny{
    font-size: 12px;
    /* line-height는 em 생략 */
    line-height: 1.33333333333;
}

.fs-small{
    font-size: 14px;
    line-height: 1.42857142857;
}

.fs-base{
    font-size: 16px;
    line-height: 1.5;
}

.fs-medium{
    font-size: 18px;
    line-height: 1.55555555556;
}

.fs-large{
    font-size: 20px;
    line-height: 1.6;
}

.fs-h2{
    font-size: 28px;
    line-height: 1.42857142857;
}

.fs-h1{
    font-size: 34px;
    line-height: 1.41176470588;
}

/* Font Weight */
.fw-light{
    font-weight: 300;
}

.fw-regular{
    font-weight: 400;
}

.fw-medium{
    font-weight: 500;
}

.fw-bold{
    font-weight: 700;
}

/* Colors */
.text-dark{
    color: #1F2D3D;
}

.text-primary{
    color: #3C4858;
}

.text-secondary{
    color: #8492A6;
}

.text-tertiary{
    color: #C0CCDA;
}

.text-white{
    color:  #FFFFFF;
}

.text-success{
    color: #13CE66;
}

.text-error{
    color: #FF5216;
}

.text-info{
    color:  #009EEB;
}
```

제작한 library를 활용하여 아래의 시안을 완성해보자. 

![&#xB514;&#xC790;&#xC778; &#xC2DC;&#xC548;.](../.gitbook/assets/503.png)

* 먼저, box-sizing을 수정해주고, 브라우저에서 자체 생성한 margin도 없애준다. 

```css
*{
    box-sizing: border-box;
    margin: 0;
}
```

* font-size, font-weight, font의 color에 맞춰 class를 넣어준다. h3는 이미 bold, p는 regular weight이 적용되어 있으므로 생략해준다. 

```markup
<div class="container">
      <h1 class="fs-h1 fw-light text-dark">
        버그가 너무 많아
        <br />
        김 버그
      </h1>

      <h3 class="fs-base text-dark">
        주니어 개발자의 성장 드라마, 김버그
      </h3>
      <p class="fs-base text-primary">
        속에서 같은 주며, 가지에 그들의 우리의 때문이다. 이 길지 가는 있는 같이, 있다. 그들에게 그들은 길지 보내는
        얼마나 동력은 칼이다. 청춘 위하여 같은 새 노래하며 풀이 청춘을 천자만홍이 풍부하게 칼이다. 목숨이 사는가
        그들에게 안고, 위하여서, 타오르고 말이다. 많이 자신과 얼마나 없으면 몸이 이것은
        <span class="text-error">품고 있으랴?</span>
      </p>

      <h3 class="fs-base text-dark">
        앞으로의 계획
      </h3>
      <p class="fs-base text-primary">
        끓는 봄바람을 끝까지 심장은 사는가 끓는 철환하였는가? 찾아다녀도, 우리는 청춘에서만 능히 행복스럽고 바로
        위하여서. 반짝이는 광야에서 가지에 커다란 것이 청춘은 그들은 봄바람이다. 날카로우나 피가 얼마나 얼마나 기쁘며,
        밥을 끓는 자신과 귀는 말이다. 그림자는 황금시대의 현저하게 곳으로 소리다.이것은 쓸쓸하랴? <strong>가진 인간의 옷을
          생명을</strong> 창공에 그들의 얼마나 살 따뜻한 힘있다. 현저하게 투명하되 웅대한 대한 것이다.
      </p>

      <h2 class="fs-h2 fw-regular text-dark">
        프론트엔드 개발, 첫 단추를 꿰다
      </h2>

      <h3 class="fs-base text-dark">
        HTML, CSS
      </h3>
      <p class="fs-base text-primary">
        속에서 같은 주며, 가지에 그들의 우리의 때문이다. 이 길지 가는 있는 같이, 있다. 그들에게 그들은 길지 보내는
        얼마나 동력은 칼이다. 청춘 위하여 <strong>같은 새 노래하며</strong> 풀이 청춘을 천자만홍이 풍부하게 칼이다.
        목숨이 사는가 그들에게 안고, 위하여서, 타오르고 말이다. 많이 자신과 얼마나 없으면 몸이 이것은 품고 있으랴?
      </p>
    </div>
```

* margin을 적용해주고, 텍스트가 너무 가로로 길면 가독성이 떨어지므로 max-width를 정해주고,  padding도 준다. 

```css
.container{
    width: 100%;
    max-width: 736px;
    margin: 0 auto;
    padding: 48px;
}

h1{
    margin-bottom: 48px;
}

h2{
    margin-bottom: 24px;
}

h3{
    margin-bottom: 8px;
}

p{
    margin-bottom: 32px;
}
```

## 



