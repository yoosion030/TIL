# ๐EVENT๐

React ์์๋ HTML๊ณผ ๊ฐ์ ์ด๋ฒคํธ๋ฅผ ์ฌ์ฉํฉ๋๋ค.  
> ex ) onclick, onchange, mouseover ๋ฑ  

---

## ๐HTML๊ณผ ์ฐจ์ด์ 

1. React์ ์ด๋ฒคํธ๋ ์๋ฌธ์ ๋์  ์บ๋ฉ ์ผ์ด์ค( camelCase )๋ฅผ ์ฌ์ฉํด์ผํฉ๋๋ค. 
   - onclick = {} (x)
   - onClick = {} (o)

2.๋ฌธ์์ด์ด ์๋ ํจ์๋ก ์ ๋ฌํฉ๋๋ค.
   - onclick = "ํจ์์ด๋ฆ()" (x)
   - onClick = {ํจ์์ด๋ฆ} (o)


HTML
``` HTML
<button onclick="activateLasers()">
  Activate Lasers
</button>
```
React
```JSX
<button onClick={activateLasers}>
  Activate Lasers
</button>
```

---

## ๐์ฃผ์ํ  ์ 
**DOM ์์์๋ง ์ด๋ฒคํธ ์ค์ ์ด ๊ฐ๋ฅํฉ๋๋ค.** `div`, `span`, `form`, `button` ๋ฑ์ DOM ์์์๋ ์ด๋ฒคํธ ์ค์ ์ด ๊ฐ๋ฅํ์ง๋ง, ๋ฆฌ์กํธ์ ์ปดํฌ๋ํธ์๋ ๋ถ๊ฐ๋ฅํฉ๋๋ค.   



์๋ชป๋ ์ฝ๋
``` JSX
function App() {
  const sayHi = function () {
    alert('hello');
  }
  return (
    <>
      <Component onClick={sayHi}/>
    </>
  );
}
```

---

## ๐preventDefault
React์์๋ `false`๋ฅผ ๋ฐํํด๋ ๊ธฐ๋ณธ ๋์์ ๋ฐฉ์งํ  ์ ์์ต๋๋ค.   
๋ฐ๋์ `preventDefault`๋ฅผ ๋ช์์ ์ผ๋ก ํธ์ถํด์ผ ํฉ๋๋ค. 
HTML
```HTML
<form onsubmit="console.log('You clicked submit.'); return false">
  <button type="submit">Submit</button>
</form>
```

React
``` JSX
function Form() {
  function handleSubmit(e) {
    e.preventDefault();
    console.log('You clicked submit.');
  }

  return (
    <form onSubmit={handleSubmit}>
      <button type="submit">Submit</button>
    </form>
  );
}
```
event๋ฅผ ์ธ์๋ก ๋ฐ๊ณ , e.preventDefault()๋ฅผ ํธ์ถํ๋ฉด, ์ด๋ฒคํธ์ ๊ธฐ๋ณธ๋์์ ๋์ํ์ง ์๊ฒ ๋๊ณ  console.log๋ง ์ํ๋ฉ๋๋ค.

---

## ๐์ด๋ฒคํธ ํธ๋ค๋ง - ํด๋์คํ ์ปดํฌ๋ํธ
React์์๋ DOM์๋ฆฌ๋จผํธ๊ฐ ์์ฑ๋ ํ ๋ฆฌ์ค๋๋ฅผ ์ถ๊ฐํ๊ธฐ ์ํด `addEventListener`๋ฅผ ํธ์ถํ  ํ์๊ฐ ์๋ค. ๋์ , ์๋ฆฌ๋จผํธ๊ฐ ์ฒ์ ๋ ๋๋ง๋ ๋ ๋ฆฌ์ค๋๋ฅผ ์ ๊ณตํ๋ฉด ๋๋ค.  
์๋์ ์์๋ฅผ ๋ณด๋ฉด, ์ด๋ฒคํธํธ๋ค๋ฌ๋ฅผ ํด๋์ค์ ๋ฉ์๋๋ก ๋ง๋ค์๊ณ  ์ด๋ฅผ ์ปดํฌ๋ํธ ๋ด์์ ์ฌ์ฉํ  ์ ์๋ค.

