# 리액트의 Hooks 완벽 정복하기

## 훅이란?

"함수 컴포넌트에서 React state와 생명주기 기능을 **연동, 연결**해주는 함수", 클래스형 컴포넌트의 문제점들을 해결하기위해 나온 것이다.

### 종류

1. useState
2. useEffect
3. useContext
4. useRef
5. useMemo
6. useCallback
7. useReducer
8. useLmperativeHandle
9. useLayoutEffect
10. useDebugValue

### 클래스형 컴포넌트의 단점

- 클래스형 컴포넌트에서 로직을 재사용할 때 사용하는 고차컴포넌트, 렌더 속성값 패턴은 리액트 요소 트리를 깊게 만든다. 따라서 성능에 부정적인 영향과 개발 시 디버깅이 힘들어지는 문제점이 발생한다.
- 서로 연관성 없는 로직들을 하나의 생명주기에서 작성해야 하는 경우가 발생한다.
- `componentDidMount`와 `componentWillUnmount`, `comopnentDidMount`와 `componentDidUpdate`처럼 반복해서 작성해야 하는 코드 발생한다.
- JS의 클래스문법, `this`에 대한 이해가 필요해, `React의` 진입장벽을 높힌다.

### 훅의 장점

- 여러 훅기리 재조립이 가능하므로, 재사용 가능한 로직을 쉽게 만들 수 있다.
- 로직을 한 곳에 모을 수 있다.
- 훅은 단수한 함수이기 때문에 정적타입 언어에서도 타입을 쉽게 작성할 수 있다.

## 1. useState

usetState는 가장 기본적인 Hook으로 함수형 컴포넌트에서도 가변적인 상태를 지니고 있게 해준다.

useState를 사용할 땐 코드의 상단에 `import`구문을 통하여 불러오고 다음과 같이 사용한다. 배열 비구조화 문법을 이용해 받는 것이기 때문에, `state`와 `setState`의 이름은 임의로 정할 수 있다.

```JS
import useState from 'react';

const [value, setValue] = useState(0);
```

이 함수의 파라미터에는 상태의 기본값을 넣어준다. 이 함수가 호출되고 나면 배열들 반환하는데, 그 배열의 첫번째 원소는 상태값이고, 두번째 원소는 상태를 설정하는 함수이다. 이 함수에 파라미터를 넣어서 호출하게되면 전달받은 파라미터로 값이 바뀌게 되고 컴포넌트는 정상적으로 리렌더링된다.

### 하나의 useState()로 여러 상탯값 관리하기 (객체)

```JS
import React, { useState } from 'react'
export default function Profile () {
    const [state,setState] = useState({name:'',age:0})
    return (
        <div>
            <p>{`name is ${state.name}`}</p>
            <p>{`age is ${state.age}`}</p>
            <input type='text' value={state.name}
            onChange={e=>setState({...state,name:e.target.value})}/>
            <input type='text' value={state.age}
            onChange={e=>setState({...state,age:e.target.value})}/>
        </div>
    )
}
```

클래스형 컴포넌트 에서도 강태값을 관리하는 것과 마찬가지로 객체형태로 관리할 수도 있다.  
주의할 점은 클래스형 컴포넌트에서는 `setState`를 하면 병합이 되지만 함수형 컴포넌트에서는 이전 상탓값을 지운다. 다라서 다른 상탯값들이 지워지지 않도록 **펼침연산자** `...state`를 사용해 펼쳐 넣어줘야 한다.

## 2. useEffect

useEffect는 리액트 컴포넌트가 렌더링 될때마다 특정 작업을 수행하도록 설정할 수 있는 Hook이다. 클래스형 컴포넌트의 `componentDidMount` 와 `componentDidUpdate` 를 합친 형태로 보아도 무방하다.

useEffect로 전달된 함수는 레이아웃 배치, 화면 그리기가 완료될 때까지 지연된 뒤 실행된다. (화면 그리는걸 막으면 안되기 때문에) 그리고 다음 렌더링이 발생하기 전에 실행되는 것도 보장된다. 물론 대부분의 작업이 렌더링을 차단해서는 안되지만, 사용자가 UI데이터와 화면의 내용 불일치를 경헙하지 않도록 동기적으로 Effect를 발생시키고 싶다면 `useLayoutEffect`함수를 이용하면 된다.

- useEffect는 화면이 다 그려진 뒤 실행된다.
- useLayoutEffect는 화면이 그려지기 이전시점에 실행된다.

### 2.1 마운트 될 때만 실행하고 싶을 때

만약 컴포넌트가 화면에 가장 처음 렌더링 될 때만 실행되고 업데이트할 경우 실행할 필요가 없을 때 함수의 두번째 파라미터로 비어있는 배열을 넣어주면 된다.

```JS
useEffect(()=> {
    console.log('마운트 될 때만 실행됩니다.')
},[])
```

컴포넌트가 처음 나타날 때만 실행되고 그 이후에는 콘솔에 문구가 나타나지 않는다.

### 2.2 특정 값이 업데이트 될 때만 실행하고 싶을 때

```JS
componentDidUpdate(prevProps, prevState) {
  if (prevProps.value !== this.props.value) {
    doSomething();
  }
}
```

위 코드에서는 props 안에 들어있는 value값이 바뀔 때에만 특정 작업을 수행하도록 한다. 만약 이러한 작업을 `useEffect`에서 해야한다면 두번째 파라미터로 전달되는 배열안에 검사하고 싶은 값을 넣어주면 된다.

```JS
 useEffect(() => {
    console.log(value);
  }, [value]);
```

### 2.3 useEffect에서 API 호출

```JS
import React, { useState, useEffect } from 'react'
function getUserAPI(userID) {
    // .... 비동기통신
    return new Promise(resolve=>{
        resolve({
            name : 'jack',
            age : '30'
        })
    })
}
export default function Profile({userID}) {
    const [user,setUser] = useState(null);
    useEffect(()=>{
        getUserAPI(userID).then(data=>setUser(data))
    },[userID]);
    return (
        <div>
            {!user && <p>사용자 정보를 가져오는중...</p>}
            {user && (
                <>
                <p>{`name is ${user.name}`}</p>
                <p>{`age is ${user.age}`}</p>
                </>
            )}
        </div>
    );
}
```

`useEffect`함수는 두버내 매개변수로 의존성배열을 받습니다. `useEffect`훅에서 API통신을 하면 렌더링할 때마다 호출되기 때문에 불필요하게 동작합니다. useEffect함수의 **두번째 매개변수로 배열을 입력하면, 배열의 값이 변경되는 경우에만 함수가 호출됩니다.** 여기에서는 `userID`가 변경되는 경우에만 호출됩니다.
