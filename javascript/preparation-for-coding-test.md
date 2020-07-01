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

## 



