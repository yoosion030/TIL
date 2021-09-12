# 🚫조건부 렌더링🚫
> 특정 조건에 따라 다른 결과물을 렌더링 하는 것을 의미합니다

리액트로 컴포넌트를 만들다보면 props나 state에 따라 달라지는 컴포넌트를 반환하고 싶을 때가 있습니다.  
조건부렌더링을 깔끔하게 작성하면, 코드의 가독성이 높아집니다.

---

## ✔if-else 조건문

사용자의 로그인 여부에 따라 `<UserGreeting/>`또는 `<GuestGreeting/>` 컴포넌트를 표시하는 예시입니다.
``` JSX
function Greeting(props) {
  const isLoggedIn = props.isLoggedIn;
  if (isLoggedIn) { //isLoggedIn==true이면
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
- 컴포넌트가 조건에 따라 렌더링할 내용 전체가 결정됨
- 컴포넌트의 일부분만 선택적으로 렌더링하기에는 적합하지 않음


if-else 패턴을 사용하면서 일부분만 렌더링하려면 즉시 실행 함수 (IIFE) 를 사용해야 가능합니다.
```JSX
function Greeting(props) {
    const isLoggedIn = props.isLoggedIn;

    return (
        <React.Fragment>
        {
            // 즉시 실행 함수 IIFE
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
- 가독성 별로
- 쓰기 어려워 보임
- 활용하기 어려움

---

## ✔논리연산자 &&

원래 논리연산자 &&는 "두 피연산자가 true이면 결론적으로 true를 반환한다" 라고 알고있었지만 자바스크립트에서는 true && expression은 항상 expression으로 평가되고 false && expression은 항상 false로 평가되기 때문에 조건부 렌더링할때 유용하게 사용할 수 있습니다.  

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
      } // 조건부 렌더링
    </div>
  );
}

const messages = ['React', 'Re: React', 'Re:Re: React'];
ReactDOM.render(
  <Mailbox unreadMessages={messages} />,
  document.getElementById('root')
);
```

위의 코드는 `unreadMessages.length > 0` 일때 `<h2>`태그의 내용을 나타냅니다.

---

## ⭐조건부 연산자 ( 삼항 연산자 )⭐
자바스크립트의 조건부 연산자인 `조건 ? 참 : 거짓` 을 사용하여 조건부 렌더링을 구현할 수 있다.

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
조건이 참이면 currently, 거짓이면 not이 출력이 됩니다.
- 코드가 보기 쉬움
- 활용하기 좋음