# Intersection Observer - 요소의 가시성 관찰

Intersection Observer는 기본적으로 브라우저 뷰포트와 설정한 요소의 교차점을 관찰하며, 요소가 뷰포트에 포함되는지 아닌지 더 쉽게는 사용자 화면에 지금 보이는 요소인지 아닌지를 구별하는 기능을 제공합니다.

이 기능은 비동기적으로 실행되기 때문에, `scroll` 같은 이벤트 기반의 요소 관찰에서 발생하는 렌더링 성능이나 이벤트 연속 호출 같은 문제 없이 사용할 수 있습니다.

## IntersectionObserver

`new IntersectionObserver()`를 통해 생성한 인스턴스로 관찰자를 초기화하고 관찰할 대상을 지정합니다.
생성자는 2개의 인수 (`callback`, `options`)를 가집니다.

```js
const io = new IntersectionObserver(callback, options); // 관찰자 초기화
io.observe(element); // 관찰할 대상(요소) 등록
```

## callback

관찰할 대상이 등록되거나 가시성에 변화가 생기면 관찰자는 콜백을 실행합니다. 콜백은 2개의 인수 (`entries`, `observer`)를 가집니다.

```js
const io = new IntersectionObserver((entries, observer) => {}, options);
io.observe(element);
```

## entries

`entries`는 IntersectionObserverEntry 인스턴스의 **배열**입니다.
IntersectionObserverEntry는 읽기 전용(Read only)의 다음 속성들을 포함합니다.

- bounding ClientRect : 관찰 대상의 사각형 정보
- intersectionRect : 관찰 대상의 교차한 영역 정보
- intersectionRatio : 관찰 대상의 교차한 영역 백분율 (`intersectionRect` 영역에서 `boundingClientRect` 영역까지 비율, Number)
- isIntersecting : 관찰 대상의 교차 상태 (Boolean)
- rootBounds : 지정한 루트 요소의 사각형 정보
- target : 관찰 대상 요소
- time : 변경이 발생한 시간 정보

```js
const io = new IntersectionObserver((entries, observer) => {
  entries.forEach((entry) => {
    console.log(entry); // entry is 'IntersectionObserverEntry'
  });
}, options);

io.observe(element);
```

## Methods

### observe()

대상 요소의 관찰을 시작합니다.

```js
const io1 = new IntersectionObserver(callback, options);
const io2 = new IntersectionObserver(callback, options);

const div = document.querySelector("div");
const li = document.querySelector("li");
const h2 = document.querySelector("h2");

io1.observe(div); // DIV 요소 관찰
io2.observe(li); // LI 요소 관찰
io2.observe(h2); // h2 요소 관찰
```

### unobserve()

대상 요소의 관찰을 중지합니다.
관찰을 중지할 하나의 대상 요소를 인수로 지정해야 합니다.
단, IntersectionObserver 인스턴스가 관찰하고 있지 않은 대상 요소가 인수로 지정된 경우 아무런 동작도 하지 않습니다.

```js
const io1 = new IntersectionObserver(callback, options);
const io2 = new IntersectionObserver(callback, options);

// ...

io1.observe(div);
io2.observe(li);
io2.observe(h2);

io1.unobserve(h2); // nothing..
io2.unobserve(h2); // H2 요소 관찰 중지
```

콜백의 두 번째 인수 observer가 해당 인스턴스를 참조하므로, 다음과 같이 작성할 수도 있습니다.

```js
const io1 = new IntersectionObserver((entries, observer) => {
  entries.forEach((entry) => {
    // 가시성의 변화가 있으면 관찰 대상 전체에 대한 콜백이 실행되므로,
    // 관찰 대상의 교차 상태가 false일(보이지 않는) 경우 실행하지 않음.
    if (!entry.isIntersecting) {
      return;
    }
    // 관찰 대상의 교차 상태가 true일(보이는) 경우 실행.
    // ...

    // 위 실행을 처리하고(1회) 관찰 중지
    observer.unobserve(entry.target);
  });
}, options);
```

## 코딩애플 Intersection Observer 설명
