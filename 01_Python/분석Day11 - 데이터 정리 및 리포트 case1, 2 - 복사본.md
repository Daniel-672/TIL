

# 분석Day11

>  파이썬을 활용한 머신러닝 쿡북 1 ~8장 summary 및 text마이닝

### - 교육내용

# **머신러닝 관련해서 필요한 데이터 전처리**

## 사이킷런의 ML 알고리즘을 쓰려면 다음과 같은 조건에 만족되는 데이터 셋이 필요하다.

## **(1) 결측치(nan, null)값이 허용되지 않는다**

### nan(null) 값이 얼마 없으면 중앙값이나 평균값으로 대체한다

### nana(null) 값이 대다수라면 해당 피쳐값은 드롭하는 것도 좋다

### 중요도가 높은 피처는 유지시킨다

## **(2) 문자열도 허용되지 않는다.**

### 문자열이 허용되지 않기때문에, 해당 피쳐값에 대한 인코딩(숫자로 변환)이 필요하다.

### 인코딩은 카테고리형(코드 값)으로 대부분 변환시킨다.

### 필요없는 피처는 드롭한다.


## **레이블 인코딩**

### 문자열로 구성되어 있는 items 데이터를 카테코리화(코드화) 하는 것이다.


```python
from sklearn.preprocessing import LabelEncoder
items=['TV', '냉장고', '전자레인지', '컴퓨터', '선풍기', '선풍기', '믹서', '믹서']
encoder = LabelEncoder()
encoder.fit(items)

```


```python
labels = encoder.transform(items)
labels
```


```python
encoder.classes_
```


```python
encoder.inverse_transform([4, 5, 2, 0, 1, 1, 3, 3])
```

< 주의 >
하지만, 여기서의 숫자들은 숫자로서의 의미가 아닌 단순한 코드의 의미로 사용되는 것이다.
따라서 이 상태로 바로 ML에 적용하면 숫자로 변환된 변수가 가중치에 영향을 줄 수 있으니 별도의 조치를 취해주어야 한다.

## **원-핫 인코딩(One-Hot Encoding)**

### One-Hot Encoding은 dummy 변수 개념을 활용하여 새롭게 코드화 하는 방법이다.


```python
from sklearn.preprocessing import OneHotEncoder
import numpy as np
items=['TV', '냉장고', '전자레인지', '컴퓨터', '선풍기', '선풍기', '믹서', '믹서']
encoder = LabelEncoder()
encoder.fit(items)
labels = encoder.transform(items)
labels = labels.reshape(-1,1)
print(labels)
oh_encoder = OneHotEncoder()
oh_encoder.fit(labels)
oh_labels = oh_encoder.transform(labels)
print(oh_labels.toarray())
print(oh_labels.shape)
```

## **pandas의 get_dummies 기능을 활용한 인코딩**

### One-Hot Encoding으로도 인코딩이 가능하지만, pandas에서 get_dummies() 기능을 활용하면 쉽게 변환해준다.


```python
import pandas as pd
df = pd.DataFrame({'item' : ['TV', '냉장고', '전자레인지', '컴퓨터', '선풍기', '선풍기', '믹서', '믹서']})
pd.get_dummies(df)
```

# Normalization(정규화) / Standardization(표준화)

### 데이터 분석을 수행하면서 많이 겪는 문제중 하나가 데이터 단위의 불일치이다. 

### 이를 해결하는 방법으로 <span style="color:blue">Normalization(정규화)과 Standardization(표준화)</span>가 있다. 

### 이 방법들은 대표적으로 2개 이상의 대상이 단위가 다를 때 대상 데이터를 같은 

### 기준으로 볼 수 있게 해준다. 즉, 다른 데이터와 같이 분석을 할 때에도 

### 표준화 또는 정규화된 데이터를 이용하면 단위 차이 문제 등에서 벗어날 수 있다.

### **[ 정규화(normalization)]**는 다음과 같은 공식을 사용해서 특성 값의 범위를 [0, 1]로 옮긴다.

## 식 : <span style="color:red">(측정값 - 최소값) / (최대값 - 최소값)</span>

### **[표준화(Standardization)]**는 데이터를 0을 중심으로 양쪽으로 데이터를 분포시키는 방법이다. 

### 표준화를 하면 각 데이터이 평균을 기준으로 얼마나 떨여져 있는지를 나타내는 값으로 변환된다. 

## 식(Z-score 표준화) : <span style="color:red">(측정값 - 평균) / 표준편차</span>



```python
# ndarray 생성 및 type 확인

import numpy as np

a = [1,2,3,4]
print("list => {}".format(a))       # [1,2,3,4]  
print("type => {}".format(type(a))) # <class 'list'>
print("----------------------------------")

b = np.array([1,2,3,4])
print("array => {}".format(b))         # [1 2 3 4]
print("type => {}".format(type(b)))    # <class 'numpy.ndarray'>
print("b.dtype => {}".format(b.dtype)) # dtype : 배열 데이터 타입 속성
                                       # int32
print("b[0] type => {}".format(type(b[0]))) # <class 'numpy.int32'>
print("----------------------------------")

c = np.array([100,"Hello",3.141592])
print("array => {}".format(c))         # array => ['100' 'Hello' '3.141592'],  
print("type => {}".format(type(c)))    # type => <class 'numpy.ndarray'>  
print("c.dtype => {}".format(c.dtype)) # b.dtype => <U11 
print("c[0] type => {}".format(type(c[0]))) # <class 'numpy.str_'>
print("c[1] type => {}".format(type(c[1]))) # <class 'numpy.str_'>
print("c[2] type => {}".format(type(c[2]))) # <class 'numpy.str_'>
```


```python
# 다차원 ndarray와 data type 지정

import numpy as np
 
my_list = [[1,2,3], [4,5,6]]
print(my_list[1][2])
arr = np.array(my_list)

print("{}".format(arr))  # [[1 2 3]
                         #  [4 5 6]]
    
print("1행 2열의 값은 : {}".format(arr[1,2])) # 1행 2열의 값은 : 6


# ndarray 생성시 dtype 명시
# ndarray 생성 시 명시적으로 타입을 지정하지 않으면
# 데이터를 보고 적절한 타입을 알아서 지정
# 혹은 ndarray 생성 시 data type을 지정할 수 있다.

my_list = [[1,2,3], [4,5,6]]
arr = np.array(my_list, dtype=np.float64)

print("{}".format(arr))  # [[1. 2. 3.]
                         #  [4. 5. 6.]]

```


```python
# ndarray의 차원 관련 속성 : ndim, shape

import numpy as np

# 1차원
list = [1,2,3,4]
arr = np.array(list)

print("arr.ndim => {}".format(arr.ndim))   # arr.ndim => 1
print("arr.shape => {}".format(arr.shape)) # arr.shape => (4,) 튜플이라 ','가 찍힌것임. 1차원이라.. 걍 원소 개수


# 2차원
list = [[1,2],[3,4],[5,6],[7,8]]
arr = np.array(list)

print("arr.ndim => {}".format(arr.ndim))   # arr.ndim => 2
print("arr.shape => {}".format(arr.shape)) # arr.shape => (4, 2)


# 3차원 (2,2,3) 형태를 list로 만들어보자!
list = [[[1,2,3],[4,5,6]],[[7,8,9],[10,11,12]]]
arr = np.array(list)
print("arr.ndim => {}".format(arr.ndim))   # arr.ndim => 3
print("arr.shape => {}".format(arr.shape)) # arr.shape => (2, 2, 3)
print(arr)

# 4차원 (3, 2, 2, 3) 형태를 list로 만들어보자!
list = [[[[1,2,3],[4,5,6]],[[7,8,9],[10,11,12]]], [[[1,2,3],[4,5,6]],[[7,8,9],[10,11,12]]], [[[1,2,3],[4,5,6]],[[7,8,9],[10,11,12]]]]
arr = np.array(list)
print("arr.ndim => {}".format(arr.ndim))   # arr.ndim => 4
print("arr.shape => {}".format(arr.shape)) # arr.shape => (3, 2, 2, 3)
print(arr)
print("크기(size) : {}".format(arr.size))    # 배열 요소의 수 : 4
print("크기(len) : {}".format(len(arr)))     # 1차원배열길이 : 2
```


```python
# ndarray의 크기 속성과 shape 조절

import numpy as np

list = [1,2,3,4]
arr = np.array(list)

print("arr.shape => {}".format(arr.shape))   # arr.shape => (4,)
print("크기(size) : {}".format(arr.size))    # 배열 요소의 수 : 4 
print("크기(len) : {}".format(len(arr)))     # 1차원배열길이 : 4


arr.shape = 2,2    # shape 변경
print("arr.shape => {}".format(arr.shape))   # arr.shape => (2, 2)
print("크기(size) : {}".format(arr.size))    # 배열 요소의 수 : 4
print("크기(len) : {}".format(len(arr)))     # 1차원배열길이 : 2
print(arr)

arr.shape = 4,1,1  # shape 변경
print("arr.shape => {}".format(arr.shape))   # arr.shape => (4, 1, 1)
print("크기(size) : {}".format(arr.size))    # 배열 요소의 수 : 4
print("크기(len) : {}".format(len(arr)))     # 1차원배열길이 : 4  첫번째 대괄호를 벗긴 후 원소의 개수 마지막 차원의 원소 개수
print(arr)

```


```python
# astype()을 이용한 ndarray data type 변경

import numpy as np

arr = np.array([1.2, 2.5, 3.8, 4.2, 5.3])
print("arr.dtype : {}".format(arr.dtype))  # float64

arr = arr.astype(np.int32)
print("arr.dtype : {}".format(arr.dtype))  # int32
print(arr)  # [1 2 3 4 5]  소수점 이하 버림 처리
```


```python
# ndarray 다양한 생성 함수-arange

import numpy as np

# python의 range()와 유사
# 주어진 범위 내에서 지정한 간격으로 
# 연속적인 원소를 가진 배열을 생성
# np.arange(시작,끝,간격)
# 시작은 inclusive, 끝은 exclusive 

arr = np.arange(0,10,2)
print("arr의 크기 : {}".format(arr.size))
print("arr : ",arr)    # [0 2 4 6 8]

arr = np.arange(10)
print("arr의 크기 : {}".format(arr.size))
print("arr : ",arr)    # [0 1 2 3 4 5 6 7 8 9]

arr = np.arange(0.1,5.3)
print("arr의 크기 : {}".format(arr.size))
print("arr : ",arr)    # [0.1 1.1 2.1 3.1 4.1 5.1]

```


```python
# ndarray 다양한 생성 함수-linspace

import numpy as np
import matplotlib.pyplot as plt

# np.linspace(start,stop,num)
# start부터 stop의 범위에서 num개를 균일한 간격으로
# 데이터를 생성하고 배열을 만드는 함수
# 원소간 간격은 (stop-start)/(num - 1).
# num의 default값은 50

arr = np.linspace(0,10,11)
print("arr의 크기 : {}".format(arr.size))
print(arr)
plt.plot(arr,"*r")   # plt.plot()은 선그래프를 그려준다.
plt.show()

arr = np.linspace(1,121,31)
print(arr)
plt.plot(arr,"o")
plt.show()
```


```python
# ndarray 다양한 생성 함수-random 기반

# np.random.normal() : 정규분포 확률밀도에서 실수 표본추출
# np.random.rand() : [0,1)의 균등분포 확률밀도에서 실수 표본추출
# np.random.randn() : 표준정규분포(평균:0, 표준편차:1) 확률밀도에서 실수 표본추출
# np.random.randint() : 주어진 범위에서 균등분포 확률밀도에서 정수 표본추출
# np.random.random() : [0,1)의 균등분포 확률밀도에서 실수 표본추출

import numpy as np
import matplotlib.pyplot as plt
```


```python
# np.random.normal(정규 분포의 평균,표준편차,shape)
# 정규분포 확률밀도에서 실수 표본추출
# 추출된 난수는 정규분포의 형상을 가진다.

mean = 50
std = 2
arr = np.random.normal(mean,std,(10000,))
plt.hist(arr,bins=100)
plt.show()
```


```python
# np.random.rand(d0,d1,d2,...)
# 난수[0,1) 균등분포 확률 밀도에서 표본을 추출
# [](대괄호)는 이상, 이하의 의미, ()(소괄호)는 초과,미만의 의미
# 추출된 난수는 균등분포의 형상을 가진다.
arr = np.random.rand(10000)
plt.hist(arr,bins=100)
plt.show()
```


```python
########################

# np.random.randn(d0,d1,d2,...)
# 표준 정규 분포 확률 밀도에서 표본을 추출
# 추출된 난수는 정규분포의 형상을 가진다.
arr = np.random.randn(10000)
plt.hist(arr,bins=100)
plt.show()
```


```python
########################

# np.random.randint(low,high,shape)
# 균등 분포 확률 밀도에서 정수 표본을 추출
# 추출된 정수 난수는 해당 범위에서 균등 분포의 형상을 가진다.
arr = np.random.randint(-100,100,(1000,))
plt.hist(arr,bins=100)
plt.show()
```


```python
########################

# np.random.random(shape)
# [0,1) 균등 분포 확률 밀도에서 표본을 추출
# 추출된 난수는 해당 범위에서 균등 분포의 형상을 가진다.
arr = np.random.random((10000,))
plt.hist(arr,bins=100)
plt.show()
```


```python
# random 기반의 배열 생성의 재현성을 확보해보자!!
# 난수는 특정 시작 숫자로부터 난수처럼 보이는 수열을 만드는
# 알고리즘의 결과물

# 시작점을 설정하면 같은 난수를 발생시킬 수 있다. ( 난수의 재현 )
# np.random.seed(x) : 난수의 시작점을 설정하는 함수

import numpy as np

np.random.seed(1)
arr = np.random.randint(0,100,(10,))
print(arr)
```


```python
##################

# 데이터의 순서를 바꾸려면 shuffle()을 이용합니다. 

arr = np.arange(1,11)
print(arr)
np.random.shuffle(arr)   # arr의 데이터 순서를 변경
print(arr)
```


```python
# 데이터 집합에서 일부를 무작위로 선택하는 샘플링(sampling)을 
# 수행하려면 choice()를 이용합니다. 

# numpy.random.choice(a, size=None, replace=True, p=None)

# a : 배열 혹은 정수
#     만약 정수면 arange(a) 명령으로 데이터 생성
# size : 정수. 샘플 숫자
# replace : True이면 한번 선택한 데이터를 다시 선택 할 수 있음.
# p : ndarray. 각 데이터가 선택될 수 있는 확률을 명시.

#arr = np.random.choice(5, 3, replace=False)
arr = np.random.choice(5, 10)
#arr = np.random.choice(5, 10, p=[0.1, 0, 0.3, 0.6, 0])



```


```python
win = [14, 3, 42, 13, 28, 12]

for cnt in range(1000000) :
    lotto = np.random.choice(np.arange(1, 46), 6, replace=False)
    makeNum = 0
    for chk in win :
        for num in lotto :
            # print(chk, num)            
            if chk == num :
                makeNum = makeNum + 1
                # print('ㅋ', makeNum)
    if makeNum == 6 :
        print('헐!!', cnt, '회', 'win', win, 'lotto', lotto, '맞춘번호숫자', makeNum)
        break
```


```python
# ndarray shape 조절 함수 - reshape

import numpy as np

arr = np.arange(0,12,1)
print(arr)

# 배열의 데이터는 공유하지만 shape이 다른 뷰(View)를 생성
arr1 = arr.reshape(4,3)
print(arr1)

# 데이터가 공유되기 때문에 배열을 변경하면 다른 View에도
# 영향을 미침
# 데이터를 공유하는지 확인

arr[4] = 100
print(arr)
print(arr1)
```


```python
#######################

# base 속성을 이용하면 현재의 View의 데이터가 어떤 객체의 
# 데이터 인지를 알 수 있다.

print(arr1.base)

if arr1.base is arr:
    print("데이터 공유!!")
```


```python
#######################

# reshape()을 사용할 때 차원 하나를 -1로 설정하면 
# 배열의 전체 원소 개수와 확정된 차원 크기로 부터 
# 남은 차원의 크기를 추론하여 배열을 생성

arr = np.arange(0,12,1)

arr1 = arr.reshape(4,-1)
print(arr1)

```


```python
#######################

# View를 생성하지 않으려면 copy()를 이용하여 새로운
# array 생성

arr2 = arr.reshape(4,3).copy()

```


```python
# ndarray shape 조절 함수 - ravel

import numpy as np

# ravel() : 배열의 모든 원소가 포함된 1차원 배열을 리턴
# ravel() 역시 View를 return

arr = np.arange(0,100,1).reshape(5,-1).copy()
print(arr)


arr1 = arr.ravel() 
print(arr1)
```


```python
# ndarray shape 조절 함수 - resize

# resize()는 reshape()과 유사한 기능을 수행.
# 단, reshape()는 배열 요소 수를 변경하지 않는반면 resize()는
# shape을 변경하는 과정에서 배열 요소 수가 변할 수 있다.

import numpy as np

np.random.seed(1)

arr = np.random.randint(0,10,(3,4))
print(arr)

# resize()를 호출하는 방식에 따라서 원본 변경 혹은
# 결과 배열이 리턴된다.
# resize()는 reshape()과는 다르게 View를 생성하지 않는다.

print(np.resize(arr,(2,6))) # 새로운 배열 생성
                            # View 생성이 아님
print(arr)

print(arr.resize(2,6)) # return 없음. 원본 변경
print(arr)

arr.resize(3,5)  # 요소수가 늘어나면 0으로 세팅
print(arr)

arr.resize(2,2)  # 요소수가 줄면 기존 데이터를 버린다.
print(arr)

```


```python
# ndarray indexing & slicing

import numpy as np

arr = np.arange(10,20,1)

# ndarray는 python list처럼 indexing과 slicing이 가능

for idx,data in enumerate(arr):
    print("index : {}, data : {}".format(idx,data))
    
# ndarray를 slicing한 결과는 View이기 때문에 
# 원본 데이터가 변경되면 View의 데이터도 변경됨을 기억하자.

arr = np.arange(0,5,1)
print(arr)
print(arr[0])
print(arr[0:1])
print(arr[0:2])
print(arr[1:-1])
print(arr[0::2])  # 첫번째 원소부터 2씩 건너띄며 원소를 슬라이싱
print(arr[1:4:2])

print(arr[[0,2,4]])
```


```python
# 2차원 ndarray의 indexing & slicing

arr = np.array([[1,2,3,4],
                [5,6,7,8],
                [9,10,11,12],
                [13,14,15,16]])
print(arr[1,1])
print(arr[2,:])     # 2차원 이상인 경우 
                    # ","를 기준으로 인덱싱을 해야 한다.
print(arr[1:3,:]) 
print(arr[:,2])
print(arr[1:3,:2])

```


```python
# ndarray Boolean indexing & Fancy indexing

# boolean indexing은 배열의 각 요소의 선택여부를 
# True,False로 구성된 boolean mask를 이용하여 
# 지정하는 방식으로 boolean mask의 True 요소에 해당하는 
# index만을 조회.

import numpy as np

np.random.seed(1)
arr = np.random.randint(0,10,(10,))

print(arr)
print(arr % 2 == 0)       # mask 생성
print(arr[arr % 2 == 0])  # boolean indexing

```


