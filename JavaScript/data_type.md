# 자료형

## boolean
- 참/거짓을 표현하기 위해 사용
- 조건문에 주로 쓰임
``` javascript
let boolean = true;
let boolean = false;
```

## null
- 의도적으로 빈 값을 넣고 싶을 때 사용
- 개발자가 명시적으로 지정해 준다는 점에서 undefined과 차이가 있음
``` javascript
let value = null;
console.log(value);
```
출력결과
> null
## undefined
- 아예 값이 지정되지 않았다는 것을 뜻함
- 변수가 선언되었으나 초기값이 주어지지 않았을 때 undifined값을 가지게 됨
``` javascript
let value;
console.log(value);
```
출력결과
> undefined
## number
- 말 그대로 숫자 !!
- 정수형 실수형 등으로 숫자를 나누지 않고 number형 하나로 표현
## string
- 문자열
- 변수에 문자열 값을 넣을 때에는 꼭 따옴표로 감싸주어야 함
``` javascript
let value = 'string';
```
## object
- 변수 object이름 = { property : 값};
- 여러 개의 변수를 하나로 묶어서 관리할 수 있는 형태

### typeof : 변수나 값의 타입을 알아내기 위한 키워드
``` javascript
let value = 'string';
console.log(typeof value);
let boolean = true;
console.log(typeof boolean);
let num = 123;
console.log(typeof num);
```
출력결과 
> string   
> boolean  
> number