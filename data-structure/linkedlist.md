# LinkedList

## LinkedList

LinkedList는 ArrayList와는 다르게 엘리먼트와 엘리먼트 간의 연결\(link\)을 이용해서 리스트를 구현한 것을 의미한다. LinkedList에서 가장 중요한 것은 연결이 무엇인가를 파악하는 것이다. 잊고 있을까봐 다시 언급하자면, **우리가 데이터 스트럭쳐를 배우는 이유는 메모리의 효율적인 사용 때문**이다.\(\*CPU-메모리-스토리지 관계의 이해\) 

메모리는 건물에 비유할 수 있다. 아래 그림은 배열을 사용하는 것과 linkedlist를 사용하는 것을 비유해서 보여주고 있다. 어떤 회사가 한 건물의 일부를 임대해서 사용한다고 생각해보자. 

![](../.gitbook/assets/image%20%2813%29.png)

![&#xB450;&#xBC88;&#xC9F8; &#xD68C;&#xC0AC;\_LinkedList](../.gitbook/assets/image%20%284%29.png)

* 첫번째 회사\(Array List\)는 모든 직원이 한 곳에 모여있어야 한다는 철학이 있기 때문에 사무실이 모여있다. 배열은 건물을 이런식으로 사용하는 것과 비슷하다. 만약 회사가 성장해서 사무실이 좁아지면 더 이상 새로운 직원을 뽑을 수 없다. 붙어 있는 공간이 없기 때문이다. 만약 더 많은 공간이 필요하다면, 더 많은 사람을 수용할 수 있는 공간을 찾아서 전체가 이사해야 한다. 
* 두번째 회사\(LinkedList\)는 한 건물 내에서 임대한 사무실이 서로 떨어져 있다. 덕분에 직원이 늘어도 큰 걱정이 없다. 건물에서 비어있는 곳 아무데나 임대해서 들어가면 되니까. 그런데 방문자가 사무실을 찾는 방법이 좀 비효율적이다. 위의 그림에 있는 방문자가 3번째 사무실을 찾아가려면 우선 첫번째 화살표의 사무실을 찾아가야 한다. 이 사무실의 직원에게 다음 사무실이 어딘지 물어본다. 그럼 알려주는 사무실로 이동한 후에 다시 물어봐서 그 다음 사무실로 이동한다. 이렇게 **물어물어 사무실을 찾아가야 하는 방식이 LinkedList**이다. 그래서 linked list에서는 몇 번째 엘리먼트를 찾는 것이 느리다. 반면에 array list는 엘리먼트가 같은 곳에 모여 있으니, 만약 3번째 자리로 가고 싶다면 한 번에 3번째 방으로 찾아갈 수 있다. **찾고자 하는 사무실이 몇 번째에 있는지 알고 있다면 arraylist는 매우 빠르다.** 

### 개념 \(1\) - Linked List의 구성/구조

**리스트는 노드\(엘리먼트\)들의 모임**이다. 따라서 내부적으로 노드를 가지고 있어야 한다. array list의 경우 엘리먼트가 배열의 엘리먼트였다. linked list는 배열  대신에 다른 구조를 사용한다. 노드는 _최소한 두 가지 정보_를 알고 있어야 한다. **노드의 값과 다음 노드**. 각각의 노드가 다음 노드를 알고 있기 때문에 하나의 연결된 값의 모임을 만들 수 있는 것이다. 이것을 구현하는 방법은 여러가지인데 만약 사용 언어가 자바와 같은 객체 지향 언어라면, 객체에 데이터 필드와 링크 필드를 만든다. 보통 데이터 필드는 value라는 이름의 변수, 링크 필드는 next 변수를 사용한다. value에는 노드의 값이 저장되고, next에는 다음 노드의 참조값을 저장해서 노드와 노드를 연결시키는 방법을 사용한다. 

![linked list&#xC758; &#xAD6C;&#xC870;](../.gitbook/assets/image%20%2814%29.png)

위의 그림을 보면 head라는 게 있다. 건물의 비유를 다시 사용해보면, 건물에 들어가기 위해서는 출입문부터 찾아야 한다. 리스트를 하나의 건물로 비유하자면 출입문에 해당하는 것이 head다. linked list를 사용하기 위해서는 이 head가 가리키는 첫번째 노드를 찾아야 한다. 취향에 따라서는 first와 같은 이름을 사용하기도 한다. 

### 개념 \(2\) - 데이터의 추가

#### 시작부분에 추가 

노드를 첫 번째 위치에 추가해보자. 

![](../.gitbook/assets/image%20%283%29.png)

우선 새로운 노드를 생성한다. 

```java
Vertex temp = new Vertex(input);
```

새로운 노드의 다음 노드로 첫번째 노드를 가리킨다. 

```java
temp.next = head;
```

![](../.gitbook/assets/image%20%286%29.png)

새로 만들어진 노드가 첫번째 노드가 되도록 head의 값을 변경한다. 

```java
head = temp;
```

![](../.gitbook/assets/image%20%2821%29.png)

#### 중간에 추가

3번째 자리\(인덱스 2\)에 90을 추가해보자.

![](../.gitbook/assets/image%20%2819%29.png)

3번째 자리는 붉은 화살표가 표시된 부분이다. 즉, 6과 23 사이에 90을 위치시켜야 하므로 우선 3번째 자리를 찾아야 한다. 

![](../.gitbook/assets/image%20%287%29.png)

head를 참조해서 첫번째 노드를 찾는 것이다. 

```java
Vertex temp1 = head;
```

23의 자리에 새로운 노드를 위치시키기 위해서는 6을 알고 있어야 한다. 6의 next로 새로운 노드를 지정해야 하기 때문이다. 아래는 6을 temp1으로 지정하기 위한 반복문이다. 

```java
//현재 k의 값은 2
while (--k!=0)
  temp1 = temp1.next;
```

6의 next를 이용해서 23을 찾아서 temp2로 지정한다. 

```java
Vertex temp2 = temp1.next;
```

![](../.gitbook/assets/image%20%2811%29.png)

값이 90인 새로운 노드를 생성한다. 

![](../.gitbook/assets/image%20%2827%29.png)

```java
Vertex newVertex = new Vertex(input);
```

6의 다음 노드로 새로운 노드를 지정하고, 새로운 노드의 다음 노드로 23을 지정한다. 

![](../.gitbook/assets/image%20%289%29.png)

```java
temp1.next = newVertex;
newVertex.next = temp2;
```

#### arraylist와 linkedlist의 핵심적인 차이

배열의 경우는 엘리먼트를 중간에 추가 또는 삭제할 경우 해당 엘리먼트의 뒤에 있는 모든 엘리먼트의 자리 이동이 필요했다. 그래서 배열은 추가/삭제가 느리다. 반대로 linkedlist의 경우 추가/삭제가 될 엘리먼트의 이전, 이후 노드의 참조값\(next\)만 변경하면 되기 때문에 속도가 빠르다. 

#### 삭제

데이터를 제거하는 것도 추가하는 것과 비슷하다. 아래 리스트에서 세번째 노드\(인덱스2\)를 제거하는 과정을 알아보자. 

![](../.gitbook/assets/image%20%2823%29.png)

우선, head를 이용해서 첫번째 노드를 찾는다.

```java
Vertex cur = head;
```

![](../.gitbook/assets/image%20%2810%29.png)

두 번째 노드로 이동한다. 

```java
//k = 2
while (--k!=0)
  cur = cur.next;
//cur이 6이 된
```

![](../.gitbook/assets/image%20%2820%29.png)

세 번째 노드를 찾고, 두번째 노드의 next를 23으로 변경한다. 그 후에 90을 지우는 게 가능하다. 

```java
Vertex tobedeleted = cur.next;
//tobedeleted = 90
cur.next = cur.next.next;
//6의 next가 23이 된다.
delete tobedeleted;
```

![](../.gitbook/assets/image%20%2829%29.png)

#### 인덱스를 이용한 데이터 조

인덱스를 이용해서 데이터를 조회할 때 linked list는 head가 가리키는 노드부터 시작해서 순차적으로 노드를 찾아가는 과정을 거쳐야 한다. 만약, 찾고자 하는 엘리먼트가 가장 끝에 있다면 모든 노드를 탐색해야 한다. 

![linked list&#xC5D0;&#xC11C; &#xB370;&#xC774;&#xD130; &#xC870;&#xD68C;](../.gitbook/assets/image%20%2815%29.png)

반면에, array를 이용해서 리스트를 구현하면 인덱스를 이용해서 해당 엘리먼트에 바로 접근할 수 있기 때문에 매우 빠르다. 

![array list&#xC5D0;&#xC11C; &#xB370;&#xC774;&#xD130; &#xC870;&#xD68C;](../.gitbook/assets/image%20%2824%29.png)

### LinkedList  java 구현 1 - 객체 생성

* LinkedList에서 가장 중요한 것이 바로 노드의 구현이다. 노드는 실제로 데이터가 저장되는 그릇과 같은 것이라서 이것부터 구현을 먼저 한다.
* 자바는 객체 지향 언어이기 때문에 노드는 객체로 만들기 딱 좋은 대상이다.
* 그리고 노드 객체는 리스트의 내부 부품이기 때문에 외부에는 노출되지 않는 게 좋다. 그래서 private으로 지정한다. 사용자가 이 객체에 대해서 알 필요가 없다. 단지 값을 넣고 빼는 것으로 충분하다. 

![](../.gitbook/assets/image%20%2828%29.png)

* head는 첫번째 노드를 지정하는 참조값이다. 
* tail은 마지막 노드를 지정한다.
* size는 노드의 크기를 의미한다. 노드를 변경할 때마다 이 값들을 수정해야 한다. 
* tail이나 size는 마지막 노드를 찾거나 노드의 수를 셀 때, 연산의 횟수를 획기적으로 줄여준다. 
* 객체 Node는 내부적으로 data와 next 변수를 가지고 있다. data는 노드의 값이고, next는 다음 노드를 가리키는 참조값이다. 

위의 내용을 코드화 시켜 보면,

```java
public class LinkedList {
    // 첫번째 노드를 가리키는 필드
    private Node head;
    private Node tail;
    private int size = 0;
    private class Node{
        // 데이터가 저장될 필드
        private Object data;
        // 다음 노드를 가리키는 필드
        private Node next;
        public Node(Object input) {
            this.data = input;
            this.next = null;
        }
        // 노드의 내용을 쉽게 출력해서 확인해볼 수 있는 기능
        public String toString(){
            return String.valueOf(this.data);
        }
    }
}
```

### LinkedList java 구현 2 - addFirst

```java
public void addFirst(Object input){
    // 노드를 생성합니다.
    Node newNode = new Node(input);
    // 새로운 노드의 다음 노드로 해드를 지정합니다.
    newNode.next = head;
    // 헤드로 새로운 노드를 지정합니다.
    head = newNode;
    size++;
    if(head.next == null){
        tail = head;
    }
}
```

### LinkedList java 구현 3 - addLast

리스트의 끝에 데이터를 추가할 때는 tail을 사용한다. tail이 없어도 구현이 가능하지만, tail이 없다면 마지막 노드를 찾아야 할 것이다. 리스트의 끝에 데이터를 추가하는 작업은 자주 있는 작업이고, 마지막 노드를 찾는 작업은 첫 노드부터 마지막 노드까지 순차적으로 탐색을 해야 하기 때문에 최악의 상황이라고 할 수 있다. 그래서 tail을 사용하도록 하겠다. 

```java
public void addLast(Object input){
    // 노드를 생성합니다.
    Node newNode = new Node(input);
    // 리스트의 노드가 없다면 첫번째 노드를 추가하는 메소드를 사용합니다.
    if(size == 0){
        addFirst(input);
    } else {
        // 마지막 노드의 다음 노드로 생성한 노드를 지정합니다.
        tail.next = newNode;
        // 마지막 노드를 갱신합니다.
        tail = newNode;
        // 엘리먼트의 개수를 1 증가 시킵니다.
        size++;
    }
}
```

### LinkedList java 구현 4 - node

중간에 노드를 추가하는 방법에  앞서 특정 위치의 노드를 찾아내는 방법을 먼저 알아보겠다. 

```java
Node node(int index) {
    Node x = head;
    for (int i = 0; i < index; i++)
        x = x.next;
    return x;
}
```

### LinkedList java 구현 5 - add

이제 node 메소드를 이용해서 특정 위치에 노드를 추가하는 메소드를 만들어보겠다. 

```java
public void add(int k, Object input){
    // 만약 k가 0이라면 첫번째 노드에 추가하는 것이기 때문에 
    //addFirst를 사
    if(k == 0){
        addFirst(input);
    } else {
        Node temp1 = node(k-1);
        // k 번째 노드를 temp2로 지정
        Node temp2 = temp1.next;
        // 새로운 노드를 생성
        Node newNode = new Node(input);
        // temp1의 다음 노드로 새로운 노드를 지정
        temp1.next = newNode;
        // 새로운 노드의 다음 노드로 temp2를 지정
        newNode.next = temp2;
        size++;
        // 새로운 노드의 다음 노드가 없다면 
        // 새로운 노드가 마지막 노드이기 때문에 tail로 지정
        if(newNode.next == null){
            tail = newNode;
        }
    }
}
```

### LinkedList java 구현 6 - toString

지금까지는 데이터를 추가하는 방법을 알아보았다. 이제는 제대로 데이터가 추가되고 있는지 확인하는 것이 필요하다. LinkedList의 toString 메소드를 구현해서 리스트가 제대로 만들어지고 있는지 확인하는 코드를 작성해보자. 

```java
public String toString() {
    // 노드가 없다면 []를 리턴
    if(head == null){
        return "[]";
    }       
    // 탐색을 시작
    Node temp = head;
    String str = "[";
    // 다음 노드가 없을 때까지 반복문을 실행
    // 마지막 노드는 다음 노드가 없기 때문에 
    //아래의 구문은 마지막 노드가 제외된다.
    while(temp.next != null){
        str += temp.data + ",";
        temp = temp.next;
    }
    //따라 마지막 노드를 출력결과에 포함
    str += temp.data;
    return str+"]";
}
```

### LinkedList java 구현 7 - removeFirst

```java
public Object removeFirst(){
    // 첫번째 노드를 temp로 지정하고 
    //head의 값을 두번째 노드로 변경
    Node temp = head;
    head = temp.next;
    // 데이터를 삭제하기 전에 리턴할 값을 임시 변수에 담는다. 
    Object returnData = temp.data;
    temp = null;
    size--;
    return returnData;
}
```

### LinkedList java 구현 8 - remove, removeLast

```java
public Object remove(int k){
    if(k == 0)
        return removeFirst();
    // k-1번째 노드를 temp의 값으로 지정
    Node temp = node(k-1);
    // 삭제 노드를 todoDeleted에 기록
    // 삭제 노드를 지금 제거하면 삭제 앞 노드와 삭제 뒤 노드를 
    //연결할 수 없다.  
    Node todoDeleted = temp.next;
    // 삭제 앞 노드의 다음 노드로 삭제 뒤 노드를 지정
    temp.next = temp.next.next;
// 삭제된 데이터를 리턴하기 위해서 returnData에 데이터를 저장
    Object returnData = todoDeleted.data; 
    if(todoDeleted == tail){
        tail = temp;
    }
    // temp.next를 삭제 
    todoDeleted = null; 
    size--;
    return returnData;
}

public Object removeLast(){
    return remove(size - 1);
}
```

### LinkedList java 구현 9 - size, get

엘리먼트의 크기를 알아내는 법은 간단하다. 내부적으로 size라는 값을 유지하고 있기 때문에 이 값을 돌려주기만 하면 된다. 

```java
public int size() {
    return size;
}

public Object get(int k){
    Node temp = node(k);
    return temp.data;
}
```

### LinkedList java 구현 10 - indexOf

특정한 값을 가진 엘리먼트의 인덱스 값을 알아내는 방법을 알아보자. 값이 있다면 그 값이 발견되는 첫번째 인덱스 값을 리턴하고, 값이 없다면 -1을 리턴한다. 

```java
public int indexOf(Object data){
    // 탐색 대상이 되는 노드를 temp로 지정
    Node temp = head;
    // 탐색 대상이 몇번째 엘리먼트에 있는지를 의미하는 변수로 
    //index를 사용
    int index = 0;
    // 탐색 값과 탐색 대상의 값을 비교 
    while(temp.data != data){
        temp = temp.next;
        index++;
        // temp의 값이 null이라는 것은 더 이상 탐색 대상이 
        //없다는 것을 의미합니다. 이 때 -1을 리턴
        if(temp == null)
            return -1;
    }
    // 탐색 대상을 찾았다면 대상의 인덱스 값을 리턴
    return index;
}
```



  

### 



#### 

#### 



#### 



