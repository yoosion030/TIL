# 상태관리

React로 application을 만들 때 필수적으로 상태를 관리하는 상황을 마주치는데 기본적으로 `state`에 기본 값을 지정하고, `setState`를 사용하여 data를 추가, 제거, 수정한다.
독립적인 component내에서 뿐만 아니라 부모-자식, 부모-자식-자식의 자식-자자자자자식 혹은 그 역순과 사돈/팔촌 관계끼리도 `state`를 공유하고 수정하고 다시 공유할 수 있다.

`state`를 `props`로 서로 넘겨주며 data를 공유하고 `setState`를 통해 data를 수정하는 등 간단한 방법으로 React에서 상태관리를 할 수 있지만 application의 규모가 복잡해지고 커질수록 상태 관리는 더욱 더 힘들어진다.

무엇이 이 간단한 방법을 복잡하고 어렵게 만드는지 알아보기 위해선 우선 React의 특성을 알아볼 필요가 있다.

## 1-1. React의 특성 : 렌더링 조건

**1. Props가 변경되었을 때**  
**2. State가 변경되었을 때**  
3. forceUpdate()를 실행하였을 때  
**4. 부모 컴포넌트가 렌더링 되었을 때**

예시

```JS
//App.js

import React from 'react';
import './App.css';

import RightButton from './components/rightButton.component';
import LeftButton from './components/leftButton.component';
import Result from './components/result.component';

class App extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: 0,
    };
  }

  handleIncrease =() => {
    this.setState({
      value: this.state.value +1
    })
  }
  handleDecrease =() => {
    this.setState({
      value: this.state.value -1
    })
  }

  render() {
    return (
      <div className="App">
        <Result sum={this.state.value}/>
	//현재 값을 보여주는 component
        <LeftButton decreasing={this.handleDecrease}/>
          //클릭 할 때 마다 숫자를 1씩 감소시키는 컴포넌트
        <RightButton increasing={this.handleIncrease} />
          //클릭 할 때 마다 숫자를 1씩 증가시키는 컴포넌트
      </div>
    );
  }
}

export default App;


// result.js
import React from 'react';

const Result = props => {
  return <div>{props.sum}</div>;
};

export default Result;



//leftButton.js
import React from 'react';

const LeftButton = props => {
  return (
    <button type="button" onClick={props.decreasing}>
      빼기
    </button>
  );
};

export default LeftButton;



//rightButton.js
import React from 'react';

const RightButton = props => {
  return (
    <button type="button" onClick={props.increasing}>
      더하기
    </button>
  );
};

export default RightButton;
```

위 코드 처럼 `<Result />`, `<LeftButton />` 그리고 `<RightButton />`라는 3개의 자식컴포넌트를 가지고 있는 `App`이 있다. 이 어플리케이션의 유저가 view에서 `RightButton` 컴포넌트 속에 있는 "더하기" 버튼을 클릭하면 세가지의 일이 발생한다.

1. `handleIncrease`라는 이벤트헨들러가 작동하여 `App`컴포넌트의 `state`속 `value`의 값이 0에서 1로 변경되고 그럼 `App`컴포넌트가 다시 렌더링 된다.
2. `Result`컴포넌트의 `props`인 `this.state.value`가 변경되었음으로 `sum`의 이름으로 넘어가는 `props`가 변경된다. 그럼으로 `Result`컴포넌트가 렌더링 된다.
3. App 컴포넌트가 렌더링 되었으므로 그 자식 컴포넌트들 모두가 다시 렌더링 된다.

## 1-2. React특성의 부작용 : 불필요한 렌더링

렌더링이란 컴포넌트를 보여주는 작업이다.

위의 일련의 과정을 살펴보면 렌더링 결과에 영향을 받는 컴포넌트는 App컴포넌트와 Result 컴포넌트인 것을 알 수 있다. Left, Right 버튼은 state가 아무리 변한다 한들 아무런 영향이 없지만 단순히 그들의 부모 컴포넌트인 App 컴포넌트가 렌더링 되었다는 이유로 다시 렌더링이 되었다.

이로인해 불필요한 렌더링이 발생된다는 것을 알 수 있다. 이렇게 불필요한 렌더링이 발생이 된다면 application의 퍼포먼스는 굉장히 낮은 퀄리티가 될 것이고 성능 손실이 일어날 것이다.

---

