# 서버 컴포넌트

## 왜 중요할까?

우리가 기다릴 필요 없이 서버사이드에서 컴포넌트를 렌더링 할 수 있기 때문이다.

SSR 페이지에서 렌더링하는데 오래 걸리는 컴포넌트가 하나 있다면 유저가 페이지 전체를 보는데까지 걸리는 시간이 엄청 길어질 것이다. 왜냐면 모든 컴포넌트가 렌더링 될 때까지 기다려야 유저에게 페이지를 보여줄 수 있기 때문이다.

만약 리액트에서 **서버 컴포넌트를 사용하면 다른 컴포넌트의 로딩이 끝나기 전에 페이지를 렌더링할 수 있다.** 이제 모든 페이지가 렌더링 되는걸 생각할 필요가 없다.

## 사용방법

사용할 컴포넌트 파일 명에 `.server`를 추가하기만 하면 된다.

```
list.jsx
-> list.server.jsx
```

만약 컴포넌트가 클라이언트에서만 렌더링되도록 만들고 싶다면 `.client`를 추가해주면 된다. 아니면 범용적으로 사용하고 싶은 컴포넌트라면 `server`나 `client`없이 평범한 이름으로 지어주면 된다.