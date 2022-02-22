# 타입스크립트 기본 타입

boolean, number, string, object, array, tuple, any, null, undefined 등등

## string, number

```ts
let str: string = 'hi'
let num: number = 100
let isUgly: boolean = false
```

## Array

```ts
let list1: number[] = [1, 2, 3]
let list2: Array<number> = [1, 2, 3]
```

## object

```ts
let obj: object = {}
let obj2: { name: string; age: number } = {
  name: 'sion',
  age: 17,
}
```

## Tuple

```ts
let x: [string, number]
x = ['hello', 10]
```

배열의 사이즈와 각 인덱스의 타입을 강제로 지정할 수 있다. 사이즈를 벗어난 인덱스를 참조하거나 각 인덱스의 타입과 다른 타입을 재할당 할 수 없다.

## Enum

JavaScript의 객체와 비슷하며,
숫자 값에 알기 쉬운 네이밍을 주는 방법이다.

```ts
enum Color {
  Red,
  Green,
  Blue,
}

let c: Color = Color.green
console.log(c) // output : 1
```

Red, Green, Blue는 순서대로 0,1,2의 값을 가지고 있다.

```ts
enum Color {
  Red = 1,
  Green,
  Blue,
}

let c: Color = Color.Green
console.log(c) // output: 2
```

시작 값을 1로 바꾸어주면 뒤의 값들도 같이 바뀐다.
또한, 아래와 같은 방식으로 각각 지정해 줄 수도 있다.

```ts
enum Color {
  Red = 1,
  Green = 2,
  Blue = 4,
}
```

반대로, 값으로부터 키 값을 구할 수도 있다.

```ts
enum Color {
  Red = 1,
  Green,
  Blue,
}

let colorName: string = Color[2]

console.log(colorName) // Green
```

## any

`any`타입은 모든 타입과 호환 가능하다. `any`타입의 변수에는 모든 값을 할당할 수 있다는 뜻이다.  
 하지만 `any`를 남용하면 타입 안정성에 구멍이 뚫린 코드가 되어 타입스크립트를 사용하는 의의가 사라지므로 **동적인 타입을 가지는 변수(타입을 하나로 고정하지 않을 변수)에만 Any라는 타입을 쓴다**.

```ts
let any: any = true
any = 'false'
any = 123
```

## function

function의 parameter와 return value도 타입을 명시해주어야 한다.

```ts
function add(a: number, b: number): number {
  return a + b
}
// a, b는 number type이여야 하고 return type도 number type이여야 함
```

## void

`void`는 `null`과 `undefined`만을 값으로 가질 수 있는 타입이다. 아무런 값도 반환하지 않는 함수의 반환 타입을 표시할 때 사용한다.

```ts
function nothing(): void {}
```

## null, undefined

```ts
let u: undefined = undefined

let n: null = null
```

기본적으로 null과 undefined는 모든 타입의 서브타입이기 때문에 다른 타입에도 null이나 undefined를 할당할 수 있다.

## never

`never`는 아무런 값도 가질 수 없는 타입이다. 값을 리턴하지 않을 때 사용한다.

```ts
function error(message: string): never {
  throw new Error(message)
}
```
