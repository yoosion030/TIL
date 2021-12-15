# class

## 정의 
- 어떠한 객체의 `변수`와 `메소드( method )`의 집합
- 동일한 속성과 행위를 수행하는 객체의 집합


## class 선언
``` JS 
class Person {
    //constructor
    constructor(name,age){
        //fields
        this.name = name;
        this.age = age;
    }

    //methods
    speak(){
        console.log(`${this.name} : hello!`);
    }
}

const sion = new Person('sion', 20);
sion.speak();   // sion : hello!
```

### constructor
- 클래스 몸체에서는 `constructor`가 생성자 역할을 한다.
- 인스턴스를 생성, 초기화하는 특수한 메서드( method ) 이므로 이름 변경이 불가능하다.
