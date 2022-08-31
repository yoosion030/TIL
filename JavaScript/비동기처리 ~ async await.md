# 비동기 처리부터 async await까지

## 비동기 처리 & 콜백 함수

비동기 함수란 쉽게 설명하자면 **호출부에서 실행결과를 기다리지 않아도 되는 함수**이다. 반대로 동기 함수는 호출부에서 실행결과가 리턴될 때 까지 기다려야 하는 함수이다.

브라우저에서 동기 함수만으로 실행될 경우, 한 함수 요청이 길어질 경우 나머지 요청도 기다려야 하기 때문에 사용자 경험에 부정적인 영향을 미칠 것이다. 또한, 비동기 함수를 사용하면 로직을 순차적으로 처리할 필요가 없기 때문에 동시 처리에서도 동기 함수 대비 유리한 것으로 알려져 있다.

**대표적인 비동기 함수, setTimeout()**

```js
function findUser(id) {
  let user;
  setTimeout(function () {
    console.log("waited 0.1 sec.");
    user = {
      id: id,
      name: "User" + id,
      email: id + "@test.com",
    };
  }, 100);
  return user;
}

const user = findUser(1);
console.log("user:", user);
```

예상 값으로 아래와 같이 wait이 먼저 찍히고 그 다음에 user 정보가 찍힐 줄 알았지만,

```console
wait ~~
user ~~
```

예상치 못한 결과로 실행됨을 알 수 있다.

```console
user: undefined
waited 0.1 sec.
```

`setTimeout`은 비동기 함수 이기 때문에 1초 기다렸다가 user 결과를 찍는게 아니라 `setTimeout`을 요청하면 바로 user 결과를 찍고 나서 그 후에 user 값을 할당 해준다.

이와 같이 코드 실행 순서가 뒤죽박죽이 될 수 있는 상황에선 **콜백 함수**를 이용해서 해결할 수 있다.

함수로 부터 결과값을 리턴 받기를 포기하고, 결과값을 이용해서 처리할 로직을 콜백 함수에 담아 인자로 던지면 됩니다.

```js
function findUserAndCallBack(id, cb) {
  setTimeout(function () {
    console.log("waited 0.1 sec.");
    const user = {
      id: id,
      name: "User" + id,
      email: id + "@test.com",
    };
    cb(user); // 함수 안에서 함수 실행
  }, 100);
}

// 두번째 인자로 함수 전달
findUserAndCallBack(1, function (user) {
  console.log("user:", user);
});
```

결과

```console
waited 0.1 sec.
user: {id: 1, name: "User1", email: "1@test.com"}
```

이와 같이 비동기 함수를 호출할 때는 결과값을 리턴 받으려고 하지말고, **결과값을 통해 처리할 로직을 콜백 함수로 넘기는 스타일**로 코딩을 해줘야 예상된 결과르 얻을 수 있습니다.

하지만 자바스크립트 프로젝트가 점점 더 복잡해지면서 최근에는 콜백 함수를 인자로 넘겨서 비동기 처리를 하는 스타일을 피하는 추세이다. 왜냐하면 콜백함수를 중첩해서 사용하게 되면 코드의 가독성이 현저하게 떨어지기 때문이다. 결국, 많은 개발자들이 **콜백지옥**이라고 불리는 끔찍한 상황을 겪게 되었고 최근에는 `Promise`나 `async/await`을 이용하는 방법으로 대체되고 있다.