```python
##################################

# Fancy Indexing

# 배열에 index 배열을 전달하여 배열요소를 참조하는 방식

import numpy as np

arr = np.arange(0,12,1).reshape(3,4).copy()
print(arr)

print(arr[2,2])       # indexing : 10
print(arr[1:2,2])     # slicing : [6]
print(arr[1:2,1:2])   # slicing : [[5]]

print(arr[[0,2],2])   # fancy indexing : [2 10]
print(arr[[0,2],2:3]) # [[ 2]
                      #  [10]]

print(arr[:,[0,2]])   # fancy indexing  
                      # [[ 0  2]
                      #  [ 4  6]
                      #  [ 8 10]]
    
print(arr[[0,2],[0,2]]) # ?? 생각처럼 나오지 않는다.
                        # 슬라이싱처럼 fancy indexing 적용 안됨
    
# 방법 1
# 행을 먼저 추출한 후 해당 행에 대해 fancy indexing을 적용

print(arr[[0,2]][:,[0,2]])  # [[ 0  2]
                            #  [ 8 10]]

# 방법 2
# numpy의 ix_() 함수를 이용

print(arr[np.ix_([0,2],[0,2])]) # [[ 0  2]
                                # [ 8 10]]
```


```python
# ndarray 사칙연산과 행렬곱

import numpy as np

arr1 = np.array([[1,2,3],[4,5,6]])            # 2 x 3 ndarray
arr2 = np.arange(10,16,1).reshape(2,3).copy() # 2 x 3 ndarray
arr3 = np.arange(10,16,1).reshape(3,2).copy() # 3 x 2 ndarray

# 같은 크기의 배열 간의 연산은 
# 같은 위치에 있는 원소 간의 연산으로 결과가 계산

print(arr1 + arr2)  # np.add(arr1,arr2)
print(arr1 - arr2)  # np.subtract(arr1,arr2)
print(arr1 * arr2)  # np.multiply(arr1,arr2)
print(arr1 / arr2)  # np.divide(arr1,arr2)

# 두 행렬간의 행렬곱은 np.matmul() 혹은 np.dot()으로 수행가능
# np.dot(A,B)에서 A 행렬의 열 vector와 B 행렬의 행 vector의 size가 같아야 한다.
# 그렇지 않으면 이전에 배운 reshape이나 전치행렬을 이용하여 형 변환 후 크기를
# 맞추고 연산을 수행해야 한다.

print("행렬곱 : ", np.matmul(arr1,arr3))  # np.dot(arr1,arr3)


# 이런 행렬곱을 왜 알아야 할까?
# 행렬곱이 없다면 matrix연산은 무조건 같은 크기의 사칙연산만을 수행할 수 있다.
# 하지만 행렬곱을 이용하면 
# 행렬곱 조건을 만족하는 다양한 크기의 행렬을 이용하여 연속적으로
# 행렬곱을 수행시킬 수 있기 때문.
# 이러한 특성이 Machine Learning과 Image processing에서 자주 사용된다.

# 예) 입력 : 32 x 32 matrix (image라고 가정)
#     출력 : 32 x 10 matrix (다양한 처리가 적용된 image)
#     행렬곱 : (32 x 32) dot (32 x 128) dot (128,64) dot (64 x 10) => 32 x 10

# 위의 예처럼 행렬곱 특성을 이용하면 다양한 크기의 행렬을 이용하여 원본 데이터를
# 변경시키는 것이 가능. 만약 행렬곱이 없고 사칙연산만 수행할 수 있다면
# 32 x 32 형태의 크기를 가지는 특성(행렬)만 이용할 수 있기 때문에 
# 다양한 특성을 가지는 필터 개발이 불가능하다.
```


```python
# ndarray broadcasting

# shape이 다른 경우 두 배열에 대한 이항연산은 두 배열간의 shape을
# 맞추는 broadcasting과정을 거친 후 수행된다.
# 가장 일반적인 경우는 배열과 scalar의 연산

import numpy as np

arr1 = np.array([[1,2,3],[4,5,6]])   # 2 x 3 ndarray
arr2 = np.array([7,8,9])             # 1차원 ndarray 
print(arr1)
print(arr2)
print(arr1 + arr2)  # arr2를 2차배열로 broadcasting

arr1 = np.array([[1,2,3],[4,5,6]])
# arr2 = np.array([[1,2],[4,5]])
arr2 = np.array([[1],[4]])
print(arr1 + arr2)  # broadcasting이 일어날 수 없다. Error 발생

print(np.dot(arr1, arr2))
# 주의!!
# 이런 ndarray의 broadcasting은 사칙연산에 한해서 일어나게 된다.
# 즉, 행렬곱 연산에 대해서는 broadcasting이 발생하지 않는다.
```


```python
# ndarray transpose

# 일반적으로 전치행렬이라고 불리는 transpose에 대해서 알아보자.
# 전치행렬은 원본 행렬의 행은 열로, 열은 행으로 바꾼 행렬을 의미
# 전치행렬의 수학적 표현은 윗첨자 T를 이용해서 표현한다. 
# ndarray의 T 속성을 이용하면 전치행렬을 구할 수 있다.(View)

import numpy as np

arr = np.array([[1,2,3],[4,5,6]])   # 2 x 3 ndarray

arr_transpose = arr.T

print(arr)
print(arr_transpose)

arr[0,0] = 100

print(arr)
print(arr_transpose)   # 전치행렬 또한 View

# Vector에 대한 transpose

arr = np.array([1, 2, 3, 4])
arr_transpose = arr.T    

print(arr)
print(arr_transpose)   # vector에 대한 전치행렬은 의미없음.

# 만약 전치행렬을 구하고 싶으면 2차원 matrix로 변환한 후 수행해야 한다.

arr_transpose = arr.reshape(1,4).T
arr[0] = 101
print(arr_transpose)
```


```python
# ndarray iterator

# ndarray의 모든 원소를 access하는 경우에 일반적으로 iterator를 이용.
# iternext()와 finished 속성을 이용하여 ndarray의 모든 요소들을 순차적으로
# access 할 수 있다.

import numpy as np

# 1차원 ndarray에 대한 요소 출력
arr = np.array([1, 2, 3, 4, 5])

for tmp in arr:
    print(tmp, end=' ')
print('\n')
####################################    

# 1차원 ndarray에 대한 iterator

arr = np.array([1, 2, 3, 4, 5])

it = np.nditer(arr, flags=['c_index'])

while not it.finished:
    
    idx = it.index
    
    print(arr[idx], end=' ')
    
    it.iternext()
```


```python
####################################

# 2차원 ndarray에 대한 요소 출력
arr = np.array([[1,2,3], [4,5,6]])

for tmp1 in range(arr.shape[0]):
    for tmp2 in range(arr.shape[1]):
        print(arr[tmp1,tmp2], end=' ')
        
```


```python
####################################    

# 2차원 ndarray에 대한 iterator

arr = np.array([[1,2,3], [4,5,6]])

it = np.nditer(arr, flags=['multi_index'])

while not it.finished:
    
    idx = it.multi_index
    print(idx)
    print(arr[idx], end=' ')
    
    it.iternext()        
```


```python
# 사칙연산과 마찬가지로 비교연산도 같은 index의 
# 요소들끼리 수행된다.

import numpy as np

arr1 = np.random.randint(0,10,(2,3))
arr2 = np.random.randint(0,10,(2,3))

print(arr1)
print(arr2)


print(arr1 == arr2) # 논리 연산의 결과는 boolean
print(arr1 > arr2)

#######################

# 2개의 ndarray 자체가 같은 데이터를 가지고 있는지
# 비교할 때는 array_equal()을 사용한다.

arr1 = np.arange(10)
arr2 = np.arange(10)

print(arr1)
print(arr2)

print(np.array_equal(arr1, arr2)) # 두 배열 전체 비교
```


```python
# NumPy 함수와 axis

import numpy as np
import matplotlib.pyplot as plt

arr = np.arange(1,7,1).reshape(2,3).copy()
print(arr)

print(np.sum(arr))        # 합, arr.sum()
print(np.cumsum(arr))     # 누적합, arr.cumsum()
print(np.mean(arr))       # 평균, arr.mean()
print(np.max(arr))        # 최대값, arr.max() 
print(np.min(arr))        # 최소값, arr.min()
print(np.argmax(arr))     # 최대값의 index => 5
print(np.argmin(arr))     # 최소값의 index => 0
print(np.std(arr))        # 표준편차, arr.std() 
print(np.sqrt(arr))       # 제곱근
print(np.exp(arr))        # 자연상수의 제곱값 (자연상수 e = 2.7182...)
print(np.log10(arr))      # 상용 log의 값
print(np.log(arr))        # 자연 log의 값 (자연상수 e = 2.7182...)

print(np.log10(100))      # 상용로그 
print(np.log(2.7182))     # 자연로그 

arr = np.arange(1,10000,1)
arr1 = np.log10(arr)
print(arr1)

plt.plot(arr1)
plt.show()

```


```python
# NumPy의 모든 집계함수는 axis를 기준으로 계산.
# 만약 axis를 지정하지 않으면 axis는 None으로 간주하고
# 대상범위를 전체 행렬로 지정

import numpy as np

arr1 = np.array([1,2,3,4,5])
print(arr1.sum(axis=0)) # 1차원에서 axis=0은 열방향
#print(arr1.sum(axis=1)) # 1차원에서 axis=1은 error

arr1 = np.array([[1,2,3],[4,5,6],[7,8,9]])
print(arr1)
print(arr1.sum()) # axis=None, 전체배열대상 => 45
print(arr1.sum(axis=0)) # 2차원에서 axis=0은 행방향, np.sum(arr1,axis=0)
print(arr1.sum(axis=1)) # 2차원에서 axis=1은 열방향, np.sum(arr1,axis=1)
print(arr1.argmax(axis=1)) # 열방향으로 최대값의 index => [2 2 2]

arr1 = np.random.randint(0,5,(2,2,3))
print(arr1)
print(arr1.sum(axis=0)) # 3차원에서 axis=0은 depth방향
```


```python
# Boolean Mask 활용

import numpy as np

arr = np.array([[1,2,3,4],
                [5,6,7,8],
                [9,10,11,12],
                [13,14,15,16]])

# ndarray arr안에 10보다 큰 수가 몇개있는지 알아보려면
# 어떻게 해야 하는가?
# 여러가지 방법이 있지만 가장 쉽고 빠른 방법은 
# boolean indexing을 이용하는 방법

# arr > 10 => boolean mask
# True는 1로, False는 0으로 간주된다는 것을 기억하자.

(arr > 10).sum()    # 조건을 만족하는 개수(True의 개수)

```


```python
# ndarray 정렬

# NumPy의 array는 axis를 기준으로 정렬하는 sort() 제공
# 만약 axis를 지정하지 않으면 -1, 
# -1의 의미는 마지막 axis
# np.sort() : 정렬된 결과 배열을 return
# arr.sort() : 원본배열을 정렬. None return

import numpy as np

arr = np.arange(10)
np.random.shuffle(arr)      # shuffle 처리
print(arr)

print(np.sort(arr))         # 오름차순 정렬한 새로운 배열 return
print(np.sort(arr)[::-1])   # 내림차순 정렬, 특수한 indexing이용
print(arr)                  # 원본은 변함없음

arr = np.random.randint(0,10,(3,3))
print(arr)
print(np.sort(arr, axis=0))

```


```python
#################################

# 2차원 배열 정렬
import numpy as np

arr = np.array([[10,2,12,4],
                [15,16,3,8],
                [9,1,11,7],
                [13,14,5,6]])

print(arr)
print(np.sort(arr,axis=0))    # 행 방향 정렬
print(np.sort(arr,axis=1))    # 열 방향 정렬

# 표준정규분포에서 
# 200개의 샘플을 추출한 후 
# 내림차순으로 상위 5%까지의 결과만 출력하세요!!

arr = np.random.randn(200)
print(len(arr))
result = np.sort(arr)[::-1][:int(0.05 * len(arr))]
print(result)
```


```python
# NumPy concatenate() 함수

# ndarray에 row(s) 또는 column(s)을 추가하기 위한 함수

import numpy as np

arr = np.array([[1,2,3], [4,5,6]])

new_row = np.array([7,8,9])

result = np.concatenate((arr, new_row.reshape(1,3)), axis=0)

print(result)
```


```python
######################################

arr = np.array([[1,2,3], [4,5,6]])

new_col = np.array([7,8,9,10])

result = np.concatenate((arr,new_col.reshape(2,2)), axis=1)

print(result)


```


```python
# ndarray delete() 함수

# delete() 함수는 axis를 기준으로 행과 열을 삭제
# axis를 지정하지 않으면 1차배열로 변환 후 삭제
# 원본배열을 변경하지 않고 새로운 배열 return

import numpy as np

arr = np.random.randint(0,10,(3,4))
print(arr)

#####################

result = np.delete(arr, 1)  # 1차 배열로 변환 후 1번 index 삭제
print(result)

#####################

result = np.delete(arr,1, axis=0)  # 1번 행 삭제
print(result)

#####################

result = np.delete(arr,3, axis=1)  # 3번 열 삭제
print(result)

```



```python
# 라이브러리를 임포트합니다.
import numpy as np
```


```python
np.__version__
```




    '1.19.1'




```python
# 하나의 행으로 벡터를 만듭니다.
vector_row = np.array([1, 2, 3])
vector_row
```




    array([1, 2, 3])




```python
# 하나의 열로 벡터를 만듭니다.
vector_column = np.array([[1],
                          [2],
                          [3]])
vector_column
```




    array([[1],
           [2],
           [3]])




```python
# 넘파이 배열의 클래스를 출력합니다.
print(type(vector_row))
```

    <class 'numpy.ndarray'>



```python
# ndarray를 사용하는 것은 권장되지 않습니다.
bad_way = np.ndarray((3,))
new_row = np.asarray([1, 2, 3])
# asarray()는 새로운 배열을 만들지 않습니다.
new_row = np.asarray(vector_row)
new_row is vector_row
```




    True




```python
# array()는 배열이 입력되면 새로운 배열을 만듭니다.
new_row = np.array(vector_row)
new_row is vector_row
```


```python
# copy() 메서드를 사용하면 의도가 분명해집니다.
new_row = vector_row.copy()
new_row is vector_row
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

matrix = np.array([[1, 2],
                   [1, 2],
                   [1, 2]])
matrix
```


```python
matrix_object = np.mat([[1, 2],
                        [1, 2],
                        [1, 2]])
matrix_object
```


```python
# 임의의 값이 채워진 배열을 만듭니다.
empty_matrix = np.empty((3, 2))
empty_matrix
```


```python
zero_matrix = np.zeros((3, 2))
zero_matrix
```


```python
one_matrix = np.ones((3, 2))
one_matrix
```


```python
# 0 행렬을 만든 후 7을 더합니다.
seven_matrix = np.zeros((3, 2)) + 7
# full() 함수를 사용하는 것이 효율적입니다.
seven_matrix = np.full((3, 2), 7)
seven_matrix
```


```python
# 라이브러리를 임포트합니다.
import numpy as np
from scipy import sparse

# 행렬을 만듭니다. 
matrix = np.array([[0, 0],
                   [0, 1],
                   [3, 0]])

# CSR 행렬을 만듭니다.
matrix_sparse = sparse.csr_matrix(matrix)
# 희소 행렬을 출력합니다.
print(matrix_sparse)
```


```python
# 큰 행렬을 만듭니다.
matrix_large = np.array([[0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
                         [0, 1, 0, 0, 0, 0, 0, 0, 0, 0],
                         [3, 0, 0, 0, 0, 0, 0, 0, 0, 0]])

# CSR 행렬을 만듭니다.
matrix_large_sparse = sparse.csr_matrix(matrix_large)

# 원래 희소 행렬을 출력합니다.
print(matrix_sparse)
```


```python
# 큰 희소 행렬을 출력합니다.
print(matrix_large_sparse)
```


```python
# (data, (row_index, col_index))로 구성된 튜플을 전달합니다.
# shape 매개변수에서 0을 포함한 행렬의 전체 크기를 지정합니다.  
matrix_sparse_2 = sparse.csr_matrix(([1, 3], ([1, 2], [1, 0])), shape=(3, 10))

print(matrix_sparse_2)
```


```python
print(matrix_sparse_2.toarray())
```


```python
matrix_sparse_2.todense()
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

# 행 벡터를 만듭니다.
vector = np.array([1, 2, 3, 4, 5, 6])

# 행렬을 만듭니다.
matrix = np.array([[1, 2, 3],
                   [4, 5, 6],
                   [7, 8, 9]])

# vector의 세 번째 원소를 선택합니다.
vector[2]
```


```python
# matrix의 두 번째 행, 두 번째 열의 원소를 선택합니다.
matrix[1,1]
```


```python
# 벡터에 있는 모든 원소를 선택합니다.
vector[:]
```


```python
# 세 번째 원소를 포함하여 그 이전의 모든 원소를 선택합니다.
vector[:3]
```


```python
# 세 번째 이후의 모든 원소를 선택합니다.
vector[3:]
```


```python
# 마지막 원소를 선택합니다.
vector[-1]
```


```python
# 행렬에서 첫 번째 두 개의 행과 모든 열을 선택합니다.
matrix[:2,:]
```


```python
# 모든 행과 두 번째 열을 선택합니다.
matrix[:,1:2]
```


```python
# 첫 번째 행과 세 번째 행을 선택합니다.
matrix[[0,2]]
```


```python
# (0, 1), (2, 0) 위치의 원소를 선택합니다.
matrix[[0,2], [1,0]]
```


```python
# matrix의 각 원소에 비교 연산자가 적용됩니다.
mask = matrix > 5

mask
```


```python
# 불리언 마스크 배열을 사용하여 원소를 선택합니다.
matrix[mask]
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

# 행렬을 만듭니다.
matrix = np.array([[1, 2, 3, 4],
                   [5, 6, 7, 8],
                   [9, 10, 11, 12]])

# 행렬의 크기를 확인합니다.
matrix.shape
```


```python
# 행렬의 원소 개수를 확인합니다(행 * 열).
matrix.size
```


```python
# 차원 수를 확인합니다.
matrix.ndim
```


```python
# 원소의 데이터 타입을 확인합니다.
print(matrix.dtype)
```


```python
# 원소 하나가 차지하는 바이트 크기입니다. 
print(matrix.itemsize)
```


```python
# 배열 전체가 차지하는 바이트 크기입니다.
print(matrix.nbytes)
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

# 행렬을 만듭니다.
matrix = np.array([[1, 2, 3],
                   [4, 5, 6],
                   [7, 8, 9]])

# 100을 더하는 함수를 만듭니다.
add_100 = lambda i: i + 100

# 벡터화된 함수를 만듭니다.
vectorized_add_100 = np.vectorize(add_100)

# 행렬의 모든 원소에 함수를 적용합니다.
vectorized_add_100(matrix)
```


```python
# 모든 원소에 100을 더합니다.
matrix + 100
```


```python
# (3, 3) 크기 행렬에 (3, ) 벡터를 더하면 
# (1, 3) 크기가 된다음 행을 따라 반복됩니다.
matrix + [100, 100, 100]
```


```python
# (3, 3) 크기 행렬에 (3, 1) 벡터를 더하면 열을 따라 반복됩니다.
matrix + [[100], [100], [100]]
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

# 행렬을 만듭니다.
matrix = np.array([[1, 2, 3],
                   [4, 5, 6],
                   [7, 8, 9]])

# 가장 큰 원소를 반환합니다.
np.max(matrix)
```


