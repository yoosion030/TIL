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