# 리액트의 Hooks 완벽 정복하기

## 1. useState

usetState는 가장 기본적인 Hook으로 함수형 컴포넌트에서도 가변적인 상태를 지니고 있을 수 잇게 해준다.

useState를 사용할 땐 코드의 상단에 `import`구문을 통하여 불러오고 다음과 같이 사용한다.

```JS
import useState from 'react';

const [value, setValue] = useState(0);
```

이 함수의 파라미터에는 상태의 기본값을 넣어준다. 이 함수가 호출되고 나면 배열들 반환하는데, 그 배열의 첫번째 원소는 상태값이고, 두번째 원소는 상태를 설정하는 함수이다. 이 함수에 파라미터를 넣어서 호출하게되면 전달받은 파라미터로 값이 바뀌게 되고 컴포넌트는 정상적으로 리렌더링된다.

## 2. useEffect

useEffect는 리액트 컴포넌트가 렌더링 될때마다 특정 작업을 수행하도록 설정할 수 있는 Hook이다. 클래스형 컴포넌트의 componentDidMount 와 componentDidUpdate 를 합친 형태로 보아도 무방하다.

### 2.1 마운트 될 때만 실행하고 싶을 때

만약 컴포넌트가 화면에 가장 처음 렌더링 될 때만 실행되고 업데이트할 경우 실행할 필요가 없을 때 함수의 두번째 파라미터로 비어있는 배열을 넣어주면 된다.

```JS
useEffect(()=> {
    console.log('마운트 될 때만 실행됩니다.')
},[])
```

컴포넌트가 처음 나타날 때만 실행되고 그 이후에는 콘솔에 문구가 나타나지 않는다.

### 2.2 특정 값이 업데이트 될 때만 실행하고 싶을 때

```JS
componentDidUpdate(prevProps, prevState) {
  if (prevProps.value !== this.props.value) {
    doSomething();
  }
}
```

위 코드에서는 props 안에 들어있는 value값이 바뀔 때에만 특정 작업을 수행하도록 한다. 만약 이러한 작업을 useEffect에서 해야한다면 두번째 파라미터로 전달되는 배열안에 검사하고 싶은 값을 넣어주면 된다.

```JS
 useEffect(() => {
    console.log(value);
  }, [value]);
```
