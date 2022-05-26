# Date 객체

# 🙋🏻‍♂️Date객체란❓

자바스크립트에서 제공하는 `표준 빌트인 생성자 함수`다. Date 생성자 함수로 date 인스턴스를 만들 수 있다.

날짜와 시간(연, 월, 일, 시, 분, 초, 밀리초)을 위한 메서드를 제공하는 `빌트인 객체이면서 생성자 함수`다.

Date객체는 `UTC기준`으로 한다. KST(한국 표준시)는 UTC에 `**9시간**`을 더한 시간이다. UTC보다 **`9시간`**이 빠르다.

<aside>
📌 **UTC란?**
1972년 1월 1일부터 시행된 국제 표준시로 국제 사회가 사용하는 과학적 시간의 표준입니다.  0시 기준점에 도달하는 도시는 `**영국 런던**`이다.

</aside>

---

# 🙋🏻‍♂️Date 생성자 함수란❓

Date 생성자 함수로 만든 인스턴스는 내부적으로 `**UTC기점**`으로 날짜, 시간을 나타내는 정수값을 갖는다.

```jsx
const date = new Date();
console.log(date.getTime()); // 1649320264053
```

현재 날짜와 시간은 자바스크립트 코드가 실행된 시스템의 시계에 의해 결정된다.

```jsx
const date1 = new Date("1970-01-01");
console.log(date1.getTime()); // 0
const date2 = new Date("1970-01-02");
console.log(date2.getTime()); // 86400000
```

`**UTC 기점**`으로 1970년 1월 1일은 정수 0부터 시작이 된다. 여기에 하루가 경과하면 1일(86,400,000)을 밀리초(24h _ 60m _ 60s \* 1000ms)로 환산되서 더 해진다.

다른 날짜와 시간을 다루고 싶다면 Date 생성자 함수 인수로 명시적으로 해당 날짜와 시간을 전달하면 된다.

### 🔎 1. new Date()

```jsx
console.log(Date());
// Thu Apr 07 2022 17:38:39 GMT+0900 (대한민국 표준시)
```

new 연산자 없이 Date 생성자 함수만 호출하면 현재 날짜와 시간을 문자열로 반환한다.

```jsx
const date = new Date();
console.log(date); // 2022-04-07T08:41:40.120Z
```

생성자 함수 인수를 전달하지 않고 new 연산자를 사용하면 인스턴스를 반환한다. 인스턴스 내부적으로 날짜와 시간을 나타내는 `**정수값**`을 갖지만 인스턴스를 콘솔에 출력하면 기본적으로 날짜와 시간 정보를 출력한다.

### 🔎 2. new Date(milliseconds)

```jsx
const date = new Date(86400000);
console.log(date); // 1970-01-02T00:00:00.000Z
```

생성자 함수 인수로 밀리초를 전달하면 UTC 기점(1970년 1월 1일 00:00:00)으로 밀리초가 더해져 경과한 날짜와 시간을 나타내는 인스턴스는 반환한다.

### 🔎 3. new Date(dateString)

```jsx
const date = new Date("May 26 2022 10:00:00");
console.log(date); // 2022-05-26T01:00:00.000Z
const date1 = new Date("2022/05/26 10:00:00");
console.log(date1); // 2022-05-26T01:00:00.000Z
```

생성자 함수 인수로 문자열을 전달하면 지정된 날짜와 시간을 나타내는 인스턴스를 반환한다. 주의해야되는 것은 전달하는 문자열은 `**Date.parse 메서드**`가 해석 가능한 형식이여야 한다.

### 🔎 4. new Date(year, month[, day, hour, minute, second, millisecond])

```jsx
const date = new Date(2022, 4, 26);
console.log(date); // 2022-05-25T15:00:00.000Z
const date1 = new Date(2022, 4, 26, 10, 00, 00, 0);
console.log(date1); // 2022-05-26T01:00:00.000Z
```

생성자 함수로 연, 월, 일, 시, 분, 초, 밀리초를 의미하는 **`정수 값`**을 전달하면 지정된 날짜와 시간을 나타내는 인스턴스를 반환한다.

