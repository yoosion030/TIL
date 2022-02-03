# 헷갈렸던 @media query 이해하기

## 미디어 쿼리 사용법

```css
.test {
  @media (max-width: 450px) {
    width: 350px;
  }
}
```

- 링크로 연결하기

```html
<link rel="stylesheet" media="(max-width:450px)" href="test.css" />
```

## 문법

- css 내부에 삽입하기

```css
@media not|only mediaType and (madia feature) {
    css-code;
}
```

- 링크로 연결하기

```html
<link
  rel="stylesheet"
  media="mediaType and|not|only (media feature)"
  href="test.css"
/>
```

## 연산자

- **and**  
  여러 미디어 특징들을 하나로 결합함
- **, (or 연산자)**  
  쉼표로 분리된 각 목록은 각각 개별 미디어 쿼리임
- **not**
  전체 미디어 쿼리를 부정하기위해 사용함
- **only**  
  미디어 쿼리를 지원하지 않는 브라우저가 주어진 스타일을 적용하는 것을 방지

**⭐ not이나 only 연산자를 사용하려면 미디어 타입을 규정해야한다 !!**

## media type ( 미디어 종류 )

- **all**
  미디어 타입의 기본값
- **print**
  프린터
- **screen**
  컴퓨터 스크린, 테블릿, 스마트폰 등
- **speech**
  페이지를 읽어주는 화면 낭독기

## 사용예시

- all ( 기본문법 )

  ```css
  .test {
    @media (max-width: 450px) {
      width: 350px;
    }
  }
  ```

  모든 유형의 장치에서 최대 너비가 450px 일 때 스타일을 적용한다. ( 0 ~ 450px )
  만약 `min-width` 였으면 최소 너비가 450px 일 때 스타일을 적용하겠다는 의미이다. ( 450px ~ 100vw )

- and

  ```css
  @media print and (min-width: 700px) and (orientation: portrait) {
    ...;
  }
  ```

  프린트 장치이며 최소 너비 700px 이상이며, 방향이 세로 모드일 때만 적용한다는 의미이다.

- or

```css
@media (min-width: 700px), print and (orientation: landscape) {
  ...;
}
```

모든 장치에서 최소너비 700px이상일 때 적용하거나, 프린트 장치에서는 가로 방향일 때만 적용하겠다는 의미이다.

- not

  not은 모든 미디어 타입을 수식한다. 미디어 구문은 개별 미디어 쿼리로 인식하므로 or 연산자 이후의 조건은 not에 영향을 미치지 않는다.

  ```css
  @media not screen and (color), print and (color) {
    ...;
  }
  ```

  모든 스크린 장치에서 색생을 적용하지 않거나, 프린트 장치에서는 색상을 적용하겠다는 의미이다.

- only
  미디어 쿼리를 인식하지 못하는 브라우저에서 미디어쿼리를 숨기기 위해 사용한다. only 키워드는 미디어 쿼리 결과에 아무런 영향을 미치지 않는다.
