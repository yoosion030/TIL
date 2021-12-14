# 펼침 연산자 (spread operator)

## 정의

- 배열에 포함된 항목을 목록으로 바꿔주는 연산자이다.
- 마침표 세 개(...)로 표시한다.
- 펼침 연산자는 단독으로 쓰일 수 없다.
- 배열에 포함된 항목을 목록으로 바꿨다면 이를 배열이나 객체 등에 담아줘야한다. 볌수에 담게되면 에러가 발생한다.

```JS
const class1 = [1, 2, 3];

const a = ...class2; // X
const b = [...class2]; // O

```

## 장점

조작이나 부수효과로 인한 문제를 피할 수 있다. 또한, `push()`, `splice()`, `concat()`등의 배열 메소드를 외울 필요없이 간결하게 코드를 작성할 수 있다.

```JS
const class1 = [1, 2, 3];
const class2 = [4, 5, 6];

// concat()
const class3 = [...class1, ...class2];
console.log(class3); // [ 1, 2, 3, 4, 5, 6 ]

// push()
const class4 = [...class1, 7];
console.log(class4); // [ 1, 2, 3, 7 ]

// splice()
const class5 = [...class1.slice(0, 2)];
console.log(class5); // [ 1, 2 ]

```

이외에도 함수의 매개변수에 값을 전달할 때도 펼침 연산자를 사용하여 코드를 편하게 관리할 수 있다.  
아래는 펼침 연산자를 대신 인덱싱을 통해 매개변수에 값을 전달하는 경우이다.

```JS
const student = ['John', 19, 'A+'];
function introduce(name, age, grade) {
    console.log(`${name}(${age}) - ${grade}`);
}
introduce(student[0], student[1], student[2]); // John(19) - A+

```

이 경우 원본 배열이 변경되면 코드 또한 함께 고쳐야 한다는 단점이 있다.  
이를 펼침 연산자를 사용하면 다음과 같이 코드를 작성할 수 있다.

```JS
introduce(...student); // John(19) - A+
```
