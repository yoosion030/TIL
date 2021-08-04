# git flow

## git Repository 구성
- Upstream Repository : 개발자들이 공유하는 저장소로 최신 소스코드가 저장되어 있는 원격 저장소
- Origin Repository : Upestream Repository를 Fork한 원격 개인 저장소
- Local Repository : 내 컴퓨터에 저장되어 있는 저장소

## git flow 전략
- master : 제품으로 출시될 수 있는 브랜치
- hotfix : 출시 버전에서 발생한 버그를 수정하는 브랜치
- release : 이번 출시 버전을 준비하는 브랜치
- develop : 다음 출시 버전을 개발하는 브랜치
- feature : 기능을 개발하는 브랜치

### 개발 흐름
1. master와 develop 브랜치 존재 
   - develop 브랜치는 master에서 시작된 브랜치임
   - develop 브랜치에서는 상시로 버그를 수정한 커밋들이 추가됨
2. 새로운 기능 추가 작업이 있는 경우 develop 브랜치에서 feature 브랜치를 생성
    - feature 브랜치는 언제나 develop 브랜치에서 시작함
3. 기능 추가 작업이 완료되었다면 feature 브랜치는 develop브랜치로 merge됨
   -  merge( 합병 ) : 두 개의 브랜치를 합치는 과정
4. develop에 모든 기능이 merge 되었다면 QA( 품질 관리 )를 하기 위해 develop 브랜치에서 release 브랜치를 생성함
- QA를 진행하면서 발생한 버그들은 relase 브랜치에 수정됨
6. relase 브랜치를 master와 develop 브랜치로 merge함
7. 마지막으로 출시된 master 브랜치에서 버전 태그를 추가함