## 비교 연산자

== : 동등 연산자 equality operator

=== : 일치 연산자 strict equality operator

null == undefined : true

null === undefined : false

null > 0 : false

null == 0 : false

null >= 0 : true

undefined > 0 : false

undefined == 0 : false

undefined >= 0 : false

---

## 상수 const와 var

- const로 선언 ⇒ 수정 불가, 초기화 반드시 : 상수
- var ⇒ (== let) : 변수 저장

---

## 조건문 if, switch, 조건부 연산자(삼항 연산자)

- if 문

> if (조건식) {
  동작문;
} else if (조건식) {
  동작문;
} else {
  동작문;
}

- switch 문

> switch (조건식) {
  case 비교조건식:     // 조건식과 비교조건식이 일치(===) 시
    동작문;
    break;
default:                      // 맨 윗줄에 있어도 상관x
  동작문;
}

- 삼항 연산자

> (조건식) ? (참일 때 실행되는 식) : (거짓일 때 실행되는 식);

- null 병합 연산자 (nullish coalescing operator)

: 여러 피연산자 중 그 값이 확정되어 있는 변수를 찾을 수 있음

> x = (a !== null && a !== undefined) ? a : b;

==

> x = a ?? b;

```jsx
let firstName = null;
let lastName = null;
let nickName = "바이올렛";

// null이나 undefined가 아닌 첫 번째 피연산자
alert(firstName ?? lastName ?? nickName ?? "익명의 사용자"); // 바이올렛
```

- 불린형으로의 변환
다음은 모두 불린형으로 변환 시 false
0, 빈문자열(""), null, undefined, NaN
