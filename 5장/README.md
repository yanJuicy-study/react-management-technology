05 - ref

dom에 직접적으로 접근시 사용.

예를 들어 여러 input중 특정 요소에 커서를 위치시킨다거나 할 때.

두 가지 방법으로 사용 가능하다.

- callback function
- createRef

콜백 함수의 경우

```jsx
<input ref={(ref) => {this.input=ref}} />
```

요소에 ref콜백 함수를 props로 전달한다.

ref콜백 함수를 ref값을 파라미터로 전달받는다.

이 때 this.input은 input요소의 dom을 가리키게 된다.

네이밍은 this.fuck 등 자유롭게 지정 가능하다.

createRef의 경우.(리액트 v16.3부터 사용가능)

```jsx
class RefSample extends Component {
  input = React.createRef();

	handleFocus = () => {
    this.input.current.focus();
  }

	render() {
    return (
      <div>
        <input ref={this.input} />
      </div>
    );
  }
}
```

React.createRef()를 담은 멤버 변수를 

원하는 요소에 ref props로 설정한다.

dom에 접근 시 this.input.current로 조회할 수 있다.

ref는 dom이 아닌 컴포넌트에도 적용 가능하다.

컴포넌트 내부의 dom을 해당 컴포넌트 외부에서 접근시 사용한다.

```jsx
<MyComponent ref={(ref) => {this.myComponent=ref}} />
```
