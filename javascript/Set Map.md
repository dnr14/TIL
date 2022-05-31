# Set / Map

# 🙋🏻‍♂️Set이란❓

set 객체는 중복되지 않는 유일한 값들의 `집합`이다. 배열과 차이점을 비교해보자.

| 구분                                 | 배열 | Set |
| ------------------------------------ | ---- | --- |
| 동일한 값을 중복하여 포함할 수 있다. | O    | X   |
| 요소 순서에 의미가 있다.             | O    | X   |
| 인덱스로 요소에 접근할 수 있다.      | O    | X   |

Set은 수학적 집합을 구현하기 위한 `자료구조`다. Set을 통해 여집합, 차집합, 합집합, 교집합 등을 구현할 수 있다.

---

# 🙋🏻‍♂️Set객체의 생성

자바스크립트는 기본 빌트인 생성자 함수 안에 `Set 생성자 함수`를 제공한다.

```jsx
const set = new Set();
console.log(set); // Set(0) {}

const set1 = new Set([1, 2, 3]);
console.log(set1); // Set(3) { 1, 2, 3 }

const set2 = new Set([1, 2, 3, 3]);
console.log(set2); // Set(3) { 1, 2, 3 }
```

생성자 함수 인수를 전달하지 않으면 빈 set 객체로 생성된다. 이터러블을 인수로 전달 받을 수 있다.

이터러블에 중복된 값이 있다면 중복이 제거되어 set 객체 요소에 저장된다.

```jsx
let arr = [1, 2, 3, 3];

arr = [...new Set(arr)];
console.log(arr); // [1,2,3]
```

배열의 중복된 값을 제거하고 싶다면 set 객체를 이용하면 쉽게 가능하다.

---

## 🙋🏻‍♂️Set객체 요소 개수 확인

```jsx
const set = new Set([1, 2, 3, 3]);
console.log(set.size); // 3
```

Set.prototype.size 프로퍼티를 제공한다.

```jsx
console.log(Object.getOwnPropertyDescriptor(Set.prototype, "size"));
// {
//   get: [Function: get size],
//   set: undefined,
//   enumerable: false,
//   configurable: true
// }
set.size = 10; // 무시된다.
console.log(set.size); // 3
```

size 프로퍼티는 setter(undefined)는 없고 `getter`만 있는 접근자 프로퍼티다. 값은 읽을 수 있지만 임의로 size를 변경할 수는 없다.

---

## 🙋🏻‍♂️Set객체 요소 추가

```jsx
const set = new Set([1, 2, 3, 3]);
const newSet = set.add(5);
console.log(set); // Set(4) { 1, 2, 3, 5 }
console.log(newSet === set);
set.add(7).add(8); // 연속 호출 가능
console.log(set); // Set(6) { 1, 2, 3, 5, 7, 8 }
```

Set.prototype.add 메서드를 제공한다. add메서드 반환으로 자기자신(set객체)을 반환한다. 이런 특징을 이용하여 메서드 체이닝이 가능하다.

```jsx
set.add(2).add(2);
console.log(set); // 에러 발생 x
```

add 메서드로 이미있는 요소 값을 넣어도 에러는 발생하지 않고 무시된다.

```jsx
console.log(NaN === NaN); // false
set.add(NaN).add(NaN);
console.log(set); // Set(7) { 1, 2, 3, 5, 7, 8, NaN }
```

일반 비교 연산자는 NaN을 같다고 평가하지 않지만 set객체는 `NaN`를 같다고 평가하여 중복을 허용하지 않는다. 0과 -0도 set은 동일하다라고 평가해서 중복 허용을 하지않는다.

```jsx
const set = new Set();

set
  .add(1)
  .add("a")
  .add(true)
  .add(undefined)
  .add(null)
  .add({})
  .add([])
  .add(function () {});
console.log(set);
// Set(8) {   1,  'a',  true,  undefined,  null,  {}, [],  [Function (anonymous)] }
```

어느 값이든 set객체의 요소로 들어갈 수 있다.

---

