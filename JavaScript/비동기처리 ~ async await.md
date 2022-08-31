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

함수로 부터 결과값을 리턴 받기를 포기하고, 결과값을 이용해서 처리할 로직을 콜백 함수에 담아 인자로 던지면 된다.

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

이와 같이 비동기 함수를 호출할 때는 결과값을 리턴 받으려고 하지말고, **결과값을 통해 처리할 로직을 콜백 함수로 넘기는 스타일**로 코딩을 해줘야 예상된 결과를 얻을 수 있다.

하지만 자바스크립트 프로젝트가 점점 더 복잡해지면서 최근에는 콜백 함수를 인자로 넘겨서 비동기 처리를 하는 스타일을 피하는 추세이다. 왜냐하면 콜백함수를 중첩해서 사용하게 되면 코드의 가독성이 현저하게 떨어지기 때문이다. 결국, 많은 개발자들이 **콜백지옥**이라고 불리는 끔찍한 상황을 겪게 되었고 최근에는 `Promise`나 `async/await`을 이용하는 방법으로 대체되고 있다.

```js
$.get("url", function (response) {
  parseValue(response, function (id) {
    auth(id, function (result) {
      display(result, function (text) {
        console.log(text);
      });
    });
  });
});
```

## Promise

프로미스는 자바스크립트 **비동기 처리에 사용되는 객체**입니다.

프로미스는 주로 서버에서 받아온 데이터를 화면에 표시할 때 사용한다.  
비동기 작업이 맞이할 미래의 완료 또는 실패와 그 결과 값을 나타낸다.

```js
$.get("url 주소/products/1", function (response) {
  // ...
});
```

위 API가 실행되면 서버에다가 '데이터 하나만 좀 주쇼'라는 요청을 보낸다. 그런데 여기서 데이터를 받아오기도 전에 마치 데이터를 다 받아온 마냥 화면에 데이터를 표시하려고 하면 오류가 발생하거나 빈 화면이 뜰 것이다. 이와 같은 문제점을 해결하기 위한 방법 중 하나가 프로미스 이다.

아래 코드는 간단한 ajax통신을 하는 코드이다.

```js
function getData(callbackFunc) {
  $.get("url 주소/products/1", function (response) {
    callbackFunc(response); // 서버에서 받은 데이터 response를 callbackFunc() 함수에 넘겨줌
  });
}

getData(function (tableData) {
  console.log(tableData); // $.get()의 response 값이 tableData에 전달됨
});
```

위 코드에 프로미스를 적용하면 아래와 같은 코드가 된다.

```js
function getData(callback) {
  // new Promise() 추가
  return new Promise(function (resolve, reject) {
    $.get("url 주소/products/1", function (response) {
      // 데이터를 받으면 resolve() 호출
      resolve(response);
    });
  });
}

// getData()의 실행이 끝나면 호출되는 then()
getData().then(function (tableData) {
  // resolve()의 결과 값이 여기로 전달됨
  console.log(tableData); // $.get()의 reponse 값이 tableData에 전달됨
});
```

콜백함수로 처리하던 구조에서 `new Promise()`, `resolve()`, `then()`과 같은 프로미스 API를 사용한 구조로 바뀌었다.

프로미스에는 3가지의 상태가 있다. 여기서 말하는 상태란 프로미스의 처리 과정을 의미한다. `new Promise()`로 프로미스를 생성하고 종료될 때까지 3가지 상태를 갖는다.

- Pending(대기): 비동기 처리 로직이 아직 완료되지 않은 상태
- Fulfilled(이행): 비동기 처리가 완료되어 프로미스 결과 값을 반환해준 상태
- Rejected(실패): 비동기 처리가 실패하거나 오류가 발생한 상태

**Pending**

아래와 같이 `new Promise()` 메서드를 호출하면 대기(Pending)상태가 된다.

```js
new Promise();
```

