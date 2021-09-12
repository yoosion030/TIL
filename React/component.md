# 컴포넌트( Component )

## 정의
긴 HTML을 한 단어로 깔끔하게 치환해서 넣을 수 있는 문법

## 특징
- Component 이름을 지을 땐 보통 영어 대문자로 시작한다.
- `return()`안엔 태그들이 평행하게 여러 개가 들어갈 수 없다.


## 사용

``` JSX
function Modal(){
  return (
    <div className="modal">
        <p>모달 창 입니다.</p>
    </div>
  )
}
```

1. function을 이용해서 함수를 하나 만든다.
2. 그 함수 안에 있는 `return()` 안에 HTML을 담는다.
3. 원하는 곳에서 `<Modal></Modal>` 이라고 쓰면 `return()` 안에 있는 HTML이 등장한다.



## Component를 사용해야 할 때❓❗
- 사이트에 반복해서 출현하는 HTML 부분
- 내용이 자주 변경될 것 같은 HTML 부분
- 다른 페이지를 만들고 싶을 때 그 페이지의 HTML 내용
- 다른 팀원과 협업할 때 웹 페이지를 컴포넌트 단위로 나눠서 작업을 분배
> 함수 문법 쓰는 것 처럼 생각하면 됨