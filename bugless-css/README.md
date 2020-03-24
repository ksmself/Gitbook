---
description: '''김버그의 CSS는 재밌다'' 강의 복습용 노트'
---

# Bugless-CSS

## Box

### Box Model 

html에서 만든 요소들은 브라우저에서 모두 '**박스**'로 표현된다. 박스는 일정한 형태의 모델로 구성되어 있기 때문에 아래와 같은 박스를 '**박스모델**'이라고 표현한다. 

![Box Model](../.gitbook/assets/394.png)

#### content

content는 말 그대로 컨텐트가 들어있는 박스다. **width**와 **height**으로 이루어져 있다. 

#### padding

안쪽 여백. 즉, 컨텐트와 테두리 사이에 있는 공간이 바로 **padding**. 

#### border

테두리. 아래의 코드와 같이 **굵기, 스타일, 색상**에 대한 속성 모두를 부여해주어야 함. 

```css
border: 3px solid #000; 

/* border가 없다고 하고 싶을 때 */
border: none;

/* border를 둥글게 하고 싶을 때 */
border-radius: 4px;

/* 박스 자체를 원형으로 만들고 싶을때 */
border-radius: 50%

/* border를 개별적으로 깎고 싶을때 */
border-top-right-radius: 4px;
border-bottom-left-radius: 5px;
```

#### margin

바깥 여백. 즉, **요소와 요소 사이의 간격**을 나타내고 싶을 때 사용. 

#### shorthand 빠르게 쓰는 법

**시계 방향**을 기억해라! **top right bottom left** 순으로 한 번에 적으면 된다. 또한, **bottom은 top**과, **left는 right**과 짝이라는 것을 기억하자. 

```css
/* top 10px right 20px bottom 30px left 40px */
margin: 10px 20px 30px 40px; 

/* top과 bottom이 30px, right과 left가 20px */
margin: 30px 20px;

/* top이 10px, right과 left가 20px, bottom이 30px */
margin: 10px 20px 30px;
```

### Box Sizing

아래와 같이 padding-top이 40px, padding-left가 50px이고, width와 height가 모두 480px인 정사각형의 박스를 만든다고 하자. 

![width&#xC640; height&#xAC00; &#xBAA8;&#xB450; 480px&#xC778; &#xC815;&#xC0AC;&#xAC01;&#xD615;](../.gitbook/assets/395.png)

위와 같은 박스를 만들기 위해 아래와 같은 css 코드를 작성하게 될 것이다. 

```css
/* 이름이 box인 class */
.box{
    width: 480px;
    height: 480px;
    padding-top: 40px;
    padding-left: 50px;
    background-color: #0066ff;
    /* text 색상은 color로 지정할 수 있다 */
    color: #fff;
}
```

그런데 위와 같이 코드를 작성하게 되면, padding 값이 포함되어 width와 height가 520, 530인 직사각형 박스가 완성된다. 

![&#xC758;&#xB3C4;&#xCE58; &#xC54A;&#xAC8C; &#xC9C1;&#xC0AC;&#xAC01;&#xD615;&#xC774; &#xB9CC;&#xB4E4;&#xC5B4;&#xC9C4; &#xC0C1;&#xD669;.](../.gitbook/assets/396.png)

왜 직사각형이 만들어졌을까? 바로 **Box-sizing이 content-box**로 설정되어 있기 때문이다. 즉, width와 height가 content-box를 기준으로 정해졌기 때문인 것이다.   
이를 border를 포함한 width와 height에 대한 설정으로 바꿔주기 위해서는 **box-sizing을 border-box**로 변경해주면 된다.

![box-sizing&#xC744; border-box&#xB85C; &#xBCC0;&#xACBD;&#xD588;&#xC744; &#xB54C;&#xC758; width&#xC640; height. ](../.gitbook/assets/397.png)

코드를 다음과 같이 변경하면, content-box에 변화가 생긴다. 

```css
/* 이름이 box인 class */
.box{
    box-sizing:border-box;
    width: 480px;
    height: 480px;
    padding-top: 40px;
    padding-left: 50px;
    background-color: #0066ff;
    /* text 색상은 color로 지정할 수 있다 */
    color: #fff;
}
```

![box-sizing&#xC744; border-box&#xB85C; &#xBCC0;&#xACBD;&#xD55C; &#xD6C4;&#xC758; content-box&#xC758; width&#xC640; height&#xC5D0; &#xC0DD;&#xAE34; &#xBCC0;&#xD654;. ](../.gitbook/assets/398.png)

대부분의 프론트엔드 개발자들은 위와 같은 상황때문에 처음부터 이를 깔고 시작한다고 한다. 

```css
/* *는 모든 요소에 해당됨을 의미*/
*{
    box-sizing: border-box;
}
```

### Box

박스모델보다 중요한 것은 바로  박스! **박스의 타입이 무엇이냐**에 따라서 박스 모델의 작동방식이 달라진다. 가장 중요하다고 여겨지는 박스 타입 4가지가 있다.  

* Block
* Inline
* Inline Block
* Flex

### Block

#### display

display는 box type을 결정 짓는 css 속성이다. display가 어떤 값이냐에 따라서 박스 값이 달라지는 것이다. 모든 html 요소는 다 display 값을 가지고 있다. 왜냐하면, 모든 html 요소는 박스로 표현되기 때문이다. 

#### block = 길막? 

브라우저가 html을 화면에 렌더할 때, 마크업이 된 순서대로 위에서 아래로 차곡차곡 쌓아나가는데, 쌓아올릴 요소가 **block** 박스라면 자기 다음에 올 요소가 자신의 옆자리로 오지 못하도록 무조건 '**길막**' 한다는 뜻이다.  아래의 사진처럼 말이다. 첫 번째 블록 요소 옆에는 600px나 자리가 남아있지만 다음 요소는 그 옆으로 갈 수가 없다. 바로 블록이 길막하고 있기 때문에! 

![&apos;&#xBE14;&#xB85D;&apos;&#xC774; &apos;&#xAE38;&#xB9C9;&apos;&#xD558;&#xB294; &#xBAA8;&#xC2B5;](../.gitbook/assets/399.png)

#### block의 특징

1. 따로 width를 선언하지 않은 경우, **width = 부모의 content-box의 100%**를 차지
2. 따로 width를 선언한 경우, **남은 공간은 margin**으로 자동으로 채움. 그렇지만 개발자 도구로 확인해보면 그 margin이 표시되어 있지 않아, 나중에 디버깅할 때 난감한 경우가 있다. 그러므로 남은 공간을 margin으로 채운다는 것을 알아두는 게 매우 중요하다!  
3. width, height, padding, border, margin, 모든 박스의 속성이 자유롭게 사용 가능하다. 
4. 따로 부모의 height를 선언하지 않을 경우, 자식 요소의 height의 합 = 부모의 height가 된다. 

#### margin: 0 auto; 

css를 배운 적이 있다면, margin: 0 auto; 에 대해 들어본 적이 있을 것이다. 나 역시 들어본 적이 있지만, block의 특징을 안다면 저걸 굳이 외울 필요가 있나 싶다. 특정 block의 width: 400px로 설정했다고 하자\(부모의 width은 1000px일때\). **남은 600px은 margin이 자동으로 채울 것**이다. 다음과 같은 상황에서 margin-left: auto; 라고 하면 margin이 모두 왼쪽으로 채워지고, block은 오른쪽으로 이동할 것이다. 그리고, margin-right: auto; 라고 추가하면 블록이 중앙으로 이동할 것이다. 다음과 같은 원리에 의해서 marign: 0 auto; 라는 표현이 나온 것이다.  

### Inline

block의 키워드는 '**길막**'이지만, **inline**의 키워드는 '**흐름**'이다. 아래와 같은 상황에서 Inline은 자동으로 다음줄로 넘어가게 된다. 우리가 텍스트를 작성할 때에도, 일정 글자 수가 넘어가면 다음줄로 넘어가듯이 말이다. 

![&#xBC15;&#xC2A4;&#xAC00; &#xC624;&#xBA74;&#xC11C; &#xC804;&#xCCB4; width&#xAC00; &#xBD80;&#xBAA8;&#xC758; width&#xB97C; &#xB118;&#xC5B4;&#xC11C;&#xB824; &#xD560;&#xB54C;. ](../.gitbook/assets/400.png)

#### Block vs Inline

block은 면, inline은 선이라고 이해하면 된다. block은 영역을 잡기 위한 박스 타입이므로, width, height, padding, border, margin 모두 사용 가능하다. 하지만 inline은 content를 옆으로 흐르게 하는 흐름이므로, 이 흐름을 방해하는 아래와 같은 상황을 매우 싫어한다.

![Inline&#xC758; &#xD750;&#xB984;&#xC744; &#xBC29;&#xD574;&#xD558;&#xB294; &#xC0C1;&#xD669;](../.gitbook/assets/401.png)

#### 사용 불가능한 속성

따라서, 위와 같이 Inline의 흐름을 방해하는 속성을 사용할 수 없다. 바로 아래의 리스트 말이다. 

* width
* height
* padding-top
* padding-bottom
* margin-top
* margin-bottom
* border-top
* border-bottom

### Inline Block

Inline Block은 '짬짜면' 이라는 키워드로 소개할 수 있다. Block && Inline, 즉, block과 inline의 장점만 모았다. 아래의 그림이 적절한 예시이다. 

![Inline Block&#xC758; &#xC608;&#xC2DC;](../.gitbook/assets/402.png)

위의 그림은 width, height, padding-top, margin-bottom을 모두 적용했다. 즉, Inline Block은 Block처럼 모든 속성을 활용할 수 있지만, Inline처럼 흐름이 있다. 

## Float

float는 **'블록 요소'의 '가로 배치'**를 하기 위한 요소이다. '블록'은 '길막' 하는 특성 때문에 가로 배치가 매우 어려운데, 이를 해결해주는 것이 바로 'float'이다.  

### what happens: float를 사용하면 무슨 일이 일어날까

#### 집 나간 내 새끼, 찾을 길 없네

* 어떤 요소에 float가 적용되면, 부모는 그 요소를 집 나간 자식으로 판단한다. 그 형제들도 마찬가지로, 그 요소가 없어졌다고 판단한다. 
* 원래 블록에서 부모의 height 값이 따로 주어지지 않으면, 부모의 height는 자식 요소들의 height의 합이 된다. 예를 들어, a, b, c라는 자식 요소\(모두 블록\) 각각의 height가 200px이라고 하자. 이때, 부모의 height는 자동으로 600px이 된다. 이때, a라는 요소에 float가 적용되면, 부모와 형제 요소들은 a가 사라졌다고 판단하고, **부모의 height는 a의 height가 빠진 400px**이 되고, b와 c는 **a의 원래 자리를 빈자리로 파악하고 그 자리를 채운다**.  

#### 블록으로 신분 상승

* 어떤 요소든지, **float를 적용시키면 display가 'Block'으로** 변하게 된다. 그 요소가 **Inline, Inline Block**일지라도 말이다. 
* 이렇게 'Block'으로 변하고 난 뒤에는, **padding, border, margin** 등 모두 사용할 수 있게 된다. 물론, **width**와 **height**도 줄 수 있다. 

#### 길막을 못해 슬픈 블록아!

* 어떤 요소에 float를 적용시키면 'Block'으로 변하긴 하는데, 약간 하자가 있는 block이 된다. 
* 바로 **'길막'을 할 수 없는** 블록이 되는 것이다. 
* 원래 블록에서는, 따로 width를 선언하지 않은 경우, block의 width는 부모의 content-box의 100%를 차지한다. 하지만, **float로 인해 블록이 된 요소의 width**는 **자신의 content-box만큼의 길이만 차지**한다. 
* 또, 원래 블록에서는 따로 width를 선언한 경우, 남은 공간은 자동으로 margin이 채우게 되어 있었다. 하지만, **float로 인해 블록이 된 요소**는, 따로 width를 선언하고 공간이 남더라도, **자동으로 margin이 그 공간을 채우지 않는다**는 것이다. 그렇다고, margin을 줄 수 없다는 것은 아니다. **margin은 얼마든지 원한다면 줄 수 있**지만, 자동으로 채워지지 않는다는 것이다. 

#### 플로트, 나만 볼 수 있어요 \(feat. 인라인\)

* f**loat가 일어나면, 블록 박스들은 이 요소를 없는 박스로 취급**한다. 
* 하지만, 텍스트나 이미지 같은 **인라인은 집 나간 float를 기가 막히게 알아내고, 그 주변을 피해서 공간을 차지**한다. =&gt; **float로 인해서 레이아웃은 와장창 무너진다**. 

### How to fix

#### 쉽지만 왜인지 알 수 없는 overflow:hidden;

원래, 자식에게 float가 적용되면, 부모는 자식이 사라졌다고 생각하고, 이 자식을 찾을 길이 없다. 하지만, **부모에게 overflow: hidden;을 적용**하면, 왜인지는 몰라도 부모는 자식을 바로 찾아낸다. 

#### fm으로 해결 가능한 clearfix

![float&#xB97C; clearfix&#xB85C; &#xCC3E;&#xC544;&#xB0B8; &#xC608;&#xC2DC;](../.gitbook/assets/413.png)

위의 사진은 clearfix로 레이아웃이 무너지는 걸 막은 예시다. **float 다음에 오는 block에 clear: left; 를 적용**하면, 이 블록은 **자신의 왼쪽에 있는 모든 float를 찾아내게 된다**. **clear:** left; 뿐 아니라 **right, both**도 사용할 수 있다. 

#### Pseudo-Element 이용해서 해결하기

Html에서는 존재하지 않는 가상 요소를 이용하는 방법이다. 

![&#xBD95;&#xAD34;&#xB41C; &#xB808;&#xC774;&#xC544;&#xC6C3;.](../.gitbook/assets/418.png)

위와 같은 상황일때, 마지막 박스 뒤에 div를 만들어, 그 div에 clear를 줄 수도 있지만, 단순히 스타일적인 부분 때문에 의미 없는 html 요소를 추가하는 것이 현명한 방법은 아니다. 대신, css로 가상 요소를 만들어 이를 해결하는 방법이다. 

![pseudo-element &#xC774;&#xC6A9;&#xD558;&#xB294; &#xBC29;&#xBC95;](../.gitbook/assets/416.png)

위와 같이 'parent'라는 클래스 뒤에 가상요소를 만드는 방법이다. 

* 가상요소를 selector **뒤에 만들면**, **selector :: after**, selector **앞에 만들면**, **selector :: before**라고 하면 된다.  
* 가상요소를 만들 때, **절대 빠트리면 안되는 것**은 '**content**'이다. 빈칸으로 두든, 이모티콘을 넣든 그 내용은 content 안에 들어가야 한다. 
* **clear 속성을 이용할 수 있는 것은 'block' 뿐**이다. 그래서 clear를 주려고 한다면, 해당 selector의 **display를 block으로** 바꿔야 한다.
* 그리고 clear를 주면 된다. **앞 요소**에 대해서는 **clear: left;** **뒤 요소**에 대해서는 **clear: right;**  

## Position

요소를 **원하는 위치에 자유롭게 이동**시키기 위한 property. position에는 **static, relative, absolute, fixed, sticky**가 있다. position에 대해 공부할 때는 다음 두 가지에 대해서 생각해야 한다. 

1. 내가 어떤 type의 position을 사용하고 있는지
2. 내가 사용하는 position은 무엇을 기준으로 요소를 위치시키는

### static

* 모든 요소의 기본 position 값이다. 
* 가장 일반적인 상태. 

### relative

* 이동의 기준점은 자신이 원래  있던 자리. 
* 어떤 요소한테 relative를 주면, float 때와 마찬가지로 부모를 떠나서 붕 뜬다. 그러나 float 때처럼 레이아웃이 완전히 붕괴된다거나, 다른 요소에게 특별한 영향을 끼치지는 않는다. 
* 자신의 원래 위치를 기억하고 있다. 또한 부모와 형제도 이 요소의 원래 위치를 기억하고 있다. 그래서 float 때처럼 빈자리를 채운다거나 하지 않고, 자신의 state를 유지한다. 

### absolute

* absolute를 사용하면 float를 사용했을 때와 비슷한 일이 일어난다. float를 사용하면 벌어지는 4가지의 일 중, 플로트 나만 볼 수 있어요\(feat. 인라인\)을 제외한 3가지의 일이 absolute를 사용하면 일어난다.
* **집 나간 내 새끼, 찾을 길 없네**: height가 200px인 요소 a,b,c를 가진 부모 요소는 height가 600px이다. 이 중, a에게 position 값으로 absolute를 주게 되면 a는 붕뜨면서, 부모와 형제들이 a가 사라졌다고 생각하게 되면서, 부모의 height 값이 400px로 바뀐다. 
* **블록으로 신분 상승**: 원래 인라인이었던 요소에 position 값으로 absolute를 주게 되면, block으로 바뀌면서 width, height, padding-bottom 등등에 값을 부여할 수 있다. 
* **길막을 못해 슬픈 블록아**: 원래 인라인이었던 요소에 position 값으로 absolute를 주게 되면, block으로 바뀌긴 하지만 '길막'을 할 수 없다. 그래서 자동으로 margin이 생기지 않는다. 
* absolute는 자신이 원하는 요소를 이동의 기준점으로 잡을 수 있는데, **position이 static이 아닌 것\(조상\)만을 기준으로 잡을 수 있다**.  

### fixed

* absolute를 사용했을 때와 동일한 일이 일어난다. 
* 집 나간 내 새끼, 찾을 길 없네 / 블록으로 신분 상승 / 길막을 못해 슬픈 블록아 
* 그러나 fixed의 기준점은 **viewport**이다. viewport는 **내가 보고 있는 브라우저 창의 전체 크기**를 의미한다. 만약, 내가 iphone x 유저라면, iphone x 디스플레이 전체가 viewport가 되는 것이고, galaxy s20 유저라면, galaxy s20 디스플레이 전체가 viewport가 되는 것이다. 

### z-index

position된 요소들의 수직 방향의 level을 알려주는 요소이다. static을 제외한 모든 type은, relative만 하더라도, 사용하게 되면 수직으로 붕 뜨게 된다. 다양한 요소들이 존재할 때, 수직적 레벨을 달리해주고 싶은 상황에서, z-index를 사용해주게 된다. 바로 아래처럼 말이다.  

![z-index &#xC0AC;&#xC6A9; &#xC608;&#xC2DC;](../.gitbook/assets/419.png)

## Flexbox

flexbox는 **정렬**의 끝판왕. flexbox는 아주 잘 만들어졌기 때문에, '_How to use it_'만 기억하면 된다. 총 4가지 step이 있다. 

### step 1: 나, 플렉스 박스 쓸거임 \(단호\)

![flexbox &#xC4F4;&#xB2E4;&#xACE0; &#xC120;&#xC5B8;&#xD558;&#xAE30;.](../.gitbook/assets/420.png)

_flexbox도 box의 일종_이다. 그래서 **display에 flex**라고 넣어주는 것! flexbox는 block과 유사하지만, block은 할 수 없는 요소를 쉽게 정렬할 수 있는 magic power를 가지고 있다고 생각하면 된다. inline-flex는 inline-block과 유사하지만 요소를 쉽게 정렬할 수 있는 힘을 가지고 있는 것! 그런데 이 선언은 반드시 **정렬하고자 하는 요소를 감싸는** _**부모**_**에게 display: flex;** 라고 해야한다.  

### step 2: 가로 정렬? 세로 정렬? 

![&#xC5B4;&#xB290; &#xBC29;&#xD5A5;&#xC73C;&#xB85C; &#xC815;&#xB82C;&#xD560;&#xC9C0; &#xC120;&#xC5B8;.](../.gitbook/assets/421.png)

가로로 정렬을 원하면 flex-direction을 row로, 세로로 정렬을 원하면 column으로! 

#### axis

flex를 사용하면 보이지 않는 두 개의 축이 생긴다. Main axis와 Cross axis가 생기는데, Main axis는 flex-direction의 방향에 따라서 생기고, Main과 정확히 수직을 이루는 방향으로 Cross axis가 생긴다. 

![flex-direction: row;](../.gitbook/assets/422.png)

![flex-direction: column;](../.gitbook/assets/423.png)

![flex-direction: row-reverse;](../.gitbook/assets/427.png)

![flex-direction: column-reverse;](../.gitbook/assets/428.png)

### step 3: 무조건 한 줄 안에 다 정렬? 

![&#xD55C; &#xC904; &#xC548;&#xC5D0; &#xB2E4; &#xC815;&#xB82C;&#xD560;&#xC9C0; &#xB9D0;&#xC9C0;.](../.gitbook/assets/429.png)

![&#xD55C; &#xC904; &#xC548;&#xC5D0; &#xB2E4; &#xC815;&#xB82C;&#xD558;&#xACE0; &#xC2F6;&#xC740; &#xC0C1;&#xD669;.](../.gitbook/assets/430.png)

위와 같은 block을 flex를 이용해서 한 줄 안에 다 정렬을 하고 싶지만, width가 600px이기 때문에 block이 한 줄에 최대 2개 들어갈 수 있는 상황이다. 이때, nowrap을 사용하면 한 줄 안에 다 정렬하는 것이 가능하다. 

![nowrap&#xC744; &#xC0AC;&#xC6A9;&#xD558;&#xBA70; &#xC790;&#xC2DD;&#xC758; &#xC0AC;&#xC774;&#xC988;&#xB97C; &#xC904;&#xC778; &#xACBD;&#xC6B0;.](../.gitbook/assets/431.png)

그런데, 물론 이렇게 자식의 사이즈를 줄이면서까지 정렬을 원하지 않는 경우도 있다. 이때는, wrap을 사용해주면 된다. 

![wrap&#xC744; &#xC0AC;&#xC6A9;&#xD55C; &#xACBD;&#xC6B0;](../.gitbook/assets/432.png)

### step 4: 씐나는 플렉스 박스 파티 타임!

플렉스 박스를 제대로 활용하려면 두 가지 축을 잘 사용해야 한다. 바로 main axis와 cross axis! **main axis**를 기준으로 할 때는, **justify-content**를, **cross axis**를 기준으로 할 때는, **align-items**, **align-content**를 활용해야 한다. 

![flex-box party time &#xC900;&#xBE44;&#xBB3C;.](../.gitbook/assets/433.png)

#### justify-content

main axis가 row이든, column이든 상관 없이 main axis를 기준으로 정렬하려고 한다면 justify-content를 활용하면 된다. 

![flex-direction&#xC774; row&#xC77C;&#xB54C;, justify-content&#xAC00; center&#xC778; &#xC0C1;&#xD669;.](../.gitbook/assets/434.png)

![flex-direction&#xC774; row&#xC77C;&#xB54C;, justify-content&#xAC00; flex-start&#xC778; &#xC0C1;&#xD669;.](../.gitbook/assets/435.png)

![flex-direction&#xC774; row-reverse&#xC77C;&#xB54C;, justify-content&#xAC00; flex-start&#xC778; &#xC0C1;&#xD669;.](../.gitbook/assets/436.png)

![flex-direction&#xC774; row&#xC77C;&#xB54C;, justify-content&#xAC00; flex-end&#xC778; &#xC0C1;&#xD669;.](../.gitbook/assets/437.png)

![flex-direction&#xC774; row&#xC77C;&#xB54C;, justify-content&#xAC00; space-between&#xC778; &#xC0C1;&#xD669;.](../.gitbook/assets/439.png)

space-around는 요소 주변 간격을 동일하게 한다. 

![flex-direction&#xC774; row&#xC77C;&#xB54C;, justify-content&#xAC00; space-around&#xC778; &#xC0C1;&#xD669;. ](../.gitbook/assets/438.png)

#### align-items

align-items는 cross-axis를 기준으로 할 때 사용한다. 

![cross axis&#xAC00; column&#xC77C;&#xB54C;, align-items&#xAC00; center&#xC778; &#xC0C1;&#xD669;.](../.gitbook/assets/440.png)

![main axis&#xAC00; column&#xC774;&#xACE0;, justify-content&#xAC00; center&#xC774;&#xBA70;, cross axis&#xAC00; row&#xC774;&#xACE0;, align-items&#xAC00; center!](../.gitbook/assets/442.png)

아래와 같이 cross axis는 column인데, 간격을 띄울 요소가 존재하지 않는 상황에서는 align-items: space-around/ space-between을 사용할 수 없다. 

![space-around&#xB97C; &#xC0AC;&#xC6A9;&#xD560; &#xC218; &#xC5C6;&#xB294; &#xC0C1;&#xD669;.](../.gitbook/assets/441.png)

#### align-content

**flex-wrap: wrap;** 일때 사용한다. 물론, cross axis를 기준으로 볼때! 

무슨 영문인지는 모르겠지만 아래처럼 떨어져 있는 요소들을 정렬해보려고 한다.

![flex-wrap: wrap; &#xC77C;&#xB54C;](../.gitbook/assets/450.png)

위의 요소를 align-items: flex-end;를 이용해서 전부 아래로 내리려고 한다. 그런데 결과는 우리가 예상한 것과 다르게 두 요소 사이의 간격이 여전히 떨어진채로 바닥에 붙는다.

![align-items: flex-end; &#xC77C;&#xB54C;.](../.gitbook/assets/445.png)

flex-end를 사용했음에도, red child와 yellow child가 저렇게 정렬된다는 것은, red child & yellow child와 blue child의 cross axis가 따로 존재한다고 볼 수 있다. 이때, **align-content**를 사용하면, 축을 하나로 판단하여 red child와 yellow child가 blue child 바로 위로 내려오게 된다. 

flex-wrap: wrap;일때, align-content: space-between;을 사용하면 아래와 같이 정렬된다. 

![align-content: space-between&#xC744; &#xC0AC;&#xC6A9;&#xD588;&#xC744; &#xB54C;.](../.gitbook/assets/448.png)

이제, align-content를 어느 때에 사용해야 하는지 알게 되었지만, 그래도 헷갈린다고 한다면 cross axis를 기준으로 볼때는 먼저, align-items를 사용하고, 원하는 대로 정렬되지 않으면 align-content를 사용하는 것도 방법이 될 수 있다.

![align-content&#xB97C; &#xC5B8;&#xC81C; &#xC368;&#xC57C;&#xD560; &#xC9C0; &#xBAA8;&#xB974;&#xACA0;&#xB2E4;&#xBA74;. ](../.gitbook/assets/451.png)

### order

item 각각에 번호를 부여해서 원하는대로 정렬하는 것이 가능하다! 

![order&#xB85C; &#xAC04;&#xB2E8;&#xD558;&#xAC8C; &#xC815;&#xB82C;&#xD558;&#xAE30;](../.gitbook/assets/452.png)

## Media Query

* media query는 **Responsive Web**\(반응형 웹\)을 만들기 위해 반드시 알아야 하는 **css 선언**! 
* 요즘에는 web browser를 데스크탑에서만 보지 않는다. 다양한 디바이스로 웹 브라우저를 보게 된다. 
* **디바이스의 사이즈에 따라**서 딱 맞게 화면에 보이도록 **css 적용을 해놓은 그런 웹 사이트**를 **반응형 웹**이라고 한다. 
* 반응형 웹을 만들기 위해서는, **html**에서의 **viewport meta** 태그 선언과 **css**에서의 **media query** 선언이 꼭 필요하다!
* 종종, width:100**vw**; height:100**vh**; 라는 표현을 쓰곤 하는데, 여기 vw와 vh는 **viewport width**, **viewport height**를 의미한다. 1vh는 내가 보고 있는 viewport height의 1%를 의미한다. 

![viewport &#xC120;&#xC5B8;.](../.gitbook/assets/454.png)

**min-width**: 768px은 **최소** 768px **부터는**~ 이라는 뜻이다. 

![media query &#xC120;&#xC5B8;.](../.gitbook/assets/455.png)

max-width도 사용 가능하다. 아래의 경우, 최소 768px부터 991px까지 animation을 적용해달라는 코드이다. 

![max-width &#xC0AC;&#xC6A9; &#xC608;&#xC2DC;.](../.gitbook/assets/457.png)

## Typography

텍스트를 예쁘게 디자인하는 것. 사용자들이 보다 읽기 좋은 텍스트를 제공하기 위한 것. 

### Essentials

![typography&#xC5D0;&#xC11C; essential&#xD55C; &#xC694;&#xC18C;&#xB4E4;](../.gitbook/assets/463.png)

#### font-size

* 글자의 크기를 나타냄.
* px: 절대 단위. 어딜 가든 1px, 2px, 3px.. 고정된 값을 가진다. 
* **em**: 상대 단위. **실제로 적용된 폰트 사이즈를 1em**으로 본다. 예를 들어, font-size가 20px이라면, 1em은 20px이 되고, width에 40em이라고 주면, width는 800px이 되는 식이다. 
* **rem**: 상대 단위. **html에 적용된 폰트 사이즈를 1rem**으로 본다. 예를 들어, html에 font-size를 20px을 주고, css에서 font-size를 3em이라고 하면, font-size를 60px이라고 지정한 것과 같다. 

#### line-height

* 줄 간격. 
* px, em, rem 모두 사용가능하지만 **주로 em을 사용**한다. 
* px이나 rem을 사용할 때는 반드시 그 단위를 표기해주어야 하지만, **em을 사용할 때**는 이를 **생략**하는 것이 관례다. 예를 들면, **line-height: 1.5;** 이런 식으로 말이다. 
* line-height가 얼마이든, **글씨는 줄 간격의 가장 가운데에  배치**가 된다. 

#### letter-spacing

* 글자와 글자 사이의 자간.
* 사용할 수 있는 단위로는 px과 em이 있다. 하지만 해당 폰트 사이즈에 비례해서 몇 퍼센트를 줄이고 늘리는 게 좋겠냐는 뉘앙스로 많이 사용되기 때문에, **주로 em을 사용**한다. 
* 자간을 폰트 사이즈에 비례해 **1% 정도 줄이고 싶으면, letter-spacing: -0.01em;** 이런 식으로 표현한다. 

#### font-family

* 폰트 서체를 표현할 때 사용하는 속성.
* font-family: "Poppins";는 Poppins라는 서체를 사용하라는 뜻.
* font-family: "Poppins", sans-serif;는 Poppins라는 서체를 사용하되, 없으면 sans-serif를 사용하라는 뜻.
* serif는 삐침이 있는 서체, sans-serif는 삐침이 없는 서체. \*아래 이미지 참고

![serif&#xC640; sans-serif &#xBE44;&#xAD50;.](../.gitbook/assets/466.png)

#### font-weight

* 폰트의 무게, 즉, 굵기를 의미함.
* 100 단위로 표현.
* **regular** 사이즈의 굵기는 **400**, **bold** 사이즈의 굵기는 **700**.

![font-weight.](../.gitbook/assets/460.png)

#### color

* 폰트의 색상값.
* **hex**: **\#0066ff** 이런 식으로 표현하는 게 hex.  
* **rgb**: **rgb\(0,102, 255\)** 이런 식으로 표현하는 게 rgb.
* **rgba** : **rgba\(0,102, 255, 1\)**이라고 해서 rgb에 a, **투명도**가 더해진 것. a가 **1이면 완전히 불투명**한 것, **0이면 완전 투명**한 것. 

### and etc...

#### text-align

* 텍스트를 정렬할 때 사용.
* left \| right \| center 로 정렬 가능. 
* \*dummy text를 만들고 싶으면 lorem이라고 쓰고 원하는 글자수를 적은 뒤 탭을 누르면 된다. 

#### text-indent

* 들여쓰기 할 때 사용. 
* text-indent: 100px; 이런 식으로 사용 가능. 
* 마이너스 값도 사용 가능한데, 이럴 경우 들여써지는 것이 아니라 앞쪽으로 밀려난다. 

#### text-transform

* 알파벳 베이스 문자들에만 유의미하다. 
* none \| capitalize \| uppercase \| lowercase 

![text-transform&#xC758; &#xC608;&#xC2DC;. ](../.gitbook/assets/467.png)

#### text-decoration

* 텍스트에 줄을 긋는 것과 관련된 속성.
* none \| underline \| line-through \| overline
* 보통 언제 쓰냐면, a 태그를 사용하게 될 경우 기본적으로 underline이 된 상태로 style이 나타나기 때문에, 이걸 없애길 원할 때, text-decoration: none; 이라고 표현하곤 한다. 

#### font-style

* 문자를 기울이고 싶을 때 사용. 
* normal \| italic \| oblique
* html에서 em 태그는 강조하고 싶을 때 사용해주는 데, em은 기본적으로 기울여진 채로 표현되기 때문에 이를 원하지 않을 때, em의 font-style: normal; 로 바꿔주곤 한다. 

### Webfont

#### 갖다 쓴다

1. [https://fonts.google.com/](https://fonts.google.com/) 에 들어간다. 
2. 마음에 드는 폰트를 고른다. 
3. 사이트에서 알려주는 대로 embed한다.  

![webfont&#xB97C; &#xAC16;&#xB2E4; &#xC4F0;&#xB294; &#xBC29;&#xBC95;.](../.gitbook/assets/468.png)

#### 직접 제공한다

1. font 압축 파일을 다운받는다. 
2. font용 css 파일을 만들어 font-face를 만든다. 
3. font-family, font-style, font-weight, src를 지정한다. 
4. font 파일이 완성되면 html에서 link에 첨부하거나, css 파일에서 import한다. 

![&#xC644;&#xC131;&#xB41C; font-face.](../.gitbook/assets/472.png)

![html&#xC758; link&#xC5D0; font &#xD30C;&#xC77C;&#xC744; &#xCCA8;&#xBD80;&#xD558;&#xB294; &#xBC29;&#xBC95;.](../.gitbook/assets/470.png)

![css&#xC5D0; font &#xD30C;&#xC77C;&#xC744; import&#xD558;&#xB294; &#xBC29;&#xBC95;. ](../.gitbook/assets/474.png)

![&quot;Kimbug&quot;&#xCCB4;&#xAC00; &#xC801;&#xC6A9;&#xB41C; &#xBAA8;&#xC2B5;.](../.gitbook/assets/473.png)

## Background

* **background-color**: 배경색, hex, rgb, rgba로 부여할 수 있다. 
* **background-image**: 배경 이미지를 넣는 것. url\(\) 함수를 이용해서, 가지고 있는 이미지의 경로를 넣어주거나, web에서 넣고 싶은 이미지를 찾아, 그 이미지의 주소를 복사해 넣어줄 수도 있다. 
* **background-repeat**: repeat \| no-repeat. 기본 값은 repeat. 이미지가 반복되어 나타나지 않기를 바란다면, no-repeat으로 설정해주면 된다. 
* **background-size**: contain \| cover \| custom. contain은 이미지가 박스 안에 완전히 포함되어 나타나고, cover은 박스가 빈 공간 없이 완전히 채워지는 것이고, custom은 사용자가 사이즈를 직접 정할 수 있다. 
* **background-position**: x, y를 기준으로 배경이미지의 위치를 정할 수 있다. 

![contain&#xACFC; cover&#xC758; &#xCC28;&#xC774;.](../.gitbook/assets/475.png)

## Transition

css에서는 스타일의 속성을 바꾸는 경우가 종종 있는데, 이 때 애니메이션을 주어 **자연스럽게 바뀔 수** 있도록 하는 것이 **Transition**! 변화가 스르륵 일어날 수 있게 도와준다. 

* **property**: css 속성을 뜻함. 변화를 일으킬 속성이 무엇인지 명시를 하기 위함. 
* 모든 property에 대해 변화를 주고 싶으면 all이라고 지정하면 된다. 
* **duration**: transition이 얼마 동안 일어나야 하는지 알려주기 위한 시간. 단위로는 ms\(1000ms == 1s\)와 s가 있음.
* \[**timing-function**\]: 생략 가능. 변화의 속도를 지정해주는 function. ease-in \| ease-out \| ease-in-out \| cubic-bezier\(\) 를 주로 사용함. 
* ease-in은 처음에는 천천히 바뀌다가 나중에는 휙 바뀜. ease-out은 처음에는 휙 바뀌고 나중에는 천천히 바뀜. ease-in-out은 짬뽕. cubic-bezier\(\)는 사용자가 가속도의 변화를 제어하고 싶을 때 사용하는 function. 
* \[**delay**\]: 생략 가능. transition이 좀 delay된 후에 나타나기를 바랄 때 사용. 
* 아래는 font-size는 1초동안 휙에서 천천히 바뀌고, background-color는 2초동안 cubic-bezier에서 지정한 가속도로 변화하며 1초 delay된 후에 나타나게 하는 transition이다. 

![transition &#xC0AC;&#xC6A9; &#xC608;&#xC2DC;.](../.gitbook/assets/476.png)

## Animation

transition은 css를 먹인 어떤 속성에 변화를 '스르륵' 주게 되지만, animation은 animation을 주고 싶을 때 자유롭게 사용 가능하다. 

어떤 박스에 animation을 주려고 할 때, 그 animation을 따로 이름을 붙여 만들어 속성을 정한다. @keyframes 뒤에 붙이고자 하는 이름을 적어주고, animation이 시작할 때 속성을 from에, 바뀔 때 속성을 to에 적어주면 된다. from, to 대신에 0%, 50%, 100%처럼 %로도 표현 가능하다. 

![Animation &#xAE30;&#xBCF8; &#xD2C0;. ](../.gitbook/assets/477.png)

* 아래는box라는 클래스에서 move-box라는 animation을 사용하려고 하는 경우이다. 즉, 사용하고자 하는 **animation-name**에 해당 animation의 이름을 넣어준다. 
* **animation-duration**은 얼마동안 animation이 실행될지 정해주는 속성이다. 
* **animation-iteration-count**는 해당 animation이 몇 번 반복할지 정해주는 속성이다. **한 번 animation이 실행되고 난 뒤에는 원래 상태로** 돌아간다. 그런데, **animation-direction**을 **alternate**으로 정해주게 되면, animation이 여러번 반복될 때, 한 번 실행후 마지막 상태에서 원래 상태로 돌아갔다 다시 돌아오는 식이다. 
* **animation-timing-function**은 '변화의 속도'를 지정해주는 속성이다. 
* **animation-delay**를 통해 ~초 뒤에 animation이 구현되도록 할 수 있다. 
* 사실 이것들 외에도 animation과 관련된 property들이 매우 많다. 궁금하다면 mdn에 들어가 css animation이라고 검색하면 animation과 관련된 속성들이 다 나온다. 

![animation &#xC0AC;&#xC6A9; &#xC608;&#xC2DC;.](../.gitbook/assets/478.png)

## Selectors

### Type, Class & ID Selector

![selector.](../.gitbook/assets/481.png)

* **Type** Selector: html 태그 selector.
* **Class** Selector: class를 선택할 때 사용. _class의 이름이 'box'_라면, **.box**{property: value}; 
* box1이자 box2이자 box3인 class를 선택하고 싶다면, **.box1.box2.box3** 이렇게 선택해주면 된다. 
* **ID** Selector: ID는 식별자. html 세상에서 해당 ID는 단 하나만 존재. ID의 이름이 'kimbug'라면, **\#kimbug**라고 표현! 
* div.active.box는 div이자 active이자 box인 요소. 
* _id가 kimbug이자 class는 box_인 요소는 **\#kimbug.box** or **.box\#kimbug**라고 표현 가능하다. 

### 













