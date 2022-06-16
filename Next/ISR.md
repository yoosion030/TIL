# ISR(Incremental Static Regeneration)이란 ?

ISR은 정적 페이지가 생성된 후, 재빌드하지 않아도 페이지를 갱신할 때 유용하다. 앞에서 봤던 `getStaticProps`에서 **revalidate**가 바로 ISR을 가능하게 해준다.

```js
export async function getStaticProps() {
  const covidStats = await axios.get("/covid/stats");

  if (!covidStats) {
    return {
      notFound: true,
    };
  }

  return {
    props: { ...covidStats },
    notFound: false,
    revalidate: 60 * 60,
  };
}
```

예를 들어 `/covid/stats` 요청 후 리턴 값으로 revalidate를 주었다고 가정한다. 이러한 코드는 다음과 같이 동작한다.

- 1시간 전에 들어온 요청은 캐시에서 리턴한다.
- 1시간이 지난 후, nextjs 페이지 재생성 요청하기 전까지는 캐싱된 데이터를 보여준다.
- next가 페이지 재생성을 요청하면, 캐싱된 데이터를 invalidate하고 새로 요청한 데이터를 리턴한다.
- 만약 새로 요청한 API가 실패하면 이전에 캐싱된 데이터를 리턴한다.

++ 기술적인 상새

- Bulid Time에만 실행되어 query parameter, HTTP header 등 요청때에만 유효한 값들은 받을 수 없다.
- Server-side 코드를 바로 작성할 수 있다.
- 페이지 뿐만 아니라 JSON도 정적으로 생성하여, `next/link` 등으로 getStaticProps를 사용하는 페이지로 라우팅 되어도 getStaticProps가 호출되는 것이 아니라 정적으로 생성된 JSON데이터를 사용한다.
- `next dev`로 실행한 개발환경에서는 매 요청마다 getStaticProps가 재호출된다.
  > 원래는 처음 빌드 시에만 요청함.
