# Axios ๐

## Axios๋?

- Axios๋ ๋ธ๋ผ์ฐ์ , Node.js๋ฅผ ์ํ Promise API๋ฅผ ํ์ฉํ๋ HTTP ๋น๋๊ธฐ ํต์  ๋ผ์ด๋ธ๋ฌ๋ฆฌ์๋๋ค.
- ์ฝ๊ฒ ๋งํด์ ๋ฐฑ์๋๋ ํ๋ก ํธ์๋๋ ํต์ ์ ์ฝ๊ฒํ๊ธฐ ์ํด Ajax์ ๋๋ถ์ด ์ฌ์ฉํฉ๋๋ค.

## axios ํน์ง

- ์ด์ ํ๊ฒฝ์ ๋ฐ๋ผ ๋ธ๋ผ์ฐ์ ์ XMLHttpRequest ๊ฐ์ฒด ๋๋ Node.js์ http api ์ฌ์ฉ
- Promise(ES6) API ์ฌ์ฉ
- ์์ฒญ๊ณผ ์๋ต ๋ฐ์ดํฐ์ ๋ณํ
- HTTP ์์ฒญ ์ทจ์
- HTTP ์์ฒญ๊ณผ ์๋ต์ JSON ํํ๋ก ์๋ ๋ณ๊ฒฝ

## Axios ์ฌ์ฉ๋ฒ

**Axios ๋ค์ด๋ก๋**

```
yarn add axios
npm i axios
```

## axios ๊ธฐ๋ณธ ์ฌ์ฉ๋ฒ

```JS
axios
  .get('/user?ID=12345')
  // ์๋ต(์ฑ๊ณต)
  .then((res) => {
    console.log(res)
  })
  // ์๋ต(์คํจ)
  .catch((err) =>{
    console.log(err)
  })
```

์๋์ ๊ฐ์ด **async await**์ ๊ฐ์ด ์ฌ์ฉํด์ ์ข ๋ ๋ณด๊ธฐ ์ข๊ฒ ์ฐ๊ธฐ๋ ํ๋ค.

```JS
 const getUser = async() => {
  try {
    const res = await axios.get('/user?ID=12345')
    console.log(res)
  } catch (err) {
    console.log(err)
  }
}
```

์ธ์คํด์ค๋ฅผ ํ๋ ์์ฑํด์ axios ๊ธฐ๋ณธ์ธํ์ ํ ์๋ ์๋ค.

```JS
const instance = axios.create({
  baseURL: 'https://some-domain.com/api/',
  headers: { 'X-Custom-Header': 'foobar' },
  timeout: 1000,
})
```

- get

```js
axios.get(url, [, config]);
```

```JS
import axios from 'axios'; // axios ๋ถ๋ฌ์ค๊ธฐ

axios.get('https://my-json-server.typicode.com/zofqofhtltm8015/fs/user').then((res)=>{
    console.log(res.data);
}).catch((err)=>{
    console.log(err);
})
```

**GET์ ์๋ฒ์์ ์ด๋ค ๋ฐ์ดํฐ๋ฅผ ๊ฐ์ ธ์์ ๋ณด์ฌ์ค๋ค๊ฑฐ๋ ํ๋ ์ฉ๋์ด๋ค.** ์ฃผ์์ ์๋ ์ฟผ๋ฆฌ์คํธ๋ง์ ํ์ฉํด์ ์ ๋ณด๋ฅผ ์ ๋ฌํ๋ ๊ฒ์ด์ง GET๋ฉ์๋๋ ๊ฐ์ด๋ ์ํ๋ฑ์ ๋ฐ๊ฟ ์ ์์ต๋๋ค.

- post

```
axios.post(url,{
    data๊ฐ์ฒด
  },[,config])
```

```JS
axios.post( 'url',
  {
   contact: 'Sion',
   email: 'rsy5487@naver.com'
   },
  {
   headers:{
    'Content-type': 'application/json',
    'Accept': 'application/json'
      }
    }
  )
  .then((res) => { console.log(res.data); })
  .catch((err) => { console.log(err) });
```

