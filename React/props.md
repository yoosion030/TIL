# Props 가 뭔데?

## 정의

- 부모 컴포넌트가 자식 컴포넌트에게 넘겨준 데이터와 기능 등을 의미함
- 컴포넌트에게 값을 전달할 때 이용하는 것

## ⭐사용방법⭐

App 이라는 컴포넌트 안에 \<Hello>라는 컴포넌트를 만들어 보았습니다.  
( App은 부모 컴포넌트, Hello는 자식 컴포넌트 )

---

자식 컴포넌트가 부모 컴포넌트 안에 있던 `state`를 쓰고 싶을 때는 `props`를 사용해야 합니다.  
그럴 땐 `{ 부모에 있던 state이름 }` 이렇게 쓰면 안되고,
`props`라는 문법으로 `state`를 전송한 뒤에 `{ props.state이름 } `이렇게 써야합니다.

```JSX
function App (){
  let [name,setName] = useState(['유시온','유시지','유시현']);
  return (
    <div>
        <Hello name={name} />
    </div>
  )
}

function Hello(props){
  return (
    <div>
      <h2> Hello, { props.name[0]} <h2>
    </div>
  )
}
```

결과  
`Hello, 유시온`

---

**1. `<자식컴포넌트 전송할이름={state명}>` 이렇게 사용해주신 후**  
**2. 자식컴포넌트 선언하는 function 안에 파라미터를 하나 만들어주면 됩니다.**  
**3. `props.전송할 이름` 이렇게 쓰면 전송된 props를 사용할 수 있습니다.**

## children

```js
<Title title="고양이 가라사대">
```

props로 title을 넘기는 것 보다

```js
<Title>고양이 가라사대</Title>
```

이렇게 자식 요소를 넘기고 싶으면 어떻게 할까?

```js
const Title = (props) => {
  console.log(props);
  return <h1>음</h1>;
};
```

일단 props를 console에 찍어보면 Object가 찍힌다.
Object에는 children 이라는 key 값과 자식으로 넘겨준 '고양이 가라사대'가 value값에 있는 것을 볼 수 있다!

그렇다면

```js
const Title = (props) => {
  return <h1>{props.children}</h1>;
};
```

props.children에 접근하면 우리가 원하던 대로 '고양이 가라사대'가 보여질 것이다

## 구조분해할당

구조분해할당 문법을 이용하면 더 보기 쉽게 props에 접근할 수 있다.

아까 children 예제에 구조분해할당을 적용시킨다면

```js
const Title = ({ children }) => {
  return <h1>{children}</h1>;
};
```

함수 인자에 `{ 객체배열 key값 }`을 넣어준다면 props.key값 이렇게 접근하지 않고 바로 접근할 수 있어 보기에도 편리하다!
