

# 분석Day04

>  데이터 수집

### - 교육내용

```python
# pandas 불러오기 
import pandas as pd
print("pandas version: ", pd.__version__)
```

    pandas version:  1.1.3



```python
# 예제 1-1
# pandas 불러오기 
import pandas as pd

# k:v 구조를 갖는 딕셔너리를 만들고, 변수 dict_data에 저장
dict_data = {'a': 1, 'b': 2, 'c': 3}
# dict_data2 = {'a': 1.1, 'b': 2.2, 'c': 3.3}

# 판다스 Series() 함수로 딕셔너리(dict_data)를 시리즈로 변환. 변수 sr에 저장 
sr = pd.Series(dict_data)

# 변수 sr의 자료형 출력
print(type(sr))
print('\n')

# 변수 sr에 저장되어 있는 시리즈 객체를 출력
print(sr)
```

    <class 'pandas.core.series.Series'>


​    

    a    1
    b    2
    c    3
    dtype: int64



```python
# 인덱스 배열은 변수 idx에 저장. 데이터 값 배열은 변수 val에 저장
idx = sr.index
val = sr.values
print(idx)
print('\n')
print(val)
```

    Index(['a', 'b', 'c'], dtype='object')


​    

    [1 2 3]



```python
# 예제 1-2
# 리스트를 시리즈로 변환하여 변수 sr에 저장
list_data = ['2019-01-02', 3.14, 'ABC', 100, True]
sr = pd.Series(list_data)
print(sr)
print('\n')
```

    0    2019-01-02
    1          3.14
    2           ABC
    3           100
    4          True
    dtype: object


​    
​    


```python
# 인덱스 배열은 변수 idx에 저장. 데이터 값 배열은 변수 val에 저장
idx = sr.index
val = sr.values
print(idx)
print('\n')
print(val)
```

    RangeIndex(start=0, stop=5, step=1)


​    

    ['2019-01-02' 3.14 'ABC' 100 True]



```python
s1 = pd.Series([1,2,3])
s2 = pd.Series(['1','2','3'])
s3 = pd.Series([True, False, True])
s4 = pd.Series([1.0,2.0,3.0])
s5 = pd.Series([1.0,2.0,3.0001])
s6 = pd.Series([1.0,100, '가'])
s7 = pd.Series(range(10,20,2))

print(s1)
print(s2)
print(s3)
print(s4)
print(s5)
print(s6)
print(s7)
print(type(s1), type(s2),type(s3),type(s4),type(s5), type(s6))
print(type(s6[0]),type(s6[1]),type(s6[2]))
print(s6[2])
print(s1 + 100)
print(s1 * 10)
```

    0    1
    1    2
    2    3
    dtype: int64
    0    1
    1    2
    2    3
    dtype: object
    0     True
    1    False
    2     True
    dtype: bool
    0    1.0
    1    2.0
    2    3.0
    dtype: float64
    0    1.0000
    1    2.0000
    2    3.0001
    dtype: float64
    0      1
    1    100
    2      가
    dtype: object
    0    10
    1    12
    2    14
    3    16
    4    18
    dtype: int64
    <class 'pandas.core.series.Series'> <class 'pandas.core.series.Series'> <class 'pandas.core.series.Series'> <class 'pandas.core.series.Series'> <class 'pandas.core.series.Series'> <class 'pandas.core.series.Series'>
    <class 'float'> <class 'int'> <class 'str'>
    가
    0    101
    1    102
    2    103
    dtype: int64
    0    10
    1    20
    2    30
    dtype: int64



```python
# 예제 1-3
import pandas as pd

# 투플을 시리즈로 변환(index 옵션에 인덱스 이름을 지정)
tup_data = ('영인', '2010-05-01', '여', True)
sr = pd.Series(tup_data, index=['이름', '생년월일', '성별', '학생여부'])
print(sr)
print('\n')
print(sr.index[0])
print('\n')
print(sr.values[0])
```

    이름              영인
    생년월일    2010-05-01
    성별               여
    학생여부          True
    dtype: object


​    

    이름


​    

    영인



```python
# 원소를 1개 선택
print(sr[0])       # sr의 1 번째 원소를 선택 (정수형 위치 인덱스를 활용)
print(sr['이름'])  # '이름' 라벨을 가진 원소를 선택 (인덱스 이름을 활용)
print('\n')
```

    영인
    영인


​    
​    


```python
# 여러 개의 원소를 선택 (인덱스 리스트 활용)
print(sr[[1, 2]]) 
print('\n')           
print(sr[['생년월일', '성별']])
print('\n')
```

    생년월일    2010-05-01
    성별               여
    dtype: object


​    

    생년월일    2010-05-01
    성별               여
    dtype: object


​    
​    


