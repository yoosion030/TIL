# Tailwind CSS란?

> CSS 프레임워크로, HTML코드 내에서 인라인 스타일을 사용하는 방식으로 해당 요소에 스타일을 준다.

## 장점

- Utility-First의 편리함과 빠른 개발
  > 쉽고 빠른 디자인이 가능하다.
- 클래스명을 고민하지 않아도 됨
  > 랩핑 태그의 클래스명을 사용할 일이 거의 없다.
- 일관된 디자인
- 쉽고 자유로운 커스텀
  > 디자인 시스템이나 다크모드 구현도 간편하다.
- 로우 레벨의 스타일 제공
- Intelli Sense
  > 미리보기, 자동완성, 신택스 하이라이팅, 린팅을 지원하기 때문에 조금만 익숙해지면 금방 문서 없이 개발할 수 있다.
- 자바스크립트 코드와의 분리
  > 중간에 자바스크립트 프레임워크를 변경하여도 큰 추가 없이 기존의 HTML 코드를 그대로 쓸 수 있다.

## 단점

- 못생긴 코드
- 초반 클래스명 러닝 커브
  > 스타일을 주는 클래스명을 하나하나 기억해야 되다보니 초반 러닝커브가 심하게 온다.
- 자바스크립트 코트 사용 불가
  > 자바스크립트 변수값에 따라 가로 길이를 설정하는 등의 구현은 가능하기는 하지만 무척 번거로운 설정이 필요하다.
- HTML과 CSS코드 혼재
  > HTML과 CSS의 관심가 분리가 이루어지지 않다.

## Tailwind CSS 사용하기

1. PostCss, autoprefixer와 함께 설치하기

```
npm install tailwindcss@latest postcss@latest autoprefixer@latest
```

2. 설정파일 생성하기

```
npx tailwindcss init
```

3. Tailwind CSS 스차일 추가하기

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

4. 최적화 하기

**파일 크기를 최소화 하기 위해 `purge`옵션을 사용한다. 프로덕션으로 빌드할 때 여기에 설정된 파일에서 사용되지 않는 모든 클래스는 제거된다.**

```JS

// tailwind.config.js
module.exports = {
  purge: ['./src/**/*.{js,jsx,ts,tsx}'],
  ...
}
```
