## import / require

> const React = require('react');

==

> import React from 'react';

> export const hello =  'hello';  // import { hello }

> export default NumberBaseball;  // import NumberBaseball;

default로 export 한 모듈은 한 번만 불러올 수 있으나
const로 export 한 모듈은 여러 번 사용 가능 

노드 모듈 시스템에서
module.exports = { hello: 'a' };
exports.hello = 'a';
두 문법은 동일

> import 문법은 바벨이 변환해준다

> node는 require, react는 import와 export를 사용한다

---

## map

- map을 통해 반복문

```jsx
{['사과', '바나나', '포도'].map( (v) => {
	return (
		<li>{v}</li>
	);
})};

// 목록 생성
/*
사과
바나나
포도
/*
```

```jsx
{[['사과', 'apple'],
	['바나나', 'banana'],
	['포도', 'grape']
].map( (v) => {
	return (
		<li><b>{v[0]}</b> - {v[1]}</li>
	);
})};

// 목록 생성 -> v는 배열 반환
/*
사과 - apple
바나나 - banana
포도 - grape
/*
```

- 리액트 반복문 key

react가 반복문의 key를 보고 같은 컴포넌트인지 판단하기에 고유한 값을 생성하여 key로 지정해주어야 한다 
key는 성능 최적화를 위해서 사용

> return ( <li key={v.fruit + v.taste}> {v} </li>

---

## 컴포넌트 분리

: 성능 및 코드 최적화, 재사용성을 위해 컴포넌트를 분리함

- Try.jsx

```jsx
import React, [ Component ] from 'react';

class Try extends Component {
	render() {
		return (
			<li>
				<b>{v.fruit}</b> - {i}
				<div>컨텐츠1</div>
				<div>컨텐츠2</div>
			</li>
		)
	}
}

export default Try;
```

- 메인.jsx

```jsx
import Try from './Try.js'

.
.
render() {
	return (
		<>
			{this.fruits.map( (v, i) => {
				return (
					<Try />
				);
			})}
		</>
	);
}
```

- props

: Try.jsx에서 v와 i는 정의되지 않았기에 메인.jsx에서 부를 때 값을 넘겨줘야 한다. 이는 html에서 속성이라 부르는 자리에 넣어준다. react에서는 이를 props라 부른다.

> <Try value={v} index=[i} />

> {this.props.value.fruit} - {this.props.index}

---

## React 속성

- 주석

: {/* react, jsx에서 주석 처리하는 방법 */}

- 배열 push 사용 불가

: push 메소드는 배열에 요소를 추가하기에 배열 자체는 변경되지 않는다. render는 변경된 상태를 감지하기에 push로 요소 추가된 배열은 반영되지 않는다. 따라서 배열을 복제하여 요소를 추가해야 한다.

> const arr2 = [...arr1, 추가할 요소]
