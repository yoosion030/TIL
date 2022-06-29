# JSP

산업기사 내부평가를 보면서 기억해야할 것들을 기록함

## 초기 세팅

인코딩 설정을 UTF-8로 설정

1. HTML
2. CSS
3. JSP
4. Workspace
5. Spelling

서버 생성

1. 서버 파일 생성
2. 톰캣 버전 설정
3. 로컬에 설치된 톰캣 폴더 선택
4. 서버 포트 8090으로 설정

Dynamic WebProject 생성

## Util.java

1. DBPKG 패키지 > Util 클래스 파일 생성
2. 다음과 같이 코드 입력

## index 화면

1. `index.jsp` 파일 생성
2. `header.jsp`, `footer.jsp` 파일 생성
3. `index.jsp` 파일에서 다음과 같이 헤더와 푸터파일 불러오기

## Oracle DB 연결

1. 먼저 다음 폴더 경로에 `ojdbc6.jar` 파일 복붙하기

2. 다음과 같이 코드 치기
   ```java
    Connection con = null;
    PreparedStatement pstmt = null;
   ```
3. Try Catch 문 작성
4. 문제 조건에 맞는 sql 입력

5. ResultSet 결과 객체 불러오기

6. 반복문으로 돌리기

## JavaScript 코드로 예외처리

1. `check.js` 생성

2. 함수 생성

3. jsp 파일에 script 태그로 자바스크립트 파일 불러오기

4. 버튼 클릭 시 함수를 return 하게 함
