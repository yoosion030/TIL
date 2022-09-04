# display, visibility, opacity

## 1. display

display는 layout 정의에 자주 사용되는 중요한 속성이다.

- block
- inline
- inline-block
- none

### 1.1 block

- 항상 새로운 라인에서 시작
- 화면 크기 전체의 width를 차지(width: 100%)
- width, height, margin, padding 속성 지정 가능
- block 레벨 요소 내에 inline 레벨 요소를 포함할 수 있다.

### 1.2 inline

- 새로운 라인에서 시작하지 않는다. 즉, 줄을 바꾸지 않고 다른 요소와 함께 한 행에 위치할 수 있다.
- content 너비만큼 가로폭을 차지 한다.
- width, height, margin-top, margin-bottom 속성을 지정할 수 없다. 상/하 여백은 line-height로 지정한다.
- inline 레벨 요소 내에 block 레벨 요소를 포함할 수 없다. inline 레벨 요소는 일반적으로 block 레벨 요소에 포함되어 사용된다.

### 1.3 inline-block

block과 inline 요소의 특징 모두 갖는다. inline속성과 같이 한 줄에 표현되면서 width, height, margin 속성을 모두 지정할 수 있다.

- content의 너비만큼 가로폭을 차지한다.

### 1.4 none

해당 요소를 화면에 표시하지 않는다. (차지하는 공간조차 사라진다.)

## 2. visibility

- visible: 해당 요소를 보이게 한다.(default)
- hidden: 요소를 보이지 않게 한다. 하지만 `display: none`과 다르게, 해당 요소의 공간은 사라지지 않고 남아있게 된다.
- collapse: table 요소에 사용하며 행이나 열을 보이지 않게 한다.
- none: table요소의 row나 column을 보이지 않게 한다. IE, 파이어폭스에서만 동작하며 크롬에서는 `hidden`과 동일하게 동작한다.

## 3. opactiy

요소의 투명도를 정의한다. 0.0은 투명 1.0은 불투명을 의미한다.
