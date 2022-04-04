# SWR mutate

## mutate 사용

`useSWRConfig()` hook으로부터 `mutate`함수를 얻을 수 있으며, `mutate(key)`를 호풀하여 동일한 키를 사용하는 다른 SWR hook에게 갱신 메시지를 전역으로 브로드캐스팅을 할 수 있다.

```JSX
import useSWR, { useSWRConfig } from "swr";

~~~
    const { mutate } = useSWRConfig();
```

```JSX
mutate("[key 값]", 변경할 데이터, "데이터가 바뀌면 첫번째 인자로 요청할 지 말지" )
```

```JSX
mutate("/api/users/me", (prev: any) => ({ ok: !prev.ok }), false);
```

## 바인딩 된 mutate

bound mutate : 필요한 데이터가 컴포넌트 안에 존재함
unbound mutate : 필요한 데이터가 다른 컴포넌트 안에 존재함

`useSWR`에 의해 반환된 SWR객체는 SWR의 키로 미리 바인딩 된 `mutate()` 함수도 포함한다. 기능적으로 전역 `mutate`함수와 동일하지만 `key`파라미터를 요구하지 않는다.

```JSX
const { data, mutate } = useSWR('/api/user', fetcher)
mutate({ ...data, name: newName })
```
