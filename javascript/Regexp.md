# Regexp

# 🙋🏻‍♂️정규식이란 ❓

일정한 패턴을 가진 문자열의 집합을 표현하기 위해 사용하는 형식 언어다. 정규식은 문자열을 댓ㅇ으로 `패턴 매칭 기능`을 제공한다.

<aside>
📒 **패턴 매칭 기능**
특정 패턴과 일치하는 문자열을 검색하거나 추출 또는 치환할 수 있는 기능이다.

</aside>

패턴 매칭 기능을 이용하면 반복문과 조건문 없이 패턴을 정의하고 테스트하는 것으로 간단히 체크할 수 있다.

```jsx
const tel = "010-1234-568팔";
const regexp = /^\d{3}-\d{4}-\d{4}$/gi;
console.log(regexp.test(tel)); // false
```

휴대번호가 맞는지 찾는 간단한 정규식이다.

---

# 🙋🏻‍♂️정규 표현식의 생성

생성방법은 `정규식 리터럴방식`과 `RegExp 생성자 함수`를 사용하면된다.

```jsx
const tel = "010-1234-5689";
const regexp1 = /^\d{3}-\d{4}-\d{4}$/gi;
const regexp2 = new RegExp(/^\d{3}-\d{4}-\d{4}$/gi);
console.log(regexp1.test(tel)); // true
console.log(regexp2.test(tel)); // true
```

정규식은 /(슬래쉬)를 이용해 `시작`과 `종료`를 알려줍니다. 슬래쉬 사이에는 `패턴`이 들어가고 종료 슬래쉬 뒤에는 `플래그`가 나열됩니다.

---

# 🙋🏻‍♂️RegExp 메서드

정규표현식을 사용하는 RegExp.prototype 메서드는 `exec`, `test`가 있다. String.prototype에는`match`, `replace`, `search`, `split` 가 있습니다.

`**exec`, `test`, `match` 의 간단한 사용법을 알아보자.\*\*

### 1. RegExp.prototype.exec

```jsx
const target = "Is this all there is?";
const regExp = /is/;
console.log(regExp.exec(target));
// [ 'is', index: 5, input: 'Is this all there is?', groups: undefined ]
console.log(regExp.exec("hi minwook")); // null
```

메서드 인수로 문자열을 전달하면 패턴을 검색하여 매칭 결과를 배열로 반환한다. 매칭이 없는 경우 null을 반환한다.

### 2. RegExp.prototype.test

```jsx
const target = "Is this all there is?";
const regExp = /is/;
console.log(regExp.test(target)); // true
```

메서드 인수로 문자열을 전달하면 패턴을 검색하여 매칭 결과를 불리언을 반환한다. 없는 경우 false를 반환한다.

### 3. String.prototype.match

```jsx
const target = `Is this all there is?`;
console.log(target.match(/is/g)); // 문자열 전체에 대해 검색
// [ 'is', 'is' ]
```

메서드 인수로 정규식을 전달하면 패턴을 검색하여 매칭 결과를 배열로 반환한다. match 메서드는 정규식에 g플래그가 있다면 문자열 전체를 검색해서 반환해준다.

RegExp.prototype.exec는 g플래그가 있어서 처음 매칭된 결과만 반환해준다.

---

# 🙋🏻‍♂️플래그

종료 슬래쉬 뒤에 플래그를 추가하여 검색 방식을 설정할 수 있다. 플래그는 총 6개가 있으며 자주 사용되는 플래그 3개를 정리해봤다.

| 플래그 | 의미        | 설명                                                            |
| ------ | ----------- | --------------------------------------------------------------- |
| i      | ignore case | 대소문자를 구별하지 않고 패턴을 검색한다.                       |
| g      | global      | 대상 문자열 내에서 패턴과 일치하는 모든 문자열을 전역 검색한다. |
| m      | multi line  | 문자열의 행이 바뀌더라도 패턴 검색을 계속한다.                  |

```jsx
const target = `Is this all there is?`;
console.log(target.match(/is/)); // 대소문자 구별
// [ 'is', index: 5, input: 'Is this all there is?', groups: undefined ]
console.log(target.match(/is/i)); // 대소문자 구별을 안한다.
// [ 'Is', index: 0, input: 'Is this all there is?', groups: undefined ]
console.log(target.match(/is/g)); // 문자열 전체에 대해 검색
// [ 'is', 'is' ]
console.log(target.match(/is/gi)); // 문자열 전체에 대해 검색, 대소문자 구별을 안한다.
// [ 'Is', 'is', 'is' ]
```