```python
# 여러 개의 원소를 선택 (인덱스 범위 지정)
print(sr[1 : 2])  
print('\n')              
print(sr['생년월일' : '성별'])
```

    생년월일    2010-05-01
    dtype: object


​    

    생년월일    2010-05-01
    성별               여
    dtype: object



```python
# 예제 1-4
import pandas as pd

# 열이름을 key로 하고, 리스트를 value로 갖는 딕셔너리 정의(2차원 배열)
dict_data = {'c0':[1,2,3], 'c1':[4,5,6], 'c2':[7,8,9], 'c3':[10,11,12], 'c4':[13,14,15]}

# 판다스 DataFrame() 함수로 딕셔너리를 데이터프레임으로 변환. 변수 df에 저장. 
df = pd.DataFrame(dict_data)

# df의 자료형 출력
print(type(df)) 
print('\n')
# 변수 df에 저장되어 있는 데이터프레임 객체를 출력
print(df)
print(df.columns)
print(df.index)
print(df.values)
print(df.values[0,0])
print(df.values[2,4])
```

    <class 'pandas.core.frame.DataFrame'>


​    

       c0  c1  c2  c3  c4
    0   1   4   7  10  13
    1   2   5   8  11  14
    2   3   6   9  12  15
    Index(['c0', 'c1', 'c2', 'c3', 'c4'], dtype='object')
    RangeIndex(start=0, stop=3, step=1)
    [[ 1  4  7 10 13]
     [ 2  5  8 11 14]
     [ 3  6  9 12 15]]
    1
    15



```python
# 예제 1-5
import pandas as pd

# 행 인덱스/열 이름 지정하여, 데이터프레임 만들기
df = pd.DataFrame([[15, '남', '덕영중'], [17, '여', '수리중']], 
                   index=['준서', '예은'],
                   columns=['나이', '성별', '학교'])

# 행 인덱스, 열 이름 확인하기
print(df)            #데이터프레임
print('\n')
print(df.index)      #행 인덱스
print('\n')
print(df.columns)    #열 이름
print('\n')
```

        나이 성별   학교
    준서  15  남  덕영중
    예은  17  여  수리중


​    

    Index(['준서', '예은'], dtype='object')


​    

    Index(['나이', '성별', '학교'], dtype='object')


​    
​    


```python
# 행 인덱스, 열 이름 변경하기
df.index=['학생1', '학생2']
df.columns=['연령', '남녀', '소속']

print(df)            #데이터프레임
print('\n')
print(df.index)      #행 인덱스
print('\n')
print(df.columns)    #열 이름
```

         연령 남녀   소속
    학생1  15  남  덕영중
    학생2  17  여  수리중


​    

    Index(['학생1', '학생2'], dtype='object')


​    

    Index(['연령', '남녀', '소속'], dtype='object')



```python
# 예제 1-6
import pandas as pd

# 행 인덱스/열 이름 지정하여, 데이터프레임 만들기
df = pd.DataFrame([[15, '남', '덕영중'], [17, '여', '수리중']], 
                   index=['준서', '예은'],
                   columns=['나이', '성별', '학교'])

# 데이터프레임 df 출력
print(df)
print("\n")

# 열 이름 중, '나이'를 '연령'으로, '성별'을 '남녀'로, '학교'를 '소속'으로 바꾸기
a=df.rename(columns={'나이':'연령', '성별':'남녀', '학교':'소속'}, inplace=True)

# df의 행 인덱스 중에서, '준서'를 '학생1'로, '예은'을 '학생2'로 바꾸기
df.rename(index={'준서':'학생1', '예은':'학생2' }, inplace=True)

# df 출력(변경 후)
print(df)
print(a)
```

        나이 성별   학교
    준서  15  남  덕영중
    예은  17  여  수리중


​    

         연령 남녀   소속
    학생1  15  남  덕영중
    학생2  17  여  수리중
    None



```python
# 예제 1-7
import pandas as pd

# DataFrame() 함수로 데이터프레임 변환. 변수 df에 저장 
exam_data = {'수학' : [ 90, 80, 70], '영어' : [ 98, 89, 95],
             '음악' : [ 85, 95, 100], '체육' : [ 100, 90, 90]}

df = pd.DataFrame(exam_data, index=['서준', '우현', '인아'])
print(df)
print('\n')

# 데이터프레임 df를 복제하여 변수 df2에 저장. df2의 1개 행(row)을 삭제
df2 = df.copy()
df2.drop('우현', inplace=True)
print(df2)
print('\n')

# 데이터프레임 df를 복제하여 변수 df3에 저장. df3의 2개 행(row)을 삭제
df3 = df.copy()
df3.drop(['우현', '인아'], axis=0, inplace=True)
print(df3)
```

        수학  영어   음악   체육
    서준  90  98   85  100
    우현  80  89   95   90
    인아  70  95  100   90


