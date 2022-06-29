# Dynamic Imports

`import {} from {}`구문은 나중에 유저가 다운로드 해야하는 자바스크립트 코드이다. 만약 때에 따라서 페이지 로딩이 끝나도 바로 사용하지 않는 컴포넌트가 있다면 어떨까? 필요에 따라서는 컴포넌트를 숨겨놨다가 유저가 무언가를 클릭할 때만 컴포넌트를 보여줄 수도 있다.

이러한 문제점을 고치려면 NextJS에서 제공해주는 `Dynamic Import`를 사용하면 된다.

`Dynamic Import`를 사용하면 유저가 실제로 그 컴포넌트를 필요로 할 때만 코드를 불러오게 만든다. => 컴포넌트를 `lazy loading`하게 만들 수 있다, 컴포넌트를 즉시 로딩하지 않게 할 수 있다.

## 사용

```js
// dynamic 불러오기
import dynamic from "next/dynamic";
```

```js
// component 불러오기
const Example = dynamic(() => import("@component/Example"));
... <Example></Exmaple>
```

**ssr**

```js
const Example = dynamic(() => import("@component/Example"), { ssr: false });
```

ssr 속성을 `false`로 지정해주면 서버단에서 로딩하지 않게 설정할 수도 있다.

## dynamic 컴포넌트가 다운로드 되는데 너무 오래 걸린다면?

ex ) 컴포넌트를 불러오는데 10초가 걸린다고 가정

해결법

- 애초에 불러오는데에 10초나 걸리는 너무 무거운 컴포넌트를 만들지 말자!
- loading 옵션 사용
  진짜 컴포넌트를 불러올 동안에 유조에게 보여줄 컴포넌트를 불러온다.

```ts
const Name = dynamic(() => import("@component/name"), {
  loading: () => <로딩할동안 불러올 컴포넌트 />,
});
```

```ts
const Example = dynamic(
  () =>
    new Promise(
      (resolve) =>
        setTimeout(() => resolve(import("@components/exmaple")), 10000) // 10초 후 진짜 컴포넌트 불러오기
    ),
  { ssr: false, loading: () => <span>Loading a big component </span>//진찌 컴포넌트를 불러올 동안 보여질 로딩 컴포넌트 }
);
```

- suspense 사용 (React 18 기능)

```ts
// suspense 불러오기
import { Suspense } from "react";

const Name = dynamic(() => import("@component/name"), { suspense: true });

~~~
<Suspense fallback={로딩동안 불러올 컴포넌트}>
  <Name />
</Suspense>;
```

UI 코드는 UI코드안에 있는게 좋기 떄문에 suspense 방법이 더 좋은듯
