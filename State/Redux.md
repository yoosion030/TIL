# 1.1 Store and Reducer

**Redux 설치**

```
npm i redux
yarn add redux
```

- store는 data를 저장하는 곳
- CreateStore는 reducer를 요구함
- Reducer는 data를 modify 해주는 함수로 reducer가 return 하는 것은 application에 있는 data가 됨

```js
import { createStore } from "redux"; // store 생성

const reducer = (state = 0) => {
  console.log(state); // 0
  return state;
};
const countStore = createStore(reducer);

console.log(countStore.getState()); // 0
```

# 1.2 Actions

- reducer의 두번째 인자로 action을 받음
- action은 reducer와 소통하기 위한 방법 (값을 어떻게 해야할 지 action의 값을 보고 결정)

**action을 지정해주는 방법**

```js
countStore.dispatch({ type: "HELLO" }); // action은 객체로 넘겨줘야힘

countStore.dispatch("HELLO"); // X
```
