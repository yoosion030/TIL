# Blocking SSG

## 서론

만약 `/product/[id]`인 페이지에서 `getStaticProps`로 페이지를 미리 html 파일로 불러오고 싶으면 어떻게 할까?

## 해결 방법

그럴 때 `getStaticPaths`를 사용하면 된다. 하지만 `getStaticPaths`에서는 **paths**를 무조건 return 해줘야 하는데, 여기서 paths는 url로 무엇을 해줘야 하는지 지정해 주고 NextJS 에게 미리 페이지를 몇개를 만들어 달라는 말과 비슷하다.

paths가 정해지면 상관이 없지만, 사용자가 상품을 추가하고 상품의 상세 페이지인 `/product/[id]` 페이지가 있다고 하자. 그러면 사용자가 상품을 추가 했을 때 상세 페이지도 추가가 되는 것이니 페이지의 개수가 1개인지 10,000개인지 NextJS는 모른다. 이럴때는 어떻게 해줘야 하는가?

그래도 다 방법이 있다. paths를 return 해줄 때 빈 배열을 return 해주면 된다. 그러고 `fallblack`을 **"blocking"**으로 지정해주면 된다. blocking 작업은 딱 한번만 일어난다. 왜냐하면 첫 요청 이후에는 html 파일이 생기기 때문에 한번 더 작업해줄 필요가 없다.

## Blocking 과정

1. 사용자가 페이지 방문
2. 페이지가 `getStaticProps`와 **fallback blocking**이 있는 `getStaticPaths`를 가지고 있는지 확인한다.
3. 그 페이지에 첫번째로 방문한 사람은 NextJS가 HTML페이지가 있는지 확인할 때까지 조금 더 기다린다.
4. 이 요청은 한번만 실행이 되고, 그 다음부터는 더이상 페이지를 만들어내지 않는다.

```js
export const getStaticPaths: GetStaticPaths = () => {
  return {
    paths: [],
    fallback: "blocking",
  };
};
```

이러면 동적 url도 정적 페이지로 생성해줄 수 있다 !!
