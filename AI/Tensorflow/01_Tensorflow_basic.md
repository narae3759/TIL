> **Reference**<br>
> * [머신러닝 교과서 with 파이썬, 사이킷런, 텐서플로 개정3판](https://github.com/gilbutITbook/080223)
> * [TensorFlow 가이드](https://www.tensorflow.org/guide?hl=ko)
---

# **TensorFlow?**
* 2015년 등장. Google Brain 팀이 개발한 딥러닝 라이브러리 중 하나. 
* 머신러닝 작업 속도를 매우 빠르게 높여준다. 

# **1. Tensor 생성**
## **1) numpy array, list를 통한 Tensor 생성**
### **`tf.convert_to_tensor(np.array/list)`**

```python
arr1 = np.array([1, 4, 6, 2, 3], dtype=np.int32)
arr2 = [2, 5, 7, 8, 4]

t_arr1 = tf.convert_to_tensor(arr1)
t_arr2 = tf.convert_to_tensor(arr2)

print(t_arr1)
print(t_arr2)

## Output
## tf.Tensor([1 4 6 2 3], shape=(5,), dtype=int32)
## tf.Tensor([2 5 7 8 4], shape=(5,), dtype=int32)
```
### **`tf.constant(np.array/list)`**

```python
const_tensor1 = tf.convert_to_tensor(np.array([1.2, 5, np.pi], dtype=np.float32))
const_tensor2 = tf.constant([1.2, 5, np.pi], dtype=tf.float32)

print(const_tensor1)
print(const_tensor2)

## Output
## tf.Tensor([1.2       5.        3.1415927], shape=(3,), dtype=float32)
## tf.Tensor([1.2       5.        3.1415927], shape=(3,), dtype=float32)
```

### **`tf.range(num)`**
* 연속된 숫자의 tensor 생성

```python
range_tensor = tf.range(10)
print(range_tensor)

## Output
## tf.Tensor([0 1 2 3 4 5 6 7 8 9], shape=(10,), dtype=int32)
```

## **2) 하나의 원소로 채우기**
* ★★★★★ 생성할 Tensor의 크기가 크다면 `tf.fill`이 더 효율적이다.
### **`tf.ones(shape) / tf.zeros(shape) / tf.fill(shape, num)`**

```python
t_ones = tf.ones((3, 4))                # 모든 원소 1
t_zeros = tf.zeros((3, 4))              # 모든 원소 0
fill_tensor = tf.fill((3, 4), 9)        # 모든 원소 사용자 지정

print(t_ones)
print(t_zeros)
print(fill_tensor)

## Output 
## tf.Tensor(
## [[1. 1. 1. 1.]
##  [1. 1. 1. 1.]
##  [1. 1. 1. 1.]], shape=(3, 4), dtype=float32)

## tf.Tensor(
## [[0. 0. 0. 0.]
##  [0. 0. 0. 0.]
##  [0. 0. 0. 0.]], shape=(3, 4), dtype=float32)

## tf.Tensor(
## [[9 9 9 9]
##  [9 9 9 9]
##  [9 9 9 9]], shape=(3, 4), dtype=int32)
```

## **3) 랜덤으로 원소 채우기**
### **`tf.random.uniform(shape, minval=0, maxval=1)`**

```python
tf.random.set_seed(1)           # seed 설정
rand_t = tf.random.uniform((3, 4), minval=-2, maxval=2)
print(rand_t)

## Output
## tf.Tensor(
## [[-1.3394766   1.6059251   0.5238967  -0.26181555]
##  [-0.8322439   0.5700083   1.903142   -0.25960207]
##  [ 0.64040756  0.41958332  0.54652596  0.45779514]], shape=(3, 4), dtype=float32)
```

## **4) 원-핫 인코딩(One-Hot Encoding)**
### **`tf.one_hot(np.array/list, depth)`**

```python
oh_tensor = tf.one_hot([1, 5, 3], 5)
print(oh_tensor)

## Output
## tf.Tensor(
## [[0. 1. 0. 0. 0.]
##  [0. 0. 0. 0. 1.]
##  [0. 0. 0. 1. 0.]], shape=(3, 5), dtype=float32)
```

## **5) 희소행렬(Sparse Matrix) 생성**
### **`tf.sparse.SparseTensor(indices, values, dense_shape)`**
* 희소행렬을 효율적으로 저장할 수 있다.
* `indices`는 0이 아닌 원소의 위치,<br> `values`는 위치에 해당하는 값, <br>`dense_shape`은 희소행렬의 크기를 의미한다.

```python
t_sparse= tf.sparse.SparseTensor(indices=[[0, 0], [1, 2], [3, 3]],
                                 values=[1, 2, 3],
                                 dense_shape=[4, 5])
print(t_sparse)
print(tf.sparse.to_dense(t_sparse).numpy())

## Output
## SparseTensor(indices=tf.Tensor(
## [[0 0]
##  [1 2]
##  [3 3]], shape=(3, 2), dtype=int64), values=tf.Tensor([1 2 3], shape=(3,), dtype=int32), dense_shape=tf.Tensor([4 5], shape=(2,), dtype=int64))
##
## [[1 0 0 0 0]
##  [0 0 2 0 0]
##  [0 0 0 0 0]
##  [0 0 0 3 0]]
```

## **6) 비정형 텐서(ragged tensor) 생성**
* 축마다 원소의 개수가 다른 텐서를 비정형 텐서라고 한다. 
* shape를 보면 길이가 정해져 있지 않은 축의 경우 `None`으로 표현된다.

```python
t_ragged = tf.ragged.constant([[1, 2],
                               [3, 4, 5, 6],
                               [7],
                               [8, 9, 10]])

print(t_ragged)
print(t_ragged.shape)

## Output
## <tf.RaggedTensor [[1, 2], [3, 4, 5, 6], [7], [8, 9, 10]]>
## (4, None)
```

# **2. Tensor 조작**
## **1) 데이터 타입 변경**
### **`tf.cast(tensor, dtype)`**

```python
t_arr = tf.constant([1, 4, 6, 2, 3])
t_arr_new = tf.cast(t_arr, tf.float32)
print(t_arr)
print(t_arr_new)

## Output
## tf.Tensor([1 4 6 2 3], shape=(5,), dtype=int32)
## tf.Tensor([1. 4. 6. 2. 3.], shape=(5,), dtype=float32)
```

## **2) 데이터 크기 변경**
### **`tf.reshape(tensor, shape)`**

```python
t_arr = tf.ones((3, 4))
t_arr_reshape = tf.reshape(t_arr, (2, 6))
print(t_arr)
print(t_arr_reshape)

## Output
## tf.Tensor(
## [[1. 1. 1. 1.]
##  [1. 1. 1. 1.]
##  [1. 1. 1. 1.]], shape=(3, 4), dtype=float32)
## tf.Tensor(
## [[1. 1. 1. 1. 1. 1.]
##  [1. 1. 1. 1. 1. 1.]], shape=(2, 6), dtype=float32)
```

## **3) 데이터 전치**
### **`tf.transpose(tensor)`**

```python
t_arr = tf.zeros((2, 4))
t_arr_trans = tf.transpose(t_arr)
print(t_arr)
print(t_arr_trans)

## Output
## tf.Tensor(
## [[0. 0. 0. 0.]
##  [0. 0. 0. 0.]], shape=(2, 4), dtype=float32)
## tf.Tensor(
## [[0. 0.]
##  [0. 0.]
##  [0. 0.]
##  [0. 0.]], shape=(4, 2), dtype=float32)
```

## **4) 데이터 불필요한 차원 삭제**
### **`tf.squeeze(tensor, axis)`**

```python
t_arr = tf.zeros((1, 1, 3, 1, 7))
t_arr_squeeze = tf.squeeze(t_arr, axis=(1, 3))
print('Before'.ljust(8), t_arr.shape)
print('After'.ljust(8), t_arr_squeeze.shape)

## Output
## Before   (1, 1, 3, 1, 7)
## After    (1, 3, 7)
```

# **3. Tensor 연산**
## **1) 원소 별 연산**
### **`tf.add(), tf.subtract(), tf.multiply()`**
* 브로드캐스팅이 가능하다.
* 연산자로 바로 써도 가능하다.

```python 
t_arr1 = tf.constant([[1,2,3],[4,5,6]])
t_arr2 = tf.fill((2, 3), 3)

print(tf.add(t_arr1, t_arr2).numpy())           # t_arr1 + t_arr2
print(tf.add(t_arr1, 3))                        # Broadcasting(위와 동일하여 output 생략)
print(tf.subtract(t_arr1, t_arr2).numpy())      # t_arr1 - t_arr2
print(tf.multiply(t_arr1, t_arr2).numpy())      # t_arr1 * t_arr2


## Output
## [[4 5 6]
##  [7 8 9]]
##
## [[-2 -1  0]
##  [ 1  2  3]]
##
## [[ 3  6  9]
##  [12 15 18]]
```

## **2) 차원 축소(축에 대한 통계)**
### **`tf.math_reduce_min/max/mean/sum/std/...(tensor, axis)`**

```python
t_col = tf.math.reduce_sum(t_arr1, axis=0)      # 열 별 합 
t_row = tf.math.reduce_sum(t_arr1, axis=1)      # 행 별 합
print(t_arr1.numpy())
print(t_col)
print(t_row)

## Output
## [[1 2 3]
##  [4 5 6]]
## tf.Tensor([5 7 9], shape=(3,), dtype=int32)
## tf.Tensor([ 6 15], shape=(2,), dtype=int32)
```

## **3) norm 계산**
### **`tf.norm(tensor, ord, axis)`**
* norm : 벡터의 크기
* $L_1$ : 벡터 원소의 절댓값의 합$(\sum |x_i|)$ 
* $L_2$ : 벡터 원소의 제곱 합에 대한 제곱근$(\sqrt{\sum x_i^2})$ 

```python
t_arr = tf.random.uniform((2, 3))
t_norm1 = tf.norm(t_arr, ord=1, axis=1)
t_norm2 = tf.norm(t_arr, ord=2, axis=1)
print(t_norm1.numpy())
print(t_norm2.numpy())

## Output
## [0.9788567 2.256493 ]
## [0.60544753 1.3160946 ]
```

## **4) 행렬 곱셈**
### **`tf.linalg.matmul(tensor1, tensor2, transpose_a, transpose_b)`**

```python
X = tf.random.uniform((2, 3))

XtX = tf.linalg.matmul(X, X, transpose_b=True)
tXX = tf.linalg.matmul(X, X, transpose_a=True)
print(XtX.numpy())
print(tXX.numpy())

## Output
## [[2.288641  1.3564196]
##  [1.3564196 1.3458307]]
## [[1.6132958  1.0531735  1.2336695 ]
##  [1.0531735  0.9869349  0.64040506]
##  [1.2336695  0.64040506 1.0342408 ]]
```

### **`tensor @ tensor`**

```python
XtX = X @ X.transpose()
tXX = X.transpose() @ X
print(XtX.numpy())
print(tXX.numpy())

## Output
## [[2.288641  1.3564196]
##  [1.3564196 1.3458307]]
## [[1.6132958  1.0531735  1.2336695 ]
##  [1.0531735  0.9869349  0.64040506]
##  [1.2336695  0.64040506 1.0342408 ]]
```

### **Numpy API, `tnp.dot(tnp1, tnp2)`**

```python
import tensorflow.experimental.numpy as tnp
tnp.experimental_enable_numpy_behavior()

tn1 = tnp.array(X)
tn2 = tnp.array(X)

XtX = tnp.dot(X, X.T)
tXX = tnp.dot(X.T, X)

print(XtX.numpy())
print(tXX.numpy())

## Output
## [[2.288641  1.3564196]
##  [1.3564196 1.3458307]]
## [[1.6132958  1.0531735  1.2336695 ]
##  [1.0531735  0.9869349  0.64040506]
##  [1.2336695  0.64040506 1.0342408 ]]
```

# **4. Tensor 분할/연결**
## **1) 여러 개의 Tensor로 분할**
### **`tf.split(tensor, num_or_size_splits)`**

```python
t_arr = tf.constant([1, 2, 3, 4, 5, 6])
t_split1 = tf.split(t_arr, num_or_size_splits = 3)
t_split2 = tf.split(t_arr, num_or_size_splits = [4, 2])

print(t_arr.numpy())
print('원소 3개씩 나누기', end='> ')
for x in t_split1:
    print(x.numpy(), end=' ')
print('\n원소 4개 2개로 나누기', end='> ')
for x in t_split2:
    print(x.numpy(), end=' ')

## Output
## [1 2 3 4 5 6]
## 원소 3개씩 나누기> [1 2] [3 4] [5 6] 
## 원소 4개 2개로 나누기> [1 2 3 4] [5 6] 
```

## **2) 하나의 Tensor로 연결**
### **`tf.concat([tensor1, tensor2, ...], axis)`**

```python
A = tf.ones((3, 2))
B = tf.zeros((3, 5))
C = tf.concat([A, B], axis=1)
print(A.numpy(), B.numpy(), C.numpy(), sep='\n')

## Output
## [[1. 1.]
##  [1. 1.]
##  [1. 1.]]
## [[0. 0. 0. 0. 0.]
##  [0. 0. 0. 0. 0.]
##  [0. 0. 0. 0. 0.]]
## [[1. 1. 0. 0. 0. 0. 0.]
##  [1. 1. 0. 0. 0. 0. 0.]
##  [1. 1. 0. 0. 0. 0. 0.]]
```
