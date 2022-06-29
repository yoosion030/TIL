# Middleware

## Middlewares가 무엇인가?

미들웨어는 양 쪽을 연결하여 데이터를 주고받을 수 있도록 **중간에서 매개 역할을 하는 소프트웨어**, 네트워크를 통해서 연결된 여러 개의 컴퓨터에 있는 많은 프로세스들에게 어떤 서비스를 사용할 수 있도록 연결해주는 소프트웨어를 말한다.

## 목적

사용자가 무슨 행동을 하였을 때 ( ex) 로그인 페이지에서 회원가입 페이지로 이동 시, 페이지 이동 시, api 요청 시 ) 특정 코드(ex ) 로그인 여부 확인)를 실행시키려고 middleware를 사용한다.

## NextJS에서 Middleware 사용

코드를 어디에 적냐에 따라서 특정 부분에만 해당 코드를 적용시킬 수 있다.

파일이름 : **\_middleware.js[ts]**

유저가 다른 페이지로 이동할 때마다 실행되는 미들웨어 => global middleware

- pages/\_middleware.js[ts]

/profile 경로 안에서만 실행되는 미들웨어

- pages/profile/\_middleware.js[ts]

## Middleware 응용

**req, ev 인자로 받기**

```ts
// 페이지 이동할 때와 api 요청할 때 middleware가 실행됨

import type { NextRequest, NextFetchEvent } from "next/server";
import { NextResponse } from "next/server";
export default function middleware(req: NextRequest, ev: NextFetchEvent);
```

**req 속성**

```ts
req :{
    geo, // 위치
    iq, // ip
    page,
    url, // page 주소
    ua : { // user 정보
        isBot: boolean; // 봇인지 아닌지
        ua: string;
        browser: {
            name?: string;
            version?: string;
        };
        device: {
            model?: string;
            type?: string;
            vendor?: string;
        };
        engine: {
            name?: string;
            version?: string;
        };
        os: {
            name?: string;
            version?: string;
        };
        cpu: {
            architecture?: string;
        };
    },
}
```

**user가 봇인걸 감지했을 때 요청 막기**

```ts
// 페이지 이동할 때와 api 요청할 때 middleware가 실행됨

import type { NextRequest, NextFetchEvent } from "next/server";
import { NextResponse } from "next/server";
export default function middleware(req: NextRequest, ev: NextFetchEvent) {
  // 봇일때
  if (req.ua?.isBot) {
    return new Response("Plz don't be a bot.", { status: 403 });
  }
}
```

**요청 주소가 /... 일 때 미들웨어 실행 막기**

```ts
// 페이지 이동할 때와 api 요청할 때 middleware가 실행됨

import type { NextRequest, NextFetchEvent } from "next/server";
import { NextResponse } from "next/server";
export default function middleware(req: NextRequest, ev: NextFetchEvent) {
  if (!req.url.includes("/api")) {
    return NextResponse.redirect("/enter");
  }
}
```

**특정 주소에서 && 쿠키가 없을 때 미들웨어 실행 막기**

```ts
// 페이지 이동할 때와 api 요청할 때 middleware가 실행됨

import type { NextRequest, NextFetchEvent } from "next/server";
import { NextResponse } from "next/server";
export default function middleware(req: NextRequest, ev: NextFetchEvent) {
  if (!req.url.includes("/enter") && !req.cookies.carrotsession) {
    return NextResponse.redirect("/enter");
  }
}
```
