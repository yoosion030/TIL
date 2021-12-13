# React에서 import할 때 {} 중괄호 유무의 의미

```JS
import example1 from './components/example';
import { example2 } from './example';
```

이 두 코드의 차이점은 무엇일까? 바로 `import`할 때 `{}`의 유무가 다르다는 것이다. example 파일 둘 다 내가 직접 만든 파일인데 왜 `import`할 때 차이가 있을까?

**이유는 바로export 방식의 차이가 있기 때문이다.**

---

./components/example

```JS
export default example1;
```

./example

```JS
export example2;
```

`export`해줄 때 `default`를 붙이면 중괄호 `{}` 없이 `import`하지만,  
`default`없는 것을 `import`할 때에는 중괄호 안에 담아 해주어야한다.
