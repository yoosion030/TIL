# 객체 ( Object ) 란?
> 여러 속성을 하나의 변수에 저장할 수 있도록 해주는 데이터 타입 ! </br> 이름과 값으로 구성된 프로퍼티의 정렬되지 않은 집합이다. </br> 프로퍼티의 값으로 함수가 올 수도 있는데, 이러한 프로퍼티를 메소드 라고 한다.
## 객체의 구성
- 객체는 0개 이상의 요소로 구성된 집합이다.
- 요소( property )는 키( key )와 값( value )으로 구성된다.
  

## 객체 생성 방식

## 1.객체 리터럴 방식
- 변수 이름 = { key : value, ...};
- key : value를 쉼표( , )로 구분하여 만듦
    ``` js
    const player = {
        name : 'sion;',
        fat : true,
    };
    console.log(player); // { name : 'sion', fat : true };
    ```

## 2.생성자 방식
- new Constructor() 방식으로 객체를 생성함

2-1. new Object()
- new 연산자를 통해 Object객체의 생성자함수를 호출함
    ``` js
    const player = new Object();
    player.name = 'sion';
    player['fat'] = true;

    console.log(player); // { name : 'sion', fat : true };
    ```
2-2. new 생성자()
- Number, String, Array 등의 내장 객체도 생성할 수 있음
    ``` js
    const player = new String('sion');
    console.log(player);    // [String: 'sion'];

    const arr = new Array([1,2,3]);
    console.log(arr);   // [[1, 2, 3]]
    ```
2-3. new 사용자 정의 생성자()
- 직접 생성자 함수를 만들어 객체를 생성할 수 있다.

## 3. Object.create() 방식
- 프로토타입 상속을 통해 객체를 만드는 방식임
- 프로토타입? 상속?