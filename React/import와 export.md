# import와 export

ReactJS로 작업을 하다보면 컴포넌트가 점점 많아지게 되고 결국엔 하나의 파일을 두개의 파일로 분리를 해야하는 일이 생기게 된다. 그럴때 파일을 불러올 때에는 **import**를, 그 파일을 내보낼때에는 **export**를 사용한다.

## import ( 불러오기 ) 💨

```JS
import React from "react"
```

import는 ReactJS 라이브러리를 가져올 때 이미 사용하고 있다.

```JS
// sampleImport.js
import { fruits, sayHello, sayHi } from "sample1.js";
```

위 코드는 `sample1.js`에서 fruits, sayHello, sayHi를 가져오겠다는 의미이다.

```JS
import { 변수나 함수 } from '파일 경로';
```

필요로 하는 변수나 함수를 `import {...}` 괄호 안에 넣어 주면 된다. 그리고 `from`뒤에는 **파일경로**를 입력하면 된다.

++ 파일 확장자는 제거해도 된다.

++ node_modules에 설치된 모듈을 불러올 때에는 경로를 지정할 필요 없이 모듈 이름만 작성하면 된다.

## export ( 내보내기 ) 💨

```JS
// sample1.js
export const fruits = ["사과", "감", "배"];
export function sayHello() {
    console.log("hello");
}
export const sayHi = () => console.log("hi");
```

위 코드는 변수 `fruit` 그리고 함수 `sayHello()`와 `sayHi()`를 내보내겠다는 의미이다.

```JS
export 변수나 함수 ~~
```

내보내길 원하는 변수나 함수 앞에 `export`를 붙여주면 된다.

---

## import as

```JS
// sampleImport.js
import { fruits as fruitsName } from "sample1";
```

sample1에 있는 변수 `fruits`를 이 파일에서는 `fruitsName`으로 사용하겠다는 의미이다.

```JS
import { 원래 이름 as 바꿀 이름 } from '파일 경로';
```

불러올 함수나 변수의 **이름을 바꾸고 싶다면** `import`할 때 `as`라는 예약어를 사용하며 된다.

## import \*

```JS
//index.js
import React from 'react'
import * as S from './style'
const Section1 = () => {
  return (
    <S.MainSection>
        코드코드
    </S.MainSection>
  )
}

export default Section1
```

```JS
//style.js
import styled from 'styled-components'

export const MainSection = styled.div`
  height: 835px;
  background-color: #750606;
  margin-top: 70px;
`
```

```JS
import * as S from './style';
```

style.js에 있는 모든 것을 'S'라는 **객체에 담아 불러오겠다**는 의미이다. 그래서 `<S.MainSection></S.MainSection>` 컴포넌트를 사용하면 'S' 라는 객체 안에 있는 `MainSection`을 불러와 그 안에 있는 코드의 스타일을 적용해준다.

```JS
import * as 이름 from '파일경로';
```

가져올 사항이 많다면 `\*`를 이용해 **객체형태**로 불러올 수 있다.

## export defult

```JS
export default 변수나 함수;
```

```JS
import 변수나 함수 from '파일 경로';
```

변수나 함수를 **기본**으로 내보내겠다는 뜻이다. `default`로 내보내기를 하게 되면 `import`할 때 `{}`가 없어도 된다.
