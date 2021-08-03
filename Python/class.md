# 클래스

## 선언
``` python
class 클래스명 :
    변수명 = 값
    변수명 = 값
    def 함수명( self, 전달값_변수명, ...) :
        코드1
        코드2
```


### 예시
``` python
class robot:
  name = "robot"
  age = 0
    def __init__(self, name, age):
        print('생성자 호출!')
        self.name = name
        self.age = age
    def __del__(self):  
        print('소멸자 호출!')
    def info(self):
        print('나의 이름은', self.name, '입니다!')
        print('나이는', self.age, '입니다!')
```
### __init__함수
- 객체가 만들어질 때 호출되는 함수
- 객체를 초기화할 때 자주 사용됨
### __del__함수
- 객체가 사랄질 때 호출되는 함수
### self
- 하나의 클래스에서 만들 여러 객체를 구별하기 위해 사용
- 전달값이 아닌 파이썬 내부에서 사용되는 약속된 값
- 함수 안에서 만든 변수가 아니라, 클래스에 속한 변수이기 때문에 self.변수명 이라고 표기해야함