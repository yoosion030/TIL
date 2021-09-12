# 🎉EVENT🎉

React 에서도 HTML과 같은 이벤트를 사용합니다.  
> ex ) onclick, onchange, mouseover 등  

---

## 🎉HTML과 차이점

1. React의 이벤트는 소문자 대신 캐멀 케이스( camelCase )를 사용해야합니다. 
   - onclick = {} (x)
   - onClick = {} (o)

2.문자열이 아닌 함수로 전달합니다.
   - onclick = "함수이름()" (x)
   - onClick = {함수이름} (o)


HTML
``` HTML
<button onclick="activateLasers()">
  Activate Lasers
</button>
```
React
```JSX
<button onClick={activateLasers}>
  Activate Lasers
</button>
```

---

## 🎉주의할 점
**DOM 요소에만 이벤트 설정이 가능합니다.** `div`, `span`, `form`, `button` 등의 DOM 요소에는 이벤트 설정이 가능하지만, 리액트의 컴포넌트에는 불가능합니다.   

---

잘못된 코드
``` JSX
function App() {
  const sayHi = function () {
    alert('hello');
  }
  return (
    <>
      <Component onClick={sayHi}/>
    </>
  );
}
```

---

## 🎉preventDefault
React에서는 `false`를 반환해도 기본 동작을 방지할 수 없습니다.   
반드시 `preventDefault`를 명시적으로 호출해야 합니다. 
HTML
```HTML
<form onsubmit="console.log('You clicked submit.'); return false">
  <button type="submit">Submit</button>
</form>
```

React
``` JSX
function Form() {
  function handleSubmit(e) {
    e.preventDefault();
    console.log('You clicked submit.');
  }

  return (
    <form onSubmit={handleSubmit}>
      <button type="submit">Submit</button>
    </form>
  );
}
```
event를 인자로 받고, e.preventDefault()를 호출하면, 이벤트의 기본동작은 동작하지 않게 되고 console.log만 수행됩니다.



