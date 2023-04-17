# **`FORMAT_DATE(DATE, FORMAT)`**
* DATE TYPE인 COLUMN의 기본형은 '0000-00-00 00:00:00'이다.
* 필요한 상황1. 조회 <br>
COLUMN을 불러오는 데 날짜의 형식을 다르게 표현하고 싶을 때 필요하다. 
* 필요한 상황2. 조건문 <br>
2022년 또는 2022년 8월과 같은 조건이 필요할 때 필요하다.
* 사용 가능한 기호<br>
    <table>
        <tr> <th>기호</th> <th>표현</th> 
            <th>기호</th> <th>표현</th>
            <th>기호</th> <th>표현</th>
            <th>기호</th> <th>표현</th> </tr>
        <tr> <td>%Y</td> <td>2022</td> 
            <td>%y</td> <td>22</td>
            <td>%W</td> <td>Saturday</td>
            <td>%a</td> <td>Sat</td> </tr>
        <tr> <td>%M</td> <td>March</td> 
            <td>%b</td> <td>Mar</td>
            <td>%I</td> <td>1</td>
            <td>%H</td> <td>13</td> </tr>
        <tr> <td>%m</td> <td>03</td> 
            <td>%c</td> <td>3</td>
            <td>%i</td> <td>05</td>
            <td>%S</td> <td>55</td> </tr>
        <tr> <td>%d</td> <td>05</td> 
            <td>%e</td> <td>5</td>
            <td>%r</td> <td>01:05:55 PM</td>
            <td>%T</td> <td>13:05:55</td> </tr>
    </table>