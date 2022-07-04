# 06 - map

데이터의 수에 따라 유동적으로 렌더링 되어야 하는 컴포넌트들이 있다.

가령 테이블 또는 ```<li>``` 등.

이러한 컴포넌트들은 배열 객체의 내장 함수 map을 이용하여 반복적으로 렌더링 할 수 있다.

map의 파라미터는 다음과 같다.

```jsx
arr.map(callback, [thisArg]) {
	...
}
```

의 형태에서

callback

- currentValue : 현재 처리중인 요소
- index : 현재 처리중인 요소의 index
- array : 현재 처리중인 요소의 원본 배열

thisArg(항목) : callback 함수 내부에서 사용할 레퍼런스

기본값은 thisArg이다.

```jsx
const IterationSample = () => {
  const names = ['f', 'u', 'c', 'k'];
  const nameList = names.map(name => <li>{name}</li>);
  return <ul>{nameList}</ul>;
};
```

위의 코드는 개발자도구에서 unique key 경고를 낸다.

key는 컴포넌트 배열을 렌더링 시 어떤 원소에 변화가 생겼는지를 감지하기 위해 사용한다.

전달된 데이터(반복할 컴포넌트)에 고유한 값이 없다면,

map의 index를 사용할 수 있다.

```jsx
const IterationSample = () => {
  const names = ['f', 'u', 'c', 'k'];
  const namesList = names.map((name, index) => 
		<li key={index}>{name}</li>
	);
  return <ul>{namesList}</ul>;
};
```

물론 이래도 뭐라한다.

index를 key로 사용하게 되면 리렌더링이 비효율적으로 발생한다.

[https://medium.com/sjk5766/react-배열의-index를-key로-쓰면-안되는-이유-3ce48b3a18fb](https://medium.com/sjk5766/react-%EB%B0%B0%EC%97%B4%EC%9D%98-index%EB%A5%BC-key%EB%A1%9C-%EC%93%B0%EB%A9%B4-%EC%95%88%EB%90%98%EB%8A%94-%EC%9D%B4%EC%9C%A0-3ce48b3a18fb)

단, 다음의 경우는 index를 key로 사용해도 무관하다.

- 렌더링되는 배열이 정적이거나 변경되지 않을 때.
- 배열내에 고유 id가 없을 때
- 배열이 재정렬되거나 필터링되지 않을 때

```jsx
const IterationSample = () => {
  const [names, setNames] = useState([
    { id: 1, text: 'f' },
    { id: 2, text: 'u' },
    { id: 3, text: 'c' },
    { id: 4, text: 'k' }
  ]);

  const namesList = names.map(name => <li key={name.id}>{name.text}</li>);
  return <ul>{namesList}</ul>;
};
```

배열을 위와 같이 구성 후 key를 id로 사용하면 해결된다.

위와 같은 배열에 요소를 추가 및 제거하는 경우.

두 가지만 잘 지키면 된다.

1. id는 계속해서 증가할 것.
2. 불변성을 지킬 것.

id의 증가는 다음과 같이 구현 가능하다.

```jsx
const [names, setNames] = useState([
{ id: 1, text: ‘눈사람‘ },
{ id: 2, text: ‘얼음‘ },
{ id: 3, text: ‘눈‘ },
{ id: 4, text: ‘바람‘ }
]);
const [inputText, setInputText] = useState(“);
const [nextId, setNextId] = useState(5); // 추가될 id

const onChange = e => setInputText(e.target.value);
const onClick = () => {
const nextNames = names.concat({
	id: nextId, // nextId 값을 id로 설정
	text: inputText
});
setNextId(nextId + 1);
setNames(nextNames);
setInputText(“); 
};
```

불변성 유지를 위해 push가 아닌 concat을 사용한다.

기존 배열(names)에 새로 추가될 요소를 합쳐 새로운 배열 nextNames를 생성한다.

데이터를 제거한다면 filter를 사용할 수 있다.

특정 조건에 해당하는 요소만을 제거한다.

```jsx
const onRemove = id => {
	const nextNames = names.filter(name => [name.id](http://name.id/) !== id);
	setNames(nextNames);
};
```

입력받은 id와 일치하는 요소를 제거한다.

!= / == 는 부등 연산자.

!== / === 는 불일치 연산자이다.

부등 연산자는 비교 수행 전 강제 형변환 후 공통 타입으로 만든다.

불일치 연산자는 타입과 값 모두를 비교한다.

예를 들면 

```jsx
console.log(false == 0) // true
console.log(false === 0) // false
```