​    

        수학  영어   음악   체육
    서준  90  98   85  100
    인아  70  95  100   90


​    

        수학  영어  음악   체육
    서준  90  98  85  100



```python
# 예제 1-8
import pandas as pd

# DataFrame() 함수로 데이터프레임 변환. 변수 df에 저장 
exam_data = {'수학' : [ 90, 80, 70], '영어' : [ 98, 89, 95],
             '음악' : [ 85, 95, 100], '체육' : [ 100, 90, 90]}

df = pd.DataFrame(exam_data, index=['서준', '우현', '인아'])
print(df)
print('\n')

# 데이터프레임 df를 복제하여 변수 df4에 저장. df4의 1개 열(column)을 삭제
df4 = df.copy()
df4.drop('수학', axis=1, inplace=True)
print(df4)
print('\n')

# 데이터프레임 df를 복제하여 변수 df5에 저장. df5의 2개 열(column)을 삭제
df5 = df.copy()
df5.drop(['영어', '음악'], axis=1, inplace=True)
print(df5)
```

        수학  영어   음악   체육
    서준  90  98   85  100
    우현  80  89   95   90
    인아  70  95  100   90


​    

        영어   음악   체육
    서준  98   85  100
    우현  89   95   90
    인아  95  100   90


​    

        수학   체육
    서준  90  100
    우현  80   90
    인아  70   90



```python
# 예제 1-9
import pandas as pd

# DataFrame() 함수로 데이터프레임 변환. 변수 df에 저장 
exam_data = {'수학' : [ 90, 80, 70], '영어' : [ 98, 89, 95],
             '음악' : [ 85, 95, 100], '체육' : [ 100, 90, 90]}

df = pd.DataFrame(exam_data, index=['서준', '우현', '인아'])
print(df)       # 데이터프레임 출력
print('\n')

# 행 인덱스를 사용하여 행 1개를 선택
label1 = df.loc['서준']    # loc 인덱서 활용
position1 = df.iloc[0]     # iloc 인덱서 활용
print(label1)
print('\n')
print(position1)
print('\n')
```

        수학  영어   음악   체육
    서준  90  98   85  100
    우현  80  89   95   90
    인아  70  95  100   90


​    

    수학     90
    영어     98
    음악     85
    체육    100
    Name: 서준, dtype: int64


​    

    수학     90
    영어     98
    음악     85
    체육    100
    Name: 서준, dtype: int64


​    
​    


```python
# 행 인덱스를 사용하여 2개 이상의 행 선택
label2 = df.loc[['서준', '우현']]
position2 = df.iloc[[0, 1]]
print(label2)
print('\n')
print(position2)
print('\n')
```

        수학  영어  음악   체육
    서준  90  98  85  100
    우현  80  89  95   90


​    

        수학  영어  음악   체육
    서준  90  98  85  100
    우현  80  89  95   90


​    
​    


```python
# 행 인덱스의 범위를 지정하여 행 선택
label3 = df.loc['서준':'인하']
position3 = df.iloc[0:1]
print(label3)
print('\n')
print(position3)
```

        수학  영어   음악   체육
    서준  90  98   85  100
    우현  80  89   95   90
    인아  70  95  100   90


​    

        수학  영어  음악   체육
    서준  90  98  85  100



```python
# 예제 1-10
import pandas as pd

# DataFrame() 함수로 데이터프레임 변환. 변수 df에 저장 
exam_data = {'이름' : [ '서준', '우현', '인아'],
             '수학' : [ 90, 80, 70],
             '영어' : [ 98, 89, 95],
             '음악' : [ 85, 95, 100],
             '체육' : [ 100, 90, 90]}
df = pd.DataFrame(exam_data)
print(df)
print(type(df))
print('\n')

# '수학' 점수 데이터만 선택. 변수 math1에 저장
math1 = df['수학']
print(math1)
print(type(math1))
print('\n')

# '영어' 점수 데이터만 선택. 변수 english에 저장
english = df.영어
print(english)
print(type(english))
print('\n')
```

       이름  수학  영어   음악   체육
    0  서준  90  98   85  100
    1  우현  80  89   95   90
    2  인아  70  95  100   90
    <class 'pandas.core.frame.DataFrame'>


​    

    0    90
    1    80
    2    70
    Name: 수학, dtype: int64
    <class 'pandas.core.series.Series'>


​    

    0    98
    1    89
    2    95
    Name: 영어, dtype: int64
    <class 'pandas.core.series.Series'>


​    
​    


```python
# '음악', '체육' 점수 데이터를 선택. 변수 music_gym 에 저장
music_gym = df[['음악', '체육']]
print(music_gym)
print(type(music_gym))
print('\n')

# '수학' 점수 데이터만 선택. 변수 math2에 저장
math2 = df[['수학']]
print(math2)
print(type(math2))
```

        음악   체육
    0   85  100
    1   95   90
    2  100   90
    <class 'pandas.core.frame.DataFrame'>


