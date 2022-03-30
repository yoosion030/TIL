# 제네릭

## 제네릭의 사전적 정의

제네릭은 C#, Java 등의 언어에서 재사용성이 높은 컴포넌트를 만들 때 자주 활용되는 특징이다. 특히, 한가지 타입보다 여러가지 타입에서 동작하는 컴포넌트를 생성하는데 사용된다.

## 제네릭의 한 줄 정의와 예시

**제네릭이란 타입을 마치 함수의 파라미터처럼 사용하는 것을 의미한다.**

```ts
function getText(text) {
  return text;
}
```

위 함수는 `text`라는 파라미터에 값을 넘겨 받아 `text`를 반환해준다. `hi`, `10`, `true` 등 어떤 값이 들어가더라도 그대로 반환한다.

```ts
getText("hi"); // 'hi'
getText(10); // 10
getText(true); // true
```

이 관점에서 제네릭을 한번 살펴보자.

```ts
function getText<T>(text: T): T {
  return text;
}
```

위 코드 중 getText<string>('hi')를 호출 했을 때 함수에서 제네릭이 어떻게 동작하는지 살펴보겠다.

```ts
getText<string>();
```

그리고 나서 함수의 인자로 hi 라는 값을 아래와 같이 넘기게 되면

```ts
getText<string>("hi");
```

`getText`함수는 아래와 같이 타입을 정의한 것과 같다.

```ts
function getText<string>(text: string): string {
  return text;
}
```

위 함수는 입력 값의 타입이 `string`이면서 반환 값 타입도 `string`이어야 한다.

## 제네릭을 사용하는 이유

```ts
function logText(text: string): string {
  return text;
}
```

위 코드는 인자를 하나 넘겨 받아 반환해주는 함수이다. 여기서 이 함수의 인자와 반환 값은 모두 `string`으로 지정되어 있지만 **만약 여러가지 타입을 허용하고 싶다면** 아래와 같이 `any`를 사용할 수 있다.

```ts
function logText(text: any): any {
  return text;
}
```

이렇게 타입을 바꾼다고 해서 함수의 동작에 문제가 생기진 않는다. 다만, **함수의 인자로 어떤 타입이 들어갔고 어떤 값이 반환되는지는 알 수가 없다.** 왜냐하면 `any`라는 타입은 타입 검사를 하지 않기 때문이다.

**이러한 문제점을 해결할 수 있는 것이 제네릭이다.**

```ts
function logText<T>(text: T): T {
  return text;
}
```

먼저 함수의 이름 봐로 뒤에 `<T>`라는 코드를 추가했다. 그리고 함수의 인자와 반환 값에 모두 `T`라는 타입을 추가한다. 이렇게 되면 함수를 호출할 때 넘긴 타입에 대해 타입스크립트가 추정할 수 있게된다. **따라서, 함수의 입력값에 대한 타입과 출력 값에 대한 타입이 동일한지 검증할 수 있게 된다.**

그리고 이렇게 선언한 함수는 아래와 같이 2가지 방법으로 호출할 수 있다.

```ts
// #1
const text = logText<string>("Hello Generic");
// #2
const text = logText("Hello Generic");
```

보통 두번째 방법이 코드도 더 짧고 가독성이 좋기 때문에 흔하게 사용한다. 그렇지만 만약 복잡한 코드에서 두번째 코드로 타입 추정이 되지 않는다면 첫번째 방법을 사용하면 된다.

## 제네릭 타입 변수

```ts
function logText<T>(text: T): T {
  return text;
}
```

만약 여기서 함수의 인자로 받은 값의 `length`를 확인하고 싶다면 어떻게 해야할까? 아마 아래와 같이 코드를 작성할 것이다.

```ts
function logText<T>(text: T): T {
  console.log(text.length); // Error: T doesn't have .length
  return text;
}
```

위 코드를 변환하려고 하면 컴파일러에서 에러를 발생시킨다. 왜냐하면 `text`에 `length`속성이 있다는 단서는 어디에도 없기 때문이다.

다시 위 제네릭 코드의 의미를 살펴보면 함수의 인자와 반환값에 대한 타입을 정하진 않았지만, 입력 값으로 어떤 타입이 들어왔고 반환 값으로 어떤 타입이 나가는지 알 수 있다. 따라서, 함수의 인자와 반환 값 타입에 마치 `any`를 지정한 것과 같은 동작을 한다는 것을 알 수 있다. 그래서 설령 인자에 `number`타입을 넘기더라도 에러가 나지 않는다.

이러한 특성때문에 현재 인자인 `text`에 문자열이나 배열이 들어와도 아직은 컴파일러 입장에서 `length`를 허용할 순 없다. 왜냐하면 `number`가 들어왔을 때는 `length` 코드가 유효하지 않기 때문이다.

그래서 이러한 경우에는 아래와 같이 제네릭에 타입을 줄 수 있다.

```ts
function logText<T>(text: T[]): T[] {
  console.log(text.length); // 제네릭 타입이 배열이기 때문에 `length`를 허용합니다.
  return text;
}
```

위 코드가 기존의 제네릭 코드와 다른 점은 인자의 `T[]`부분이다. 이 제네릭 함수 코드는 일단 `T`라는 변수 타입을 받고, 인자 값으로는 배열 형태의 `T`를 받는다. 예를 들면, 함수에 `[1, 2, 3]`처럼 숫자로 이뤄진 배열을 받으면 반환 값으로 `number`를 돌려주는 것이다. 이런 방식으로 제네릭을 사용하면 꽤 유연한 방식으로 타입을 정의해줄 수 있다.

혹은 다음과 같이 좀 더 명시적으로 제네릭 타입을 선언할 수 있다.

```ts
function logText<T>(text: Array<T>): Array<T> {
  console.log(text.length);
  return text;
}
```

## 제네릭 타입

아래 두 코드는 같은 의미이다.

```ts
function logText<T>(text: T): T {
  return text;
}
// #1
let str: <T>(text: T) => T = logText;
// #2
let str: { <T>(text: T): T } = logText;
```

위와 같은 변형 방식으로 제네릭 인터페이스 코드를 다음과 같이 작성할 수 있다.

```ts
interface GenericLogTextFn {
  <T>(text: T): T;
}
function logText<T>(text: T): T {
  return text;
}
let myString: GenericLogTextFn = logText; // Okay
```

위 코드에서 만약 인터페이스에 인자 타입을 강조하고 싶다면 아래와 같이 변경할 수 있다.

```ts
interface GenericLogTextFn<T> {
  (text: T): T;
}
function logText<T>(text: T): T {
  return text;
}
let myString: GenericLogTextFn<string> = logText;
```

이와 같은 방식으로 제네릭 인터페이스 뿐만 아니라 클래스도 생성할 수 있다. 다만. enum과 namespace는 제네릭으로 생성할 수 없다.

[제네릭 클래스, 제네릭 제약조건 더 알아보기](https://joshua1988.github.io/ts/guide/generics.html#%EC%A0%9C%EB%84%A4%EB%A6%AD-%ED%83%80%EC%9E%85)
