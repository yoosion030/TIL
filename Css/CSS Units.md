# CSS 단위

## 종류
**Ablsolute ( 절대적인 => 값이 정해져 있는 )**
- ⭐px⭐

**Relative ( 상대적인 )**
- em
- rem
- vh
- vh
- % 



## px
모니터 위에서 화면에 나타낼 수 있는 가장 작은 단위

단점
- 브라우저 화면의 크기가 변경되어도 컨텐츠가 그대로 고정된 값으로 유지됨
- 사용자가 브라우저에서 폰트 사이즈 설정을 바꿔도 전혀 반응하지 않음

## em
현재 지정된 폰트 사이즈를 나타내는 단위  
부모의 폰트 사이즈를 곱한 값

예제

--- 
```HTML
<div class="parent">
    Parent
    <div class="child">Child</div>
</div>
```
```CSS
.parent {
    font-size : 8em;
}
.child {
    font-size : 0.5em;
}
```
- ⭐브라우저의 기본 폰트 사이즈 크기는 16px임⭐
- parent > 8em : parent의 부모 요소인 즉 HTML의 폰트 사이즈 16px에서 8을 곱한 값 = 128px
- child > 0.5em : child의 부모 요소인 즉 parent의 폰트 사이즈 128px에서 0.5를 곱한 값 = 64px

## rem
rem = 'r'oot + em  
루트에 지정된 폰트 사이즈에 따라서 크기가 결정됨

예제

--- 
```HTML
<div class="parent">
    Parent
    <div class="child">Child</div>
</div>
```
```CSS
.parent {
    font-size : 8rem;
}
.child {
    font-size : 0.5rem;
}
```
- parent > 8em : root요소인 즉 HTML에서 기본적으로 지정된 16px에서 8을 곱한 값 = 124px
- child > 0.5em : root요소인 즉 HTML에서 기본적으로 지정된 16px에서 0.5를 곱한 값 = 8px


## em, rem

장점
- 브라우저에서 지정된 폰트 사이즈를 따라가기 때문에 브라우저 환경에서 폰트 사이즈를 변경하면 페이지에서도 반응적으로 폰트 사이즈가 변경이 됨


## viewport

**종류**
- vw ( viewport width )
- vh ( viewport height )

예제

---
`width : 100vw`  
`height : 100vh`

- 100vw : 브라우저의 너비 100%
- 100vh : 브라우저의 높이 100%


## %
부모 요소에 상대적으로 크기가 계산

예제

--- 
```HTML
<div class="parent">
    Parent
    <div class="child">Child</div>
</div>
```
```CSS
.parent {
    width : 500px;
}
.child {
    width : 50%;
}
```
- chile > 50% : child의 부모 요소인 즉 parent의 너비 크기인 500px에서의 50% = 250