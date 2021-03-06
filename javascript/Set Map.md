# Set / Map

# ππ»ββοΈSetμ΄λβ

set κ°μ²΄λ μ€λ³΅λμ§ μλ μ μΌν κ°λ€μ `μ§ν©`μ΄λ€. λ°°μ΄κ³Ό μ°¨μ΄μ μ λΉκ΅ν΄λ³΄μ.

| κ΅¬λΆ                                 | λ°°μ΄ | Set |
| ------------------------------------ | ---- | --- |
| λμΌν κ°μ μ€λ³΅νμ¬ ν¬ν¨ν  μ μλ€. | O    | X   |
| μμ μμμ μλ―Έκ° μλ€.             | O    | X   |
| μΈλ±μ€λ‘ μμμ μ κ·Όν  μ μλ€.      | O    | X   |

Setμ μνμ  μ§ν©μ κ΅¬ννκΈ° μν `μλ£κ΅¬μ‘°`λ€. Setμ ν΅ν΄ μ¬μ§ν©, μ°¨μ§ν©, ν©μ§ν©, κ΅μ§ν© λ±μ κ΅¬νν  μ μλ€.

---

# ππ»ββοΈSetκ°μ²΄μ μμ±

μλ°μ€ν¬λ¦½νΈλ κΈ°λ³Έ λΉνΈμΈ μμ±μ ν¨μ μμ `Set μμ±μ ν¨μ`λ₯Ό μ κ³΅νλ€.

```jsx
const set = new Set();
console.log(set); // Set(0) {}

const set1 = new Set([1, 2, 3]);
console.log(set1); // Set(3) { 1, 2, 3 }

const set2 = new Set([1, 2, 3, 3]);
console.log(set2); // Set(3) { 1, 2, 3 }
```

μμ±μ ν¨μ μΈμλ₯Ό μ λ¬νμ§ μμΌλ©΄ λΉ set κ°μ²΄λ‘ μμ±λλ€. μ΄ν°λ¬λΈμ μΈμλ‘ μ λ¬ λ°μ μ μλ€.

μ΄ν°λ¬λΈμ μ€λ³΅λ κ°μ΄ μλ€λ©΄ μ€λ³΅μ΄ μ κ±°λμ΄ set κ°μ²΄ μμμ μ μ₯λλ€.

```jsx
let arr = [1, 2, 3, 3];

arr = [...new Set(arr)];
console.log(arr); // [1,2,3]
```

λ°°μ΄μ μ€λ³΅λ κ°μ μ κ±°νκ³  μΆλ€λ©΄ set κ°μ²΄λ₯Ό μ΄μ©νλ©΄ μ½κ² κ°λ₯νλ€.

---

## ππ»ββοΈSetκ°μ²΄ μμ κ°μ νμΈ

```jsx
const set = new Set([1, 2, 3, 3]);
console.log(set.size); // 3
```

Set.prototype.size νλ‘νΌν°λ₯Ό μ κ³΅νλ€.

```jsx
console.log(Object.getOwnPropertyDescriptor(Set.prototype, "size"));
// {
//   get: [Function: get size],
//   set: undefined,
//   enumerable: false,
//   configurable: true
// }
set.size = 10; // λ¬΄μλλ€.
console.log(set.size); // 3
```

size νλ‘νΌν°λ setter(undefined)λ μκ³  `getter`λ§ μλ μ κ·Όμ νλ‘νΌν°λ€. κ°μ μ½μ μ μμ§λ§ μμλ‘ sizeλ₯Ό λ³κ²½ν  μλ μλ€.

---

## ππ»ββοΈSetκ°μ²΄ μμ μΆκ°

```jsx
const set = new Set([1, 2, 3, 3]);
const newSet = set.add(5);
console.log(set); // Set(4) { 1, 2, 3, 5 }
console.log(newSet === set);
set.add(7).add(8); // μ°μ νΈμΆ κ°λ₯
console.log(set); // Set(6) { 1, 2, 3, 5, 7, 8 }
```

Set.prototype.add λ©μλλ₯Ό μ κ³΅νλ€. addλ©μλ λ°νμΌλ‘ μκΈ°μμ (setκ°μ²΄)μ λ°ννλ€. μ΄λ° νΉμ§μ μ΄μ©νμ¬ λ©μλ μ²΄μ΄λμ΄ κ°λ₯νλ€.

