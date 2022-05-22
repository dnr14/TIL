# this

## this 란❓

`this` 는 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 `자기 참조 변수` 다.

`this` 를 통해 자신이 속한 객체 또는 자신이 `생성할 인스턴스`의 `프로퍼티`나 `메서드`를 참조할 수 있다.

`this` 가 가르키는 값은 `this` 바인딩은 함수 호출 방식에 의해 동적으로 결정된다.

<aside>
📌 **바인딩**이란 식별자와 값을 연결하는 과정을 의미한다. 변수 선언은 식별자와 메모리가 확보된 공간을 연결하는걸 바인딩이라고 한다.

**this바인딩**은 this와 this가 가리킬 객체를 바인딩하는 것이다.

</aside>

### 🤖 **메소드 안에 this**

```jsx
const circle = {
  radius: 5,
  getDiameter() {
    return 2 * this.radius;
  },
};

console.log(circle.getDiameter());
```

메소드 내부에서의 `this` 는 메서드를 호출한 객체를 가리킨다.

---

### 🤖 **생성자 함수 안에 this**

```jsx
function Circle(radius) {
  this.radius = radius;
}

Circle.prototype.getDiameter = function () {
  return 2 * this.radius;
};

const circle = new Circle(5);
console.log(circle.getDiameter());
```

생성자 함수 내부에서 `this` 는 자신이 생성할 인스턴스를 가리킨다. `this` 는 상황에 따라 대상이 다르다.

---

## 함수 호출 방식과 this 바인딩❓

```jsx
console.log(this);

function square(number) {
  console.log(this);
  return number * number;
}

square(2);

const person = {
  name: "lee",
  getName() {
    console.log(this);
    return this.name;
  },
};
console.log(person.getName());

function Person(name) {
  this.name = name;

  console.log(this);
}

const me = new Person("lee");
```

> **this 바인딩은 함수 호출 방식, 함수가 어떻게 호출되었는지에 따라 동적으로 결정된다.**

함수 호출하는 방식을 나누어보면 아래와 같다.

1. 일반 함수 호출
2. 메서드 호출
3. 생성자 함수 호출
4. Function.prototype.apply/call/bind 메서드에 의한 간접호출

---

### 🧑‍🎓 **일반 함수 호출**

```jsx
function foo() {
  console.log("foo`s this : ", this); // window
  function bar() {
    console.log("bar`s this : ", this); // window
  }
  bar();
}
foo();

// 스트릭 모드
function foo() {
  "use strict";

  console.log("foo`s this : ", this); // undefined
  function bar() {
    console.log("bar`s this : ", this); // undefined
  }
  bar();
}
foo();
```

`일반 함수` 내부 안에서 `this` 는 전역 객체를 바인딩한다. `stric mode` 가 적용된 함수 내부 안의 `this` 는`undefined` 가 바인딩 된다.

```jsx
const obj = {
  foo() {
    console.log("foo`s this : ", this); // obj
    function bar() {
      console.log("bar`s this : ", this); // window
    }
    bar();
  },
};

obj.foo();
```

메소드 안에 정의한 중첩 함수도 일반 함수로 취급되어 `this` 는 인스턴스를 가리키지 않고 `전역 객체` 가 바인딩된다. 다시 말하지만 함수는 호출방식에 따라 this가 동적으로 변경된다.

```jsx
const obj = {
  foo() {
    console.log("foo`s this : ", this); // obj

    setTimeout(function timer() {
      console.log("callback`s this :", this); // window
    }, 1000);
  },
};

obj.foo();
```

`콜백 함수` 내부의 `this` 도 `전역 객체` 를 가리킨다. 핵심은 어떤 함수라도 일반 함수로 호출되면 `this` 는 `전역 객체` 가 바인딩 된다.

**이처럼 일반 함수로 호출된 모든함수(중첩 함수, 콜백 함수) 내부의 this에는 전역 객체가 바인딩된다.**

```jsx
const obj = {
  name: "lee",
  foo() {
    console.log("foo`s this : ", this); // obj
    const that = this;
    setTimeout(function timer() {
      console.log("callback`s this :", that.name);
    }, 1000);
  },
};

