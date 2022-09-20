# type과 interface의 차이점

## 차이점

1. 확장성

interface: extends 사용

```ts
interface PeopleInterface {
  name: string;
  age: number;
}

interface StudentInterface extends PeopleInterface {
  school: string;
}
```

type: &연산자 사용

```ts
type PeopleType = {
  name: string;
  age: number;
};

type StudentType = PeopleType & {
  school: string;
};
```

2. 선언적 확장

```ts
interface Window {
  title: string;
}

interface Window {
  ts: TypeScriptAPI;
}

// 같은 interface 명으로 Window를 다시 만든다면, 자동으로 확장이 된다.

const src = 'const a = "Hello World"';
window.ts.transpileModule(src, {});
```

```ts
type Window = {
  title: string;
};

type Window = {
  ts: TypeScriptAPI;
};

// Error: Duplicate identifier 'Window'.
// 타입은 안된다.
```

3. 사용 범위

interface: 객체에만 사용 가능

```ts
interface FooInterface {
  value: string;
}

type FooType = {
  value: string;
};

type FooOnlyString = string;
type FooTypeNumber = number;

// 불가능
interface X extends string {}
```

type: computed value 사용

```ts
type names = "firstName" | "lastName";

type NameTypes = {
  [key in names]: string;
};

const yc: NameTypes = { firstName: "hi", lastName: "yc" };

interface NameInterface {
  // error
  [key in names]: string;
}
```

## 결론

무엇이 되었건 간에, 프로젝트 전반에서 type을 쓸지 interface를 쓸지 **통일**은 필요해보인다. 그러나 객체, 그리고 타입간의 합성등을 고려해 보았을 때 **interface**를 쓰는 것이 더 나을지 않을까 싶다.
