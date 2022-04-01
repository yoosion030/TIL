# SWR (stale-while-revalidate)

## SWR 설명

예를 들어, 유저가 홈 화면으로 간다고 하자. 홈 화면에는 user 정보를 불러오는 API가 있다. 우리는 이 API를 호출해서 유저에 대한 정보를 받을 것이다.

홈 화면이 아닌 다른 페이지로 갔다가 다시 홈 화면으로 돌아오면, **SWR은 API를 다시 요청하지 않고 전에 받은 데이터를 가져온다.** 이렇게 페이지로 돌아오면 로딩을 다시 보지 않을 것이다.

## SWR 과정

우선 페이지에 접근하면 SWR이 데이터를 불러오고 API 응답이 도착하면 그 데이터를 캐시에 저장한다. 다른 페이지에 갔다가 다시 돌아오면 SWR이 전에 받은 데이터를 불러오고 아무도 모르게 API에 새로운 데이터가 있는지 확인한다. SWR이 API에 요청을 보내고 새로운 데이터가 있으면 업데이트 해준다. **그래서 항상 최신 데이터를 확인할 수 있고, 페이지를 이동할 때마다 로딩표시를 볼 필요가 없다.**

## SWR 설치

```terminal
> npm install swr
```

오류가 난다면

```terminal
> npm install swr --legacy-peer-deps
```

## useSWR 사용

```tsx
import useSWR from "swr" // swr 불러오기

~~~
const {} = useSWR(url, fetcher);
```

useSWR은 2개의 인자를 가진다. 첫번째는 요청을 보낼 url이고 두번째 인자는 fetcher함수이다. fetcher 함수는 첫번재 key에 입력한 url을 받는다. 이 url은 API를 요청할 url이기도 하면서 캐시를 저장할 때 사용할 key 이기도 한다.

```tsx
const fetcher = (url: string) => fetch(url).then((res) => res.json());

~~~
const {data, error} = useSWR("/api/users/me",fetcher);
```

fetcher 함수가 하는 일은 데이터를 불러오고, 그 데이터를 리턴하는 것이다.

```tsx
import { useRouter } from "next/router";
import { useEffect, useState } from "react";

export default function useUser() {
  const [user, setUser] = useState();
  const router = useRouter();
  useEffect(() => {
    fetch("/api/users/me")
      .then((res) => res.json())
      .then((data) => {
        if (!data.ok) {
          return router.replace("/enter");
        }
        setUser(data.profile);
      });
  }, [router]);
  return user;
}
```

## SWR 개쩌는 점

SWR은 아무도 모르게 API 요청을 보내 데이터 내용이 바뀌었는지 체크한다. 만약에 데이터가 바뀌었다면 바뀐 데이터를 업데이트 해주는 것이다.

useSWR의 첫번째 key, 즉 url은 API url로 사용하기도 하고 fetcher가 캐시에서 데이터를 가져올 때 사용하는 id로도 사용한다. 그러니 앱의 어느 곳에서라도 여기로 요청을 보내면 id가 유일하고 같기 때문에 유저가 어떤 컴포넌트에서든지 캐시 데이터를 확인할 수 있다.
**즉, 이 말은 useSWR을 사용하면 앱, 컴포넌트, 페이지 모든 곳에서 데이터를 공유할 수 있다는 것이다.** props 지옥에서 벗어날 수 있다는 거임!!!!

처음 페이지에 들어오고 Network 탭을 보면 아무것도 없다. 여기서 유저가 다른 탭에 있는 다른 웹사이트에서 다른 작업을 하고 다시 우리 페이지로 돌아오면 유저가 새로운 알림을 받았을 수도 있고 DB내용이 바뀌었을 수도 있다. 그러면 유저가 웹 사이트로 돌아왔을 때 바뀐 데이터를 보여주는게 좋을 것이다. 근데 이 작업을 useSWR이 알아서 해준다는 거임!!!!
한번 다른 페이지를 갔다가 우리 페이지를 돌아와서 Network 탭을 봐보자.  
**useSWR은 유저가 다른 탭에 갔다가 다시 돌아왔을 때 데이터를 새로고침 해준다.** 이 모든게 아무도 모르게 알아서 처리되는 것이다.