## 🙋🏻‍♂️Set객체 요소 존재 여부 확인

```jsx
const set = new Set([1, 2, 3]);
console.log(set.has(1)); // true
```

Set.prototype.has 메서드를 사용하면 요소가 존재하는지 확인 가능하다. 반환으로 불리언 값을 준다.

---

## 🙋🏻‍♂️Set객체 요소 삭제

```jsx
const set = new Set([1, 2, 3]);
console.log(set.delete(1)); // true
console.log(set); // Set(2) { 2, 3 }
```

Set.prototype.delete 메서드를 제공한다. 요소가 삭제 됬다면 반환으로 불리언 값을 준다. delete메서드 인수로 요소를 전달해야된다. 요소가 Reference Type이라면 참조 값을 넘겨야 삭제가된다.

```jsx
const set = new Set([1, 2, 3]);
console.log(set.delete(1)); // true
console.log(set); // Set(2) { 2, 3 }
console.log(set.delete(1)); // false 무시된다.
```

존재 하지 않는 요소를 인수로 전달 시 에러는 발생하지 않고 `무시`된다.

---

## 🙋🏻‍♂️Set객체 요소 일괄 삭제

```jsx
const set = new Set([1, 2, 3]);
console.log(set.clear());
console.log(set); // Set(0) {}
```

Set.prototype.clear 메서드를 제공한다. undefined를 반환한다.

---

## 🙋🏻‍♂️Set객체 요소 순회

Set.prototype.forEach 메서드를 제공해서 `순회`가 가능하다. Array.prototype.forEach 메서드와 유사하다.

Set.prototype.forEach 메서드의 콜백 함수는 `3개`의 인수를 전달받는다.

1. **첫번째 인수** : 현재 순회 중인 `요소값`
2. **두번째 인수** : 현재 순회 중인 `요소값`
3. **세번째 인수** : 현재 순회 중인 `this(Set 객체 자체)`

```jsx
const set = new Set([1, 2, 3]);
set.forEach((value1, value2, _this) => console.log(value1, value2, _this));
// 1 1 Set(3) { 1, 2, 3 }
// 2 2 Set(3) { 1, 2, 3 }
// 3 3 Set(3) { 1, 2, 3 }
```

첫번째, 두번째 인수가 동일하다. 이처럼 동작하는 이유는 Array.prototype.forEach 메서드와 `인터페이스`를 통일하기 위함이며 다른 의미는 없다.

```jsx
const set = new Set([1, 2, 3]);
const [a] = set;
console.log(Symbol.iterator in Set.prototype); // true
console.log(a); // 1
console.log(...set); // 1 2 3
for (const iterator of set) console.log(iterator);
```

Set 객체는 이터러블이다. 이터러블은 for...fo문으로 순회가 가능하고 스프레드 문법과 디스트럭처링할당 의 대상이 된다.

set 객체는 요소의 순서에 의미를 갖지 않지만 set 객체를 순회하는 순서는 요소가 추가된 순서를 따른다.

---

# 🙋🏻‍♂️Map이란❓

Map 객체는 `키`와 `값`의 쌍으로 이루어진 `컬렉션`이다. 일반 객체와 유사하지만 차이점이 있다.

| 구분                   | 객체                    | Map객체               |
| ---------------------- | ----------------------- | --------------------- |
| 키로 사용할 수 있는 값 | 문자열 또는 심벌 값     | 객체를 포함한 모든 값 |
| 이터러블               | X                       | O                     |
| 요소 개수 확인         | Object.keys(obj).length | map.size              |

---

## 🙋🏻‍♂️Map 객체의 생성

```jsx
const map = new Map();
console.log(map); // Map(0) {}
```

자바스크립트는 Map 생성자 함수를 제공한다. Map 생성자 함수로 map 객체를 생성할 수 있다. 인수로 아무것도 전달하지 않으면 빈 map이 생성된다.

```jsx
const map = new Map([
  ["key1", "value1"],
  ["key2", "value2"],
]);
console.log(map); //Map(2) { 'key1' => 'value1', 'key2' => 'value2' }
```

