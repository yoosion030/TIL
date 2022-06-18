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
    revalidate: 60 * 60, // 60초 * 60 = 1시간,
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

## On-demand Revalidation

ODR을 이용하면 수동으로 `getStaticProps`를 어디에서든지 작동시킬 수 있게된다.

### ODR 장점

예를들어 revalidate 시간을 60초로 잡았다고 가정해보자.
그럼 유저는 60초 동안은 전에 생성된 오래된 페이지를 보게된다. 최신 데이터를 보기 위해서는 유저가 60초 이후에 페이지에 방문하는 것밖에 없다. 만약에 1분안에 새로운 글 300개가 등록되었다면, 첫 1분 동안은 새로 등록된 300개 글이 보이지 않을 것이다.

**하지만 ODR이 있으면 `getStaticProps`를 API 핸들러로 작동시킬 수 있다.** 이게 있으면 말 그대로 모든걸 HTML로 제작할 수 있다는 것이다. 예를 들어 유저가 프로필을 편집하면 페이지를 다시 생성하도록 작동시키게 하는 것이다.

### ODR 사용

ODR을 사용하려면 NextJS를 12.1 버전 이상이어야 함
ㅈㄴ 쉬움
API 핸들러 안에 한줄만 추가하면 됨

```JS
    await res.unstable_revalidate('validate할 url')
```
// 아직은 베타 버전이라 `unstable_revalidate`라는 이름으로 사용될 수 있음
