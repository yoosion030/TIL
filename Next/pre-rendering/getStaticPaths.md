# getStaticPaths

동적 url을 가지는 페이지들을 빌드 타임에 생성해주고 싶다면 해당 페이지 컴포넌트에서 `getStaticPaths` + `getStaticProps`함수를 export 해줘야 한다.

## getStaticPaths 반환객체

이 때, **어떤 path들에 대해서 정적 페이지 생성을 할지** 정하는 `getStaticPaths` 함수는 반환 객체로 `paths`와 `fallback`을 반드시 포함시켜야 한다.

```js
// getStaticPaths
// pages/users/[id].js
return {
  paths: [
    { params: { id: '1' } },
    { params: { id: '2' } }
  ],
  fallback: ...
}

```

> Next JS는 `users/1`, `users/2` 페이지를 빌드타임에 생성하게 된다.

## paths

> 어떤 path의 페이지들을 빌드 타임에 생성할지 정하는 배열이다.
> paths 배열에서 각각의 `params` 값은 페이지 이름에 있는 파라미터와 일치해야한다.

주의할 점

- 만약 파일명이 `pages/users/[userId].js` 였다면, `params` 객체도 userId 키값을 가지고 있어야한다.
- 파일명이 `pages/[...slug]`와 같이 catch-all 라우트를 이용중인 경우, `params` 객체는 `slug` 배열을 가지고 있어야한다.
- 파일명이 `pages/[[..slug]]`와 같이 optional catch-all 라우트를 이용중인 경우, null / [] / undefined / false 값을 넣어주면 루트 라우트를 렌더링하게 된다.

## fallback

> 빌드 타임에 생성해놓지 않은 path로 요청이 들어온 경우 어떻게 할지 정하는 `boolean` 또는 `'blocking'` 값이다.

```js
fallback: boolean | "blocking";
```

### fallback: false,

`getStaticPaths`가 반환하지 않은 모든 path에 대해서 404 페이지를 반환한다. (paths가 빈 배열이라면 전부 404 페이지를 return 해줌)

아래와 같은 경우에 사용할 수 있다.

- **적은 숫자**의 path만 프리 렌더링 해야하는 경우
- 새로운 페이지가 추가 될 일이 많지 않은 경우
  - 새로운 페이지가 자주 추가 된다면, 추가될 때마다 다시 빌드 해줘야 한다는 단점이 있다.

### fallback: "blocking",

1. NextJS가 최초 요청 시에 그 페이지에 대한 HTML을 만들어준다.
2. 그리고 그 이후엔 그 HTML파일을 모든 사람들에게 보여준다.
3. 그러면 그 이후의 사람들은 로딩과정을 겪지 않아도 된다.
4. 하지만, "blocking"으로 지정해주면 로딩화면은 안보인다.

### fallback: true,

"blocking"과 작동은 비슷하지만

4. **로딩 화면을 보여주는가 안보여주는가에 차이가 있다.**

"blocking"으로 지정해주면 로딩화면을 볼 수 없지만 `true`로 지정을 해준다면 사용자가 최초 요청시에 로딩화면을 볼 수 있게 해준다.

```js
if (router.isFallback) {
  return (
    <Layout title="Loading for you" seoTitle="Loading..">
      <span>I love you</span>
    </Layout>
  );
}
```

> fallback이 true 이면 아래 컴포넌트를 return 해라.