post ๋ฉ์๋์ **๋ ๋ฒ์งธ ์ธ์๋ ๋ณธ๋ฌธ์ผ๋ก ๋ณด๋ผ ๋ฐ์ดํฐ๋ฅผ ์ค์ ํ ๊ฐ์ฒด ๋ฆฌํฐ๋ด์ ์ ๋ฌ**ํฉ๋๋ค.

- delete

```
axios.delete(URL,[,config]);
```

REST ๊ธฐ๋ฐ API ํ๋ก๊ทธ๋จ์์ **๋ฐ์ดํฐ๋ฒ ์ด์ค์ ์ ์ฅ๋์ด ์๋ ๋ด์ฉ์ ์ญ์ ํ๋ ๋ชฉ์ ์ผ๋ก ์ฌ์ฉ**ํฉ๋๋ค. delete ๋ฉ์๋๋ ์๋ฒ์ ์๋ ๋ฐ์ดํฐ๋ฒ ์ด์ค์ ๋ด์ฉ์ ์ญ์ ํ๋ ๊ฒ์ ์ฃผ ๋ชฉ์ ์ผ๋ก ํ๊ธฐ์ ๋๋ฒ์ฌ ์ธ์๋ฅผ ์์ ์ ๋ฌํ์ง ์์ต๋๋ค.

```JS
axios.delete("/thisisExample/list/30")
  .then((res)=>{
    console.log(res);
  })
  .catch((err)=>{
    console.log(err)
  }
```

- put

```
axios.put(url[, data[, config]])
```

REST ๊ธฐ๋ฐ API ํ๋ก๊ทธ๋จ์์ ๋ฐ์ดํฐ๋ฒ ์ด์ค์ ์ ์ฅ๋์ด ์๋ ๋ด์ฉ์ ๊ฐฑ์ ํ๋ ๋ชฉ์ ์ผ๋ก ์ฌ์ฉ๋ฉ๋๋ค.

## axios์ fetch์ ์ฐจ์ด์ 