​    

       수학
    0  90
    1  80
    2  70
    <class 'pandas.core.frame.DataFrame'>



```python
print(df.iloc[::2])
```

       이름  수학  영어   음악   체육
    0  서준  90  98   85  100
    2  인아  70  95  100   90



```python
print(df.iloc[:3:2])
```

       이름  수학  영어   음악   체육
    0  서준  90  98   85  100
    2  인아  70  95  100   90



```python
print(df.iloc[::-1])
```

       이름  수학  영어   음악   체육
    2  인아  70  95  100   90
    1  우현  80  89   95   90
    0  서준  90  98   85  100



```python
# 예제 1-11
import pandas as pd

# DataFrame() 함수로 데이터프레임 변환. 변수 df에 저장 
exam_data = {'이름' : [ '서준', '우현', '인아'],
             '수학' : [ 90, 80, 70],
             '영어' : [ 98, 89, 95],
             '음악' : [ 85, 95, 100],
             '체육' : [ 100, 90, 90]}
df = pd.DataFrame(exam_data)

# '이름' 열을 새로운 인덱스로 지정하고, df 객체에 변경사항 반영
df.set_index('이름', inplace=True)
print(df)
print('\n')
print(df.loc[::-1])
```

        수학  영어   음악   체육
    이름                  
    서준  90  98   85  100
    우현  80  89   95   90
    인아  70  95  100   90


​    

        수학  영어   음악   체육
    이름                  
    인아  70  95  100   90
    우현  80  89   95   90
    서준  90  98   85  100



```python
# 데이터프레임 df의 특정 원소 1개 선택 ('서준'의 '음악' 점수)
a = df.loc['서준', '음악']
print(a)
b = df.iloc[0, 2]
print(b)
print('\n')
```

    85
    85


​    
​    


```python
# 데이터프레임 df의 특정 원소 2개 이상 선택 ('서준'의 '음악', '체육' 점수) 
c = df.loc['서준', ['음악', '체육']]
print(c)
d = df.iloc[0, [2, 3]]
print(d)
e = df.loc['서준', '음악':'체육']
print(e)
f = df.iloc[0, 2:]
print(f)
print('\n')
```

    음악     85
    체육    100
    Name: 서준, dtype: int64
    음악     85
    체육    100
    Name: 서준, dtype: int64
    음악     85
    체육    100
    Name: 서준, dtype: int64
    음악     85
    체육    100
    Name: 서준, dtype: int64


​    
​    


```python
# df의 2개 이상의 행과 열로부터 원소 선택 ('서준', '우현'의 '음악', '체육' 점수) 
g = df.loc[['서준', '우현'], ['음악', '체육']]
print(g)
h = df.iloc[[0, 1], [2, 3]]
print(h)
i = df.loc['서준':'우현', '음악':'체육']
print(i)
j = df.iloc[0:2, 2:]
print(j)
```

        음악   체육
    이름         
    서준  85  100
    우현  95   90
        음악   체육
    이름         
    서준  85  100
    우현  95   90
        음악   체육
    이름         
    서준  85  100
    우현  95   90
        음악   체육
    이름         
    서준  85  100
    우현  95   90



```python
# 예제 1-12
import pandas as pd

# DataFrame() 함수로 데이터프레임 변환. 변수 df에 저장 
exam_data = {'이름' : [ '서준', '우현', '인아'],
             '수학' : [ 90, 80, 70],
             '영어' : [ 98, 89, 95],
             '음악' : [ 85, 95, 100],
             '체육' : [ 100, 90, 90]}
df = pd.DataFrame(exam_data)
print(df)
print('\n')

# 데이터프레임 df에 '국어' 점수 열(column)을 추가. 데이터 값은 80 지정
df['국어'] = 80
print(df)
print(df.국어)
df.국어 = 100
print(df)
df.국어 = [100, 90, 80]
print(df)
df['사회'] = 70 # 처음 추가하는 열이름인 경우에는 . 사용 못함
print(df)
```

       이름  수학  영어   음악   체육
    0  서준  90  98   85  100
    1  우현  80  89   95   90
    2  인아  70  95  100   90


​    

       이름  수학  영어   음악   체육  국어
    0  서준  90  98   85  100  80
    1  우현  80  89   95   90  80
    2  인아  70  95  100   90  80
    0    80
    1    80
    2    80
    Name: 국어, dtype: int64
       이름  수학  영어   음악   체육   국어
    0  서준  90  98   85  100  100
    1  우현  80  89   95   90  100
    2  인아  70  95  100   90  100
       이름  수학  영어   음악   체육   국어
    0  서준  90  98   85  100  100
    1  우현  80  89   95   90   90
    2  인아  70  95  100   90   80
       이름  수학  영어   음악   체육   국어  사회
    0  서준  90  98   85  100  100  70
    1  우현  80  89   95   90   90  70
    2  인아  70  95  100   90   80  70



