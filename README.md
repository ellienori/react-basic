# THE BASIC OF REACT
## React 세팅
* 관련 내용 확인
  + <https://ko.reactjs.org/versions/>
  + <https://github.com/facebook/react/blob/main/CHANGELOG.md>
* 세팅하기
```html
<script src="https://unpkg.com/react@17.0.2/umd/react.production.min.js"></script>
<script src="https://unpkg.com/react-dom@17.0.2/umd/react-dom.production.min.js"></script>
```
## 세팅 확인하기
* 콘솔 창에서 React라고 치면 관련 Object가 나옴
  + 이제 ReactJS를 사용할 수 있다는 뜻

## React 기초
* __React JS__: App이 아주 interactive 하도록 만들어주는 라이브러리 (엔진)
* __React DOM__: 모든 React elements를 HTML body에 둘 수 있도록 하는 라이브러리/패키지
* html을 쓰지 않고 JS와 React JS를 사용해서 element를 생성할거야 -> React DOM으로 배치 할 거야

## 아무도 이렇게 안할 거지만 개념 이해를 위해 가르쳐주는 방법 (ㅋㅋ)
### element 생성
```js
const span = React.createElement("span");
const button = React.createElement("button", {
  id: "btn", style: {color: "tomato"},
  onClick: () => {
    count++;
  }
}, "Click me!");
const container = React.createElement("div", null, [span, button]);
ReactDOM.render(container, root);
```
  + createElement 안에 들어가는 첫번째 인자는 HTML tag 명과 같아야 함
  + 두번째 인자로 property를 넣을 수 있고 여기에 이벤트도 넣을 수 있다
  + 마지막 인자에 value 값을 넣을 수 있다

### JSX
* javascript를 확장한 문법
  + babel 사용해야 함
```html
<script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
<script type="text/babel">
  const Title = () => {
    return (
      <span id="sexy-span" style={{color: "teal",}}>Total clicks: {count}</span>
    );
  };
  const Button = () => {
    return (
      <button id="btn" style={{backgroundColor: "tomato",}} onClick={() => count++}>Click me!</button>
    );
  };
  const Container = () => (
    <div>
      <Title />
      <Button />
    </div>
  );
  ReactDOM.render(<Container />, root);
</script>
```
  + 꼭 직접 만든 요소는 __Uppercase__ 로 시작할 것
  + 소문자로 쓰면 html에서 제공하는 태그로 이해함

# STATE
## Understanding State
* 데이터가 저장되는 곳
  + 바뀌는 데이터
* 어떻게하면 React JS에 값이 바뀔 데이터를 담을 수 있을까?
* react에서 변수 쓸 때는 ```{}``` 안에 쓴다.

### 아무도 쓰지 않는 그런 방법
* 변수 변경이 되면 새로 render를 한다
  + 바뀐 부분 (count 변수) 만 변경됨 짱이야
```js
let count = 0;
function countUp() {
  count++;
  render();
}
function render() {
  ReactDOM.render(<Container />, root);
}
const root = document.getElementById("root");
const Container = () => (
  <div>
    <h3>Total clicks: {count}</h3>
    <button onClick={countUp}>Click me!</button>
  </div>
);
render();
```

## setState
>const [count, modifier] = React.useState(0);
>(초기값, 함수)
* modifier로 값을 바꾸면 자동으로 render도 됨
```js
const root = document.getElementById("root");
function App() {
  const [count, setCount] = React.useState(0);
  const onClick = () => {
    setCount(count + 1);
  }
  return (
    <div>
      <h3>Total clicks: {count}</h3>
      <button onClick={onClick}>Click me!</button>
    </div>
  );
}
ReactDOM.render(<App />, root);
```

## State Function
* 우리가 위에서 사용한 방법은 count의 값이 다른 곳에서 변경이 되면 우리가 예상하지 못한 값이 나올 수 있다
* 그래서 이전 값을 바탕으로 값을 지정하게 하자
```js
// setCount(count + 1);
setCount((current) => current+1);
```

## Practice: Unit conversion
### jsx 쓸 때 주의해야 할 점
* JS에서 이미 선점된 문법 용어를 사용할 수 없다.
> class -> className
> for -> htmlFor
* script src에 넣은 react 관련 js를 production이 아니라 development로 하면 에러를 미리 확인할 수 있다.

