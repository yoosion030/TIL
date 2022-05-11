# getStaticProps, getServerSideProps

**용어 알고가기**

1. 사전렌더링 (pre-rendering)

NextJS가 작동하는 방식과 이를 빠르게 만드는 데 있어 큰 부분을 차지한다.  
기본적으로 NextJS는 실행해야 하는 최소한의 Javascript와 함께 **Hypdration을 통해 각 페이지 HTML을 미리 생성하여 모든 페이지를 사전 렌더링한다.**

사전 렌더링에는 정적 생성(SG)과 서버 사이드 렌더링(SSR)이 있다.

이 둘의 차이점은 데이터를 가져올 때이다.

1-2. 정적 생성(SG)
SG의 경우 데이터는 빌드 시 가져와서 모든 요청에서 재사용된다. (캐시 될 수 있기 때문에 더 빠름)

**캐시** - 사용자가 웹 사이트에 접속할 때, 정적 컨텐츠를 특정 위치에 저장하여 매번 요청하여 받는 것이 아니라, 특정 위치에서 불러옴으로써 응답시간을 줄이고, 서버 트래픽 감소 효과를 볼 수 있다.

**캐싱** - 애플리케이션의 처리 속도를 높여줌. 이미 가져온 데이터나 계산된 결괏값의 복사본을 저장함으로써 처리 속도를 향상함.

1-3. 서버 사이드 렌더링(SSR)
SSR에서는 모든 요청에서 데이터를 가져온다.
즉, NextJS 앱의 일부는 정적 생성을 사용하고 다른 일부는 SSR을 사용할 수 있다.

## getStaticProps

`getStaticProps`는 페이지 콘텐츠가 외부 데이터에 의존할 때 **SG(정적 생성)**에서 사용되고, `async`를 사용하여 export하게 되면 NextJS에서는 **빌드할 때 해당 페이지를 Pre-render한다.**

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FDt4ZQ%2FbtqN01Q20Ej%2FMIzZYVPdpFamKa2YLJzwrK%2Fimg.png)

**특징**

- 외부 데이터를 가져와서 페이지의 기본 구성요소에 반환할 수 있는 비동기 함수이다. 데이터는 props로 반환되며 페이지에 있는 기본 내보내기 구성요소의 props에 암시적으로 매핑됨.
- **빌드 시 고정되는 값으로 빌드 이후네는 변경 불가**

**언제 사용해야 하는가?**

- 데이터가 공식적으로 캐싱될 수 있을 때
- SEO등의 이슈로 인해 빠르게 미리 렌더링 해야만 하는 페이지의 경우 HTML, json파일을 모두 생성해둔다. 쉽게말해 그냥 거의 외부에서 API를 통해 데이터를 가져와 렌더링 하는 모든 페이지는 써도 무방한 듯 하다.
- **client 사이드에서 절대로 실행되지 않는다.**
- **Static Data (정적인 데이터)를 위해 사용한다.**

## getServerSideProps

빌드와 상관없이, **매 요청마다 데이터를 서버로부터 가져온다.**
getStaticProps와 사용하는 방법은 동일하다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FGW2St%2FbtqNWDYcfoz%2FV57sAjC9ITPhmEtjN1g39k%2Fimg.png)

파라미터로 **context**를 받아오고 있는데, context 매개 변수는 몇 가지의 키를 포함하는 객체이다.

- **params**: 페이지가 동적 경로를 사용하는 경우 경로 매개 변수를 포함한다. 예를 들어 `user/[id].tsx` 이면 다음 params는 { id: ... }와 같이 표시된다. (동적 라우팅)
- **req**: HTTP IncomingMessage 객체
- **res**: HTTP 응답 객체
- **query**: 쿼리 문자열

등등 몇가지의 키를 포함하고 있다.

**특징**

- 클라이언트 사이드에서 실행되지 않는 것과 page에서만 사용할 수 있다.
- **빌드와 상관없이 매 요청마다 데이터를 서버로부터 가져온다.**
- 매 요청 시마다 서버에서 계산해야 하므로 더 느릴 수 밖에 없다.

**언제 사용해야 하는가?**

- SSR을 위해 데이터 패칭할 때 사용한다.
- 페이지 렌더링 하기 전에 꼭 fetch해야하는 데이터가 있을 경우 사용한다.

## getStaticProps와 getServerSidePorps의 차이

별 차이가 없어 보이지만, **빌드 이후 데이터의 변경 가능 여부**이다.

`getStaticProps`는 변경이 안되고, `getServerSideProps`는 변경이 가능하다.
