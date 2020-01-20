# ArrayList

## ArrayList

* 리스트를 만들 때, 그 내부적으로 배열을 사용하는 것 
* 배열의 특성상 데이터를 리스트의 처음이나 간에 저장하면,  이후의 데이터들이 한칸씩 뒤로 물러나야 한다. 따라서 시간이 많이 소요된다는 것이 단점
* 하지만, 데이터를 가져올 때, 인덱스를 이용하여 접근하기 때문에 빠르게 가져올 수 있다는 것이 장점. 

### Java에서 ArrayList 사용법

java에는 기본적으로 ArrayList가 내장되어 있다. 그래서 사용법을 아는 것이 중요하다. 

* 생성

ArrayList를 사용하기 위해서는 먼저 ArrayList 객체를 만들어야 한다.  또, ArrayList는 java.util.ArrayList에 포함되어 있기 때문에 import를 해줘야 한다. 

```java
import java.util.ArrayList; 
ArrayList<Integer> numbers = new ArrayList<>(); 
```

* 추가

add 메소드를 사용한다. 또, 특정 위치에 추가하고 싶다면 add의 첫번째 인자로 인덱스를 지정하면 된다.

```java
numbers.add(10);
numbers.add(20);
...
numbers.add(1, 50); //1번째 인덱스에 50을 추가하겠다는 
```

\*자바의 배열은 크기가 고정되어 있다. 데이터를 추가하는 과정에서 내부적으로 사용하는 배열이 꽉차면 기존의 배열 대비 크기가 2배 큰 새로운 배열을 만들고, 기존의 데이터를 새로운 배열로 복제한다. 덕분에 프로그래머는 ArrayList의 크기에 신경쓰지 않고 편리하게 프로그램을 만들 수 있다. 

* 삭제

특정 인덱스에 위치하는 엘리먼트를 삭제할때는 remove를 사용한다.

```java
numbers.remove(2); //2번째 인덱스 엘리먼트를 삭제한다는 뜻 
```

* 가져오기

엘리먼트를 가져올 때는 get을 사용한다. 

```java
numbers.get(2); //2번째 인덱스의 엘리먼트를 가져온다는 뜻 
```

* 반

자바에서는 ArrayList를 탐색하기 위한 방법으로 iterator를 제공한다. 이는 주로 객체지향 프로그래밍에서 사용하는 기법이다. 우선 iterator 객체를 만들어야 한다. 

```java
Iterator it<Integer> = numbers.iterator();
```

 Iterator 객체는 numbers 객체 내부에 저장된 값을 하나씩 순회하면서 탐색할 수 있도록 돕는 객체이다.  it.next\(\) 메소드를 호출할 때마다 엘리먼트를 순서대로 리턴한다. 만약, 더 이상 순회할 엘리먼트가 없다면 it.hasNext\(\)의 값은 false가 되면서 while문이 종료된다. 

```java
while(it.hasNext()){
 System.out.println(it.next());
}

//조금 더 편리한 방법도 있다
for(int value : numbers){
 System.out.println(value);
}

```

 단순 출력을 위해서만 순회를 하지는 않는다. 순회 과정에서 필요에 따라서는 엘리먼트를 삭제, 추가 하는 작업을 해야할 것이다. 그런 경우 아래와 같이 처리할 수 있다. 

```java
while(it.hasNext()){
 int value = it.next();
 if(value == 30){
//it.next()를 통해서 반환된 numbers의 엘리먼트를 삭제하라는 명령 
    it.remove(); 
  }
}
```

### ArrayList 구현 1 - 객체 생성 

우선, ArrayList라는 이름의 객체를 만든다. 

* ArrayList.java

```java
package list.arraylist.implementation;
 
public class ArrayList {
//현 리스트에 장되어 있는 데이터의 개수, size가 0이라는 뜻 
    private int size = 0;
//object 타입의 private한 배열 elementData는 최대 100개까지 수용 가능하다 
    private Object[] elementData = new Object[100];
}
```

* Main.java

```java
package list.arraylist.implementation;
 
public class Main {

    public static void main(String[] args) {
    
        ArrayList numbers = new ArrayList();
        
    }
    
}
```

### ArrayList 구현 2 - addLast

데이터를 마지막 위치에 추가하는 메소드의 구현은 아래와 같다. 

```java
public boolean addLast(Object element) {
//현재 elementData에 저장되어 있는 데이터의 개수 뒤 인덱스에 element가 추가된다. 
//즉, 리스트의 마지막 위치에 데이터를 추가하는 과정이다. 
    elementData[size] = element;
//데이터를 추가한 후에는 size를 1 증가해준다. 
    size++;
    return true;
}
```

