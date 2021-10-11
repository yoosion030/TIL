# State
- 컴포넌트 내부에서 가지고 있는 컴포넌트의 상태값
- 화면에 보여줄 컴포넌트의 UI정보를 지니고 있는 객체
- 컴포넌트 내에서 정의하고 사용하며 얼마든지 데이터가 변경될 수 있음

## Class component state

```JSX
class App extends React.Component {
    constructor() {
        super();
    this.state = {
      color: 'red'
    };
  }

  render() {
      return (
      <div className="App">
        <h1>내가 좋아하는 색은 {this.state.color}</h1>
      </div>
    );
  }
}
```
- 클래스형 컴포넌트에서는 state를 설정할 때는 `constructor` 함수를 작성하여 설정합니다.
- `constructor` 함수는 컴포넌트 선언문(class State extends Component)과 `render` 함수 사이에 작성합니다.
- 그리고 `constructor` 안에는 `super()`를 호출합니다.
- 그 다음에는 `this.state`값에 컴포넌트의 초기 상태값을 설정해줍니다.


## state 객체
``` JSX
 this.state = {
      color: 'red'
    };
```
`state`는 객체로 `key`,`value` 형태로 지정합니다.

## state 사용
```JSX
 <h1>내가 좋아하는 색은 {this.state.color}</h1>
    // this : 해당 컴포넌트
    // this.state : 해당 컴포넌트의 state 객체
    // this.state.color : state 객체의 특정 key(color)값. 즉 "red"
 ```
결과  
`내가 좋아하는 색은 red`

⭐{ this.state.color }⭐
- this.state를 통해 선언한 state값을 가져옴
- {} 중괄호를 이용해 state값을 가져옴

## state 수정하기

```JSX
// Wrong
this.state.color = 'blue';
```

``` JSX
// Correct
this.setState({color: 'blue'});
```

⭐중요⭐
- `this.state`를 지정할 수 있는 유일한 공간은 바로 `constructor`입니다.
- state 객체의 값들은 `setState()`를 통해 값을 변경할 수 있습니다.
- `this.state`를 통해 바로 값을 변경할 경우 `render` 함수를 실행하지 않아 화면의 변경사항을 적용할 수 없습니다.