```python
# 예제 1-13
import pandas as pd

# DataFrame() 함수로 데이터프레임 변환. 변수 df에 저장 
exam_data = {'이름' : ['서준', '우현', '인아'],
             '수학' : [ 90, 80, 70],
             '영어' : [ 98, 89, 95],
             '음악' : [ 85, 95, 100],
             '체육' : [ 100, 90, 90]}
df = pd.DataFrame(exam_data)
print(df)
print('\n')

# 새로운 행(row)을 추가 - 같은 원소 값을 입력
df.loc[3] = 0
print(df)
print('\n')

# 새로운 행(row)을 추가 - 원소 값 여러 개의 배열 입력
df.loc[4] = ['동규', 90, 80, 70, 60]
print(df)
print('\n')

# 새로운 행(row)을 추가 - 기존 행을 복사
df.loc['행5'] = df.loc[3]
print(df)

```

       이름  수학  영어   음악   체육
    0  서준  90  98   85  100
    1  우현  80  89   95   90
    2  인아  70  95  100   90


​    

       이름  수학  영어   음악   체육
    0  서준  90  98   85  100
    1  우현  80  89   95   90
    2  인아  70  95  100   90
    3   0   0   0    0    0


​    

       이름  수학  영어   음악   체육
    0  서준  90  98   85  100
    1  우현  80  89   95   90
    2  인아  70  95  100   90
    3   0   0   0    0    0
    4  동규  90  80   70   60


​    

        이름  수학  영어   음악   체육
    0   서준  90  98   85  100
    1   우현  80  89   95   90
    2   인아  70  95  100   90
    3    0   0   0    0    0
    4   동규  90  80   70   60
    행5   0   0   0    0    0



```python
# 예제 1-14
import pandas as pd

# DataFrame() 함수로 데이터프레임 변환. 변수 df에 저장 
exam_data = {'이름' : [ '서준', '우현', '인아'],
             '수학' : [ 90, 80, 70],
             '영어' : [ 98, 89, 95],
             '음악' : [ 85, 95, 100],
             '체육' : [ 100, 90, 90]}
df = pd.DataFrame(exam_data)

# '이름' 열을 새로운 인덱스로 지정하고, df 객체에 변경사항 반영
df.set_index('이름', inplace=True)
print(df)
print('\n')

# 데이터프레임 df의 특정 원소를 변경하는 방법: '서준'의 '체육' 점수
df.iloc[0][3] = 80
print(df)
print('\n')

df.loc['서준']['체육'] = 90
print(df)
print('\n')

df.loc['서준', '체육'] = 100
print(df)
print('\n')
```

        수학  영어   음악   체육
    이름                  
    서준  90  98   85  100
    우현  80  89   95   90
    인아  70  95  100   90


​    

        수학  영어   음악  체육
    이름                 
    서준  90  98   85  80
    우현  80  89   95  90
    인아  70  95  100  90


​    

        수학  영어   음악  체육
    이름                 
    서준  90  98   85  90
    우현  80  89   95  90
    인아  70  95  100  90


​    

        수학  영어   음악   체육
    이름                  
    서준  90  98   85  100
    우현  80  89   95   90
    인아  70  95  100   90


​    
​    


```python
# 데이터프레임 df의 원소 여러 개를 변경하는 방법: '서준'의 '음악', '체육' 점수
df.loc['서준', ['음악', '체육']] = 50
print(df)
print('\n')

df.loc['서준', ['음악', '체육']] = 100, 50
print(df)
```


```python
# 예제 1-15
import pandas as pd

# DataFrame() 함수로 데이터프레임 변환. 변수 df에 저장 
exam_data = {'이름' : [ '서준', '우현', '인아'],
             '수학' : [ 90, 80, 70],
             '영어' : [ 98, 89, 95],
             '음악' : [ 85, 95, 100],
             '체육' : [ 100, 90, 90]}
df = pd.DataFrame(exam_data)
print(df)
print('\n')

# 데이터프레임 df를 전치하기 (메소드 활용)
df = df.transpose()
print(df)
print('\n')

# 데이터프레임 df를 다시 전치하기 (클래스 속성 활용)
df = df.T
print(df)
```


