# 리액트의 Hooks 완벽 정복하기

## 훅이란?

"함수 컴포넌트에서 React state와 생명주기 기능을 **연동, 연결**해주는 함수", 클래스형 컴포넌트의 문제점들을 해결하기위해 나온 것이다.

### 종류

1. useState
2. useEffect
3. useContext
4. useRef
5. useMemo
6. useCallback
7. useReducer
8. useLmperativeHandle
9. useLayoutEffect
10. useDebugValue

### 클래스형 컴포넌트의 단점

- 클래스형 컴포넌트에서 로직을 재사용할 때 사용하는 고차컴포넌트, 렌더 속성값 패턴은 리액트 요소 트리를 깊게 만든다. 따라서 성능에 부정적인 영향과 개발 시 디버깅이 힘들어지는 문제점이 발생한다.
- 서로 연관성 없는 로직들을 하나의 생명주기에서 작성해야 하는 경우가 발생한다.
- `componentDidMount`와 `componentWillUnmount`, `comopnentDidMount`와 `componentDidUpdate`처럼 반복해서 작성해야 하는 코드 발생한다.
- JS의 클래스문법, `this`에 대한 이해가 필요해, `React의` 진입장벽을 높힌다.

### 훅의 장점

- 여러 훅기리 재조립이 가능하므로, 재사용 가능한 로직을 쉽게 만들 수 있다.
- 로직을 한 곳에 모을 수 있다.
- 훅은 단수한 함수이기 때문에 정적타입 언어에서도 타입을 쉽게 작성할 수 있다.
