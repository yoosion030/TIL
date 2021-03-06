# ๐Styled Component

## ๐์ ์
`styled-component`๋ Javascriptํ์ผ ๋ด์์ CSS๋ฅผ ์ฌ์ฉํ  ์ ์๊ฒ ํด์ฃผ๋ ๋ํ์ ์ธ **CSS-in-JS** ๋ผ์ด๋ธ๋ฌ๋ฆฌ๋ก React ํ๋ ์์ํฌ๋ฅผ ์ฃผ์ ๋์์ผ๋ก ํ ๋ผ์ด๋ธ๋ฌ๋ฆฌ์ด๋ค.

## ๐์ฌ์ฉ

**1. styled-components ์ค์น (ํฐ๋ฏธ๋์ ์๋ ฅ)**
> `npm install styled-components`  

**2. import ์ถ๊ฐ ํ๊ธฐ(์ ์ฉํ๊ณ ์ ํ๋ componentsํ์ผ ์๋จ์)**
> `import styled from 'styled-components';`

**3. ์ ์ฉ**
> `const ์์์ ์ง์ ํด์ค component๋ช = styled.ํ๊ทธ๋ช ``;`

**4. ์คํ์ผ ์ปดํฌ๋ํธ ์ด๋ฆ์ โญ๋๋ฌธ์โญ๋ก !!**


๊ธฐ์กด CSS ์คํ์ผ๋ง ๋ฐฉ์
``` JSX
  const divStyle = {
    backgroundColor: "black",
    width: "100px",
    height: "100px",
  };

  return <div style={divStyle}></div>
```

--- 

styled-components๋ฅผ ์ฌ์ฉํ ๋ฐฉ์
``` JSX
  const StyledDiv = styled.div`
    background-color: black;
    width: 100px;
    height: 100px;
  `;

  return <StyledDiv></StyledDiv>
```

## ๐์ฅ์ 
### **1. component ๋จ์ ์คํ์ผ๋ง**
styled component๋ ์ค๋ณต๋์ง ์๋ ํน์  class๋ช์ ์์ฑํด ์คํ์ผ์ ์ ์ฉํ๊ธฐ ๋๋ฌธ์, className์ด ์ค๋ณต๋๊ฑฐ๋ selector์ ์ฐ์  ์ ์ฉ ์์ ๋๋ฌธ์ css ์คํ์ผ๋ง์ด ํผ์ ์ ์ผ์ผํค๋ ์ฌ๊ณ ๋ฅผ ๋ฐฉ์งํ  ์ ์์ต๋๋ค.

### **2. ์กฐ๊ฑด๋ถ ์คํ์ผ๋ง**

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
styled-components๋ Component์ props๋ฅผ ์ ๋ฌ๋ฐ์ ์ฌ์ฉํ๋ ๊ฒ์ด ๊ฐ๋ฅํฉ๋๋ค.

### **3. ํ์ฅ ์คํ์ผ๋ง**

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

๊ธฐ์กด์ Component์ ์คํ์ผ์ ์ถ๊ฐํ  ์ ์์ต๋๋ค. ํ์ฅ ์คํ์ผ๋ง์ ์ฌ์ฉํ๋ฉด ์ค๋ณต๋ ์ฝ๋ ์์ ์ค์ด๊ณ , ๋ถ์ฐ๋ ์คํ์ผ์ ์ผ๊ด์ ์ผ๋ก ๊ด๋ฆฌํ  ์ ์์ต๋๋ค.

### **4. ์ค์ฒฉ ์ค์ฝํ**

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

SASS์ ์ค์ฒฉ ์ค์ฝํ ๊ท์น์ ์ฌ์ฉํ  ์ ์์ต๋๋ค. ํ์ ์ปดํฌ๋ํธ์๊ฒ๋ง ์ ์ฉํ๊ณ  ์ถ์ ์คํ์ผ์ ์ค์ฝํ ํํ๋ก ๊ตฌํํ  ์ ์์ต๋๋ค.

### **5. ์์**
๊ธฐ์กด์ ๋ง๋ค์๋ ์ปดํฌ๋ํธ๋ฅผ ์์๋ฐ์ ์ฌ์ฉํ  ์ ์์ต๋๋ค.

```JSX
import styled from 'styled-components'; const Button = styled.button`
 padding: 6px 12px;
`;
const RedButton = styled(Button)`
  background-color: #f53e3e;
`;
```