![](https://cdn.discordapp.com/attachments/902487399605604352/942793400804073492/unknown.png)

## config ์ต์๊ณผ ์๋ต ์คํค๋ง

```JS
{
  // `url`์ ์์ฒญ์ ์ฌ์ฉ๋  ์๋ฒ URL์๋๋ค.
  url: '/user',

  // `method`๋ ์์ฒญ์ ํ  ๋ ์ฌ์ฉ๋  ๋ฉ์๋ ์ด๋ฆ์๋๋ค.
  method: 'get', // ๊ธฐ๋ณธ

  // `url` ์์ฑ ๊ฐ์ด ์ ๋ URL์ด ์๋๋ผ๋ฉด, `url` ์์ `baseURL`์ด ๋ถ์ต๋๋ค.
  // axios ์ธ์คํด์ค๊ฐ ์๋ URL์ ํด๋น ์ธ์คํด์ค์ ๋ฉ์๋์ ์ ๋ฌํ๋๋ก
  // `baseURL`์ ์ค์ ํ๋ ๊ฒ์ด ํธ๋ฆฌ ํ  ์ โโ์์ต๋๋ค.
  baseURL: 'https://some-domain.com/api/',

  // `transformRequest`๋ ์๋ฒ์ ๋ณด๋ด๊ธฐ ์ ์ ์์ฒญ ๋ฐ์ดํฐ๋ฅผ ๋ณ๊ฒฝํ  ์ ์์ต๋๋ค.
  // ์์ฒญ ๋ฉ์๋ 'PUT', 'POST' ๋ฐ 'PATCH' ์๋ง ์ ์ฉ ๊ฐ๋ฅํฉ๋๋ค.
  // ๋ฐฐ์ด์ ๋ง์ง๋ง ํจ์๋ ๋ฒํผ(buffer)์ ๋ฌธ์์ด์ด๋ ์ธ์คํด์ค๋ฅผ ๋ฐํํด์ผ ํฉ๋๋ค.
  // ArrayBuffer, FormData ๋๋ Stream ํค๋ ๊ฐ์ฒด๋ฅผ ์์ ํ  ์ ์์ต๋๋ค.
  transformRequest: [function (data, headers) {
    // ๋ฐ์ดํฐ ๋ณํ ์ํ ํ, ๋ฐํ
    // ...
    return data;
  }],

  // `transformResponse`๋ ์๋ตํ  ๋ฐ์ดํฐ์ ๋ํ ๋ณ๊ฒฝ์ ์ ๋ฌํด
  // then/catch์ ์ ๋ฌํ๋๋ก ํ์ฉํฉ๋๋ค.
  transformResponse: [function (data) {
    // ๋ฐ์ดํฐ ๋ณํ ์ํ ํ, ๋ฐํ
    // ...
    return data;
  }],

  // `headers`๋ ์๋ฒ์ ์ ์ก ๋  ์ฌ์ฉ์ ์ ์ ํค๋ ์๋๋ค.
  headers: { 'X-Requested-With': 'XMLHttpRequest' },

  // `params`๋ ์์ฒญ๊ณผ ํจ๊ป ์ ์ก ๋  URL ๋งค๊ฐ ๋ณ์์๋๋ค.
  // ์ผ๋ฐ ๊ฐ์ฒด ์ด๊ฑฐ๋ URLSearchParams ๊ฐ์ฒด์ฌ์ผ ํฉ๋๋ค.
  params: {
    ID: 12345
  },

  // `paramsSerializer`๋`params`๋ฅผ ์ง๋ ฌํ(serializing) ํ๋ ์ต์ ํจ์์๋๋ค.
  // (์: https://www.npmjs.com/package/qs, http://api.jquery.com/jquery.param/)
  paramsSerializer: function (params) {
    return Qs.stringify(params, {arrayFormat: 'brackets'})
  },

  // `data`๋ ์์ฒญ ๋ณธ๋ฌธ(request body)์ผ๋ก ์ ์กํ  ๋ฐ์ดํฐ์๋๋ค.
  // 'PUT', 'POST' ๋ฐ 'PATCH' ์์ฒญ ๋ฉ์๋์๋ง ์ ์ฉ ๊ฐ๋ฅํฉ๋๋ค.
  // 'transformRequest`๊ฐ ์ค์ ๋์ง ์์ ๊ฒฝ์ฐ ๋ค์ ์ ํ ์ค ํ๋์ฌ์ผ ํฉ๋๋ค.
  // - [ string, plain object, ArrayBuffer, ArrayBufferView, URLSearchParams ]
  // - ๋ธ๋ผ์ฐ์  ์ ์ฉ: FormData, File, Blob
  // - Node.js ์ ์ฉ: Stream, Buffer
  data: {
    firstName: 'Fred'
  },

  // `timeout`์ ์์ฒญ์ด ํ์ ์์๋๋ ๋ฐ๋ฆฌ ์ด(ms)๋ฅผ ์ค์ ํฉ๋๋ค.
  // ์์ฒญ์ด`timeout` ์ค์  ์๊ฐ๋ณด๋ค ์ง์ฐ๋  ๊ฒฝ์ฐ, ์์ฒญ์ ์ค๋จ๋ฉ๋๋ค.
  timeout: 1000, // ๊ธฐ๋ณธ ๊ฐ: `0` (ํ์์์ ์์)

  // ํ์ค CORS์์ฒญ์ ๊ธฐ๋ณธ์ ์ผ๋ก ์ฟ ํค๋ฅผ ์ค์ ํ๊ฑฐ๋ ๋ณด๋ผ ์ ์๊ธฐ ๋๋ฌธ์ ํ๋ก ํธ์์ withCredentials๋ถ๋ถ์ true๋ก ํด์ ์๋์ผ๋ก CORS ์์ฒญ์ ์ฟ ํค๊ฐ์ ๋ฃ์ด์ค์ผ ํ๋ค.
  withCredentials: false, // ๊ธฐ๋ณธ ๊ฐ

  // `adapter`๋ ํ์คํธ๋ฅผ ๋ณด๋ค ์ฝ๊ฒ ํด์ฃผ๋ ์ปค์คํ ํธ๋ค๋ง ์์ฒญ์ ํ์ฉํฉ๋๋ค.
  // ์ ํจํ ์๋ต(Promise)์ ๋ฐํํด์ผ ํฉ๋๋ค. (lib/adapters/README.md ์ฐธ๊ณ ).
  adapter: function (config) {
    // ...
  },

  // `auth`๋ HTTP ๊ธฐ๋ณธ ์ธ์ฆ(auth)์ด ์ฌ์ฉ๋๋ฉฐ, ์๊ฒฉ ์ฆ๋ช(credentials)์ ์ ๊ณตํจ์ ๋ํ๋๋๋ค.
  // ๊ธฐ์กด์ `Authorization` ์ปค์คํ ํค๋๋ฅผ ๋ฎ์ด์ฐ๋ `Authorization` ํค๋(header)๋ฅผ ์ค์ ํฉ๋๋ค.
  auth: {
    username: 'janedoe',
    password: 's00pers3cret'
  },

  // `responseType`์ ์๋ฒ์์ ์๋ตํ  ๋ฐ์ดํฐ ํ์์ ์ค์ ํฉ๋๋ค.
  // [ 'arraybuffer', 'blob', 'document', 'json', 'text', 'stream' ]
  responseType: 'json', // ๊ธฐ๋ณธ ๊ฐ

  // `responseEncoding`์ ์๋ต ๋์ฝ๋ฉ์ ์ฌ์ฉํ  ์ธ์ฝ๋ฉ์ ๋ํ๋๋๋ค.
  // [์ฃผ์!] ํด๋ผ์ด์ธํธ ์ฌ์ด๋ ์์ฒญ ๋๋ `responseType`์ด 'stream'์ธ ๊ฒฝ์ฐ๋ ๋ฌด์ํฉ๋๋ค.
  responseEncoding: 'utf8', // ๊ธฐ๋ณธ ๊ฐ

  // `xsrfCookieName`์ xsrf ํ ํฐ(token)์ ๋ํ ๊ฐ์ผ๋ก ์ฌ์ฉํ  ์ฟ ํค ์ด๋ฆ์๋๋ค.
  xsrfCookieName: 'XSRF-TOKEN', // ๊ธฐ๋ณธ ๊ฐ

  // `xsrfHeaderName`์ xsrf ํ ํฐ ๊ฐ์ ์ด๋ฐํ๋ HTTP ํค๋ ์ด๋ฆ์๋๋ค.
  xsrfHeaderName: 'X-XSRF-TOKEN', // ๊ธฐ๋ณธ ๊ฐ

  // `onUploadProgress`๋ ์๋ก๋ ํ๋ก๊ทธ๋์ค ์ด๋ฒคํธ๋ฅผ ์ฒ๋ฆฌํฉ๋๋ค.
  onUploadProgress: function (progressEvent) {
    // ๋ค์ดํฐ๋ธ ํ๋ก๊ทธ๋์ค ์ด๋ฒคํธ(Native Progress Event) ์ฒ๋ฆฌ ์ฝ๋
    // ...
  },

  // `onDownloadProgress`๋ ๋ค์ด๋ก๋ ํ๋ก๊ทธ๋์ค ์ด๋ฒคํธ๋ฅผ ์ฒ๋ฆฌํฉ๋๋ค.
  onDownloadProgress: function (progressEvent) {
    // ๋ค์ดํฐ๋ธ ํ๋ก๊ทธ๋์ค ์ด๋ฒคํธ(Native Progress Event) ์ฒ๋ฆฌ ์ฝ๋
    // ...
  },

  // `maxContentLength`๋ HTTP ์๋ต ์ฝํ์ธ ์ ์ต๋ ํฌ๊ธฐ๋ฅผ ๋ฐ์ดํธ(Bytes) ๋จ์๋ก ์ค์ ํฉ๋๋ค.
  maxContentLength: 2000,

 // `validateStatus`๋ ์ฃผ์ด์ง HTTP ์๋ต ์ํ ์ฝ๋์ ๋ํ ์ฝ์์ ํด๊ฒฐํ ์ง ๊ฑฐ์  ํ ์ง๋ฅผ ์ ์ํฉ๋๋ค.
 // `validateStatus`๊ฐ`true`๋ฅผ ๋ฐํํ๋ฉด (๋๋`null`,`undefined`) promise๋ฅผ resolve ํฉ๋๋ค.
 // ๊ทธ๋ ์ง ์์ผ๋ฉด promise๊ฐ reject ๋ฉ๋๋ค.
  validateStatus: function (status) {
    return status >= 200 && status < 300; // ๊ธฐ๋ณธ ๊ฐ
  },

  // `maxRedirects`๋ Node.js์์ ๋ฆฌ๋๋ ์ ๊ฐ๋ฅํ ์ต๋ ๊ฐฏ์๋ฅผ ์ ์ํฉ๋๋ค.
  // 0์ผ๋ก ์ค์ ํ๋ฉด ๋ฆฌ๋๋ ์์ด ์ํ๋์ง ์์ต๋๋ค.
  maxRedirects: 5, // ๊ธฐ๋ณธ ๊ฐ

  // `socketPath`๋ Node.js์์ ์ฌ์ฉ๋  UNIX ์์ผ์ ์ ์ํฉ๋๋ค.
  // ์: '/var/run/docker.sock'์ ์ฌ์ฉํ์ฌ docker ๋ฐ๋ชฌ์ ์์ฒญ์ ๋ณด๋๋๋ค.
  // `socketPath` ๋๋`proxy`๋ง์ด ์ง์  ๋  ์ ์์ต๋๋ค.
  // ๋ ๋ค ์ง์ ๋๋ฉด`socketPath`๊ฐ ์ฌ์ฉ๋ฉ๋๋ค.
  socketPath: null, // ๊ธฐ๋ณธ ๊ฐ

  // `httpAgent`์`httpsAgent`๋ ๊ฐ๊ฐ Node.js์์ http์ https ์์ฒญ์ ์ํ ํ  ๋
  // ์ฌ์ฉํ  ์ปค์คํ ์์ด์ ํธ๋ฅผ ์ ์ํฉ๋๋ค. ์ด๊ฒ์ ๊ธฐ๋ณธ์ ์ผ๋ก ํ์ฑํ๋์ง ์์ `keepAlive`์ ๊ฐ์
  // ์ต์์ ์ถ๊ฐ ํ  ์ ์๊ฒ ํฉ๋๋ค.
  httpAgent: new http.Agent({ keepAlive: true }),
  httpsAgent: new https.Agent({ keepAlive: true }),

  // 'proxy'๋ ํ๋ก์ ์๋ฒ์ ํธ์คํธ ์ด๋ฆ๊ณผ ํฌํธ๋ฅผ ์ ์ํฉ๋๋ค.
  // ๊ธฐ์กด์ `http_proxy` ๋ฐ `https_proxy` ํ๊ฒฝ ๋ณ์๋ฅผ ์ฌ์ฉํ์ฌ ํ๋ก์๋ฅผ ์ ์ ํ  ์๋ ์์ต๋๋ค.
  // ํ๋ก์ ์ค์ ์ ํ๊ฒฝ ๋ณ์๋ฅผ ์ฌ์ฉํ๊ณ  ์๋ค๋ฉด `no_proxy` ํ๊ฒฝ ๋ณ์๋ฅผ ์ผํ๋ก ๊ตฌ๋ถ ๋ ๋๋ฉ์ธ ๋ชฉ๋ก์ผ๋ก
  // ์ ์ํ์ฌ ํ๋ก์ ํ  ํ์๊ฐ ์์ต๋๋ค.
  // ํ๊ฒฝ ๋ณ์๋ฅผ ๋ฌด์ํ๊ณ  ํ๋ก์๋ฅผ ์ฌ์ฉํ์ง ์์ผ๋ ค๋ฉด `false`๋ฅผ ์ค์ ํฉ๋๋ค.
  // `auth`๋ HTTP ๊ธฐ๋ณธ ์ธ์ฆ(Basic Auth)๋ฅผ ์ฌ์ฉํ์ฌ ํ๋ก์์ ์ฐ๊ฒฐํ๊ณ  ์๊ฒฉ ์ฆ๋ช์ ์ ๊ณตํด์ผ ํจ์ ๋ํ๋๋๋ค.
  // ๊ธฐ์กด์ `Proxy-Authorization` ์ปค์คํ ํค๋๋ฅผ ๋ฎ์ด์ฐ๋ `Proxy-Authorization` ํค๋(header)๋ฅผ ์ค์ ํฉ๋๋ค.
  proxy: {
    host: '127.0.0.1',
    port: 9000,
    auth: {
      username: 'mikeymike',
      password: 'rapunz3l'
    }
  },

  // `cancelToken`์ ์์ฒญ์ ์ทจ์ํ๋ ๋ฐ ์ฌ์ฉํ  ์ ์๋ ์ทจ์ ํ ํฐ์ ์ง์ ํฉ๋๋ค.
  // (์์ธํ ๋ด์ฉ์ ํด์ (Cancellation) ์น์ ์ฐธ์กฐ).
  cancelToken: new CancelToken(function (cancel) {
    // ...
  })

}
```

then์ ์ฌ์ฉํ๋ฉด ๋ค์๊ณผ ๊ฐ์ด ์๋ต์ ๋ฐ์ ์ ์๋ค.

```JS
axios.get('/user/12345').then(function(response) {
  console.log(response.data)
  console.log(response.status)
  console.log(response.statusText)
  console.log(response.headers)
  console.log(response.config)
})
```

## ์์ฃผ ๋ณผ config ์ต์

**header**

```js
// `headers`๋ ์๋ฒ์ ์ ์ก ๋  ์ฌ์ฉ์ ์ ์ ํค๋ ์๋๋ค.
headers: { 'X-Requested-With': 'XMLHttpRequest' }
```

**withCredentials**

```js
// ํ์ค CORS์์ฒญ์ ๊ธฐ๋ณธ์ ์ผ๋ก ์ฟ ํค๋ฅผ ์ค์ ํ๊ฑฐ๋ ๋ณด๋ผ ์ ์๊ธฐ ๋๋ฌธ์ ํ๋ก ํธ์์ withCredentials๋ถ๋ถ์ true๋ก ํด์ ์๋์ผ๋ก CORS ์์ฒญ์ ์ฟ ํค๊ฐ์ ๋ฃ์ด์ค์ผ ํ๋ค.

