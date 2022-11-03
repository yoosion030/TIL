# 불필요한 재렌더링 막기 (memo, useMemo, useCallback)

리액트에서 렌더링이 자주일어나 복잡하고 무거운 코드를 계속 렌더링 시킨다면 성능도 떨어지고 속도도 느려질 것이다. 이래서 불필요한 렌더링을 막아야 하는 것이다.

## 리액트 렌더링 방식

리액트에선 기본적으로 부모컴포넌트가 렌더링된다면, 자동적으로 자식 컴포넌트도 렌더링이 된다.

자식이 계속 똑같은 값만 가져도 부모 컴포넌트가 계속 재렌더링 된다면 자식 또한 불필요한 렌더링이 이루어진다.

```js
// 부모 컴포넌트
const School = () => {
  return <Student name="홍길동" age={20} address="우리집" />;
};
```

```js
// 자식 컴포넌트
const Student = ({ name, age, address }) => {
  return (
    <div>
      <h1>{name}</h1>
      <span>{age}</span>
      <span>{address}</span>
    </div>
  );
};
```

여기서 Student 컴포넌트의 props가 변경될 때만 렌더링이 되게 만들면 효율적일 것이다! 이럴 때 사용하는게 `React.memo`이다.

## React.memo

리엑트에서 제공해주는 고차 컴포넌트(HOC, Higher Order Component)이다.

먼저 고차 컴포넌트란 ?
컴포넌트 로직을 재 사용하기 위한 React의 고급기술이다. 구체적으로, 고차 컴포넌트는 컴포넌트를 가져와 새 컴포넌트를 반환하는 함수이다. UI나 기능적으론 똑같지만 조금 더 최적화된 컴포넌트를 반환시켜준다.

---

이렇게 최적화된 컴포넌트는 렌더링이 되어야할 상태일 때마다 prop check, 자신이 받는 props에 변화가 있는지 없는지 확인한다.

변화가 있을 경우 렌더링 시키고 변화가 없으면 기존에 렌더링 되었던 내용을 재사용한다.

---

React.memo에서의 memo는 Memoization을 뜻한다. 이미 계산에 놓은 값을 메모리 상에 저장해 놓고 필요할 때마가 꺼내서 재사용하는 기법이다.

React.memo는 꼭 필요할 때만 사용해야한다. 왜냐하면 컴포넌트를 메모이징할 때 렌더링된 결과를 어디에 저장하여 메모리를 추가적으로 소비하기 때문이다..

1. 컴포넌트가 같은 Props로 자주 렌더링 될 때
2. 컴포넌트가 렌더링 될때마다 복잡한 로직을 처리해야할 때

이 두가지 상황에서 React.memo를 사용하면 좋다.

**React.memo는 오직 Props 변화에만 의존하는 최적화 방법이다!**

위 예제에서 사용하자면

```js
import { memo } from "react";

// 자식 컴포넌트
const Student = ({ name, age, address }) => {
  return (
    <div>
      <h1>{name}</h1>
      <span>{age}</span>
      <span>{address}</span>
    </div>
  );
};

export default memo(Student);
```

자식 컴포넌트에 memo를 감싸주면 name, age, address가 바뀔 때만 재렌더링을 시켜준다.

memo 안에 있는 컴포넌트를 인자로 받아 새로운 컴포넌트를 만들어준다.

## React.memo와 useMemo같이 사용하기

예제를 조금 수정해보자

```js
import { useState } from "react";
import Child from "./Child";

const Parent = () => {
  const [parentAge, setParentAge] = useState(0);

  const incrementParentAge = () => {
    setParentAge(parentAge + 1);
  };

  const name = {
    lastName: "홍",
    firstName: "길동",
  };

  console.log("부모 렌더링");
  return (
    <div style={{ margin: "20px", padding: "10px" }}>
      <h1>부모</h1>
      <p>age :{parentAge}</p>
      <button onClick={incrementParentAge}>부모나이증가</button>
      <Child name={name} />
    </div>
  );
};

export default Parent;
```

```js
import { memo } from "react";

const Child = ({ name, age }) => {
  return (
    <div style={{ border: "20x solid powderblue", padding: "10px" }}>
      <p>자녀</p>

      <p>성: {name.lastName}</p>
      <p>이름: {name.firstName}</p>
    </div>
  );
};

export default memo(Child);
```

부모에서 object를 생성하고 그 객체를 자식에게 props로 넘겨주었다. 언뜻보면 name이라는 객체에 변경이 없으니까 Memoization 되어있는 child는 재렌더링이 되지 않을것이다. 하지만 생각과는 다르게 child는 재렌더링이 이루어진다.

왜냐하면 prop으로 넘긴 값이 객체이기 때문이다. 원시타입과는 다르게 메모리의 주소가 변수 안에 저장되기 때문이다. 부모가 렌더링 될 때마다 name도 다시 초기화 된 것이다. 값은 똑같지만 전달되는 주소값이 변경되기 때문에 자식 컴포넌트도 재렌더링 된다.

이런 문제를 해결할 때 `useMemo`를 사용하면 된다.

object에 useMemo에 감싼다.

```js
const name = useMemo(() => {
  return {
    lastName: "홍",
    firstName: "길동",
  };
}, []);
```

## React.memo와 useCallback같이 사용하기

예제를 다시 수정해보자.

```js
import { useMemo, useState } from "react";
import Child from "./Child";

const Parent = () => {
  const [parentAge, setParentAge] = useState(0);

  const incrementParentAge = () => {
    setParentAge(parentAge + 1);
  };

  const tellMe = () => {
    console.log("길동아 스릉해");
  };

  console.log("부모 렌더링");
  return (
    <div style={{ margin: "20px", padding: "10px" }}>
      <h1>부모</h1>
      <p>age :{parentAge}</p>
      <button onClick={incrementParentAge}>부모나이증가</button>
      <Child name={"홍길동"} tellMe={tellMe} />
    </div>
  );
};

export default Parent;
```

```js
import { memo } from "react";

const Child = ({ name, age, tellMe }) => {
  console.log("자녀 렌더링");
  return (
    <div style={{ border: "20x solid powderblue", padding: "10px" }}>
      <p>자녀</p>

      <p>이름: {name}</p>
      <button onClick={tellMe}>엄마 나 사랑해?</button>
    </div>
  );
};

export default memo(Child);
```

부모에서 함수를 생성한 후 자식에세 prop으로 넘기는 형식으로 수정하였다.
여기서 `incrementParentAge` 부모나이증가 버튼을 눌러주면 자식도 렌더링되는 것을 볼 수 있다. 자식이 prop으로 받는 name과 tellMe는 업데이트되지 않았는데 왜 다시 렌더링 되는걸까?

왜냐하면 자바스크립트에서 함수는 객체의 한 종류이기 때문이다. 위에서 객체를 넘겨줬을 때 재렌더링 되는 이유와 같다. 아무리 함수의 내용이 변경되지 않더라도 자식은 재렌더링 된다. 이럴 때 `useCallback`을 사용하자.

```js
const tellMe = useCallback(() => {
  console.log("길동아 스릉해");
}, []);
```

## 결론

React.memo를 사용할 땐 불필요한 렌더링을 막을 수 있어 좋지만, 잘못사용한다면 오히려 메모리 상으로 안좋을 수 있어 정말 필요할 때만 사용하자!

**React.memo는 오직 Props 변화에만 의존하는 최적화 방법이다!**