```python
import pandas as pd

# DataFrame() 함수로 데이터프레임 변환. 변수 df에 저장 
exam_data = {'name' : [ 'dooly', 'ddoch', 'dounar'],
             'math' : [ 90, 80, 70],
             'eng' : [ 98, 89, 95],
             'music' : [ 85, 95, 100],
             'exer' : [ 100, 90, 90]}
df = pd.DataFrame(exam_data)
df.set_index('name', inplace=True)
print(df)
df.plot()
print('\n')

# 데이터프레임 df를 전치하기 (메소드 활용)
df = df.transpose()
print(df)
df.plot()
print('\n')

# 데이터프레임 df를 다시 전치하기 (클래스 속성 활용)
df = df.T
print(df)
```

            math  eng  music  exer
    name                          
    dooly     90   98     85   100
    ddoch     80   89     95    90
    dounar    70   95    100    90


​    

    name   dooly  ddoch  dounar
    math      90     80      70
    eng       98     89      95
    music     85     95     100
    exer     100     90      90


​    

            math  eng  music  exer
    name                          
    dooly     90   98     85   100
    ddoch     80   89     95    90
    dounar    70   95    100    90



![png](C:/Users/Daniel/AppData/Local/Temp/Temp1_exam4.zip/output_33_1.png)



![png](C:/Users/Daniel/AppData/Local/Temp/Temp1_exam4.zip/output_33_2.png)



```python
# 예제 1-16
import pandas as pd

# DataFrame() 함수로 데이터프레임 변환. 변수 df에 저장 
exam_data = {'이름' : [ '서준', '우현', '인아'],
             '수학' : [ 90, 80, 70],
             '영어' : [ 98, 89, 95],
             '음악' : [ 85, 95, 100],
             '체육' : [ 100, 90, 90]}
df = pd.DataFrame(exam_data)
print(df)
print('\n')

# 특정 열(column)을 데이터프레임의 행 인덱스(index)로 설정 
ndf = df.set_index(['이름'])
print(ndf)
print('\n')
ndf2 = ndf.set_index('음악')
print(ndf2)
print('\n')
ndf3 = ndf.set_index(['수학', '음악'])
print(ndf3)
```


```python
# 예제 1-17
import pandas as pd

# 딕셔서리를 정의
dict_data = {'c0':[1,2,3], 'c1':[4,5,6], 'c2':[7,8,9], 'c3':[10,11,12], 'c4':[13,14,15]}

# 딕셔서리를 데이터프레임으로 변환. 인덱스를 [r0, r1, r2]로 지정
df = pd.DataFrame(dict_data, index=['r0', 'r1', 'r2'])
print(df)
print('\n')

# 인덱스를 [r0, r1, r2, r3, r4]로 재지정
new_index = ['r0', 'r1', 'r2', 'r3', 'r4']
ndf = df.reindex(new_index)
print(ndf)
print('\n')

# reindex로 발생한 NaN값을 숫자 0으로 채우기
new_index = ['r0', 'r1', 'r2', 'r3', 'r4']
ndf2 = df.reindex(new_index, fill_value=0)
print(ndf2)
```

        c0  c1  c2  c3  c4
    r0   1   4   7  10  13
    r1   2   5   8  11  14
    r2   3   6   9  12  15


​    

         c0   c1   c2    c3    c4
    r0  1.0  4.0  7.0  10.0  13.0
    r1  2.0  5.0  8.0  11.0  14.0
    r2  3.0  6.0  9.0  12.0  15.0
    r3  NaN  NaN  NaN   NaN   NaN
    r4  NaN  NaN  NaN   NaN   NaN


​    

        c0  c1  c2  c3  c4
    r0   1   4   7  10  13
    r1   2   5   8  11  14
    r2   3   6   9  12  15
    r3   0   0   0   0   0
    r4   0   0   0   0   0



```python
# 예제 1-18
import pandas as pd

# 딕셔서리를 정의
dict_data = {'c0':[1,2,3], 'c1':[4,5,6], 'c2':[7,8,9], 'c3':[10,11,12], 'c4':[13,14,15]}

# 딕셔서리를 데이터프레임으로 변환. 인덱스를 [r0, r1, r2]로 지정
df = pd.DataFrame(dict_data, index=['r0', 'r1', 'r2'])
print(df)
print('\n')

# 행 인덱스를 정수형으로 초기화 
ndf = df.reset_index()
print(ndf)
```


```python
# 예제 1-19
import pandas as pd

# 딕셔서리를 정의
dict_data = {'c0':[1,2,3], 'c1':[4,5,6], 'c2':[7,8,9], 'c3':[10,11,12], 'c4':[13,14,15]}

# 딕셔서리를 데이터프레임으로 변환. 인덱스를 [r0, r1, r2]로 지정
df = pd.DataFrame(dict_data, index=['r0', 'r1', 'r2'])
print(df)
print('\n')

# 내림차순으로 행 인덱스 정렬 
ndf = df.sort_index(ascending=False)
print(ndf)
```


