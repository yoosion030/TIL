# JSX란(JavaScript eXtension)


## 소개
``` jsx
const element = <h1> Hello, world!</h1>;
```

위 코드는 JS도 아니고 HTML도 아닌 ⭐**JSX**⭐ 라는 문법이다 !! React와 함께 사용할 것은 권장한다.
## 정의
JSX는 자바스크립트 XML이다. 쉽게 말하자면 HTML 문법을 JavaScript 코드 내부에 쓴 것

> xml은 마크업 언어를 정의하기 위한 언어, 확장이 가능한 언어이다.

## JSX 문법

### 💻변수 사용
변수를 사용할 때는 중괄호 안에 넣어주어야 한다.
``` JSX
const name = 'Yoosion';
const hello = <h1>Hello, {name}</h1>
```
JSX의 중괄호 안에는 유효한 모든 `JS 표현식`을 넣을 수 있다.


### 💻className
HTML에서 class를 주고싶으면 `class=" "` class를 사용하면 되지만 JSX에서는 `className`을 사용해야 한다. 


### 💻닫힌 태그
HTML에서는 태그를 닫지 않는 경우가 있지만 JSX에서는 반드시 클로징 태그를 써야한다.

---  

HTML
```HTML
<input type = "text">
<br>
```
JSX

```JSX
</>
<input type = "text"/>
<br/>
```