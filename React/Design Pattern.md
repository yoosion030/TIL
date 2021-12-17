# Design Pattern

## 디자인 패턴이란?

소프트웨어 개발 방법으로 사용되는 디자인 패턴은 과거의 소프트웨어 개발 과정에서 발견된 설계의 노하우를 축적하여 그 방법에 이름을 붙여서 이후에 재사용하기 좋은 형태로 특정 규약을 만들어서 정리한 것이다. 디자인 패턴은 소프트웨어 설계에 있어 공통적인 문제들에 대한 표준적인 해법과 작명법을 제안하고, 알고리즘과 같이 프로그램 코드로 바로 변환될 수 있는 형태는 아니지만 특정한 상황에서 구조적인 문제를 해결하는 방식이다. 쉽게 말하자면 **"효율적인 코드를 만들기 위한 방법론"**이라고 생각하면 된다.

디자인 패턴을 외우기 보다는 어떠한 패턴이 있는지 알고 수많은 디자인 패턴에서 다양한 코딩 노하우를 습득하는 것이 중요하다. "이 코드에는 무조건 이 패턴을 적용시킬거야!"가 아니라 여러가지 패턴이 자연스럽게 코드에 녹아드는것이 좋다.

## 디자인 패턴의 종류

### 생성 패턴 (Creational Patterns)

객체 생성에 관련된 패턴이다. 객체의 생성과 조합을 캡슐화해 특정 객체가 생성되거나 변경되어도 프로그램 구조에 영향을 크게 받지 않도록 유연성을 제공한다.

**종류**

1. 싱글톤 패턴
2. 추상팩토리 패턴
3. 빌더 패턴
4. 팩토리 메서트 패턴
5. 원형 패턴

### 구조 패턴 (Structural Patterns)

클래스나 객체를 조합해 더 큰 구조를 만드는 패턴이다. 예를 들어 서로 다른 인터페이스를 지닌 2개의 객체를 묶어 단일 인터페이스를 제공하거나 서로 다른 객체들을 묶어 새로운 기능을 제공하는 패턴이다.

**종류**

1. 적응자 패턴
2. 브리지 패턴
3. 데코레이터 패턴
4. 퍼사드 패턴
5. 프록시 패턴

## 행위 패턴 (Behavioral Patterns)

객체나 클래스 사이의 알고리즘이나 책임 분배에 관련된 패턴입니다. 한 객체가 혼자 수행할 수 없는 작업을 여러개의 객체로 어떻게 분배하는지, 또 그렇게 하면서도 객체 사이의 결합도를 최소화하는 것에 중점을 두는 방식이다.

**종류**

1. 옵저버 패턴
2. 상태 패턴
3. 스트레이트지 패턴
4. 템플릿 패턴
5. 비지터 패턴
6. 역할 사슬 패턴
7. 커맨드 패턴
8. 인터프리터 패턴
9. 이터레이터 패턴
10. 미디에이터 패턴

---

# React 에서의 Design Pattern

## 1. Persentational and Container Component Pattern

> 데이터 처리와 데이터 출력을 분리하는 패턴이다.

### Container Components : how things work

- 컨테이너 컴포넌트에서는 주로 데이터 `fetch`가 이루어지게 된다.
  - Redux를 이용해 상태관리를 하게된다면 `dispatch`를 예로 들 수 있다.
- 연관이 있는 서브 컴포넌트를 렌더링한다.
- DOM Markup이나 스타일(css)이 없다.
- Presentational 또는 Container Components에 callback 함수나 데이터를 전달해 줄 수 있다.
- stateful한 경향을 가지고있는 컴포넌트이다.

### Presentational Components : how things look

> 화면에 보여지는 것만 담당하는 Components이다.

- DOM markup과 style(css)을 가지고 있다.
- props를 통해서 데이터나 callbacks를 받아올 수 있다.
- 뷰에 필요한 state를 가지고 있을 수 있다.
- state, lifecycle, Performance optimization이 필요한 경우가 아니면 Functional component로 작성한다.
- stateless한 경향을 가지고 있는 컴포넌트이다.

## 예시

**Container Component**

> 데이터를 Presenter Component에 전달해줌.

```JS
import React from "react";
import CommentList from "./CommentList";

class CommentListContainer extends React.Component {
  constructor() {
    super();
    this.state = { comments: [] };
  }

  componentDidMount() {
    fetch("/my-comments.json")
      .then(res => res.json())
      .then(comments => this.setState({ comments }));
  }

  render() {
    return <CommentList comments={this.state.comments} />;
  }
}
```

