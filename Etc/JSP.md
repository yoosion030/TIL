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
3. try catch 문 작성
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

**Select면 `executeQuery` Insert, Delete, Update이면 `executeUpdate`**

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

## 데이터 Insert
1. hidden input 생성
```html
<input type="hidden" name="mode" value="insert"/> 
```
**value = "insert"**  

2. form action, method 추가
```html
<form name="frm" action="action.jsp" method="post" ...>
```
3. 등록 button 생성
```html
<input type="button" value="등록" onclick="return TryVote()"/>
```

```js
function TryVote() {
	if 예외처리...
	else {
		document.frm.submit();
	}
	return true;
}
```

4. action.jsp 에서 값 가져오기
```java
      request.setCharacterEncoding("UTF-8"); // 한글 인코딩
		Connection conn = null;
		PreparedStatement pstmt = null;
		
		String mode = request.getParameter("mode");
		String jumin = request.getParameter("jumin");
		String name = request.getParameter("name");
		String voteNum = request.getParameter("voteNum");
		String time = request.getParameter("time");
		String area = request.getParameter("area");
		String confirm = request.getParameter("confirm");
```
**request.getParameter(value)**

5. try catch 문 작성
```java
try {
   conn = Util.getConnection();
   String sql = "";
   
   switch(mode) {
   case "insert" : 
      sql = "INSERT INTO tbl_vote_202005 VALUES(" 
            + jumin + ","
            + "'" + name + "'" + "," 
            + "'" + voteNum + "'" + ","
            + "'" + time + "'" + ","
            + "'" + area + "'" + ","
            + "'" + confirm + "'" 
      +")";
      pstmt = conn.prepareStatement(sql);
      pstmt.executeUpdate();
   %>
   <jsp:forward page="voteList.jsp"/> // 이동할 페이지
   <%
   }
} catch (Exception e) {
   e.printStackTrace();
}
```

**insert라서 executeUpdate()**

## 데이터 delete

1. 리스트 페이지에서 수정 페이지로 이동할 link 생성
```jsp
<td>
   <a href="modify.jsp?id=<%=rs.getString(1)%>">수정페이지로 이동</a>
</td>
```
**`?id=아이디` 쿼리스트링으로 파라미터를 넘겨줌**

2. 파라미터로 넘어온 아이디로 기존 값 불러오기
```java
request.setCharacterEncoding("UTF-8");
String id = request.getParameter("id");
try {
   Connection conn = Util.getConnection();
   String sql = "SELECT * FROM course_tbl WHERE id = " + id;
   PreparedStatement pstmt = conn.prepareStatement(sql);
   ResultSet rs = pstmt.executeQuery();
   rs.next();
   String lecturer = rs.getString(4);
   String week = rs.getString(5);
   String start_hour = rs.getString(6);
   
%>
``` 
```html
<tr>
   <td>과목코드</td>
   <td><input type="text" name="id" style="width:100%" value="<%=id %>" readonly/>
</tr>
<tr>
   <td>과목명</td>
   <td><input type="text" name="name" style="width:100%" value="<%=rs.getString(2) %>" />
</tr>
<tr>
   <td>학점</td>
   <td><input type="text" name="credit" style="width:100%" value="<%=rs.getString(3) %>" />
</tr>
```
**input value안에 값 넣어주기**

3. hidden input 생성
```html
<input type="hidden" name="mode" value="modify"/>
```

4. form action, method 추가
```html
<form name="frm" action="action.jsp" method="post" ...>
```

5. 수정 button 생성
```html
<input type="button" value="수정" onclick="return modify()"/>
```

```js
function modify() {
	document.frm.submit();
}
```

6. action.jsp 작성
```java
case "modify" :
   sql = "UPDATE course_tbl SET name=?, credit=?, lecturer=?, week=?, start_hour=?, end_hour=? WHERE id=?";
   pstmt = conn.prepareStatement(sql);
   pstmt.setString(1, name);
   pstmt.setString(2, credit);
   pstmt.setString(3, lecturer);
   pstmt.setString(4, week);
   pstmt.setString(5, start_hour);
   pstmt.setString(6, end_hour);
   pstmt.setString(7, id);
   
   pstmt.executeUpdate();
%>
<jsp:forward page="modify.jsp"/>
```

**executeUpdate()** 필수 !!  
**setString(1, 값) 해주면 첫번째 물음표에 값이 들어감**

## 데이터 delete

1. 리스트 페이지에서 수정 페이지로 이동할 link 생성
```jsp
<td>
   <a href="action.jsp?id=<%=rs.getString(1)%>&mode=delete">삭제</a>
</td>
```

2. action.jsp 작성
```java
String id = request.getParameter("id");

case "delete" :
   sql = "DELETE FROM course_tbl WHERE id="+id;
   pstmt = conn.prepareStatement(sql);
   pstmt.setString(1, id);
   
   pstmt.executeUpdate();
%>
<jsp:forward page="list.jsp"/>			
<%
   break;
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
4. 인풋에 name 추가
```html
<input name="test" type="text" />
```

5. js 에서 예외처리

```js
if(document.frm.test.value.length === 0) {
		alert("ㅇㅇㅇ가 입력되지 않았습니다.");
		frm.test.focus();
		return false;
	}
```
`document.frm.test.value.length`로 접근

6. 버튼 클릭 시 함수를 return 하게 함
```html
<input type="button" onclick="return Ok()" value="눌러보셈"/>
```
7. 버튼 클릭 시 폼 리셋하기
```html
<form name="frm">
   ...
   <input type="button" onclick="return reset()>
```

```js
function TryReset(){
   	frm.reset();
}
```

## 데이터 형식 포맷
100000원을 100,000원 형식으로 표현
```java
DecimalFormat dcf = new DecimalFormat("###,###");
String tuition2 = dcf.format(100000); // 100,000
```