# yarn berry

## npm과 yarn v1

**기존 npm의 문제**

- lock 파일이 없다보니 생기는 패키지의 버저닝 / 의존성 이슈
- 보안 이슈
- 패키지가 늘어날 수록 성능 저하

npm의 문제를 해결해보고자 생긴 새로운 패키지 매니저 -> 🤩yarn🤩

**yarn v1의 장점**

- `yarn.lock` 파일 자동 생성, checksum을 통해 어느 환경에서든 동일한 패키지를 설치하게 함
- 의존성 트리 이슈는 lock파일과 설치 알고리즘을 통해 개선
- 패키지 병렬 설치를 통한 성능 개선
- `cache directory`를 통한 오프라인 미러링과 left-pad 이슈 방지

**npm 과 yarn v1의 공통적인 문제점**

- node_modules의 거대함과 depth의 문제

간단한 패키지를 몇 개 설치하지 않아도 `node_modules`의 depth와 용량은 엄청나게 커지게 된다.
더군다나 next.js등과 같이 다양한 기능을 제공하는 프레임워크, 라이브러리를 사용하게 된다면 최소 몇백메가에서 기가 단위의 디스크 용량을 사용하게 된다.
거기 더해서 depth는 점점 깊어지는 문제가 발생하게 되고, 이것은 설치, 삭제, 수정, 실행 등의 속도에 영향을 끼치게 되고, 패키지의 내용은 확인하지 못하고 기본적인 의존성 트리만 검증하게 된다.

- 유령 의존성
  ![](https://miro.medium.com/max/1400/0*dBcvEKcuTdmiUGfA.png)

왼쪽 그림은 package-1에서 B(1.0)패키지를 가져다 쓸 수 없는 구조지만 오른쪽 그림은 Hoisted가 되면서 package-1이 B(1.0)을 설치한 적이 없지만 B(1.0)을 가져다 쓸 수 있게 된다.

이런 현상을 **유령 의존성**이라고 보면 된다.

위와 같은 이슈가 발생시에는 `package.json`을 통해 설치 되지 않은 패키지를 사용할 수도 있고, 삭제할때도 잘 사용하던 패키지를 갑자기 사용할 수 없게 된다.

이러한 npm과 yarn의 문제점을 해결해보고자 생긴 새로운 패키지 매니저 -> ❤️yarn berry❤️

## yarn berry(v2)

yarn berry(v2)에서는 pnp라는 개념을 도입하여 아래와 같은 내용들을 해결해 준다.

- node_modules의 성능 문제

node_modules는 많은 양의 파일들을 포함하고 있다. 그러다 보니 `hot cache`를 이용하여 `yarn install`을 사용하여 `node_modules`을 생성하는 것보다 70%이상의 시간이 걸린다. 이러한 방식은 I/O bound를 사용하기 때문에 패키지 매니저는 이러한 복사 등에 최적화 할 수 없다.

- nodejs는 package라는 개념이 없음

nodejs는 어떤 파일들에 접근가능한 지와 끌어올려지는지 알 수 없다.
개발할 때는 문제가 ㅇ벗던 코드가 프로덕션 형태일 때는 `package.json`에 누락된 패키지때문에 실패할 수도 있다.

이는 유령 의존성과도 연관이 될 수 있다.

- 비효율적인 resolution

`node resolution`은 하나의 파일 의존성을 로드하기까지 `readdir`, stat과 같은 느린 I/O와 같은 `system call`을 반복적으로 호출한다.

- node_modules의 비효율적인 구조

`node_modules`의 다양한 구조는 실용적이지 못하며, 원하는 만큼의 중복제거를 할 수 없다. 같은 이름의 다양한 버전을 가지고 있는 패키지들 때문에 완벽한 hoist를 보장할 수 없다.

## Plug’n’Play (PnP)

yarn2에서는 비효율적인 `node_modules`대신에 `.pnp.js`라는 파일을 생성하게 된다.

`.pnp.js`는 다음과 같은 포맷을 가지게 된다.

    패키지 이름 + 패키지 버전 + 패키지의 실제 위치를 담은 맵과, 패키지 이름 + 패키지 버전 + 패키지의 종속성을 담은 맵을 저장합니다.

코드는 다음과 같다.

```js
["@ant-design/react-slick", [ //패키지 이름
  ["npm:0.28.3", { //패키지 버전
    //패키지 경로
    "packageLocation": "./.yarn/cache/@ant-design-react-slick-npm-0.28.3-ece1f2feb7-887cb395bd.zip/node_modules/@ant-design/react-slick/",
    "packageDependencies": [ //패키지 종속성
      ["@ant-design/react-slick", "npm:0.28.3"],
      ["@babel/runtime", "npm:7.14.6"],
      ["classnames", "npm:2.3.1"],
      ["json2mq", "npm:0.2.0"],
      ["lodash", "npm:4.17.21"],
      ["resize-observer-polyfill", "npm:1.5.1"]
    ],
    "linkType": "HARD",
  }]
]],
```

위와 같은 방식은 아래와 같은 이점을 가지고 있다.

1. `.pnp.js`파일 하나만 생성하게 됨으로서 설치가 빨라진다.
2. disk I/O 사용이 줄어들기 때문에 안정적으로 설치가 가능하다.
3. 종속성 트리의 최적화 및 예측가능한 패키지 인스턴스와
4. **Zero-Installs**의 부분으로서 `repository`에 `.pnp.js`를 commit할 수 있다. (다른 곳에서도 yarn install을 할 필요가 없다.)
5. 프로그램을 빠르게 시작할 수 있다. 위에서 얘기한 `node resolution`의 file system의 순회가 이전보다 줄어든다.
6. 의존성 끌어올리기를 하지 않기 때문에 `node_modules`에 설치되었던 패키지를 사용할 수 있었던 부분이 제거 되었고 유령 의존성 현상을 막을 수 있다.
7. `Yarn PnP`에서는 **Zip**파일을 이용하여 패키지를 관리하기 때문에 빠진 의존성을 찾거나 의존성 파일이 변경되었음을 찾기 쉽다. 이로써 의존성이 잘못되었을 때 바로잡을 수 있다.

## Zero-Installs

`yarn pnp`는 의존성 관리를 `.yarn/cache` 디렉토리 내에 zip 파일로 관리한다. 또한 다른 환경에서도 별도의 `yarn install`을 통한 설치가 필요없도록 repository에 commit을 하도록 요구한다.

`Zero-Installs`을 사용할지 아닐지에 따라 `.gitignore` 내용도 제공해주고 있습니다.

**Zero-Installs을 사용하였을 때 기존 yarn v1과 다른점**

- 거대한 용량차이

node_modules 는 1.2GB 크기이고 13만 5천개의 파일로 구성되어 있는 반면, Yarn PnP의 필요한 패키지들은 139MB 크기의 2천개의 압축 파일로 구성됩니다.

위의 용량차이로 인하여 `repository`에 울리도록 하는 것에 대한 비효율에 대한 의문은 해결이 되었다. `Zero-Installs`을 사용하여 ex ) 원티드 CI의 배포 시간을 기존 7~8분에서 5~6분으로 줄일 수 있었다.


