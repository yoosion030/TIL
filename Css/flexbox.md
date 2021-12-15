# FlexBox
- 주축 : flex-direction 속성을 사용하여 지정함
- 교차축 : 주축의 수직인 축

## 주축
flex-decoration 으로 속성 지정
> - row ( 기본값 )
> - row-reverse
> - column
> - column-reverse

## row / row-reverse
> 주축은 인라인 방향 ( 가로 )으로 행을 따름

## column, column-reverse
> 주축은 하단으로 블록 방향 ( 세로 )을 따름

## 속성

flex-decoration 
> 정렬할 방향을 지정












flex-wrap 
> 컨테이너가 더 이상 아이템들을 한 줄에 담을 여유 공간이 없을 때 아이템 줄바꿈을 어떻게 할지 결정하는 속성

flex-flow 
> flex-decoration flex-wrap;

justify-content
> 중심축에서 아이템을 어떻게 배치할지 결정함

align-items 
> 교차축에서 어떻게 배치할지 결정함

align-content
> flex-wrap: wrap;이 설정된 상태에서 아이템들의 행이 2줄 이상 되었을 때의 수직축 방향 정렬을 결정하는 속성


align-self
> 지정된 align-items 값을 무시하고 교차축 상에서 정렬함

flex-grow   
> flex-basis는 Flex 아이템의 기본 크기를 설정함 ( flex-direction이 row일 때는 너비, column일 때는 높이 )

flex-basis 
> 아이템이 flex-basis의 값보다 커질 수 있는지를 결정하는 속성

flex-shrink 
> 아이템이 flex-basis의 값보다 작아질 수 있는지를 결정함 

order
> flex 요소의 순서 지정함. order의 기본값은 0이며 숫자가 커질수록 요소의 순서가 뒤로감.

z-index
> z-index로 Z축 정렬함. 숫자가 클 수록 위로 올라옵니다.
