# Stric mode

## strict mode란❓

자바스크립트 언어의 문법을 좀 더 엄격히 적용하여 오류를 발생시킬 가능성이 높거나 자바스크립트 엔진의 최적화 작업에 문제를 일으킬 수 있는 코드에 명시적인 에러를 발생시킨다.

### 1. 전역 strict mode

```jsx
"use strict";

function foo() {
  x = 10; // ReferenceError: x is not defined
}
foo();
```

전역에 `strict mode` 를 선언하게되면 전체 스크립트에 엄격모드가 적용이된다. 함수 내부에서 x를 참조 시 `strict mode` 가 없었다면 암묵적 전역 상태로 x는 글로벌 객체의 프로퍼티가 되지만 `strict mode` 에서는 명시적인 에러를 발생시킨다.

### 2. 함수 strict mode

```jsx
function foo() {
  "use strict";
  x = 10; // ReferenceError: x is not defined
}
foo();
```

`strict mode` 범위를 제한하고 싶다면 함수 내부에서 `strict mode` 를 사용할 수 있다.

---

# 어떤 방식을 피해야되는지 알아보자.

## 전역에 strict mode를 피하자

```jsx
<!DOCTYPE html>
<html lang="ko">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=], initial-scale=1.0">
  <title>Document</title>
</head>

<body>
</body>
<script>
  'use strict'
</script>
<script>
  y = 1;
</script>

</html>
```

`strict mode` 는 스크립트 단위로 적용이 된다. `strict mode` 와 `non-strict mode` 스크립트를 혼용해서 사용하면 오류가 발생할 수도있다. 그리고 써드 파티 라이브러리 대부분은 `non-strict mode` 이기 때문에 전역에 `strict mode` 를 사용하는건 지양해야된다.

## 함수 단위로 strict mode를 적용하는 것을 피하자

```jsx
(function () {
  var let = 10;

  function foo() {
    "use strict";
    let = 20; // SyntaxError: Unexpected strict mode reserved word
  }
  foo();
})();
```

어는 함수는 `strict mode` 다른 함수는 `non strict mode` 이런 통일 없이 사용하는 것은 지양해야된다. 하지만 모든 함수에 `strict mode` 를 적용하는 것도 번거로운 일이다. 중첩 함수 내부에서는 `strict mode` 를 사용하지만 상위 함수에서는 안쓰면 문제가 발생한다.

따라서 `strict mode` 는 즉시 실행 함수로 감싼 스크립트 단위로 관리하는게 바림직하다.

---

## strict mode가 발생시키는 에러들

1. **암묵적 전역**

```jsx
(function () {
  "use strict";
  x = 10;
  console.log(x); // ReferenceError: x is not defined
})();
```

암묵전 전역상태를 방지하고 `에러`를 발생 시킨다.

1. **변수, 함수, 매개변수 삭제**

```jsx
(function () {
  "use strict";
  var x = 10;
  delete x;
  function foo(a) {
    delete a;
  }
  delete foo;
})();
```

delete연산자로 삭제하는걸 방지하고 `문법 에러`를 발생시킨다.

1. **매개변수 이름의 중복**

```jsx
(function () {
  "use strict";
  // SyntaxError: Duplicate parameter name not allowed in this context
  function foo(a, a) {
    return a + a;
  }
  console.log(foo(1, 2));
})();
```

중복된 매개변수 이름 사용을 방지해준다.

1. **with문의 사용**

```jsx
(function () {
  "use strict";
  with ({ x: 1 }) {
    console.log(x);
  }
})();
```

strict 모드에서는 with문을 사용하지 못하게한다. 코드는 간단하지만 성능과 가독성이 나빠지는 문제 때문이다.

---

## strict mode 적용에 의한 변화

1. **일반 함수의 this**

```jsx
(function () {
  "use strict";
  function foo() {
    console.log(this); // undefined
  }
  foo();
})();
```

일반 함수로 호출 시 `this` 는 `전역 객체`를 바인딩한다. `strict mode` 에서는 `undefined` 가 바인딩된다.

1. **arguments 객체**

```jsx
(function (a) {
  "use strict";
  a = 2;
  console.log(arguments); // [Arguments] { '0': 3 }
})(3);
```

매개변수를 재할당하여 변경해도 `arguments` 객체에는 반영되지 않는다.