```python
# 예제 1-20
import pandas as pd

# 딕셔서리를 정의
dict_data = {'c0':[1,2,3], 'c1':[4,5,6], 'c2':[7,8,9], 'c3':[10,11,12], 'c4':[13,14,15]}

# 딕셔서리를 데이터프레임으로 변환. 인덱스를 [r0, r1, r2]로 지정
df = pd.DataFrame(dict_data, index=['r0', 'r1', 'r2'])
print(df)
print('\n')

# c1 열을 기준으로 내림차순 정렬 
ndf = df.sort_values(by='c1', ascending=False)
print(ndf)
```


```python
# 예제 1-21
# 라이브러리 불러오기 
import pandas as pd

# 딕셔너리 데이터로 판다스 시리즈 만들기
student1 = pd.Series({'국어':100, '영어':80, '수학':90})
print(student1)
print('\n')

# 학생의 과목별 점수를 200으로 나누기
percentage = student1 / 200

print(percentage)
print('\n')
print(type(percentage))
```


```python
# 예제 1-22
# 라이브러리 불러오기 
import pandas as pd

# 딕셔너리 데이터로 판다스 시리즈 만들기
student1 = pd.Series({'국어':100, '영어':80, '수학':90})
student2 = pd.Series({'수학':80, '국어':90, '영어':80})

print(student1)
print('\n')
print(student2)
print('\n')

# 두 학생의 과목별 점수로 사칙연산 수행
addition = student1 + student2               #덧셈
subtraction = student1 - student2            #뺄셈
multiplication = student1 * student2         #곱셈
division = student1 / student2               #나눗셈
print(division)
print(type(division))
print('\n')

result = pd.DataFrame([addition, subtraction, multiplication], 
                      index=['덧셈', '뺄셈', '곱셈'])
print(result)

# 사칙연산 결과를 데이터프레임으로 합치기 (시리즈 -> 데이터프레임)
result = pd.DataFrame([addition, subtraction, multiplication, division], 
                      index=['덧셈', '뺄셈', '곱셈', '나눗셈'])
print(result)
```


```python
# 예제 1-23
# 라이브러리 불러오기 
import pandas as pd
import numpy as np

# 딕셔너리 데이터로 판다스 시리즈 만들기
student1 = pd.Series({'국어':np.nan, '영어':80, '수학':90})
student2 = pd.Series({'수학':80, '국어':90})

print(student1)
print('\n')
print(student2)
print('\n')

# 두 학생의 과목별 점수로 사칙연산 수행 (시리즈 vs. 시리즈)
addition = student1 + student2               #덧셈
subtraction = student1 - student2            #뺄셈
multiplication = student1 * student2         #곱셈
division = student1 / student2               #나눗셈
print(type(division))
print(division)
print('\n')

# 사칙연산 결과를 데이터프레임으로 합치기 (시리즈 -> 데이터프레임)
result = pd.DataFrame([addition, subtraction, multiplication, division], 
                      index=['덧셈', '뺄셈', '곱셈', '나눗셈'])
print(result)
```

    국어     NaN
    영어    80.0
    수학    90.0
    dtype: float64


​    

    수학    80
    국어    90
    dtype: int64


​    

    <class 'pandas.core.series.Series'>
    국어      NaN
    수학    1.125
    영어      NaN
    dtype: float64


​    

         국어        수학  영어
    덧셈  NaN   170.000 NaN
    뺄셈  NaN    10.000 NaN
    곱셈  NaN  7200.000 NaN
    나눗셈 NaN     1.125 NaN



```python
# 예제 1-24
# 라이브러리 불러오기 
import pandas as pd
import numpy as np

# 딕셔너리 데이터로 판다스 시리즈 만들기
student1 = pd.Series({'국어':np.nan, '영어':80, '수학':90})
student2 = pd.Series({'수학':80, '국어':90})

print(student1)
print('\n')
print(student2)
print('\n')

# 두 학생의 과목별 점수로 사칙연산 수행 (연산 메소드 사용)
sr_add = student1.add(student2, fill_value=0)    #덧셈
sr_sub = student1.sub(student2, fill_value=0)    #뺄셈
sr_mul = student1.mul(student2, fill_value=0)    #곱셈
sr_div = student1.div(student2, fill_value=0)    #나눗셈

# 사칙연산 결과를 데이터프레임으로 합치기 (시리즈 -> 데이터프레임)
result = pd.DataFrame([sr_add, sr_sub, sr_mul, sr_div], 
                      index=['덧셈', '뺄셈', '곱셈', '나눗셈'])
print(result)

```

    국어     NaN
    영어    80.0
    수학    90.0
    dtype: float64


​    

    수학    80
    국어    90
    dtype: int64


​    

           국어        수학    영어
    덧셈   90.0   170.000  80.0
    뺄셈  -90.0    10.000  80.0
    곱셈    0.0  7200.000   0.0
    나눗셈   0.0     1.125   inf



