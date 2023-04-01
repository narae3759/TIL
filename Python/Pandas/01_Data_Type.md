> **Reference**<br>
> * 시계열 데이터 분석 with 파이썬 강의(Jose Portilla, Udemy)
> * [파이썬 라이브러리(datetime)](https://docs.python.org/ko/3/library/datetime.html)
---

# **1. DateTime**
## **1) datetime형 index 생성하기**
### **방법 1. `datetime()`**
* 각 속성들을 입력하여 datetime type을 만들 수 있다. 

    ```python
    from datetime import datetime

    # default, 24시간 형식으로 인식함.
    year = 2023
    month = 3 
    day = 22
    hour = 22
    minute = 44
    second = 17 

    # datetime 형식의 date 변수 생성
    date = datetime(year, month, day, hour, minute, second)
    print(date)
    ```

    ```
    2023-03-22 22:44:17
    ```

* datetime type인 경우 속성을 통해 추출할 수 있다. 
    * month, day의 경우 `month_name`, `day_name`으로 `January`, `Monday` 형식을 추출할 수 있다.  
&nbsp;


    ```python 
    # date 변수의 속성으로 print하기
    print(f'{date.year}년 {date.month}월 {date.day}일 {date.hour}시 {date.minute}분 {date.second}초')
    ```

    ```
    2023년 3월 22일 22시 44분 17초
    ```

### **방법 2. Numpy**
* option `dtype='datetime64`을 통해 datetime type의 array를 생성할 수 있다. 
* `datetime[■]`(■=['Y','M','D',....])을 통해 정밀도를 조정할 수 있다.(default = 'D')

    ```python
    # 배열 생성 I
    np.array(['2023-03-22', '2023-03-23', '2023-03-24'], dtype='datetime64')

    # 배열 생성 II(정밀도 M)
    np.array(['2023-03-22', '2023-03-23', '2023-03-24'], dtype='datetime64[M]')
    ```
    ```
    array(['2023-03-22', '2023-03-23', '2023-03-24'], dtype='datetime64[D]')
    array(['2023-03', '2023-03', '2023-03'], dtype='datetime64[M]')
    ```

* `arrange()`를 통해 연속된 배열을 생성할 수 있다. 

    ```python
    # 연속된 배열 생성 I : 2023년 3월의 월요일 날짜 배열 만들기
    np.arange('2023-03-06','2023-03-31', 7, dtype='datetime64')

    # 연속된 배열 생성 II : 2002년부터 오늘까지 연도 배열 만들기
    np.arange('2002-01-01','2023-03-22', 1, dtype='datetime64[Y]')
    ```
    ```
    array(['2023-03-06', '2023-03-13', '2023-03-20', '2023-03-27'],
          dtype='datetime64[D]')
    array(['2002', '2003', '2004', '2005', '2006', '2007', '2008', '2009',
          '2010', '2011', '2012', '2013', '2014', '2015', '2016', '2017',
          '2018', '2019', '2020', '2021', '2022'], dtype='datetime64[Y]')
    ```

### **방법 3. Pandas**
* `date_range(str, periods=int, freq='■')`(■=['Y','M','D',....])를 통해 time stamp 인덱스를 생성할 수 있다.
    * 기본 형식 : '%Y-%m-%d' or '%b %m, %Y' (ex. '2023-01-01', 'Mar 19, 2023')
    * freq로 'Y' 또는 'M'을 사용하면 다른 뒤의 형식은 마지막 날짜로 생성된다. <br>
    (ex. freq='M'인 경우 '2012-01-14'라고 입력하더라도 '2012-01-31'부터 출력됨.)  
    &nbsp;

    ```python
    # 데이터프레임 time stamp index 생성 I : 2023년 3월 index 만들기(31개)
    pd.date_range('2023-03-01', periods=31, freq='D')

    # 데이터프레임 time stamp index 생성 II : 2013년 1월부터 연도-월 index 만들기(12개)
    pd.date_range('Jan 01, 2012', periods=12, freq='M')
    ```
    ```
    DatetimeIndex(['2023-03-01', '2023-03-02', '2023-03-03', '2023-03-04',
                  '2023-03-05', '2023-03-06', '2023-03-07', '2023-03-08',
                  '2023-03-09', '2023-03-10', '2023-03-11', '2023-03-12',
                  '2023-03-13', '2023-03-14', '2023-03-15', '2023-03-16',
                  '2023-03-17', '2023-03-18', '2023-03-19', '2023-03-20',
                  '2023-03-21', '2023-03-22', '2023-03-23', '2023-03-24',
                  '2023-03-25', '2023-03-26', '2023-03-27', '2023-03-28',
                  '2023-03-29', '2023-03-30', '2023-03-31'],
                  dtype='datetime64[ns]', freq='D')
    DatetimeIndex(['2012-01-31', '2012-02-29', '2012-03-31', '2012-04-30',
                  '2012-05-31', '2012-06-30', '2012-07-31', '2012-08-31',
                  '2012-09-30', '2012-10-31', '2012-11-30', '2012-12-31'],
                  dtype='datetime64[ns]', freq='M')
    ```

* `to_datetime()`을 통해 string을 datetime type으로 변형시킬 수 있다. 
    * option `format=''`으로 기본 표준형식이 아니어도 datetime type으로 바꿀 수 있다.   
    &nbsp;

    ```python
    # 데이터프레임 dtype변환
    pd.to_datetime(['2023/01/05 15:02:47', '2023/01/05 21:45:11'], format='%Y/%m/%d %H:%M:%S')
    ```
    ```
    DatetimeIndex(['2023-03-01', '2023-03-02'], dtype='datetime64[ns]', freq=None)
    ```