`new Promise()`메서드를 호출할 때 콜백 함수를 선언할 수 있고, 콜백 함수의 인자는 `resolve`, `reject`이다.

```js
new Promise(function (resolve, reject) {
  // ...
});
```

**Fulfilled**

여기서 콜백함수의 인자 `resolve`를 아래와 같이 실행하면 이행(Fulfilled)상태가 된다.

```js
new Promise(function (resolve, reject) {
  resolve();
});
```

그리고 이행상태가 되면 아래와 같이 `then()`을 이용하여 처리 결과 값을 받을 수 있다.

```js
function getData() {
  return new Promise(function (resolve, reject) {
    var data = 100;
    resolve(data);
  });
}

// resolve()의 결과 값 data를 resolvedData로 받음
getData().then(function (resolvedData) {
  console.log(resolvedData); // 100
});
```

**Rejected**

여기서 `reject`를 아래와 같이 호출하면 실패 상태가 된다.

```js
new Promise(function (resolve, reject) {
  reject();
});
```

그리고, 실패 상태가 되면 실패한 이유를 `catch()`로 받을 수 있다.

**예제**

```js
function getData() {
  return new Promise(function (resolve, reject) {
    $.get("url 주소/products/1", function (response) {
      if (response) {
        resolve(response);
      }
      reject(new Error("Request is failed"));
    });
  });
}

// 위 $.get() 호출 결과에 따라 'response' 또는 'Error' 출력
getData()
  .then(function (data) {
    console.log(data); // response 값 출력
  })
  .catch(function (err) {
    console.error(err); // Error 출력
  });
```

서버에서 제대로 응답을 받아오면 `resolve`메서드를 호출하고, 응답이 없으면 `reject()` 메서드를 호출하는 예제입니다. 호출된 메서드에 따라 `then()`이나 `catch()`로 분기하여 응답 결과 또는 오류를 출력한다.

프로미스의 또 다른 특징은 여러개의 프로미스를 연결하여 사용할 수 있다는 점이다.
앞 예제에서 `then()`메서드를 호출하고 나면 새로운 프로미스 객체가 반환된다. 따라서, 아래와 같이 사용할 수 있다.

```js
function getData() {
  return new Promise({
    // ...
  });
}

// then() 으로 여러 개의 프로미스를 연결한 형식
getData()
  .then(function (data) {
    // ...
  })
  .then(function () {
    // ...
  })
  .then(function () {
    // ...
  });
```

**프로미스의 에러 처리 방법**

1. `then()`의 두번제 인자로 에러 처리하는 방법

```js
getData().then(handleSuccess, handleError);
```

2. `catch()`를 이용하는 방법

위 2가지 방법 모두 프로미스의 `reject()`메서드가 호출되어 실패 상태가 된 경우에 실행된다.

```js
function getData() {
  return new Promise(function (resolve, reject) {
    reject("failed");
  });
}

// 1. then()의 두 번째 인자로 에러를 처리하는 코드
getData().then(
  function () {
    // ...
  },
  function (err) {
    console.log(err);
  }
);

// 2. catch()로 에러를 처리하는 코드
getData()
  .then()
  .catch(function (err) {
    console.log(err);
  });
```

앞에서 프로미스 에러 처리 방법 2가지를 살펴봤지만 가급적으로는 `catch()`로 처리하는게 더 효율적이다.

```js
// then()의 두 번째 인자로는 감지하지 못하는 오류
function getData() {
  return new Promise(function (resolve, reject) {
    resolve("hi");
  });
}

getData().then(
  function (result) {
    console.log(result);
    throw new Error("Error in then()"); // Uncaught (in promise) Error: Error in then()
  },
  function (err) {
    console.log("then error : ", err);
  }
);
```

getData() 함수의 프로미스에서 resolve() 메서드를 호출하여 정상적으로 로직을 처리했지만, then()의 첫 번째 콜백 함수 내부에서 오류가 나는 경우 오류를 제대로 잡아내지 못한다.

