# ๐ซ์กฐ๊ฑด๋ถ ๋ ๋๋ง๐ซ
> ํน์  ์กฐ๊ฑด์ ๋ฐ๋ผ ๋ค๋ฅธ ๊ฒฐ๊ณผ๋ฌผ์ ๋ ๋๋ง ํ๋ ๊ฒ์ ์๋ฏธํฉ๋๋ค

๋ฆฌ์กํธ๋ก ์ปดํฌ๋ํธ๋ฅผ ๋ง๋ค๋ค๋ณด๋ฉด props๋ state์ ๋ฐ๋ผ ๋ฌ๋ผ์ง๋ ์ปดํฌ๋ํธ๋ฅผ ๋ฐํํ๊ณ  ์ถ์ ๋๊ฐ ์์ต๋๋ค.  
์กฐ๊ฑด๋ถ๋ ๋๋ง์ ๊น๋ํ๊ฒ ์์ฑํ๋ฉด, ์ฝ๋์ ๊ฐ๋์ฑ์ด ๋์์ง๋๋ค.

---

## โif-else ์กฐ๊ฑด๋ฌธ

์ฌ์ฉ์์ ๋ก๊ทธ์ธ ์ฌ๋ถ์ ๋ฐ๋ผ `<UserGreeting/>`๋๋ `<GuestGreeting/>` ์ปดํฌ๋ํธ๋ฅผ ํ์ํ๋ ์์์๋๋ค.
``` JSX
function Greeting(props) {
  const isLoggedIn = props.isLoggedIn;
  if (isLoggedIn) { //isLoggedIn==true์ด๋ฉด
    return <UserGreeting />;
  }
  return <GuestGreeting />;
}

ReactDOM.render(
  // Try changing to isLoggedIn={true}:
  <Greeting isLoggedIn={false} />,
  document.getElementById('root')
);
```
- ์ปดํฌ๋ํธ๊ฐ ์กฐ๊ฑด์ ๋ฐ๋ผ ๋ ๋๋งํ  ๋ด์ฉ ์ ์ฒด๊ฐ ๊ฒฐ์ ๋จ
- ์ปดํฌ๋ํธ์ ์ผ๋ถ๋ถ๋ง ์ ํ์ ์ผ๋ก ๋ ๋๋งํ๊ธฐ์๋ ์ ํฉํ์ง ์์


if-else ํจํด์ ์ฌ์ฉํ๋ฉด์ ์ผ๋ถ๋ถ๋ง ๋ ๋๋งํ๋ ค๋ฉด ์ฆ์ ์คํ ํจ์ (IIFE) ๋ฅผ ์ฌ์ฉํด์ผ ๊ฐ๋ฅํฉ๋๋ค.
```JSX
function Greeting(props) {
    const isLoggedIn = props.isLoggedIn;

    return (
        <React.Fragment>
        {
            // ์ฆ์ ์คํ ํจ์ IIFE
            (() => {
                    if (isLoggedIn) {
                        return <UserGreeting />;
                    }
                    else {
                        return <GeustGreeting />;
                    }
                }
            )();
        }
        </React.Fragment>
    );
}
```
- ๊ฐ๋์ฑ ๋ณ๋ก
- ์ฐ๊ธฐ ์ด๋ ค์ ๋ณด์
- ํ์ฉํ๊ธฐ ์ด๋ ค์

---

## โ๋ผ๋ฆฌ์ฐ์ฐ์ &&

์๋ ๋ผ๋ฆฌ์ฐ์ฐ์ &&๋ "๋ ํผ์ฐ์ฐ์๊ฐ true์ด๋ฉด ๊ฒฐ๋ก ์ ์ผ๋ก true๋ฅผ ๋ฐํํ๋ค" ๋ผ๊ณ  ์๊ณ ์์์ง๋ง ์๋ฐ์คํฌ๋ฆฝํธ์์๋ true && expression์ ํญ์ expression์ผ๋ก ํ๊ฐ๋๊ณ  false && expression์ ํญ์ false๋ก ํ๊ฐ๋๊ธฐ ๋๋ฌธ์ ์กฐ๊ฑด๋ถ ๋ ๋๋งํ ๋ ์ ์ฉํ๊ฒ ์ฌ์ฉํ  ์ ์์ต๋๋ค.  

```JSX
function Mailbox(props) {
  const unreadMessages = props.unreadMessages;
  return (
    <div>
      <h1>Hello!</h1>
      {unreadMessages.length > 0 &&
        <h2>
          You have {unreadMessages.length} unread messages.
        </h2>
      } // ์กฐ๊ฑด๋ถ ๋ ๋๋ง
    </div>
  );
}

const messages = ['React', 'Re: React', 'Re:Re: React'];
ReactDOM.render(
  <Mailbox unreadMessages={messages} />,
  document.getElementById('root')
);
```

์์ ์ฝ๋๋ `unreadMessages.length > 0` ์ผ๋ `<h2>`ํ๊ทธ์ ๋ด์ฉ์ ๋ํ๋๋๋ค.

---

## โญ์กฐ๊ฑด๋ถ ์ฐ์ฐ์ ( ์ผํญ ์ฐ์ฐ์ )โญ
์๋ฐ์คํฌ๋ฆฝํธ์ ์กฐ๊ฑด๋ถ ์ฐ์ฐ์์ธ `์กฐ๊ฑด ? ์ฐธ : ๊ฑฐ์ง` ์ ์ฌ์ฉํ์ฌ ์กฐ๊ฑด๋ถ ๋ ๋๋ง์ ๊ตฌํํ  ์ ์๋ค.

```JSX
render() {
  const isLoggedIn = this.state.isLoggedIn;
  return (
    <div>
      The user is
      <p>
      { isLoggedIn 
      ? 'currently' 
      : 'not'}
      </p>
       logged in.
    </div>
  );
}
```
์กฐ๊ฑด์ด ์ฐธ์ด๋ฉด currently, ๊ฑฐ์ง์ด๋ฉด not์ด ์ถ๋ ฅ์ด ๋ฉ๋๋ค.
- ์ฝ๋๊ฐ ๋ณด๊ธฐ ์ฌ์
- ํ์ฉํ๊ธฐ ์ข์