- JS์ ํด๋์ค ๋ฉ์๋๋ ๊ธฐ๋ณธ์ ์ผ๋ก ๋ฐ์ธ๋ฉ๋์ด์์ง ์๊ธฐ ๋๋ฌธ์ `this.handleClick`์ ๋ฐ์ธ๋ฉํ์ง ์๊ณ  ํธ์ถํ๋ฉด `this`๋ `undefined`๊ฐ ๋๋ค. ๋ฐ๋ผ์ ๋ฐ์ธ๋ฉํด์ฃผ๊ณ  ์ฌ์ฉํด์ผํ๋ค.
- `binding`์ ๋ฐ๋ก ์ง์ ํด์ฃผ์ง ์์ผ๋ฉด ํด๋น ๋ฉ์๋์์ ํธ์ถํ๋ `this`๊ฐ ํด๋น ํด๋์ค์์์์ `event`๊ฐ์ด ์๋ ์ต์์์ `window`์์ ๊ฐ์ ๊ฐ์ ธ์ฌ ์ ์๊ธฐ ๋๋ฌธ์ ์ฃผ์ํด์ผํ๋ค.

```JSX
class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = {isToggleOn: true};
    //์ฝ๋ฐฑ์์ `this`๊ฐ ์๋ํ๋ ค๋ฉด ๋ฐ์ธ๋ฉ์ ํด์ค์ผํ๋ค
    this.handleClick = this.handleClick.bind(this); 
  }

  handleClick() {
    this.setState(state => ({
      isToggleOn: !state.isToggleOn
    }));
  }

  render() {
    return (
      //render() ํจ์ ์์์ this ๊ฐ์ render() ํจ์๊ฐ ์ํ ์ปดํฌ๋ํธ๋ฅผ ๊ฐ๋ฆฌํด
      <button onClick={this.handleClick}>
        {this.state.isToggleOn ? 'ON' : 'OFF'}
      </button>
    );
  }
}
```

---

## ๐์ด๋ฒคํธ ํธ๋ค๋ง - ํจ์ํ ์ปดํฌ๋ํธ

ํจ์ํ ์ปดํฌ๋ํธ์ ์ํ๊ฐ์ `useState`ํ์ผ๋ก ๊ด๋ฆฌ๋๊ธฐ ๋๋ฌธ์ ์ปดํฌ๋ํธ์ `this`๋ก๋ถํฐ ์์ ๋กญ์ต๋๋ค.   
๋ํ ํจ์ํ ์ปดํฌ๋ํธ ์์ฒด์ ํจ์ํ ์ปดํฌ๋ํธ ์์์ ์ ์ธํ ํจ์๋ค ๋ชจ๋ ์ ์ญ ๊ฐ์ฒด๋ฅผ `this`๋ก ๊ฐ์ง๊ธฐ ๋๋ฌธ์ ์ ์ด์ `this`๊ฐ ๋ค ๊ฐ์ต๋๋ค. ๊ทธ๋์ ์ด๋ฒคํธ ํธ๋ค๋ฌ์ ์ฝ๋ฐฑ ํจ์๋ฅผ ๋๊ธฐ๋ ์ํฉ์๋ ๋ฑํ ์ ๊ฒฝ ์ธ ํ์๊ฐ ์์ต๋๋ค.

- const + ํจ์ ํํ
- ์์์ ์ ์ฉํ๊ธฐ ์ํด this๊ฐ ๋ฐ๋ก ํ์์์

```JSX
import React, {useState} from "react";

function NumberTest() {
  const [num, setNumber] = useState(0);

  const increase = () => {
    setNumber(num+1);
  } // const + ํจ์ ํํ

  return (
    <div>
      <h1>Number Test</h1>
      <h2>{num}</h2>
      <button onClick={increase}>์ฆ๊ฐ</button>
    </div>
  );
}

export default NumberTest;
```