Main.java에서 위의 메소드를 사용해보자.

```java
public static void main(String[] args) {
    ArrayList numbers = new ArrayList();
    numbers.addLast(10);
    numbers.addLast(20);
    numbers.addLast(30);
    numbers.addLast(40);
}
```

### ArrayList 구현 3 - add

데이터를 중간에 추가하는 로직은 조금 더 복잡하다. 데이터를 추가할 빈공간을 확보해야 하기 때문이다. 엘리먼트의 이동을 코드로 표현하는 것이 처음에는 쉽지 않다. 아래 그림을 보도록 하자. 

그림에 표시된 숫자의 순서대로 엘리먼트를 왼쪽에서 오른쪽으로 옮겨야 한다. 이때 가장 중요한 것은 반복조건을 헷갈리지 않는 것이다. 반복문을 만들때는 시작과 끝을 잘 파악하는 것이 중요하다.

* 시작: 반복작업이 시작되는 인덱스, size - 1이다.
* 끝: 반복작업이 끝나는 인덱스, 중간 추가를 하려고 했던 인덱스 값이다. 
* 반복작업: i--

![](../.gitbook/assets/image%20%2812%29.png)

그럼 이제 전체 코드를 보자.

```java
public boolean add(int index, Object element) {
// 엘리먼트 중간에 데이터를 추가하기 위해서는 끝의 엘리먼트부터
//index의 노드까지 뒤로 한칸씩 이동시켜야 합니다.
    for (int i = size - 1; i >= index; i--) {
        elementData[i + 1] = elementData[i];
    }
    // index에 노드를 추가합니다.
    elementData[index] = element;
    // 엘리먼트의 숫자를 1 증가 시킵니다.
    size++;
    return true;
}
```

데이터를 처음에 추가하는 메소드의 구현은 아래와 같다. 

```java
public boolean addFirst(Object element){
    return add(0, element);
}
```

### ArrayList 구현 4 - toString

데이터를 확인하기 위해서 toString 객체를 상속해서 구현해보도록 하자. 

```java
public String toString(){
    String str = "[";
    for(int i=0; i < size; i++){
        str += elementData[i];
        //마지막 엘리먼트 뒤에는 ,를 추가하지 않기 위해 
        if(i < size-1){
            str += ",";
        }
    }
    return str + "]";
}
```

이제, Main.java에서 아래와 같은 코드를 실행하면 리스트의 엘리먼트를 쉽게 파악할 수 있다. 

```java
public static void main(String[] args) {
    ArrayList numbers = new ArrayList();
    numbers.addLast(10);
    numbers.addLast(20);
    numbers.addLast(30);
    numbers.addLast(40);
    numbers.add(1, 15);
    numbers.addFirst(5);
    System.out.println(numbers);
}
```

출력값은 아래와 같다.

```java
[5,10,15,20,30,40]
```

### ArrayList 구현 5 - remove

데이터를 삭제하는 것은 중간에 추가하는 것과 유사하다. 다음 그림을 보도록 하자. 그림에 나타난것처럼 엘리먼트를 삭제할 때는 뒤에 있는 엘리먼트를 한칸씩 전진시킨다. 이때, 시작과 끝을 잘 파악하는 것이 중요한데, 시작은 삭제할 인덱스의 다음 인덱스이며, 끝은 size - 1이다. 그리고 엘리먼트를 옮기는 작업이 끝난 후에는 size의 값을 1 감소시키고, 마지막 엘리먼트도 삭제해다. 

![](../.gitbook/assets/image%20%2816%29.png)

코드를 보도록 하자.

```java
public Object remove(int index) {
// 엘리먼트를 삭제하기 전에 삭제할 데이터를 removed 변수에 저
    Object removed = elementData[index];
// 삭제된 엘리먼트 다음 엘리먼트부터 마지막 엘리먼트까지 
// 순차적으로 이동해서 빈자리를 채다.
    for (int i = index + 1; i <= size - 1; i++) {
        elementData[i - 1] = elementData[i];
    }
    // 크기를 줄다.
    size--;
    // 마지막 위치의 엘리먼트를 명시적으로 삭제해다. 
    elementData[size] = null;
    return removed;
}   
```

Main.java 코드는 다음과 같을 때, 

```java
ArrayList numbers = new ArrayList();
numbers.addLast(10);
numbers.addLast(15);
numbers.addLast(20);
numbers.addLast(30);
numbers.remove(1);
System.out.println(numbers);
```

결과는 다음과 같다. 

```java
[10,20,30]
```

### ArrayList 구현 6 - remove first last

