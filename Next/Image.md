# NextJS Image Component

NextJS에서 `<img/>` 태그를 사용하면 img HTML 태그를 사용하지 말라는 경고가 뜬다. 무슨 이유때문인지 한번 알아보자.

## NextJS의 \<Image/>

**lazy loading**

lazy loading이란 페이지를 읽어들이는 시점에 중요하지 않은 리소스 로딩을 추 후에 하는 기술 이다. 이미지들이 흐리게 보이다가 로드되는 것이다. 사용자가 이미지가 나올 때까지 스크롤 하지 않으면 이미지를 로드하지 않는다. 웹 사이트의 성능을 향상기킬 수 있는 아주 좋은 기능이다.

**\<img/> 태그와의 차이점**

- img태그는 사용자가 웹 사이트에 도달했을 때 모든 이미지를 로드 해야함. \<Image>컴포넌트는 사용자가 보고있는 이미지만 로드함

**NextJS가 알아서 해주는 것**

- span, img, srcset등 많은 styles
- image URL 생성
  => NextJS가 이미지를 압축하기 때문

## Local Image

> 파일 시스템에 있는 이미지, API 응답에 의존하지 않는 이미지

**Local Image 속성**

ex ) `http://localhost:3001/_next/image?url=https%3A%2F%2Fgithub.com%2Fyoosion030.png&w=256&q=75`

- Quality
  url의 `q={0~100}`부분이 이미지의 품질을 알려주는 부분이다. 100으로 하면 품질이 올라가고 0으로 하면 품질이 떨어진다.
- placeholder
  - empty (기본값, 이미지가 로드되는 동안 어떤 placeholder도 없을 것이며 빈 공간만 보일 것임)
  - blur
- width
- height

## Remote Image

> API 응답하기를 기다리는 이미지 => 이미지의 source, URL이 무엇인지 알아야함, NextJS 파일에 없기 때문에 local image만큼 최적화가 되지 않음

**Remote Image 속성**

ex ) `http://localhost:3001/_next/image?url=https%3A%2F%2Fgithub.com%2Fyoosion030.png&w=256&q=75`

- Quality
  url의 `q={0~100}`부분이 이미지의 품질을 알려주는 부분이다. 100으로 하면 품질이 올라가고 0으로 하면 품질이 떨어진다.

ex ) ` src={'https://github.com/yoosion030.png'}`

- Domain
  url의 도메인네임을 지정해줘야 한다. 지정해주지 않는다면 `Unhandled Runtime Error`가 난다.

```js
// next.config.js

/** @type {import('next').NextConfig} */
const nextConfig = {
  reactStrictMode: true,
  images: {
    domains: ["github.com"],
  },
};

module.exports = nextConfig;
```

- width, height 속성이 필수 => lazy loading을 위해 (이미지가 보여지길 원하는 크기를 명시)
