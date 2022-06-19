(여기서부터 킹액트의 진면목을 볼 수 있다.)

컴포넌트는 클래스형과 함수형이 있다.

리액트 공식 문서는 함수형과 리액트 훅을 사용하는 것을 추천하지만

훅의 state와 생명주기는 클래스형 컴포넌트를 완벽히 대체하지는 못한다.

킹치만 클래스형 컴포넌트는 사용하기가 졸래리 불편하다.

대충 다음의 코드가 있다.

```jsx
import React from 'react';

const testComp = () => {
  return <div> 웹개발 생태계 깡패 교란종 리액트 </div>;
};

export default testComp;
```

() ⇒ {}

ES6부터 도입된 화살표 함수로

function 키워드로 생성된 일반 함수는 this키워드가 종속된 객체를,

화살표 함수는 this 키워드가 종속된 인스턴스(클래스의 오브젝트)를 가리킨다는 차이가 있다.

export

외부 파일에서 해당 파일을 import하기 위해 내보냄.

import

저렇게 export된 파일을 불러옴.

+

```jsx
**import** SignInPage **from** './components/SignInPage';
**import** signInPage **from** './components/SignInPage';
```

import하는 컴포넌트명이 소문자로 시작하면 안됨.

개지랄함 ㄹㅇ

props

부모 컴포넌트에서 자식 컴포넌트로 전달하는 속성 또는 요소이다.

(파라미터와 비슷한 개념)

```jsx
import MyComponent from './MyComponent';

const App = () => {
  return <MyComponent name="fuck you" />;
};
```

와 같이 선언하고

```jsx
const MyComponent = props => {
	return <div>Hey world, {[props](http://props.name/).name}.</div>;
};
```

와 같이 받는다.

props의 기본값

```jsx
const MyComponent = props => {
  return <div>Hey world, {[props](http://props.name/).name}.</div>;
};

MyComponent.defaultProps = {
  name: 'Damn'
};

```

으로 사용할 수 있다.

+

또는 비구조화 할당으로 사용 가능.

```jsx
const MyComponent = ({props.name = 'Damn'}) => {
  return <div>Hey world, {[props](http://props.name/).name}.</div>;
};
```

child

```jsx
import MyComponent from './MyComponent';

const App = () => {
  return <MyComponent name="fuck you" > Bitch </MyComponent>;
};
```

와 같이 컴포넌트 태그 사이에 뭔가가 있을 때, 이를 props로 전달한다면

```jsx
const MyComponent = (props) => {
  return (
    <div>
	    Hey world, {[props](http://props.name/).name}.
      children은 {props.children}
    </div>
  );
};
```

이렇게 받아서 쓰면 된다.

이를 위의 비구조화 할당으로 표현하면

```jsx
const MyComponent = ({ name, children }) => {
  return (
    <div>
      Hey world, {name}.
      children은 {children}
    </div>
  );
};
```

PropsType

props의 타입을 지정하거나 필수 props를 지정시 사용한다.

```jsx
import PropTypes from ‘prop-types‘;

...

MyComponent.propTypes = {
	name: PropTypes.string
};
```

이러면 props 중 name은 반드시 문자열로 전달하고 받아야 한다.

안 그러면 크롬 콘솔에서 지랄.

클래스형 컴포넌트에서 props사용

```jsx
class MyComponent extends Component {
	render() {
		const { name, favoriteNumber, children } = this.props; // 비구조화 할당

		return (
			<div>
			안녕하세요, 제 이름은 {name}입니다. <br />
			children 값은 {children}
			입니다.
			<br />
			제가 좋아하는 숫자는 {favoriteNumber}입니다.
			</div>
		);
	}
}

MyComponent.defaultProps = {
  name: ‘기본 이름‘
};

MyComponent.propTypes = {
  name: PropTypes.string,
  favoriteNumber: PropTypes.number.isRequired
};
```

대충 이렇게 쓰면 된다

defaultProps 와 propTypes는 똑같이 쓰면 되고.

```jsx
class MyComponent extends Component {
	static defaultProps = {
		name: ‘기본 이름‘
	};
	static propTypes = {
		name: PropTypes.string,
		favoriteNumber: PropTypes.number.isRequired
	};
render() {
	...
}
```

또는 클래스 내부에서 지정

state

부모 컴포넌트에서 설정하여 자식 컴포넌트로 전달한다.

기본적으로 컴포넌트 내부에서 바뀔 수 없다.

(state의 불변성)

state는

클래스형 컴포넌트가 지니는 state,

함수형 컴포넌트의 useState를 통해 사용하는 state

이렇게 두 가지 종류가 있다.

클래스형 컴포넌트의 state의 경우

```jsx
import React, { Component } from ‘react‘;

class Counter extends Component {
  constructor(props) {
    super(props);
	  // state의 초기값
    this.state = {
      number: 0
			fixedNumber : 0
    };
  }
  render() {
    const { number } = this.state; // this.state로 조회.
    return (
      <div>
        <h1>{number}</h1>
				<h2> {fixedNumber} </h2>
        <button
		        onClick={() => {    // 클릭 이벤트
            this.setState({ number: number + 1 });
          }}
        >
          +1
        </button>
      </div>
    );
  }
}

export default Counter;
```

