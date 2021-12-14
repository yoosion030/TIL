# Axios 😍

## Axios란?

- Axios는 브라우저, Node.js를 위한 Promise API를 활용하는 HTTP 비동기 통신 라이브러리입니다.
- 쉽게 말해서 백엔드랑 프론트엔드랑 통신을 쉽게하기 위해 Ajax와 더불어 사용합니다.

## Axios 사용법

**Axios 다운로드**

```
yarn add axios
npm i axios
```

**HTTP Method**

- get
  axios.get(url, [,config])
  예제

```JS
import axios from 'axios';

axios.get('https://my-json-server.typicode.com/zofqofhtltm8015/fs/user').then((Response)=>{
    console.log(Response.data);
}).catch((Error)=>{
    console.log(Error);
})
```
