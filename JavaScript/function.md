# ⭐함수⭐

## 1.함수 정의
- 함수 선언문
- 함수 표현식
- Function 생성자 함수

### 1-1.함수 선언문
``` JS
// 함수 선언문
function hello(name) {
  conols.log('hello '+name);
}
```

### 1-2.함수 선언식
- 무명의 리터럴로 표현이 가능하다.
- 변수나 자료 구조(객체, 배열…)에 저장할 수 있다.
- 함수의 파라미터로 전달할 수 있다.
- 반환값(return value)으로 사용할 수 있다.

``` JS
// 함수 표현식
var square = function(number) {
  return number * number;
};

// 기명 함수 표현식(named function expression)
var foo = function multiply(a, b) {
  return a * b;
};

// 익명 함수 표현식(anonymous function expression)
// 익명 함수 : 함수 표현식 방식으로 정의한 함수이며 함수명을 생략을 하는 함수
var bar = function(a, b) {
  return a * b;
};

console.log(foo(10, 5)); // 50
console.log(multiply(10, 5)); // Uncaught ReferenceError: multiply is not defined

// ⭐함수 호출시 함수명이 아니라 함수를 가리키는 변수명을 사용하여야 한다.⭐
```

### 1.3 Function 생성자 함수

``` JS
new Function(arg1, arg2, ... argN, functionBody)

var square = new Function('number', 'return number * number');
console.log(square(10)); // 100
``` 
- 일반적으로 사용하지 않음

---

## 사용
```JS
// 함수 선언
function functionName(){
    // 실행 내용
}

//함수 호출
functionName();
```

- ⭐하나의 함수는 한가지의 기능만 가져야 함⭐
- JS에서 함수는 Object임


