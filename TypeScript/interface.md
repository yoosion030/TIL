# interface

## interface 정의

interface란?

> 쉽게 말하자면, **같은 모양의 타입들을 naming하는 역할**로 정리할 수 있다.

## interface 사용

ex )

```ts
interface User {
  age: string;
  name: string;
}
```

위 `User` interface는 `age`와 `name`의 속성을 가지고 있는 인터페이스이다. 하나의 타입을 딱 만들어서 사용하는 것이다.

타입을 만들었으니, 아래와 같이 사용할 수 있다.

```ts
let seho: User = {
  age: 33,
  name: "seho",
};
```

> seho 라는 변수를 만드는데, 그 seho 라는 변수의 타입은 User인 것이다.

## interface 활용

**1) 객체 선언에 활용**

```ts
let seho: User = {
  age: 33,
  name: "seho",
};

const getUser = (user: User) => {
  console.log(user);
};

getUser(seho); // { "age": 33, "name": "seho"}
```

`getUser`라는 함수를 만들고, 그 함수 인자로는 `User`타입의 객체를 넘겨준다.
해당 함수는 객체를 받아서 그대로 출력한다.
`seho`를 받은 함수는 그대로 `seho`를 출력한다.

**2) 함수의 스펙에 활용**

`interface`는 함수를 정의하는 모습에서도 활용이 가능하다.

```ts
interface SumFunction {
  (a: number, b: number): number;
}
```

`SumFunction`에 사용되는 인자와 반환타입에 대해서 인터페이스를 정의할 수 있고, 이를 아래와 같이 활용할 수 있다.

```ts
let sum: SumFunction;

sum = function (a, b) {
  return a + b;
};
```

[TypeScript interface란?](https://velog.io/@ghdtjrrl94/TypescriptDay03interface%EB%9E%80)
