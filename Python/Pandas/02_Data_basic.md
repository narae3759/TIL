> **Reference**<br>
> * [쇼핑데이터를 활용한 머신러닝](https://www.boostcourse.org/ai224)
> * [Pandas API Reference](https://pandas.pydata.org/docs/reference/)
> * [Analytics Vidhya Blog, Skewness and Kurtosis: Quick Guide](https://www.analyticsvidhya.com/blog/2021/05/shape-of-data-skewness-and-kurtosis/)
---


# **데이터 파악하기**

## **<학습 목표>**
* 데이터 불러오기
* 데이터 정보 확인하기
* 결측치 여부 체크하기 ★★★
* 데이터 요약하기

## **1. 데이터 불러오기**
### **`pd.read_csv()/pd.read_excel()`**
* options
    * `index` : 인덱스로 설정할 column의 번호
    * `columns` : column 명 설정
    * `parse_dates` : 시계열 column을 설정하면, 자동으로 `datetime` 타입으로 인식한다.

## **2. 데이터 정보 확인하기**
### **`dataframe.info()`**
* 데이터 크기, 변수들의 속성, Null의 여부 등을 한번에 파악할 수 있다.

## **3. 결측치 여부 체크하기**
* 실 데이터를 보면 결측치 있는 데이터 많다. 
* 결측치는 분석 결과에 많은 영향을 미치기 때문에 파악하는 것은 매우 중요하다. 
### **`is.na()`**
* 각 데이터를 하나의 '셀'이라고 할 때,
각 셀이 Null이면 True 아니면 False라고 반환한다. 
* ***응용 1*** : `is.na().sum(axis=0)`, 변수마다 결측치가 몇 개 있는지 파악할 수 있다.
* ***응용 2*** : `is.na().sum(axis=0)/data.shape[0]`, 변수마다 결측치 비율을 파악할 수 있다.

```python
def check_NA(data):
    nrow = data.shape[0]
    count_NA = data.isna().sum(axis=0)
    ratio_NA = count_NA / nrow

    report_NA = pd.concat([count_NA, ratio_NA], axis=1)
    report_NA.index.name = 'variables'
    report_NA.columns = ['count', 'ratio']

    if report_NA['count'].sum() == 0:
        return 'There are no missing values in this data!'

    return report_NA
```

## **4. 데이터 요약하기**
* 데이터 유형은 `number`(`float`, `int`) / `datetime` / `object` / `category`로 나눌 수 있다. 
### **`dataframe.describe()`**
* default로 데이터 타입이 `number, datetime`인 columns에 대한 요약으로 출력한다.
* 요약할 데이터 타입에 따라 출력하는 요약 통계량이 다르다.
    * `object`, `category` : count, unique, top, freq
    * `number`, `datetime` : count, mean, std, min, 25%, 50%, 75%, max (default)
* options
    * `percentiles`: default로 4분위수가 출력되지만 다른 분위수를 보고 싶을 때 설정이 가능하다. (ex.`[0.1, 0.99]`)
    * `include`,`exclude` : 출력할 데이터 타입을 지정할 수 있다.<br>
        * EX1. include='all', 모든 데이터 변수를 요약한다.
        * EX2. include='number', `float`, `int` 타입인 변수만 요약한다.
        * EX3. exclude='datetime', `datetime` 타입을 제외한 나머지 변수를 요약한다.
    
    
```python
# 실험해보기
df = pd.DataFrame({'categorical': pd.Categorical(['d','e','f','e','f']),
                'numeric': [1, 2, 3, 4, 5],
                'object': ['a', 'b', 'c', 'd', 'e'],
                'datetime': np.arange('2023-03-06','2023-03-11', dtype='datetime64')
                })
```

### **`dataframe.skew()/kurtosis()`**
* 이상적인 데이터 분석은 변수가 ***정규성***을 띄는 것이다. 
<br>skewness(치우침의 정도)와 kurtosis(꼬리의 두꺼운 정도)를 통해 데이터의 분포를 확인할 수 있다.
* skewness(왜도) : 데이터의 비대칭을 확인할 수 있는 척도
    * skewness > 0 : 데이터가 ***왼쪽***으로 치우쳐져 있다. 
    * skewness = 0 : 데이터가 ***대칭***이다.
    * skewness < 0 : 데이터가 ***오른쪽***으로 치우쳐져 있다.
* kurtosis(척도) : 데이터의 분산을 파악할 수 있는 척도
    * kurtosis > 3 : Mesokutric, 꼬리가 두껍다
    * kurtosis = 3 : leptokurtic, 정규분포
    * kurtosis < 3 : platykurtic, 꼬리가 얇다. 너무 크면 이상치가 있음을 의심해볼 수 있다. 

```python
# pandas의 describe()에 skewness/kurtosis를 추가하여 summary 함수를 만들었다.
def summary(data):
    describe = data.describe()
    skewness = data.skew(axis=0, numeric_only=True)
    kurtosis = data.kurtosis(axis=0, numeric_only=True)
    add_describe = pd.concat([skewness, kurtosis], axis=1)
    add_describe.columns = ['skewness', 'kurtosis']

    result = pd.concat([describe, add_describe.transpose()], axis=0)

    return result
```