**Presenter Component**

> Container Component에서 받은 데이터를 보여줌

```JS
import React from "react";

const Commentlist = comments => (
  <ul>
    {comments.map(({ body, author }) => (
      <li>
        {body}-{author}
      </li>
    ))}
  </ul>
```

### 장점

1. **관심사의 분리를 더 잘할 수 있다.**
2. **재 사용성을 높일 수 있다.**
3. **Markup 작업이 편하다.**

## 2. Atomic Design Pattern

> 디자인 요소들을 나누어 파악하고 이 요소들이 조합되는 과정을 통해서 디자인을 구성하는 방식을 의미한다.

**구분**

- Atoms
- Molecules
- Organisms
- Templates
- Pages

### Atoms

> 하나의 구성요소. 보인 자체의 스타일만 가지고 있으며 다른 곳에 영향을 미치는 스타일은 적용되징 낳아야 한다. 원자는 from, label, input, button과 같은 basic html elements를 포함한다.

**예시**

```JS
const Button = ({ type = 'button', children = '' }) => (
  <button type={type}>{children}</button>   // 가장 기본이 되는 html 태그입니다.
)
```

### Molecules

> Atoms가 모여 만들어지는 하나의 구성요소. Atom 단위인 input, label, input, button을 함쳐 새로운 의미있는 단위를 만들 수 있다. 실제로 무언가 동작을 할 수 있게 된다.

### Organisms (유기체)

> 분자들의 모음. 비교적 복잡한 구조를 가지게 된다. 서로 동일하거나 다른 molecules(분자)로 구성될 수 있다. 유기체는 로고, 메인 네비게이션, 검색, 소셜 미디어 채널리스트와 같은 다양한 컴포넌트로 구성될 수 있다.

### Templates

> 유기체들을 모아 템플릿으로 생성, 스타일링에 집중한 단위. Templates의 중요한 특성을 페이지의 최종 내용보다는 페이지의 기본 내용 구조에 초점을 맞춘다는 것이다. ppt 템플릿 생각하면 될듯 ㅇㅇ

### Pages

> 실제 페이지를 구성. 페이지는 실제 대표적인 콘텐츠가 배치된 UI의 모습을 보여주는 템플릿의 특정 인스턴스이다.

Pages 단위에서 어플리케이션 상태관리가 이루어져야 하다.

하지만 분자, 유기체, 템플릿단위에서 컴포넌트를 위한 상태를 관리하는 것은 괜찮다.

## 디자인 패턴 적용해보기

**Presentational and Container Component Pattern**

페이지 내에서 후기, 클래스 소개 커리큘럼, 키트 소개, 크리에이터, 커뮤니티, 환불 정책, 추천 항목 별로 컴포넌트를 나눴다.

각 컴포넌트 별로 디렉토리를 생성하고 각 디렉토리 내부에는 로직을 담당하는 **Container**와 화면에 데이터를 보여주는 **Presenter** 그리고 스타일 파일로 나눠주었다.

프로젝트에서 전체 스타일링을 담당하는 `globalStyle`는 디렉토리에서 따로 고나리할 수 있도록 하였다.

상태관리는 담당하는 `store`디렉토리를 생성하고 그 안에 `reducers`, `sagas`디렉토리를 생성하여 구조를 잡았다.

자주 쓰이는 Header와 Footer는 `Common`디렉터리 안에 담았다.

