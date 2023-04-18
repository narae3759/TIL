# **기본**
## **처음 N개의 행만 추출: `LIMIT N`**
## **서브쿼리는 ()안에 적용한다**
* 조건들이 적용된 쿼리들을 결합해야 할 때 효율적으로 표현하기 위해 `WITH`를 사용한다.

# **SELECT**
## **조건에 따른 새로운 COLUMN 생성 : `CASE WHEN THEN ELSE END`**
* EX1. 'SCORE'가 70점 넘으면 합격 아니면 불합격이라는 'RESULT' COLUMNS을 생성하자.
    ```sql 
    SELECT CASE WHEN SCORE >= 70 THEN "합격"
                ELSE "불합격"
           END
    FROM DATA  
    ```

# **WHERE**
## **문자의 포함 여부 확인 : `LIKE`**
* EX1. 이메일 주소가 네이버인 행만 추출 $\rightarrow$ `LIKE "%@NAVER.COM"`
* EX2. 성이 '김'씨인 고객만 추출 $\rightarrow$ `LIKE "김%"`
* EX3. 문장에 'no'가 포함된 행만 추출 $\rightarrow$ `LIKE "%no%"`

## **하나의 COLUMN에 다중 조건** : `IN (조건1, 조건2, ...)`
* ※ `LIKE`와 `IN`은 동시에 사용할 수 없다. 
* EX1. 통근수단이 '버스', '지하철', '자전거'인 행만 추출 $\rightarrow$ `IN ('버스', '지하철', '자전거)`




# **FUNCTIONS**
## **`DATE_FORMAT(DATE, FORMAT)`**
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

## **`DATEDIFF(AFTER DATE, BEFORE DATE)`**
* 두 날짜 사이의 일수를 계산한다.(<u>※ 이때 두 날짜는 포함되지 않는다.</u>)
* EX1. 강아지가 보호소에 들어온 날짜(DATE1)과 입양일(DATE2)사이의 기간을 계산하자.<br>
$\rightarrow$ `DATEDIFF(DATE2, DATE1)`
* EX1. 대여일(START_DATE)과 반납일(END_DATE)를 통해 대여 기간을 계산하자.<br>
$\rightarrow$ `DATEDIFF(DATE2, DATE1) + 1` (대여일도 대여 기간에 포함되기 때문)