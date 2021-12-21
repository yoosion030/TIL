# 12/21 useContext 사용과정

바야흐로 2021년 12월 21일 아이디어 페스티벌에서 useContext를 사용하였다.

어쩌다 사용하게 되었냐면 Start 페이지에서 로그인을 하고 User 페이지로 사용자 정보를 넘겨줘야 했다. Start컴포넌트랑 User 컴포넌트는 부모 자식 관계가 아니기 때문에 props를 사용하지 못하였다. 그래서 Context를 사용하게 되었다.

## 내 방식대로 설명하기

**Context/Data.js**

1. 먼저 Context로 넘겨줘야할 변수들을 따로 모아두고 싶어서 Context 폴더를 만들고 그 안에 Data라는 파일을 만듦
2. createContext, useContext를 import 해줌
3. Context 객체를 생성
4. 넘겨줄 값 선언
5. value에 그 값 넣기
6. 다른 컴포넌트에서 context를 사용할 때 쓰는 함수 생성 => useContext
7. 앞에서 객체 선언했던거.Provider value={value} props 넘기기

```JS
// context.js
import { createContext, useContext, useState } from 'react'

export const ResultContext = createContext(undefined)
// createContext 선언

export function ResultContextProvider({ children }) {
  const [data, setData] = useState({}) ////글로벌하게 관리할 state
  const value = {
    data,
    setData,
  }

  return (
    <ResultContext.Provider value={value}>{children}</ResultContext.Provider>
  )
}

export function useResultContext() {
  return useContext(ResultContext)
} //다른 컴포넌트에서 context를 사용할 때 쓰임.

```

**App.js**

1. Context를 import 해줘야함
2. 부모 컴포넌트에 감싸줘야함

```JS
import { Component } from 'react'
import { BrowserRouter, Route, Routes } from 'react-router-dom'
import { ResultContextProvider } from './Context/Data' //provider 불러오기

class App extends Component {


  render() {
    return (
      <div className="App">
        <ResultContextProvider>
          <BrowserRouter>
                 어쩌구 저쩌구
          </BrowserRouter>
        </ResultContextProvider>
      </div>
    )
  }
}

export default App

```

**Start.js**

1. Context import
2. useContext 불러오기

```JS
import React, { useState } from 'react'

import { useResultContext } from '../../Context/Data'
const Start = () => {

  const { data, setData } = useResultContext()

  const onSuccess = response => {
    const userData = {
      profileImage: response.profileObj.imageUrl,
      email: response.profileObj.email,
      name: response.profileObj.name,
    }
    setData(userData)
  }
}

export default Start

```

## Context 말고 useContext 적용시키기
