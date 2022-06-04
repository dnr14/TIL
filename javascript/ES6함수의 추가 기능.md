# ES6함수의 추가 기능

# 🙋🏻‍♂️함수는 어떻게 부분되는가❓

ES6이전에 함수는 별다른 구분 없이 다양한 목적으로 사용되었다. 

1. **일반 함수로 호출**
2. **new 연산자와 함께 사용하는 생성자 함수 호출**
3. **객체에 바인딩되는 메서드 호출**

```jsx
var foo = function () {
  return 1;
};
foo(); // 1

new foo(); // {}

var obj = { foo };
obj.foo(); // 1
```

호출 방식만 다르고 동일한 함수이다. ES6 이전 모든 함수는 일반 함수 호출, 생성자 함수 호출이 가능했다. 이말은 callable이면서 constructor라는 말이다.(**호출자이면서 생성자 이다.**) 

<aside>
📌 호출할 수 있는 객체를 callable이라 하며 인스턴스를 생성할 수 있는 객체를 constructor 생성하지 못하는 객체를 non-constructor라고 부른다.

</aside>

```jsx
new obj.foo(); // {}
```

메서드도 함수여서 생성자 함수로 호출이 가능하다. 위 같은 함수들은 문제점이 있다. 메서드에는 문제점이 있다. 객체에 바인딩된 함수가 constructor라는 것은 함수 객체의 prototype 프로퍼티를 가지고 프로토타입 객체도 생성한가는 것이다. 생성자 함수 역할을 하지않는데 불필요한 메모리를 차지한다는 것이다. 콜백 함수 constructor이기 때문에 불필요한 프로토타입 객체가 생성된다.

| ES6 함수의 구분 | constructor | prototype | super | arguments |
| --- | --- | --- | --- | --- |
| 일반 함수 | O | O | O | O |
| 메서드(ES6) | X | X | O | O |
| 화살표 함수 | X | X | X | X |

ES6 부터는 함수를 사용 목적에 따라 세 가지 종류로 구분하고 있다. 일반 함수는 함수 선언문 함수 표현식으로 정의한 함수를 말한다.

---

# 🙋🏻‍♂️메서드란❓

```jsx
const obj = {
  x: 1,
  foo() {
    return this.x;
  }, // 메서드
  bar: function () {
    return this.x;
  }, // 객체에 바인딩된 일반 함수
};

console.log(obj.foo()); // 1
console.log(obj.bar()); // 1
```

ES6부터는 메서드 축약 표현으로 정의된 함수만을 의미한다. 메서드 축약 표현으로 정의한 메서드는 인스턴스를 생성할 수 없는 non-constructor다. 

```jsx
new obj.foo(); // TypeError: obj.foo is not a constructor
new obj.bar(); // bar {}

console.log(obj.foo.prototype); // undefined
console.log(obj.bar.prototype); // {}
```

new 연산자와 생성자 함수 호출 시 에러를 발생 시킨다. non-constructor 함수는 프로토타입 프로퍼티가 없고 프로토타입도 생성되지 않는다.

<aside>
💡 표준 빌트인 객체가 제공하는 프로토타입 메서드와 정적 메서드는 모두  non-constructor 함수다.

</aside>

```jsx
const base = {
  name: "lee",
  sayHi() {
    return `hi! ${this.name}`;
  },
};

const derived = {
  __proto__: base,
  sayHi() {
    return `${super.sayHi()}. how ar you doing`;
  },
};
console.log(derived.sayHi()); // hi! lee. how ar you doing
```

ES6 메서드는 자신을 바인딩한 객체를 가리키는 내부 슬롯 [[HomeObject]]를 갖는다. super 참조는  [[HomeObject]]를 사용하여 수퍼클래스의 메서드를 참조한다.  [[HomeObject]]가 있는 함수는 super 키워드를 사용할 수 있다. 일반함수에서 super를 참조 시 에러가 발생한다.

<aside>
⚠️ 메서드를 정의할 때 프로퍼티 값으로 익명 함수 표현식을 할당하는 ES6 이전의 방식은 사용하지 않는 것이 좋다.

</aside>

---

# 🙋🏻‍♂️화살표 함수❓

```jsx
const multiply = (x, y) => x * y;
multiply(2, 3); // 6
```

화살표 함수는 함수 선언문으로 정의할 수 없고 표현식으로 정의해야된다. 

❗ **화살표 함수는 매개변수 선언에 몇가지 규칙이있다.**

```jsx
const arrow1 = (x, y) => {};
const arrow2 = x => {};
const arrow3 = () => {};
```

1. 매개변수가 여러개 일때는 소괄호를 해줘야한다. 
2. 매개변수가 한개라면 생략도 가능하다.
3. 매개변수가 없는 경우 소괄호를 써줘야된다.

