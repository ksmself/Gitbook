# Preparation for Coding Test

## 20.07.01

### Programmers Lv 1. 완주하지 못한 선수 

* filter: The **filter\(\)** method **creates a new array** with all elements that pass the test implemented by the provided function. 
* indexOf: The **indexOf\(\)** method returns the first index at which a given element can be found in the array, or -1 if it is not present. 
* splice: The **splice\(\)** method changes the contents of an array by removing or replacing existing elements and/or adding new elements in place. 
* 위의 메소드를 사용하여 문제는 맞추었지만, 효율성 기준을 통과하지 못했다. 어떻게든 풀기만 하면 될 줄 알았는데\(그다지 복잡하게 풀었다고 생각하지도 않았다.\) '효율성' 때문에 다음으로 넘어가지 못하고 있다. 난감하다. 

```javascript
//filter Example 
const words = ['spray', 'limit', 'elite', 'exuberant', 'destruction', 'present'];

const result = words.filter(word => word.length > 6);

console.log(result);
// expected output: Array ["exuberant", "destruction", "present"]

//indexOf Example 
const beasts = ['ant', 'bison', 'camel', 'duck', 'bison'];

console.log(beasts.indexOf('bison'));
// expected output: 1

// start from index 2
console.log(beasts.indexOf('bison', 2));
// expected output: 4

console.log(beasts.indexOf('giraffe'));
// expected output: -1

//splice Example 
const months = ['Jan', 'March', 'April', 'June'];
months.splice(1, 0, 'Feb');
// inserts at index 1
console.log(months);
// expected output: Array ["Jan", "Feb", "March", "April", "June"]

months.splice(4, 1, 'May');
// replaces 1 element at index 4
console.log(months);
// expected output: Array ["Jan", "Feb", "March", "April", "May"]
```

### Programmers Lv 1. 2016년 

* 2016년은 윤년이라고 할 때, 월에 해당하는 a와 일에 해당하는 b가 들어오면 무슨 요일인지 알려주는 함수 작성. 
* switch문을 사용하려고 했으나, 같은 case가 적용되는 month가 있어 한 번에 여러 개의 값을 처리하려고 했는데 잘 되지 않아서, if-else문을 사용해 해결함. 

## 20.07.02

### Programmers Lv 1. 나누어 떨어지는 숫자 배열 

* array의 각 element 중 divisor로 나누어 떨어지는 값을 오름차순으로 정렬한 배열을 반환하는 함수 작성. 
* sort: The **sort\(\)** method sorts the elements of an array in place and returns the sorted array. The default sort order is ascending, built upon converting the elements into strings, then comparing their sequences of UTF-16 code units values. 
* arr.sort\(**compareFunction**\): Specifies a function that defines the sort order. If omitted, the array elements are converted to strings, then sorted according to each character's Unicode code point value. **In a numeric sort, 9 comes before 80, but because numbers are converted to strings, "80" comes before "9" in the Unicode order**. All undefined elements are sorted to the end of the array. If **compareFunction\(a, b\) returns less than 0, sort a to an index lower than b**. 
* map 
* answer.length == 0 과 answer == \[ \]와의 차이?  답은, answer.length == 0으로 해야지만 맞출 수 있었다. 

### Programmers Lv 1. 가운데 글자 가져오기 

* 단어의 가운데 글자를 반환하는 함수. 단어의 길이가 짝수라면 가운데 두 글자를 반환. 
* 나누기 연산을 한 후, parseInt를 이용해야 정수로 변환됨 
* slice: The **slice\(\)** method **returns** a shallow copy of a portion of **an array** into a new array object selected from **start to end\(end not included\)** where start and end represent the index of items in that array. The original array will not be modified. 

## 20.07.03

### 부스트캠프 자가진단테스트 

배열을 처음부터 탐색하면서 중복횟수를 count하는 함수 작성. 

* 객체 Set: 데이터 타입 중 하나. 중복되는 값을 가지지 않는 리스트. 값의 순서가 존재하지 않음. 
* 객체 Map: 키-값 쌍을 저장. 각 쌍의 삽입 순서도 기억. 
* Map.prototype.set\(\): set\(\) 메서드는 Map 객체에서 주어진 키를 가진 요소를 추가하고, 이미 있다면 대체. 
* myMap.set\(key, value\); 에서 key는 Map에 추가하거나 변경할 요소의 키, value는 Map에 추가하거나 변경할 요소의 값 
* Map.prototype.get\(\): get\(\) 메서드는 Map 객체에서 지정한 요소를 회수. 

