# Element Rendering

## 정의
- Element는 React 에서의 가장 작은 단위이다.  
- Element는 컴포넌트의 구성요소 이다.
- Element는 사용자 화면에 표시하기 위한 내용을 기술한다.
- Rendering 이란 서버로 부터 HTML파일을 받아 브라우저에 뿌려주는 과정이다.

## ⏰DOM에 Element Rendering 하기
```HTML
<div id="root"></div>
```
- 이 안에 들어가는 모든 엘리먼트를 React DOM에서 관리
- 리액트 앱은 일반적으로 하나의 루트 돔 노드가 있음

React App에는 기본적으로 모든 Element를 React DOM에서 관리하기 때문에 이와같은 DOM을 루트(root) DOM 노드라고 부릅니다.  
React 엘리먼트를 루트 DOM 노드에 렌더링하려면 둘 다 ReactDOM.render()로 전달하면 됩니다.  

예제
``` JSX
const element = <h1>Hello, world</h1>;
ReactDOM.render(element, document.getElementById('root'));
```
결과  
`Hello, world`

## ⏰Rendering 된 Element 업데이트 하기
UI를 업데이트하는 유일한 방법  
-> 새로운 Element를 생성 후 이를 ReactDOM.render()로 전달함


## ⏰ 변경된 부분만 업데이트하기
React DOM은 해당 엘리먼트와 그 자식 엘리먼트를 이전의 엘리먼트와 비교하고 DOM을 원하는 상태로 만드는데 필요한 경우에만 DOM을 업데이트합니다.   
매초 전체 UI를 다시 그리도록 엘리먼트를 만들어도 React DOM은 내용이 변경된 텍스트 노드만 업데이트합니다.