```jsx
set.add(2).add(2);
console.log(set); // μλ¬ λ°μ x
```

add λ©μλλ‘ μ΄λ―Έμλ μμ κ°μ λ£μ΄λ μλ¬λ λ°μνμ§ μκ³  λ¬΄μλλ€.

```jsx
console.log(NaN === NaN); // false
set.add(NaN).add(NaN);
console.log(set); // Set(7) { 1, 2, 3, 5, 7, 8, NaN }
```

μΌλ° λΉκ΅ μ°μ°μλ NaNμ κ°λ€κ³  νκ°νμ§ μμ§λ§ setκ°μ²΄λ `NaN`λ₯Ό κ°λ€κ³  νκ°νμ¬ μ€λ³΅μ νμ©νμ§ μλλ€. 0κ³Ό -0λ setμ λμΌνλ€λΌκ³  νκ°ν΄μ μ€λ³΅ νμ©μ νμ§μλλ€.

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

μ΄λ κ°μ΄λ  setκ°μ²΄μ μμλ‘ λ€μ΄κ° μ μλ€.

---

## ππ»ββοΈSetκ°μ²΄ μμ μ‘΄μ¬ μ¬λΆ νμΈ

```jsx
const set = new Set([1, 2, 3]);
console.log(set.has(1)); // true
```

Set.prototype.has λ©μλλ₯Ό μ¬μ©νλ©΄ μμκ° μ‘΄μ¬νλμ§ νμΈ κ°λ₯νλ€. λ°νμΌλ‘ λΆλ¦¬μΈ κ°μ μ€λ€.

---

## ππ»ββοΈSetκ°μ²΄ μμ μ­μ 

```jsx
const set = new Set([1, 2, 3]);
console.log(set.delete(1)); // true
console.log(set); // Set(2) { 2, 3 }
```

Set.prototype.delete λ©μλλ₯Ό μ κ³΅νλ€. μμκ° μ­μ  λ¬λ€λ©΄ λ°νμΌλ‘ λΆλ¦¬μΈ κ°μ μ€λ€. deleteλ©μλ μΈμλ‘ μμλ₯Ό μ λ¬ν΄μΌλλ€. μμκ° Reference Typeμ΄λΌλ©΄ μ°Έμ‘° κ°μ λκ²¨μΌ μ­μ κ°λλ€.

```jsx
const set = new Set([1, 2, 3]);
console.log(set.delete(1)); // true
console.log(set); // Set(2) { 2, 3 }
console.log(set.delete(1)); // false λ¬΄μλλ€.
```

μ‘΄μ¬ νμ§ μλ μμλ₯Ό μΈμλ‘ μ λ¬ μ μλ¬λ λ°μνμ§ μκ³  `λ¬΄μ`λλ€.

---

## ππ»ββοΈSetκ°μ²΄ μμ μΌκ΄ μ­μ 

```jsx
const set = new Set([1, 2, 3]);
console.log(set.clear());
console.log(set); // Set(0) {}
```

Set.prototype.clear λ©μλλ₯Ό μ κ³΅νλ€. undefinedλ₯Ό λ°ννλ€.

---

## ππ»ββοΈSetκ°μ²΄ μμ μν

Set.prototype.forEach λ©μλλ₯Ό μ κ³΅ν΄μ `μν`κ° κ°λ₯νλ€. Array.prototype.forEach λ©μλμ μ μ¬νλ€.

Set.prototype.forEach λ©μλμ μ½λ°± ν¨μλ `3κ°`μ μΈμλ₯Ό μ λ¬λ°λλ€.

1. **μ²«λ²μ§Έ μΈμ** : νμ¬ μν μ€μΈ `μμκ°`
2. **λλ²μ§Έ μΈμ** : νμ¬ μν μ€μΈ `μμκ°`
3. **μΈλ²μ§Έ μΈμ** : νμ¬ μν μ€μΈ `this(Set κ°μ²΄ μμ²΄)`

```jsx
const set = new Set([1, 2, 3]);
set.forEach((value1, value2, _this) => console.log(value1, value2, _this));
// 1 1 Set(3) { 1, 2, 3 }
// 2 2 Set(3) { 1, 2, 3 }
// 3 3 Set(3) { 1, 2, 3 }
```