```python
# 가장 작은 원소를 반환합니다.
np.min(matrix)
```


```python
# 각 열에서 최댓값을 찾습니다.
np.max(matrix, axis=0)
```


```python
# 각 행에서 최댓값을 찾습니다.
np.max(matrix, axis=1)
```


```python
# 이전 예와 달리 (3, 1) 크기의 열 벡터가 만들어 집니다.
vector_column = np.max(matrix, axis=1, keepdims=True)

vector_column
```


```python
# 열 벡터이므로 브로드캐스팅을 이용하여 각 행의 최댓값을 뺄 수 있습니다.
matrix - vector_column
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

# 행렬을 만듭니다.
matrix = np.array([[1, 2, 3],
                   [4, 5, 6],
                   [7, 8, 9]])

# 평균을 반환합니다.
np.mean(matrix)
```


```python
# 분산을 반환합니다.
np.var(matrix)
```


```python
# 표준 편차를 반환합니다.
np.std(matrix)
```


```python
# 각 열의 평균을 계산합니다.
np.mean(matrix, axis=0)
```


```python
np.std(matrix, ddof=1)
```


```python
import pandas as pd

df = pd.DataFrame(matrix.flatten())
df.std()
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

# 4x3 행렬을 만듭니다.
matrix = np.array([[1, 2, 3],
                   [4, 5, 6],
                   [7, 8, 9],
                   [10, 11, 12]])

# 2x6 행렬로 크기를 바꿉니다.
matrix.reshape(2, 6)
```


```python
matrix.size
```


```python
matrix.reshape(1, -1)
```


```python
matrix.reshape(12)
```


```python
matrix.reshape(-1)
```


```python
matrix.ravel()
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

# 행렬을 만듭니다.
matrix = np.array([[1, 2, 3],
                   [4, 5, 6],
                   [7, 8, 9]])

# 행렬을 전치합니다.
matrix.T
```


```python
# 벡터를 전치합니다.
np.array([1, 2, 3, 4, 5, 6]).T
```


```python
# 행 벡터를 전치합니다.
np.array([[1, 2, 3, 4, 5, 6]]).T
```


```python
matrix.transpose()
```


```python
# 2x3x2 행렬을 만듭니다.
matrix = np.array([[[ 1,  2],
                    [ 3,  4],
                    [ 5,  6]],

                   [[ 7,  8],
                    [ 9, 10],
                    [11, 12]]])

# 두 번째와 세 번째 차원을 바꾸어 2x2x3 행렬로 만듭니다.
matrix.transpose((0, 2, 1))
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

# 행렬을 만듭니다.
matrix = np.array([[1, 2, 3],
                   [4, 5, 6],
                   [7, 8, 9]])

# 행렬을 펼칩니다.
matrix.flatten()
```


```python
matrix.reshape(1, -1)
```


```python
vector_reshaped = matrix.reshape(-1)
vector_flattened = matrix.flatten()

# (0, 0) 위치의 원소를 바꿉니다.
matrix[0][0] = -1

# 배열의 뷰는 원본 배열의 변경 사항을 반영합니다.
vector_reshaped
# 복사된 배열에는 영향이 미치지 않습니다.
vector_flattened
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

# 행렬을 만듭니다.
matrix = np.array([[1, 1, 1],
                   [1, 1, 10],
                   [1, 1, 15]])

# 행렬의 랭크를 반환합니다.
np.linalg.matrix_rank(matrix)
```

넘파이 0.18 버전에서 `rank()` 함수가 삭제되었습니다. 대신 `ndim()` 함수를 사용하세요.


```python
# 2D 배열이므로 2가 반환됩니다.
np.ndim(matrix)
```


```python
# svd 함수로 특잇값만 계산합니다.
s = np.linalg.svd(matrix, compute_uv=False)
# 오차를 고려하여 0에 가까운 아주 작은 값을 지정합니다.
np.sum(s > 1e-10)
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

# 행렬을 만듭니다.
matrix = np.array([[1, 2, 3],
                   [2, 4, 6],
                   [3, 8, 9]])

# 행렬의 행렬식을 반환합니다.
np.linalg.det(matrix)
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

# 행렬을 만듭니다.
matrix = np.array([[1, 2, 3],
                   [2, 4, 6],
                   [3, 8, 9]])

# 대각 원소를 반환합니다.
matrix.diagonal()
```


```python
# 반환된 배열을 변경하려면 복사해야 합니다.
a = matrix.diagonal().copy()
```


```python
a = np.diag(matrix)
print(a)
```


```python
# 1차원 배열이 주어지면 2차원 대각행렬을 만듭니다.
np.diag(a)
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

# 행렬을 만듭니다.
matrix = np.array([[1, 2, 3],
                   [2, 4, 6],
                   [3, 8, 9]])

# 대각합을 반환합니다.
matrix.trace()
```


```python
# 대각 원소를 사용하여 합을 구합니다.
sum(matrix.diagonal())
```


```python
# 주 대각선 하나 위의 대각 원소의 합을 반환합니다.
matrix.trace(offset=1)
```


```python
# 주 대각선 하나 아래의 대각 원소의 합을 반환합니다.
matrix.trace(offset=-1)
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

# 행렬을 만듭니다.
matrix = np.array([[1, -1, 3],
                   [1, 1, 6],
                   [3, 8, 9]])

# 고윳값과 고유벡터를 계산합니다.
eigenvalues, eigenvectors = np.linalg.eig(matrix)
# 고윳값을 확인합니다.
eigenvalues
# 고유벡터를 확인합니다.
eigenvectors
```


```python
# 대칭 행렬을 만듭니다.
matrix = np.array([[1, -1, 3],
                   [-1, 1, 6],
                   [3, 6, 9]])

# 고윳값과 고유벡터를 계산합니다.
eigenvalues, eigenvectors = np.linalg.eigh(matrix)
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

# 두 벡터를 만듭니다.
vector_a = np.array([1,2,3])
vector_b = np.array([4,5,6])

# 점곱을 계산합니다.
np.dot(vector_a, vector_b)
```


```python
scalar_a = np.array(1)
scalar_b = np.array(2)
```


```python
np.dot(scalar_a, scalar_b)
```


```python
# 스칼라 배열에 적용되지 않습니다.
scalar_a @ scalar_b
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

# 행렬을 만듭니다.
matrix_a = np.array([[1, 1, 1],
                     [1, 1, 1],
                     [1, 1, 2]])

# 행렬을 만듭니다.
matrix_b = np.array([[1, 3, 1],
                     [1, 3, 1],
                     [1, 3, 8]])

# 두 행렬을 더합니다.
np.add(matrix_a, matrix_b)
```


```python
# 두 행렬을 뺍니다.
np.subtract(matrix_a, matrix_b)
```


```python
# 두 행렬을 더합니다.
matrix_a + matrix_b
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

# 행렬을 만듭니다.
matrix_a = np.array([[1, 1],
                     [1, 2]])

# 행렬을 만듭니다.
matrix_b = np.array([[1, 3],
                     [1, 2]])

# 두 행렬을 곱합니다.
np.dot(matrix_a, matrix_b)
```


```python
# 두 행렬을 곱합니다.
matrix_a @ matrix_b
```


```python
# 두 행렬의 원소별 곱셈을 수행합니다.
matrix_a * matrix_b
```


```python
a = np.random.rand(2, 1, 4, 5)
b = np.random.rand(1, 3, 5, 6)

np.dot(a, b).shape
```


```python
np.matmul(a, b).shape
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

# 행렬을 만듭니다.
matrix = np.array([[1, 4],
                   [2, 5]])

# 역행렬을 계산합니다.
np.linalg.inv(matrix)
```


```python
# 행렬과 역행렬을 곱합니다.
matrix @ np.linalg.inv(matrix)
```


```python
matrix = np.array([[1, 4, 7],
                   [2, 5, 8]])

# 유사 역행렬을 계산합니다.
np.linalg.pinv(matrix)
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

# 초깃값을 지정합니다.
np.random.seed(0)

# 0.0과 1.0 사이에서 세 개의 실수 난수를 생성합니다.
np.random.random(3)
```


```python
# 1과 10 사이에서 세 개의 정수 난수를 생성합니다.
np.random.randint(0, 11, 3)
```


```python
# 평균이 0.0이고 표준 편차가 1.0인 정규 분포에서 세 개의 수를 뽑습니다.
np.random.normal(0.0, 1.0, 3)
```


```python
# 평균이 0.0이고 스케일이 1.0인 로지스틱 분포에서 세 개의 수를 뽑습니다.
np.random.logistic(0.0, 1.0, 3)
```


```python
# 1.0보다 크거나 같고 2.0보다 작은 세 개의 수를 뽑습니다.
np.random.uniform(1.0, 2.0, 3)
```


```python
# 0.0(포함)과 1.0 사이에서 세 개의 실수 난수를 생성합니다.
# np.random.random((2, 3)), np.random.sample((2, 3)), 
# np.random.uniform(0.0, 1.0, (2, 3))과 동일합니다.
np.random.random_sample((2, 3))
```


```python
# np.random.random_sample((2, 3))과 동일합니다.
np.random.rand(2, 3)
```


```python
np.random.randint(0, 1, 10)
```


```python
# np.random.normal(0.0, 1.0, (2, 3))과 동일합니다.
np.random.standard_normal((2, 3))
```


```python
# np.random.normal(0.0, 1.0, (2, 3))과 동일합니다.
np.random.randn(2, 3)
```


```python
# 0~2 사이의 정수 중 랜덤하게 10번을 뽑습니다.
# np.random.choice(3, 5)와 동일합니다.
np.random.choice([0,1,2], 5)
```


```python
a = np.array([0, 1, 2, 3, 4])
np.random.shuffle(a)
a
```


```python
# a는 변경되지 않습니다.
np.random.permutation(a)
```


```python
np.random.permutation(5)
```



```python
# 라이브러리를 임포트합니다.
import numpy as np
```


```python
np.__version__
```




    '1.19.1'




```python
# 하나의 행으로 벡터를 만듭니다.
vector_row = np.array([1, 2, 3])
vector_row
```




    array([1, 2, 3])




```python
# 하나의 열로 벡터를 만듭니다.
vector_column = np.array([[1],
                          [2],
                          [3]])
vector_column
```




    array([[1],
           [2],
           [3]])




```python
# 넘파이 배열의 클래스를 출력합니다.
print(type(vector_row))
```

    <class 'numpy.ndarray'>



```python
# ndarray를 사용하는 것은 권장되지 않습니다.
bad_way = np.ndarray((3,))
new_row = np.asarray([1, 2, 3])
# asarray()는 새로운 배열을 만들지 않습니다.
new_row = np.asarray(vector_row)
new_row is vector_row
```




    True




```python
# array()는 배열이 입력되면 새로운 배열을 만듭니다.
new_row = np.array(vector_row)
new_row is vector_row
```


```python
# copy() 메서드를 사용하면 의도가 분명해집니다.
new_row = vector_row.copy()
new_row is vector_row
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

matrix = np.array([[1, 2],
                   [1, 2],
                   [1, 2]])
matrix
```


```python
matrix_object = np.mat([[1, 2],
                        [1, 2],
                        [1, 2]])
matrix_object
```


```python
# 임의의 값이 채워진 배열을 만듭니다.
empty_matrix = np.empty((3, 2))
empty_matrix
```


```python
zero_matrix = np.zeros((3, 2))
zero_matrix
```


```python
one_matrix = np.ones((3, 2))
one_matrix
```


```python
# 0 행렬을 만든 후 7을 더합니다.
seven_matrix = np.zeros((3, 2)) + 7
# full() 함수를 사용하는 것이 효율적입니다.
seven_matrix = np.full((3, 2), 7)
seven_matrix
```


```python
# 라이브러리를 임포트합니다.
import numpy as np
from scipy import sparse

# 행렬을 만듭니다. 
matrix = np.array([[0, 0],
                   [0, 1],
                   [3, 0]])

# CSR 행렬을 만듭니다.
matrix_sparse = sparse.csr_matrix(matrix)
# 희소 행렬을 출력합니다.
print(matrix_sparse)
```


```python
# 큰 행렬을 만듭니다.
matrix_large = np.array([[0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
                         [0, 1, 0, 0, 0, 0, 0, 0, 0, 0],
                         [3, 0, 0, 0, 0, 0, 0, 0, 0, 0]])

# CSR 행렬을 만듭니다.
matrix_large_sparse = sparse.csr_matrix(matrix_large)

# 원래 희소 행렬을 출력합니다.
print(matrix_sparse)
```


```python
# 큰 희소 행렬을 출력합니다.
print(matrix_large_sparse)
```


```python
# (data, (row_index, col_index))로 구성된 튜플을 전달합니다.
# shape 매개변수에서 0을 포함한 행렬의 전체 크기를 지정합니다.  
matrix_sparse_2 = sparse.csr_matrix(([1, 3], ([1, 2], [1, 0])), shape=(3, 10))

print(matrix_sparse_2)
```


```python
print(matrix_sparse_2.toarray())
```


```python
matrix_sparse_2.todense()
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

# 행 벡터를 만듭니다.
vector = np.array([1, 2, 3, 4, 5, 6])

# 행렬을 만듭니다.
matrix = np.array([[1, 2, 3],
                   [4, 5, 6],
                   [7, 8, 9]])

# vector의 세 번째 원소를 선택합니다.
vector[2]
```


```python
# matrix의 두 번째 행, 두 번째 열의 원소를 선택합니다.
matrix[1,1]
```


```python
# 벡터에 있는 모든 원소를 선택합니다.
vector[:]
```


```python
# 세 번째 원소를 포함하여 그 이전의 모든 원소를 선택합니다.
vector[:3]
```


```python
# 세 번째 이후의 모든 원소를 선택합니다.
vector[3:]
```


```python
# 마지막 원소를 선택합니다.
vector[-1]
```


```python
# 행렬에서 첫 번째 두 개의 행과 모든 열을 선택합니다.
matrix[:2,:]
```


```python
# 모든 행과 두 번째 열을 선택합니다.
matrix[:,1:2]
```


```python
# 첫 번째 행과 세 번째 행을 선택합니다.
matrix[[0,2]]
```


```python
# (0, 1), (2, 0) 위치의 원소를 선택합니다.
matrix[[0,2], [1,0]]
```


```python
# matrix의 각 원소에 비교 연산자가 적용됩니다.
mask = matrix > 5

mask
```


```python
# 불리언 마스크 배열을 사용하여 원소를 선택합니다.
matrix[mask]
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

# 행렬을 만듭니다.
matrix = np.array([[1, 2, 3, 4],
                   [5, 6, 7, 8],
                   [9, 10, 11, 12]])

# 행렬의 크기를 확인합니다.
matrix.shape
```


```python
# 행렬의 원소 개수를 확인합니다(행 * 열).
matrix.size
```


```python
# 차원 수를 확인합니다.
matrix.ndim
```


```python
# 원소의 데이터 타입을 확인합니다.
print(matrix.dtype)
```


```python
# 원소 하나가 차지하는 바이트 크기입니다. 
print(matrix.itemsize)
```


```python
# 배열 전체가 차지하는 바이트 크기입니다.
print(matrix.nbytes)
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

# 행렬을 만듭니다.
matrix = np.array([[1, 2, 3],
                   [4, 5, 6],
                   [7, 8, 9]])

# 100을 더하는 함수를 만듭니다.
add_100 = lambda i: i + 100

# 벡터화된 함수를 만듭니다.
vectorized_add_100 = np.vectorize(add_100)

# 행렬의 모든 원소에 함수를 적용합니다.
vectorized_add_100(matrix)
```


```python
# 모든 원소에 100을 더합니다.
matrix + 100
```


```python
# (3, 3) 크기 행렬에 (3, ) 벡터를 더하면 
# (1, 3) 크기가 된다음 행을 따라 반복됩니다.
matrix + [100, 100, 100]
```


```python
# (3, 3) 크기 행렬에 (3, 1) 벡터를 더하면 열을 따라 반복됩니다.
matrix + [[100], [100], [100]]
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

# 행렬을 만듭니다.
matrix = np.array([[1, 2, 3],
                   [4, 5, 6],
                   [7, 8, 9]])

# 가장 큰 원소를 반환합니다.
np.max(matrix)
```


```python
# 가장 작은 원소를 반환합니다.
np.min(matrix)
```


```python
# 각 열에서 최댓값을 찾습니다.
np.max(matrix, axis=0)
```


```python
# 각 행에서 최댓값을 찾습니다.
np.max(matrix, axis=1)
```


```python
# 이전 예와 달리 (3, 1) 크기의 열 벡터가 만들어 집니다.
vector_column = np.max(matrix, axis=1, keepdims=True)

vector_column
```


```python
# 열 벡터이므로 브로드캐스팅을 이용하여 각 행의 최댓값을 뺄 수 있습니다.
matrix - vector_column
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

# 행렬을 만듭니다.
matrix = np.array([[1, 2, 3],
                   [4, 5, 6],
                   [7, 8, 9]])

# 평균을 반환합니다.
np.mean(matrix)
```


```python
# 분산을 반환합니다.
np.var(matrix)
```


```python
# 표준 편차를 반환합니다.
np.std(matrix)
```


```python
# 각 열의 평균을 계산합니다.
np.mean(matrix, axis=0)
```


```python
np.std(matrix, ddof=1)
```


```python
import pandas as pd

df = pd.DataFrame(matrix.flatten())
df.std()
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

# 4x3 행렬을 만듭니다.
matrix = np.array([[1, 2, 3],
                   [4, 5, 6],
                   [7, 8, 9],
                   [10, 11, 12]])

# 2x6 행렬로 크기를 바꿉니다.
matrix.reshape(2, 6)
```


```python
matrix.size
```


```python
matrix.reshape(1, -1)
```


```python
matrix.reshape(12)
```


```python
matrix.reshape(-1)
```


```python
matrix.ravel()
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

# 행렬을 만듭니다.
matrix = np.array([[1, 2, 3],
                   [4, 5, 6],
                   [7, 8, 9]])

# 행렬을 전치합니다.
matrix.T
```


```python
# 벡터를 전치합니다.
np.array([1, 2, 3, 4, 5, 6]).T
```


```python
# 행 벡터를 전치합니다.
np.array([[1, 2, 3, 4, 5, 6]]).T
```


```python
matrix.transpose()
```


```python
# 2x3x2 행렬을 만듭니다.
matrix = np.array([[[ 1,  2],
                    [ 3,  4],
                    [ 5,  6]],

                   [[ 7,  8],
                    [ 9, 10],
                    [11, 12]]])

# 두 번째와 세 번째 차원을 바꾸어 2x2x3 행렬로 만듭니다.
matrix.transpose((0, 2, 1))
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

# 행렬을 만듭니다.
matrix = np.array([[1, 2, 3],
                   [4, 5, 6],
                   [7, 8, 9]])

# 행렬을 펼칩니다.
matrix.flatten()
```


```python
matrix.reshape(1, -1)
```


```python
vector_reshaped = matrix.reshape(-1)
vector_flattened = matrix.flatten()

# (0, 0) 위치의 원소를 바꿉니다.
matrix[0][0] = -1

# 배열의 뷰는 원본 배열의 변경 사항을 반영합니다.
vector_reshaped
# 복사된 배열에는 영향이 미치지 않습니다.
vector_flattened
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

# 행렬을 만듭니다.
matrix = np.array([[1, 1, 1],
                   [1, 1, 10],
                   [1, 1, 15]])

# 행렬의 랭크를 반환합니다.
np.linalg.matrix_rank(matrix)
```

