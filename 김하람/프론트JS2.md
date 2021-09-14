## 객체

→ JS는 8가지의 자료형이 존재하는데, 그 중 7개는 오직 하나의 데이터를 담을 수 있어 '원시형(primitive type)'이라 부름. 나머지 하나가 객체형 자료형인데, 이는 다양한 데이터를 담을 수 있음.

→ 객체는 중괄호 {...}를 이용해 만들 수 있는데, 중괄호 안에는 '키 : 값' 쌍으로 구성된 '프로퍼티(property)'를 여러 개 넣을 수 있음. 키(key)는 문자형, 값(value)는 모든 자료형이 허용됨. 

- 빈 객체를 만드는 방법

```jsx
let user = new Object();  // '객체 생성자' 문법
let user = {};  // '객체 리터럴(object literal)' 문법
```

- 리터럴과 프로퍼티

```jsx
let user = {
	name : "john",
	age : 30
};

alert(user.name);  // 점 표기법(dot notation)을 이용하여 프로퍼티 값 접근
```

- 프로퍼티 추가/삭제

    > user.isAdmin = true;  // 프로퍼티 추가
    delete user.age;  // delete 연산자를 이용해 프로퍼티 삭제

- 특징
1. 여러 단어를 조합해 프로퍼티 이름(프로퍼티 키)를 만든 경우에는 따옴표로 묶어줘야 함

    > "likes birds" : true,

2. 마지막 프로퍼티의 끝은 쉼표로 끝날 수 있음
3. 상수 객체는 수정될 수 있음
4. 변수와 달리 프로퍼티 이름에는 제약이 없음
5. 프로퍼티 키에 문자형이나 심볼형에 속하지 않은 값은 문자열로 자동 형 변환됨

- 대괄호 표기법

    : 여러 단어를 조합해 프로퍼티 키를 만든 경우에는 점 표기법을 사용해 프로퍼티 값을 읽을 수 없음. 점 표기법은 유효한 변수 식별자인 경우에만 사용할 수 있으므로 아닌 경우에는 점 표기법 대신 대괄호 표기법(square bracket notation)을 사용해야함.

    > user["likes birds"] = true;

    +) 또한 변수를 프로퍼티의 키로 사용할 경우 변수는 런타임에 평가되기 때문에 점 표기법에서는 사용하지 못하는 방식을 대괄호 표기법을 통해 해결할 수 있음

    > let key = prompt();

    alert(user[key]);  // 가능
    alert(user.key);  // 불가능

- 계산된 프로퍼티(computed property)

    : 객체를 만들 때 객체 리터럴 안의 프로퍼티가 대괄호로 둘러쌓여 있는 경우, 계산된 프로퍼티라 부름

    ```jsx
    let fruit = prompt("어떤 과일을 구매하시겠습니까?", "apple");

    let bag = {
      [fruit]: 5, // 변수 fruit에서 프로퍼티 이름을 동적으로 받아 옵니다.
    };

    alert( bag.apple ); // fruit에 "apple"이 할당되었다면, 5가 출력됩니다.
    ```

- 단축 프로퍼티

    ```jsx
    function makeUser(name, age) {
      return {
        name, // name: name 과 같음
        age,  // age: age 와 같음
        // ...
      };
    }
    ```

- 'in' 연산자로 프로퍼티 존재 여부 확인

    > "key" in object  // true or false 반환

    → 일치 연산자를 사용하여 프로퍼티 존재 여부를 알아내는 방법(=== undefined)도 사용할 수 있으나, 프로퍼티는 존재하나 값에 undefined가 할당된 경우에는 잘못 작동

- for ... in 반복문

    : 반복문을 사용하여 객체의 모든 키를 순회할 수 있음

    ```jsx
    for (let key in object) {
      // 각 프로퍼티 키(key)를 이용하여 본문(body)을 실행합니다.
    }
    ```

- 객체 정렬 방식

    : 객체의 프로퍼티는, '정수 프로퍼티(integer property)'는 자동으로 정렬되고, 그 외의 프로퍼티는 객체에 추가한 순서 그대로 정렬 됨.
    (정수 프로퍼티란, 변형 없이 정수에서 왔다 갔다 할 수 있는 문자열)
