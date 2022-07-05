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

**action 활용**
action이 ADD이면 +1, MINUS이면 -1

```js
const countModifier = (count = 0, action) => {
  if (action.type === "ADD") {
    return count + 1;
  } else if (action.type === "MINUS") {
    return count - 1;
  } else {
    return count;
  }
};

countStore.dispatch({ type: "ADD" }); // 0 + 1 = 1
countStore.dispatch({ type: "MINUS" }); // 1 - 1 = 0
```

# 1.3 Subscriptions

subscribe는 store안에 있는 변화들을 알 수 있게 해준다.

**subscribe**

```js
countStore.subscribe(onChange);
```

store이 변화가 일어날 때마다 인자에 넘겨준 함수 실행

**활용**

```js
const onChange = () => {
  number.innerText = countStore.getState();
};

countStore.subscribe(onChange);
```

store의 값이 변할때마다 number에 store의 값 반영

# 1.4 Recap Refactor

**if문 => switch문**

```js
const countModifier = (count = 0, action) => {
  switch (action.type) {
    case "ADD":
      return (count = count + 1);
    case "MINUS":
      return (count = count - 1);
    default:
      return count;
  }
};
```

**string 파라미터보다 실수하기 적은 변수를 파라미터로 사용하자**

```js
const ADD = "ADD";
const MINUS = "MINUS";

add.addEventListener("click", () => countStore.dispatch({ type: ADD }));
minus.addEventListener("click", () => countStore.dispatch({ type: MINUS }));
```

# 2.0 Vanilla ToDo

새로운 투두랑 함께 array를 리턴할 수 있다.

```js
const reducer = (state = [], action) => {
  switch (action.type) {
    case ADD_TODO:
      return [];
    case DELETE_TODO:
      return [];
    default:
      return state;
  }
};
```

**절대 MUTATE STATE를 쓰면 안된다. NEVER!**

# 2.1 State Mutation

- store를 수정할 수 있는 유일한 방법은 action을 보내는 방법뿐이다.
- Mutation이란 변형을 의미한다.
- state를 mutate하면 안된다.
- mutating state하는 대신에 new state objects를 리턴해야한다.
- 상태를 수정하는 것이 아니라 새로운 것을 return 해야한다.

```js
return [...state, { text: action.text }]; // O
return state.push(action.text); // X
```

# 3.1 Connecting the Store

**react-redux 설치**

```
yarn add react-redux
```

react-redux는 **Provider 컴포넌트**를 통해 다른 컴포넌트에서 store를 사용할 수 있게한다.

```js
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./components/App";
import { Provider } from "react-redux";
import store from "./store";

const root = ReactDOM.createRoot(document.getElementById("root"));

root.render(
  <Provider store={store}>
    <App />
  </Provider>
);
```

# 3.2 mapStateToProps

- **connect**함수는 components들을 store에 연결시켜준다.
- connect는 두개의 arguments를 가진다. **state or dispatch**

**connect 사용**

```js
const getCurrentState = () => {};

export default connect(getCurrentState)(Home);
```

connect함수는 store로부터 Home컴포넌트에 state를 가져다 준다.

**mapStateToProps**

```js
function mapStateToProps(state, ownProps) {
  return {};
}
```

- 함수 형식
- 두 종류의 arguments와 함께 호출된다. 하나는 Redux store로부터 온 state이고 나머지는 coomponent의 props이다.
- Redux state로부터 home(component)에 prop으로써 전달하는 것이다.

**활용**

```js
const mapStateToProps = (state, ownProps) => {
  return {
    toDos: state,
  };
};
```

# 3.3 mapDispatchToProps

```js
function mapDispatchToProps(dispatch, ownProps) {
  return {};
}

export default connect(null, mapDispatchToProps)(Home);
```

# 3.5 Detail Screen

**find()**
testing function에 만족하는 첫번째 요소를 반환

```js
const found = arr1.find((ele) => ele > 10);
```

# 4.0 Redux Toolkit

Redux 단점

- 복잡하다.
- 많은 양의 코드를 써야한다. (action, Switch, store.....)

**해결방법**

> Redux Toolkit을 사용하자! (Redux 코드를 짧게 쓸 수 있음. 중요한 것은 Redux Toolkit을 먼저 배우면 안된다.)

**설치**

```
yarn add @reduxjs/toolkit
```

# 4.1 createAction

> action을 생성해주는 함수

```js
const increment = createAction("함수X");
```

첫번째 인자에 함수를 넣지 않는다.

**활용**

```js
// NO Redux Toolkit
const addToDo = (text) => {
  return {
    type: ADD,
    text,
  };
};

// YES Redix Toolkit
const addToDo = createAction("ADD");

console.log(addToDo.type); // ADD
console.log(addToDo()); // {type: 'ADD', payload: undefined};
```

action에서 무언가를 받으면 다 payload 안에 있다.

# 4.2 createReducer

> reducer를 생성해주는 함수

```js
const reducer = createReducer([], {});
```

첫번째 인자에는 초기값(initialState)을 넣는다. 두번째 인자에는 객체를 넣는다.

state를 새로 생성하지 않고 state를 mutate 할 수 있다는 큰 장점이 있다.

**활용**

```js
// NO Redux Toolkit
const reducer = (state = [], action) => {
  switch (action.type) {
    case addToDo.type:
      console.log(action);
      return [{ text: action.payload, id: Date.now() }, ...state];
    case deleteToDo.type:
      return state.filter((toDo) => toDo.id !== action.payload);
    default:
      return state;
  }
};

// YES Redux Toolkit
const reducer = createReducer([], {
  [addToDo]: (state, action) => {
    state.push({ text: action.payload, id: Date.now() });
  } // no return (yes mutate),
  [deleteToDo]: (state, action) =>
    state.filter((toDo) => toDo.id !== action.payload) // yes return(new state / no mutate),
});
```

# 4.3 configureStore

> redux developer tool

```js
const store = legacy_createStore(reducer); // NO Redux Toolkit

const store = configureStore({ reducer }); // YES Redux Toolkit
```

# 4.4 createSlice

> 여태까지 배웠던 것(state, action... )을 캡슐화한 함수이다.

```js
// NO createSlice
const addToDo = createAction("ADD");
const deleteToDo = createAction("DELETE");

const reducer = createReducer([], {
  [addToDo]: (state, action) => {
    state.push({ text: action.payload, id: Date.now() });
  },
  [deleteToDo]: (state, action) =>
    state.filter((toDo) => toDo.id !== action.payload),
});

const store = configureStore({ reducer });

// YES createSlice
const toDos = createSlice({
  name: "toDoReducer",
  initialState: [],
  reducers: {
    add: (state, action) => {
      state.push({ text: action.payload, id: Date.now() });
    },
    remove: (state, action) =>
      state.filter((toDo) => toDo.id !== action.payload),
  },
});

const store = configureStore({ reducer: toDos.reducer });
```