| 인수                        | 내용                                                                 |
| --------------------------- | -------------------------------------------------------------------- |
| year                        | 연을 나타내는 1900년 이후 정수, 0부터 99는 1900부터 1999로 처리된다. |
| month                       | 월을 나타내는 0~11까지 정수                                          |
| (주의: 0부터 시작, 0 = 1월) |
| day                         | 일을 나타내는 1~31까지 정수                                          |
| hour                        | 시를 나타내는 0~23까지 정수                                          |
| minute                      | 분을 나타내는 0~59까지 정수                                          |
| second                      | 초를 나타내는 0~59까지 정수                                          |
| millisecond                 | 밀리초를 나타내는 0~999까지 정수                                     |

---

# 🙋🏻‍♂️Date 메서드

### 🔎 1. Date.now

```jsx
console.log(Date.now()); // 1649321927266
```

UTC 기점으로 현재 시간까지 경과한 밀리초를 `**정수**`로 반환한다.

### 🔎 2. Date.parse

```jsx
console.log(Date.parse("2022/05/26/10:00:00:00")); // 1653526800000
```

UTC 기점으로 인수로 전달된 지정 시간까지의 **`밀리초`**를 정수로 반환한다.

메서드의 인수는 **`new Date(dateString)`** 인수와 동일한 형식을 따라야한다.

### 🔎 3. Date.UTC

```jsx
console.log(Date.UTC(1970, 0, 1)); // 0
console.log(Date.UTC(1970, 0, 2, 1, 1, 1, 1)); // 90061001
```

**`new Date(year, month[, day, hour, minute, second, millisecond])`** 인수와 동일한 형식으로 전달해야된다. 전달하면 UTC 기점으로 밀리초가 경과한 정수를 반환한다. 인수는 UTC 기준으로 인식한다. 주의점은 월은 `**0**`부터 시작이다.

### 🔎 4. Date.prototype.getFullYear

```jsx
const date = new Date();
console.log(date.getFullYear()); // 2022
```

연도를 나타내는 정수를 반환한다.

### 🔎 5. Date.prototype.setFullYear

```jsx
const date = new Date();
date.setFullYear(2020);
console.log(date); // 2020-04-07T09:05:13.753Z

console.log(new Date(2022, 10, 1)); // 2022-10-31T15:00:00.000Z
```

연도를 나타내는 정수를 설정한다. 옵션으로 월, 일도 설정 가능하다.

### 🔎 6. Date.prototype.getMonth

```jsx
const date = new Date();
console.log(date.getMonth()); // 3
```

월을 나타내는 `**0 ~ 11**` 정수를 반환한다. 1월은 **`0`**이다.

### 🔎 7. Date.prototype.setMonth

```jsx
const date = new Date();
date.setMonth(10, 1);
console.log(date); // 2022-11-01T09:08:11.331Z
```

월을 나타내는 **`0 ~ 11`**의 정수를 메서드 인수로 전달하면 변경이 된다. 옵셥으로 일도 변경 가능하다.

### 🔎 8. Date.prototype.getDate

```jsx
const date = new Date();
console.log(date.getDate()); // 7
```

날짜 ( 1 ~ 31 )를 나타내는 정수를 반환한다.

### 🔎 9. Date.prototype.setDate

```jsx
const today = new Date();
today.setDate(11);
console.log(today.getDate()); // 11
```

날짜 ( 1 ~ 31 )를 나타내는 정수를 인수로 전달하면 변경이 가능하다.

### 🔎 10. Date.prototype.getDay

```jsx
const today = new Date();
console.log(today.getDay()); // 4
```

요일 ( 0 ~ 6 )을 나타내는 정수를 반환한다. **`일요일(0)`**을 기준으로 숫자가 오른다.

### 🔎 11. Date.prototype.getHours

```jsx
const today = new Date();
console.log(today.getHours()); // 18
```

시간을 ( 0 ~ 23 )을 나타내는 정수를 반환한다.

### 🔎 12. Date.prototype.setHours

```jsx
const today = new Date();
today.setHours(15, 0, 0, 0);
console.log(today.getHours()); // 15
```

시간( 0 ~ 23 )을 나타내는 정수를 인수로 전달하면 시간을 변경할 수 있다. 옵션으로 분, 초, 밀리초도 설정할 수 있다.

### 🔎 13. Date.prototype.getMinutes

```jsx
const today = new Date();
console.log(today.getMinutes()); // 15
```

분( 0 ~ 59 )을 나타내는 정수를 반환한다.

### 🔎 14. Date.prototype.setMinutes

```jsx
const today = new Date();
today.setMinutes(1, 0, 0);
console.log(today.getMinutes()); // 1
```

