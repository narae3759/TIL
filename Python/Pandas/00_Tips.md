
# **`dataframe.groupby()`**
* 그룹별 통계를 내고 싶을 때 사용한다. 
* 뒤에 `sum(), mean(), var(), ...`의 함수로 보고서를 쉽게 만들 수 있다.
* 여러 개의 변수를 통해 combination으로 요약이 가능하다. <br>
ex. 데이터 `data`에서 변수 `col1`이 'A', 'B'인 범주형 자료이고, `col2`가 '가','나'인 범주형 자료라고 하자. <br>
col1, col2별로 value의 평균을 구하고 싶다.<br>
$\rightarrow$ `data.groupby(['col1','col2'])['value'].mean()`
* :exclamation: *<u>혹시나 통계를 냈는데 숫자가 너무너무 이상하다?</u>*
<br> $\rightarrow$ 데이터 타입을 확인해보자. 가끔 숫자가 아닌 'object'로 설정되어 있을 때가 있으니 주의하자.

# **날짜/시간 다루기**
> 참고자료
> 1. [datetime 라이브러리](https://docs.python.org/ko/3/library/datetime.html)
> 2. [dateutil.relativedelta 라이브러리](https://dateutil.readthedocs.io/en/stable/examples.html#relativedelta-examples)

* 데이터를 정제할 때, datetime을 원하는 포맷에 맞게 string으로 변환하는 작업을 많이 하게 된다. 
* 매일 헷갈려하는 것. datetime $\rightarrow$ string : `strftime()` /  string $\rightarrow$ datetime : `strptime()`

## **1) Format 변환 : `datetime.datetime.strftime()/strptime()`**
1. datetime $\rightarrow$ string : `datetime.datetime.strftime()`
2. string $\rightarrow$ datetime : `datetime.datetime.strptime()`

    ```python
    from datetime import datetime

    # datetime -> string
    date = datetime(2022,12,25,13,34,59)
    print(f"date: {date}")                                          # 2022-12-25 13:34:59
    print(f"YYYY-MM-DD: {datetime.strftime(date, '%Y-%m-%d')}")     # 2022-12-25
    print(f"YYMMDD: {datetime.strftime(date, '%y%m%d')}")           # 221225

    # string -> datetime
    date = '2022.05.05 07:25:29 PM'
    print(datetime.strptime(date, '%Y.%m.%d %I:%M:%S %p'))          # 2022-05-05 19:25:29

    date = '04 Jan, 2022'
    print(datetime.strptime(date, '%d %b, %Y'))                     # 2022-01-04 00:00:00

    date = '22-04'
    print(datetime.strptime(date, '%y-%m'))                         # 2022-04-01 00:00:00
    ```
* :exclamation: `dataframe`일 때에는?<br>
$\rightarrow$ `dataframe.dt.strftime()/strptime()`

## **2) 날짜 계산: `dateutil.relativedelta.relativedelta()`**
* 날짜 사이의 간격을 계산하거나 일정 시간 전/후의 날짜를 계산할 수 있다.

```python
from datetime import datetime
from dateutil.relativedelta import relativedelta

# 날짜 사이의 간격 알아보기 
start_date = datetime(2022,3,15)
end_date = datetime(2023,3,22)
print(relativedelta(end_date, start_date))      

## relativedelta(years=+1, days=+7)

# 1년 전/후의 날짜 계산하기
today = datetime(2022,6,5)
print(f'1년 전: {today + relativedelta(days=-365)}')
print(f'1년 후: {today + relativedelta(years=+1)}')

## 1년 전: 2021-06-05 00:00:00
## 1년 후: 2023-06-05 00:00:00
```

## **3) 응용**
* '2022-05'의 1년 후 날짜를 'May, 2023'으로 나타내자.

    ```python
    from datetime import datetime
    from dateutil.relativedelta import relativedelta

    strtime = '2022-05'
    convert_datetime = datetime.strptime(strtime, '%Y-%m')      # string -> datetime
    after1year = convert_datetime + relativedelta(years=+1)     # + 1 year
    convert_string = after1year.strftime("%b, %Y")              # datetime -> string

    print(convert_string)   # May, 2023
    ```