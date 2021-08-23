
# git 명령어
## 생성하기
> - git clone { 저장소 url } : 저장소 복제하기
> - git init : 새로운 repository 생성
## 브랜치 작업
> - git checkout { branch 명 } : 브랜치 변경하기
> - git branch -d { branch 명 } : 브랜치 삭제하기
>  - git branch { new-branch 명 } : 브랜치 생성하기
## 살펴보기 
> - git status : 작업 디렉토리에 변경된 파일 보기
> - git log : 변경 이력 보기
## 커밋 작업
> - git commit -m "commit message" : 메세지와 함께 커밋
## 연동하기
> - git remote add origin { 깃허브 url } : 원격 저장소 추가
> - git retmoe -v : 원격 저장소 url 보기
> - git remote rm origin : 원격 저장소 삭제
> - git remote remove origin : 원격 저장소 삭제
> - git remote set -url origin { 깃허브 url } : repository 이름 변경 후 깃허브 연동 