μ²«λ²μ§Έ, λλ²μ§Έ μΈμκ° λμΌνλ€. μ΄μ²λΌ λμνλ μ΄μ λ Array.prototype.forEach λ©μλμ `μΈν°νμ΄μ€`λ₯Ό ν΅μΌνκΈ° μν¨μ΄λ©° λ€λ₯Έ μλ―Έλ μλ€.

```jsx
const set = new Set([1, 2, 3]);
const [a] = set;
console.log(Symbol.iterator in Set.prototype); // true
console.log(a); // 1
console.log(...set); // 1 2 3
for (const iterator of set) console.log(iterator);
```

Set κ°μ²΄λ μ΄ν°λ¬λΈμ΄λ€. μ΄ν°λ¬λΈμ for...foλ¬ΈμΌλ‘ μνκ° κ°λ₯νκ³  μ€νλ λ λ¬Έλ²κ³Ό λμ€νΈλ­μ²λ§ν λΉ μ λμμ΄ λλ€.

set κ°μ²΄λ μμμ μμμ μλ―Έλ₯Ό κ°μ§ μμ§λ§ set κ°μ²΄λ₯Ό μννλ μμλ μμκ° μΆκ°λ μμλ₯Ό λ°λ₯Έλ€.

---

# ππ»ββοΈMapμ΄λβ

Map κ°μ²΄λ `ν€`μ `κ°`μ μμΌλ‘ μ΄λ£¨μ΄μ§ `μ»¬λ μ`μ΄λ€. μΌλ° κ°μ²΄μ μ μ¬νμ§λ§ μ°¨μ΄μ μ΄ μλ€.

| κ΅¬λΆ                   | κ°μ²΄                    | Mapκ°μ²΄               |
| ---------------------- | ----------------------- | --------------------- |
| ν€λ‘ μ¬μ©ν  μ μλ κ° | λ¬Έμμ΄ λλ μ¬λ² κ°     | κ°μ²΄λ₯Ό ν¬ν¨ν λͺ¨λ  κ° |
| μ΄ν°λ¬λΈ               | X                       | O                     |
| μμ κ°μ νμΈ         | Object.keys(obj).length | map.size              |

---

## ππ»ββοΈMap κ°μ²΄μ μμ±

```jsx
const map = new Map();
console.log(map); // Map(0) {}
```

μλ°μ€ν¬λ¦½νΈλ Map μμ±μ ν¨μλ₯Ό μ κ³΅νλ€. Map μμ±μ ν¨μλ‘ map κ°μ²΄λ₯Ό μμ±ν  μ μλ€. μΈμλ‘ μλ¬΄κ²λ μ λ¬νμ§ μμΌλ©΄ λΉ mapμ΄ μμ±λλ€.

```jsx
const map = new Map([
  ["key1", "value1"],
  ["key2", "value2"],
]);
console.log(map); //Map(2) { 'key1' => 'value1', 'key2' => 'value2' }
```

Map μμ±μ ν¨μ μΈμλ‘ μ΄ν°λ¬λΈμ μ λ¬ λ°μ μ μλ€. `ν€`μ `κ°`μ μμΌλ‘ μ΄λ£¨μ΄μ§ μμλ‘ κ΅¬μ±λ μ΄ν°λ¬λΈμ μ λ¬ν΄μΌλλ€. `ν€`μ `κ°`μ μμ΄ μλλ©΄ μλ¬λ₯Ό λ°μ μν¨λ€.

```jsx
const map = new Map([
  ["key1", "value1"],
  ["key1", "value2"],
]);
console.log(map); // Map(1) { 'key1' => 'value2' }
```

μ€λ³΅λ ν€λ Map κ°μ²΄μ μμλ‘ μ μ₯λμ§ μλλ€.

## ππ»ββοΈMap κ°μ²΄ μμ κ°μ νμΈ

```jsx
const map = new Map([
  ["key1", "value1"],
  ["key2", "value2"],
]);
console.log(map.size); // 2
map.size = 100; // λ¬΄μλλ€.
console.log(map.size); // 2
```

Map.prototype.size νλ‘νΌν°λ₯Ό μ κ³΅νλ€. mapμ sizeλ setμ size νλ‘νΌν°μ λμΌνκ² getterλ§ μ κ³΅νλ μ κ·Όμ νλ‘νΌν°λ€. μμλ‘ μ¬μ΄μ¦λ₯Ό λ³κ²½ν  μ μλ€.

## ππ»ββοΈMap κ°μ²΄ μμ μΆκ°