```
.
└── src
    ├── @types  // 타입을 관리하는 곳
    │   ├── dataTypes.ts
    │   └── handlerTypes.ts
    ├── App.tsx
    ├── Modal
    │	├── ModalContainer.tsx
    │	├── ModalPresenter.tsx
    │	└── Modal.style.ts
    │
    ├── components
    │   ├── ClassInformation
    │   │   ├── ClassInformation.style.ts
    │   │   ├── ClassInformationContainer.tsx
    │   │   └── ClassInformationPresenter.tsx
    │   ├── Common
    │   │   ├── Footer
    │   │   │   ├── Footer.style.ts
    │   │   │   └── Footer.tsx
    │   │   └── Header
    │   │       ├── Header.style.ts
    │   │       └── Header.tsx
    │   ├── Community
    │   │   ├── Community.style.ts
    │   │   ├── CommunityContainer.tsx
    │   │   └── ContainerPresenter.tsx
    │   ├── Creator
    │   │   ├── Creator.style.ts
    │   │   ├── CreatorContainer.tsx
    │   │   └── CreatorPresenter.tsx
    │   ├── Curriculum
    │   │   ├── Curriculum.style.ts
    │   │   ├── CurriculumContainer.tsx
    │   │   └── CurriculumPresenter.tsx
    │   ├── Kit
    │   │   ├── Kit.style.ts
    │   │   ├── KitContainer.tsx
    │   │   └── KitPresenter.tsx
    │   ├── Recommend
    │   │   ├── Recommend.style.ts
    │   │   ├── RecommendCotainer.tsx
    │   │   └── RecommnedPresenter.tsx
    │   ├── RefundPolicy
    │   │   ├── RefundPolicy.style.ts
    │   │   ├── RefundPolicyContainer.tsx
    │   │   └── RefundPolicyPresenter.tsx
    │   ├── Review
    │   │   ├── Review.style.ts
    │   │   ├── ReviewContainer.tsx
    │   │   └── ReviewPresenter.tsx
    │   └── SideNavigationBar
    │       ├── SideNavigationBar.style.ts
    │       ├── SideNavigationBarContainer.tsx
    │       └── SideNavigationBarPresenter.tsx
    ├── api
    │   └── classInformation.ts
    ├── assets  // 이미지 파일 등 관리
    ├── data
    │   └── classInformation.json
    ├── globalStyle
    │   └── globalStyle.ts
    ├── index.tsx
    ├── react-app-env.d.ts
    └── store
        ├── reducers
        │   ├── ClassInformation.ts
        │   └── index.ts
        └── sagas
            ├── ClassInformation.ts
            └── index.ts

```

**Atomic Design Pattern**

atomic design pattern으로 프로젝트 설계하는게 시간이 더 오래걸리는 것 같다. atomic design pattern에서는 최소 단위은 atoms를 어떻게 구성을 해야할 지도 고려해봐야 하고 각 구조 단위를 사용하는 것이 효율적인지를 생각해봐야 한다.

