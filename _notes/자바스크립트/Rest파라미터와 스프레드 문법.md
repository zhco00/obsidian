
# Rest 파라미터 

Rest파라미터는 매개변수 이름 앞에 `...`을 붙여서 정의한 매개변수이다.
- Rest파라미터는 함수에 전달된 **인수**들을 **배열**의 형태로 전달받는다.

```
function foo(x, y, ...z){
  console.log(x, y); // 1 2
  console.log(z); // [3, 4, 5]
}
foo(1, 2, 3, 4, 5);
```
foo에서 1,2,3,4,5를 넣어주고 x와y는 1,2를 받는다. 그리고 z는 나머지 3,4,5를 받는다.

Rest파라미터는 남은 인수들을 배열로 만들어 주는 것이기 때문에 Rest파라미터가 다른 것보다 앞에 오면 안된다.

```
function foo(...z,x,y){   //SyntaxError: Rest parameter must be last formal parameter
console.log(x,y);
console.log(z);
}
foo(1,2,3,4,5)

```

이런식으로 하나만 있을 경우에는 인수 전부가 z에 들어간다.
```
function foo(...z){
  console.log(z); // [1, 2, 3, 4, 5]
}
foo(1, 2, 3, 4, 5);
```

주의 해야할 점은 ==Rest파라미터는 매개변수로 밖에 쓸 수 없다는 점이다.==


# 스프레드 문법

스프레드 문법은 Rest파라미터와 반대로 ...을 통해 하나로 뭉쳐있는 여러 값들의 집합을 펼쳐서 개별적인 값들로 만드는 것이다. 
```
function foo(...z){
  console.log(z); // [1, 2, 3, 4, 5]
  console.log(...z); // 1 2 3 4 5
  console.log(z); // [1, 2, 3, 4, 5]
}
foo(1, 2, 3, 4, 5);
```
위의 ...z를 통해 배열 값인 z를 풀어서 1 2 3 4 5로 보여준 것이다. 물론 개별적인 값으로 고정되는 것은 아니기 때문에 다시 한번 console로 z를 찍었을 때는 다시 배열 형태로 나온다. 
스프레드 문법을 통해 나온 결과는 값이 아니고 보여주는것이라고만 생각하면 될 것 같다.
그렇기 때문에 스프레드 문법을 통해 나온 결과는 값으로 사용할 수 없다.

```
const list = ...[1, 2, 3] //SyntaxError: Unexpected token '...'
```

스프레드 문법은  for...of 문으로 순회할 수 있는 이터러블(Array, Map, String, Set 등)에 한정된다.

```
const arr = [1, 2, 3];
const max = Math.max(...arr);
console.log(max);  //3


const arr = [...[1, 2], ...[3, 4]];
console.log(arr); // [1, 2, 3, 4]


const arr1 = [1, 4]
const arr2 = [2, 3]
arr1.splice(1, 0, ...arr2)
console.log(arr1) // [1, 2, 3, 4]


const origin = [1, 2]
const copy = [...origin]
const copy1 = origin
console.log(copy) // [1, 2]
console.log(copy === origin) // false   얕은 복사
console.log(copy1 === origin) // true   깊은 복사


const sum = (...args) => { args.reduce((acc, val) => acc + val, 0) }
console.log(sum(1, 2, 3, 4, 5)) // 15 


const merged = { ...{ x: 1, y: 2 }, ...{ y: 3, z: 4 } };
console.log(merged); // { x: 1, y: 3, z: 4 }

```
이런식으로도 활용할 수 있다.