예를 들어 부모 자식 컴포넌트의 관계가 `1번-2번-3번-4번-5번`으로 되어있고 `state`가 렌더링의 영향을 주는 컴포넌트가 1번과 5번뿐이라고 가정을 해보겠다. 2, 3, 4번 컴포넌트는 단지 1번의 `state`를 `props`로 넘겨주기만 하고 view에 영향을 주지 않음에도 1번의 `state`나 `props`가 변경되었다는 조건 때문에 불필요한 렌더링이 발생하게 된다. 이뿐만 아니라 규모가 커질수록 data flow는 복잡해지기도 하며 버그나 오류에 대한 트랙킹이 불가능해질 수 있다.

그럼 이러한 복잡성과 성능손실을 어떻게 개선할 수 있을까?

## 2. Redux 두두둥장

Redux는 application 전체의 **상태(state)**를 편리하게 관리하기 위해 사용하는 라이브러리 중 하나이다. 앞에서 말한 data flow의 복잡성 개선과 불필요한 렌더링을 막아주는 장점이 있다.

## Redux 사용 전

![](https://media.vlpt.us/images/_jouz_ryul/post/d9646da3-253a-4db1-a2f9-50e90f96726a/%E1%84%85%E1%85%B5%E1%84%83%E1%85%A5%E1%86%A8%E1%84%89%E1%85%B3-%E1%84%8C%E1%85%A5%E1%86%A8%E1%84%8B%E1%85%AD%E1%86%BC%E1%84%8C%E1%85%A5%E1%86%AB.001.jpeg.001.jpeg)

4개의 **테이블(컴포넌트)**과 4명의 **종업원(view)**들이 있고 주방에서 **음식(props)**이 완료되면 **매니저(state)**가 음식을 서버에게 전달하고 정업원이 **서빙(rendering)**을 하는 **식당(어플리케이션)**이 있다.

하지만 이 식당에는 하나의 불변의 규칙이 있는데 음식의 조리가 완료되면 모든 종업원들이 와서 본인 담당 테이블의 음식이 맞는지 확인하여야 한다.

=> 너무 불필요한 동선 낭비!! 댓츠 노노

## Redux 사용 후

![](https://media.vlpt.us/images/_jouz_ryul/post/5add9e36-2071-4d92-99f4-cf13c3533a2a/%E1%84%85%E1%85%B5%E1%84%83%E1%85%A5%E1%86%A8%E1%84%89%E1%85%B3-%E1%84%8C%E1%85%A5%E1%86%A8%E1%84%8B%E1%85%AD%E1%86%BC%E1%84%92%E1%85%AE-2.001.jpeg)

먼저 사장은 테이블 마다 원격으로 주문할 수 있는 **원격 주문 시스템(Redux)**을 각각 설치하고 이 주문기계는 wifi를 통해서 AI로봇과 연동되어 있다. 손님이 테이블에서 원격주문을 하게 되면 모든 정보가 AI로봇에게 입력된다. 주방에서 음식 조리가 완료되면 하나의 로봇이 테이블로 서빙해주는데 이 로봇의 성능은 매우 뛰어나서 일일히 각 테이블에 가서 맞는지 확인할 필요도 없이 해당 테이블로 서빙을 해준다. (전원 공급만 연결 시켜주면 된다.)

단 하나의 연동된 로봇으로 인해 하나의 테이블에 관련한 일에 대해서 다른 테이블의 담당자가 알 필요가 없을 뿐더러 관여하지도 않는다. 결국 식당은 효율적으로 운영될 것이다.

## Redux 가보자~

```
npm install redux react-redux
```

기본적으로 자바스크립트로 작성된 라이브러리에서 모두 사용 가능한 redux와
리액트와 리덕스의 공식 바인딩 패키지인 react-redux를 함께 설치해준다.

### Action

=> state의 변화

식당 예제에서 손님이 모니터를 통해 원격으로 주문내용이 `action`이라고 간단히 생각해볼 수 있다.

action은 `type`과 `payload`의 **프로터리를 포함하는 하나의 객체를 반환하는 함수**다.

`type`에는 어떤 행동을 설명하는 string으로 지정해준다.
`payload`는 state에 추가하거나 수정할 데이터값이 있다면 같이 지정해주고 없다면 type만 지정해주면 된다.

```Js

const increaseCurrentValue = () => ({
  type: 'INCREASE_VALUE'
})

const decreaseCurrentValue =() => ({
  type: 'DECREASE_VALUE'
})
```

아까 봤던 예제

```Js
//rightButton.js
import React from 'react';

const RightButton = props => {
  return (
    <button type="button" onClick={props.increasing}>
      더하기
    </button>
  );
};

export default RightButton;
  // props.increasing에는 App.js에 작성한 handleIncrease함수를 지정되어있다.
  // 함수는 아래와 같다
  // handleIncrease =() => {
  //   this.setState({
  //     value: this.state.value +1
  //   })
  // }


//leftButton.js
import React from 'react';

const LeftButton = props => {
  return (
    <button type="button" onClick={props.decreasing}>
      빼기
    </button>
  );
};

export default LeftButton;
  // props.decreasing에는 App.js에 작성한 handleDecrease함수를 지정되어있다.
  // 함수는 아래와 같다
  // handleDecrease =() => {
  //   this.setState({
  //     value: this.state.value -1
  //   })
  // }
```

이렇게 더하기 버튼의 `onClick` 이벤트는 App.js에서 `props`로 넘어온 이벤트핸들러로 지정 되어 있다. 더하기 버튼을 눌렀을 때 `props`로 넘어온 `increasing`의 값을 사용하라는 뜻이다.

하지만 redux에서는 하나의 state에서 관리하기 때문에 **그 state에 취할 행동과 정보를 (필요하다면) 지정해주는 것이 action이다.**

action 적용은 쩌 밑에서 다시 할거임

## Reducer

`Reducer`는 하나의 `state`가 관리되는 곳에서 직접 `state`를 변경 혹은 추가 시키는 함수이다. 간단하게 말하자면 `Reducer`는 손님이 주문한 음식을 조리해주는 주방의 역할이라고 보면 된다.

⭐`Reducer`함수는 이전의 `state`와 `action`을 매개변수로 갖는다.⭐ 앞써 지정된 `action`의 타입에 따라 각기 다른 `state`의 변화를 줄 수 있다. 추가로 `action`에 `payload`가 지정되어 있다면 그 `payload`를 적용할 수 있다.

**추가하거나 변경한 state는 반드시 하나의 객체로서 반한되어야 한다.** 그 이유는 리덕스 특징 중 하나 때문인데 바로 `Reducer`는 순수함수(같은 입력 값을 넣으면 값은 출력 값을 반환해 내는 함수)로 이루어져야 한다는 것이다. `Reducer`는 이전의 state와 action을 받아서 하나의 변화한 **next state**를 반환한다. 즉 새로운 하나의 state를 반환하기 때문에 next state에 현재의 action과 상관없는 현재 state의 값들도 넣어주어야 하는데 알아서 이전의 `state`를 보존해주는 `setState`와는 조금 다르다는 점을 명심해야 한다.

( 이게 뭔 소리지

```JS
// app.js
...
const INITIAL_STATE = {
    value: 0
}
// 사용하고자 하는 초기 state를 적어준다
export const valueReducer = (state=INITIAL_STATE, action) => {
  // 바로 다음에 설명할 store에 넣어줘야 하기 때문에 export해주는것을 잊지 말자.
  // 또한 state=INITIAL_VALUE 대신에 null로 사용 가능하지만
  // 원하는 값이 있다면 지정 후 INITIAL_STATE를 값으로 넣어주자
  switch (action.type) {
    // switch는 if 와 같다고 보면 된다.
    // action의 property인 action의 값이 존재한다면 다음으로 단계로 함수를 실행한다는 뜻이다.
    case 'INCREASE_VALUE':
      // case도 if와 같다.
      // 만약 action에 작성된 action함수의 type이 case뒤에 오는 string값이라면
      // 밑에있는 return안의 객체를 반환하겠다고 하는것이다
      // payload가 있다면 반환하는 객체에 적용할 수 있다.
      return {
        ...state,
        // Reducer는 전체 state를 하나로 반환해야하기 때문에
        // ...state로 현재 이 액션과 상관없는 state값들을 보존시켜줘야한다.
        value: state.value + 1,
        // 실제로 변경시킬 state값을 변경시켜주었다.
      };
    case 'DECREASE_VALUE':
      return {
        ...state,
        value: state.value - 1,
      };
    default:
      return state;
      // 위의 action.type검사에 하나도 해당하지 않는다면 현재의 state를 그대로 반환한다는 뜻이다.
  }
};
```
