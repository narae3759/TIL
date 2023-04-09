> **Reference**<br>
> * 시계열 데이터 분석 with 파이썬 강의(Jose Portilla, Udemy)
> * [Forecasting: Principles and Practice](https://otexts.com/fppkr/expsmooth.html)
---

# **시계열 데이터 분석 과정**
## **1) 데이터 분할**
* Time Series data = Training data(과거 데이터) + Test data(최근 데이터)
* Test data의 크기는 전체 데이터의 크기와 예측하고자 하는 기간에 따라 달라진다.<br>
<u>Test data의 크기는 예측하고자 하는 기간보다는 커야한다.</u>
* 보통 전체 데이터의 20%로 결정한다. 

## **2) 모델링**
* Exponential Smoothing

## **3) Test data 예측**

## **4) 평가**
1. Plot으로 확인
2. 수치적으로 확인
    * 이산적인 값에 대한 분류
        * 정확도, 정밀도, 재현율, F1-Score
    * 연속적인 값에 대한 회귀
        * MAE(Mean Absolute Error) $= \dfrac{1}{n}\sum|y_i-\hat{y}_i|$<br>
        오차의 절댓값에 대한 평균이기 때문에 해석이 직관적이지만,<br>
        작은 지점에서 큰 오차가 난 경우 이 지점을 파악할 수 없어 해석이 왜곡될 수 있다.
        * MSE(Mean Square Error) $= \dfrac{1}{n}\sum(y_i-\hat{y}_i)^2$<br>
        제곱을 하게 되면 큰 오차가 난 경우 이를 파악하기가 더 쉽다.
        * RMSE(Root Mean Square Error) $= \sqrt{\dfrac{1}{n}\sum(y_i-\hat{y}_i)}$<br>
        MSE는 오차의 제곱에 대한 것으로 보고서에서 해석하기에 쉽지 않다.<br>
        단위를 원래 상태로 돌려 해석하기 위해 Root를 사용한다.  
    * 오차를 어느정도 허용할 것인가? $\rightarrow$ 상황에 따라 다르다.

## **5) 관찰되지 않은 미래 예측**
* 미래 날짜에 대한 예측은 관측되지 않은 값이기 때문에 비교할 대상이 없다.<br>
즉, 미래에 대한 예측값은 평가할 수 없다.<br>
$\Rightarrow$ 그래서 Test data의 크기 설정이 매우 중요하다.

# **정상성과 차분**
1. 정상성(Stationary)
    * 추세나 계절성을 나타내지 않는 경우
    * 데이터의 변동은 외부의 힘이나 noise에 의해 발생한다. 
2. 차분(Differencing)
    * 연속적인 지점 간의 차(diff)를 계산
    * Nonstationary data를 Stationary data로 바꿀 수 있다. 

# **ACF(자기상관함수) / PACF(부분자기상관함수)**
1. ACF
    * 현재와 $x$차 시점 간의 상관관계를 나타낸 것이다.
    * 상관계수 $\rho(-1\leq \rho\leq 1)$ : 선형관계를 파악할 수 있다.
    * 현재의 관측값과 $x$차  시점 관측값 간의 종속성 정보를 포함한 상관관계를 보인다.
2. PACF
    * 어제와 오늘 데이터가 선형이라고 하자.<br>
    이때의 오차는 선형모델로 설명할 수 없는 부분을 말한다. 
    * 위를 적합하여 잔차를 구하고, 그제 데이터와 잔차의 상관 관계를 파악한다. 
    * 이를 계속 반복한다.
    * 현재의 관측값과 이전 시점 관측값 사이의 직접적 관계만 보인다.
    * 급격한 감소를 보이는 시차가 곧 AR항의 차수를 나타낸다.

# **ARIMA Model**
* AR(자동회귀) + I(누적) + MA(이동평균)
* 시계열 데이터가 시간의 경과에 따른 관련성이 있을때 매우 효과적이다. 
* 제일 많이 사용되는 모델이지만, ARIMA가 모든 시계열자료를 잘 예측한다고 할 수는 없다. <br>
ex. 주식 데이터(주식은 시간뿐만 아니라 영향을 받는 다양한 외부 요소들이 존재한다.)
* 발달 과정<br>
ARMA - ARIMA(누적 추가) - SARIMA(계절성 추가) - SARIMAX(외생변수 추가)
* Stationary data일 때 적용한다. 만약 Nonstationary data라면 차분(differencing)을 통해 비정상성을 제거한다. 

## **비계절성 ARIMA**
* ARIMA(p, d, q)
    * p : AR(p)
    * d : I
    * q : MA(q)