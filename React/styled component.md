# 💅Styled Component

## 💅정의
`styled-component`란 Javascript파일 내에서 CSS를 사용할 수 있게 해주는 대표적인 CSS-in-JS 라이브러리로 React 프레임워크를 주요 대상으로 한 라이브러리이다.

## 💅사용
`const 위에서 지정해준 component명 = styled.태그명 ``;`

기존 CSS 스타일링 방식
``` JSX
  const divStyle = {
    backgroundColor: "black",
    width: "100px",
    height: "100px",
  };

  return <div style={divStyle}></div>
```

--- 

styled-components를 사용한 방식
``` JSX
  const StyledDiv = styled.div`
    background-color: black;
    width: 100px;
    height: 100px;
  `;

  return <StyledDiv></StyledDiv>
```

## 💅장점
### 1. component 단위 스타일링
styled component는 중복되지 않는 특정 class명을 생성해 스타일을 적용하기 때문에, className이 중복되거나 selector의 우선 적용 순위 때문에 css 스타일링이 혼선을 일으키는 사고를 방지할 수 있습니다.

### 2. 조건부 스타일링

```JSX
const StyledDiv = styled.div`
    background-color: black;
    width: 100px;
    height: 100px;
    ${({ login }) => {
      return login ? `display: none` : null;
    }}
  `;

  return <StyledDiv login={true}></StyledDiv>;
  ```
styled-components는 Component의 props를 전달받아 사용하는 것이 가능합니다.

### 3. 확장 스타일링

```JSX
const Container = styled.div`
    max-width: 600px;
    width: 100%;
    height: 100px;
  `;

  const BlackContainer = styled(Container)`
    background-color: black;
  `;

  const RedContainer = styled(Container)`
    background-color: red;
  `;

  return (
    <>
      <BlackContainer />
      <RedContainer />
    </>
  );
  ```

기존의 Component에 스타일을 추가할 수 있습니다. 확장 스타일링을 사용하면 중복된 코드 양을 줄이고, 분산된 스타일을 일괄적으로 관리할 수 있습니다.

### 4. 중첩 스코프

```JSX
const StyledDiv = styled.div`
    background-color: black;
    width: 100px;
    height: 100px;
    p {
      color: white;
    }
  `;

  return (
    <>
      <StyledDiv>
        <p>Title</p>
      </StyledDiv>
      <p>content</p>
    </>
  );
  ```
SASS의 중첩 스코프 규칙을 사용할 수 있습니다. 하위 컴포넌트에게만 적용하고 싶은 스타일을 스코프 형태로 구현할 수 있습니다.