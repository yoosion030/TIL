# react-router-dom v6

## Switch -> Routes

## useHistory -> useNavigate

```JS
// v5
const history = useHistory();
```

```JS
<button onClick={()=>history.push("/")}>
<button onClick={()=>history.goBack()}>
<button onClick={()=>history.go(-2)}>

```

```JS
// v6
const navigate = useNavigate();
```

```JS
<button onClick={()=>navigate('/')}>
<button onClick={()=>navigate(-1)}>
<button onClick={()=>navigate(-2)}>
```

## useRouteMatch -> 상대경로로 지정

```JS
// v5
const match = useRouteMatch();
const { username } = useRarams();
```

```JS
<Link to = {match.url}></Link>
<Link to = {`${math.url}/about`}></Link>
<Link path = {match.path}></Link>
<Link path = {`${math.path}/about`}></Link>
```

```JS
// v6
const { username } = useRarams();
```

```JS
<Link to = ""></Link>
<Link to = "about"></Link>
<Link path = ""></Link>
<Link path = "about"></Link>
```

## Route children, component -> element

```JS
// v5
<Route path="/" exact component={Home} />
```

```JS
// v6
<Route path="/" element={<P.Home />} />
```

## Route는 Routes의 직속 자식이어야 함

```JS
// v5
<Route path="/" exact component={Home} />
```

```JS
// v6
<Routes>
    <Route path="/" exact component={Home} />
</Routes>
```
