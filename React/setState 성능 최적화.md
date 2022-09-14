# setState 성능 최적화

useState 초깃값에 localStorage값을 넣어준다면 계속 localStorage에 접근하기 때문에 시간부하가 걸릴 수도 있다.

우리는 맨 처음에 접속했을 때만 localStorage에 접근하면 된다.

useState에 함수를 넘기는 것으로 시간부하 문제를 해결할 수 있다!

## setState 함수

useState 초깃값에 함수를 넣어줄 수 있다!

```js
const [counter, setCounter] = useState(() => {
  return localStorage.getItem("counter");
});
```

setState 인자로 함수를 넘겨줄 수 있다!

```js
setCounter((prev) => {
  return prev + 1;
});
```

setCounter에서 함수를 생성하면 첫번째 인자로 prev(이전 값)을 받는다.