### input에서 값 가져오기
* state로 값을 설정해준 다음 onChange event에서 event.target.value를 가지고 온다
```jsx
function App() {
  const [minutes, setMinutes] = React.useState(0);
  const [hours, setHours] = React.useState(0);
  const onChange = (event) => {
    setMinutes(event.target.value);
  }
  return (
    <div>
      <h1>Supoer Converter</h1>
      <div>
        <label htmlFor="minutes">Minutes</label>
        <input value={minutes} id="minutes" placeholder="Minutes" type="number"
          onChange={onChange} />
      </div>
      <div>
        <h1>You want to convert {minutes} </h1>
      </div>
      <div>
        <label htmlFor="hours">Hours</label>
        <input id="hours" placeholder="Hours" type="number" />
      </div>
    </div>
  );
}
```

### 추가 내용
* disabled={flipped}
```js
const flip = () => {
  setFlipped((current) => !current);
  reset();
}
<input value={flipped ? amount * 60 : amount}
  id="minutes" placeholder="Minutes" type="number"
  onChange={onChange}
  disabled={flipped}/>
```

* value
```js
<input value={flipped ? amount : Math.round(amount/60)} id="hours" .... />
```

### Final Practice
#### 구조
* KmsToMiles(){}와 MinutesToHours(){}를 만들고 App()에서 두 컴포넌트를 품었다.
#### select
```js
const [index, setIndex] = React.useState("0");
const selectIndex = (event) => {
  setIndex(event.target.value);
}
<select onChange={selectIndex}>
  <option value="0">Minutes & Hours</option>
  <option value="1">Kms & Miles</option>
</select>
<div>
  {index === "0" ? <MinutesToHours /> : null }
  {index === "1" ? <KmsToMiles/> : null}
</div>
```

# PROPS
## Understanding props
* 부모 컴포넌트로부터 자식 컴포넌트에게 데이터를 보낼 수 있게 해주는 방법
* 컴포넌트를 사용할 때 인자로 프로퍼티를 넣을 수 있는데 그 인자를 __props__ 라고 한다.
  + 즉 ```<Btn nameOfBtn="Save Changes"/>``` 이런 식으로 ```nameOfBtn```이라는 프로퍼티를 임의로 만들었을 때 실제 컴포넌트에서 ```function Btn(props){}```인자로 받아와서 쓴다.
  + 여기서는 ```{props.nameOfBtn}``` 이렇게 사용할 수 있다.
  + ```function Btn({nameOfBtn, color, ..}){}``` 이런 식으로도 사용할 수 있다. props는 오브젝트니까.
* 이벤트리스너인지 props인지 구분해야 함
  + 예를 들어 ```<Btn nameOfBtn={value} onClick={changeValue}/>```에서 onClick은 컴포넌트 안에 있는 내용이기 때문에 실제 onclick 이벤트리스너가 아니라 prop이다.
  + ```<button onClick=click>``` 여기 들어가는 onClick은 이벤트리스너
  + prop으로 넣은 onClick을 사용하고 싶으면 아래처럼 컴포넌트에 prop을 받아서 넣으면 된다.
  ```js
  function Btn({nameOfBtn, onClick}) {
    return <button onClick={onClick} style={{
      backgroundColor: "tomato",
      color: "white",
      padding: "10px 20px",
      border: 0,
      borderRadius: 10,
    }}>{nameOfBtn}</button>;
  }
  ```

## React Memo
* Memorize: prop이 변경되지 않았다면 우리는 이 컴포넌트가 다시 그려지는 것을 원치 않는다고 기억하게 하는 것
```js
const MemorizedBtn = React.memo(Btn);

<MemorizedBtn nameOfBtn={value} onClick={changeValue}/>
<MemorizedBtn nameOfBtn="Confirm"/>
```

## Prop Types
* props의 데이터타입이 무엇인지 알려줌 (예를 들어 fontSize에 String을 넘길 수도 있잖아)

### import 및 적용
* import
```html
<script src="https://unpkg.com/prop-types@15.7.2/prop-types.js"></script>
```

* 적용
```js
Btn.propTypes = {
  nameOfBtn: PropTypes.string.isRequired,
  fontSize: PropTypes.number,
};
```
  + ```isRequired```를 넣으면 이 값이 무조건 필요하다는 의미

### default 값 설정하기
```js
function Btn({nameOfBtn, fontSize = 14})
```
* props 인자 안에 default 값을 설정할 수 있다.

# CREATE REACT APP (CRA)
## What is the create-react-app?
* react 관련 라이브러리들의 집합체

## 프로젝트 초기화
* CRA를 사용하기 위해서 프로젝트를 새로 생성해야 함
* 그리고 nodeJS 설치 해야 함
* 뒤 이야기는 이제 다음 프로젝트에 이어서!