# var, let, const의 차이점은 무엇일까 🙄❓

## 스코프( Scope )

>     함수 레벨 스코프 : var
>     블록 레벨 스코프 : let, const
>
> [더 자세한 내용](https://github.com/yoosion030/TIL/blob/master/JavaScript/scope.md)

## 중복 이름 ( Duplicate Name )

var 키워드는 중복 이름을 사용하여 변수를 선언하는 것을 허용함

```js
var name = "Yoosion";
console.log(name); // Yoosion
var name = "blahblah"; // 중복 선언 허용!!
console.log(name); // blahblah
```

let과 const는 중복 이름을 사용하면 SyntaxError가 발생한다.

```js
let name = "Yoosion";
console.log(name); // Yoosion
let name = "blahblah"; // 중복 선언 xx
console.log(name); // SyntaxError: Identifier 'name' has already been declared

const name = "Yoosion";
const name = "blahblah";
console.log(name); // SyntaxError: Identifier 'name' has already been declared
```

>      중복 이름 사용 가능 : var
>      중복 이름 사용 x : let/const

## 초기화 ( Initialization )

```js
const a;	 // SyntaxError: Missing initializer in const declaration
console.log(a);
a = 1;
console.log(a);
```

>      var,let : 초기 값이 없어도 됨
>      const : 생성과 동시에 초기 값을 지정해 주어야 함

## 재할당 ( Reallocation )

const는 재할당하면 에러가 발생한다.

```js
const a = 1;
a = 2; // TypeError: Assignment to constant variable.
console.log(a);
```

⭐ 예외적으로 const로 선언된 변수 값의 재 할당은 불가능하지만, 객체 내의 프로퍼티 값은 수정할 수 있다. ⭐

```js
const a = { age: 10 };
a.age = 20;
console.log(a.age); // 20
```

>       변수( 재할당 o ) : var/let
>       상수( 재할당 x ) : const