obj.foo();
```

`this` 를 다른식별자(that)를 이용해서 바인딩을 우회하는 방식도 있다.

---

### 🧑‍🎓 **메서드 호출**

```jsx
const person = {
  name: "lee",
  getName() {
    return this.name;
  },
};
console.log(person.getName()); // lee
```

메소드 내부의 `this` 는 메소드를 소유한 객체가 아닌 메서드를 호출한 객체에 바인딩된다.

함수 객체는 `person` 객체에 포함된 것이 아니라 독립적으로 존재하는 별도의 객체다. `getName` 프로퍼티가 함수 객체를 가리키고 있을 뿐이다.

```jsx
const obj = {
  name: "lee",
  foo() {
    console.log(this);
    setTimeout(() => {
      console.log("callback`s this :", this);
    }, 100);
  },
};
obj.foo();

const _obj = {
  foo: obj.foo,
};

_obj.foo();
const foo2 = obj.foo;
foo2(); // window
```

이말은 getName 메서드를 `다른 객체 프로퍼티`에 할당이 가능하고 일반 변수에 할당 후 `일반 함수`로 호출 가능하다.

function object 안 `this` 프로퍼티의 바인딩될 객체는 호출 시점에 결정된다.

```jsx
function Person(name) {
  this.name = name;
}

Person.prototype.getName = function () {
  return this.name;
};

const me = new Person("lee");
console.log(me.getName()); // lee

Person.prototype.name = "kim";
console.log(Person.prototype.getName()); // kim
```

me 인스턴스에서 메소드를 호출하여서 이때 `this` 는 me 인스턴스로 바인딩되고 name을 `lee` 를 호출한다. Person 프로토타입 객체에서 getName을 호출 시 `this` 는 Person.prototype에 바인딩이 되고 `kim` 을 호출한다.

---

### 🧑‍🎓 **생성자 함수 호출**

```jsx
function Person(name) {
  this.name = name;
  this.getName = function () {
    return this.name;
  };
}

const me1 = new Person("lee");
const me2 = new Person("kim");
console.log(me1.getName()); // lee
console.log(me2.getName()); // kim

const me3 = Person("woo");
console.log(me3); // undefined
```

생성자 함수 내부의 `this` 는 생성자 함수가 생성할 인스턴스가 바인딩된다. new 연산자를 사용하지 않고 일반 호출을하면 일반 함수처럼 동작한다.

일반 함수로 호출된 Person함수는 반환문이 없으므로 암묵적으로 `undefined` 가 반환되어 me3는 `undefined` 가 할당된다.

---

### 🧑‍🎓 **Function.prototype.apply/call/bind 메소드에 의한 간접호출**

1 . **call/bind**

```jsx
function getThisBinding() {
  console.log(arguments);
  return this;
}
const thisArg = { a: 1 };

console.log(getThisBinding.apply(thisArg, [1, 2, 3]));
console.log(getThisBinding.call(thisArg, 1, 2, 3));
```

`call, apply` 메소드는 본질적인 기능은 함수를 호출하는 것이다. 이때 첫번째 인수로 호출될 함수 this에 바인딩될 객체를 전달하면된다. `call, apply` 는 기능은 동일하다. 호출 되는 함수에 인수를 전달하는 방식이 다르다. call은 `배열`에 담아서 보내고 apply는 `쉼표`를 구분해서 넘긴다.

1. **bind**

```jsx
function getThisBinding() {
  return this;
}
const thisArg = { a: 1 };

console.log(getThisBinding.bind(thisArg)); // getThisBinding
console.log(getThisBinding.bind(thisArg)()); // { a : 1}
```

bind 메소드는 함수를 호출하지 않고 `this` 로 사용할 객체만 전달한다.

```jsx
const person = {
  name: "lee",
  foo(callback) {
    setTimeout(callback.bind(this));
  },
};

person.foo(function () {
  console.log(this.name); // lee
});
```

bind 메소드를 통해 콜백 함수의 `this` 불일치하는 문제도 해결가능하다.

---

### 📜 this바인딩 정리

| 함수 호출 방식                                             | this 바인딩                        |
| ---------------------------------------------------------- | ---------------------------------- |
| 일반 함수 호출                                             | 전역 객체                          |
| 메서드 호출                                                | 메서드를 호출한 객체               |
| 생성자 함수 호출                                           | 생성자 함수가 생성할 인스턴스      |
| Function.prototype.apply/call/bind 메소드로 의한 간접 호출 | 메소드의 첫번째 인수로 전달한 객체 |
