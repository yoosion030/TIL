# 🎉EVENT🎉

React 에서도 HTML과 같은 이벤트를 사용합니다.  
> ex ) onclick, onchange, mouseover 등  

---

## 🎉HTML과 차이점

1. React의 이벤트는 소문자 대신 캐멀 케이스( camelCase )를 사용해야합니다. 
   - onclick = {} (x)
   - onClick = {} (o)

2.문자열이 아닌 함수로 전달합니다.
   - onclick = "함수이름()" (x)
   - onClick = {함수이름} (o)


HTML
``` HTML
<button onclick="activateLasers()">
  Activate Lasers
</button>
```
React
```JSX
<button onClick={activateLasers}>
  Activate Lasers
</button>
```

---

## 🎉주의할 점
**DOM 요소에만 이벤트 설정이 가능합니다.** `div`, `span`, `form`, `button` 등의 DOM 요소에는 이벤트 설정이 가능하지만, 리액트의 컴포넌트에는 불가능합니다.   



잘못된 코드
``` JSX
function App() {
  const sayHi = function () {
    alert('hello');
  }
  return (
    <>
      <Component onClick={sayHi}/>
    </>
  );
}
```

---

## 🎉preventDefault
React에서는 `false`를 반환해도 기본 동작을 방지할 수 없습니다.   
반드시 `preventDefault`를 명시적으로 호출해야 합니다. 
HTML
```HTML
<form onsubmit="console.log('You clicked submit.'); return false">
  <button type="submit">Submit</button>
</form>
```

React
``` JSX
function Form() {
  function handleSubmit(e) {
    e.preventDefault();
    console.log('You clicked submit.');
  }

  return (
    <form onSubmit={handleSubmit}>
      <button type="submit">Submit</button>
    </form>
  );
}
```
event를 인자로 받고, e.preventDefault()를 호출하면, 이벤트의 기본동작은 동작하지 않게 되고 console.log만 수행됩니다.

---

## 🎉이벤트 핸들링 - 클래스형 컴포넌트
React에서는 DOM엘리먼트가 생성된 후 리스너를 추가하기 위해 `addEventListener`를 호출할 필요가 없다. 대신, 엘리먼트가 처음 렌더링될때 리스너를 제공하면 된다.  
아래의 예시를 보면, 이벤트핸들러를 클래스의 메서드로 만들었고 이를 컴포넌트 내에서 사용할 수 있다.

- JS의 클래스 메서드는 기본적으로 바인딩되어있지 않기 때문에 `this.handleClick`을 바인딩하지 않고 호출하면 `this`는 `undefined`가 된다. 따라서 바인딩해주고 사용해야한다.
- `binding`을 따로 지정해주지 않으면 해당 메서드에서 호출하는 `this`가 해당 클래스안에서의 `event`값이 아닌 최상위의 `window`에서 값을 가져올 수 있기 때문에 주의해야한다.

```JSX
class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = {isToggleOn: true};
    //콜백에서 `this`가 작동하려면 바인딩을 해줘야한다
    this.handleClick = this.handleClick.bind(this); 
  }

  handleClick() {
    this.setState(state => ({
      isToggleOn: !state.isToggleOn
    }));
  }

  render() {
    return (
      //render() 함수 안에서 this 값은 render() 함수가 속한 컴포넌트를 가리킴
      <button onClick={this.handleClick}>
        {this.state.isToggleOn ? 'ON' : 'OFF'}
      </button>
    );
  }
}
```

---

## 🎉이벤트 핸들링 - 함수형 컴포넌트

함수형 컴포넌트의 상태값은 `useState`훅으로 관리되기 때문에 컴포넌트의 `this`로부터 자유롭습니다.   
또한 함수형 컴포넌트 자체와 함수형 컴포넌트 안에서 선언한 함수들 모두 전역 객체를 `this`로 가지기 때문에 애초에 `this`가 다 같습니다. 그래서 이벤트 핸들러에 콜백 함수를 넘기는 상황에도 딱히 신경 쓸 필요가 없습니다.

- const + 함수 형태
- 요소에 적용하기 위해 this가 따로 필요없음

```JSX
import React, {useState} from "react";

function NumberTest() {
  const [num, setNumber] = useState(0);

  const increase = () => {
    setNumber(num+1);
  } // const + 함수 형태

  return (
    <div>
      <h1>Number Test</h1>
      <h2>{num}</h2>
      <button onClick={increase}>증가</button>
    </div>
  );
}

export default NumberTest;
```