```jsx
const map = new Map();
console.log(map); // Map(0) {}
const _map = map.set("key1", "value1");
console.log(map); // Map(1) { 'key1' => 'value1' }
console.log(_map === map); // true
```

Map.prototype.set λ©μλλ₯Ό μ κ³΅νλ€. setλ©μλ μΈμλ 2κ°λ₯Ό λ°λλ€. μ²«λ² μ§Έ μΈμλ μμμ ν€κ° , λλ² μ§Έ μΈμλ μμμ κ°μ΄λ€. μμ μΆκ°λ₯Ό νλ©΄ μκΈ°μμ (Mapκ°μ²΄ μμ²΄)μ λ°ννλ€.

```jsx
map.set("key2", "value2").set("key3", "value3").set("key4", "value4");
```

μ΄λ° νΉμ§μΌλ‘ λ©μλ μ²΄μ΄λμ΄ κ°λ₯νλ€.

```jsx
map.set("key2", "value2").set("key2", "value2");
console.log(map);
// Map(2) { 'key1' => 'value1', 'key2' => 'value2' }
```

μ€λ³΅λ ν€λ₯Ό νμ© νμ§μλλ€. setλ©μλ μΈμλ‘ μ€λλ ν€κ° λ€μ΄μλ μλ¬λ λ°μνμ§ μκ³  λ¬΄μλλ€.

```jsx
console.log(NaN === NaN); // false
console.log(-0 === +0); // true

const map = new Map();
map.set(NaN, 1);
map.set(NaN, 2);
console.log(map); // Map(1) { NaN => 2 }
map.set(+0, "0μ΄λ€.").set(-0, "-0μ΄λ€.");
console.log(map); // Map(2) { NaN => 2, 0 => '-0μ΄λ€.' }
```

μΌλ° λΉκ΅ μ°μ°μμμ NaNμ μ λ κ°μ κ°μ΄ λμ¬ μ μλ€. Map κ°μ²΄μ ν€λ‘ NaNλ₯Ό μ¬μ©νλ©΄ μ€λ³΅μ νμ©νμ§ μλλ€.

-0κ³Ό +0 λ λμΌνκ² νκ°νμ¬ μ€λ³΅μ νμ©νμ§ μλλ€.

```jsx
const map = new Map();
const lee = { name: "lee" };
const kim = { name: "kim" };

map.set(lee, "developer");
map.set(kim, "PM");

console.log(map);
// Map(2) { { name: 'lee' } => 'developer', { name: 'kim' } => 'PM' }
```

Mapμ `ν€ νμ`μ μ νμ΄ μλ€. λ°λΌμ κ°μ²΄λ₯Ό ν¬ν¨ν `λͺ¨λ  κ°`μ ν€λ‘ μ¬μ©ν  μ μλ€.

## ππ»ββοΈMap κ°μ²΄ μμ μ·¨λ

```jsx
const map = new Map();
const lee = { name: "lee" };
const kim = { name: "kim" };

map.set(lee, "developer");
map.set(kim, "PM");

console.log(map.get(lee)); // developer
console.log(map.get("woo")); // undefined
```

Map.prototype.get λ©μλλ₯Ό μ κ³΅νλ€. get λ©μλ μΈμλ‘ ν€λ₯Ό μ λ¬νλ©΄ Mapκ°μ²΄μμ μΈμλ‘ μ λ¬ν ν€λ₯Ό κ°λ κ°μ λ°ννλ€. ν€κ° μλ€λ©΄ `undefined`λ₯Ό λ°ννλ€.

## ππ»ββοΈMap κ°μ²΄ μμ μ‘΄μ¬ μ¬λΆ νμΈ

```jsx
const map = new Map();
const lee = { name: "lee" };
const kim = { name: "kim" };

map.set(lee, "developer");
map.set(kim, "PM");

console.log(map.has(lee)); // true
console.log(map.has("woo")); // false
```

Map.prototype.hasλ©μλλ₯Ό μ κ³΅νλ€. μΈμλ‘ ν€λ₯Ό μ λ¬νλ©΄ λΆλ¦¬μΈ κ°μ λ°ννλ€. μμΌλ©΄ `true` μμΌλ©΄ `false`λ€.

## ππ»ββοΈMap κ°μ²΄ μμ μ­μ 

