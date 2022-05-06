# 노마드코더 강의 정리

## ☑ 1. Library VS Framework

**library**

> 개발자로서 자신이 사용하는 것

내가 원하는대로 코드를 작성할 수 있고 사용하고 싶을 때 사용할 수 있음

**framework**

> 자신의 코드를 불러오는 것

내가 코드를 적절한 위치에 잘 적기만 한다면 framework는 내 코드를 불러와서 모든걸 동작하게 함

### ReactJS ( library ) VS NextJS ( framework )

차이점

- **NextJS**에는 REactDOM.render 가 없음
- **ReactJ**S는 어디에서 컴포넌트를 호출하고 라우팅을 할지 자유롭지만 **NextJS**는 정해진 틀 안에서 코드를 짜야하기 때문에 그 규칙을 따라야 함

## ☑ 2. Pages

- pages 폴더 안에 있는 파일 명 -> 해당 파일 url의 이름  
  **따로 라우팅 안해줘도 됨 개꿀 ㅋ**
- 컴포넌트의 이름은 중요하지 않음
- 홈 화면은 기본적으로 **index.js**에서 나옴
- React를 import안해줘도 됨

주의점

- **화면에 보여질 컴포넌트는 export default 해줘야함**
- useState나 useEffect와 같은 react method를 쓰고 싶다면 import 구문을 써줘야함

## ☑ 3. Static Pre Rendering

noscript

> 유저가 브라우저에서 자바스크립트를 비활성화 했을 때만 나오는 태그

**client-side-rendering => ReactJS**

> 브라우저가 자바스크립트를 가져와서 client-side의 자바스크립트가 모든 UI를 만듦

- 느린 연결로 웹페이지에 들어갈 경우 초기 화면은 빈 화면이 뜸

=> 아직 자바스크립트 코드를 안가져왔기 때문 자바스크립트 코드를 가져와야 비로소 UI들을 볼 수 있음

- HTML이 js 코드를 가져왔을 때 보여짐

**pre-rendering => NextJS**

> 앱의 초기상태를 활용해서 미리 렌더링 되어짐

- 유저들의 연결 속도가 느리거나 자바스크립트가 비활성화 되어있더라도 페이지를 볼 수 있음
- js 코드를 가져오기 전에도 HTML이 보여짐
- 페이지가 로딩 됐을 때, ReactJS가 넘겨받아서 동작시키게 함

NextJS는 HTML을 페이지의 소스코드에 넣어주기 때문에 유저는 자바스크립트와 ReactJS가 로딩되지 않았더라도 콘텐츠를 볼 수 있음

ReactJS가 로딩되었을 때 기본적으로 이미 존재하는 것들과 연결이 되어서 일반적인 ReactJS앱이 됨

**hydration**

> ReactJS를 프론트엔드 안에서 실행시키는 것

맨 처음 페이지에 들어갔을 때 HTML을 보여지게하고 그러고 나서 ReactJS가 클라이언트로 전송됐을 때 ReactJS 앱이 됨

## ☑ 4. Routing

NextJS에서 a태그를 사용하려고 하면 경고 문구가 뜸
=> NextJS에 앱 내에서 페이지를 이동할 때 사용해야만 하는 특정 컴포넌트가 있기 때문

**Link**
사용예시

````JSX
import Link from 'next/link'

~~~ return (
      <Link href="/about">
        <a>about</a>
      </Link>
  )
```
````

=> 페이지를 새로고침 안해도 됨 개빠름

하지만 Link 태그에 **className**이나 *style*을 줄 수 없기 때문에 Link 태그 안에 a 태그를 넣어서 속성을 추가 해주면 됨

**useRouter 훅을 이용해 activeStyle 주기**

```JSX
import { useRouter } from 'next/router'

  const router = useRouter()
~~~  return (
    <>
      <Link href="/">
        <a style={{ color: router.pathname === '/' ? 'red' : 'blue' }}>Home</a>
      </Link>
      <Link href="/about">
        <a style={{ color: router.pathname === '/about' ? 'red' : 'blue' }}>
          about
        </a>
      </Link>
    </>
  )
```

## ☑ 5. CSS Modules

(파일명).module.css 로 파일 생성
사용예시

```css
.nav {
  display: flex;
  justify-content: space-between;
  background-color: tomato;
}
```

```JSX
import styles from './NavBar.module.css'

      ~~~
       <nav className={styles.nav}>
```

위의 코드 처럼 import해준 후 className을 `className="nav"`로 해주는게 아니라 객체 프로퍼티 형식으로 선언해줘야함

Module css의 장점으로는 코드에서는 클래스네임이 `nav`이지만 브라우저에서 코드를 보면 `NavBar_nav__OBiyO`와 같이 무작위로 클래스네임을 만들기 때문에, 다른 모듈에서 똑같은 이름의 클래스를 선언해줘도 중복될 일이 없음 개꿀 ㅋ

**activeClass**
사용예시

```JSX
import { useRouter } from 'next/router'
  import styles from './NavBar.module.css'

  const router = useRouter()
~~~  return (
    <nav>
      <Link href="/">
        <a className={router.pathname === '/' ? styles.active : ''}>Home</a>
      </Link>
      <Link href="/about">
        <a className={router.pathname === '/about' ? styles.active : ''}>
          about
        </a>
      </Link>
    </nav>
  )

  )
```

**클래스 여러개 주기**

1. 문자열 사용

```JSX
  <a className={`${styles.link} ${styles.nav}`}></a>