클래스형 컴포넌트에 state를 설정할 때에는 생성자를 이용한다.

반드시 super(props)를 호출한다.

이는 클래스형 컴포넌트가 상속하는 리액트의 Component 클래스의 생성자 함수를 호출한다.

state는 여러개가 존재 가능하다.

위의 state를 생성자를 사용하지 않고 지정한다면

```jsx
class Counter extends Component {
  state = {
    number: 0,
    fixedNumber: 0
  };
  render() {
    const { number, fixedNumber } = this.state; // state를 조회할 때는 this.state로 조회합니다.
    return (...);
  }
}
```

this.setState(useState도 마찬가지)는 비동기로 작동한다.

즉, setter의 업데이트 내용이 바로 변하지 않는다.

this.setState에 객체 대신 함수를 인자로 넣어 줌으로써 해결 가능하다.

```jsx
this.setState((prevState, props) => {
	return {
	  // 업데이트하고 싶은 내용
	}
})
```

this.setState 이후.

setState이후 특정 작업을 실행하려는 경우, 두 번째 인자로 콜백 함수를 등록한다.

```jsx
<button
  // onClick을 통해 버튼이 클릭되었을 때 호출할 함수를 지정합니다.
  onClick={() => {
    this.setState(
      {
        number: number + 1
      },
      () => {
        console.log(‘1 더했음’);
        console.log(this.state);
      }
    );
  }}
>
  +1
</button>
```

배열 비구조화 할당

```jsx
const array = [1, 2];
const one = array[0];
const two = array[1];
```

이따위 배열 선언이 있다면

```jsx
const array = [1, 2];
const [one, two] = array;
```

로 표현할 수 있다.

useState와 setState

this.state는 클래스 기반의 상태 관리였다면

useState는 함수 기반의 상태 관리이다.

useState는 리액트 훅의 일종이다.

```jsx
import React, { useState } from ‘react‘;

const Say = () => {
  const [message, setMessage] = useState('');
  const onClickEnter = () => setMessage(‘fuck you’);

return (
    <div>
      <button onClick={onClickEnter}>입장</button>
      <h1>{message}</h1>
    </div>
  );
};

export default Say;
```

와 같이 사용한다.

보편적으로 useState의 setState는

message, setMessage와 같이

set + state의 이름 형태를 카멜 케이스로 사용한다.

당연한 얘기지만 state와 setState는 여러 번 사용 가능하다.

state의 올바른 사용.

예를 들어 다음의 저세상 코드가 있다고 하자.

클래스 컴포넌트의 경우

```jsx
this.state.number = this.state.number + 1;
this.state.array = this.array.push(2);
this.state.object.value = 5;
```

함수형 컴포넌트의 경우

```jsx
const [object, setObject] = useState({ a: 1, b: 1 });
object.b = 2;
```

물론 실행하면 지랄 발광을 한다.

+

useState, this.state와 같은 state는 기본적으로 불변성이라는 특징을 가진다.

불변성이라 함은 메모리 영역에서 직접적인 변경이 불가능하다는 얘기다.

setter와 같은 setState를 통하지 않고서는 그 값이 변경되어서는 안된다.

따라서 다음과 같이 복사본을 만들어 이에 값을 할당하고 

이 복사본을 원본 state에 적용하는 것이 올바른 사용법이다.

객체의 경우

```jsx
const object = { a: 1, b: 2, c: 3 };
const nextObject = { ...object, b: 4 }; // 사본을 만들어서 b 값만 덮어 쓰기
```

spread연산자 ( … )를 사용하여 기존 object 객체를 모두 가져오고, 이 중 b 에만 값을 할당,

이 후 이 변경사항(복사본)을 원본에 적용하면 된다.

배열의 경우

```jsx
const array = [
	{ id: 1, value: true },
	{ id: 2, value: true },
	{ id: 3, value: false }
];
let nextArray = array.concat({ id: 4 }); 
nextArray.filter(item => item.id != = 2);
```

concat은 두 문자열을 합쳐 새로운 문자열을 만들어낸다.

또는 두 배열을 합쳐 새로운 배열을 생성한다.

위의 예제에서는 nextArray는 id : 1 id : 2  id : 3  id : 4 가 될거다

filter는 해당 함수를 통과하는 요소를 모아 새로운 배열로 만든다.

filter를 통해 nextArray는

id : 1 id : 3 id : 4가 될거다.

이렇게 새로 만들어진 배열 nextArray를 기존 원본에 적용해야 한다.

나는 대충 이런식으로 쓴다.

```jsx
**const** [checkedItems, setCheckedItems] **=** useState([]);
**const** [checkedItemsName, setCheckedItemsName] **=** useState([]);

**const** checkedItemHandler **=** (id, title) **=>** {
	setCheckedItems(checkedItems **=>** checkedItems.some(checkId **=>** checkId **===** id) **?** checkedItems.filter(seq **=>** seq **!==** id) **:** checkedItems.concat(id));
	setCheckedItemsName(checkedItemsName **=>** checkedItemsName.some(checkTitle **=>** checkTitle **===** title) **?** checkedItemsName.filter(name **=>** name **!==** title) **:** checkedItemsName.concat(title));
};
```
