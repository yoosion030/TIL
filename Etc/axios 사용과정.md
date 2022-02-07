# 1/4 axios 사용과정

이번 페스티벌 때 처음으로 서버와 통신을 하여 데이터를 주고받았다.

## 내맘대로 설명하기

**baseURL** 설정부터 하자

```JS
 useEffect(() => {
    axios
      .get(`http://192.168.0.32:8888/like/${googleId}`)
      .then(res => {
        setLiked(res.data)
      })
      .catch(err => console.log(err))
  }, [])
```

맨 처음 axios를 사용할 때에는 url 부분에 ip 주소와 함께 작성했다. 처음에는 상관이 없었는데 api 연동할 부분이 점점 많아지고 ip주소가 계속바뀌면서 변경할 부분이 많아 엄청 귀찮았다. 그래서 맨 처음에는 baseURL을 정의하여 기본 url을 지정해 ip주소가 바뀌면 그 baseURL만 바뀌게 해주어야한다.

```JS
// App.js

export const api = axios.create({
    baseURL:'http://192.168.0.32:8888'
})
```

```JS
// example.js
import api from './App.js'
api.get(~~~)
```

**post**

데이터를 보낼때는 post를 이용하면 된다.

```JSX

  function onSuccess(res) {
    // 로그인 성공 시 로그인 된 유저 정보를 보여줌
    api
      .post('/login', {
        googleId: res.profileObj.googleId,
        email: res.profileObj.email,
        name: res.profileObj.name,
        img: res.profileObj.imageUrl,
      })
      .then(function (res) {
        setIsLogin(true)
        setId(sessionStorage.getItem('googleId'))
        toast.success('로그인 성공')
        navigate('/Draw')
      })
      .catch(function (err) {
        console.log(err)
        toast.error('로그인 실패')
      })
  }

```

```
axios.post(url주소, {
  보낼 데이터
})
.then((res)=> {
  성공적으로 보낸 후 해야할 코드
}).catch((err)=> {
  오류가 났을 때 코드
})
```

**get**

데이터를 가져올 때는 get을 이용하면 된다.

```JSX
  // 모든 맵 조회
  useEffect(() => {
    api.get('/map').then(res => {
      setShared(res.data)
    }).catch(err=> {
      console.log(err)
    })
  }, [])
```

```
axios.post(url주소, {
  보낼 데이터
})
.then((res)=> {
  성공적으로 보낸 후 해야할 코드
}).catch((err)=> {
  오류가 났을 때 코드
})
```

저 위의 코드를 try catch 문을 이용하여 바꿀 수도 있다.


```JS
async funciton 어쩌구() {
  try {
    const res = await axios.get('/map')
    getShared(res.data);
  }
  catch (err) {
    console.log(err);
  }
}
```

아무튼 axios를 이용하여 쉽게 서버와 소통을 할 수 있어 무사히 프로젝트를 마칠 수 있었다.
