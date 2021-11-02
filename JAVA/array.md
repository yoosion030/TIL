# 배열
> 같은 타입의 여러 변수를 하나의 묶음으로 다루는 것

## 배열의 선언
`타입 [] 변수이름;` -> 배열 선언  
`변수이름 = new 타입[길이];` -> 배열 생성

```JAVA
int[] score;
score = new int[5];
```

`타입[] 변수이름 = new int[5];`
``` JAVA
int[] score = new int[5];
```

---

**초기화**
``` JAVA
int[] score;
score = new int[]{100, 100, 100};
```

```JAVA
int[] score = new int[]{100, 100, 100}; // 선언과 생성을 동시에
int[] score = {100, 100, 100}; // new int[] 생략 가능
```



**❌생성이 안되는 경우❌**

1. 선언과 동시에 배열 크기를 지정해주는 경우
```JAVA
int score[5];
```
2. new 연신자를 이용하지 않고 값을 지정해주는 경우
``` JAVA
int[] score;
score = {100, 100, 100}; // new int[] 생략 X
```



## 이차원 배열 선언

`타입[][] 변수이름;`

``` JAVA
int[][] score = new int[4][3]; //4행 3열
```

**초기화**

```JAVA
int[][] arr = new int[][]{{1, 2, 3}, {4, 5, 6}};
int[][] arr = {{1, 2, 3}, {4, 5, 6}}; // new int[][] 생략 가능
```


## 객체의 배열

**예시**
``` JAVA
Ball[] balls = new Ball[5];
```





