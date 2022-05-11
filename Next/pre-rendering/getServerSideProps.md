# getServerSideProps (SSR)

`getServerSideProps` 는 요청할 때마다 html이 생성되기 때문에 데이터가 계속 업데이트 된다.  
요청할때마다 데이터를 계속 불러오는 것이다.  
그래서 데이터를 새로 받아오면 그 데이터로 페이지가 렌더링 된다.

```js
//page

function Page({ data }) {
...
}

export async function getServerSideProps() {

  const res = await axios.get(`https://localholst:3065/user`)
  const data = res.data

  return { props: { data } }
}
```

page를 사용자가 요청하면 `getServerSideProps`를 먼저 실행 후 프론트가 서버에 직접요청 후 데이터를 받아와서 page컴포넌트에 date를 props로 전달하여 렌더링 할 수 있다.
`getServerSideProps`는 계속 데이터가 바뀌어야하는 페이지의 경우 사용한다.
