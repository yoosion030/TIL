# 호이스팅( Hoisting ) 이란?
- 함수 안에 있는 선언들을 모두 끌어올려서 해당 함수 유효 범위의 최상단에 선언하는 것

## 호이스팅의 대상
- var 변수/함수의 선언만 위로 끌러 올려지며, 할당은 끌어 올려지지 않음
- let, const 는 호이스팅이 발생하지만 다른 방식으로 작동한다.

## 예시
## var
``` js
console.log(name);  // undefined
var name = 'Yoosion';
```
>name 변수 생성과 초기화가 console.log 이후에 이루어졌으니 에러가 발생할 것 같아 보이지만, undefined으로 출력이 된다.  

위 코드는 아래와 같은 의미를 가진다.
```js
var name;   // 선언부분만 끌어 올림
console.log(name);  // undefined
name = 'Yoosion';
```
> 이러한 현상이 호이스팅으로, 해당 변수가 상단으로 끌러올려져 **undefined**으로 초기값이 할당되는 것이다.


## let/const
```js
console.log(name); // ReferenceError
const name = 'Yoosion';
```
> var와 달리 에러를 발생시킨다. </br> 호이스팅이 발생하긴 하지만 값을 참조할 수 없어서 호이스팅이 발생하지 않는 것처럼 보이는 것이다.

### 호이스팅이 발생하는 것일까?🙄
```js
let a = 10; // 전역변수 a선언
 if(true){
    console.log(a); // 10 
 }
```
> let이 전역변수이기 때문에 a의 값 10을 if문 블럭에서 참조하여 출력하고 있다.

``` js
let a = 10; //전역변수 a 선언
if(true){
    console.log(a); // ReferenceError: a is not defined
    let a = 20; // 지역변수 a 선언
}
```
> ⭐전역변수가 있음에도 오류가 발생했기 때문에 호이스팅이 되었다는 것을 알 수 있다. </br> 지역변수가 전역변수보다 우선 순위를 갖기 때문에 호이스팅이 된 것이다.⭐

