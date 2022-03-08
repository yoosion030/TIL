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

## parseInt()

parseInt 메소드는 문자를 숫자로 변경합니다.
**만약, string의 첫 글자를 정수로 변경할 수 없으면 Nan값을 리턴한다.**

```JS
parseInt("-10"); // -10
```

문자열 "-10"을 숫자로 변환하여 정수 음수 -10을 리턴합니다.

```JS
parseInt("10n"); // 10
parseInt("10nnn13"); // 10
```

문자열의 첫 글자가 숫자이고, 그 이후에 숫자가 아닌 다른 문자열이 나올 경우 **숫자가 아닌 문자 이후의 값은 무시하고, 그 이전의 숫자만 정수로 변환합니다.**

```JS
parseInt("10.9"); // 10
```

문자열 타입의 실수값은 소수점을 제거한 후, 정수값만 리턴합니다.

```JS
parseInt("k10"); // NaN
```

문자열의 첫글자가 숫자가 아니면, NaN(Not a Number)를 리턴합니다.

```JS
parseInt("    10"); // 10
```

문자열의 첫글자는 반드시 숫자여야 하지만, 처음에 오는 공백 문자는 허용됩니다.

```JS
parseInt("10      "); // 10
```

문자열의 첫글자가 숫자이면, 뒤에 오는 공백은 무시됩니다.

## join()

```JS
arr.join(separator)
```

join 메소드는 배열의 모든 값들을 연결한 문자열을 리턴합니다.  
이때 각각의 값들 사이에는 파라미터로 입력된 구분자(separator)가 들어가게 됩니다.  
**만약, separator를 입력하지 않은 경우, default로 ','가 들어갑니다.**

```JS
const arr = ['Apple', 'Banana', 'Orange'];
const str1 = arr.join(); // "Apple, Banana, Orange"
```

파라미터에 아무 값이 안들어있기 때문에 ','로 연결됩니다.

```JS
const str2 = arr.join('-'); // "Apple-Banana-Orange"
```

```JS
const str3 = arr.join(''); // "AppleBananaOrange"
```

## toString()

toString 메소드는 배열을 표현하는 문자열을 리턴합니다.

```JS
const arr = ['Apple', 'Banana', 'Orange'];
arr.toString(); // "Apple,Banana,Orange"
```
