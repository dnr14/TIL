# try/catch

# 😱 에러를 처리해야되는 이유

```jsx
console.log("start");

foo(); // foo 함수가 없어서 에러 발생!! 프로그램은 죽는다.

console.log("end");
```

에러가 발생하지 않고 코드를 작성하는 것은 `불가능`하다. 에러를 처리해야되는 이유는 에러가 발생되면 프로그램은 `강제 종료`가 된다.

에러를 처리하지 않아 프로그램이 꺼진다면 프로그램의 `사용성`과 `신뢰도`는 낮아질 것이다.

```jsx
try {
  console.log("start");

  foo(); // foo 함수가 없어서 에러 발생!! 프로그램은 죽는다.

  console.log("end");
} catch (error) {
  console.log("프로그램은 죽지 않아요!");
}
```

try/catch문을 사용해 발생한 에러를 대응 한다면 프로그램이 강제로 죽는 상황은 발생 하지 않는다.

---

# 🚀 try catch finally문

`try catch finally문`은 3개의 코드 블록으로 구성된다. fianlly문은 `선택`이다. 불필요하다면 생략이 가능하다.

```jsx
try {
  // 실행할 코드(에러가 발생할 가능성이 있는 코드)
} catch (error) {
  // try 코드 블록에서 에러가 발생하면 이 코드 블록의 코드가 실행된다.
  // error에는 try코드 블록에서 발생한 error 객체가 전달된다.
} finally {
  // 에러 발생과 상관없이 반드시 한 번 실행된다.
}
```

try 코드 블록이 실행이 된다. 실행 중 에러가 발생되면 try 코드 블록에서 발생한 에러는 catch문의 error변수에 전달되고 catch 코드 블록이 실행된다.

```jsx
try {
  console.log("start");

  foo(); // foo 함수가 없어서 에러 발생!! 프로그램은 죽는다.

  console.log("end");
} catch (error) {
  console.log("프로그램은 죽지 않아요!");
} finally {
  console.log("나는 성공 실패 상관없이 실행되요!!");
}
// start
// 프로그램은 죽지 않아요!
// 나는 성공 실패 상관없이 실행되요!!
```

finally 코드 블록은 에러 발생과 상관없이 반드시 `한 번 실행`된다.

---

# 🤖 Error 객체

자바스크립트에는 에러 객체가 있다. 빌트인 생성자 함수 중에 `Error 생성자 함수`가 있다.

```jsx
const error = new Error("invalid");
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bb51eddf-2b03-4579-9fb6-b8db24bbaee8/Untitled.png)

Error 생성자 함수는 에러 객체를 생성한다. 프로퍼티로 `message, stack`를 갖는다.

message의 값은 생성자 함수의 인수로 전달한 에러 메세지고, stack 값은 에러를 발생시킨 콜스택의 호출 정보를 나타내는 문자열이다.

```jsx
1 @ 1 // SyntaxError
foo(); // ReferenceError: foo is not defined
null.foo; // TypeError: Cannot read property 'foo' of null
new Array(-1); // RangeError: Invalid array length
decodeURIComponent("%"); // URIError: URI malformed
```

**Error 생성자 함수 뿐만 아니라 Error 객체를 포함한 7개의 에러 객체를 생성할 수 있다.**

| 생성자 함수    | 인스턴스                                                                       | 프로토타입      |
| -------------- | ------------------------------------------------------------------------------ | --------------- |
| Error          | 일반적인 에러 객체                                                             | Error.prototype |
| SyntaxError    | 자바스크립트 문법에 맞지 않는 문을 해석할 때 발생하는 에러 객체                | Error.prototype |
| ReferenceError | 참조할 수 없는 식별자를 참조했을 때 발생하는 에러 객체                         | Error.prototype |
| TypeError      | 피연산자 또는 인수의 데이터 타입이 유요하지 않을 때 발생하는 에러 객체         | Error.prototype |
| RangeError     | 숫자값의 허용 범위를 벗어났을 때 발생하는 에러                                 | Error.prototype |
| URIError       | encodeURI 또는 decodeURI 함수에 부적절한 인수를 전달했을 때 발생하는 에러 객체 | Error.prototype |
| EvalError      | eval 함수에서 발생하는 에러 객체                                               | Error.prototype |

---

# ⚾ throw 문

```jsx
try {
  throw new Error("error!!!");
} catch (error) {
  console.log(error); // Error: error!!!
}
```

에러를 발생시키려면 try 코드 블록에서 throw 문으로 에러 객체를 던져야 한다. 어떤 값이든 throw으로 던질 수 있다. 일반적으로 `에러 객체`를 지정한다.

에러를 던지게 되면 catch 문의 에러 변수가 생성되고 던져진 에러 객체가 할당된다.

```jsx
function add(a, b) {
  if (typeof a !== "number" || typeof b !== "number")
    throw new TypeError("variable is not number");

  return a + b;
}

add("1", 2); // TypeError:: variable is not number
```

add 함수를 구현을하는데 매개변수가 숫자가 아니라면 `타입에러`를 발생 시켜서 알려줄수 있다.

---

# ☝ 에러의 전파

에러는 `호출자 방향`으로 전파된다. 즉 `콜 스택의 아래 방향`으로 전파된다.

```jsx
const foo = () => {
  throw new Error("에러는 호출자 방향으로 전파 !!");
};
const bar = () => foo();
const baz = () => bar();

try {
  baz();
} catch (error) {
  console.log(error);
}
```

콜 스택이 쌓여있는 모습을 보면 `baz ⇒ bar ⇒ foo` 순으로 실행 컨텍스트가 쌓여있을 것이다. 이때 foo함수 내부에서 error가 발생이되면 콜 스택에 쌓여 있는 실행 컨텍스트의 역방향으로 에러가 전파 되면서 전역에 있는 `try/catch문`에 캐치 된다.

throw된 에러를 캐치하여 적절히 대응하면 프로그램을 강제 종료시키지 않고 코드의 실행 흐름을 복수할 수 있다. throw된 에러를 캐치하지 않으면 프로그램은 죽어버린다.