하지만 똑같은 오류를 `catch()`로 처리하면 다른 결과가 나온다.

```js
// catch()로 오류를 감지하는 코드
function getData() {
  return new Promise(function (resolve, reject) {
    resolve("hi");
  });
}

getData()
  .then(function (result) {
    console.log(result); // hi
    throw new Error("Error in then()");
  })
  .catch(function (err) {
    console.log("then error : ", err); // then error :  Error: Error in then()
  });
```

## async & await

async 와 await은 자바스크립트의 비동기 처리 패턴 중 가장 최근에 나온 문법이다. 기존의 비동기 처리 방식인 콜백함수와 프로미스의 단점을 보완하고 개발자가 읽기 좋은 코드를 작성할 수 있게 도와준다.

개발자에게 읽기 좋은 코드란 위에서 아래로 한 줄 한 줄 차근히 읽으면서 사고할 수 있는 코드 일 것이다. 이런 코드를 짜기 위해 async, await 문법이 생겨난 것이다.

**async & await 적용된 코드와 그렇지 않은 코드**

```js
function logName() {
  var user = fetchUser("domain.com/users/1");
  if (user.id === 1) {
    console.log(user.name);
  }
}
```

`fetchUser`가 서버에서 데이터를 받아오는 HTTP 통신 코드라고 가정했을 때 일반적으로 자바스크립트의 비동기 처리 코드는 아래와 같이 콜백을 사용해야지 코드의 실행순서를 보장받을 수 있다.

```js
function logName() {
  // 아래의 user 변수는 위의 코드와 비교하기 위해 일부러 남겨놓았습니다.
  var user = fetchUser("domain.com/users/1", function (user) {
    if (user.id === 1) {
      console.log(user.name);
    }
  });
}
```

처음 콜백을 접하면 콜백과 같은 처리 방식이 익숙하지 않을 수 있다. 그래서 아래와 같이 간단하게 생각하자.

```js
// 비동기 처리를 콜백으로 안해도 된다면..
function logName() {
  var user = fetchUser("domain.com/users/1");
  if (user.id === 1) {
    console.log(user.name);
  }
}
```

서버에서 사용자 데이터를 불러와서 변수에 담고, 사용자 아이디가 1이면 사용자 이름을 출력한다.

이러한 방식에서 async await만 붙이면 된다.

```js
// async & await 적용 후
async function logName() {
  var user = await fetchUser("domain.com/users/1");
  if (user.id === 1) {
    console.log(user.name);
  }
}
```

**기본 문법**

```js
async function 함수명() {
  await 비동기_처리_메서드_명();
}
```

먼저 함수 앞에 `async`라는 예약어를 붙이고 비동기 처리 코드 앞에 await을 붙이면 된다. 여기서 주의해야할 점은 비동기 처리 코드가 꼭 프로미스 객체를 반환해야 await이 의도한 대로 동작한다.

일반적으로 `await`의 대상이 되는 비동기 처리 코드는 Axios 등 프로미스를 반환하는 API 호출 함수이다.

`await`을 사용하지 않았다면 데이터를 받아온 시점에 콘솔을 출력할 수 있게 콜백함수나 `then()`등을 사용해야 했을 것이다. 하지만 async await 문법 덕에 비동기에 대한 사고를 하지 않아도 된다.

**async & await 예외처리**

async & await에서 예외처리 하는 방법은 바로 `try catch`이다. 프로미스에서 에러 처리를 위해 `catch()`를 사용했던 것 처럼 async에서는 `catch{}`를 사용하면 된다.

```js
async function logTodoTitle() {
  try {
    var user = await fetchUser();
    if (user.id === 1) {
      var todo = await fetchTodo();
      console.log(todo.title); // delectus aut autem
    }
  } catch (error) {
    console.log(error);
  }
}
```