넘파이 0.18 버전에서 `rank()` 함수가 삭제되었습니다. 대신 `ndim()` 함수를 사용하세요.


```python
# 2D 배열이므로 2가 반환됩니다.
np.ndim(matrix)
```


```python
# svd 함수로 특잇값만 계산합니다.
s = np.linalg.svd(matrix, compute_uv=False)
# 오차를 고려하여 0에 가까운 아주 작은 값을 지정합니다.
np.sum(s > 1e-10)
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

# 행렬을 만듭니다.
matrix = np.array([[1, 2, 3],
                   [2, 4, 6],
                   [3, 8, 9]])

# 행렬의 행렬식을 반환합니다.
np.linalg.det(matrix)
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

# 행렬을 만듭니다.
matrix = np.array([[1, 2, 3],
                   [2, 4, 6],
                   [3, 8, 9]])

# 대각 원소를 반환합니다.
matrix.diagonal()
```


```python
# 반환된 배열을 변경하려면 복사해야 합니다.
a = matrix.diagonal().copy()
```


```python
a = np.diag(matrix)
print(a)
```


```python
# 1차원 배열이 주어지면 2차원 대각행렬을 만듭니다.
np.diag(a)
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

# 행렬을 만듭니다.
matrix = np.array([[1, 2, 3],
                   [2, 4, 6],
                   [3, 8, 9]])

# 대각합을 반환합니다.
matrix.trace()
```


```python
# 대각 원소를 사용하여 합을 구합니다.
sum(matrix.diagonal())
```


```python
# 주 대각선 하나 위의 대각 원소의 합을 반환합니다.
matrix.trace(offset=1)
```


```python
# 주 대각선 하나 아래의 대각 원소의 합을 반환합니다.
matrix.trace(offset=-1)
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

# 행렬을 만듭니다.
matrix = np.array([[1, -1, 3],
                   [1, 1, 6],
                   [3, 8, 9]])

# 고윳값과 고유벡터를 계산합니다.
eigenvalues, eigenvectors = np.linalg.eig(matrix)
# 고윳값을 확인합니다.
eigenvalues
# 고유벡터를 확인합니다.
eigenvectors
```


```python
# 대칭 행렬을 만듭니다.
matrix = np.array([[1, -1, 3],
                   [-1, 1, 6],
                   [3, 6, 9]])

# 고윳값과 고유벡터를 계산합니다.
eigenvalues, eigenvectors = np.linalg.eigh(matrix)
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

# 두 벡터를 만듭니다.
vector_a = np.array([1,2,3])
vector_b = np.array([4,5,6])

# 점곱을 계산합니다.
np.dot(vector_a, vector_b)
```


```python
scalar_a = np.array(1)
scalar_b = np.array(2)
```


```python
np.dot(scalar_a, scalar_b)
```


```python
# 스칼라 배열에 적용되지 않습니다.
scalar_a @ scalar_b
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

# 행렬을 만듭니다.
matrix_a = np.array([[1, 1, 1],
                     [1, 1, 1],
                     [1, 1, 2]])

# 행렬을 만듭니다.
matrix_b = np.array([[1, 3, 1],
                     [1, 3, 1],
                     [1, 3, 8]])

# 두 행렬을 더합니다.
np.add(matrix_a, matrix_b)
```


```python
# 두 행렬을 뺍니다.
np.subtract(matrix_a, matrix_b)
```


```python
# 두 행렬을 더합니다.
matrix_a + matrix_b
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

# 행렬을 만듭니다.
matrix_a = np.array([[1, 1],
                     [1, 2]])

# 행렬을 만듭니다.
matrix_b = np.array([[1, 3],
                     [1, 2]])

# 두 행렬을 곱합니다.
np.dot(matrix_a, matrix_b)
```


```python
# 두 행렬을 곱합니다.
matrix_a @ matrix_b
```


```python
# 두 행렬의 원소별 곱셈을 수행합니다.
matrix_a * matrix_b
```


```python
a = np.random.rand(2, 1, 4, 5)
b = np.random.rand(1, 3, 5, 6)

np.dot(a, b).shape
```


```python
np.matmul(a, b).shape
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

# 행렬을 만듭니다.
matrix = np.array([[1, 4],
                   [2, 5]])

# 역행렬을 계산합니다.
np.linalg.inv(matrix)
```


```python
# 행렬과 역행렬을 곱합니다.
matrix @ np.linalg.inv(matrix)
```


```python
matrix = np.array([[1, 4, 7],
                   [2, 5, 8]])

# 유사 역행렬을 계산합니다.
np.linalg.pinv(matrix)
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

# 초깃값을 지정합니다.
np.random.seed(0)

# 0.0과 1.0 사이에서 세 개의 실수 난수를 생성합니다.
np.random.random(3)
```


```python
# 1과 10 사이에서 세 개의 정수 난수를 생성합니다.
np.random.randint(0, 11, 3)
```


```python
# 평균이 0.0이고 표준 편차가 1.0인 정규 분포에서 세 개의 수를 뽑습니다.
np.random.normal(0.0, 1.0, 3)
```


```python
# 평균이 0.0이고 스케일이 1.0인 로지스틱 분포에서 세 개의 수를 뽑습니다.
np.random.logistic(0.0, 1.0, 3)
```


```python
# 1.0보다 크거나 같고 2.0보다 작은 세 개의 수를 뽑습니다.
np.random.uniform(1.0, 2.0, 3)
```


```python
# 0.0(포함)과 1.0 사이에서 세 개의 실수 난수를 생성합니다.
# np.random.random((2, 3)), np.random.sample((2, 3)), 
# np.random.uniform(0.0, 1.0, (2, 3))과 동일합니다.
np.random.random_sample((2, 3))
```


```python
# np.random.random_sample((2, 3))과 동일합니다.
np.random.rand(2, 3)
```


```python
np.random.randint(0, 1, 10)
```


```python
# np.random.normal(0.0, 1.0, (2, 3))과 동일합니다.
np.random.standard_normal((2, 3))
```


```python
# np.random.normal(0.0, 1.0, (2, 3))과 동일합니다.
np.random.randn(2, 3)
```


```python
# 0~2 사이의 정수 중 랜덤하게 10번을 뽑습니다.
# np.random.choice(3, 5)와 동일합니다.
np.random.choice([0,1,2], 5)
```


```python
a = np.array([0, 1, 2, 3, 4])
np.random.shuffle(a)
a
```


```python
# a는 변경되지 않습니다.
np.random.permutation(a)
```


```python
np.random.permutation(5)
```





```python
# 라이브러리를 임포트합니다.
import pandas as pd

# 데이터 URL
url = 'https://tinyurl.com/titanic-csv'

# 데이터프레임으로 데이터를 적재합니다.
dataframe = pd.read_csv(url)

# 처음 다섯 개의 행을 출력합니다.
dataframe.head(5)
```


```python
# 라이브러리를 임포트합니다.
import pandas as pd

# 데이터프레임을 만듭니다.
dataframe = pd.DataFrame()

# 열을 추가합니다.
dataframe['Name'] = ['Jacky Jackson', 'Steven Stevenson']
dataframe['Age'] = [38, 25]
dataframe['Driver'] = [True, False]

# 데이터프레임을 확인합니다.
dataframe
```


```python
# 열을 만듭니다.
new_person = pd.Series(['Molly Mooney', 40, True], index=['Name','Age','Driver'])

# 열을 추가합니다.
dataframe.append(new_person, ignore_index=True)
```


```python
import numpy as np

data = [ ['Jacky Jackson', 38, True], ['Steven Stevenson', 25, False] ]

matrix = np.array(data)
pd.DataFrame(matrix, columns=['Name', 'Age', 'Driver'])
```


```python
pd.DataFrame(data, columns=['Name', 'Age', 'Driver'])
```


```python
data = {'Name': ['Jacky Jackson', 'Steven Stevenson'],
        'Age': [38, 25],
        'Driver': [True, False]}
pd.DataFrame(data)
```


```python
data = [ {'Name': 'Jacky Jackson', 'Age': 38, 'Driver': True},
         {'Name': 'Steven Stevenson', 'Age': 25, 'Driver': False} ]
pd.DataFrame(data, index=['row1', 'row2'])
```


```python
# 라이브러리를 임포트합니다.
import pandas as pd

# 데이터 URL
url = 'https://tinyurl.com/titanic-csv'

# 데이터를 적재합니다.
dataframe = pd.read_csv(url)

# 두 개의 행을 확인합니다.
dataframe.head(2)
```


```python
# 차원을 확인합니다.
dataframe.shape
```


```python
# 통곗값을 확인합니다.
dataframe.describe()
```


```python
# 라이브러리를 임포트합니다.
import pandas as pd

# 데이터 URL
url = 'https://tinyurl.com/titanic-csv'

# 데이터를 적재합니다.
dataframe = pd.read_csv(url)

# 첫 번째 행을 선택합니다.
dataframe.iloc[0]
```


```python
# 세 개의 행을 선택합니다.
dataframe.iloc[1:4]
```


```python
# 네 개의 행을 선택합니다.
dataframe.iloc[:4]
```


```python
# 인덱스를 설정합니다.
dataframe = dataframe.set_index(dataframe['Name'])

# 행을 확인합니다.
dataframe.loc['Allen, Miss Elisabeth Walton']
```


```python
# 'Allison, Miss Helen Loraine' 이전까지 Age 열과 Sex 열만 선택합니다.
dataframe.loc[:'Allison, Miss Helen Loraine', 'Age':'Sex']
```


```python
# dataframe[:2]와 동일합니다.
dataframe[:'Allison, Miss Helen Loraine']
```


```python
dataframe[['Age', 'Sex']].head(2)
```


```python
# 라이브러리를 임포트합니다.
import pandas as pd

# 데이터 URL
url = 'https://tinyurl.com/titanic-csv'

# 데이터를 적재합니다.
dataframe = pd.read_csv(url)

# ‘sex’ 열이 ‘female’인 행 중 처음 두 개를 출력합니다.
dataframe[dataframe['Sex'] == 'female'].head(2)
```


```python
# 행을 필터링합니다.
dataframe[(dataframe['Sex'] == 'female') & (dataframe['Age'] >= 65)]
```


```python
# 라이브러리를 임포트합니다.
import pandas as pd

# 데이터 URL
url = 'https://tinyurl.com/titanic-csv'

# 데이터를 적재합니다.
dataframe = pd.read_csv(url)

# 값을 치환하고 두 개의 행을 출력합니다.
dataframe['Sex'].replace("female", "Woman").head(2)
```


```python
# "female"과 "male을 "Woman"과 "Man"으로 치환합니다.
dataframe['Sex'].replace(["female", "male"], ["Woman", "Man"]).head(5)
```


```python
# 값을 치환하고 두 개의 행을 출력합니다.
dataframe.replace(1, "One").head(2)
```


```python
# 값을 치환하고 두 개의 행을 출력합니다.
dataframe.replace(r"1st", "First", regex=True).head(2)
```


```python
# female과 male을 person으로 바꿉니다.
dataframe.replace(["female", "male"], "person").head(3)
```


```python
# female을 1로 바꾸고 male을 0으로 바꿉니다.
dataframe.replace({"female": 1, "male": 0}).head(3)
```


```python
# 라이브러리를 임포트합니다.
import pandas as pd

# 데이터 URL
url = 'https://tinyurl.com/titanic-csv'

# 데이터를 적재합니다.
dataframe = pd.read_csv(url)

# 열 이름을 바꾸고 두 개의 행을 출력합니다.
dataframe.rename(columns={'PClass': 'Passenger Class'}).head(2)
```


```python
# 열 이름을 바꾸고 두 개의 행을 출력합니다.
dataframe.rename(columns={'PClass': 'Passenger Class', 'Sex': 'Gender'}).head(2)
```


```python
# 라이브러리를 임포트합니다.
import collections

# 딕셔너리를 만듭니다.
column_names = collections.defaultdict(str)

# 키를 만듭니다.
for name in dataframe.columns:
    column_names[name]

# 딕셔너리를 출력합니다.
column_names
```


```python
# 인덱스 0을 -1로 바꿉니다.
dataframe.rename(index={0:-1}).head(2)
```


```python
# 열 이름을 소문자로 바꿉니다.
dataframe.rename(str.lower, axis='columns').head(2)
```


```python
# 라이브러리를 임포트합니다.
import pandas as pd

# 데이터 URL
url = 'https://tinyurl.com/titanic-csv'

# 데이터를 적재합니다.
dataframe = pd.read_csv(url)

# 통곗값을 계산합니다.
print('최댓값:', dataframe['Age'].max())
print('최솟값:', dataframe['Age'].min())
print('평균:', dataframe['Age'].mean())
print('합:', dataframe['Age'].sum())
print('카운트:', dataframe['Age'].count())
```


```python
# 카운트를 출력합니다.
dataframe.count()
```


```python
# 수치형 열의 공분산을 계산합니다.
dataframe.cov()
```


```python
# 수치형 열의 상관계수를 계산합니다.
dataframe.corr()
```


```python
# 라이브러리를 임포트합니다.
import pandas as pd

# 데이터 URL
url = 'https://tinyurl.com/titanic-csv'

# 데이터를 적재합니다.
dataframe = pd.read_csv(url)

# 고유한 값을 찾습니다.
dataframe['Sex'].unique()
```


```python
# 카운트를 출력합니다.
dataframe['Sex'].value_counts()
```


```python
# 카운트를 출력합니다.
dataframe['PClass'].value_counts()
```


```python
# 고유한 값의 개수를 출력합니다.
dataframe['PClass'].nunique()
```


```python
dataframe.nunique()
```


```python
# 라이브러리를 임포트합니다.
import pandas as pd

# 데이터 URL
url = 'https://tinyurl.com/titanic-csv'

# 데이터를 적재합니다.
dataframe = pd.read_csv(url)

## 누락된 값을 선택하고 두 개의 행을 출력합니다.
dataframe[dataframe['Age'].isnull()].head(2)
```


```python
# NaN으로 값을 바꾸려고 합니다.
dataframe['Sex'] = dataframe['Sex'].replace('male', NaN)
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

# NaN으로 값을 바꿉니다.
dataframe['Sex'] = dataframe['Sex'].replace('male', np.nan)
```


```python
# 데이터를 적재하고 누란된 값을 설정합니다.
dataframe = pd.read_csv(url, na_values=[np.nan, 'NONE', -999])
```


```python
dataframe = pd.read_csv(url, na_values=['female'], 
                        keep_default_na=False)
dataframe[12:14]
```


```python
dataframe = pd.read_csv(url, na_filter=False)
dataframe[12:14]
```


```python
# 라이브러리를 임포트합니다.
import pandas as pd

# 데이터 URL
url = 'https://tinyurl.com/titanic-csv'

# 데이터를 적재합니다.
dataframe = pd.read_csv(url)

# 열을 삭제합니다.
dataframe.drop('Age', axis=1).head(2)
```


```python
# 열을 삭제합니다.
dataframe.drop(['Age', 'Sex'], axis=1).head(2)
```


```python
# PClass 열을 삭제합니다.
dataframe.drop(dataframe.columns[1], axis=1).head(2)
```


```python
dataframe.head(2)
```


```python
# 라이브러리를 임포트합니다.
import pandas as pd

# 데이터 URL
url = 'https://tinyurl.com/titanic-csv'

# 데이터를 적재합니다.
dataframe = pd.read_csv(url)

# 행을 삭제하고 처음 두 개의 행을 출력합니다.
dataframe[dataframe['Sex'] != 'male'].head(2)
```


```python
# 행을 삭제하고 처음 두 개의 행을 출력합니다.
dataframe[dataframe['Name'] != 'Allison, Miss Helen Loraine'].head(2)
```


```python
# 행을 삭제하고 처음 두 개의 행을 출력합니다.
dataframe[dataframe.index != 0].head(2)
```


```python
# 라이브러리를 임포트합니다.
import pandas as pd

# 데이터 URL
url = 'https://tinyurl.com/titanic-csv'

# 데이터를 적재합니다.
dataframe = pd.read_csv(url)

# 중복 행을 삭제하고 처음 두 개의 행을 출력합니다.
dataframe.drop_duplicates().head(2)
```


```python
# 행의 개수를 출력합니다.
print("원본 데이터프레임 행의 수:", len(dataframe))
print("중복 삭제 후 행의 수:", len(dataframe.drop_duplicates()))
```


```python
# 중복된 행을 삭제합니다.
dataframe.drop_duplicates(subset=['Sex'])
```


```python
# 중복된 행을 삭제합니다.
dataframe.drop_duplicates(subset=['Sex'], keep='last')
```


```python
# 라이브러리를 임포트합니다.
import pandas as pd

# 데이터 URL
url = 'https://tinyurl.com/titanic-csv'

# 데이터를 적재합니다.
dataframe = pd.read_csv(url)

# ‘Sex’ 열의 값으로 행을 그룹핑하고 평균을 계산합니다.
dataframe.groupby('Sex').mean()
```


```python
# 행을 그룹핑합니다.
dataframe.groupby('Sex')
```


```python
# 행을 그룹핑하고 카운팅합니다.
dataframe.groupby('Survived')['Name'].count()
```


```python
# 행을 그룹핑한 다음 평균을 계산합니다.
dataframe.groupby(['Sex','Survived'])['Age'].mean()
```


```python
# 라이브러리를 임포트합니다.
import pandas as pd
import numpy as np

# 날짜 범위를 만듭니다.
time_index = pd.date_range('06/06/2017', periods=100000, freq='30S')

# 데이터프레임을 만듭니다.
dataframe = pd.DataFrame(index=time_index)

# 난수 값으로 열을 만듭니다.
dataframe['Sale_Amount'] = np.random.randint(1, 10, 100000)

# 주 단위로 행을 그룹핑한 다음 합을 계산합니다.
dataframe.resample('W').sum()
```


```python
# 세개의 행을 출력합니다.
dataframe.head(3)
```


```python
# 2주 단위로 그룹핑하고 평균을 계산합니다.
dataframe.resample('2W').mean()
```


```python
# 한 달 간격으로 그룹핑하고 행을 카운트합니다.
dataframe.resample('M').count()
```


```python
# 월 간격으로 그룹핑하고 행을 카운트합니다.
dataframe.resample('M', label='left').count()
```


```python
dataframe.resample('MS').count()
```


```python
# 라이브러리를 임포트합니다.
import pandas as pd

# 데이터 URL
url = 'https://tinyurl.com/titanic-csv'

# 데이터를 적재합니다.
dataframe = pd.read_csv(url)

# 처음 두 이름을 대문자로 바꾸어 출력합니다.
for name in dataframe['Name'][0:2]:
    print(name.upper())
```


```python
# 처음 두 이름을 대문자로 바꾸어 출력합니다.
[name.upper() for name in dataframe['Name'][0:2]]
```


```python
# 라이브러리를 임포트합니다.
import pandas as pd

# 데이터 URL
url = 'https://tinyurl.com/titanic-csv'

# 데이터를 적재합니다.
dataframe = pd.read_csv(url)

# 함수를 만듭니다.
def uppercase(x):
    return x.upper()

# 함수를 적용하고 두 개의 행을 출력합니다.
dataframe['Name'].apply(uppercase)[0:2]
```