처음과 끝 엘리먼트를 지우는 것은 간단하다. remove 메소드를 이용하면 된다. 아래 코드를 보자.

```java
public Object removeFirst(){
    return remove(0);
}
 
public Object removeLast(){
    return remove(size-1);
}
```

Main.java 코드가 아래와 같을 때,

```java
ArrayList numbers = new ArrayList();
numbers.addLast(5);
numbers.addLast(10);
numbers.addLast(20);
numbers.addLast(30);
numbers.addLast(40);
numbers.removeFirst();
numbers.removeLast();
System.out.println(numbers);
```

결과는 다음과 같다. 

```java
[10,20,30]
```

### ArrayList 구현 7 - get

데이터를 가져오는 기능은 get이다. get은 인자로 전달된 인덱스 값을 그대로 배열로 전달한다. **배열은 메모리의 주소에 직접 접근하는 랜덤 엑세스**이기 때문에 매우 빠르게 처리된다. 

```java
public Object get(int index) {
    return elementData[index];
}
```

```java
ArrayList numbers = new ArrayList();
numbers.addLast(10);
numbers.addLast(20);
numbers.addLast(30);
numbers.addLast(40);
System.out.println(numbers.get(0));
System.out.println(numbers.get(1));
System.out.println(numbers.get(2));
```

```java
10
20
30
```

### ArrayList 구현 8 - size, indexOf

엘리먼트의 크기를 알아내는 법은 간단하다. 내부적으로 size라는 값을 유지하고 있기 때문에 이 값을 돌려주기만 하면 된다. 

```java
public int size() {
    return size;
}
```

특정한 값을 가진 엘리먼트의 인덱스 값을 알아내는 방법을 알아보자. 값이 있다면 그 값이 발견되는 첫번째 인덱스 값을 리턴하고, 값이 없다면 -1을 리턴한다.  

```java
public Object indexOf(Object o){
    for(int i=0; i < size; i++){
        if(o.equals(elementData[i])){
            return i;
        }
    }
    return -1;
}
```

```java
ArrayList numbers = new ArrayList();
numbers.addLast(10);
numbers.addLast(20);
numbers.addLast(30);
System.out.println(numbers.indexOf(20));
System.out.println(numbers.indexOf(40));
```

```java
1
-1
```

### ArrayList 구현 9 - Iterator next, hasNext

```java
ArrayList.ListIterator it = numbers.listIterator();
while (it.hasNext()) {
    int value = (int) it.next();
    System.out.println(value);
}
```

위의 코드는 ListIterator라는 객체를 이용한 방법이다. ListIterator 객체는 반복 작업을 위해서 고안된 것이다. 이 객체를 만드는 방법은 ArrayList의 listIterator 메소드를 호출하는 것이다. 우선 이 메소드를 만드는 코드를 보자. 

```java
public ListIterator listIterator() {
    // ListIterator 인스턴스를 생성해서 리턴합니다.
    return new ListIterator();
} 
```

아래는 ListIterator 클래스이다. 

```java
public class ListIterator {
    // 현재 탐색하고 있는 순서를 가르키는 인덱스 값
    private int nextIndex = 0;
 
    // next 메소드를 호출할 수 있는지를 체크합니다.
    public boolean hasNext() {
    // nextIndex가 엘리먼트의 숫자보다 적다면 next를 이용해서 
    //탐색할 엘리먼트가 존재하는 것이기 때문에 true를 리턴합니다. 
        return nextIndex < size();
    }
     
    // 순차적으로 엘리먼트를 탐색해서 리턴합니다. 
    public Object next() {
       // nextIndex에 해당하는 엘리먼트를 리턴하고 
       // nextIndex의 값을 1 증가 시킵니다.
        return elementData[nextIndex++];
    }
}
```

### ArrayList 구현 10 - Iterator previous, hasPrevious

```java
// previous 메소드를 호출해도 되는지를 체크합니다.
public boolean hasPrevious(){
    // nextIndex가 0보다 크다면 이전 엘리먼트가 
    //존재한다는 의미입니다.
    return nextIndex > 0;
}
 
// 순차적으로 이전 노드를 리턴합니다.
public Object previous(){
    // 이전 엘리먼트를 리턴하고 nextIndex의 값을 
    // 1 감소합니다. 
    return elementData[--nextIndex];
}
```

### ArrayList 구현 11 - Iterator add, remove

```java
// 현재 엘리먼트를 추가합니다. 
public void add(Object element){
    ArrayList.this.add(nextIndex++, element);
}
 
// 현재 엘리먼트를 삭제합니다. 
public void remove(){
    ArrayList.this.remove(nextIndex-1);
    nextIndex--;
}
```

#### 

