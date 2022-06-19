# 4장 이벤트 핸들링

이벤트: 사용자가 웹 브라우저에서 DOM 요소들과 상호작용 하는 것

### 이벤트 사용 시 주의 사항

1. 이벤트 이름은 카멜 표기법으로 작성한다.

onclick → onClick, onkeyup → onKeyUp

1. 이벤트에 실행할 자바스크립트 코드를 전달하는 것이 아닐, 함수 형태의 값을 전달한다.
    - HTML: 이벤트 설정 시 큰따옴표 안에 실행할 코드를 넣음
    - 리액트: 함수 형태의 객체 전달
    
    ```html
    <button style={{ color: "red" }} onClick={() => setColor("red")}>
    <button onClick={onClickLeave}>퇴장</button>
    ```
    

1. DOM 요소에만 이벤트 설정 가능
    - div, button, input, form, span 등의 DOM 요소에는 이벤트 설정 가능
    - 사용자 정의 컴포넌트에는 이벤트 설정 불가능
    
    ```html
    <MyComponent onClick={doSomething} />  props를 전달해줄 뿐
    
    <div onClick={this.props.onClick}> 이렇게 설정해줘야 함
    ```
    

### 이벤트 종류

- Clipboard
- Composition
- Keyboard
- Focus
- Form
- Mouse
- Selection
- Touch
- UI
- Wheel
- Media
- Image
- Animation
- Transition

### onChange 이벤트 핸들링

e 객체는 SyntheticEvent로 웹 브라우저의 네이티브 이벤트를 감싸는 객체다.

SyntheticEvent 및 네이티브 이벤트와 달리 이벤트가 끝나고 나면 이벤트가 초기화되므로 정보를 참조할 수 없다.

```jsx
class EventPractice extends Component {
  render() {
    return (
      <div>
        <h1>이벤트 연습</h1>
        <input
          type=“text“
          name=“message“
          placeholder=“아무거나 입력해 보세요“
          onChange={
            (e) => {
              console.log(e);
            }
          }
        />
      </div>
    );
  }
}
```

### state에 input 값 담기

함수가 호출될 때 this는 호출부에 따라 결정되므로, 클래스의 임의 메서드가 특정 HTML 요소의 이벤트로 등록되는 과정에서 메서드와 this의 관계가 끊어져 버린다.

바인딩하지 않으면 this가 undefined를 가리킨다.

```jsx
class EventPractice extends Component {
  state = {
    message: "",
  };

  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
    this.handleClick = this.handleClick.bind(this);
  }

  handleChange(e) {
    this.setState({
      message: e.target.value,
    });
  }

  handleClick() {
    alert(this.state.message);
    this.setState({
      message: "",
    });
  }

	render() {
	    return (
	      <div>
	        <h1>이벤트 연습</h1>
	        <input
	          type="text"
	          name="message"
	          placeholder="아무거나 입력해 보세요"
	          value={this.state.message}
	          onChange={this.handleChange}
	        />
	        <button onClick={this.handleClick}>확인</button>
	      </div>
	    );
	  }
```

Property Initailizer Syntax를 이용한 메서드 작성

- 메서드 바인딩은 생성자 메서드에서 하는 것이 정석 but 귀찮음
- 바벨의 transform-class-properties 문법을 사용하는 것이 간단함