❗ **화살표 함수는 함수 몸체 정의에 몇가지 규칙이있다.**

```jsx
const power1 = (x) => x ** 2;
const power2 = (x) => {
  return x ** 2;
};
const power2 = (x) => const y = x ** 2; // error
const create = (id, pwd) => ({ id, pwd });
```

1. 함수의 반환으로 선언문이 아닌 표현식이라면 return과 중괄호를 생략가능하다. 선언문을 반환하면 에러가 발생한다.
2. 함수의 반환이 객체 리터럴이면 소괄호를 감싸주면 된다. 소괄호가 없으면 객체 리터럴을 함수 몸체 중괄호로 해석한다.
3. 함수 몸체에 여러개 선언문으로 구성된다면 중괄호를 생략할 수 없다.

### 🙊 화살표 함수와 일반함수의 차이점

1. 화살표 함수는 인스턴스를 생성할 수 없는 non-constructor다. prototype 프로퍼티와 프로토타입 객체도 생성되지 않는다.
2. 중복된 매개변수 이름을 선언할 수 없다. 
3. 화살표 함수는 함수 자체의 this, arguments, super, new.target 바인딩을 갖지 않는다.
    1. 화살표 함수는 스코프 체인을 통해 상위 스코프의 this, arguments, super, new.target 를 참조한다.
    2. 화살표 함수가 중첩이 되어있으면 스코프 체인을 따라 this, arguments, super, new.target 를 갖는 제일 가까운 함수를 참조한다.

### 👻 화살표 함수에서 this

화살표 함수와 일반 함수의 큰 차이점은 this 바인딩이다. 화살표 함수는 this를 가지지 않기 때문에 this 바인딩을 하지 않는다. this를 참조할 때는 스코프 체인에서 상위 스코프의 this를 참조한다.

```jsx
class Prefixer {
  constructor(prefix) {
    this.prefix = prefix;
  }

  add(arr) {
    return arr.map(
      function (item) {
        return this.prefix + item; // error
      }.bind(this)
    );
  }
}
console.log(new Prefixer("-webkiy-").add(["transition", "user-select"]));
```

ES6이전에는 콜백 함수의 this문제를 해결하기 위해서 this 참조를 함수가 호출 됬을때 that 식별자에 따로 할당을하는 방식으로 우회하거나 apply/call/bind 함수 프로토타입 메서드를 이용해서 this에 간접적으로 바인딩을 해주었다.

```jsx
class Prefixer {
  constructor(prefix) {
    this.prefix = prefix;
  }

  add(arr) {
    return arr.map((item) => this.prefix + item);
  }
}

console.log(new Prefixer("-webkiy-").add(["transition", "user-select"]));
```

ES6이후 화살표 함수를 이용하여 콜백 함수 내부의 this 문제를 해결하였다. 

<aside>
⚠️ 화살표 함수 자체는 this 바인딩을 갖지 않는다. 따라서 화살표 함수 내부에서 this를 참조하면 상위 스코프의 this를 참조한다. 이를 lexical this라 한다.
**렉시컬 스코프와 같이 화살표 함수의 this가 함수가 정의된 위치에 의해 결정된다는 것이다.**

</aside>

```jsx
(function () {
  const bar = () => console.log(this); // { a: 1 }
  const bar2 = () => () => console.log(this); // { a: 1 }
  bar();
  bar2()();
}.call({ a: 1 }));
```

⭐⭐ **중첩 화살표 함수는 스코프 체인에서 가장 가까운상위 함수 중에서 this를 갖는 함수의 this를 참조한다.**

```jsx
globalThis.x = 1;

const normal = function () {
  return this.x;
};
const arrow = () => this.x; 

console.log(normal.call({ x: 10 })); // 10
console.log(arrow.call({ x: 100 })); // 1
```

⭐⭐ **화살표 함수는 this를 갖지 않아 apply/call/bind 메서드를 사용해도 함수 내부 this는 변경할 수 없다. 언제나 상위 스코프의 this 바인딩을 참조한다.**

```jsx
const person = {
  name: "lee",
  sayName: () => {
    return this.name;
  },
};

console.log(person.sayName()); // undefined
```

메서드(일반 메서드, ES6 메서드)를 정의할 때는 화살표 함수로 정의하는 걸 지양해야된다. 함수 내부 this는 메서드를 호출한 객체의 person을 가리키지 않고 상위 스코프인 전역의 this가 가리키는 전역 객체를 가리킨다. 화살표 함수로 정의하면 this가 개발자 의도한대로 작동하지 않을 수 있다. 객체의 메서드를 정의할 때는 ES6 메서드 축약 표현으로 정의하는게 좋다.