플패그 사용은 옵션이고 사용 시 순서 상관없이 하나 이상의 플래그를 동시에 설정 가능하다.

아무 플래그도 없다면 `default` 는 대소문자를 구별해서 패턴을 검색한다.

---

# 🙋🏻‍♂️패턴

패턴은 /(슬래쉬)로 열고 닫으며 슬래쉬 사이 따옴표를 생략한 문자열을 작성하면된다. 문자열 내 패턴과 일치하는 문자열이 존재할 때 `정규 표현식과 매치`한다고 표현한다.

### 1. 문자열 검색

```jsx
const target = `Is this all there is?`;
const regExp = /is/;
console.log(target.match(/is/)); // 대소문자 구별
// [ 'is', index: 5, input: 'Is this all there is?', groups: undefined ]
console.log(regExp.test(target)); // true
```

플래그를 생략하며 대소문자를 구별하여 정규 표현식과 매치한 첫 번째 결과만 반환한다.

```jsx
const target = `Is this all there is?`;
const regExp = /is/i;
console.log(target.match(regExp)); // 대소문자 구별 X
// // [ 'Is', index: 0, input: 'Is this all there is?', groups: undefined ]
```

플래그 i는 대소문자 구별하지 않는다.

```jsx
const target = `Is this all there is?`;
const regExp = /is/gi;
console.log(target.match(regExp)); // 대소문자 구별 X
// // [ 'Is', 'is', 'is' ]
```

플래그 g는 문자열 전체에서 패턴과 매치하는 결과를 반환한다.

### 2. 임의의 문자열 검색

```jsx
const target = `Is this all there is?`;
const regExp = /.../g;
console.log(target.match(regExp));
// [
  'Is ', 'thi',
  's a', 'll ',
  'the', 're ',
  'is?'
]
```

. 은 임의의 문자 한 개를 의미한다. 문자열로 올 수 있는 무엇이든 상관없다. `...` 문자열 3개 중 아무거나 매치되어도 상관없다라는 뜻이다.

### 3. 반복 검색

```jsx
const target = `A AA B BB Aa Bb AAA`;
const regExp = /A{1,2}/g;
console.log(target.match(regExp)); // [ 'A', 'AA', 'A', 'AA', 'A' ]
```

최소 m번, 최대 n번 반복되는 문자열을 의미한다.

```jsx
const target = `A AA B BB Aa Bb AAA`;
const regExp = /A{2}/g;
console.log(target.match(regExp)); // [ 'AA', 'AA' ]
console.log(target.match(/A{2,2}/g)); // [ 'AA', 'AA' ]
```

m만 붙여도 가능하다. 이때는 m번 반복하는 문자열을 찾는다. {m} 은 {m,m}과 동일하다.

```jsx
const target = `A AA B BB Aa Bb AAA`;
const regExp = /A{2,}/g;
console.log(target.match(regExp)); // [ 'AA', 'AAA' ]
```

최소 2번 이상되는 문자열을 찾는다.

### 4. OR 검색

```jsx
const target = `A AA B BB Aa Bb AAA`;
const regExp = /A|B/g;
console.log(target.match(regExp));
// [
//   'A', 'A', 'A', 'B',
//   'B', 'B', 'A', 'B',
//   'A', 'A', 'A'
// ]
```

| 은 or 의미를 갖는다. A 또는 B 문자열을 찾는다.

```jsx
const target = `A AA B BB Aa Bb AAA`;
const regExp = /[AB]/g;
console.log(target.match(regExp));
// [
//   'A', 'A', 'A', 'B',
//   'B', 'B', 'A', 'B',
//   'A', 'A', 'A'
// ]
```

[] 대괄호를 써도 동일한 결과를 나타낸다.

### 5. NOT 검색

```jsx
const target = `A AA B BB Aa Bb AAA`;
const regExp = /[^A]/g;
console.log(target.match(regExp));
// [
//   ' ', ' ', 'B', ' ',
//   'B', 'B', ' ', 'a',
//   ' ', 'B', 'b', ' '
// ]
```

^ 는 not의 의미를 갖는다. 예를 들어 [^0-9]는 숫자를 제외한 문자를 의미한다.

### 6. 시작 위치로 검색

```jsx
const target = `https://www.naver.com`;
const regExp = /^https/g;
console.log(regExp.test(target)); // true
```

^은 문자열의 시작을 의미한다. 대괄호 내의 ^는 not의 의미를 가지므로 주의한다.

### 7. 마지막 위치로 검색

```jsx
const target = `https://www.naver.com`;
const regExp = /(.com|.kr)$/g;
console.log(regExp.test(target)); // true
```

$는 문자열의 마지막을 의미한다.
