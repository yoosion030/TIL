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
```java
package DBPKG;
import java.sql.*;

public class Util {
	public static Connection getConnection() throws Exception {
		Class.forName("oracle.jdbc.OracleDriver");
		Connection con = DriverManager.getConnection("jdbc:oracle:thin:@//localhost:1521/xe", "system", "1234");
		return con;
	}
}

```

## index 화면

1. `index.jsp` 파일 생성
2. `header.jsp`, `footer.jsp` 파일 생성
3. `index.jsp` 파일에서 다음과 같이 헤더와 푸터파일 불러오기

```jsp
	<jsp:include page="header.jsp"/>
	<jsp:include page="footer.jsp"/>
```

## sqlplus 접속

1. cmd 창 열기
2. sqlplus 사용자이름/비밀번호
3. table create 및 샘플 데이터 insert

## Oracle DB 연결

1. 먼저 다음 폴더 경로에 `ojdbc6.jar` 파일 복붙하기  

![](/Image/ojdbc6.png)

2. 다음과 같이 코드 치기
   ```java
    Connection con = null;
    PreparedStatement pstmt = null;
   ```
3. Try Catch 문 작성
```java
try {

   }
   catch(Exception e) {
      e.printStackTrace();
   }
```
4. try 문에 db 연결과 문제 조건에 맞는 sql 입력
```java
try {
      con = Util.getConnection();
      String sql = "select me.menuno, me.menuname, sum(amount), sum(amount * price) " +
            "from menu_tbl me, order_tbl od " +
            "where me.menuno = od.menuno " + 
            "group by me.menuno, me.menuname " +
            "order by me.menuno ASC";

      pstmt = con.prepareStatement(sql);
```
5. ResultSet 결과 객체 불러오기
```java
ResultSet rs = pstmt.executeQuery();
```
6. 반복문으로 돌리기
```java
while(rs.next()) {
   %>
      <tr>
         <td><%=rs.getString(1) %></td>
         <td><%=rs.getString(2) %></td>
         <td><%=rs.getString(3) %></td>
         <td><%=rs.getString(4) %>원</td>
      </tr>
   <% 
}
```
## JavaScript 코드로 예외처리

1. `check.js` 생성

2. 함수 생성
```js
function Ok() {
	alert("속았징? ㅋ");
}
```
3. jsp 파일에 script 태그로 자바스크립트 파일 불러오기
```html
<script type="text/javascript" src="check.js"></script>
```
4. 버튼 클릭 시 함수를 return 하게 함
```html
<input type="button" onclick="return Ok()" value="눌러보셈"/>
```