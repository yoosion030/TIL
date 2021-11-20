# react-router-dom

## react-router-dom이란?

리액트 라우터 돔을 이용하면 페이지의 로딩없이 페이지에 필요한 컴포넌트들을 렌더링 하여 보여주도록 도와줍니다.

## 사용방법

react-router-dom을 사용할려면 **npm**이나 **yarn**을 이용하여 모듈을 설치해주어야 합니다.

**명령어**  
npm  
`npm i react-router-dom`  
yarn  
`yarn add react-router-dom`

### Route: 특정 주소에 컴포넌트 연결하기

`<Route path="주소" component={보여주고싶은 컴포넌트}>`

### Link: 누르면 다른 주소로 이동시키기

`<Link to="주소">소개</Link>`

## 예제

```JS
import React from 'react';
import { Route, Link } from 'react-router-dom';
import About from './About';
import Home from './Home';

const App = () => {
  return (
    <div>
      <ul>
        <li>
          <Link to="/">홈</Link>
        </li>
        <li>
          <Link to="/about">소개</Link>
        </li>
      </ul>
      <hr />
      <Route path="/" exact={true} component={Home} />
      <Route path="/about" component={About} />
    </div>
  );
};

export default App;
```

`import { Route, Link } from 'react-router-dom';`

> Route나 Link를 사용할 때에는 import 구문을 무조건 서야함 !!
