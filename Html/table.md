# \<table> 태그

## \<table> 태그는 HTML문서에서 표를 만듦. 행과 열을 표현하기 위해 \<tr>, \<td>등의 태그와 함께 작성됨

### \<tr>
>표의 행을 나타냄
### \<td>
>표의 열을 나타냄, \<tr>태그 하위에 위치함
### \<thead>
>표의 재목 영역을 나타냄, \<table>하위, \<tr>상위에 위치
### \<tbody>
>표의 본문 영역을 나타냄, \<thead>와 같은 위치
### \<th>
>제목 셀을 나타냄, \<td>대신 사용


### 예제
```html
<table>
    <thead>
        <tr>
            <th>이름</th>
            <th>나이</th>
        </tr>
    </thead>
        <tbody>
            <tr>
                <td>유시온</td>
                <td>17</td>
            </tr>
            <tr>
                <td>유시지</td>
                <td>23</td>
            </tr>
        </tbody>
</table>
```

### 출력결과
<table>
    <thead>
        <tr>
            <th>이름</th>
            <th>나이</th>
        </tr>
    </thead>
        <tbody>
            <tr>
                <td>유시온</td>
                <td>17</td>
            </tr>
            <tr>
                <td>유시지</td>
                <td>23</td>
            </tr>
        </tbody>
</table>