Map 생성자 함수 인수로 이터러블을 전달 받을 수 있다. `키`와 `값`의 쌍으로 이루어진 요소로 구성된 이터러블을 전달해야된다. `키`와 `값`의 쌍이 아니면 에러를 발생 시킨다.

```jsx
const map = new Map([
  ["key1", "value1"],
  ["key1", "value2"],
]);
console.log(map); // Map(1) { 'key1' => 'value2' }
```

중복된 키는 Map 객체에 요소로 저장되지 않는다.

## 🙋🏻‍♂️Map 객체 요소 개수 확인

```jsx
const map = new Map([
  ["key1", "value1"],
  ["key2", "value2"],
]);
console.log(map.size); // 2
map.size = 100; // 무시된다.
console.log(map.size); // 2
```

Map.prototype.size 프로퍼티를 제공한다. map의 size는 set의 size 프로퍼티와 동일하게 getter만 제공하는 접근자 프로퍼티다. 임의로 사이즈를 변경할 수 없다.

## 🙋🏻‍♂️Map 객체 요소 추가

```jsx
const map = new Map();
console.log(map); // Map(0) {}
const _map = map.set("key1", "value1");
console.log(map); // Map(1) { 'key1' => 'value1' }
console.log(_map === map); // true
```

Map.prototype.set 메서드를 제공한다. set메서드 인수는 2개를 받는다. 첫번 째 인수는 요소의 키값 , 두번 째 인수는 요소의 값이다. 요소 추가를 하면 자기자신(Map객체 자체)을 반환한다.

```jsx
map.set("key2", "value2").set("key3", "value3").set("key4", "value4");
```

이런 특징으로 메서드 체이닝이 가능하다.

```jsx
map.set("key2", "value2").set("key2", "value2");
console.log(map);
// Map(2) { 'key1' => 'value1', 'key2' => 'value2' }
```

중복된 키를 허용 하지않는다. set메서드 인수로 중독된 키가 들어와도 에러는 발생하지 않고 무시된다.

```jsx
console.log(NaN === NaN); // false
console.log(-0 === +0); // true

const map = new Map();
map.set(NaN, 1);
map.set(NaN, 2);
console.log(map); // Map(1) { NaN => 2 }
map.set(+0, "0이다.").set(-0, "-0이다.");
console.log(map); // Map(2) { NaN => 2, 0 => '-0이다.' }
```

일반 비교 연산자에서 NaN은 절대 같은 값이 나올 수 없다. Map 객체의 키로 NaN를 사용하면 중복을 허용하지 않는다.

-0과 +0 도 동일하게 평가하여 중복을 허용하지 않는다.

```jsx
const map = new Map();
const lee = { name: "lee" };
const kim = { name: "kim" };

map.set(lee, "developer");
map.set(kim, "PM");

console.log(map);
// Map(2) { { name: 'lee' } => 'developer', { name: 'kim' } => 'PM' }
```

Map은 `키 타입`에 제한이 없다. 따라서 객체를 포함한 `모든 값`을 키로 사용할 수 있다.

## 🙋🏻‍♂️Map 객체 요소 취득

```jsx
const map = new Map();
const lee = { name: "lee" };
const kim = { name: "kim" };

map.set(lee, "developer");
map.set(kim, "PM");

console.log(map.get(lee)); // developer
console.log(map.get("woo")); // undefined
```

Map.prototype.get 메서드를 제공한다. get 메서드 인수로 키를 전달하면 Map객체에서 인수로 전달한 키를 갖는 값을 반환한다. 키가 없다면 `undefined`를 반환한다.

## 🙋🏻‍♂️Map 객체 요소 존재 여부 확인

```jsx
const map = new Map();
const lee = { name: "lee" };
const kim = { name: "kim" };

map.set(lee, "developer");
map.set(kim, "PM");

console.log(map.has(lee)); // true
console.log(map.has("woo")); // false
```

