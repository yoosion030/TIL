# Recoil

## 정의

페이스북에서 내놓은 새로운 상태관리 라이브러리  
=> 이거 사용하면 모든 컴포넌트에서 공통된 변수를 사용할 수 있음

## 설치

```
npm install recoil
yarn add recoil
```

## RecoilRoot

recoil 상태를 사용하는 컴포넌트는 부모 트리 어딘가에 나타나는 `RecoilRoot` 가 필요하다. 루트 컴포넌트가 `RecoilRoot`를 넣기에 가장 좋은 장소다.

```JSX
import React from 'react'
import ReactDOM from 'react-dom'
import App from './App'
import reportWebVitals from './reportWebVitals'
import { RecoilRoot } from 'recoil'

ReactDOM.render(
  <RecoilRoot>
    <React.StrictMode>
      <App />
    </React.StrictMode>
  </RecoilRoot>,
  document.getElementById('root')
)

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals()

```

대충 index에서 RecoilRoot import 해준 뒤 최상위 컴포넌트로 감싸주면 됨

## Atom

- 상태의 일부를 나타냄
- 키와 기본 값만 설정하면 됨
- 숫자, 객체, 배열 등 다양한 형태로 사용 가능함

atom의 값을 읽는 컴포넌트들은 암묵적으로 **atom을 구독한다.** 그래서 atom에 어떤 변화가 있으면 그 atom을 구독하는 모든 컴포넌트들이 재 렌더링 되는 결과가 발생할 것이다.

```JSX
import { atom } from 'recoil'

const textState = atom({
  key: 'textState', // unique ID (with respect to other atoms/selectors)
  default: '', // default value (aka initial value)
});
```

먼저 atom을 import해준다. 그리고 변수 이름을 선언해준 뒤 고유한 key 값과 기본 값을 설정해주면 된다.

## Atom 불러오기

```JSX
import { useResetRecoilState, useRecoilState } from 'recoil'
~~~
  const test = useRecoilValue(textState);
  const [text, setText] = useRecoilState(textState);
```

atom을 사용하고 싶다면 `useRecoilValue`를 import 해준 뒤 괄호 안에 사용할 atom을 넣어주면 된다.
만약 atom을 useState처럼 읽고 쓰게 하기 위해서는 `useRecoilState()`를 import해주고 위의 코드와 같이 사용해주면 된다.

`useResetRecoilState`

```JSX
import { useResetRecoilState } from 'recoil'
~~~
  const test = useResetRecoilState(textState);
```

atom의 state를 default 값으로 reset 시키는 역할을 한다.

## Selector

**state.js**

```JSX
export const cookieState = atom({
  key: 'cookieState',
  default: []
});

export const getCookieSelector = selector({
  key: "cookie/get",
  get: async ({ get }) => {
    try{
      const { data } = await client.get('/cookies');
      return data.data;
    } catch (err) {
    	throw err;
    }
  },
  set: ({set}, newValue)=> {
    set(cookieState, newValue)
  }
});
```

## 장점

- redux에 비해 매우 적은 러닝커브로 익힐 수 있다.
- 웬만한 기능은 기본적으로 hook으로 구현되어 있기 때문에 가져다쓰기도 편하다. 개꿀띠
