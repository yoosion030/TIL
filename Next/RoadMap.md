# NextJS Roadmap

## 서론

이 글은 아래 블로그를 번역한 것입니다. 구글번역으로 번역하였기 때문에 영문 번역에 오류가 있을 수도 있습니다.

(2021년 NextJS를 마스터하기 위한 3분 로드맵)[https://well-balanced.medium.com/next-js-%EA%B7%B8%EA%B1%B0-%EC%96%B4%EB%96%BB%EA%B2%8C-%ED%95%98%EB%8A%94-%EA%B1%B4%EB%8D%B0-ea5637f25fa4]

NextJS를 배우고 싶은데 뭐부터 배워야할지 모른다면 !!!
NextJS를 새로 배우려고 한다면 !!!

꼭 이 로드맵을 확인하시길 바랍니다. CRA나 Gatsby는 NextJS에 비하면 아무것도 아닙니다. NextJS는 React 개발자들에게 새로운 유행입니다. 오늘 저는 NextJS를 마스터하기 위한 완벽한 로드맵과 가이드라인을 다룰 것입니다.

가보자고~

## 1. Architecture

개발 프로세스를 시작하기 위해 먼저 NextJS에서 따르는 기본 아키텍처를 배워야합니다.

( 이것은 중요하고 과소평가되어있습니다. 저는 NextJS 작업을 시작한 지 6개월이 지나가기 전까지는 배운적이 없었습니다. 하지만 나중에 더 많이 작업하면서 결국 배우게 될 것입니다. 그러나 더 나은 이해를 위해 코드로 뛰어들기 전에 아키텍처를 미리 배우는 것이 좋습니다. )

[Building solid Next JS architexture](https://medium.com/nerd-for-tech/building-solid-next-js-architecture-a8c6702dc67d)

## 2. Routing & Dynamic Routing

NextJS는 페이지 디렉토리 내부에 존재하는 파일 이름으로 처리되는 모든 단일 라우팅을 제공합니다. 이를 처음 접해보는 개발자에게는 매우 혼란스러울 수 있습니다. 그러나 일단 제대로 이해한다면 이 Express 기반 프레임워크가 얼마나 강력한지 이해하게 될 것입니다.

Dynamic routes는 기본 URL이 동일하지만 쿼리 키-값이 변경되는 경로입니다. 전자상거래 웹사이트나 블로그페이지 등에서 본 적이 있을 것입니다. 동적 라우팅은 페이지나 경로의 수가 불확실한 애플리케이션에 매우 강력하고 유용합니다.

[NextJS 공식문서](https://nextjs.org/docs/routing/introduction)
[Next.js 에서 라우팅 사용하기 블로그](https://merrily-code.tistory.com/52)

## 3. Next JS API

NextJS는 Image, routing, Head, Link 컴포넌트, 상수, 오류 등과 같은 내장 구성요소를 제공해줍니다.

가장 중요하고 널리 사용되는 3가지 구성요소를 설명하겠습니다.

- NextJS에서 제공해주는 Image컴포넌트는 lazy-loading으로 이미지를 로드하고 모든 브라우저에서 호환되는 이미지를 로드하는데 도움을 줍니다.
- Routing 컴포넌트는 응용 프로그램 내의 다른 페이지로 이동하는 데 도움을 줍니다. 이 컴포넌트는 쿼리를 통해 속성 전달을 처리할 수도 있습니다.
- HTML의 "a" 태그인 링크 컴포넌트는 사용자가 탐색하거나 리다이렉션을 할 전체페이지를 미리 로드하는 장점이 있습니다.

**Image**
[NextJS 공식문서](https://nextjs.org/docs/api-reference/next/image)
[최적화된 이미지 컴포넌트 블로그](https://mingeesuh.tistory.com/entry/NEXTjs-%EB%84%A5%EC%8A%A4%ED%8A%B8-JS%EB%A5%BC-%EB%B0%B0%EC%9B%8C%EB%B3%B4%EC%9E%90-3%ED%8E%B8-%EC%9D%B4%EB%AF%B8%EC%A7%80)

**Head**
[NextJS 공식문서](https://nextjs.org/docs/api-reference/next/head)

**Link**
[NextJS 공식문서](https://nextjs.org/docs/api-reference/next/link)
[NextJS 공식문서 번역 블로그](https://crong-dev.tistory.com/50)

## 4. Advanced Features

사용자 지정 앱 컴포넌트, 사용자 지정 문서 파일 등과 같은 고급 기능에 대해 알아봅시다. 고급 기능 중 일부는 다음과 같습니다.

- Custom App (Inside_app.js file)
- Custom Document (Inside \_document.js file)
- Absolute Import & Export module
- Customising PostCSS and Babel
- Measuring performance
- Adding Internalization
- Debugging

## 5. Data Fetching

NextJS는 페이지또는 컴포넌트가 렌더링되기 직전에 서버 측에서 데이터를 가져오는데 도움이되는 내장 함수를 제공합니다. 이는 UI가 해당 데이터에 의존하기 때문에 UI를 표시하기 전에 데이터를 가져오려는 경우 중요한 기능입니다.

- getInitialProps
- getServerSideProps
- useSWR

[NextJS 공식문서](https://nextjs.org/docs/api-reference/data-fetching/get-initial-props)
[next.js getInitialProps 사용법](https://kyounghwan01.github.io/blog/React/next/getInitialProps/#shallow-route%E1%84%8B%E1%85%AA-getinitialprops%E1%84%80%E1%85%AA-%E1%84%80%E1%85%AA%E1%86%AB%E1%84%80%E1%85%A8)

## 6. Serverless Components

NextJS는 프론트엔드 애플리케이션에 내장된 서버를 제공합니다. 이것은 데이터를 가져오거나 보내는 메서드를 작성할 수 있는 NodeJS 서버와 같습니다.

[Serverless Function in NextJS](https://javascript.plainenglish.io/serverless-function-in-next-js-3cd0d22ab983?gi=65f6c3871934)

## 7. Third-party support

Next JS는 UI 라이브러리, 파일 시스템 라이브러리, 실시간 애플리케이션용 소켓 라이브러리, Firebase와 같은 인증 라이브러리, SASS 또는 SCSS 또는 Typescript 작업과 같은 타사와 작업하기가 매우 쉽습니다.

[Google Authentication in less than 5 minutes](https://medium.com/nerd-for-tech/firebase-authentication-in-less-than-5-minutes-dce8ad5b8459)
