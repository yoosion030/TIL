# Axios 😍

## Axios란?

- Axios는 브라우저, Node.js를 위한 Promise API를 활용하는 HTTP 비동기 통신 라이브러리입니다.
- 쉽게 말해서 백엔드랑 프론트엔드랑 통신을 쉽게하기 위해 Ajax와 더불어 사용합니다.

## axios 특징

- 운영 환경에 따라 브라우저의 XMLHttpRequest 객체 또는 Node.js의 http api 사용
- Promise(ES6) API 사용
- 요청과 응답 데이터의 변형
- HTTP 요청 취소
- HTTP 요청과 응답을 JSON 형태로 자동 변경

## Axios 사용법

**Axios 다운로드**

```
yarn add axios
npm i axios
```

- get

```
  axios.get(url, [,config])
```

```JS
import axios from 'axios'; // axios 불러오기

axios.get('https://my-json-server.typicode.com/zofqofhtltm8015/fs/user').then((Response)=>{
    console.log(Response.data);
}).catch((Error)=>{
    console.log(Error);
})
```

**GET은 서버에서 어떤 데이터를 가져와서 보여준다거나 하는 용도이다.** 주소에 있는 쿼리스트링을 활용해서 정보를 전달하는 것이지 GET메서드는 값이나 상태등을 바꿀 수 없습니다.

- post

```
axios.post(url,{
    data객체
  },[,config])
```

post 메서드의 **두 번째 인자는 본문으로 보낼 데이터를 설정한 객체 리터럴을 전달**합니다.

- delete

```
axios.delete(URL,[,config]);
```

REST 기반 API 프로그램에서 **데이터베이스에 저장되어 있는 내용을 삭제하는 목적으로 사용**합니다. delete 메서드는 서버에 있는 데이터베이스의 내용을 삭제하는 것을 주 목적으로 하기에 두번재 인자를 아예 전달하지 않습니다.

- put

```
axios.put(url[, data[, config]])
```

REST 기반 API 프로그램에서 데이터베이스에 저장되어 있는 내용을 갱신하는 목적으로 사용됩니다.
