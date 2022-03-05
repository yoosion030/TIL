# CORS 에러란

## 첫 만남

axios로 api요청을 하니 밑에 있는 오류 창이 떴다.

![](https://blog.kakaocdn.net/dn/mt0QR/btq251Jf8UD/epGbjsFvDNPMrMFvvAn70k/img.png)

라이브러리도 잘 불러왔고 서버도 켜져있는데 왜 이러한 오류가 뜨는걸까?

## CORS 발생 이유

![](https://blog.kakaocdn.net/dn/t8IFv/btq26nrRXXh/ADipqPCoL57g8ObPu2taO1/img.png)

**교차 출처 리소스 공유(Cross-Origin Resource Sharing, CORS)**는 추가 HTTP 헤더를 사용하여, 한 출처에서 실행 중인 웹 애플리케이션이 다른 출처의 선택한 자원에 접근할 수 있는 권한을 부여하도록 브라우저에 알려주는 체제이다. 웹 애플리케이션은 리소스가 자신의 출처와 다를 때 교차 출처 HTTP 요청을 실행한다.

교차 출처 요청의 예시

https://domain-a.com/ 의 프론트엔드 JS 코드가 XMLHttpRequest를 사용하여  
https://www.domain-b.com/data.json 을 요청하는 경우

보안 상의 이유로, 브라우저는 스크립트에서 시작한 교차출처 HTTP 요청을 제한한다. 예를 들어, XMLHttpRequest와 Fetch API는 동일 출처 정책을 따른다. 즉, 이 API를 사용하는 웹 애플리케이션은 자신의 출처와 동일한 리소스만 불러올 수 있으며, 다른 출처의 리소스를 불러오려면 그 출처에서 올바른 CORS 헤더를 포함한 응답을 반환해야한다.

**요약**

- CORS는 서로 다른 출처간에 리소스를 전달하는 방식을 제어하는 체제이다.
- CORS 요청이 가능하려면 서버에서 특정헤더인 Access-Control-Allow-Origin과 합께 응답할 필요가 있다.

CORS 정책을 위반하여 서로 다른 출처를 가진 상태에서 무언가를 요청하게 되면 브라우저가 보안 상의 이유로 차단해버린다.

예를들어, 클라이언트 포트가 3000번이고 서버의 포트가 8000번일 때, 클라이언트에서 서버로 리소스 요청을 했을 때 CORS에러 메세지가 클라이언트 콘솔에 빨갛게 뜨고 데이터를 주지 않게 된다.

## 해결방법 1. 남이 만든 프록시 서버 사용하기

프록시 서버란 클라이언트가 프록시 서버 자신을 통해서 다른 네트워크 서비스에 간접적으로 접속할 수 있게 해주는 서버이다. 쉽게말해 브러우저와 서버간의 통신을 도와주는 중계서버라고 생각하면 된다.

```
https://cors-anywhere.com
```

위 서버를 프록시 서버로 사용하게 되면, 요청해야하는 URL앞에 프록시 서버 URL을 붙여서 요청하면 된다.

```JS
axios.get('https://cors-anywhere.com/https://api.dropper.com')
```


## 해결방법 2. 클라이언트 : http-proxy-middleware 사용하기

CRA로 개발중일 경우, **http-proxy-middleware** 라이브러리를 설치하고, setupProxy.js 라는 파일을 생성한다.
```JS
const { createProxyMiddleware } = require("http-proxy-middleware")

module.exports = function(app) {
    app.use("/api", createProxtMiddleware({
        target: "http://localhost:3000",
        changeOrigin: true,
    }))
}
```
위와 같이 코드를 작성해두면, 로컬 환경에서 :3000/api로 시작되는 요청을 라이브러리가 ex) 5000:api로 프록싱 해주게 된다.

## 해결방법 3. package.json 에서 프록시 설정

**package.json**

proxy : 접근할 도메인
```JSON
{
    "proxy": "http://localhost:8000",
}
```

:3000/api에 요청하려고 하면,
```JS
axios.post("/api",)
```
이런식으로 URL을 적어주면 된다.


