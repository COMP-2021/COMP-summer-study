## React Hooks

- Functional Component(함수 컴포넌트)

> return <div>Hello, Hooks</div>

React Hooks로 함수 컴포넌트에서 state(상태)와 ref를 사용할 수 있음

- class vs React Hooks (구구단 예시)

```jsx
<!-- class -->
class GuGuDan extends React.Component {
	state = {
		first: Math.ceil(Math.random() * 9),
		second: Math.ceil(Math.radom() * 9),
		value: '',
		result: '',
	};
}
```

```jsx
<!-- React Hooks -->
const GuGuDan = () => {
	const [first, setFirst] = React.useState( Math.ceil(Math.random() * 9) );
	const [second, setSecond] = React.useState( Math.ceil(Math.random() * 9) );
	const [value, setValue] = React.useState('');
	const [result, setResult] = React.useState('');

	return <div> {first] {second} {value} {result} </div>;
}
```

단, React Hooks 구문은 함수 컴포넌트 내부에 위치해야 함

---

## Webpack

- 여러 개의 JS 파일을 하나의 JS 파일로 합치는 기술

- 모듈 시스템 설정

```jsx
const React = requre('react');
const { Component } = React;       // 파일에서 필요한 패키지나 라이브러리 불러오기

class WordRelay extends Component {
	state = {
	};

	render() {
	}
}

module.exports = WordRelay;  // 컴포넌트를 외부에서 사용할 수 있도록 설정
```

exports한 컴포넌트는 외부에서 사용할 수 있다
const WordRelay = require('./WordRelay');

**but, html에서는 script src에는 하나의 js 파일만 넣을 수 있는 문제점이 있음**

**이를 위해 파일을 하나로 합쳐주는 Webpack을 사용함!**

- webpack 설정

```jsx
const path = require('path');  // node문법으로써 경로 설정 관련 라이브러리

module.exports = {
	name: 'wordrelay-setting',
	model: 'development', // 실서비스: production
	devtool: 'eval',  // 실서비스: hidden-source-map

	entry: {
		app: ['./client.jsx'],  // client.jsx에서 다른 파일을 불러오고 있다면 client.jsx만 불러와도 ok
	}, // 입력
	output: {
		path: path.join(__dirname, 'dist'),  // path 라이브러리 명령어로써 현재 디렉터리에 'dist'라는 디렉터리를 만듦
		filename: 'app.js'
	},  // 출력
};
```

이떄, webpack에서도 babel 세팅을 해야 최신 문법 등을 사용할 수 있음.

> npm i @babel/core → babel의 기본 
npm i @babel/preset-env → 브라우저에 맞게 알아서 최신 문법을 이전 문법으로 바꿔줌
npm i @babel/preset-react → jsx 등 지원
npm i babel-loader → babel과 webpack 연결
