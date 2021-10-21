# ⭐컴포넌트( Component )

### 정의
- 긴 HTML을 한 단어로 깔끔하게 치환해서 넣을 수 있는 문법
- 앱을 이루는 최소한의 단위

### 종류
- 클래스형 컴포넌트
- 함수형 컴포넌트

## ⭐클래스형 컴포넌트와 함수형 컴포넌트

⭐**클래스형 컴포넌트**
```JSX
import React, { Component } from 'react';

class App extends Component {
  render() {
    const name = '리액트';
    return <div>{name}</div>;
  }
}

export default App;
```
클래스 컴포넌트의 경우 바로 return 하는 것이 아니라  render함수를 호출하고 그 안에서 component를 return 해주어야 한다.


``` JSX
export default App;
```
이 코드는 App이라는 컴포넌트를 내보내겠다는 의미이다. 이렇게 해주면 다른 컴포넌트에서 불러와서 사용할 수 있다.

⭐**함수형 컴포넌트**
```JSX
import React from 'react';

function App() {
  const name = '리액트';
  return <div>{name}</div>;
}

export default App;
```



### 함수형 컴포넌트의 장점
함수형 컴포넌트는 클래스형 컴포넌트보다 선언하기가 좀 더 편하고, 메모리 자원을 덜 사용한다.

### 사용

``` JSX
function Modal(){
  return (
    <div className="modal">
        <p>모달 창 입니다.</p>
    </div>
  )
}
```

1. function을 이용해서 함수를 하나 만든다.
2. 그 함수 안에 있는 `return()` 안에 HTML을 담는다.
3. 원하는 곳에서 `<Modal></Modal>` 이라고 쓰면 `return()` 안에 있는 HTML이 등장한다.


### 🚨사용할 때 규칙
1. Component 이름을 지을 땐 보통 영어 대문자로 시작한다.
2. `return()`안엔 태그들이 평행하게 여러 개가 들어갈 수 없다. = 
component의 return값은 가장 큰 하나의 component로 감싸져야 한다. 

잘못된 코드
```JSX 
return (
    <Component1 />
    <Component2 />
)
```
올바른 코드
```JSX 
return (
   <React.Fragment>
      <Component1 />
      <Component2 />
    </React.Fragment>
)
```

`React.Fragment` = JSX에서 시맨틱태그와 같은 conponent   

`React.Fragment`는 생략이 가능하기 때문에 `<> ... </>`이런 형태로 변경할 수 있다.

```JSX 
return (
   <>
      <Component1 />
      <Component2 />
    </>
)
```

### Component를 사용해야 할 때❓❗
- 사이트에 반복해서 출현하는 HTML 부분
- 내용이 자주 변경될 것 같은 HTML 부분
- 다른 페이지를 만들고 싶을 때 그 페이지의 HTML 내용
- 다른 팀원과 협업할 때 웹 페이지를 컴포넌트 단위로 나눠서 작업을 분배
> 함수 문법 쓰는 것 처럼 생각하면 됨


