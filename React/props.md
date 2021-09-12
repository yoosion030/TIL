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



``` JSX
function App (){
  let[name,setName] = useState(['유시온','유시지','유시현']);
  return (
    <div>
        <Hello name={name}></Hello>
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

**1. `<자식컴포넌트 전송할이름={state명}>` 이렇게 사용해주신 후**  
**2. 자식컴포넌트 선언하는 function 안에 파라미터를 하나 만들어주면 된다.**  
**3. `props.전송할 이름` 이렇게 쓰면 전송된 props를 사용할 수 있다.**