withCredentials: false, // ๊ธฐ๋ณธ ๊ฐ
```

**data**

```js
// `data`๋ ์์ฒญ ๋ณธ๋ฌธ(request body)์ผ๋ก ์ ์กํ  ๋ฐ์ดํฐ์๋๋ค.
// 'PUT', 'POST' ๋ฐ 'PATCH' ์์ฒญ ๋ฉ์๋์๋ง ์ ์ฉ ๊ฐ๋ฅํฉ๋๋ค.
// 'transformRequest`๊ฐ ์ค์ ๋์ง ์์ ๊ฒฝ์ฐ ๋ค์ ์ ํ ์ค ํ๋์ฌ์ผ ํฉ๋๋ค.
// - [ string, plain object, ArrayBuffer, ArrayBufferView, URLSearchParams ]
// - ๋ธ๋ผ์ฐ์  ์ ์ฉ: FormData, File, Blob
// - Node.js ์ ์ฉ: Stream, Buffer
data: {
  firstName: "Fred";
}
```

**baseUrl**

```js
// `url` ์์ฑ ๊ฐ์ด ์ ๋ URL์ด ์๋๋ผ๋ฉด, `url` ์์ `baseURL`์ด ๋ถ์ต๋๋ค.
// axios ์ธ์คํด์ค๊ฐ ์๋ URL์ ํด๋น ์ธ์คํด์ค์ ๋ฉ์๋์ ์ ๋ฌํ๋๋ก
// `baseURL`์ ์ค์ ํ๋ ๊ฒ์ด ํธ๋ฆฌ ํ  ์ โโ์์ต๋๋ค.
baseURL: 'https://some-domain.com/api/',
```

[config option ์์ธํ ์์๋ณด๊ธฐ](https://grepper.tistory.com/72)
