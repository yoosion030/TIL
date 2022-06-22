# 데이터를 가져오기 위한 Suspense

```js
const ProfilePage = React.lazy(() => import("./ProfilePage")); // 지연 로딩

// 프로필을 불러오는 동안 스피너를 표시합니다
<Suspense fallback={<Spinner />}>
  <ProfilePage />
</Suspense>;
```

데이터를 가져오기 위한 Suspense는 `<Suspense>`를 사용하여 선언적으로 데이터를 비롯한 무엇이든 "기다릴" 수 있도록 해주는 새로운 기능입니다.

## Suspense가 정확히 무엇인가요?

Suspense를 사용하면 컴포넌트가 렌더링되기 전까지 기다릴 수 있습니다.

```js
const resource = fetchProfileData();

function ProfilePage() {
  return (
    <Suspense fallback={<h1>Loading profile...</h1>}>
      <ProfileDetails />
      <Suspense fallback={<h1>Loading posts...</h1>}>
        <ProfileTimeline />
      </Suspense>
    </Suspense>
  );
}

function ProfileDetails() {
  // 비록 아직 불러오기가 완료되지 않았겠지만, 사용자 정보 읽기를 시도합니다
  const user = resource.user.read();
  return <h1>{user.name}</h1>;
}

function ProfileTimeline() {
  // 비록 아직 불러오기가 완료되지 않았겠지만, 게시글 읽기를 시도합니다
  const posts = resource.posts.read();
  return (
    <ul>
      {posts.map((post) => (
        <li key={post.id}>{post.text}</li>
      ))}
    </ul>
  );
}
```

Suspense는 데이터 불러오기 라이브러리가 아닙니다. Suspense는 컴포넌트가 읽어들이고 있는 데이터가 아직 준비되지 않았다고 React에 알려줄 수 있는, **데이터 불러오기 라이브러리에서 사용할 수 있는 메커니즘**입니다.

이후에 React는 데이터가 준비되기를 기다렸다가 UI를 갱신할 수 있습니다.

### Suspense로 가능한 것

그렇다면 Suspense는 왜 사용하는 것일까요?

- **데이터 불러오기 라이브러리들이 React와 깊게 결합할 수 있도록 해줍니다.** 데이터 불러오기 라이브러리가 Suspense지원을 구현한다면, React 컴포넌트에서 이를 사용하는 것이 아주 자연스럽게 느껴질 것입니다.
- **의도적으로 설계된 로딩 상태를 조정할 수 있도록 해줍니다.** Suspense는 데이터가 어떻게 불러져야 하는지를 정하지 않고, 앱의 시각적인 로딩 단계를 밀접하게 통제할 수 있도록 해줍니다.
- **경쟁 상태를 피할 수 있도록 돕습니다.** `await`를 사용하더라도 비동기 코드는 종종 오류가 발생하기 쉽습니다. Suspense를 사용하면 데이터를 동기적으로 읽어오는 것처럼 느껴지게 해줍니다. 마치 이미 불러오기가 완료된 것처럼 말입니다.

## 오류 처리하기

프로미스를 사용하여 코드를 작성할 때, 오류를 처리하기 위하여 `catch()`를 사용했을 겁니다. Suspense를 사용할 때는 프로미스가 렌더링을 시작하길 기다리지 않는데, 이러한 오류 처리가 어떻게 이루어질까요?

Suspense를 사용하면, 불러오기에서 발생한 오류를 처리하는 것이 렌더링 오류를 처리하는 것과 동일한 방식으로 이루어집니다.

우선 프로젝트 전체에 걸쳐 사용할 오류 경계 컴포넌트를 아래와 같이 정의합니다.

```js
// 오류 경계는 현재 클래스 형태이어야 합니다.
class ErrorBoundary extends React.Component {
  state = { hasError: false, error: null };
  static getDerivedStateFromError(error) {
    return {
      hasError: true,
      error,
    };
  }
  render() {
    if (this.state.hasError) {
      return this.props.fallback;
    }
    return this.props.children;
  }
}
```

이제 오류 경계를 아래와 같이 트리 상의 오류를 잡아낼 곳 어디에든 배치하면 됩니다.

```js
function ProfilePage() {
  return (
    <Suspense fallback={<h1>Loading profile...</h1>}>
      <ProfileDetails />
      <ErrorBoundary fallback={<h2>Could not fetch posts.</h2>}>
        <Suspense fallback={<h1>Loading posts...</h1>}>
          <ProfileTimeline />
        </Suspense>
      </ErrorBoundary>
    </Suspense>
  );
}
```