분( 0 ~ 59 )을 나타내는 정수를 인수로 전달하면 변경할 수 있다. 옵션으로 초, 밀리초도 변경 가능하다.

### 🔎 15 Date.prototype.getSeconds

```jsx
const today = new Date();
console.log(today.getSeconds()); // 21
```

초( 0 ~ 59 )을 나타내는 정수를 반환한다.

### 🔎 16. Date.prototype.setSeconds

```jsx
const today = new Date();
today.setSeconds(22, 11100);
console.log(today.getSeconds()); // 33
```

초( 0 ~ 59 )을 나타내는 정수를 인수로 전달하면 변경할 수 있다. 옵션으로 밀리초도 변경 가능하다.

### 🔎 17. Date.prototype.getMilliseconds

```jsx
console.log(new Date("2020/05/25/12:30:10:150").getMilliseconds()); // 150
```

밀리초( 0 ~ 999 )을 나타내는 정수를 반환한다.

### 🔎 18. Date.prototype.setMilliseconds

```jsx
const today = new Date();
today.setMilliseconds(150);
console.log(today.getMilliseconds()); // 150
```

밀리초( 0 ~ 999 )을 나타내는 정수를 설정한다.

### 🔎 19. Date.prototype.getTime

```jsx
console.log(new Date().getTime()); // 1649323299676
```

UTC 기점으로 인스턴스의 시간까지 경과된 밀리초를 반환한다.

### 🔎 20. Date.prototype.setTime

```jsx
const today = new Date();
today.setTime(86400000); // 86400000은 1일이다.
console.log(today); // 1970-01-02T00:00:00.000Z
```

UTC 기점으로 인스턴스의 시간까지 경과된 밀리초를 설정한다.

### 🔎 21. Date.prototype.getTimezoneOffset

```jsx
const today = new Date();
console.log(today.getTimezoneOffset() / 60); // -9
```

UTC와 인스턴스에 지정된 **`로컬 시간`**과의 차이를 분 단위로 반환한다.
KST는 UTC에서 `**9**`를 더한 값이다. UTC = KST - 9다.

### 🔎 22. Date.prototype.toDateString

```jsx
const today = new Date();
console.log(today.toDateString()); // Thu Apr 07 2022
```

인스턴스의 날짜를 반환한다.

### 🔎 23. Date.prototype.toTimeString

```jsx
const today = new Date();
console.log(today.toTimeString());
// 18:25:29 GMT+0900 (대한민국 표준시)
```

사람이 읽을 수 있는 형식으로 인스턴스의 시간을 표현한 문자열을 반환한다.

### 🔎 24. Date.prototype.toISOString

```jsx
const today = new Date();
console.log(today.toISOString()); // 2022-04-07T09:26:59.457Z
```

ISO 8601 형식으로 인스턴스 객체의 날짜와 시간을 표현한 문자열을 반환한다.

### 🔎 25. Date.prototype.toLocalString

```jsx
const today = new Date();
console.log(today.toLocaleString()); // 2022. 4. 7. 오후 6:28:02
```

인수로 전달한 로컬을 기준으로 인스턴스의 날짜와 시간을 표현한 문자열을 반환한다. `**인수를 전달하지 않으면 브라우저가 동작 중인 시스템 로컬**`을 적용한다.

```jsx
const today = new Date();
console.log(today.toLocaleString()); // 2022. 4. 7. 오후 6:28:02
console.log(today.toLocaleString("ko-KR")); // 2022. 4. 7. 오후 6:28:02
console.log(today.toLocaleString("en-US")); // 4/7/2022, 6:29:19 PM
console.log(today.toLocaleString("ja-JP")); // 2022/4/7 18:29:19
```

### 🔎 25 . Date.prototype.toLocalTimeString

```jsx
const today = new Date();
console.log(today.toLocaleTimeString()); // 오후 6:28:02
console.log(today.toLocaleTimeString("ko-KR")); // 오후 6:28:02
console.log(today.toLocaleTimeString("en-US")); //  6:29:19 PM
console.log(today.toLocaleTimeString("ja-JP")); //  18:29:19
```

인수로 전달한 로컬을 기준으로 인스턴스의 시간을 표현한 문자열을 반환한다.

**`인수를 전달하지 않으면 브라우저가 동작 중인 시스템 로컬`**을 적용한다.
