## Set

set객체는 중복되지 않는 유일한 값들의 집합이다. Set은 배열과 비슷하지만 약간의 차이가 있다.
1. 동일한 값을 중복하여 포함할 수 없다. 
2. 들어간 순서에 의미가 없다.
3. 즉 인덱스가 존재하지 않는다.
 
==Set객체는 Set 생성자 함수로 생성하고 이터러블을 인수로 전달받아 Set객체를 생성한다.==

```
const set = new Set()
console.log(set) // Set(0)

const set1=new Set([1,2,3,4])
console.log(set1) // Set(4) {1,2,3,4}

const set2=new Set('hello')
console.log(set1) // Set(5) {'h' ,'e', 'l', 'o'}
```
set을 사용하면 중복된 값을 제거할 때 편하다.

#### 요소의 확인, 추가, 삭제 방법들
```
** 요소 갯수 확인**
const {size} =new Set([1,2,2,3])
console.log(size) //3

** 추가 삭제 방법**
const set= new Set()
console.log(set) //set(0) {}
set.add(1)
console.log(set) //set(1) {1}
set.add(2).add(3)
console.log(set) //set(3) {1,2,3}
//NaN과 +0,-0도 중복추가를 허용하지 않는다.

set.delete(3)
console.log(set) // Set(2) {1,2}
// Set은 인덱스를 갖지 않기 때문에 요소값을 통해 삭제를 할 수 있다.
// add메서드는 연속 호출이 가능하지만 delete는 연속호출이 불가능 하다.


** 요소 존재 여부 확인 **
console.log(set.has(1)) // true
console.log(set.has(1,2)) // true
console.log(set.has(4)) // true
// has메서드도 delete와 마찬가지로 중복 호출이 불가능하다.

** 요소 일괄 삭제 **
set.clear()
console.log(set)  //set(0) {}
```

#### 요소 순회
Set 객체는 forEach, for ... of, 스프레드 문법, 디스트럭처링 할당 모두 가능하다.

forEach는 Set.prototype.forEach를 사용하는데 이는 Array.prototype.forEach와 유사하게
콜백 함수와 forEach 메서드의 콜백 함수 내부에서 this로 사용될 객체를 인수로 전달 받는다고 한다.

forEach문은 3개의 인수를 전달받는다.
1. 현재 순회 중인 요소 값
2. 현재 순회 중인 요소의 인덱스 값
3. 현재 순회 중인 Set 객체 자체

==하지만 Set에는 인덱스가 없기 때문에 2번을 생략해야 하지만 모든 forEach문의 인터페이스를 통일하기 위해서 인덱스 값 대신 1번 값을 한번 더 전달 받는다 .==
즉 
1. 현재 순회 중인 요소 값
2. 현재 순회 중인 요소 값
3. 현재 순회 중인 Set 객체 자체
이렇게 전달 받는다.
```
const set =new Set([1,2,3])

set.forEach((v,v2,set))=> console.log(v,v2,set)
/*
1 1 Set(3) { 1, 2, 3 }
2 2 Set(3) { 1, 2, 3 }
3 3 Set(3) { 1, 2, 3 }
*/

for const value of set{
console.log(value) //1 2 3
}

console.log(...set) // 1 2 3

const [a,...rest] = set
console.log(a, rest) // 1, [2,3]

```
set객체는 요소의 순서는 존재하지 않지만 Set객체를 순회하는 순서는 요소가 추가된 순서를 따른다.
이는 ECMAScript에 규정되어 있지는 않지만 다른 이터러블의 순회와 호환성을 유지하기 위함이라고 한다.

#### 순서대로 추가된다면 인덱스를 추가하면 안되나?
이러한 궁금증이 생겼고 약간의 조사와 책, gpt를 사용한 결과 정확하진 않지만 이러한 결과를 얻었다.

Set에 인덱스가 없는 이유는 Set의 목적과 특성 때문이다. 
Set은 고유한 값을 저장하는 데이터 구조로써, 순서에 기반하지 않고 값의 중복을 허용하지 않는 집합의 개념을 따른다.
==Set은 수학적 집합을 구현하기 위한 자료구조이기 때문이다.== 라는 결과를 얻을 수 있었다.

set은 집합을 위한 자료구조인데 집합에서는 순서와 상관없이 집합에 포함되어있는지 안되어 있는 지를 따지는 것이고 그렇기 때문에 중복되는 값은 삭제 되는 것 같다.
set의 목적은 고유한 값을 저장하고 관리하는 것이 주요 목적이라고 한다.  - 챗 GPT

## Map

Map객체는 키와 값의 쌍으로 이루어진 컬렉션이다. Map은 객체와 유사하지만 약간의 차이가 있다.
1. 객체를 포함한 모든 값을 키로 사용할 수 있다. 
2. 이터러블이다.
3. map.size를 통해 요소의 개수를 확인 할 수 있다.
 
==Map 객체는  Map 생성자 함수로 생성하고 이터러블을 인수로 전달받아 Map객체를 생성한다. 이때 인수인 이터러블은 키와 값으로 이루어져 있어야 한다.==

```
const map = new Map()
console.log(map) //Map(0) {}

const map1 = new Map([['key1','value1'] , ['key2', 'value2']])
console.log(map1) //Map(2) {'key1' => 'value1', 'key2' => 'value2'}

const map2 = new Map([1, 2]); //Iterator value 1 is not an entry object
```

#### 요소의 확인, 추가, 삭제 방법들
Map함수도 Set함수와 대부분 비슷하여 다른 부분만 작성해보자

```
** 요소 추가 **
const map = new Map()
console.log(map) //Map() {}

map.set('key1', 'value1').set('key2', 'value2')
console.log(map) //Map(2) {'key1' => 'value1', 'key2' => 'value2'}
// 객체에는 중복된 키를 갖는 요소가 존재할 수 없어서 중복된 키를 갖는 요소를 추가하면 값이 덮어 써짐


** 요소 취득 **
const map1 = new Map()
const lee = {name : 'LEE'}
const kim = {name : 'KIM'}

map.set(lee, 'developer').set(kim, 'designer')
console.log(map.get(lee)) // developer
console.log(map.get(kim)) // designer
// get을 써서 특정 요소를 취득할 수 있다.
// get메서드의 인수로 키를 전달하면 Map객체에서 인수로 전달한 키를 갖는 값을 반환한다.
```
Map객체는 키 타입에 제한이 없다. 따라서 객체를 포함한 모든 값을 키로 사용할 수 있다.

#### 요소 순회
요소 순회도 set과 거의 비슷하다.

다른 점 중 하나는 forEach문dml 2번째 인수이다.
1. 현재 순회 중인 요소 값
2. 현재 순회 중인 요소 키
3. 현재 순회 중인 Map 객체 자체
로 forEach의 인터페이스를 통일하기 위함인지 값이 먼저 나오고 키가 나온다.

```
const lee = { name: "LEE" };
const kim = { name: "KIM" };

const map = new Map([
  ["LEE", "developer"],
  ["KIM", "designer"],
]);
map.forEach((v, k, map) => console.log(v, k, map));

/*
developer LEE Map(2) {'LEE' => 'developer', 'KIM' => 'designer',}
designer KIM  Map(2) {'LEE' => 'developer', 'KIM' => 'designer',}
*/
```
Map도 마찬가지로 요소의 순서에 의미를 갖지 않지만 Map객체를 순회하는 순서는 요소가 추가된 순서를 따른다.
이는 ECMAScript에 규정되어 있지는 않지만 다른 이터러블의 순회와 호환성을 유지하기 위함이라고 한다.
