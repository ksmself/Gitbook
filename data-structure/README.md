---
description: 생활코딩의 Data Structure 강의 듣고 정리.
---

# Data Structure

## Data Structure란 무엇인가? 

현실을 프로그래밍적으로 표현하는 것. 

* 이미 만들어져 있는 data structure를 프로그래밍에 활용하면 된다. 
* 예시\) tree, set, graph 등
* 큰 데이터를 효율적으로 관리하기 위해 필요함. 책이 한 권 있다면 상관 없겠지만, 책이 몇 백권 된다면 정리도 어렵지만, 내가 필요한 책을 찾는 것도 쉽지 않음. 그래서 책을 어떠한 기준에 맞춰 분류하게 된다. 데이터도 마찬가지로 많은 양의 데이터일때, 효율적으로 관리하는 것이 필요하다는 것! 
* data structure가 어려운 이유: 실무 경험이 없다, 공감이 안된다, 이해가 안된다.  =&gt; data structure를 몰라도 프로그램을 만들 수 있다. 경험을 더 쌓으면, 충분히 이해 가능하다! 이해가 안된다면, 정기적으로 다시 시도해보자!

##  Array

배열, 거의 모든 언어에서 지원하는 데이터 타입. 

* 많은 data structure들이 배열을 부품으로 용. 
* 데이터가 많아지면 그룹 관리의 필요성이 생김. 1학년1반/.../2학년1반/../3학년1반/.. 이런 식으로 나누지 않는다면 학생들을 호명할 때 문제가 생긴다. 이럴 때 사용하는 것이 바로 배열!
* 여러 데이터를 하나의 이름으로 그룹핑해서 관리하기 위한 data structure 
* 반복문을 사용해서 배열에 있는 데이터를 하나 하나 꺼내서 각각의 값에 대한 처리를 할 수 있도록 함. 
* 장점이자 단점: 크기가 정해져 있다, 기능이 없다 &lt;= 배열을 좋은 부품\(작고, 단\)으로 만들기 위해

![\*index: &#xACE0;&#xC720;&#xD55C; &#xBC88;&#xD638;, &#xC804;&#xCCB4; &#xC9D1;&#xB2E8;&#xC5D0;&#xC11C; &#xB370;&#xC774;&#xD130;&#xB97C; &#xC2DD;&#xBCC4;&#xD574;&#xC8FC;&#xB294; &#xC911;&#xC694;&#xD55C; &#xC5ED;&#xD560; ](../.gitbook/assets/image%20%287%29.png)

## List

순서대로 저장되며 중복을 허용함.

### array와 list의 차이 

array는 데이터가 저장되어 있는 위치, 주소가 중요하다면 list는 데이터가 저장되어 있는 순서가 중요함 

* 데이터를 추가할 때: 세 번째 인덱스에 50이라는 값을 추가한다고 할 때, array는 기존의 세 번째 인덱스의 40이라는 값이 50으로 바뀐다. 반면, list는 2번째 인덱스와 4번째 인덱스 사이에 50이라는 값이 들어간다. 

![&#xC6D0;&#xBCF8; data](../.gitbook/assets/image%20%288%29.png)

![array](../.gitbook/assets/image.png)

![list](../.gitbook/assets/image%20%286%29.png)

* 데이터를 삭제할 때: 0번째 인덱스에 10, 1번째 인덱스에 20, 2번째 인덱스에 30, 3번째 인덱스에 40, 4번째 인덱스에 50이 들어있는 데이터가 있었다고 하자. 여기서 3번째 인덱스의 40이라는 값을 지우면, array는 40이 없어진 자리가 빈자리로 남아 있지만, list는 4번째 인덱스에 있던 값이 3번째 인덱스로 옮겨 오게 된다. 즉, **array에서는 인덱스**가 주민등록번호처럼 변하지 않는 **고유한 값을 가질 수 있게** 하는 역할을 해주지만, **list**는 데이터 밀도를 촘촘하게 유지하게 하기 위해, **인덱스를 식별자로 사용하지 않는다**. 

![array](../.gitbook/assets/image%20%282%29.png)

![list](../.gitbook/assets/image%20%283%29.png)

### list의 기능

* 처음, 끝, 중간에 엘리먼트를 추가/삭제하는 기능
* 리스트에 데이터가 있는지를 체크하는 기
* 리스트의 모든 데이터에 접근할 수 있는 기

### 언어별 비교

* c는 리스트를 지원하지 않음, 그래서 개발자가 리스트를 잘 알고 있는 것이 중요함. 왜냐하면 직접 만들어서 사용해야 하기 때문.
* javascript는 c의 패밀리이지만, 배열이 리스트이기도 함. 
* python에서 리스트가 배열이기도 함. 
* 최근의 언어는 리스트를 기본적으로 지원한
* java는 배열과 리스트를 완전히 독립된 문법으로 제공하고 있음. 리스트를 두 개\(LinkedList, ArrayList\) 지원, LinkedList는 데이터를 빠르게 추가/삭제할수있지만, 인덱스를 통해서 조회할 때는 느리다. ArrayList는 데이터를 추가/삭제할 때 굉장히 느리지만, 인덱스를 이용하면 빠르게 데이터를 가져올 수 있음. 즉, 개발자가 필요에 따라 선택해서 잘 쓰면 된다! 
* data structure는 언어마다 다르다. So, 본질, 중심되는 컨셉이 중요하다. 

#### 
