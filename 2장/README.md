# 02 - JSX

리액트를 들어가기 전, 리액트에서 사용되는 jsx의 특징 및 문법에 관한 정리.

Bundler, webpack

react는 기본적으로 node_modules 디렉터리에 react관련 모듈이 설치되고

import React from ‘react’ 를 통해 리액트를 사용할 수 있다.

이를 가능케 하는 것이 번들러다.

리액트에서는 이 번들러 중 대표적으로 웹팩이 사용된다.

[https://velog.io/@jeff0720/React-개발-환경을-구축하면서-배우는-Webpack-기초](https://velog.io/@jeff0720/React-%EA%B0%9C%EB%B0%9C-%ED%99%98%EA%B2%BD%EC%9D%84-%EA%B5%AC%EC%B6%95%ED%95%98%EB%A9%B4%EC%84%9C-%EB%B0%B0%EC%9A%B0%EB%8A%94-Webpack-%EA%B8%B0%EC%B4%88)

ES6

ECMAScript의 6번째 버전.

2015년 6월에 발표된 버전으로 이전의 ES5와 문법 및 키워드의 차이가 있다.

틀딱 브라우저가 아닌 이상 대부분 ES6로 구동된다.

JSX

JavaScript XML라는 이름 그대로 js에 xml을 추가한 확장 문법이다.

리액트로 개발시에 사용되는 문법이기에 공식 js문법은 아니다.

브라우저에서 실행 전 babel을 이용해 js형태의 코드로 변환된다.

```jsx
function App() {
	return (
      <h1>Fuck you</h1>
    );
}
```

```jsx
function App() {
	return React.createElement("h1", null, "Fuck you");
}
```

이런 식으로.

그냥 알아만 두자.

jsx에는 여러 요소를 사용시엔 최상위 부모 태그가 있어야 한다는 규칙이 있다.

부모 태그를 단순히 형식적으로만 사용한다면 <> </> 형태의 fragment를 사용 할 수 있다. (react v16부터 지원)

jsx내에서는 js표현식을 사용할 수 있다.

```jsx
let message = ‘fuck’;
return (
	<b> {message} </b>
)
```

const, let, var

var를 쓰는 경우.

```jsx
var a = "hello";
  if(true) {
    var a = "bye";
    console.log(a); // bye
  }
  console.log(a); // bye
```

let을 쓰는 경우

```jsx
let a = 1;
  if(true) {
     let a = 2;
		 console.log(a); // 2
  }
  console.log(a); // 1
```

[https://developer.mozilla.org/ko/docs/Glossary/Hoisting](https://developer.mozilla.org/ko/docs/Glossary/Hoisting)

삼항 연산자를 사용하여 렌더링을 분기할 수 있음.

```jsx
<div>
  {name === ‘리액트‘ ? (
    <h1>리액트입니다.</h1>
  ) : (
    <h2>리액트가 아닙니다.</h2>
  )}
</div>
```

and 연산자 사용.

```jsx
return <div>{name === '리액트' ? <h1>리액트입니다.</h1> : null}</div>;
// 또는
return <div>{name === ‘리액트‘ && <h1>리액트입니다.</h1>}</div>;
```

undefined는 렌더링 되지 않는다.

```jsx
const name = undefined;
return name;
```

이러면 지랄한다.

```jsx
const name = undefined;
return name || ‘값이 undefined입니다.‘;
```

와 같이 방지한다.

단 jsx 내부에서 렌더링 하는것은 무관하다.

```jsx
const name = undefined;
return <div>{name}</div>;
```

style을 인라인 형태로 줄 수 있다.

style.css와 다르게 카멜 케이스로 작성한다.

```jsx
const style = {
	backgroundColor: ‘black‘
}

return <div style={style}> Fuck you </div>
```

또는

```jsx
return <div style={{backgroundColor : 'black'}}> Fuck you </div>
```

태그의 클래스는 class가 아닌 className 으로 사용한다.

별 문제는 없지만 크롬 콘솔에서 지랄한다.

모든 태그는 닫아야 한다.

```jsx
<input/>
<label/>

<input> 이러면 또 지랄함
```

jsx내의 주석은 {/* */} 의 형태이다.

렌더링 되지 않는 jsx외부에서는 // 로 쓴다
