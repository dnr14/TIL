### var 키워드로 선언한 변수의 문제점

😣 **변수 중복 선언 허용**

```jsx
var x = 1;
var y = 2;

var x = 100;
var y;

console.log(x); // 100
console.log(y); // 2
```

var 키워드는 중복 선언과 할당이 가능하다. 이때 에러는 발생하지 않는다. 개발자가 의도치 않게 값이 변경되어 부작용이 발생할 수 있다.

😣 **함수 레벨 스코프**

```jsx
var x = 1;

if (true) {
  var x = 10;
}

console.log(x);
```

var 키워드는 함수 레벨 스코프를 따른다. 함수 안에서만 `지역 스코프`로 인정한다. 블록에서 동일한 이름은 선언하고 할당하면 에러는 발생하지 않고 값이 변경된다. `x변수` 는 전역 변수이다.

😣 **변수 호이스팅**

```jsx
console.log(foo); // undefined

foo = 123;

console.log(foo); // 123

var foo;
```

var 키워드는 `변수 호이스팅`이 발생한다. 런타임 이전에 미리 선언과 초기화가 되어서 선언문에 도달하기 전에도 참조가 가능하다. 하지만 할당문 이전에 참조를 하면 항상 `undefined` 이다.

선언문 전에 참조는 가능하고 에러는 발생 시키지 않지만 코드 흐름상 맞지 않아 개발자의 가독성을 떨어트린다.

---

### let 키워드

😃 **변수 중복 선언 금지**

```jsx
let bar = 123;
let bar = 456; // SyntaxError: Identifier 'bar' has already been declared
```

let 키워드는 재할당은 가능하지만 `재 선언`은 금지된 키워드 입니다. 재 선언을 하게되면 `문법에러`를 발생 시킵니다.

😃 **블록 레벨 스코프**

```jsx
let bar = 123;

if (true) {
  let bar = 456;
  console.log(bar); // 456
}
console.log(bar); // 123
```

let 키워드는 블록 레벨 스코프이다. `블록 스코프`만 지역 스코프로 인정한다. 블록 스코프안의 bar변수와 전역 스코프에 bar변수는 서로 지역이 달라 별개의 변수이다. 함수도 블록이므로 스코프를 만들며 let키워드도 지역변수이다.

😃 **변수 호이스팅**

```jsx
console.log(foo); // ReferenceError: Cannot access 'foo' before initialization
// TDZ 발생

let foo;
console.log(foo); // undefined

foo = 123;
console.log(foo); // 123
```

let 키워드도 호이스팅이 발생한다. var 키워드 처럼 선언단계와 초기화 단계가 한번에 진행이 안되고

선언 단계와 초기화 단계가 분리되어 진행이 된다. 초기화 단계에 변수를 참조할려고 하면 `참조 에러` 가 발생한다. 스코프의 시작 지점 부터 초기화 시작 지점까지 변수를 참조할 수 없는 구간을 `일시적 사각지대` 라고 부른다.

😃 **전역 객체와 let**

```jsx
let x = 1;

console.log(window.x); // undefined
console.log(x); // 1
```

let 키워드는 전역에 선언하여도 `전역 변수`가 아니다.

---

### const 키워드

😃 **선언과 초기화**

```jsx
const foo = 1;
const bar; // SyntaxError: Missing initializer in const declaration
bar = 1;

{
  console.log(foo); // ReferenceError: Cannot access 'foo' before initialization
  const foo = 1;
}
```

const 키워드는 선언과 할당을 동시에 해야된다. 따로하게 되면 `문법 에러` 가 발생한다.

const 키워드도 `변수 호이스팅`이 발생한다. let 키워드와 마찬가지로 `블록 레벨 스코프`를 가진다.

let 키워드와 동일하게 초기화문에 도착하기 전에 참조를 하면 `TDZ` 에 걸려서 참조 에러를 발생 시킨다

😃 **재할당 금지**

```jsx
const foo = 1;
foo = 12; // TypeError: Assignment to constant variable.
```

const 키워드로 선언한 변수는 재할당이 금지 된다. 재할당 시 에러를 발생 시킨다.

😃 **상수**

```jsx
const TAX_RATE = 0.1;

let preTaxPrice = 100;

let afterTaxPrice = preTaxPrice + preTaxPrice * TAX_RATE;
console.log(afterTaxPrice); // 110;

const person = {
  name: "lee",
};
person.name = "kim";
console.log(person.name); // 'kim'
```

const 키워드는 재할당이 금지된 키워드로 `상수` 라는 표현도 쓴다. const 키워드에 원시 값을 할당하면 `불변` 하고 `재할당도 금지`므로 할당된 값을 변경할 수 있는 방법은 없다.

하지만 `객체 타입`을 할당하면 값은 변할 수 있다. 재할당 금지할 뿐 `불변` 을 의미 하지 않는다. const 키워드의 상수 개념은 `메모리 주소`를 더 이상 변경을 못한다는 의미이다.

---