```javascript
//풀이방법 1 
function countOf(arr, value){
 var count = 0;
 arr.forEach(element => {
  if(element == value) count++; 
 }); 
 return count; 
}

function solution(arr){
 var answer = [];
 var set = new Set([]); 
 arr.forEach(element => {
  if(set.has(element)) return; 
  set.add(element); 
  count = countOf(arr, element); 
  if(count > 1) answer.push(count); 
 }); 
 if(answer.length == 0) answer.push(-1); 
 return answer;
}

//풀이방법 2 
function solution(arr){
 var answer = [];
 var map = new Map(); 
 arr.forEach(element => {
  if(map.has(element)){
   map.set(element, map.get(element) + 1); 
  }
  else{
   map.set(element, 1);
  }
 });
 map.forEach( value => {
  if(value > 1){
   answer.push(value);
  }
 });
 if(answer.length == 0) answer.push(-1); 
 return answer; 
}
```

## 20.07.06

### Programmers Lv 1. 핸드폰 번호 가리기 

* 길이가 4 이상 20 이하인 핸드폰 번호가 주어지면, 마지막 4자리를 제외한 나머지 숫자를 전부 \*으로 가린 문자열을 리턴하는 함수 작성. 
* \*으로 가릴 문자의 개수를 repeated라는 변수에 담음. 그리고 '\*'.repeat\(repeated\)를 통해 그 개수만큼 \*을 반복함 
* 필요한만큼 \*을 반복한 후, phone\_number.substr\(phone\_number.length-4, 4\)와 합침. substr의 첫번째 인자에는 substring을 시작할 인덱스를 넣어주고,  그 다음 인자에는 잘라낼 개수를 넣어준다. 

### Programmers Lv 2. 위장 

* \[\[yellow\_hat, headgear\], \[blue\_sunglasses, eyewear\], \[green\_turban, headgear\]\] 와 같이 옷이 주어졌을 때, 서로 다른 옷의 조합의 수를 리턴하는 함수 작성.
* 레벨 2가 처음이라 그런지, object 활용을 많이 안 해봐서 그랬는지 어느 정도 그림은 그려졌는데, 디테일에서 잘 구현되지 않아 아쉬웠다. 
* 우선, 같은 옷의 종류끼리 분류하기 위해 Object를 사용했다. obj에 이미 cloth\[1\]이 있으면, 즉, obj\[cloth\[1\]\]이 1보다 크거나 같으면, obj\[cloth\[1\]\] += 1;을 해주고, 아니면 obj\[cloth\[1\]\] = 1으로 설정했다. 
* 이제 분류를 마쳤기 때문에, value 값을 빼와 계산하는 작업만 해주면 되었다. n은 key를 나타낸다. 

```javascript
for(var n in obj){
        answer *= (obj[n] + 1);
    }
answer -= 1; 
```

## 20.07.08

### Programmers Lv 1. k번째 수 

* 배열 array의 i번째 숫자부터 j번째 숫자까지 자르고 정렬했을 때, k번째에 있는 수를 구하는 함수 
* 예를 들어, 2번째 숫자부터 5번째 숫자까지 자른다고 하면, index 상에서는 1번째 index부터 4번째 index까지 잘라야 하는 것이다. 따라서 slice를 이용하면 slice\(i - 1, j\)라고 해야 i-1 인덱스부터 j-1 인덱스까지 잘라진다. 

### Programmers Lv 1. 모의고사 

* 3명의 수포자가 특정 규칙을 가지고 처음부터 마지막문제까지 찍는다고 했을 때, 가장 많은 문제를 맞춘 사람이 누구인지 배열에 담아 return 하는 solution 함수 작성. 
* 어제 풀었을 때도 비슷한 방식으로 풀었지만, 어디가 잘못됐는지 찾아낼 수 없었다. 오늘은 코드 중간중간에 print문을 넣어서 어디가 잘못됐는지 확인해보니  정답과 비교할 배열이 완전히 비어있었다. 배열에 특정 element들을 추가한다는 의미로 concat을 사용했는데 잘 되지 않았다. \*이유는 **concat은 기존 배열을 변경하지 않는다. 추가된 새로운 배열을 반환**하기 때문에 코드블록의 line 13처럼 사용하면 arr1은 바뀌지 않고 여전히 \[\]이다. 바뀐 배열을 담을 변수를 새로 설정해 이용하거나, push를 이용하는 것이 방법이 되겠다. 
* concat과 push 비교: concat은 배열에 요소를 추가하거나 배열에 배열을 더하는 메서드, 비슷한 메서드로 push가 있는데 push는 배열을 이어붙일 때도 요소 한 개로서 붙인다. 

```javascript
var arr1 = ['a', 'b'];
var arr2 = ['c', 'd'];
arr = arr1.concat(arr2);
//['a', 'b', 'c', 'd']

var arr1 = ['a', 'b'];
var arr2 = ['c', 'd'];
arr = arr1.push(arr2);
//['a', 'b', ['c', 'd']];

var arr1 = [];
var arr2 = ['c', 'd'];
arr1.concat(arr2);
console.log(arr1);
//[]
```

### 

