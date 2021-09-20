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

---
## ES6 문법

- 템플릿 문자열

    ```jsx
    var greeting = `${string1} ${string2}`;
    var message = `제품 ${product.name}의 가격은 ${product.price}입니다`;
    var operator1 = `곱셈값은 ${value1 * value2}입니다`;
    ```

- 전개 연산자

    ```jsx
    var array1 = ['one', 'two'];
    var array2 = ['three', 'four'];
    const combined = [...array1, ...array2];
    // 결과 : combined = ['one', 'two', 'three', 'four'];

    const [first, second, three = 'empty', ...others] = array1;
    // 결과 : first = 'one', second = 'two', three = 'empty', others = []

    ```

    - 가변 변수, 불변 변수

        → 가변 변수는 let 키워드로 선언. let으로 선언한 변수는 일거나 수정 가능.

        → 불변 변수는 const 키워드로 선언. const로 선언한 변수는 읽기만 가능. 불변 변수는 값을 다시 할당할 수는 없지만 값을 변경할 수는 있음. 이는 무결성 제약 조건에 위반하기 때문에 개발자 스스로 정해야 함. 이런 경우에는 수정할 불변 변수를 새로 만들어 새 값을 할당하여 새로 정의하는 방법으로 수정하는 방법을 사용.

    - 클래스

        ```jsx
        class Shape {
        	static create(x, y) { return new Shape(x, y); }
        	name = 'Shape';
        	constructor(x, y) {
        		this.move(x, y);
        	}
        	move(x, y) {
        		this.x = x;
        		this.y = y;
        	}
        	area() {
        		return 0;
        	}
        }

        var s = new Shape(0, 0);
        s.area(); // 0
        ```

    - 화살표 함수

        ```jsx
        /* 기존 JS 함수 문법 */
        function add(first, second) {
        	return first + second;
        }
        var add = function(first, second) {
        	return first + second;
        }

        /* ES6 함수 문법 */
        var add = (first, second) => {
        	return first + second;
        };
        var add = (first, second) => first + second; // 본문 블록이 비어있고 결괏값을 바로 반환하는 경우에 중괄호 생략 후 반환 표현식을 넣을 수 있음
        var addAndMultiple = (first, second) => ({ add: first + second, multiple: first * second }); // 반환값이 객체라면 괄호로 결괏값을 감싸 표현 가능

        ```

    - 객체 확장 표현식

        ```jsx
        var x = 0;
        var y = 0;
        var obj = {x, y}; // 객체의 변수를 선언할 때 키값을 생략하면 자동으로 키의 이름으로 키값을 지정
        var randomKeyString = 'other';
        var combined = {
        	['one' + randomKey]: 'some Value',  // 객체 생성 블록 안에 대괄호를 사용하여 표현식을 작성하면 추가하여 계산된 키값을 생성할 수 있음
        };
        var obj2 = {
        	x,
        	methodA() { console.log('method A'); },  // function 키워드를 생략하여 함수를 선언할 수 있음
        	methodB() { return 0; },
        };
        ```

    - 구조 분해 할당

        ```jsx
        var list = [0, 1];
        var [
        	item1,  // 대괄호 블록 사이에 추출하고자 하는 값의 인덱스 위치에 변수를 배치 
        	item2,
        	item3 = -1,  // 선언 부호(=)를 변수와 함께 사용하여 기본값을 할당
        ] = list;  
        [item2, item1] = [item1, item2];  // 인덱스 위치에 각각 변경할 변수를 교차 배치하여 배열의 두 값을 치환

        var obj = {
        	key1: 'one',
        	key2: 'two',
        };
        var {
        	key1: newKey1,  // 콜론 부호와 함께 새 변수명을 선언하여 추출된 키 값을 다른 변수명으로 할당
        	key2,  // 객체의 키값을 변수에 할당
        	key3 = 'default key3 value',
        } = obj;
        ```

        ```jsx
        /* 구조 할동 + 전개 연산자 */
        var [item1, ...otherItems] = [0, 1, 2];
        var { key1, ...others } = { key1: 'one', key2: 'two' };
        // otherItems = [1, 2]
        // others = { key2: 'two' }
        ```

    - 배열 함수
        1. forEach()
        2. map() 

            : 각 배열 요소를 정의된 함수를 통해 변환한 결괏값들로 새 배열을 반환. 배열을 가공하여 새 배열을 만드는 함수. 불변 변수에 할당할 때 자주 사용. forEach()와는 다르게 결괏값을 바로 반환하므로 가변 변수를 사용하지 않아도 됨

        3. reduce()

            ```jsx
            function sum(numbers) {
            	return numbers.reduce( (total, num) => total + sum, 0 );
            }
            sum([1, 2, 3, 4, 5, 6, 7, 8, 9, 10]);  // 55

            /*
            1회차 - total: 0                  num: 1
            2회차 - total: 0+1                qnum: 2
            ...
            10회차 - total: 0+1+...+9         num: 10
            최종 반환값 - total: 0+1+...+10   num: 55
            ```

            → 첫 번째 인자에는 변환함수, 두 번째 인자에는 초깃값 전달

        +) 디바운스(debounce)

        : 어떤 내용을 입력하다가 특정 시간 동안 대기하고 있으면 마지막에 입력된 내용을 바탕으로 서버 요청을 하는 방법

        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/88b16312-f4b0-4fa6-8716-3e9761b5babb/Untitled.png)

        ```jsx
        function debounce(func, delay) {
        	let inDebounce;
        	return function(...args) {
        		if(inDebounce) {
        			clearTimeout(inDebounce);
        		}
        		indebounce = setTimeout(
        			() => func(...args),
        			delay);
        	}
        }
        // func 인자가 '서버요청', delay 인자가 '지연 시간'
        const run = debounce(val => console.log(val), 100);
        run('a');
        run('b');
        run(2);
        // 100ms 이후 2
        ```

        +) 스로틀(throttle) 

        : 입력되는 동안 바로 이전에 요청한 작업을 주기적으로 실행

        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f8e5f267-2ba9-46b8-932d-a15851daabba/Untitled.png)