```
.
└── src
    ├── @types
    │   ├── dataTypes.ts
    │   └── handlerTypes.ts
    ├── App.tsx
    ├── Modal
    │   ├── atoms
    │   ├── molecules
    │   ├── organisms
    │   └── templates
    ├── _components
    │   ├── UI
    │   │   ├── atoms
    │   │   │   ├── Button
    │   │   │   │   ├── Button.style.ts
    │   │   │   │   └── index.tsx
    │   │   │   ├── Icon
    │   │   │   │   ├── Icon.style.ts
    │   │   │   │   └── index.tsx
    │   │   │   ├── Image
    │   │   │   │   ├── Image.style.ts
    │   │   │   │   └── index.tsx
    │   │   │   ├── Input
    │   │   │   │   ├── Input.style.ts
    │   │   │   │   └── index.tsx
    │   │   │   ├── Text
    │   │   │   │   ├── Test.style.ts
    │   │   │   │   └── index.tsx
    │   │   │   └── index.ts
    │   │   ├── molecules
    │   │   │   ├── Banner
    │   │   │   │   ├── Banner.style.ts
    │   │   │   │   └── index.tsx
    │   │   │   ├── ClassIntroduceContent
    │   │   │   │   ├── ClassIntroduceContent.style.ts
    │   │   │   │   └── index.tsx
    │   │   │   ├── ClassIntroduceTitle
    │   │   │   │   ├── ClassIntroduceTitle.style.ts
    │   │   │   │   └── index.tsx
    │   │   │   ├── ClassSimpleInforrmation
    │   │   │   │   ├── ClassSimpleInformation.style.ts
    │   │   │   │   └── index.tsx
    │   │   │   ├── CommentInput
    │   │   │   │   ├── CommentInput.style.ts
    │   │   │   │   └── index.tsx
    │   │   │   ├── CommunityTitle
    │   │   │   │   ├── CommunityTitle.style.ts
    │   │   │   │   └── index.tsx
    │   │   │   ├── CurriculumContentList
    │   │   │   │   ├── CurriculumContentList.style.ts
    │   │   │   │   └── index.tsx
    │   │   │   ├── CurriculumTitle
    │   │   │   │   ├── CurriculumTitle.style.ts
    │   │   │   │   └── index.tsx
    │   │   │   ├── FooterInformation
    │   │   │   │   ├── FooterInformation.style.ts
    │   │   │   │   └── index.tsx
    │   │   │   ├── KitIntroduceContent
    │   │   │   │   ├── KitIntroduceContent.style.ts
    │   │   │   │   └── index.tsx
    │   │   │   ├── KitIntroduceTitle
    │   │   │   │   ├── KitIntroduceTitle.style.ts
    │   │   │   │   └── index.tsx
    │   │   │   ├── RecommendInformation
    │   │   │   │   ├── RecommendInformation.style.ts
    │   │   │   │   └── index.tsx
    │   │   │   ├── RecommendPrice
    │   │   │   │   ├── RecommendPrice.style.ts
    │   │   │   │   └── index.tsx
    │   │   │   ├── ReviewGrid
    │   │   │   │   ├── ReviewGrid.style.ts
    │   │   │   │   └── index.tsx
    │   │   │   ├── ReviewList
    │   │   │   │   ├── ReviewList.style.ts
    │   │   │   │   └── index.tsx
    │   │   │   ├── SearchInput
    │   │   │   │   ├── SearchInput.style.ts
    │   │   │   │   └── index.tsx
    │   │   │   ├── SectionNavBar
    │   │   │   │   ├── SectionNavBar.style.ts
    │   │   │   │   └── index.tsx
    │   │   │   ├── SideNavBarButton
    │   │   │   │   ├── SideNavBarButton.style.ts
    │   │   │   │   └── index.tsx
    │   │   │   ├── SideNavBarOption
    │   │   │   │   ├── SideNavBarOption.style.ts
    │   │   │   │   └── index.tsx
    │   │   │   ├── SideNavBarPrice
    │   │   │   │   ├── SideNavBarPrice.style.ts
    │   │   │   │   └── index.tsx
    │   │   │   ├── SideNavbarTitle
    │   │   │   │   ├── SideNavbarTitle.style.ts
    │   │   │   │   └── index.tsx
    │   │   │   ├── UserInformation
    │   │   │   │   ├── UserInformation.style.ts
    │   │   │   │   └── index.tsx
    │   │   │   └── index.ts
    │   │   └── organisms
    │   │       ├── ClassIntroduceSection
    │   │       │   ├── ClassIntroduceSection.style.ts
    │   │       │   └── index.tsx
    │   │       ├── ClassKitIntroduceSection
    │   │       │   ├── ClassKitIntroductSection.style.ts
    │   │       │   └── index.tsx
    │   │       ├── CommentSection
    │   │       │   ├── CommentSection.style.ts
    │   │       │   └── index.tsx
    │   │       ├── CommunitySection
    │   │       │   ├── CommunitySection.style.ts
    │   │       │   └── index.tsx
    │   │       ├── CurriculumSection
    │   │       │   ├── CurriculumSection.style.ts
    │   │       │   └── index.tsx
    │   │       ├── Footer
    │   │       │   ├── Footer.style.ts
    │   │       │   └── index.tsx
    │   │       ├── Header
    │   │       │   ├── Header.style.ts
    │   │       │   └── index.tsx
    │   │       ├── RecommendSection
    │   │       │   ├── RecommendSection.style.ts
    │   │       │   └── index.tsx
    │   │       ├── SideNavBarSection
    │   │       │   ├── SideNavNarSection.style.ts
    │   │       │   └── index.tsx
    │   │       └── index.ts
    │   ├── pages
    │   │   ├── ClassDetail
    │   │   │   ├── ClassDetail.style.ts
    │   │   │   └── index.tsx
    │   │   └── index.tsx
    │   └── templates
    │       ├── ClassInformation
    │       │   └── index.tsx
    │       ├── Community
    │       │   └── index.tsx
    │       ├── SideNavBar
    │       │   └── index.tsx
    │       └── index.ts
    ├── api
    │   └── classInformation.ts
    ├── assets
    ├── data
    │   └── classInformation.json
    ├── globalStyle
    │   └── globalStyle.ts
    ├── index.tsx
    ├── react-app-env.d.ts
    └── store
        ├── reducers
        │   ├── ClassInformation.ts
        │   └── index.ts
        └── sagas
            ├── ClassInformation.ts
            └── index.ts
```

### ++

리액트에서 가장 대표적인 디자인 패턴에는 **Presentational and Container Component Pattern**와 **Atomic Design Pattern**가 있고 내가 사용하고 있던 패턴은 Presentational and Container Component Pattern 이였다~