Map.prototype.has메서드를 제공한다. 인수로 키를 전달하면 불리언 값을 반환한다. 있으면 `true` 없으면 `false`다.

## 🙋🏻‍♂️Map 객체 요소 삭제

```jsx
const map = new Map();
const lee = { name: "lee" };
const kim = { name: "kim" };

map.set(lee, "developer");
map.set(kim, "PM");

console.log(map.delete(lee)); // true
console.log(map.delete("woo")); // false
```

Map.prototype.delete메서드를 제공한다. 삭제 성공 여부를 불리언 값을 반환한다.

## 🙋🏻‍♂️Map 객체 요소 일괄 삭제

```jsx
const map = new Map();
const lee = { name: "lee" };
const kim = { name: "kim" };

map.set(lee, "developer");
map.set(kim, "PM");

console.log(map.clear()); // undefined
console.log(map); // Map(0) {}
```

Map.prototype.clear메서드를 제공한다. clear메서드는 언제나 `undefined`를 반환한다.

## 🙋🏻‍♂️Map 객체 요소 순회

```jsx
const map = new Map();
const lee = { name: "lee" };
const kim = { name: "kim" };

map.set(lee, "developer");
map.set(kim, "PM");

map.forEach((v, k, map) => console.log(v, k, map));
// developer { name: 'lee' } Map(2) { { name: 'lee' } => 'developer', { name: 'kim' } => 'PM' }
// PM { name: 'kim' } Map(2) { { name: 'lee' } => 'developer', { name: 'kim' } => 'PM' }
```

Map 객체의 요소를 순회하려면 Map.prototype.forEach 메서드를 사용한다. Map.prototype.forEach 메서드는 Array.prototype.forEach 메서드와 유사하다.

Map.prototype.forEach 메서드 콜백 함수는 `3개`의 인수를 전달 받는다.

1. **첫 번째 인수 :** 현재 순회 중인 `요소값`
2. **두 번째 인수 :** 현재 순회 중인 `요소키`
3. **세 번째 인수 :** 현재 순회 중인 `Map객체 자체`

```jsx
console.log(Symbol.iterator in map); // true
for (const iterator of map) console.log(iterator);
// [ { name: 'lee' }, 'developer' ]
// [ { name: 'kim' }, 'PM' ]
console.log(...map);
// [ { name: 'lee' }, 'developer' ] [ { name: 'kim' }, 'PM' ]
const [a] = map;
console.log(a);
// [ { name: 'lee' }, 'developer' ]
```

Map 객체는 이터러블이다. for..of문, 스프레드 문법, 디스트럭처링 할당의 대상이 된다.

```jsx
const iterator = map.keys(); // 이터레이터 반환
console.log(iterator.next());
```

Map 객체는 이터레이터 객체를 반환하는 메서드를 제공한다.

| Map 메서드            | 설명                                                                                           |
| --------------------- | ---------------------------------------------------------------------------------------------- |
| Map.prototype.keys    | Map 객체에서 요소키를 값으로 갖는 이터러블이면서 동시에 이터레이터인 객체를 반환한다.          |
| Map.prototype.values  | Map 객체에서 요소값를 값으로 갖는 이터러블이면서 동시에 이터레이터인 객체를 반환한다.          |
| Map.prototype.entries | Map 객체에서 요소키와 요소값을 값으로 갖는 이터러블이면서 동시에 이터레이터인 객체를 반환한다. |

```jsx
const keys_iterator = map.keys(); // 이터레이터 반환
for (const iterator of keys_iterator) console.log(iterator);
// { name: 'lee' } { name: 'kim' }
const values_iterator = map.values(); // 이터레이터 반환
for (const iterator of values_iterator) console.log(iterator);
// developer PM
const entries_iterator = map.entries(); // 이터레이터 반환
for (const iterator of entries_iterator) console.log(iterator);
// [ { name: 'lee' }, 'developer' ] [ { name: 'kim' }, 'PM' ]
```

Map 객체는 요소의 순서에 의미를 갖지 않지만 Map 객체를 순회하는 순서는 요소가 추가된 순서를 따른다.
