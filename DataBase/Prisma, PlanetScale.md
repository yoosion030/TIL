# Prisma, PlanetScale 찍먹하기

## Prisma 란?

> Node.js와 Typescript ORM

ORM : Object Relational Mapping => 번역기 역할

JS, TS 코드와 DB사이에 다리를 놓아줌

## 장점

SQL같은 데이터베이스 언어를 작성하지 않고 타입스크립트 코드만 작성함
=> 타입스크립트로만 작성하면 요류가 발생하기 전에 알려주기 때문에 매우 굳굳

## PlanetScale 란?

> MySQL과 호환되는 serverless 데이터베이스 플랫폼

serverless : 서버가 없다는게 아니라, 우리가 서버를 유지할 필요가 없다는 뜻
데이터베이스 플랫폼 : 데이터베이스 제공

### Vitess ?

- 가장 스케일링 기능이 뛰어난 오픈소스 데이터베이스
- 대기업들이 규모에 맞게 MySQL을 scale 하기 위해 쓰는 방법

## 장점

- CLI(Command-line interface)가 좋음
- 데이터 베이스를 마치 깃을 쓰는 것처럼 다룰 수 있음
- 데이터 베이스에 브랜치를 만들 수 있음

## Set Up

**prisma 설정**

1. VSCode extension에서 Prisma 설치 ( 자동완성 기능 땜시 )
2. Prisma 설치
   > npm i prisma -D
3. Prisma 생성
   > npx prisma init
   > .env와 schema.prisma 파일이 생김
4. 사용할 데이터 베이스 설정
   provider = "사용할 데이터베이스"

```js
datasource db {
  provider = "mysql" // postgresql, sqlserver, mongodb, sqlite ...
  url = env("DATABASE_URL")
}
```

5. 데이터 베이스 만들기

```js
// schema.prisma
model User {
  id        Int      @id @default(autoincrement())
  phone     Int?     @unique
  email     String?  @unique
  name      String
  avatar    String?
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
}
```

이름 | 자료형 | 조건

- 자료형? : 필수적이지 않은 선택적인 옵션
- @id : model의 id = 유니크한 식별자
- autoincrement() : 자동으로 증가
- unique : 중복 X
- DateTime : 날짜를 나타내는 자료형
- now() : 새 모델이 만들어질 때 그 시점의 날짜를 가져와주는 함수
- updatedAt : 모델이 업데이트 될 때마다 이 field가 변함

**planetscale 설정**

1. PlanetScale, mysql-client 설치

   > brew install planetscale/tap/pscale  
   > brew install mysql-client

   다운로드 후 pscale 명령어 입력하면 CLI를 볼 수 있음

2. https://planetscale.com/ 로그인
3. 로그인 (planetscale 연결)
   > pscale auth login
   > confirm code
4. 데이터 베이스 만들기

   > pscale database create --region [데이터베이스 이름] ap-northeast

   https://app.planetscale.com/rsy5487 관리자 페이지 가보면 데이터베이스가 만들어져 있음

5. 데이터베이스와 보안 tunnel 연결하기

   > pscale connect [연결할 데이터베이스 이름]

   터미널에 url이 뜨고 계속 연결하려면 터미널 창을 닫으면 안됨 ㅇㅇ

6. 환경변수 설정
   ```env
   //env
   DATABASE_URL="mysql://127.0.0.1:3306/[데이터베이스 이름]"
   ```
7. 호환설정하기  
   PlanetScale은 MySQL과 '호환되는' 서버 플랫폼이라 MySQL이랑은 몇가지를 다르게 처리함. 그래서 몇몇 오류들이 생기면 에러를 발생하지 않고 그냥 넘기기 때문에 호환 설정을 해주면 좋음

   ```JS
   // schema.prisma
   generator client { ~~~
   previewFeatures = ["referentialIntegrity"]
   }
   datasource db { ~~~
   referentialIntegrity = "prisma"
   }
   ```

8. schema를 planetscaledp push 하기
   > npx prisma db push
   > tunnel 연결 창이 꺼져있으면 안됨 ㅇㅇ

**Prisma Client 사용**

1. prisma studio 설치

   > npx prisma studio

   여기서 데이터 필드들을 볼 수 있음
   새로고침해서 데이터 갱신도 가능
   수동으로 추가 가능

2. client 초기화, libs/clients.ts 파일 생성
3. client 설치
   > npm install @prisma/client
4. @prisma/client 생성

```js
// libs/clients.ts
import { PrismaClient } from "@prisma/client";

export default new PrismaClient();
```

5. > npx prisma generate

client를 프론트엔드 상에서 접근하려고 한다면 에러가 뜸
브라우저에서 PrismaClient를 실행할 수 있으면 안됨

- client는 데이터베이스에 직접 접근할 수 있는 파일을 프론트엔드인 브라우저에 추가했기 때문
- 사용자들에게 데이터베이스를 수정할 수 있는 권한을 주면 안되기 때문

**Next 서버에서 prisma 접근**

1. pages/api/test.tsx 파일 생성
2. API 생성하기  
   connection 핸들러인 함수를 export default 해주면 됨

```TSX
// pages/api/test.tsx
import { NextApiRequest, NextApiResponse } from "next";

export default async function handler(
  req: NextApiRequest,
  res: NextApiResponse,
) {

   }
```

Nextjs 가 제공해주는 req, res 사용

3. prisma client 불러오기

```js
import client from "../../libs/client";
```

4. prisma client 접근, 생성하기

```TSX
export default async function handler(
  req: NextApiRequest,
  res: NextApiResponse,
) {
  await client.user.create({
    data: {
      email: "hi",
      name: "hi",
    },
  });
  res.json({
    ok: true,
  });
}
```

promise 를 return 해주기 때문에 비동기 처리 (async, await)

5. localhost:3000/api/test 접속

```JS
  res.json({
    ok: true,
  });
```

를 해줬기 때문에 페이지에 접속하면 아래 값이 보임

```JSON
{"ok":true}
```

6. prisma studio 에서 새로고침하면

```JS
    data: {
      email: "hi",
      name: "hi",
    },
```
값이 추가됨