```python
# Survived 열의 1을 Live로, 0을 Dead로 바꿉니다.
dataframe['Survived'].map({1:'Live', 0:'Dead'})[:5]
```


```python
# 함수의 매개변수(age)를 apply 메서드를 호출할 때 전달할 수 있습니다.
dataframe['Age'].apply(lambda x, age: x < age, age=30)[:5]
```


```python
# 각 열에서 가장 큰 값을 뽑습니다.
dataframe.apply(lambda x: max(x))
```


```python
def truncate_string(x):
    if type(x) == str:
        return x[:20]
    return x

# 문자열의 길이를 최대 20자로 줄입니다.
dataframe.applymap(truncate_string)[:5]
```


```python
# 라이브러리를 임포트합니다.
import pandas as pd

# 데이터 URL
url = 'https://tinyurl.com/titanic-csv'

# 데이터를 적재합니다.
dataframe = pd.read_csv(url)

# 행을 그룹핑한 다음 함수를 적용합니다.
dataframe.groupby('Sex').apply(lambda x: x.count())
```


```python
# 라이브러리를 임포트합니다.
import pandas as pd

# 데이터프레임을 만듭니다.
data_a = {'id': ['1', '2', '3'],
          'first': ['Alex', 'Amy', 'Allen'],
          'last': ['Anderson', 'Ackerman', 'Ali']}
dataframe_a = pd.DataFrame(data_a, columns = ['id', 'first', 'last'])

# 데이터프레임을 만듭니다.
data_b = {'id': ['4', '5', '6'],
          'first': ['Billy', 'Brian', 'Bran'],
          'last': ['Bonder', 'Black', 'Balwner']}
dataframe_b = pd.DataFrame(data_b, columns = ['id', 'first', 'last'])

# 행 방향으로 데이터프레임을 연결합니다.
pd.concat([dataframe_a, dataframe_b], axis=0)
```


```python
# 열 방향으로 데이터프레임을 연결합니다.
pd.concat([dataframe_a, dataframe_b], axis=1)
```


```python
# 행을 만듭니다.
row = pd.Series([10, 'Chris', 'Chillon'], index=['id', 'first', 'last'])

# 행을 추가합니다.
dataframe_a.append(row, ignore_index=True)
```


```python
# 라이브러리를 임포트합니다.
import pandas as pd

# 데이터프레임을 만듭니다.
employee_data = {'employee_id': ['1', '2', '3', '4'],
                 'name': ['Amy Jones', 'Allen Keys', 'Alice Bees',
                 'Tim Horton']}
dataframe_employees = pd.DataFrame(employee_data, columns = ['employee_id',
                                                              'name'])

# 데이터프레임을 만듭니다.
sales_data = {'employee_id': ['3', '4', '5', '6'],
              'total_sales': [23456, 2512, 2345, 1455]}
dataframe_sales = pd.DataFrame(sales_data, columns = ['employee_id',
                                                      'total_sales'])

# 데이터프레임을 병합합니다.
pd.merge(dataframe_employees, dataframe_sales, on='employee_id')
```


```python
# 데이터프레임을 병합합니다.
pd.merge(dataframe_employees, dataframe_sales, on='employee_id', how='outer')
```


```python
# 데이터프레임을 병합합니다.
pd.merge(dataframe_employees, dataframe_sales, on='employee_id', how='left')
```


```python
# 데이터프레임을 병합합니다.
pd.merge(dataframe_employees,
         dataframe_sales,
         left_on='employee_id',
         right_on='employee_id')
```



```python
# 라이브러리를 임포트합니다.
import numpy as np
from sklearn import preprocessing

# 특성을 만듭니다.
feature = np.array([[-500.5],
                    [-100.1],
                    [0],
                    [100.1],
                    [900.9]])

# 스케일러 객체를 만듭니다.
minmax_scale = preprocessing.MinMaxScaler(feature_range=(0, 1))

# 특성의 스케일을 변환합니다.
scaled_feature = minmax_scale.fit_transform(feature)

# 특성을 출력합니다.
scaled_feature
```




    array([[0.        ],
           [0.28571429],
           [0.35714286],
           [0.42857143],
           [1.        ]])




```python
# 훈련 세트를 변환합니다.
preprocessing.MinMaxScaler().fit_transform(feature[:3])
```


```python
# 테스트 세트를 변환합니다.
preprocessing.MinMaxScaler().fit_transform(feature[3:])
```


```python
# 훈련 세트로 변환기를 학습합니다.
scaler = preprocessing.MinMaxScaler().fit(feature[:3])
scaler.transform(feature[:3])
```


```python
# 훈련 세트에서 학습한 변환기로 테스트 세트를 변환합니다.
scaler.transform(feature[3:])
```


```python
# 라이브러리를 임포트합니다.
import numpy as np
from sklearn import preprocessing

# 특성을 만듭니다.
x = np.array([[-1000.1],
              [-200.2],
              [500.5],
              [600.6],
              [9000.9]])

# 변환기 객체를 만듭니다.
scaler = preprocessing.StandardScaler()

# 특성을 변환합니다.
standardized = scaler.fit_transform(x)

# 특성을 출력합니다.
standardized
```


```python
# 평균과 표준 편차를 출력합니다.
print("평균 Mean:", round(standardized.mean()))
print("표준 편차 Standard deviation:", standardized.std())
```


```python
# 변환기 객체를 만듭니다.
robust_scaler = preprocessing.RobustScaler()

# 특성을 변환합니다.
robust_scaler.fit_transform(x)
```


```python
interquatile_range = x[3] - x[1]
(x - np.median(x)) / interquatile_range
```


```python
preprocessing.QuantileTransformer().fit_transform(x)
```


```python
# 라이브러리를 임포트합니다.
import numpy as np
from sklearn.preprocessing import Normalizer

# 특성 행렬을 만듭니다.
features = np.array([[0.5, 0.5],
                     [1.1, 3.4],
                     [1.5, 20.2],
                     [1.63, 34.4],
                     [10.9, 3.3]])

# 변환기 객체를 만듭니다.
normalizer = Normalizer(norm="l2")

# 특성 행렬을 변환합니다.
normalizer.transform(features)
```


```python
# 특성 행렬을 변환합니다.
features_l2_norm = Normalizer(norm="l2").transform(features)

# 특성 행렬을 출력합니다.
features_l2_norm
```


```python
# 특성 행렬을 변환합니다.
features_l1_norm = Normalizer(norm="l1").transform(features)

# 특성 행렬을 출력합니다.
features_l1_norm
```


```python
# 합을 출력합니다.
print("첫 번째 샘플 값의 합:",
   features_l1_norm[0, 0] + features_l1_norm[0, 1])
```


```python
# L1 노름을 사용한 변환.
# 각 행(axis=1)을 합한 결과가 2차원 배열로 유지되도록 keepdims를 True로 설정합니다.
features / np.sum(np.abs(features), axis=1, keepdims=True)
```


```python
# L2 노름을 사용한 변환.
features / np.sqrt(np.sum(np.square(features), axis=1, keepdims=True))
```


```python
# 각 행에서 최댓값으로 나눕니다.
Normalizer(norm="max").transform(features)
```


```python
# 라이브러리를 임포트합니다.
import numpy as np
from sklearn.preprocessing import PolynomialFeatures

# 특성 행렬을 만듭니다.
features = np.array([[2, 3],
                     [2, 3],
                     [2, 3]])

# PolynomialFeatures 객체를 만듭니다.
polynomial_interaction = PolynomialFeatures(degree=2, include_bias=False)

# 다항 특성을 만듭니다.
polynomial_interaction.fit_transform(features)
```


```python
interaction = PolynomialFeatures(degree=2, 
                                 interaction_only=True, include_bias=False)
interaction.fit_transform(features)
```


```python
# 상수항 1을 추가합니다.
polynomial_bias = PolynomialFeatures(degree=2, include_bias=True).fit(features)
polynomial_bias.transform(features)
```


```python
polynomial_bias.get_feature_names()
```


```python
# 라이브러리를 임포트합니다.
import numpy as np
from sklearn.preprocessing import FunctionTransformer

# 특성 행렬을 만듭니다.
features = np.array([[2, 3],
                     [2, 3],
                     [2, 3]])

# 간단한 함수를 정의합니다.
def add_ten(x):
    return x + 10

# 변환기 객체를 만듭니다.
ten_transformer = FunctionTransformer(add_ten)

# 특성 행렬을 변환합니다.
ten_transformer.transform(features)
```


```python
# 라이브러리를 임포트합니다.
import pandas as pd

# 데이터프레임을 만듭니다.
df = pd.DataFrame(features, columns=["feature_1", "feature_2"])

# 함수를 적용합니다.
df.apply(add_ten)
```


```python
FunctionTransformer(add_ten, validate=False).transform(np.array([1, 2, 3]))
```


```python
from sklearn.compose import ColumnTransformer

# 100을 더하는 함수를 만듭니다.
def add_hundred(x):
    return x + 100

# (이름, 변환기, 열 리스트)로 구성된 튜플의 리스트를 ColumnTransformer에 전달합니다.
ct = ColumnTransformer(
    [("add_ten", FunctionTransformer(add_ten, validate=True), ['feature_1']),
     ("add_hundred", FunctionTransformer(add_hundred, validate=True), ['feature_2'])])

ct.fit_transform(df)
```


```python
# 라이브러리를 임포트합니다.
import numpy as np
from sklearn.covariance import EllipticEnvelope
from sklearn.datasets import make_blobs

# 모의 데이터를 만듭니다.
features, _ = make_blobs(n_samples = 10,
                         n_features = 2,
                         centers = 1,
                         random_state = 1)

# 첫 번째 샘플을 극단적인 값으로 바꿉니다.
features[0,0] = 10000
features[0,1] = 10000

# 이상치 감지 객체를 만듭니다.
outlier_detector = EllipticEnvelope(contamination=.1)

# 감지 객체를 훈련합니다.
outlier_detector.fit(features)

# 이상치를 예측합니다.
outlier_detector.predict(features)
```


```python
# 하나의 특성을 만듭니다.
feature = features[:,0]

# 이상치의 인덱스를 반환하는 함수를 만듭니다.
def indicies_of_outliers(x):
    q1, q3 = np.percentile(x, [25, 75])
    iqr = q3 - q1
    lower_bound = q1 - (iqr * 1.5)
    upper_bound = q3 + (iqr * 1.5)
    return np.where((x > upper_bound) | (x < lower_bound))

# 함수를 실행합니다.
indicies_of_outliers(feature)
```


```python
# 라이브러리를 임포트합니다.
import pandas as pd

# 데이터프레임을 만듭니다.
houses = pd.DataFrame()
houses['Price'] = [534433, 392333, 293222, 4322032]
houses['Bathrooms'] = [2, 3.5, 2, 116]
houses['Square_Feet'] = [1500, 2500, 1500, 48000]

# 샘플을 필터링합니다.
houses[houses['Bathrooms'] < 20]
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

# 불리언 조건을 기반으로 특성을 만듭니다.
houses["Outlier"] = np.where(houses["Bathrooms"] < 20, 0, 1)

# 데이터를 확인합니다.
houses
```


```python
# 로그 특성
houses["Log_Of_Square_Feet"] = [np.log(x) for x in houses["Square_Feet"]]

# 데이터를 확인합니다.
houses
```


```python
# 라이브러리를 임포트합니다.
import numpy as np
from sklearn.preprocessing import Binarizer

# 특성을 만듭니다.
age = np.array([[6],
                [12],
                [20],
                [36],
                [65]])

# Binarizer 객체를 만듭니다.
binarizer = Binarizer(threshold=18)

# 특성을 변환합니다.
binarizer.fit_transform(age)
```


```python
# 특성을 나눕니다.
np.digitize(age, bins=[20,30,64])
```


```python
# 특성을 나눕니다.
np.digitize(age, bins=[20,30,64], right=True)
```


```python
# 특성을 나눕니다.
np.digitize(age, bins=[18])
```


```python
from sklearn.preprocessing import KBinsDiscretizer

# 네 개의 구간으로 나눕니다.
kb = KBinsDiscretizer(4, encode='ordinal', strategy='quantile')
kb.fit_transform(age)
```


```python
# 원-핫 인코딩을 반환합니다.
kb = KBinsDiscretizer(4, encode='onehot-dense', strategy='quantile')
kb.fit_transform(age)
```


```python
# 동일한 길이의 구간을 만듭니다.
kb = KBinsDiscretizer(4, encode='onehot-dense', strategy='uniform')
kb.fit_transform(age)
```


```python
kb.bin_edges_
```


```python
# 라이브러리를 임포트합니다.
import pandas as pd
from sklearn.datasets import make_blobs
from sklearn.cluster import KMeans

# 모의 특성 행렬을 만듭니다.
features, _ = make_blobs(n_samples = 50,
                         n_features = 2,
                         centers = 3,
                         random_state = 1)

# 데이터프레임을 만듭니다.
dataframe = pd.DataFrame(features, columns=["feature_1", "feature_2"])

# k-평균 군집 모델을 만듭니다.
clusterer = KMeans(3, random_state=0)

# 모델을 훈련합니다.
clusterer.fit(features)

# 그룹 소속을 예측합니다.
dataframe["group"] = clusterer.predict(features)

# 처음 몇 개의 샘플을 조회합니다.
dataframe.head(5)
```


```python
# 라이브러리를 임포트합니다.
import numpy as np

# 특성 행렬을 만듭니다.
features = np.array([[1.1, 11.1],
                     [2.2, 22.2],
                     [3.3, 33.3],
                     [4.4, 44.4],
                     [np.nan, 55]])

# (~ 연산자를 사용하여) 누락된 값이 없는 샘플만 남깁니다.
features[~np.isnan(features).any(axis=1)]
```


```python
# 라이브러리를 임포트합니다.
import pandas as pd

# 데이터를 적재합니다.
dataframe = pd.DataFrame(features, columns=["feature_1", "feature_2"])

# 누락된 값이 있는 샘플을 제거합니다.
dataframe.dropna()
```


```python
# 라이브러리를 임포트합니다.
import numpy as np
from fancyimpute import KNN
from sklearn.preprocessing import StandardScaler
from sklearn.datasets import make_blobs

# 모의 특성 행렬을 만듭니다.
features, _ = make_blobs(n_samples = 1000,
                         n_features = 2,
                         random_state = 1)

# 특성을 표준화합니다.
scaler = StandardScaler()
standardized_features = scaler.fit_transform(features)

# 첫 번째 샘플의 첫 번째 특성을 삭제합니다.
true_value = standardized_features[0,0]
standardized_features[0,0] = np.nan

# 특성 행렬에 있는 누락된 값을 예측합니다.
features_knn_imputed = KNN(k=5, verbose=0).fit_transform(standardized_features)

# 실제 값과 대체된 값을 비교합니다.
print("실제 값:", true_value)
print("대체된 값:", features_knn_imputed[0,0])
```

사이킷런 0.22 버전에서 `Imputer` 클래스가 삭제되었습니다.


```python
# # 라이브러리를 임포트합니다.
# from sklearn.preprocessing import Imputer

# # Imputer 객체를 만듭니다.
# mean_imputer = Imputer(strategy="mean", axis=0)

# # 누락된 값을 채웁니다.
# features_mean_imputed = mean_imputer.fit_transform(features)

# # 실제 값과 대체된 값을 비교합니다.
# print("실제 값 True Value:", true_value)
# print("대체된 값 Imputed Value:", features_mean_imputed[0,0])
```


```python
from sklearn.impute import SimpleImputer

simple_imputer = SimpleImputer()
features_simple_imputed = simple_imputer.fit_transform(features)

# 실제 값과 대체된 값을 비교합니다.
print("실제 값 True Value:", true_value)
print("대체된 값 Imputed Value:", features_simple_imputed[0,0])
```

```python
# 라이브러리를 임포트합니다.
import numpy as np
from sklearn.preprocessing import LabelBinarizer, MultiLabelBinarizer

# 특성을 만듭니다.
feature = np.array([["Texas"],
                    ["California"],
                    ["Texas"],
                    ["Delaware"],
                    ["Texas"]])

# 원-핫 인코더를 만듭니다.
one_hot = LabelBinarizer()

# 특성을 원-핫 인코딩합니다.
one_hot.fit_transform(feature)
```




    array([[0, 0, 1],
           [1, 0, 0],
           [0, 0, 1],
           [0, 1, 0],
           [0, 0, 1]])




```python
# 특성의 클래스를 확인합니다.
one_hot.classes_
```


```python
# 원-핫 인코딩을 되돌립니다.
one_hot.inverse_transform(one_hot.transform(feature))
```


```python
# 라이브러리를 임포트합니다.
import pandas as pd

# 특성으로 더미(dummy) 변수를 만듭니다.
pd.get_dummies(feature[:,0])
```


```python
# 다중 클래스 특성을 만듭니다.
multiclass_feature = [("Texas", "Florida"),
                      ("California", "Alabama"),
                      ("Texas", "Florida"),
                      ("Delware", "Florida"),
                      ("Texas", "Alabama")]

# 다중 클래스 원-핫 인코더를 만듭니다.
one_hot_multiclass = MultiLabelBinarizer()

# 다중 클래스 특성을 원-핫 인코딩합니다.
one_hot_multiclass.fit_transform(multiclass_feature)
```


```python
# 클래스를 확인합니다.
one_hot_multiclass.classes_
```


```python
from sklearn.preprocessing import OneHotEncoder

# 여러 개의 열이 있는 특성 배열을 만듭니다.
feature = np.array([["Texas", 1],
                    ["California", 1],
                    ["Texas", 3],
                    ["Delaware", 1],
                    ["Texas", 1]])

one_hot_encoder = OneHotEncoder(sparse=False)
one_hot_encoder.fit_transform(feature)
```


```python
one_hot_encoder.categories_
```


```python
# 라이브러리를 임포트합니다.
import pandas as pd

# 특성을 만듭니다.
dataframe = pd.DataFrame({"Score": ["Low", "Low", "Medium", "Medium", "High"]})

# 매핑 딕셔너리를 만듭니다.
scale_mapper = {"Low":1,
                "Medium":2,
                "High":3}

# 특성을 정수로 변환합니다.
dataframe["Score"].replace(scale_mapper)
```


```python
dataframe = pd.DataFrame({"Score": ["Low",
                                    "Low",
                                    "Medium",
                                    "Medium",
                                    "High",
                                    "Barely More Than Medium"]})

scale_mapper = {"Low":1,
                "Medium":2,
                "Barely More Than Medium": 3,
                "High":4}

dataframe["Score"].replace(scale_mapper)
```


```python
scale_mapper = {"Low":1,
                "Medium":2,
                "Barely More Than Medium": 2.1,
                "High":3}
dataframe["Score"].replace(scale_mapper)
```


```python
from sklearn.preprocessing import OrdinalEncoder

features = np.array([["Low", 10],
                     ["High", 50],
                     ["Medium", 3]])

ordinal_encoder = OrdinalEncoder()
ordinal_encoder.fit_transform(features)
```


```python
ordinal_encoder.categories_
```


