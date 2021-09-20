- 메서드와 this

    ```jsx
    let user = {
    	// ...
    };

    user.sayHi = function() {
    	alert("Hello");
    };

    user.sayHi(); // Hello
    ```

    ```jsx
    // 아래 두 객체는 동일하게 동작

    user = {
    	sayHi : function() {
    		alert("Hello");
    	}
    };

    // 단축 구문
    user = {
    	sayHi() {
    		alert("Hello");
    	}
    };
    ```

    ```jsx
    let user = {
      name: "John",
      age: 30,

      sayHi() {
        // 'this'는 '현재 객체'를 나타냅니다.
        alert(this.name);
    		// alert(user.name); 외부 변수를 참조해서 객체를 접근하는 것도 가능하나 다른 변수에 할당하면 예기치 못한 결과 발생 가능
      }

    };

    user.sayHi(); // John
    ```

    자바스크립트의 this는 다른 프로그래밍 언어의 this와 동작 방식이 다름.
    this 값은 런타임에 결정됨. 동일한 함수라도 다른 객체가 호출 했다면 this가 참조하는 값이 달라짐

    화살표 함수는 일반 함수와는 달리 고유한 this를 가지지 않음.
    화살표 함수에서 this를 참조하면, 화살표 함수 자체가 아닌 평범한 외부 함수에서 this값을 가져옴

- 심볼형

    : 객체 프로퍼티 키로 오직 문자형과 심볼형만을 허용. 숫자형, 불린형 모두 불가능, 오직 문자형과 심볼형만 가능.

    : 심볼(symbol)은 유일한 식별자(unique indentifier)를 만들고 싶을 때 사용. `Symbol()` 을 사용하여 심볼값 생성 가능

    ```jsx
    // id는 새로운 심볼이 됨
    let id = Symbol();

    // 심볼 id에는 "id"라는 설명이 붙음. 심볼 이름은 디버깅 시 유용하게 쓰임.
    // 설명이 동일한 심볼을 여러 개 만들어도 각 심볼값은 다름.
    let id = Symbol("id");
    ```

    : 심볼을 사용하면 '숨김 프로퍼티'를 만들 수 있음. 숨김 프로퍼티는 외부 코드에서 접근이 불가능하고 값도 덮어쓸 수 있는 프로퍼티. 

    ```jsx
    let user = { // 서드파티 코드에서 가져온 객체
      name: "John"
    };

    let id = Symbol("id");

    user[id] = 1;

    alert( user[id] ); // 심볼을 키로 사용해 데이터에 접근할 수 있습니다.
    ```

키가 심볼인 프로퍼티는 외부 스크립트나 라이브러리가 접근하지 못함. `for...in`, `Object.keys(user)` 등에서도 배제됨. 그러나 `Object.assign` 은 프로퍼티를 배제하지 않고 객체 내 모든 프로퍼티를 복사.

: 심볼은 이름이 같더라도 모두 별개로 취급이나 이름이 같은 심볼이 같은 개체를 가리키길 원하는 경우도 존재. 이를 위해 *전역 심볼 레지스트리(global symbol registry)* 존재. 레지스트리 안에 있는 심볼을 읽거나 새로운 심볼을 생성하려면 `Symbol.for(key)` 사용. 이 메서드는 이름이 key인 심볼을 반환. 조건에 맞는 심볼이 레지스트리 안에 없으면 새로운 심볼 `Symbol(key)` 를 만들고 레지스트리 안에 저장.

```jsx
// 전역 레지스트리에서 심볼을 읽습니다.
let id = Symbol.for("id"); // 심볼이 존재하지 않으면 새로운 심볼을 만듭니다.

// 동일한 이름을 이용해 심볼을 다시 읽습니다(좀 더 멀리 떨어진 코드에서도 가능합니다).
let idAgain = Symbol.for("id");

// 두 심볼은 같습니다.
alert( id === idAgain ); // true
```
