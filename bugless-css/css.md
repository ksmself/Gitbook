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

## 

