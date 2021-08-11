---

## react를 사용하는 이유

1. 사용자 경험이 좋음(웹에서 앱을 구현한듯한)
2. 재사용 컴포넌트(중복되는 부분을 묶어 유지보수 편함)
3. 데이터-화면 일치 시키기 편함

## react 사용하기

```jsx
<script crossorigin src="https://unpkg.com/react@17/umd/react.development.js"></script>

<script crossorigin src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
```

```jsx
<html>
    <head>
        <script crossorigin src="https://unpkg.com/react@17/umd/react.development.js"></script>
        <script crossorigin src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
    </head>
    <body>
        <div id="root"></div> 
        <script>
            const e = React.createElement;

            class LikeButton extends React.Component {
                constructor(props) {
                    super(props);
                }

                render() {
                    return e('button', null, 'Like');   // <button>Like</button>
                }
            }
        </script>
        <script>
            ReactDOM.render(e(LikeButton), document.querySelector('#root'));
        </script>
    </body>
</html>
```

⇒ react 스크립트, react dom 스크립트 불러오기

⇒ body 태그 내 첫 번재 스크립트에서 react가 LikeButton이라는 컴포넌트를 만듦

⇒ 그 컴포넌트가 'Like' 버튼을 만들 "예정"

⇒ 두 번째  스크립트에서 'LikeButton' 컴포넌트를 root 안에 그림

> **결과 :** <div id="root"><button>Like</button></div>

---

## HTML 속성과 상태(state)

- 위의 코드에서 render() {} 에서 반환하는 e의 두 번째 요소는 HTMl 속성을 객체 형식으로 표현하는 자리이다.(html -> js 속성은 camel case로)

> return e('button', { onClick: () ⇒ { console.log('clicked')}, type: 'submit'  }, 'Like');

- 바뀔 여지가 있는 부분은 '상태(state)'이다

ex) { onClick: () ⇒ { this.setState({ liked: true }) } }

---

## JSX와 바벨(babel)

- 바벨은 최신 문법과 실험적인 문법을 쓸 수 있도록 도와준다 ex) 자바스크립트에서 html 문법 사용하기

바벨 사용하는 방법

```jsx
<script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
```

 script 속성 추가

```jsx
<script type="text/babel"></script>
```

사용 예시

```jsx
render() {
       return <button type="submit" onClick={() => { this.setState({ liked: true})}}>Like</button
}
```

위를 JSX ( JS + XML ) 이라 한다