```python
# 라이브러리를 임포트합니다.
from sklearn.feature_extraction import DictVectorizer

# 딕셔너리를 만듭니다.
data_dict = [{"Red": 2, "Blue": 4},
             {"Red": 4, "Blue": 3},
             {"Red": 1, "Yellow": 2},
             {"Red": 2, "Yellow": 2}]

# DictVectorizer 객체를 만듭니다.
dictvectorizer = DictVectorizer(sparse=False)

# 딕셔너리를 특성 행렬로 변환합니다.
features = dictvectorizer.fit_transform(data_dict)

# 특성 행렬을 확인합니다.
features
```


```python
# 특성 이름을 얻습니다.
feature_names = dictvectorizer.get_feature_names()

# 특성 이름을 확인합니다.
feature_names
```


```python
# 라이브러리를 임포트합니다.
import pandas as pd

# 특성으로 데이터프레임을 만듭니다.
pd.DataFrame(features, columns=feature_names)
```


```python
# 네 개의 문서에 대한 단어 카운트 딕셔너리를 만듭니다.
doc_1_word_count = {"Red": 2, "Blue": 4}
doc_2_word_count = {"Red": 4, "Blue": 3}
doc_3_word_count = {"Red": 1, "Yellow": 2}
doc_4_word_count = {"Red": 2, "Yellow": 2}

# 리스트를 만듭니다.
doc_word_counts = [doc_1_word_count,
                   doc_2_word_count,
                   doc_3_word_count,
                   doc_4_word_count]

# 단어 카운트 딕셔너리를 특성 행렬로 변환합니다.
dictvectorizer.fit_transform(doc_word_counts)
```


```python
# 라이브러리를 임포트합니다.
import numpy as np
from sklearn.neighbors import KNeighborsClassifier

# 범주형 특성을 가진 특성 행렬을 만듭니다.
X = np.array([[0, 2.10, 1.45],
              [1, 1.18, 1.33],
              [0, 1.22, 1.27],
              [1, -0.21, -1.19]])

# 범주형 특성에 누락된 값이 있는 특성 행렬을 만듭니다.
X_with_nan = np.array([[np.nan, 0.87, 1.31],
                       [np.nan, -0.67, -0.22]])

# KNN 학습기를 훈련합니다.
clf = KNeighborsClassifier(3, weights='distance')
trained_model = clf.fit(X[:,1:], X[:,0])

# 누락된 값의 클래스를 예측합니다.
imputed_values = trained_model.predict(X_with_nan[:,1:])

# 예측된 클래스와 원본 특성을 열로 합칩니다.
X_with_imputed = np.hstack((imputed_values.reshape(-1,1), X_with_nan[:,1:]))

# 두 특성 행렬을 연결합니다.
np.vstack((X_with_imputed, X))
```


```python
from sklearn.impute import SimpleImputer

# 두 개의 특성 행렬을 합칩니다.
X_complete = np.vstack((X_with_nan, X))

imputer = SimpleImputer(strategy='most_frequent')
imputer.fit_transform(X_complete)
```


```python
# 라이브러리를 임포트합니다.
import numpy as np
from sklearn.ensemble import RandomForestClassifier
from sklearn.datasets import load_iris

# 붓꽃 데이터를 적재합니다.
iris = load_iris()

# 특성 행렬을 만듭니다.
features = iris.data

# 타깃 벡터를 만듭니다.
target = iris.target

# 처음 40개 샘플을 삭제합니다.
features = features[40:,:]
target = target[40:]

# 클래스 0을 음성 클래스로 하는 이진 타깃 벡터를 만듭니다.
target = np.where((target == 0), 0, 1)

# 불균형한 타깃 벡터를 확인합니다.
target
```


```python
# 가중치를 만듭니다.
weights = {0: .9, 1: 0.1}

# 가중치를 부여한 랜덤 포레스트 분류기를 만듭니다.
RandomForestClassifier(class_weight=weights)
```


```python
# 균형잡힌 클래스 가중치로 랜덤 포레스트 모델을 훈련합니다.
RandomForestClassifier(class_weight="balanced")
```


```python
# 각 클래스의 샘플 인덱스를 추출합니다.
i_class0 = np.where(target == 0)[0]
i_class1 = np.where(target == 1)[0]

# 각 클래스의 샘플 개수
n_class0 = len(i_class0)
n_class1 = len(i_class1)

# 클래스 0의 샘플만큼 클래스 1에서 중복을 허용하지 않고 랜덤하게 샘플을 뽑습니다.
# from class 1 without replacement
i_class1_downsampled = np.random.choice(i_class1, size=n_class0, replace=False)

# 클래스 0의 타깃 벡터와 다운샘플링된 클래스 1의 타깃 벡터를 합칩니다.
np.hstack((target[i_class0], target[i_class1_downsampled]))
```


```python
np.vstack((features[i_class0,:], features[i_class1_downsampled,:]))[0:5]
```


```python
# 클래스 1의 샘플 개수만큼 클래스 0에서 중복을 허용하여 랜덤하게 샘플을 선택합니다.
i_class0_upsampled = np.random.choice(i_class0, size=n_class1, replace=True)

# 클래스 0의 업샘플링된 타깃 벡터와 클래스 1의 타깃 벡터를 합칩니다.
np.concatenate((target[i_class0_upsampled], target[i_class1]))
```


```python
# 클래스 0의 업샘플링된 특성 행렬과 클래스 1의 특성 행렬을 합칩니다.
np.vstack((features[i_class0_upsampled,:], features[i_class1,:]))[0:5]
```



```python
# 텍스트를 만듭니다.
text_data = ["   Interrobang. By Aishwarya Henriette     ",
             "Parking And Going. By Karl Gautier",
             "    Today Is The night. By Jarek Prakash   "]

# 공백 문자를 제거합니다.
strip_whitespace = [string.strip() for string in text_data]

# 텍스트를 확인합니다.
strip_whitespace
```


```python
# 마침표를 제거합니다.
remove_periods = [string.replace(".", "") for string in strip_whitespace]

# 텍스트를 확인합니다.
remove_periods
```


```python
# 함수를 만듭니다.
def capitalizer(string: str) -> str:
    return string.upper()

# 함수를 적용합니다.
[capitalizer(string) for string in remove_periods]
```


```python
# 라이브러리를 임포트합니다.
import re

# 함수를 만듭니다.
def replace_letters_with_X(string: str) -> str:
    return re.sub(r"[a-zA-Z]", "X", string)

# 함수를 적용합니다.
[replace_letters_with_X(string) for string in remove_periods]
```


```python
# 라이브러리를 임포트합니다.
from bs4 import BeautifulSoup

# 예제 HTML 코드를 만듭니다.
html = """
       <div class='full_name'><span style='font-weight:bold'>
       Masego</span> Azra</div>"
       """

# html을 파싱합니다.
soup = BeautifulSoup(html, "lxml")

# "full_name" 이름의 클래스를 가진 div를 찾아 텍스트를 출력합니다.
soup.find("div", { "class" : "full_name" }).text
```


```python
# 라이브러리를 임포트합니다.
import unicodedata
import sys

# 텍스트를 만듭니다.
text_data = ['Hi!!!! I. Love. This. Song....',
             '10000% Agree!!!! #LoveIT',
             'Right?!?!']

# 구두점 문자로 이루어진 딕셔너리를 만듭니다.
punctuation = dict.fromkeys(i for i in range(sys.maxunicode)
                            if unicodedata.category(chr(i)).startswith('P'))

# 문자열의 구두점을 삭제합니다.
[string.translate(punctuation) for string in text_data]
```


```python
# 구두점 데이터를 다운로드합니다.
import nltk
nltk.download('punkt')
```


```python
# 라이브러리를 임포트합니다.
from nltk.tokenize import word_tokenize

# 텍스트를 만듭니다.
string = "The science of today is the technology of tomorrow"

# 단어를 토큰으로 나눕니다.
word_tokenize(string)
```


```python
# 라이브러리를 임포트합니다.
from nltk.tokenize import sent_tokenize

# 텍스트를 만듭니다.
string = "The science of today is the technology of tomorrow. Tomorrow is today."

# 문장으로 나눕니다.
sent_tokenize(string)
```


```python
# 불용어 데이터를 다운로드합니다.
import nltk
nltk.download('stopwords')
```


```python
# 라이브러리를 임포트합니다.
from nltk.corpus import stopwords

# 단어 토큰을 만듭니다.
tokenized_words = ['i',
                   'am',
                   'going',
                   'to',
                   'go',
                   'to',
                   'the',
                   'store',
                   'and',
                   'park']

# 불용어를 적재합니다.
stop_words = stopwords.words('english')

# 불용어를 삭제합니다.
[word for word in tokenized_words if word not in stop_words]
```


```python
# 불용어를 확인합니다.
stop_words[:5]
```


```python
stopwords.abspath
```


```python
from sklearn.feature_extraction.text import ENGLISH_STOP_WORDS

len(ENGLISH_STOP_WORDS), len(stop_words)
```


```python
list(ENGLISH_STOP_WORDS)[:5]
```


```python
# 라이브러리를 임포트합니다.
from nltk.stem.porter import PorterStemmer

# 단어 토큰을 만듭니다.
tokenized_words = ['i', 'am', 'humbled', 'by', 'this', 'traditional', 'meeting']

# 어간 추출기를 만듭니다.
porter = PorterStemmer()

# 어간 추출기를 적용합니다.
[porter.stem(word) for word in tokenized_words]
```


```python
# 태거를 다운로드합니다.
import nltk
nltk.download('averaged_perceptron_tagger')
```


```python
# 라이브러리를 임포트합니다.
from nltk import pos_tag
from nltk import word_tokenize

# 텍스트를 만듭니다.
text_data = "Chris loved outdoor running"

# 사전 훈련된 품사 태깅을 사용합니다.
text_tagged = pos_tag(word_tokenize(text_data))

# 품사를 확인합니다.
text_tagged
```


```python
# 단어를 필터링합니다.
[word for word, tag in text_tagged if tag in ['NN','NNS','NNP','NNPS'] ]
```


```python
from sklearn.preprocessing import MultiLabelBinarizer

# 텍스트를 만듭니다.
tweets = ["I am eating a burrito for breakfast",
          "Political science is an amazing field",
          "San Francisco is an awesome city"]

# 빈 리스트를 만듭니다.
tagged_tweets = []

# 각 단어와 트윗을 태깅합니다.
for tweet in tweets:
    tweet_tag = nltk.pos_tag(word_tokenize(tweet))
    tagged_tweets.append([tag for word, tag in tweet_tag])

# 원-핫 인코딩을 사용하여 태그를 특성으로 변환합니다.
one_hot_multi = MultiLabelBinarizer()
one_hot_multi.fit_transform(tagged_tweets)
```


```python
# 특성 이름을 확인합니다.
one_hot_multi.classes_
```


```python
# 브라운 코퍼스를 다운로드합니다.
import nltk
nltk.download('brown')
```


```python
# 라이브러리를 임포트합니다.
from nltk.corpus import brown
from nltk.tag import UnigramTagger
from nltk.tag import BigramTagger
from nltk.tag import TrigramTagger

# 브라운 코퍼스에서 텍스트를 추출한 다음 문장으로 나눕니다.
sentences = brown.tagged_sents(categories='news')

# 4,000개의 문장은 훈련용으로 623개는 테스트용으로 나눕니다.
train = sentences[:4000]
test = sentences[4000:]

# 백오프 태그 객체를 만듭니다.
unigram = UnigramTagger(train)
bigram = BigramTagger(train, backoff=unigram)
trigram = TrigramTagger(train, backoff=bigram)

# 정확도를 확인합니다.
trigram.evaluate(test)
```


```python
# 코랩에서 실행하는 경우 다음 주석을 제거하고 실행하세요.
#!pip install konlpy
```


```python
from konlpy.tag import Okt
okt = Okt()
```


```python
text = '태양계는 지금으로부터 약 46억 년 전, 거대한 분자 구름의 일부분이 중력 붕괴를 일으키면서 형성되었다'

okt.pos(text)
```


```python
okt.morphs(text)
```


```python
okt.nouns(text)
```


```python
# 라이브러리를 임포트합니다.
import numpy as np
from sklearn.feature_extraction.text import CountVectorizer

# 텍스트를 만듭니다.
text_data = np.array(['I love Brazil. Brazil!',
                      'Sweden is best',
                      'Germany beats both'])

# BoW 특성 행렬을 만듭니다.
count = CountVectorizer()
bag_of_words = count.fit_transform(text_data)

# 특성 행렬을 확인합니다.
bag_of_words
```


```python
bag_of_words.toarray()
```


```python
# 특성 이름을 확인합니다.
count.get_feature_names()
```


```python
# 옵션을 지정하여 특성 행렬을 만듭니다.
count_2gram = CountVectorizer(ngram_range=(1,2),
                              stop_words="english",
                              vocabulary=['brazil'])
bag = count_2gram.fit_transform(text_data)

# 특성 행렬을 확인합니다.
bag.toarray()
```


```python
# 1-그램과 2-그램을 확인합니다.
count_2gram.vocabulary_
```


```python
# 라이브러리를 임포트합니다.
import numpy as np
from sklearn.feature_extraction.text import TfidfVectorizer

# 텍스트를 만듭니다.
text_data = np.array(['I love Brazil. Brazil!',
                      'Sweden is best',
                      'Germany beats both'])

# tf-idf 특성 행렬을 만듭니다.
tfidf = TfidfVectorizer()
feature_matrix = tfidf.fit_transform(text_data)

# tf-idf 특성 행렬을 확인합니다.
feature_matrix
```


```python
# tf-idf 특성 행렬을 밀집 배열로 확인합니다.
feature_matrix.toarray()
```


```python
# 특성 이름을 확인합니다.
tfidf.vocabulary_
```



```python
# 라이브러리를 임포트합니다.
import numpy as np
import pandas as pd

# 문자열을 만듭니다.
date_strings = np.array(['03-04-2005 11:35 PM',
                         '23-05-2010 12:01 AM',
                         '04-09-2009 09:09 PM'])

# Timestamp 객체로 바꿉니다.
[pd.to_datetime(date, format='%d-%m-%Y %I:%M %p') for date in date_strings]
```


```python
# datetime으로 바꿉니다.
[pd.to_datetime(date, format="%d-%m-%Y %I:%M %p", errors="ignore")
for date in date_strings]
```


```python
pd.to_datetime(date_strings)
```


```python
# 라이브러리를 임포트합니다.
import pandas as pd

# datetime을 만듭니다.
pd.Timestamp('2017-05-01 06:00:00', tz='Europe/London')
```




    Timestamp('2017-05-01 06:00:00+0100', tz='Europe/London')




```python
# datetime을 만듭니다. 
date = pd.Timestamp('2017-05-01 06:00:00')

# 시간대를 지정합니다.
date_in_london = date.tz_localize('Europe/London')

# datetime을 확인합니다.
date_in_london
```


```python
# 시간대를 바꿉니다.
date_in_london.tz_convert('Africa/Abidjan')
```


```python
# 세 개의 날짜를 만듭니다.
dates = pd.Series(pd.date_range('2/2/2002', periods=3, freq='M'))

# 시간대를 지정합니다.
dates.dt.tz_localize('Africa/Abidjan')
```


```python
# 라이브러리를 임포트합니다.
from pytz import all_timezones

# 두 개의 시간대를 확인합니다.
all_timezones[0:2]
```


```python
dates.dt.tz_localize('dateutil/Aisa/Seoul')
```


```python
import pytz

tz = pytz.timezone('Asia/Seoul')
dates.dt.tz_localize(tz)
```


```python
# 라이브러리를 임포트합니다.
import pandas as pd

# 데이터프레임을 만듭니다.
dataframe = pd.DataFrame()

# datetime을 만듭니다.
dataframe['date'] = pd.date_range('1/1/2001', periods=100000, freq='H')

# 두 datetime 사이의 샘플을 선택합니다.
dataframe[(dataframe['date'] > '2002-1-1 01:00:00') &
          (dataframe['date'] <= '2002-1-1 04:00:00')]
```


```python
# 인덱스를 설정합니다.
dataframe = dataframe.set_index(dataframe['date'])

# 두 datetime 사이 샘플을 선택합니다.
dataframe.loc['2002-1-1 01:00:00':'2002-1-1 04:00:00']
```


```python
# 라이브러리를 임포트합니다.
import pandas as pd

# 데이터프레임을 만듭니다.
dataframe = pd.DataFrame()

# 다섯 개의 날짜를 만듭니다.
dataframe['date'] = pd.date_range('1/1/2001', periods=150, freq='W')

# 년, 월, 일, 시, 분에 대한 특성을 만듭니다.
dataframe['year'] = dataframe['date'].dt.year
dataframe['month'] = dataframe['date'].dt.month
dataframe['day'] = dataframe['date'].dt.day
dataframe['hour'] = dataframe['date'].dt.hour
dataframe['minute'] = dataframe['date'].dt.minute

# 세 개의 행을 확인합니다.
dataframe.head(3)
```


```python
# 라이브러리를 임포트합니다.
import pandas as pd

# 데이터프레임을 만듭니다.
dataframe = pd.DataFrame()

# 두 datetime 특성을 만듭니다.
dataframe['Arrived'] = [pd.Timestamp('01-01-2017'), pd.Timestamp('01-04-2017')]
dataframe['Left'] = [pd.Timestamp('01-01-2017'), pd.Timestamp('01-06-2017')]

# 특성 사이의 차이를 계산합니다.
dataframe['Left'] - dataframe['Arrived']
```


```python
# 특성 간의 기간을 계산합니다.
pd.Series(delta.days for delta in (dataframe['Left'] - dataframe['Arrived']))
```


```python
# 라이브러리를 임포트합니다.
import pandas as pd

# 시리즈 객체를 만듭니다.
dates = pd.Series(pd.date_range("2/2/2002", periods=3, freq="M"))

# 요일을 확인합니다.
dates.dt.day_name()
```


```python
# 요일을 확인합니다.
dates.dt.weekday
```


```python
# 라이브러리를 임포트합니다.
import pandas as pd

# 데이터프레임을 만듭니다.
dataframe = pd.DataFrame()

# 날짜를 만듭니다.
dataframe["dates"] = pd.date_range("1/1/2001", periods=5, freq="D")
dataframe["stock_price"] = [1.1,2.2,3.3,4.4,5.5]

# 한 행 뒤의 값을 가져옵니다.
dataframe["previous_days_stock_price"] = dataframe["stock_price"].shift(1)

# 데이터프레임을 확인합니다.
dataframe
```


```python
# 라이브러리를 임포트합니다.
import pandas as pd

# datetime을 만듭니다.
time_index = pd.date_range("01/01/2010", periods=5, freq="M")

# 데이터프레임을 만들고 인덱스를 설정합니다.
dataframe = pd.DataFrame(index=time_index)

# 특성을 만듭니다.
dataframe["Stock_Price"] = [1,2,3,4,5]

# 이동 평균을 계산합니다.
dataframe.rolling(window=2).mean()
```


```python
dataframe.ewm(alpha=0.5).mean()
```


```python
# 라이브러리를 임포트합니다.
import pandas as pd
import numpy as np

# 날짜를 만듭니다.
time_index = pd.date_range("01/01/2010", periods=5, freq="M")

# 데이터프레임을 만들고 인덱스를 지정합니다.
dataframe = pd.DataFrame(index=time_index)

# 누락된 값이 있는 특성을 만듭니다.
dataframe["Sales"] = [1.0,2.0,np.nan,np.nan,5.0]

# 누락된 값을 보간합니다.
dataframe.interpolate()
```