```jsx
const map = new Map();
const lee = { name: "lee" };
const kim = { name: "kim" };

map.set(lee, "developer");
map.set(kim, "PM");

console.log(map.delete(lee)); // true
console.log(map.delete("woo")); // false
```

Map.prototype.deleteλ©μλλ₯Ό μ κ³΅νλ€. μ­μ  μ±κ³΅ μ¬λΆλ₯Ό λΆλ¦¬μΈ κ°μ λ°ννλ€.

## ππ»ββοΈMap κ°μ²΄ μμ μΌκ΄ μ­μ 

```jsx
const map = new Map();
const lee = { name: "lee" };
const kim = { name: "kim" };

map.set(lee, "developer");
map.set(kim, "PM");

console.log(map.clear()); // undefined
console.log(map); // Map(0) {}
```

Map.prototype.clearλ©μλλ₯Ό μ κ³΅νλ€. clearλ©μλλ μΈμ λ `undefined`λ₯Ό λ°ννλ€.

## ππ»ββοΈMap κ°μ²΄ μμ μν

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

Map κ°μ²΄μ μμλ₯Ό μννλ €λ©΄ Map.prototype.forEach λ©μλλ₯Ό μ¬μ©νλ€. Map.prototype.forEach λ©μλλ Array.prototype.forEach λ©μλμ μ μ¬νλ€.

Map.prototype.forEach λ©μλ μ½λ°± ν¨μλ `3κ°`μ μΈμλ₯Ό μ λ¬ λ°λλ€.

1. **μ²« λ²μ§Έ μΈμ :** νμ¬ μν μ€μΈ `μμκ°`
2. **λ λ²μ§Έ μΈμ :** νμ¬ μν μ€μΈ `μμν€`
3. **μΈ λ²μ§Έ μΈμ :** νμ¬ μν μ€μΈ `Mapκ°μ²΄ μμ²΄`

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

Map κ°μ²΄λ μ΄ν°λ¬λΈμ΄λ€. for..ofλ¬Έ, μ€νλ λ λ¬Έλ², λμ€νΈλ­μ²λ§ ν λΉμ λμμ΄ λλ€.

```jsx
const iterator = map.keys(); // μ΄ν°λ μ΄ν° λ°ν
console.log(iterator.next());
```

Map κ°μ²΄λ μ΄ν°λ μ΄ν° κ°μ²΄λ₯Ό λ°ννλ λ©μλλ₯Ό μ κ³΅νλ€.

| Map λ©μλ            | μ€λͺ                                                                                           |
| --------------------- | ---------------------------------------------------------------------------------------------- |
| Map.prototype.keys    | Map κ°μ²΄μμ μμν€λ₯Ό κ°μΌλ‘ κ°λ μ΄ν°λ¬λΈμ΄λ©΄μ λμμ μ΄ν°λ μ΄ν°μΈ κ°μ²΄λ₯Ό λ°ννλ€.          |
| Map.prototype.values  | Map κ°μ²΄μμ μμκ°λ₯Ό κ°μΌλ‘ κ°λ μ΄ν°λ¬λΈμ΄λ©΄μ λμμ μ΄ν°λ μ΄ν°μΈ κ°μ²΄λ₯Ό λ°ννλ€.          |
| Map.prototype.entries | Map κ°μ²΄μμ μμν€μ μμκ°μ κ°μΌλ‘ κ°λ μ΄ν°λ¬λΈμ΄λ©΄μ λμμ μ΄ν°λ μ΄ν°μΈ κ°μ²΄λ₯Ό λ°ννλ€. |

```jsx
const keys_iterator = map.keys(); // μ΄ν°λ μ΄ν° λ°ν
for (const iterator of keys_iterator) console.log(iterator);
// { name: 'lee' } { name: 'kim' }
const values_iterator = map.values(); // μ΄ν°λ μ΄ν° λ°ν
for (const iterator of values_iterator) console.log(iterator);
// developer PM
const entries_iterator = map.entries(); // μ΄ν°λ μ΄ν° λ°ν
for (const iterator of entries_iterator) console.log(iterator);
// [ { name: 'lee' }, 'developer' ] [ { name: 'kim' }, 'PM' ]
```

Map κ°μ²΄λ μμμ μμμ μλ―Έλ₯Ό κ°μ§ μμ§λ§ Map κ°μ²΄λ₯Ό μννλ μμλ μμκ° μΆκ°λ μμλ₯Ό λ°λ₯Έλ€.
