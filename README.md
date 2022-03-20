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
  + 소문자로 쓰면 html에서 제공하는 태그로 이해할 것