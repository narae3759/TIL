> **Reference**<br>
> * [머신러닝 교과서 with 파이썬, 사이킷런, 텐서플로 개정3판](https://github.com/gilbutITbook/080223)
> * [TensorFlow 가이드](https://www.tensorflow.org/guide?hl=ko)
---

# **`tf.Variable()`**
* 모델을 훈련할 때 파라미터를 저장하고 업데이트 할 수 있는 Tensor 객체를 의미한다.<br>
원하는 파라미터의 값을 계속해서 업데이트 할 수 있도록 만든 메모리라고 생각하자.
* 값을 업데이트 하는 과정에서 <u>크기나 타입을 바꿀 수 없다.</u>
* `w = tf.Variable()`이라고 할 때, `w.value()`는 variable을 tensor 객체로 출력한다.

## **1) 변수 이름 중복 가능**
다른 텐서 변수더라도 같은 이름일 수 있다.

```python
# 변수 이름 중복 가능
t_var1 = tf.Variable([[1, 2, 3], [4, 5, 6]], name="Var")
t_var2 = tf.Variable([[10, 20], [30, 40]], name="Var")

print(t_var1.numpy())
print(t_var2.numpy())
print(t_var1 == t_var2)

## Output
## [[1 2 3]
##  [4 5 6]]

## [[10 20]
##  [30 40]]

## tf.Tensor(False, shape=(), dtype=bool)
``` 

## **2) 변수 값 변경 가능**
* `tensor.assign()`으로 값을 자유롭게 변경할 수 있다.
    * `read_value=True/False` : assign 함수를 실행할 때 출력할 지의 여부를 결정한다. 
* `tensor.assign_add()/sub()`으로 기존의 값에 대한 연산으로 변경할 수도 있다.

```python
# 변수값 변경
t_var = tf.Variable([1, 2, 3, 4, 5])

## [1, 2, 3, 4, 5] -> [10, 20, 30, 40, 50]
t_var.assign([10, 20, 30, 40, 50]) 
print(t_var.numpy())    ## [10 20 30 40 50]

## [10, 20, 30, 40, 50] + [1, 2, 3, 4, 5]
t_var.assign_add([1, 2, 3, 4, 5])
print(t_var.numpy())    ## [11 22 33 44 55]

## [11, 22, 33, 44, 55] - [10, 20, 30, 40, 50]
t_var.assign_sub([10, 20, 30, 40, 50])
print(t_var.numpy())    ## [1 2 3 4 5]
```        

## **3) 변수 복제 가능**
기존의 변수를 새로운 변수로 만들면 복제가 가능하다.

```python
# 변수 복제
t_var = tf.Variable([1, 2, 3, 4, 5])
t_var_copy = tf.Variable(t_var)
t_var_copy.assign([10, 20, 30, 40, 50])

print(t_var.numpy())        ## [1, 2, 3, 4, 5]
print(t_var_copy.numpy())   ## [10, 20, 30, 40, 50]
```   

## **4) 초기값 설정 필요**
* 딥러닝 학습을 위해서는 가중치 초기화가 매우 중요하다.<br>
가중치를 초기화에 따라 결과가 크게 달라질 수 있기 때문에 유의해야 한다.
* 어떤 랜덤한 값으로 지정해야 하는데 어떻게 설정할지에 대한 방법은 여러가지가 존재한다. <br>
(ex. 0으로 설정, Uniform 분포, Normal 분포 등) <br>
!!! 보편적으로 많이 쓰이는 방법을 알고 싶다면 **Weight Initialization**을 공부하자.
* 이 설정을 사용하고 싶지 않다면 `trainable=False` 옵션을 추가한다.
    
```python
# 초기값 설정
tf.random.set_seed(1)
init = tf.keras.initializers.GlorotNormal()     ## 세이비어(글로럿) 초기화 방법
print(init(shape=(5,)))

## Output
## tf.Tensor([-0.3358418   0.30700108  0.6716258  -0.59793264 -0.57963747], shape=(5,), dtype=float32)
```
※ 세이비어(글로럿) 초기화 방법<br>
이전 층의 노드 수와 다음 층의 노드 수를 이용하여 랜덤하게 값을 생성한다.