```python
# 예제 1-25
# 라이브러리 불러오기
import pandas as pd
import seaborn as sns

# titanic 데이터셋에서 age, fare 2개 열을 선택하여 데이터프레임 만들기
titanic = sns.load_dataset('titanic')
df = titanic.loc[:, ['age','fare']]
print(df.head())   #첫 5행만 표시
print('\n')
print(type(df))
print('\n')

# 데이터프레임에 숫자 10 더하기
addition = df + 10
print(addition.head())   #첫 5행만 표시
print('\n')
print(type(addition))
```

        age     fare
    0  22.0   7.2500
    1  38.0  71.2833
    2  26.0   7.9250
    3  35.0  53.1000
    4  35.0   8.0500


​    

    <class 'pandas.core.frame.DataFrame'>


​    

        age     fare
    0  32.0  17.2500
    1  48.0  81.2833
    2  36.0  17.9250
    3  45.0  63.1000
    4  45.0  18.0500


​    

    <class 'pandas.core.frame.DataFrame'>



```python
# 예제 1-26
# 라이브러리 불러오기
import pandas as pd
import seaborn as sns

# titanic 데이터셋에서 age, fare 2개 열을 선택하여 데이터프레임 만들기
titanic = sns.load_dataset('titanic')
df = titanic.loc[:, ['age','fare']]
print(df.tail())          #마지막 5행을 표시
print('\n')
print(type(df))
print('\n')

# 데이터프레임에 숫자 10 더하기
addition = df + 10
print(addition.tail())    #마지막 5행을 표시
print('\n')
print(type(addition))
print('\n')

# 데이터프레임끼리 연산하기 (additon - df)
subtraction = addition - df
print(subtraction.tail())   #마지막 5행을 표시
print('\n')
print(type(subtraction))
```

          age   fare
    886  27.0  13.00
    887  19.0  30.00
    888   NaN  23.45
    889  26.0  30.00
    890  32.0   7.75


​    

    <class 'pandas.core.frame.DataFrame'>


​    

          age   fare
    886  37.0  23.00
    887  29.0  40.00
    888   NaN  33.45
    889  36.0  40.00
    890  42.0  17.75


​    

    <class 'pandas.core.frame.DataFrame'>


​    

          age  fare
    886  10.0  10.0
    887  10.0  10.0
    888   NaN  10.0
    889  10.0  10.0
    890  10.0  10.0


​    

    <class 'pandas.core.frame.DataFrame'>



```python
len?
```


    [1;31mSignature:[0m [0mlen[0m[1;33m([0m[0mobj[0m[1;33m,[0m [1;33m/[0m[1;33m)[0m[1;33m[0m[1;33m[0m[0m
    [1;31mDocstring:[0m Return the number of items in a container.
    [1;31mType:[0m      builtin_function_or_method




```python
help(len)
```

    Help on built-in function len in module builtins:
    
    len(obj, /)
        Return the number of items in a container.

​    

### - 실습


```python
from selenium import webdriver
import time
import re

driver = webdriver.Chrome('C:/Temp/chromedriver')
driver.get("http://gs25.gsretail.com/gscvs/ko/products/event-goods")
time.sleep(2)

# 2+1행사 탭으로 이동
twoPlusOnetab = driver.find_element_by_css_selector('#TWO_TO_ONE')
twoPlusOnetab.click()
time.sleep(1)

titleList_all = []
priceList_all = []
page = 0

while True :
    page += 1
    
    titleList = driver.find_elements_by_css_selector('div.cnt_section.mt50 div > p.tit')
    priceList = driver.find_elements_by_css_selector('div.cnt_section.mt50 div > p.price > span')

    productCount = 0
    for oneTitle in titleList :
        if len(oneTitle.text.strip()) > 0 :
            titleList_all.append(oneTitle.text.strip())
            productCount += 1
            # print(oneTitle.text.strip())
    print(str(page) + " page 상품명 누적 " + str(len(titleList_all)) + "개 적재")

    for onePrice in priceList :
        if len(onePrice.text.strip()) > 0 :
            content = re.sub('[^0-9]', '', onePrice.text.strip())
            priceList_all.append(content)
            # print(content)
    print(str(page) + " page 가격 누적 " + str(len(priceList_all)) + "개 적재")

    # 마지막 페이지이면 정지
    if productCount < 8 : break  
    
    # 다음페이지로 이동 - 잘 안되서 스크립트로
    driver.execute_script("goodsPageController.moveControl(1)")
    time.sleep(1)

with open('C:/Temp/gs25_twotoone.csv', "wt", encoding="utf-8") as f:
    f.write('goodsname,goodsprice \n')  
    for i in range(len(titleList_all)):
        f.write(titleList_all[i] + ","+ priceList_all[i] + '\n') 
```