# emotion.js 소개 및 사용법

## emotion.js란?

> CSS-in-JS의 종류 중 하나로 JavaScript안에서 스타일을 작성할 수 있게 해준다.

## emotion.js 설치

```terminal
> npm install @emotion/css

> npm install @emotion/react

> $ npm install @emotion/styled @emotion/react
```

## emotion.js 장점

- 중복 className 해결
- props, 조건 등에 따라 스타일을 지정 가능
- styled components 보다 사이즈가 작고 ssr시 서버 작업이 필요 없다.
- css-in-js 형식으로 스타일을 사용할 수 있다.
- vendor-prefixing, nested selectors, and media queries 등이 적용되어 작성이 간편하다.

## emotion.js 사용

**import 하기**

```js
import { jsx, css } from "@emotion/react";
import styled from "@emtion/styled";
```

`styled`는 사실 상 `styled-components`와 똑같다.

**기본 구조**

```js
/** @jsxImportSource @emotion/react */
import { css, jsx } from "@emotion/react";

const divStyle = css`
  background-color: hotpink;
  font-size: 24px;
  border-radius: 4px;
  padding: 32px;
  text-align: center;
  &:hover {
    color: white;
  }
`;

export default function App() {
  return <div css={divStyle}>Hover to change color.</div>;
}
```

**라벨링**

`emtion.js`는 styled-components처럼 className을 임의로 생성해준다.

이는 `@emtion/bable-plugin`을 사용하면 커스텀마이징이 가능하다.

```terminal
> npm install --save-dev @emotion/babel-plugin

> yarn add --dev @emotion/babel-plugin
```

```js
const divStyle = css`
  background-color: hotpink;
  font-size: 24px;
  border-radius: 4px;
  padding: 32px;
  text-align: center;
  &:hover {
    color: white;
  }
  label: divStyle;
`;
```

```html
<div class="css-mfy11-divStyle">...</div>
```

`label: divStyle;` 이럼 className을 직접 수정할 수 있음 아주 개굴띠

**재사용**
스타일을 입힐 것을 component로 만들어서 어느 곳에서든 재사용이 가능하다.

```js

const P = props => (
  <p
    css={{
      margin: 0,
      fontSize: 12,
      lineHeight: '1.5',
      fontFamily: 'sans-serif',
      color: 'blue',
    }}
    {...props}
  />
)

const ArticleText = props => (
  <P
    css={{
      fontSize: 20,
      fontFamily: 'Georgia, serif',
      color: 'darkgray',
    }}
    {...props}
  />
)

export default function App() {
  return (
    <div>
      <P>Using P component</P>
      <ArticleText>Using ArticleText component</ArticleText>
    </div>
  )

```

같은 CSS 속성이 있다면, 제일 최근 것으로 덮어씌워진다. (ex. ArticleText의 fontSize, fontFamily, color로 대체)

만약 component로 사용하여, CSS 속성을 `inline`으로 쓴다면 따로 `css`를 써줄 필요도 없으며, 속성명을 `camelCase`로 작성해야 한다. (ex. fontSize, fontFamily, backgroundColor 등)

**Nested**

```js
import { jsx, css } from "@emotion/react";

const paragraph = css`
  color: turquoise;

  a {
    border-bottom: 1px solid red;
    cursor: pointer;
  }
`;
render(
  <p css={paragraph}>
    Some text.
    <a>A link with a bottom border.</a>
  </p>
);
```

**미디어 쿼리**
반응형은 일반적으로 사용하는 미디어 쿼리와 사용법이 동일하다.

```js
/** @jsxImportSource @emotion/react */
import { jsx, css } from "@emotion/react";

render(
  <p
    css={css`
      font-size: 30px;
      @media (min-width: 420px) {
        font-size: 50px;
      }
    `}
  >
    Some text!
  </p>
);
```

**Global Theme 및 Typescript 설정**

```js
import { Global, css } from "@emotion/react";

const style = css`
  * {
    margin: 0;
    padding: 0;
  }

  body {
    box-sizing: border-box;
  }
`;

const GlobalStyle = () => {
  return <Global styles={style} />;
};

export default GlobalStyle;
```

```js
export const size = {
  largest: "75em", // 1200px
  large: "56.25em", // 900px
  medium: "37.5em", // 600px
  small: "31.25em", // 500px
  smallest: "25em", // 400px
};

const theme = {
  mainColor: "#0000ff",
  mq: {
    laptop: `@media only screen and (min-width: ${size.largest})`,
    tablet: `@media only screen and (min-width: ${size.large})`,
    mobile: `@media only screen and (min-width: ${size.small})`,
  },
};

export default theme;
```

타입스크립트를 사용할 경우, theme에 대한 타입 지정이 필요하다. `theme.ts`에서 설정한 것과 동일한 구조의 타입을 넣어주며, 파일 이름은 `emotion.d.ts`여야 한다.

```js
import '@emotion/react'

declare module '@emotion/react' {
  export interface Theme {
    mainColor: string
    mq: {
      laptop: string
      tablet: string
      mobile: string
    }
  }
}
```

```js
import ReactDOM from "react-dom";
import { BrowserRouter } from "react-router-dom";

import { ThemeProvider } from "@emotion/react";
import theme from "@styles/theme"; // 위치한 경로 설정
import GlobalStyle from "@styles/global"; // 위치한 경로 설정

import App from "./App";

ReactDOM.render(
  <BrowserRouter>
    <ThemeProvider theme={theme}>
      <GlobalStyle />
      <App />
    </ThemeProvider>
  </BrowserRouter>,
  document.getElementById("root")
);
```
