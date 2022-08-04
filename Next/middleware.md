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

# 중요! v12.2 Middleware 업그레이드 사항

## 업그레이드 방법

nextjs 버전을 v12.2 이상으로 업그레이드 하거나 최신버전을 유지하면 된다.

```
npm i next@latest
npm i next@12.2
```

프로젝트에 ESLint를 구성한 경우 nextjs 버전과 동일한 버전을 사용해야한다.

```
npm i eslint-config-next@latest --dev
npm i eslint-config-next@12.2 --dev
```

## 파일 위치 및 이름 변경

원래는 `_middleware.ts`의 위치에 따라 코드가 적용되는 부분이 달라졌지만
이제는 `pages` 디렉토리와 동일한 위치에 `middleware.ts`를 생성해야 한다.

Before

```
[src]/[pages]/_middleware.ts
```

After

```
[src]/middleware.ts
```

**요약**

- pages폴더 옆에 단일 미들웨어 파일 정의
- 파일에 밑줄을 붙일 필요가 없습니다.
- 사용자 지정 매처를 사용하여 내보낸 구성 개체를 사용하여 일치하는 경로를 정의할 수 있습니다.

## 다중 파일 -> 단일 파일

미들웨어는 앱의 모든 경로에 대해 호출되며 지정 매처를 사용하여 특정 상황에서만 정의할 수 있다.

1. 특정 경로만 요청 하지 않을 때

```ts
// middleware.ts
import { NextResponse } from "next/server";
import type { NextRequest } from "next/server";

export function middleware(request: NextRequest) {
  return NextResponse.rewrite(new URL("/about-2", request.url));
}

// Supports both a single string value or an array of matchers
export const config = {
  matcher: ["/about/:path*", "/dashboard/:path*"],
};
```

2. 특정 경로와 일치할 때만 실행하려고 할 때

```ts
// <root>/middleware.js
import type { NextRequest } from "next/server";

export function middleware(request: NextRequest) {
  if (request.nextUrl.pathname.startsWith("/about")) {
    // This logic is only applied to /about
  }

  if (request.nextUrl.pathname.startsWith("/dashboard")) {
    // This logic is only applied to /dashboard
  }
}
```

## Response 사용 X

Before

```ts
// pages/_middleware.ts
import { NextResponse } from "next/server";
import type { NextRequest } from "next/server";
import { isAuthValid } from "./lib/auth";

export function middleware(request: NextRequest) {
  // Example function to validate auth
  if (isAuthValid(request)) {
    return NextResponse.next();
  }

  return NextResponse.json({ message: "Auth required" }, { status: 401 });
}
```

After

```ts
// middleware.ts
import { NextResponse } from "next/server";
import type { NextRequest } from "next/server";
import { isAuthValid } from "./lib/auth";

export function middleware(request: NextRequest) {
  // Example function to validate auth
  if (isAuthValid(request)) {
    return NextResponse.next();
  }

  const loginUrl = new URL("/login", request.url);
  loginUrl.searchParams.set("from", request.nextUrl.pathname);

  // Response 대신 redirect로 처리
  return NextResponse.redirect(loginUrl);
}
```

**요약**

- 미들웨어는 더 이상 `Response`을 생성할 수 없습니다.
- 미들웨어가 `Response` 응답하면 런타임 오류가 발생합니다.
- 페이지/API 응답을 `rewrite`나 `redirect를 사용하여 마이그레이션

## 새로워진 User-Agent

미들웨어에서는 `User-Agent` 일명 `ua`를 응답으로 부터 얻을 수 있었습니다. 업그레이드 전에는 request에서 바로 접근할 수 있었지만 이제는 `userAgent`를 호출하여 접근해야한다.

Before

```ts
// pages/_middleware.ts
import { NextRequest, NextResponse } from "next/server";

export function middleware(request: NextRequest) {
  const url = request.nextUrl;
  const viewport = request.ua.device.type === "mobile" ? "mobile" :

  return NextResponse.rewrite(url);
}
```

After

```ts
import { NextRequest, NextResponse, userAgent } from "next/server";

export function middleware(request: NextRequest) {
  const url = request.nextUrl;
  // userAgent 호출
  const { device } = userAgent(request);
  const viewport = device.type === "mobile" ? "mobile"

  return NextResponse.rewrite(url);
}
```
