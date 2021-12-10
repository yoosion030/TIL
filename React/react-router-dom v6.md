# react-router-dom v6

## Switch -> Routes

`Switch`가 `Routes`로 변경되었다.

v5

```JS
<Switch>
  <Route />
</Routes>
```

v6

```JS
<Routes>
  <Route />
</Routes>
```

## exact 옵션 삭제

기존의 라우트 경우 경로의 앞부분만 일치해도 전부 매칭되기 때문에 정확히 라우트를 일치시키고자 `exact` 옵션을 사용하였다. 하지만 v6부터 `exact`가 기본으로 적용이 되었고, 만약 하위경로에 여러 라우팅을 매칭시키고 싶다면 다음과 같이 URL 뒤에 \* 을 사용하면 된다.

v6

```JS
<Route path='categories/*' />
```

## Route children, component -> element

`Route`에 컴포넌트를 연결하려면 `element`를 사용해야한다.

v5

```JS
<Route path="/" exact component={Home} />
```

v6

```JS
<Route path="/" element={<Home />} />
```

## Route는 Routes의 직속 자식이어야 함

`Route`를 사용하려면 `Routes`로 감싸주어야 한다.

v5

```JS
<Route path="/" exact component={Home} />
```

v6

```JS
<Routes>
    <Route path="/" element={<Home />} />
</Routes>
```

## 중첩 라우팅

v6버전에서는 하나의 파일에 모든 경로를 지정하고 중첩영역 렌더링 요소에는 `Outlet` 속성을 제공하여 더욱 간결하게 중첩된 라우트 구조를 사용하도록 개선되었습니다.

v5

```JS
import {
  BrowserRouter,
  Switch,
  Route,
  Link,
  useRouteMatch
} from 'react-router-dom';

function App() {
  return (
    <BrowserRouter>
      <Switch>
        <Route path="/user" component={User} />
      </Switch>
    </BrowserRouter>
  );
}

function User() {

  const { path } = useRouteMatch();
  return (
    <div>
      <Switch>
        <Route path={`${path}/detail`}>
          <UserDetail />
        </Route>
      </Switch>
    </div>
  );
}
```

v6

```JS
import {
  BrowserRouter,
  Routes,
  Route,
  Outlet
} from 'react-router-dom';

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path='user' element={<User />} >
          <Route path='detail' element={<UserDetail />} />
        </Route>
      </Routes>
    </BrowserRouter>
  );
}

function User() {
  return (
    <>
      <Outlet />
    </>
  )
}
```

## Optional URL -> Route 2개

v5

```JS
<Route path="/optional/:value?"></Route>
```

v6

```JS
<Route path="/optional/:value"></Route>
<Route path="/optional"></Route>
```

## useHistory -> useNavigate

v5

```JS
const history = useHistory();
```

```JS
<button onClick={()=>history.push("/")}>
<button onClick={()=>history.goBack()}>
<button onClick={()=>history.go(-2)}>
```

v6

```JS
const navigate = useNavigate();
```

```JS
<button onClick={()=>navigate('/')}>
<button onClick={()=>navigate(-1)}>
<button onClick={()=>navigate(-2)}>
```

## NavLink에 activeStyle, activeClassName이 사라짐

v5

```JS
<NavLink
    to="/"
    style={{color:'blue'}}
    activeStyle={{color:'green'}} ></NavLink>
```

v6

```JS
<NavLink
    to="/"
    style={({isActive})=>({color: isActive ? 'green' : 'blue'})} ></NavLink>
```

v5

```JS
<NavLink
    to="/"
    className = "nav-link"
    activeClassName = "activated" ></NavLink>
```

v6

```JS
<NavLink
    to="/"
    className = {({isActive}) => "nav-link" + (isActive ? "activated" : "" )} ></NavLink>
```

## useRouteMatch -> 상대경로로 지정

v5

```JS
const match = useRouteMatch();
const { username } = useRarams();
```

```JS
<Link to = {match.url}></Link>
<Link to = {`${math.url}/about`}></Link>
<Link path = {match.path}></Link>
<Link path = {`${math.path}/about`}></Link>
```

v6

```JS
const { username } = useRarams();
```

```JS
<Link to = ""></Link>
<Link to = "about"></Link>
<Link path = ""></Link>
<Link path = "about"></Link>
```

## StaticRouter import 위치 변경

v5

```JS
import { StaticRouter } from 'react-router-dom';
```

v6

```JS
import { StaticRouter } from 'react-router-dom/server';
```

## react-router-config -> useRoutes

기존의 `react-router-config`가 v6 에서 `useRoutes` 라는 훅으로 이동되었습니다. 이제 별도로 패키지를 추가설치 하지 않고 `useRoutes` 훅을 사용해 `routes` 를 구성할 수 있다.

`참고자료`

> [react-router v6에서는 어떤것들이 변했을까??](https://blog.woolta.com/categories/1/posts/211)  
> [React Router v5 → v6 빠르게 훑어보기](https://www.youtube.com/watch?v=CHHXeHVK-8U&t=307s&ab_channel=MinjunKim)
