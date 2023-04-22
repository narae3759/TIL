# **기본**
* **`AS`를 통해 COLUMN의 이름을 다시 설정할 수 있다**
* **처음 N개의 행만 추출: `LIMIT N`**
* **서브쿼리는 ()안에 적용한다**
    <details>
    <summary>내가 가장 많이 하는 실수</summary>
    <div markdown="1">
    서브쿼리들의 결합으로 만들어진 TABLE을 `FROM` 뒤에 붙일 때 ()안에 서브쿼리들을 다시 써야 한다. 

    ```sql
    SELECT *
    FROM 
    (
        (
            서브쿼리1
        )
        UNION ALL
        (
            서브쿼리2
        )
    )
    ```
    </div>
    </details>

# **SELECT**
## **기본 계산 함수 : `SUM(), MIN(), MAX(), COUNT(), AVG()`**
* 그룹별 통계를 내고 싶을 때 `GROUP BY 'COLUMN'`과 함께 쓰인다. 
* 전체 행의 카운트를 셀 때에는 따로 COLUMN 설정 없이 `COUNT(*)`를 사용한다. 

## **조건에 따른 새로운 COLUMN 생성 : `CASE WHEN THEN ELSE END`**
* EX1. 'SCORE'가 70점 넘으면 합격 아니면 불합격이라는 'RESULT' COLUMNS을 생성하자.
    ```sql 
    SELECT CASE WHEN SCORE >= 70 THEN "합격"
                ELSE "불합격"
           END
    FROM DATA  
    ```

## **중복되지 않는 COLUMN 추출 : `DISTINCT 'COLUMN'`**
* EX1. 결제 수단(PAY)의 종류를 추출 $\rightarrow$  `DISTINCT PAY`

# **WHERE**
## **문자의 포함 여부 확인 : `LIKE`**
* EX1. 이메일 주소가 네이버인 행만 추출 $\rightarrow$ `LIKE "%@NAVER.COM"`
* EX2. 성이 '김'씨인 고객만 추출 $\rightarrow$ `LIKE "김%"`
* EX3. 문장에 'no'가 포함된 행만 추출 $\rightarrow$ `LIKE "%no%"`

## **하나의 COLUMN에 다중 조건** : `IN (조건1, 조건2, ...)`
* ※ `LIKE`와 `IN`은 동시에 사용할 수 없다. 
* EX1. 통근수단이 '버스', '지하철', '자전거'인 행만 추출 $\rightarrow$ `IN ('버스', '지하철', '자전거)`

## **사이에 있는 값 찾기 :  `BETWEEN A AND B`**
* 점수(SCORE)가 70점 <u>이상</u> 80점 <u>이하</u>인 행만 추출 $\rightarrow$ `SCORE BETWEEN 70 AND 80`

# **ORDER BY**
* EX1. USER_ID를 기준 오름차순으로 정렬 $\rightarrow$ `ORDER BY USER_ID` / `ORDER BY USER_ID ASC`
* EX2. USER_ID를 기준 내림차순으로 정렬 $\rightarrow$ `ORDER BY USER_ID DESC`
* EX3. NAME을 기준 오름차순으로 정렬 후 같으면 USER_ID를 기준 내림차순으로 정렬 <br>
$\rightarrow$ `ORDER BY NAME, USER_ID DESC`
* EX4. NAME을 기준 내립차순으로 정렬 후 같으면 USER_ID를 기준 오름차순으로 정렬<br>
$\rightarrow$ `ORDER BY NAME DESC, USER_ID`

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