```jsx
class Person {
  constructor(name) {
    this.name = name;
  }
  seyName = () => {
    return this.name;
  };
}

const me = new Person("lee");
console.log(me.seyName()); // lee
```

클래스 필드에 화살표 함수를 할당할 수도 있다. 이때 sayName 함수 내부의 this는 상위스코프의constructor이다. 함수 내부의 this가 전역 this 전역 객체를 참조하지 않아서 잘 작동하는 거 처럼 보인다. 

클래스 필드에 화살표 함수로 정의한 함수는 프로토타입 메서드가 아니라 인스턴스 메서드가 된다. 인스턴스가 생성될때 마다 매번 동일한 기능을하는 메서드를 메모리에 올리는 것이다. 

클래스에서 함수를 정의할 때도 ES6 메서드 축약  표현으로 정의하는 것이 좋다. 

### 👻 화살표 함수에서 super

```jsx
class Person {
  constructor(name) {
    this.name = name;
  }
  seyName() {
    return `hi! ${this.name}`;
  }
}

class Min extends Person {
  sayName = () => console.log(`${super.seyName()} how are you doing?`);
}
const min = new Min("min");
min.sayName();
```

화살표 함수는 super 바인딩을 갖지 않는다. super도 this와 동일하게 스코프 체인상에서 상위 스코프의 super를 참조한다. 클래스 필드에 할당한 화살표 함수 상위 스코프는 constructor다. 함수 내부의 super는 constructor의 super바인딩을 참조한다.

### 👻 화살표 함수에서 arguments

```jsx
(function () {
  const foo = () => console.log(arguments); // [Arguments] { '0': 3, '1': 4 }
  foo(10, 20);
})(3, 4);
```

화살표 함수는 arguments바인딩을 갖지 않는다. arguments도 this와 동일하게 스코프 체인상에서 상위 스코프의 arguments를 참조한다.

---

# 🙋🏻‍♂️Rest 파라미터❓

화살표 함수는 상위스코프 arguments를 참조하기 때문에 가변 인자 함수를 구현하고 싶다면 Rest 파라미터를 이용해야된다.

```jsx
function foo(...rest) {
  console.log(rest); // [ 1, 2, 3, 4, 5 ]
}
foo(1, 2, 3, 4, 5);

function foo(a, b, ...rest) {
  console.log(a, b, rest); // 1 2 [ 3, 4, 5 ]
}
foo(1, 2, 3, 4, 5);
```

Rest 파라미터는 함수에 전달된 인수들의 목록을 배열로 전달받는다. 일반 매개변수와 같이 사용이 가능하다. 함수 인수로 넘긴 값들은 순차적으로 매개변수에 할당이 되고 나머지 인수들로 구성된 배열이 Rest 파라미터에 할당된다. Rest 파라미터는 반드시 마지막 파라미터이어야 한다. 

```jsx
function foo(...rest, ...rest) {} // error

function foo(...rest) {
  console.log(rest.length); // 5
}
foo(1, 2, 3, 4, 5);
console.log(foo.length); // 0
```

Rest 파라미터는 하나만 선언가능하다.  Rest 파라미터 배열길이는 함수 객체 length 프로퍼티에 영향을 주지 않는다.

### Rest 파라미터와 arguments 객체

| 이름 | 차이점 |
| --- | --- |
| Rest 파라미터 | 배열, 배열이여서 배열 프로토타입 메서드 사용하면된다. |
| arguments 객체 | 유사배열, 요소 순회 시 보조 메서드 사용해야된다. |

---

# 🙋🏻‍♂️매개변수 기본값❓

```jsx
function add(x, y) {
  return x + y;
}
console.log(add(1)); // NaN
console.log(add(1, 2)); // 3

function add(x = 0, y = 0) {
  return x + y;
}
console.log(add(1)); // 1
console.log(add(1, 2)); // 3
```

ES5에서는 인수가 전달되지 않은 매개변수의 값은 undefined다. ES6부터는 매개변수에 기본값을 줄 수 있다.  undefined로 할당되는 걸 방어할 수 있다.

```jsx
function add(x, y) {
  x = x || 0;
  y = y || 0;
  return x + y;
}
console.log(add(1)); // 1
console.log(add(1, 2)); // 3
```

매개변수 기본값을 주지 못했던 ES5에서는 오작동을 방지하기 위해 방어코드가 필요했다. 하지만 ES6부터 기본값을 할당할 수 있어서 함수 내부의 방어코드를 간소화할 수 있게 되었다.

```jsx
function sayName(name = "lee") {
  return name;
}
console.log(sayName(undefined)); // lee
console.log(sayName(null)); // null
```

인수 값으로 undefined를 전달한 경우에만 유효하다.