```python
# 앞쪽으로 채우기(Forward-fill)
dataframe.ffill()
```


```python
# 뒤쪽으로 채우기(Back-fill)
dataframe.bfill()
```


```python
# 누락된 값을 보간하기
dataframe.interpolate(method="quadratic")
```


```python
# 누락된 값을 보간하기
dataframe.interpolate(limit=1, limit_direction="forward")
```



```python
import cv2
import matplotlib.pyplot as plt

img_basic = cv2.imread('images/cat.jpg', cv2.IMREAD_COLOR)
#print(img_basic)
print(type(img_basic))
print(img_basic.ndim)
plt.imshow(cv2.cvtColor(img_basic, cv2.COLOR_BGR2RGB))
plt.show()

img_basic = cv2.cvtColor(img_basic, cv2.COLOR_BGR2GRAY)
plt.imshow(cv2.cvtColor(img_basic, cv2.COLOR_GRAY2RGB))
plt.show()
```


```python
import cv2
image = cv2.imread('images/cat.jpg')

# 픽셀 수 및 이미지 크기 확인
print(image.shape)
print(image.size)

# 이미지 Numpy 객체의 특정 픽셀을 가리킵니다.
px = image[100, 100]

# B, G, R 순서로 출력됩니다.
# (단, Gray Scale인 경우에는 B, G, R로 구분되지 않습니다.)
print(px)

# R 값만 출력하기
print(px[2])
```


```python
import cv2
import matplotlib.pyplot as plt

image = cv2.imread('images/cat.jpg')

# Numpy Slicing: ROI 처리 가능
roi = image[200:350, 50:200]

# ROI 단위로 이미지 복사하기
image[0:150, 0:150] = roi

plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
plt.show()
```


```python
import cv2
import matplotlib.pyplot as plt

image = cv2.imread('images/cat.jpg')
print(image)
print(image[:, :, 2])
image[:, :, 2] = 0
print(image)
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
plt.show()
```


```python
# 라이브러리를 임포트합니다.
import cv2
import numpy as np
from matplotlib import pyplot as plt

# 흑백 이미지로 로드합니다.
image = cv2.imread("images/plane.jpg", cv2.IMREAD_GRAYSCALE)
```


```python
from matplotlib import pyplot as plt
```


```python
# 이미지를 출력합니다.
plt.imshow(image, cmap="gray"), plt.axis("off")
plt.show()
```


```python
# 데이터 타입을 확인합니다.
type(image)
```


```python
# 이미지 데이터를 확인합니다.
image
```


```python
# 차원을 확인합니다.
image.shape
```


```python
# 컬러로 이미지를 로드합니다.
image_bgr = cv2.imread("images/plane.jpg", cv2.IMREAD_COLOR)

# 픽셀을 확인합니다.
image_bgr[0,0]
```


```python
# RGB로 변환합니다.
image_rgb = cv2.cvtColor(image_bgr, cv2.COLOR_BGR2RGB)

# 이미지를 출력합니다.
plt.imshow(image_rgb), plt.axis("off")
plt.show()
```


```python
# 라이브러리를 임포트합니다.
import cv2
import numpy as np
from matplotlib import pyplot as plt

# 흑백 이미지로 로드합니다.
image = cv2.imread("images/plane.jpg", cv2.IMREAD_GRAYSCALE)

# 이미지를 저장합니다.
cv2.imwrite("images/plane_new.jpg", image)
```


```python
# 코랩에서 실행하는 경우 다음 주석을 제거하고 실행하세요.
#!wget https://github.com/rickiepark/machine-learning-with-python-cookbook/raw/master/images/plane_256x256.jpg -O images/plane_256x256.jpg
```


```python
# 라이브러리를 임포트합니다.
import cv2
import numpy as np
from matplotlib import pyplot as plt

# 흑백 이미지로 로드합니다.
image = cv2.imread("images/plane_256x256.jpg", cv2.IMREAD_GRAYSCALE)

# 이미지 크기를 50x50 픽셀로 바꿉니다.
image_50x50 = cv2.resize(image, (50, 50))

# 이미지를 출력합니다.
plt.imshow(image_50x50, cmap="gray"), plt.axis("off")
plt.show()
```


```python
# 라이브러리를 임포트합니다.
import cv2
import numpy as np
from matplotlib import pyplot as plt

# 흑백 이미지로 로드합니다.
image = cv2.imread("images/plane_256x256.jpg", cv2.IMREAD_GRAYSCALE)

# 열의 처음 절반과 모든 행을 선택합니다.
image_cropped = image[:,:128]

# 이미지를 출력합니다.
plt.imshow(image_cropped, cmap="gray"), plt.axis("off")
plt.show()
```


```python
# 라이브러리를 임포트합니다.
import cv2
import numpy as np
from matplotlib import pyplot as plt

# 흑백 이미지로 로드합니다.
image = cv2.imread("images/plane_256x256.jpg", cv2.IMREAD_GRAYSCALE)

# 이미지를 흐리게 합니다.
image_blurry = cv2.blur(image, (5,5))

# 이미지를 출력합니다.
plt.imshow(image_blurry, cmap="gray"), plt.axis("off")
plt.show()
```


```python
# 이미지를 흐리게 합니다.
image_very_blurry = cv2.blur(image, (100,100))

# 이미지를 출력합니다.
plt.imshow(image_very_blurry, cmap="gray"), plt.xticks([]), plt.yticks([])
plt.show()
```


```python
# 커널을 만듭니다.
kernel = np.ones((5,5)) / 25.0

# 커널을 확인합니다.
kernel
```


```python
# 커널을 적용합니다.
image_kernel = cv2.filter2D(image, -1, kernel)

# 이미지를 출력합니다.
plt.imshow(image_kernel, cmap="gray"), plt.xticks([]), plt.yticks([])
plt.show()
```


```python
#  가우시안 블러를 적용합니다.
image_very_blurry = cv2.GaussianBlur(image, (5,5), 0)

# 이미지를 출력합니다.
plt.imshow(image_very_blurry, cmap="gray"), plt.xticks([]), plt.yticks([])
plt.show()
```


```python
gaus_vector = cv2.getGaussianKernel(5, 0)
gaus_vector
```


```python
# 벡터를 외적하여 커널을 만듭니다.
gaus_kernel = np.outer(gaus_vector, gaus_vector)
gaus_kernel
```


```python
# 커널을 적용합니다.
image_kernel = cv2.filter2D(image, -1, gaus_kernel)

# 이미지를 출력합니다.
plt.imshow(image_kernel, cmap="gray"), plt.xticks([]), plt.yticks([])
plt.show()
```


```python
# 라이브러리를 임포트합니다.
import cv2
import numpy as np
from matplotlib import pyplot as plt

# 흑백 이미지로 로드합니다.
image = cv2.imread("images/plane_256x256.jpg", cv2.IMREAD_GRAYSCALE)

# 커널을 만듭니다.
kernel = np.array([[0, -1, 0],
                   [-1, 5,-1],
                   [0, -1, 0]])

# 이미지를 선명하게 만듭니다.
image_sharp = cv2.filter2D(image, -1, kernel)

# 이미지를 출력합니다.
plt.imshow(image_sharp, cmap="gray"), plt.axis("off")
plt.show()
```


```python
# 라이브러리를 임포트합니다.
import cv2
import numpy as np
from matplotlib import pyplot as plt

# 흑백 이미지로 로드합니다.
image = cv2.imread("images/plane_256x256.jpg", cv2.IMREAD_GRAYSCALE)

# 이미지 대비를 향상시킵니다.
image_enhanced = cv2.equalizeHist(image)

# 이미지를 출력합니다.
plt.imshow(image_enhanced, cmap="gray"), plt.axis("off")
plt.show()
```


```python
# 이미지를 로드합니다.
image_bgr = cv2.imread("images/plane.jpg")

# YUV로 바꿉니다.
image_yuv = cv2.cvtColor(image_bgr, cv2.COLOR_BGR2YUV)

# 히스토그램 평활화를 적용합니다.
image_yuv[:, :, 0] = cv2.equalizeHist(image_yuv[:, :, 0])

# RGB로 바꿉니다.
image_rgb = cv2.cvtColor(image_yuv, cv2.COLOR_YUV2RGB)

# 이미지를 출력합니다.
plt.imshow(image_rgb), plt.axis("off")
plt.show()
```


```python
# 라이브러리를 임포트합니다.
import cv2
import numpy as np
from matplotlib import pyplot as plt

# 이미지를 로드합니다.
image_bgr = cv2.imread('images/plane_256x256.jpg')

# BGR에서 HSV로 변환합니다.
image_hsv = cv2.cvtColor(image_bgr, cv2.COLOR_BGR2HSV)

# HSV에서 파랑 값의 범위를 정의합니다.
lower_blue = np.array([50,100,50])
upper_blue = np.array([130,255,255])

# 마스크를 만듭니다.
mask = cv2.inRange(image_hsv, lower_blue, upper_blue)

# 이미지에 마스크를 적용합니다.
image_bgr_masked = cv2.bitwise_and(image_bgr, image_bgr, mask=mask)

# BGR에서 RGB로 변환합니다.
image_rgb = cv2.cvtColor(image_bgr_masked, cv2.COLOR_BGR2RGB)

# 이미지를 출력합니다.
plt.imshow(image_rgb), plt.axis("off")
plt.show()
```


```python
# 마스크를 출력합니다.
plt.imshow(mask, cmap='gray'), plt.axis("off")
plt.show()
```


```python
# 라이브러리를 임포트합니다.
import cv2
import numpy as np
from matplotlib import pyplot as plt

# 흑백 이미지로 로드합니다.
image_grey = cv2.imread("images/plane_256x256.jpg", cv2.IMREAD_GRAYSCALE)

# 적응적 임계처리를 적용합니다.
max_output_value = 255
neighborhood_size = 99
subtract_from_mean = 10
image_binarized = cv2.adaptiveThreshold(image_grey,
                                        max_output_value,
                                        cv2.ADAPTIVE_THRESH_GAUSSIAN_C,
                                        cv2.THRESH_BINARY,
                                        neighborhood_size,
                                        subtract_from_mean)

# 이미지를 출력합니다.
plt.imshow(image_binarized, cmap="gray"), plt.axis("off")
plt.show()
```


```python
# cv2.ADAPTIVE_THRESH_MEAN_C를 적용합니다.
image_mean_threshold = cv2.adaptiveThreshold(image_grey,
                                             max_output_value,
                                             cv2.ADAPTIVE_THRESH_MEAN_C,
                                             cv2.THRESH_BINARY,
                                             neighborhood_size,
                                             subtract_from_mean)

# 이미지를 출력합니다.
plt.imshow(image_mean_threshold, cmap="gray"), plt.axis("off")
plt.show()
```


```python
# 라이브러리를 임포트합니다.
import cv2
import numpy as np
from matplotlib import pyplot as plt

# 이미지를 로드하고 RGB로 변환합니다.
image_bgr = cv2.imread('images/plane_256x256.jpg')
image_rgb = cv2.cvtColor(image_bgr, cv2.COLOR_BGR2RGB)

# 사각형 좌표: 시작점의 x, 시작점의 y, 너비, 높이
rectangle = (0, 56, 256, 150)

# 초기 마스크를 만듭니다.
mask = np.zeros(image_rgb.shape[:2], np.uint8)

# grabCut에 사용할 임시 배열을 만듭니다.
bgdModel = np.zeros((1, 65), np.float64)
fgdModel = np.zeros((1, 65), np.float64)

# grabCut을 실행합니다.
cv2.grabCut(image_rgb, # 원본 이미지
            mask, # 마스크
            rectangle, # 사각형
            bgdModel, # 배경을 위한 임시 배열
            fgdModel, # 전경을 위한 임시 배열
            5, # 반복 횟수
            cv2.GC_INIT_WITH_RECT) # 사각형을 사용한 초기화

# 배경인 곳은 0, 그외에는 1로 설정한 마스크를 만듭니다.
mask_2 = np.where((mask==2) | (mask==0), 0, 1).astype('uint8')

# 이미지에 새로운 마스크를 곱해 배경을 제외합니다.
image_rgb_nobg = image_rgb * mask_2[:, :, np.newaxis]

# 이미지를 출력합니다.
plt.imshow(image_rgb_nobg), plt.axis("off")
plt.show()
```


```python
# 마스크를 출력합니다.
plt.imshow(mask, cmap='gray'), plt.axis("off")
plt.show()
```


```python
# 마스크를 출력합니다.
plt.imshow(mask_2, cmap='gray'), plt.axis("off")
plt.show()
```


```python
# 라이브러리를 임포트합니다.
import cv2
import numpy as np
from matplotlib import pyplot as plt

# 흑백 이미지로 로드합니다.
image_gray = cv2.imread("images/plane_256x256.jpg", cv2.IMREAD_GRAYSCALE)

# 픽셀 강도의 중간값을 계산합니다.
median_intensity = np.median(image_gray)

# 중간 픽셀 강도에서 위아래 1 표준 편차 떨어진 값을 임계값으로 지정합니다.
lower_threshold = int(max(0, (1.0 - 0.33) * median_intensity))
upper_threshold = int(min(255, (1.0 + 0.33) * median_intensity))

# 캐니 경계선 감지기를 적용합니다.
image_canny = cv2.Canny(image_gray, lower_threshold, upper_threshold)

# 이미지를 출력합니다.
plt.imshow(image_canny, cmap="gray"), plt.axis("off")
plt.show()
```


```python
# 라이브러리를 임포트합니다.
import cv2
import numpy as np
from matplotlib import pyplot as plt

# 흑백 이미지로 로드합니다.
image_bgr = cv2.imread("images/plane_256x256.jpg")
image_gray = cv2.cvtColor(image_bgr, cv2.COLOR_BGR2GRAY)
image_gray = np.float32(image_gray)

# 모서리 감지 매개변수를 설정합니다.
block_size = 2
aperture = 29
free_parameter = 0.04

# 모서리를 감지합니다.
detector_responses = cv2.cornerHarris(image_gray,
                                      block_size,
                                      aperture,
                                      free_parameter)

# 모서리 표시를 부각시킵니다.
detector_responses = cv2.dilate(detector_responses, None)

# 임계값보다 큰 감지 결과만 남기고 흰색으로 표시합니다.
threshold = 0.02
image_bgr[detector_responses >
          threshold *
          detector_responses.max()] = [255,255,255]

# 흑백으로 변환합니다.
image_gray = cv2.cvtColor(image_bgr, cv2.COLOR_BGR2GRAY)

# 이미지를 출력합니다.
plt.imshow(image_gray, cmap="gray"), plt.axis("off")
plt.show()
```


```python
# 가능성이 높은 모서리를 출력합니다.
plt.imshow(detector_responses, cmap='gray'), plt.axis("off")
plt.show()
```


```python
# 이미지를 로드합니다.
image_bgr = cv2.imread('images/plane_256x256.jpg')
image_gray = cv2.cvtColor(image_bgr, cv2.COLOR_BGR2GRAY)

# 감지할 모서리 개수
corners_to_detect = 10
minimum_quality_score = 0.05
minimum_distance = 25

# 모서리를 감지합니다.
corners = cv2.goodFeaturesToTrack(image_gray,
                                  corners_to_detect,
                                  minimum_quality_score,
                                  minimum_distance)
corners = np.float32(corners)

# 모서리마다 흰 원을 그립니다.
for corner in corners:
    x, y = corner[0]
    cv2.circle(image_bgr, (x,y), 10, (255,255,255), -1)

# 흑백 이미지로 변환합니다.
image_rgb = cv2.cvtColor(image_bgr, cv2.COLOR_BGR2GRAY)

# 이미지를 출력합니다.
plt.imshow(image_rgb, cmap='gray'), plt.axis("off")
plt.show()
```


```python
# 이미지를 로드합니다.
import cv2
import numpy as np
from matplotlib import pyplot as plt

# 흑백 이미지로 로드합니다.
image = cv2.imread("images/plane_256x256.jpg", cv2.IMREAD_GRAYSCALE)

# 이미지를 10x10 픽셀 크기로 변환합니다.
image_10x10 = cv2.resize(image, (10, 10))

# 이미지 데이터를 1차원 벡터로 변환합니다.
image_10x10.flatten()
```


```python
plt.imshow(image_10x10, cmap="gray"), plt.axis("off")
plt.show()
```


```python
image_10x10.shape
```


```python
image_10x10.flatten().shape
```


```python
# 컬러 이미지로 로드합니다.
image_color = cv2.imread("images/plane_256x256.jpg", cv2.IMREAD_COLOR)

# 이미지를 10 × 10 픽셀 크기로 변환합니다.
image_color_10x10 = cv2.resize(image_color, (10, 10))

# 이미지 데이터를 1차원 벡터로 변환하고 차원을 출력합니다.
image_color_10x10.flatten().shape
```


```python
# 흑백 이미지로 로드합니다.
image_256x256_gray = cv2.imread("images/plane_256x256.jpg", cv2.IMREAD_GRAYSCALE)

# 이미지 데이터를 1차원 벡터로 변환하고 차원을 출력합니다.
image_256x256_gray.flatten().shape
```


```python
# 컬러 이미지로 로드합니다.
image_256x256_color = cv2.imread("images/plane_256x256.jpg", cv2.IMREAD_COLOR)

# 이미지 데이터를 1차원 벡터로 변환하고 차원을 출력합니다.
image_256x256_color.flatten().shape
```


```python
# 라이브러리를 임포트합니다.
import cv2
import numpy as np
from matplotlib import pyplot as plt

# BGR 이미지로 로드합니다.
image_bgr = cv2.imread("images/plane_256x256.jpg", cv2.IMREAD_COLOR)

# 각 채널의 평균을 계산합니다.
channels = cv2.mean(image_bgr)

# 파랑과 빨강을 바꿉니다(BGR에서 RGB로 만듭니다)
observation = np.array([(channels[2], channels[1], channels[0])])

# 채널 평균 값을 확인합니다.
observation
```


```python
# 이미지를 출력합니다.
plt.imshow(observation), plt.axis("off")
plt.show()
```


```python
# 라이브러리를 임포트합니다.
import cv2
import numpy as np
from matplotlib import pyplot as plt

# 이미지를 로드합니다.
image_bgr = cv2.imread("images/plane_256x256.jpg", cv2.IMREAD_COLOR)

# RGB로 변환합니다.
image_rgb = cv2.cvtColor(image_bgr, cv2.COLOR_BGR2RGB)

# 특성 값을 담을 리스트를 만듭니다.
features = []

# 각 컬러 채널에 대해 히스토그램을 계산합니다.
colors = ("r","g","b")

# 각 채널을 반복하면서 히스토그램을 계산하고 리스트에 추가합니다.
for i, channel in enumerate(colors):
    histogram = cv2.calcHist([image_rgb], # 이미지
                        [i], # 채널 인덱스
                        None, # 마스크 없음
                        [256], # 히스토그램 크기
                        [0,256]) # 범위
    features.extend(histogram)

# 샘플의 특성 값으로 벡터를 만듭니다.
observation = np.array(features).flatten()

# 처음 다섯 개의 특성을 출력합니다.
observation[0:5]
```


```python
# RGB 채널 값을 확인합니다.
image_rgb[0,0]
```