```

2. 배열 사용

```JSX
  <a className={[styles.link, styles,nav].join(" ")}></a>


```

## ☑ 6. Styles JSX

**styles jsx**
사용 예시

```JSX
      <style jsx>{`
        nav {
          background-color: tomato;
        }
        a {
          text-decoration: none;
        }
      `}</style>
```

**범위 : 선언해준 컴포넌트 내부**  
NavBar에서 `className`이 `active`인 클래스를 선언하면 Hello컴포넌트에서는 active클래스를 사용할 수 없다

## ☑ 7. Custom App

**global style**

```JSX
<style jsx global></style>
```

범위 : 선언해준 컴포넌트 내부

**모든 페이지에 스타일이나 컴포넌트 주기**

1. Pages폴더에 \_app.js 파일 생성
2. Props 부분에 `Component`랑 `pageProps` 넘겨주기

```JSX
export default function App({ Component, pageProps }) {
  return (
      <Component {...pageProps}></Component>
  )
}

```

3. about, home 컴포넌트에서 `NavBar` 라는 컴포넌트가 중복되어있기 때문에 \_app.js 에서 NavBar를 불러와준다.

```JSX
import NavBar2 from '../components/NavBar2'

export default function App({ Component, pageProps }) {
  return (
    <div>
      <NavBar2></NavBar2>
      <Component {...pageProps}></Component>
    </div>
  )
}

```

4. 그러면 home, about 컴포넌트 둘다 NavBar 가 보이게 된다 !!
5. 모든 컴포넌트에 동일한 스타일을 주고싶다면 \_app.js에 jsx global 을 주면 됨

```JSX
      <style jsx global>
        {`
          body {
            background: #b8b8fd;
          }
        `}
      </style>
```

## ☑ 8. Head

NextJS 에서는 ReactJS와 다르게 index.html이 없어서 `title`을 직접 바꿀 수가 없다. 하지만 NextJS에서는 **HEAD** 라는 것을 제공하여 index.html에 접근할 수 있다.

```JSX
import Head from 'next/head';

~~~
<Head>
  <title>Next 짱 !</title>
</Head>

```

**더 편리하게 사용하기**

1. components 폴더에 Seo.js 파일을 만들어준다.

2. Seo.js

```jsx
import Head from "next/head";

export default function Seo({ title }) {
  return (
    <Head>
      <title>{title} | Next Movies</title>
    </Head>
  );
}
```

3. about.js

```JSX
import Seo from '../components/Seo'
export default function About() {
return (
  <>
    <Seo title="About"></Seo>
  </>
)
}

```

## ☑ 9. Server Side Rendering ( SSR )

**SSR의 동작 순서**

1. 서버는 렌더링 할 준비가 된 HTML 응답을 브라우저에게 보낸다.
2. 브라우저는 페이지를 렌더링한다. 이 때 페이지를 볼 수 있게된다.
3. 브라우저가 JS를 다운로드 받는다.
4. 브라우저가 React를 실행한다.
5. 페이지를 상호작용할 수 있다.

**장점**

1. CSR에 비해 렌더링 속도가 빨라 사용자가 기다리는 로딩시간이 짧다.
2. 검색엔진 최적화가 쉽다.

**단점**

1. CSR에 비해 서버에 부하가 많다.
2. 사용자가 페이지를 전환 시 화면이 깜빡깜빡 거린다는 느낌을 받을 수 있다.

### getServerSideProps

만약 하나의 페이지에서 **Server-side Rendering**하게 되면, HTML 페이지는 모든 요청(request)에서 생성됩니다.

하나의 페이지를 Server-side Rendering 하기 위해서, **getServerSideProps** 함수를 비동기 처리하여 사용합니다. 이 함수는 모든 요청(request)에서 Server에 의해 실행됩니다. (빌드할 때 실행 X)

예를 들어, 외부 API로 부터 자주 업데이트되는 데이터를 **pre-rendering**하기 위한 페이지가 필요하다면, 데이터를 가져오기 위한 **getServerSideProps** 함수를 작성할 수 있으며 아래 코드와 같이 페이지에 데이터를 전달할 수 있습니다.

```JSX

export async function getServerSideProps() {
  const { results } = await (await fetch(`http://localhost:3000/api/movies`)).json();
  return {
    props:{
      results,
    }
  }

}
```

props로 넘기기

```JSX
export default function Home({results})
```

## ☑ 10. Dynamic Routes

ex ) movies/all -> 라우팅 하는 방법

1. pages 폴더에 movies 폴더를 만들어 준다.
2. movies 폴더 안에 all.js 파일을 만들어주면 끝

만약 movies 만 라우팅 하고 싶다면?

1. movies 폴더 안에 index.js 파일을 만들어주면 끝

**URL 변수 달아주기**
ex ) movies/영화id

파일명 -> [변수명].js

**페이지 이동시키기**

1. 함수를 만들어 onClick 함수에서 실행시키기

```JSX
  const router = useRouter();
  const onClick = (id, title) => {
    router.push(
      {
        pathname: `movies/${id}`,
        query: {
          title,
        },
      },
      `movies/${id}`,
    );
  };
```

2. Link 컴포넌트 이용하기

```JSX
  <Link
    href={{
      pathname: `movies/${movie.id}`,
      query: {
        title: movie.original_title,
      },
    }}
    as={`movies/${movie.id}`}
  >
    <a>
      <h4>{movie.original_title}</h4>
    </a>
  </Link>
```

## ☑ 11. 404Page

파일명 : 404.js
