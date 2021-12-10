# react-router-dom v6

## Switch -> Routes

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

## 중첩 라우팅

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

## Route children, component -> element

v5

```JS
<Route path="/" exact component={Home} />
```

v6

```JS
<Route path="/" element={<Home />} />
```

## Route는 Routes의 직속 자식이어야 함

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

## StaticRouter import 위치 변경

v5

```JS
import { StaticRouter } from 'react-router-dom';
```

v6

```JS
import { StaticRouter } from 'react-router-dom/server';
```

## exact 옵션 삭제

만약 하위경로에 여러 라우팅을 매칭시키고 싶다면 다음과 같이 URL 뒤에 \* 을 사용하면 된다.

v6

```JS
<Route path='categories/*' />
```
