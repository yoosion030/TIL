# 자바스크립트 유용한 메소드 모음

## Number.isInteger()

Number.isInteger 메소드는 인수의 값이 정수인지 아닌지를 반환해줍니다.  
전달된 값이 정수이면 true 아니라면 NaN, Infinity와 같은 값은 모두 false를 반환합니다.

```JS
Number.isInteger(0); // true
Number.isInteger(0.1); // false
Number.isInteger("문자열"); // false
Number.isInteger(true); // false
Number.isInteger(Infinity); // false
```

## Math.sqrt()

sqrt 메소드는 특정숫자의 제곱근 값을 계산해줍니다. 쉽게말해 루트값을 구하는 것입니다.

```JS
Math.sqrt(4); // 2
Math.sqrt(16); // 4
Math.sqrt(-1); // NaN
Math.sqrt(2); // 1.424~~~
```

## Math.pow()

pow 메소드는 제곱값을 반환해줍니다.

```JS
Math.pow(base, exponent)
```
base : 밑 값 (기준값)  
exponent : base값을 제곱하기 위해 사용하는 지수

```JS
Math.pow(7, 2); // 49
Math.pow(7, 3); // 343
Math.pow(4, 0.5) // 2
Math.pow(7, -2); // 0.02040816326530612 (1/49)
Math.pow(-7, 1/3); 	// NaN
```