```python
# 판다스를 임포트합니다.
import pandas as pd

# 예시 데이터를 만듭니다.
data = pd.Series([1, 1, 2, 2, 3, 3, 3, 4, 5])

# 히스토그램을 출력합니다.
data.hist(grid=False)
plt.show()
```


```python
# 각 컬러 채널에 대한 히스토그램을 계산합니다.
colors = ("r","g","b")

# 컬러 채널을 반복하면서 히스토그램을 계산하고 그래프를 그립니다.
for i, channel in enumerate(colors):
    histogram = cv2.calcHist([image_rgb], # 이미지
                        [i], # 채널 인덱스
                        None, # 마스크 없음
                        [256], # 히스토그램 크기
                        [0,256]) # 범위
    plt.plot(histogram, color = channel)
    plt.xlim([0,256])

# 그래프를 출력합니다.
plt.show()
```



# 파이썬으로 구현하는 텍스트 분석(자연어 처리)

-----

### 1. koNLPy를 활용한 형태소 분석

### 2. 워드 클라우드

### 3. 한국어 기반의 자연어 처리 모듈 - nltk

### 4. 텍스트 전처리

### 5. 카운트 기반의 단어 표현

### 6. 한글 자모 분해와 결합

## *KoNLPy : 한국어 정보처리를 위한 파이썬 패키지 (https://konlpy.org/ko/latest/)

## 1. koNLPy를 활용한 형태소 분석


```python
from konlpy.tag import Kkma
from konlpy.utils import pprint
import pandas as pd
import numpy as np 
```


```python
kkma = Kkma()
```


```python
pprint(kkma.sentences('네, 안녕하세요. 반갑습니다.'))
```


```python
pprint(kkma.nouns('질문이나 건의사항은 깃헙 이슈 트래커에 남겨주세요.'))

```


```python
pprint(kkma.pos('오류보고는 실행환경, 에러메세지와함께 설명을 최대한상세히!^^'))
```

### [형태소 분석기 비교]


```python
sample = '이것은 형태소 분석기 입니다 아버지가방에들어가신다'
```


```python
from konlpy.tag import Hannanum  
hannanum = Hannanum() 
pprint(hannanum.nouns(sample))
pprint(hannanum.morphs(sample))
pprint(hannanum.pos(sample))
```


```python
kkma = Kkma() 
pprint(kkma.nouns(sample))
pprint(kkma.morphs(sample))
pprint(kkma.pos(sample))
```


```python
from konlpy.tag import Okt        ## 다른 형태소를 클래스를 가져온다. 트위터
okt = Okt()
pprint(okt.nouns(sample))
pprint(okt.morphs(sample))
pprint(okt.pos(sample))
```


```python
from konlpy.tag import Komoran                    ## 다른 형태소 분석을 하는 클래스를 사용한다 
komoran = Komoran()
pprint(komoran.nouns(sample))
pprint(komoran.morphs(sample))
pprint(komoran.pos(sample))
```


```python
hannanum.tagset
```


```python
kkma.tagset
```


```python
okt.tagset
```


```python
komoran.tagset
```


```python
tagsets = pd.DataFrame()                            ## 빈 데이터프레임을 만든다. 
N = 67

                                                   ##  한글 형태소 분서기에 있는 품사에 대한 정보를 데이터프레임에 넣는다. 
tagsets["Hannanum-기호"] = list(hannanum.tagset.keys()) + list("*" * (N - len(hannanum.tagset)))
tagsets["Hannanum-품사"] = list(hannanum.tagset.values()) + list("*" * (N - len(hannanum.tagset)))
tagsets["Kkma-기호"] = list(kkma.tagset.keys()) + list("*" * (N - len(kkma.tagset)))
tagsets["Kkma-품사"] = list(kkma.tagset.values()) + list("*" * (N - len(kkma.tagset)))
tagsets["Komoran-기호"] = list(komoran.tagset.keys()) + list("*" * (N - len(komoran.tagset)))
tagsets["Komoran-품사"] = list(komoran.tagset.values()) + list("*" * (N - len(komoran.tagset)))
tagsets["OKT-기호"] = list(okt.tagset.keys()) + list("*" * (N - len(okt.tagset)))
tagsets["OKT-품사"] = list(okt.tagset.values()) + list("*" * (N - len(okt.tagset)))
```


```python
display(tagsets.head(N))
```

## 2. 워드 클라우드


```python
from matplotlib import font_manager, rc
font_path = "./data/THEdog.ttf"   #폰트파일의 위치
font_name = font_manager.FontProperties(fname=font_path).get_name()
rc('font', family=font_name)
```


```python
from wordcloud import WordCloud             ## 워드 클라우드 모듈을 사용한다 
import matplotlib.pyplot as plt 
```


```python
myfontpath = "data/THEdog.ttf" 
```


```python
wordcloud = WordCloud(                        ## 워드클라우드 객체를 만들때 한글로 출력되도록 객체를 만든다 
    font_path = myfontpath,
    width = 800,
    height = 800
)
```


```python
text = "둘리 도우너 또치 마이콜 희동이 둘리 둘리 도우너 또치 토토로 둘리"
```


```python
wordcloud = wordcloud.generate(text)                   
```


```python
fig = plt.figure()
plt.imshow(wordcloud, interpolation='bilinear')               ## 워드 클라우드 이미지로 출력한다 
plt.axis('off')
plt.show()
```


```python
wordcloud = WordCloud(
    font_path = myfontpath,
    background_color='white',                     ## 배경색을 지정한다 
    width = 800,
    height = 800
)
wordcloud_ = wordcloud.generate(text)
fig = plt.figure()
plt.imshow(wordcloud, interpolation='bilinear')
plt.axis('off')
plt.show()
```


```python
keywords = {'파이썬':7, '넘파이':3, '판다스':5, '매트플롭립':2, '시본':2, '폴리엄':2}             ## 특정 단어의 빈도를 딕셔너리로 만든다 

wordcloud = wordcloud.generate_from_frequencies(keywords)        ## 빈도별로 워드클라우드를 만든다 

fig = plt.figure()
plt.imshow(wordcloud, interpolation='bilinear')
plt.axis('off')
plt.show()
```


```python
from PIL import Image                                ## 이미지 파일을 처리하는 모듈을 사용한다. 
```


```python
r2d2_mask = np.array(Image.open('data/r2d2.JPG'))       ## 이미지를 읽어와서 다차원 배열로 변환한다 
```


```python
from wordcloud import STOPWORDS  
```


```python
stopwords = set()                               ## 한글은 별도로 집합으로 불용어를 만든다 
stopwords.add("은")
stopwords.add("입니다")
stopwords.add("것인가")
stopwords.add("처럼")

wordcloud = WordCloud( stopwords=stopwords,              ## 워드 클라우드 객체를 만든다 
                          font_path = myfontpath,
                          background_color='white',
                           width = 800,
                           height = 800,
                          mask=r2d2_mask)            ## 마스크 인자에 이미지를 전달한다 
```


```python
texts = ['로봇 처럼 표시하는 것을 보기 위해 이것 은 예문 입니다 가을이라 겨울 바람 솔솔 불어오니 ',
         '여러분 의 문장을 넣 으세요 ㅎㅎㅎ 스타워즈 영화에 나오는 다양한 로봇처럼 r2d2']
```


```python
wordcloud = wordcloud.generate_from_text(texts[0]+texts[1])    ## 두 개의 문자을 연결해서 워드클라우드를 만든다 
wordcloud
```


```python
plt.figure(figsize=(8,8))
plt.imshow(wordcloud, interpolation="bilinear")         ## 이미지를 출력하면 전달된 모양에 따라 표시한다 
plt.axis("off")
plt.show()
```

## 3. 한국어 기반의 자연어 처리 모듈 : nltk


```python
import nltk                     ## 한국어 자연어처리 모듈 : pip install nltk
```


```python
from konlpy.corpus import kobill
files_ko = kobill.fileids()
```


```python
files_ko
```


```python
doc_ko = kobill.open('1809898.txt').read()         ## 특정 텍스트 파일을 읽어온다 
```


```python
t = Okt()
tokens_ko = t.nouns(doc_ko)                ## 텍스트에서 명사를 추출한다. 
print(tokens_ko[:10])
```


```python
ko_ = nltk.Text(tokens_ko, name='국군부대의 소말리아 해역 파견연장 동의안')       ## 명사로 추출한 것을 텍스트 객체로 만든다 
```


```python
type(ko_)
```


```python
len(ko_.tokens)                         ##  명사로 분리된 개수를 확인한다 
```


```python
len(set(ko_.tokens))                   ## 유일한 단어의 개수를 확인한다 
```


```python
ko_.tokens[:10]
```


```python
ko_.vocab()                    ## 동일한 단어의 발생 빈도를 확인한다. 
```


```python
import matplotlib.pyplot as plt
```


```python
from matplotlib import font_manager, rc
font_path = "data/THEdog.ttf"   #폰트파일의 위치
font_name = font_manager.FontProperties(fname=font_path).get_name()
rc('font', family=font_name)
```


```python
plt.figure(figsize=(12,6))
ko_.plot(50)                         ## 단어별로 발생빈도에 맞도록 그래프를 그린다. 
```


```python
ko_.count('파견')                  ## 특정 단어의 발생빈도를 확인한다. 
```


```python
ko_.count('소말리아')
```


```python
ko_.concordance('소말리아')             ## 특정 단어가 있는 곳은 단어를 확인한다. 
```


```python
data = ko_.vocab().most_common(150)                 ## 가장 많이 발생한 단어를 선택한다. 
```


```python
data
```


```python
wordcloud = WordCloud(font_path=myfontpath,                                    ## .한글에 대한 위치를 표시한다. 
                      relative_scaling = 0.2,
                      background_color='white',
                      ).generate_from_frequencies(dict(data))             ## .단어별 빈도수를 딕셔너리로 변환해서 전달한다 
plt.figure(figsize=(10,6))
plt.imshow(wordcloud)                                                      ## .이미지를 출력한다 
plt.axis("off")                                                            ## 그래프에 대한 축을 표시하지 않는다 
plt.show()
```

## 4. 텍스트 전처리

### ** 한국어 전처리 패키지 : PyKoSpacing & Py-Hanspell **

#### 전희원님이 개발한 PyKoSpacing은 한국어 띄어쓰기 패키지로 띄어쓰기가 되어있지 않은 문장을 띄어쓰기를 한 문장으로 변환해주는 패키지이다. PyKoSpacing은 대용량 코퍼스를 학습하여 만들어진 띄어쓰기 딥 러닝 모델로 준수한 성능을 가지고 있다.

##### pip install git+https://github.com/haven-jeon/PyKoSpacing.git

##### pip install git+https://github.com/ssut/py-hanspell.git


```python
sent = '김철수는 극중 두 인격의 사나이 이광수 역을 맡았다. 철수는 한국 유일의 태권도 전승자를 가리는 결전의 날을 앞두고 10년간 함께 훈련한 사형인 유연재(김광수 분)를 찾으러 속세로 내려온 인물이다.'
```


```python
new_sent = sent.replace(" ", '') # 띄어쓰기가 없는 문장 임의로 만들기
print(new_sent)
```


```python
from pykospacing import spacing

kospacing_sent = spacing(new_sent)
print(sent)
print(kospacing_sent)
```


```python
from hanspell import spell_checker

sent = "맞춤법 틀리면 외 않되? 쓰고싶은대로쓰면돼지 "
spelled_sent = spell_checker.check(sent)

hanspell_sent = spelled_sent.checked
print(hanspell_sent)
```


```python
spelled_sent = spell_checker.check(new_sent)

hanspell_sent = spelled_sent.checked
print(hanspell_sent)
print(kospacing_sent) 
```

### **Bag of Words(BoW) 만들기**

#### Bag of Words란 단어들의 순서는 전혀 고려하지 않고, 단어들의 출현 빈도(frequency)에만 집중하는 텍스트 데이터의 수치화 표현 방법이다.


```python
from konlpy.tag import Okt
import re  
okt=Okt()  

token=re.sub("(\.)","","정부가 발표하는 물가상승률과 소비자가 느끼는 물가상승률은 다르다.")  
# 정규 표현식을 통해 온점을 제거하는 정제 작업입니다.  
token=okt.morphs(token)  
# OKT 형태소 분석기를 통해 토큰화 작업을 수행한 뒤에, token에다가 넣습니다.  
print(token)
word2index={}  
bow=[]  
for voca in token:  
         if voca not in word2index.keys():  
             word2index[voca]=len(word2index)  
# token을 읽으면서, word2index에 없는 (not in) 단어는 새로 추가하고, 이미 있는 단어는 넘깁니다.   
             bow.insert(len(word2index)-1,1)
# BoW 전체에 전부 기본값 1을 넣어줍니다. 단어의 개수는 최소 1개 이상이기 때문입니다.  
         else:
            index=word2index.get(voca)
# 재등장하는 단어의 인덱스를 받아옵니다.
            bow[index]=bow[index]+1
# 재등장한 단어는 해당하는 인덱스의 위치에 1을 더해줍니다. (단어의 개수를 세는 것입니다.)  
print(word2index)  
```


```python
token
```


```python
from sklearn.feature_extraction.text import CountVectorizer
token = ["정부가 발표하는 물가상승률과 소비자가 느끼는 물가상승률은 다르다"]
corpus = token
vector = CountVectorizer()
print(vector.fit_transform(corpus).toarray()) # 코퍼스로부터 각 단어의 빈도 수를 기록한다.
print(vector.vocabulary_)
```

## 5. 카운트 기반의 단어 표현


```python
import pandas as pd # 데이터프레임 사용을 위해
from math import log # IDF 계산을 위해
```


```python
docs = [
  '먹고 싶은 사과',
  '먹고 싶은 바나나',
  '길고 노란 바나나 바나나',
  '저는 과일이 좋아요'
] 
vocab = list(set(w for doc in docs for w in doc.split()))
vocab.sort()
print(vocab)
```


```python
N = len(docs) # 총 문서의 수

def tf(t, d):
    return d.count(t)

def idf(t):
    df = 0
    for doc in docs:
        df += t in doc
    return log(N/(df + 1))

def tfidf(t, d):
    return tf(t,d)* idf(t)
```


```python
result = []
for i in range(N): # 각 문서에 대해서 아래 명령을 수행
    result.append([])
    d = docs[i]
    for j in range(len(vocab)):
        t = vocab[j]        
        result[-1].append(tf(t, d))

tf_ = pd.DataFrame(result, columns = vocab)
tf_
```


```python
result = []
for j in range(len(vocab)):
    t = vocab[j]
    result.append(idf(t))

idf_ = pd.DataFrame(result, index = vocab, columns = ["IDF"])
idf_
```


```python
result = []
for i in range(N):
    result.append([])
    d = docs[i]
    for j in range(len(vocab)):
        t = vocab[j]

        result[-1].append(tfidf(t,d))

tfidf_ = pd.DataFrame(result, columns = vocab)
tfidf_
```


```python
from sklearn.feature_extraction.text import CountVectorizer

corpus = [
  '먹고 싶은 사과',
  '먹고 싶은 바나나',
  '길고 노란 바나나 바나나',
  '저는 과일이 좋아요'
]
vector = CountVectorizer()
print(vector.fit_transform(corpus).toarray()) # 코퍼스로부터 각 단어의 빈도 수를 기록한다.
print(vector.vocabulary_) # 각 단어의 인덱스가 어떻게 부여되었는지를 보여준다.
```


```python
from sklearn.feature_extraction.text import TfidfVectorizer
corpus = [
  '먹고 싶은 사과',
  '먹고 싶은 바나나',
  '길고 노란 바나나 바나나',
  '저는 과일이 좋아요'
]
tfidfv = TfidfVectorizer().fit(corpus)
print(tfidfv.transform(corpus).toarray())
print(tfidfv.vocabulary_)
```


```python
from sklearn.feature_extraction.text import CountVectorizer

corpus = [
  '저는 사과 좋아요',
  '저는 바나나 좋아요',
  '저는 바나나 좋아요 저는 바나나 좋아요'
]
vector = CountVectorizer()
dtm = vector.fit_transform(corpus).toarray()
print(dtm) # 코퍼스로부터 각 단어의 빈도 수를 기록한다.
print(vector.vocabulary_) # 각 단어의 인덱스가 어떻게 부여되었는지를 보여준다.
```


```python
from numpy import dot
from numpy.linalg import norm
import numpy as np
def cos_sim(A, B):
       return dot(A, B)/(norm(A)*norm(B))
```


```python
print(cos_sim(dtm[0], dtm[1])) #문서1과 문서2의 코사인 유사도
print(cos_sim(dtm[0], dtm[2])) #문서1과 문서3의 코사인 유사도
print(cos_sim(dtm[1], dtm[2])) #문서2과 문서3의 코사인 유사도
```

## 5. 한글 자모 분해와 결합


```python
import hgtk                      ## 한글의 자음과 모음을 분리하는 모듈을 사용한다 
```

### 한글 자모 분해, 조합(오토마타), 조사 붙이기, 초/중/종 분해조합, 한글/한자/영문 여부 체크 등을 지원합니다.


```python
hgtk.letter.decompose('감')          ## 특정 글자를 분리하면 초성 중성 종성으로 분리된다 
```


```python
hgtk.letter.compose('ㄱ', 'ㅏ', 'ㅁ')      ## 분리된 글자를 하나의 글자로 합친다. 
```


```python
sample_text = '''타밀어는 드라비다어족의 남부 계통, 즉 남부드라비다어파에 속하는 언어이다.
공식어로 지정된 인도의 주요 언어 중에서 타밀어와 계통적으로 가장 가까운 것은 말라얄람어인데, 
9세기 무렵까지 말라얄람어는 타밀어의 방언이었다.
이 두 언어 간에는 선사 시대에 일어난 서부 방언(말라얄람어의 원형) 분열의 증거가 되는 많은 차이가 있지만, 
13~14세기 무렵까지도 두 언어는 완전히 서로 다른 언어로 분리되지 않은 채였다.'''
```


```python
s = hgtk.text.decompose(sample_text)        ## 여러 문장에 대해 단어를 분리한다. 
```


```python
s[:40]
```


```python
hgtk.text.compose(s)[:40]                     ## 분리된 것을 하나로 합친다. 
```


```python
hgtk.checker.is_hangul('한글입니다')           ## 한글 여부를 확인한다 
```


```python
hgtk.checker.is_hangul('no한글입니다')         ## 일부 영어가 들어가면 한글로 인식하지 않는다 
```


```python
hgtk.checker.is_hangul('it is english')
```


```python
hgtk.checker.is_hanja('大韓民國')                  ## 한자도 확인할 수 있다. 
```


```python
hgtk.checker.is_hanja('大한민국')
```


```python
hgtk.checker.is_hanja('대한민국')
```

## Josa

EUN_NEUN - 은/는


```python
hgtk.josa.attach('하늘', hgtk.josa.EUN_NEUN)                 ## 단어에 맞는 조사를 붙여볼 수 있다. 
```


```python
hgtk.josa.attach('바다', hgtk.josa.EUN_NEUN)
```


```python
hgtk.josa.attach('하늘', hgtk.josa.I_GA)
```


```python
hgtk.josa.attach('바다', hgtk.josa.I_GA)
```


```python
hgtk.josa.attach('하늘', hgtk.josa.EUL_REUL)
```


```python
hgtk.josa.attach('바다', hgtk.josa.EUL_REUL)
```


```python

```