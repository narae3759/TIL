# **Column: 'COLUMN명' in where clause is ambiguous**
* 두 테이블을 JOIN한 테이블에서 COLUMN명이 겹치는 경우 발생한다.
* **해결방법**<br>
TABLE에 별칭을 붙이고(ex.t1, t2) 어느 테이블의 COLUMN명을 의미하는지 작성한다.
* <b><u>예시. [BOARD_ID, REPLY_ID, TITLE, CONTENTS(댓글내용)]을 추출하자.</u></b><br>
TABLE1 : [BOARD_ID, WRITER_ID, TITLE, CREATED_DATE, CONTENTS]<br>
(게시글 ID, 작성자 ID, 글 제목, 글 작성일, 글 내용)<br>
TABLE2 : [BOARD_ID, REPLY_ID, CREATED_DATE, CONTENTS]<br>
(게시글 ID, 댓글 ID, 댓글 작성일, 댓글 내용)
    ```sql
    SELECT BOARD_ID, REPLY_ID, TITLE, t2.CONTENTS 
    FROM TABLE1 t1
    LEFT JOIN TABLE2 t2 ON t1.BOARD_ID = t2.BOARD_ID
    ```