# 정적 사이트 생성기 Gatsby

### 정적사이트란(Static Web Page)?

> 서버에 **미리 저장된 파일**이 그대로 전달되는 웹 페이지이다. 모든 사용자는 같은 결과의 웹 페이지를 서버에 요청하고 응답을 받는다.

## 미리 알고가자! JAMstack(JavaScript API Markup)

> 더 빠르고, 안전하며, 스케일링하기 쉬운 웹을 만들기 위해 디자인된 아키텍처

![](https://cdn.inflearn.com/public/files/courses/326897/units/75995/0a45a363-2b26-4848-bdc9-a6d05bbe367c/gatsby-lecture-1-1-2.png)

> **JavaScript**와 **API** 그리고 **Markup**만으로 이루어진 웹의 구성을 말한다. 우리가 알고 있는 SPA과는 비슷하지만 다르다.

> JavaScript  
> Clinet의 모든 처리는 JavaScript에게 맡긴다.

> API  
> 모든 기능 및 비즈니스 로직은 재사용 가능한 API로 추상화한다.

> Markup
> SSG (Static Site Generator)나 Template Engine(Webpack 등)을 이용하여 Markup을 미리 생성한다.

### Markup

세상에는 정말 다양한 Markup을 만들 수 있는 방법이 존재한다.

HTML을 직접 작성하거나, Template Engine같은 툴을 이용하거나, `Jekyll`, `Nextjs`, `Gatsby` 같은 **정적 사이트 생성기**(Static Site Generator, SSG)를 이용해서, **StaticHTML**을 생성할 수도 있다.

그리고 미리 작성된 `Static HTML`은 웹 서버의 리소스를 쓸 필요 없이, 사용자에게 HTML만을 전달 해주면 된다.

이는 매우 큰 장점을 가져오게 되는데, Static HTML을 `CDN`을 통해 `Cache`하고 배포하여, **빠른속도**를 유지한다.

하지만 모든 HTML 이 Static HTML 만으로 이루어진 것을 뜻하지는 않는다.

모든 Markup 을 정적 으로 유지하게 되면, 최신 데이터를 유지하기 어렵기 때문이다.

중요한 것은 최대한 **HTML Build** 을 빌드하여, Cache 하고 사용자를 위한 `First meaningful paint` 의 속도를 높히자는 점이다.

### JAM Stack 과정

JAM Stack을 가장 쉽게 따라해볼 수 있는 방법은 `Gatsby`와 `Netlify`를 이용해 웹사이트를 구축하는 것이다.

`Gatsby` 는 **React** 와 **GraphQL** 를 이용한 정적 사이트 생성기다.

`Netlify` 는 Javascript 코드를 **빌드** 하고 **배포** 하고 **운영**할 수 있게 도와주는 플랫폼이다.

1. GitHub로 프로젝트를 관리한다.
2. Gatsby(SSG)로 정적사이트 생성기를 구축한다.
3. Netlify에 배포환경을 구성한다.
4. GitHub에 코드가 변경되면, Netlify에서 빌드를 시작한다.
5. Netlify로 Gatsby를 빌드하고, 사이트를 배포한다.

한편 배포된 Package는 더 이상 빌드를 위한 웹서버의 자원은 필요하지 않게되고, 모든 처리는 **JavaScript**와 **API**에서 이루어지게 된다.

**JAM Stack**은 하나의 개념이기 때문에, 특정 라이브러리나 플랫폼을 이용하지 않고, 본인이 직접 빌드 툴 혹은 프레임워크을 만들거나, 호스팅 서버나 CDN 을 운영해도 전혀 문제가 없다.

## Gatsby 장점

1. React 문법
2. SEO와 성능
3. 콘텐츠 관리가 쉽다.
4. 기존 방식에 비해 더 빠르게 웹 사이트를 제공할 수 있다.
5. 안전한 웹 사이트를 제공할 수 있다.
6. 스케일링하기 쉬운 웹 사이트를 제공할 수 있다.

## Gatsby 프로젝트 생성하기

```
npx gatsby-cli new "[프로젝트 명]"
```

**실행**

```
cd "[프로젝트 명]"
gatsby develop
# yarn develop 도 마찬가지로 가능
```

**프로젝트 구조**

> /.cache  
> Gatsby의 내부 캐시이다.  
> /public  
> gatsby build 의 Output이 들어간다.  
> /plugins  
> npm에 들어가지 않은 라이브러리나 플로그인을 넣을 수 있다.  
> /src
>
> - /pages  
>   파일 이름과 폴더 이름을 경로로 따르는 페이지
> - /component  
>   컴포넌트의 모음 폴더
> - /images  
>    이미지 모음 폴더  
>    /static  
>    static 폴더에 파일을 저장하면 Webpack 에서 파일을 처리하지 않고 공용 폴더에 복사되는 폴더가 존재한다.

**설정파일**

- gatsby-config.js

  Gatsby 사이트의 기본 구성 파일이다.
  여기서 사이트 제목 및 설명, 포함 할 Gatsby 플러그인 등 사이트 (메타 데이터)에 대한 정보를 지정할 수 있다.

- gatsby-browser.js

  Gatsby 브라우저 API 의 사용이 있는 경우 사용한다.

- gatsby-node.js

  Gatsby 노드 API 사용이 있을 경우의 사용법을 정의한다.

- gatsby-ssr.js

  Gatsby 서버 사이드 렌더링 API 사용이 있을 경우의 사용법 정의한다.
