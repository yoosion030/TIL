# pre-rendering

React는 기본적으로 CSR(Client Side Rendering) 방식이다.

**1.자바스크립트 불러오기 -> 2.js가 HTML을 구성**

정적인 HTML보다 SEO(Search Engine Optimization)가 약하다.
검색엔진 크롤러가 URL로 접근해도 자바스크립트를 받기 전까지 HTML 내용을 알 수 없기 때문이다.

## Pre-rendering

SSR을 쓰면 접속 시 검색엔진에 유의미한 HTML문서를 바로 받아올 수 있다.
클라이언트에 보내주기 전에 이미 완성된 HTML문서를 보내준다.
이를 NextJS에서는 pre-rendering이라고 한다.

**1.HTML 불러와 화면 구성 -> 2.JS 불러와 기능추가**

정적인 HTML 문서를 바로 받을 수 있어 SEO에 유리하다. 다만 사용자가 HTML문서만 다운 받은 뒤 클릭 등의 조작을 할 수 있도록 기본적인 인터렉션을 위한 자바스크립트의 내용이 미니멀하게 HTML문서에 포함된다. 그 다음으로 자바스크립트 다운로드가 완료되고 나서야 컴포넌트 변경 등의 인터렉션을 수행할 수 있다.

NextJS에서 pre-rendering을 두가지 방식으로 할 수 있다.

- Static Generation
- Server-side Rendering

## Static Genderation

Static Genderation은 대부분 사용되는 방식으로 빌드할 때 HTML문서를 만들어 둔다. 그리하여 사용자가 페이지를 요청할 때마다 이 HTML 문서를 보내주게 된다. 만들어진 문서를 보내는 것이기 때문에 속도가 빠르다는 장점이 있다.

## Server Side Rendering

사용자의 요청을 받았을 때마다 HTML문서를 새로 생성해서 보내주는 방식이다. 페이지의 내용이 매번 바뀌거나 자주 업데이트가 되는 경우 사용하는 것이 좋다.
