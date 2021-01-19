

# 분석Day05

>  pandas

### - 교육내용

```python
# 예제 2-1
# 라이브러리 불러오기
import pandas as pd

# 파일경로를 찾고, 변수 file_path에 저장
file_path = './data/read_csv_sample.csv'

# read_csv() 함수로 데이터프레임 변환. 변수 df1에 저장
df1 = pd.read_csv(file_path)
print(df1)
display(df1)
print('\n')

# read_csv() 함수로 데이터프레임 변환. 변수 df2에 저장. header=None 옵션
df2 = pd.read_csv(file_path, header=None)
print(df2)
display(df2)
print('\n')

# read_csv() 함수로 데이터프레임 변환. 변수 df3에 저장. index_col=None 옵션
df3 = pd.read_csv(file_path, index_col=None)
print(df3)
display(df3)
print('\n')

# read_csv() 함수로 데이터프레임 변환. 변수 df4에 저장. index_col='c0' 옵션
df4 = pd.read_csv(file_path, index_col='c0')
print(df4)
display(df4)
```

       c0  c1  c2  c3
    0   0   1   4   7
    1   1   2   5   8
    2   2   3   6   9



```python
# 예제 2-2
import pandas as pd

# read_excel() 함수로 데이터프레임 변환 
df1 = pd.read_excel('./data/남북한발전전력량.xlsx')            # header=0 (default 옵션)
df2 = pd.read_excel('./data/남북한발전전력량.xlsx', header=None)  # header=None 옵션

# 데이터프레임 출력
print(df1)
display(df1)
print(df2)
display(df2)
pd.get_option('display.max_columns')
```



```python
pd.set_option('display.max_columns', 100)

import pandas as pd

# read_excel() 함수로 데이터프레임 변환 
df1 = pd.read_excel('./data/남북한발전전력량.xlsx')            # header=0 (default 옵션)
df2 = pd.read_excel('./data/남북한발전전력량.xlsx', header=None)  # header=None 옵션

# 데이터프레임 출력
display(df1)
display(df2)
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }
```python
pd.reset_option("^display")
```




```python
# 예제 2-3
import pandas as pd

# read_json() 함수로 데이터프레임 변환 
df = pd.read_json('./data/read_json_sample.json')  
print(df)
print('\n')
print(df.index)
```

               name  year        developer opensource
    pandas           2008    Wes Mckinneye       True
    NumPy            2006  Travis Oliphant       True
    matplotlib       2003   John D. Hunter       True


​    

    Index(['pandas', 'NumPy', 'matplotlib'], dtype='object')



```python
# 예제 2-4
import pandas as pd

# HTML 파일 경로 or 웹 페이지 주소를 url 변수에 저장
url ='./data/sample.html'

# HTML 웹페이지의 표(table)를 가져와서 데이터프레임으로 변환 
tables = pd.read_html(url)

# 표(table)의 개수 확인
print(len(tables))
print('\n')

# tables 리스트의 원소를 iteration하면서 각각 화면 출력
for i in range(len(tables)):
    print("tables[%s]" % i)
    print(tables[i])
    print('\n')

# 파이썬 패키지 정보가 들어 있는 두 번째 데이터프레임을 선택하여 df 변수에 저장
df = tables[1] 

# 'name' 열을 인덱스로 지정
df.set_index(['name'], inplace=True)
print(df)
```

    2


​    

    tables[0]
       Unnamed: 0  c0  c1  c2  c3
    0           0   0   1   4   7
    1           1   1   2   5   8
    2           2   2   3   6   9


​    

    tables[1]
             name  year        developer  opensource
    0       NumPy  2006  Travis Oliphant        True
    1  matplotlib  2003   John D. Hunter        True
    2      pandas  2008    Wes Mckinneye        True


​    

                year        developer  opensource
    name                                         
    NumPy       2006  Travis Oliphant        True
    matplotlib  2003   John D. Hunter        True
    pandas      2008    Wes Mckinneye        True



```python
## google 지오코딩 API 통해 위도, 경도 데이터 가져오기 
# 예제 2-6
# 라이브러리 가져오기
import googlemaps
import pandas as pd

my_key = "AIzaSyDy81EbO46BRSnX1DOgg_F84bhsdbku2z4"

# 구글맵스 객체 생성하기
maps = googlemaps.Client(key=my_key)  # my key값 입력

lat = []  #위도
lng = []  #경도

# 장소(또는 주소) 리스트
places = ["서울시청", "국립국악원", "해운대해수욕장"]

i=0
for place in places:   
    i = i + 1
    try:
        print(i, place)
        # 지오코딩 API 결과값 호출하여 geo_location 변수에 저장
        geo_location = maps.geocode(place)[0].get('geometry')
        lat.append(geo_location['location']['lat'])
        lng.append(geo_location['location']['lng'])
        

    except:
        lat.append('')
        lng.append('')
        print(i)

# 데이터프레임으로 변환하기
df = pd.DataFrame({'위도':lat, '경도':lng}, index=places)
print('\n')
print(df)
```

    1 서울시청
    2 국립국악원
    3 해운대해수욕장


​    

                    위도          경도
    서울시청     37.566295  126.977945
    국립국악원    37.477759  127.008304
    해운대해수욕장  35.158698  129.160384



```python
# 예제 2-7
import pandas as pd

# 판다스 DataFrame() 함수로 데이터프레임 변환. 변수 df에 저장 
data = {'name' : [ 'Jerry', 'Riah', 'Paul'],
        'algol' : [ "A", "A+", "B"],
        'basic' : [ "C", "B", "B+"],
        'c++' : [ "B+", "C", "C+"],
        }

df = pd.DataFrame(data)
df.set_index('name', inplace=True)   #name 열을 인덱스로 지정
print(df)

# to_csv() 메소드를 사용하여 CSV 파일로 내보내기. 파열명은 df_sample.csv로 저장
df.to_csv("./output/df_sample.csv")
```

          algol basic c++
    name                 
    Jerry     A     C  B+
    Riah     A+     B   C
    Paul      B    B+  C+



```python
# 예제 2-8
import pandas as pd

# 판다스 DataFrame() 함수로 데이터프레임 변환. 변수 df에 저장 
data = {'name' : [ 'Jerry', 'Riah', 'Paul'],
        'algol' : [ "A", "A+", "B"],
        'basic' : [ "C", "B", "B+"],
        'c++' : [ "B+", "C", "C+"],
        }

df = pd.DataFrame(data)
df.set_index('name', inplace=True)   #name 열을 인덱스로 지정
print(df)

# to_json() 메소드를 사용하여 JSON 파일로 내보내기. 파열명은 df_sample.json로 저장
df.to_json("./output/df_sample.json")
```

          algol basic c++
    name                 
    Jerry     A     C  B+
    Riah     A+     B   C
    Paul      B    B+  C+



```python
# 예제 2-9
import pandas as pd

# 판다스 DataFrame() 함수로 데이터프레임 변환. 변수 df에 저장 
data = {'name' : [ 'Jerry', 'Riah', 'Paul'],
        'algol' : [ "A", "A+", "B"],
        'basic' : [ "C", "B", "B+"],
        'c++' : [ "B+", "C", "C+"],
        }

df = pd.DataFrame(data)
df.set_index('name', inplace=True)   #name 열을 인덱스로 지정
print(df)

# to_excel() 메소드를 사용하여 엑셀 파일로 내보내기. 파열명은 df_sample.xlsx로 저장
df.to_excel("./output/df_sample.xlsx")
```

          algol basic c++
    name                 
    Jerry     A     C  B+
    Riah     A+     B   C
    Paul      B    B+  C+



```python
# 예제 2-10
import pandas as pd

# 판다스 DataFrame() 함수로 데이터프레임 변환. 변수 df1, df2에 저장 
data1 = {'name' : [ 'Jerry', 'Riah', 'Paul'],
         'algol' : [ "A", "A+", "B"],
         'basic' : [ "C", "B", "B+"],
          'c++' : [ "B+", "C", "C+"]}

data2 = {'c0':[1,2,3], 
         'c1':[4,5,6], 
         'c2':[7,8,9], 
         'c3':[10,11,12], 
         'c4':[13,14,15]}

df1 = pd.DataFrame(data1)
df1.set_index('name', inplace=True)      #name 열을 인덱스로 지정
print(df1)
print('\n')

df2 = pd.DataFrame(data2)
df2.set_index('c0', inplace=True)        #c0 열을 인덱스로 지정
print(df2)

# df1을 'sheet1'으로, df2를 'sheet2'로 저장 (엑셀파일명은 "df_excelwriter.xlsx")
writer = pd.ExcelWriter("./output/df_excelwriter.xlsx")
df1.to_excel(writer, sheet_name="sheet1")
df2.to_excel(writer, sheet_name="sheet2")
writer.save()
```

          algol basic c++
    name                 
    Jerry     A     C  B+
    Riah     A+     B   C
    Paul      B    B+  C+


​    

        c1  c2  c3  c4
    c0                
    1    4   7  10  13
    2    5   8  11  14
    3    6   9  12  15



### - 실습

```python
# 함수버전
import urllib.request
import json
from bs4 import BeautifulSoup

def naver_search (keyword, callType = 'JSON') :
    client_key = 'izGsqP2exeThwwEUVU3x'
    client_secret = 'WrwbQ1l6ZI'
    query = keyword
    encText = urllib.parse.quote_plus(query)

    num = 5
    if callType == 'JSON' :
        urlhead = 'https://openapi.naver.com/v1/search/local.json?query='
    elif callType == 'XML' :
        urlhead = 'https://openapi.naver.com/v1/search/local.xml?query='
    else :
        print('JSON or XML only')
        return
    
    naver_url = urlhead + encText + '&display=' + str(num)

    request = urllib.request.Request(naver_url)
    request.add_header("X-Naver-Client-Id",client_key)
    request.add_header("X-Naver-Client-Secret",client_secret)
    response = urllib.request.urlopen(request)
    rescode = response.getcode()

    if(rescode == 200):
        response_body = response.read()
        count = 1        
        if callType == 'JSON' :
            dataList = json.loads(response_body)
            print(type(dataList))
            print('[' + query + '에 대한 네이버 지역 정보(JSON)]')
            for data in dataList['items'] :
                print (str(count) + ' : ' + data['title'] + ',' + data['telephone'] + ',' + data['address'])
                count += 1
        elif callType == 'XML' :
            xmlsoup = BeautifulSoup(response_body, 'xml')
            items = xmlsoup.find_all('item')
            print(type(items))
            print('[' + query + '에 대한 네이버 지역 정보(XML)]')
            for data in items:
                print (str(count) + ' : ' + data.title.string + ',' + ('없음' if data.telephone.string == None else data.telephone.string) + ',' + data.address.string)
                count += 1
    else:
        print('오류 코드 : ' + rescode)

naver_search('쌀국수', 'XML')
print('***')
naver_search('쌀국수', 'JSON')
```

```python
import pandas as pd

# 문제 1
data = {
    'name':['둘리', '또치', '도우너', '희동이'],
    'kor':[90, 80, 70, 70],
    'eng':[99, 98, 97, 46],
    'mat':[90, 70, 70, 60],
}
df = pd.DataFrame(data)
print(df)

df['class'] = [str(x) + '반' for x in range(1, 3)] * 2
print(df)
```

      name  kor  eng  mat
    0   둘리   90   99   90
    1   또치   80   98   70
    2  도우너   70   97   70
    3  희동이   70   46   60
      name  kor  eng  mat class
    0   둘리   90   99   90    1반
    1   또치   80   98   70    2반
    2  도우너   70   97   70    1반
    3  희동이   70   46   60    2반



```python
# 문제 2
print(df)

df.loc[4] = ['마이콜', 80, 80, 80, '1반']
print(df)
```

      name  kor  eng  mat class
    0   둘리   90   99   90    1반
    1   또치   80   98   70    2반
    2  도우너   70   97   70    1반
    3  희동이   70   46   60    2반
      name  kor  eng  mat class
    0   둘리   90   99   90    1반
    1   또치   80   98   70    2반
    2  도우너   70   97   70    1반
    3  희동이   70   46   60    2반
    4  마이콜   80   80   80    1반



```python
# 문제 3
print(df)

df.set_index('name', inplace=True)
df.columns=['국어', '영어', '수학', '반번호']
print(df)
```

      name  kor  eng  mat class
    0   둘리   90   99   90    1반
    1   또치   80   98   70    2반
    2  도우너   70   97   70    1반
    3  희동이   70   46   60    2반
    4  마이콜   80   80   80    1반
          국어  영어  수학 반번호
    name                
    둘리    90  99  90  1반
    또치    80  98  70  2반
    도우너   70  97  70  1반
    희동이   70  46  60  2반
    마이콜   80  80  80  1반



```python
# 문제 4
print(df)

df.loc['마이콜', '국어':'수학'] = 100
df.loc['희동이', '영어'] = 90
print(df)
```

          국어  영어  수학 반번호
    name                
    둘리    90  99  90  1반
    또치    80  98  70  2반
    도우너   70  97  70  1반
    희동이   70  46  60  2반
    마이콜   80  80  80  1반
           국어   영어   수학 반번호
    name                   
    둘리     90   99   90  1반
    또치     80   98   70  2반
    도우너    70   97   70  1반
    희동이    70   90   60  2반
    마이콜   100  100  100  1반



```python
# 문제 5
print(df)
df.reset_index(inplace=True)
print(df)
df.rename(columns={'name':'성명'}, inplace=True)
print(df)
```

           국어   영어   수학 반번호
    name                   
    둘리     90   99   90  1반
    또치     80   98   70  2반
    도우너    70   97   70  1반
    희동이    70   90   60  2반
    마이콜   100  100  100  1반
      name   국어   영어   수학 반번호
    0   둘리   90   99   90  1반
    1   또치   80   98   70  2반
    2  도우너   70   97   70  1반
    3  희동이   70   90   60  2반
    4  마이콜  100  100  100  1반
        성명   국어   영어   수학 반번호
    0   둘리   90   99   90  1반
    1   또치   80   98   70  2반
    2  도우너   70   97   70  1반
    3  희동이   70   90   60  2반
    4  마이콜  100  100  100  1반



```python
# 문제 6
print(df)
df1 = df.sort_values(by='국어', ascending=False)
df2 = df.sort_values(by='영어')
print(df1)
print(df2)
```

        성명   국어   영어   수학 반번호
    0   둘리   90   99   90  1반
    1   또치   80   98   70  2반
    2  도우너   70   97   70  1반
    3  희동이   70   90   60  2반
    4  마이콜  100  100  100  1반
        성명   국어   영어   수학 반번호
    4  마이콜  100  100  100  1반
    0   둘리   90   99   90  1반
    1   또치   80   98   70  2반
    2  도우너   70   97   70  1반
    3  희동이   70   90   60  2반
        성명   국어   영어   수학 반번호
    3  희동이   70   90   60  2반
    2  도우너   70   97   70  1반
    1   또치   80   98   70  2반
    0   둘리   90   99   90  1반
    4  마이콜  100  100  100  1반



```python
# 문제 7
print(df)
# print(df.loc[ : , '국어':'수학'])
# print([sum(df.loc[ x , '국어':'수학']) for x in range(0, len(df))])

# df['총점'] = [sum(df.loc[ x , '국어':'수학']) for x in range(0, len(df))]
df['총점'] = df['국어'] + df['수학'] + df['영어']
df.sort_values(by='총점', ascending=False, inplace=True )
print(df)
```

           국어   영어   수학 반번호
    name                   
    둘리     90   99   90  1반
    또치     80   98   70  2반
    도우너    70   97   70  1반
    희동이    70   90   60  2반
    마이콜   100  100  100  1반
           국어   영어   수학 반번호   총점
    name                        
    마이콜   100  100  100  1반  300
    둘리     90   99   90  1반  279
    또치     80   98   70  2반  248
    도우너    70   97   70  1반  237
    희동이    70   90   60  2반  220



```python
# 문제 8
df3 = df.drop('반번호', axis=1)
print(df3)
print(df)
```

        성명   국어   영어   수학   총점
    4  마이콜  100  100  100  300
    0   둘리   90   99   90  279
    1   또치   80   98   70  248
    2  도우너   70   97   70  237
    3  희동이   70   90   60  220
        성명   국어   영어   수학 반번호   총점
    4  마이콜  100  100  100  1반  300
    0   둘리   90   99   90  1반  279
    1   또치   80   98   70  2반  248
    2  도우너   70   97   70  1반  237
    3  희동이   70   90   60  2반  220



```python
# 문제 9
df4 = df.drop(4)
print(df4)
print(df)
```

        성명  국어  영어  수학 반번호   총점
    0   둘리  90  99  90  1반  279
    1   또치  80  98  70  2반  248
    2  도우너  70  97  70  1반  237
    3  희동이  70  90  60  2반  220
        성명   국어   영어   수학 반번호   총점
    4  마이콜  100  100  100  1반  300
    0   둘리   90   99   90  1반  279
    1   또치   80   98   70  2반  248
    2  도우너   70   97   70  1반  237
    3  희동이   70   90   60  2반  220



```python
# 문제 10
data1 = {'kor':90, 'mat':80}
data2 = {'kor':90, 'eng':70}
data3 = {'kor':90, 'eng':70, 'mat':80}
series1 = pd.Series( data1 )
series2 = pd.Series( data2 )
series3 = pd.Series( data3 )
result = series1 + series2 + series3
print(result)

result2 = series1.add(series2, fill_value=0).add(series3, fill_value=0)
print(result2)
```

    eng      NaN
    kor    270.0
    mat      NaN
    dtype: float64
    eng    140.0
    kor    270.0
    mat    160.0
    dtype: float64



```python
# 문제 11
data = {
    'X1':[2.9, 2.4, 2, 2.3, 3.2],
    'X2':[9.2, 8.7, 7.2, 8.5, 9.6],
    'X3':[13.2, 11.5, 10.8, 12.3, 12.6],
    'X4':[2, 3, 4, 3, 2]
} 
df = pd.DataFrame(data, index=['Y1','Y2','Y3', 'Y4', 'Y5'])
print(df)
print('=======================================')
df.loc['Y6'] = [x for x in range(10, 50, 10)]
print(df)
df10 = df + 10
print(df10)
# print([sum(df10.loc[ 'Y' + str(x) , 'X1':'X4']) for x in range(1, len(df)+1)])
# df10['total'] = [sum(df10.loc[ 'Y' + str(x) , 'X1':'X4']) for x in range(1, len(df)+1)]
df10['total'] = df10.sum(axis=1)
print(df10)
print(df10.T)
tdf10 = df10.transpose()
print(tdf10)
```

         X1   X2    X3  X4
    Y1  2.9  9.2  13.2   2
    Y2  2.4  8.7  11.5   3
    Y3  2.0  7.2  10.8   4
    Y4  2.3  8.5  12.3   3
    Y5  3.2  9.6  12.6   2
    =======================================
          X1    X2    X3  X4
    Y1   2.9   9.2  13.2   2
    Y2   2.4   8.7  11.5   3
    Y3   2.0   7.2  10.8   4
    Y4   2.3   8.5  12.3   3
    Y5   3.2   9.6  12.6   2
    Y6  10.0  20.0  30.0  40
          X1    X2    X3  X4
    Y1  12.9  19.2  23.2  12
    Y2  12.4  18.7  21.5  13
    Y3  12.0  17.2  20.8  14
    Y4  12.3  18.5  22.3  13
    Y5  13.2  19.6  22.6  12
    Y6  20.0  30.0  40.0  50
          X1    X2    X3  X4  total
    Y1  12.9  19.2  23.2  12   67.3
    Y2  12.4  18.7  21.5  13   65.6
    Y3  12.0  17.2  20.8  14   64.0
    Y4  12.3  18.5  22.3  13   66.1
    Y5  13.2  19.6  22.6  12   67.4
    Y6  20.0  30.0  40.0  50  140.0
             Y1    Y2    Y3    Y4    Y5     Y6
    X1     12.9  12.4  12.0  12.3  13.2   20.0
    X2     19.2  18.7  17.2  18.5  19.6   30.0
    X3     23.2  21.5  20.8  22.3  22.6   40.0
    X4     12.0  13.0  14.0  13.0  12.0   50.0
    total  67.3  65.6  64.0  66.1  67.4  140.0
             Y1    Y2    Y3    Y4    Y5     Y6
    X1     12.9  12.4  12.0  12.3  13.2   20.0
    X2     19.2  18.7  17.2  18.5  19.6   30.0
    X3     23.2  21.5  20.8  22.3  22.6   40.0
    X4     12.0  13.0  14.0  13.0  12.0   50.0
    total  67.3  65.6  64.0  66.1  67.4  140.0



```python
import pandas as pd
# 문제1
df = pd.read_csv('./data/score.csv', header=0)
print("컬럼명 :", df.columns)
print("인덱스 :", df.index)

# df['total'] = df.sum(axis=1)
df['total'] = df.kor + df.eng + df.mat
df['avg'] = round(df.total / 3, 2)
display(df)
```

    컬럼명 : Index(['name', 'kor', 'eng', 'mat'], dtype='object')
    인덱스 : RangeIndex(start=0, stop=5, step=1)



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>kor</th>
      <th>eng</th>
      <th>mat</th>
      <th>total</th>
      <th>avg</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>둘리</td>
      <td>90</td>
      <td>90</td>
      <td>90</td>
      <td>270</td>
      <td>90.00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>또치</td>
      <td>80</td>
      <td>80</td>
      <td>80</td>
      <td>240</td>
      <td>80.00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>도우너</td>
      <td>70</td>
      <td>70</td>
      <td>70</td>
      <td>210</td>
      <td>70.00</td>
    </tr>
    <tr>
      <th>3</th>
      <td>희동이</td>
      <td>90</td>
      <td>80</td>
      <td>70</td>
      <td>240</td>
      <td>80.00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>마이콜</td>
      <td>60</td>
      <td>50</td>
      <td>50</td>
      <td>160</td>
      <td>53.33</td>
    </tr>
  </tbody>
</table>

</div>



```python
# 문제2
df = pd.read_csv('./data/score_noheader.csv', header=None)
display(df)
print("컬럼명 :", df.columns)
print("인덱스 :", df.index)

print("컬럼명 추가 --------------")
df.columns=['name', 'kor', 'eng', 'mat']
print("컬럼명 :", df.columns)
display(df)

print("total과 avg열 추가 --------------")
df['total'] = df.kor + df.eng + df.mat
df['avg'] = round(df.total / 3, 2)
display(df)
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>둘리</td>
      <td>90</td>
      <td>90</td>
      <td>90</td>
    </tr>
    <tr>
      <th>1</th>
      <td>또치</td>
      <td>80</td>
      <td>80</td>
      <td>80</td>
    </tr>
    <tr>
      <th>2</th>
      <td>도우너</td>
      <td>70</td>
      <td>70</td>
      <td>70</td>
    </tr>
    <tr>
      <th>3</th>
      <td>희동이</td>
      <td>90</td>
      <td>80</td>
      <td>70</td>
    </tr>
    <tr>
      <th>4</th>
      <td>마이콜</td>
      <td>60</td>
      <td>50</td>
      <td>50</td>
    </tr>
  </tbody>
</table>

</div>


    컬럼명 : Int64Index([0, 1, 2, 3], dtype='int64')
    인덱스 : RangeIndex(start=0, stop=5, step=1)
    컬럼명 추가 --------------
    컬럼명 : Index(['name', 'kor', 'eng', 'mat'], dtype='object')



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>kor</th>
      <th>eng</th>
      <th>mat</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>둘리</td>
      <td>90</td>
      <td>90</td>
      <td>90</td>
    </tr>
    <tr>
      <th>1</th>
      <td>또치</td>
      <td>80</td>
      <td>80</td>
      <td>80</td>
    </tr>
    <tr>
      <th>2</th>
      <td>도우너</td>
      <td>70</td>
      <td>70</td>
      <td>70</td>
    </tr>
    <tr>
      <th>3</th>
      <td>희동이</td>
      <td>90</td>
      <td>80</td>
      <td>70</td>
    </tr>
    <tr>
      <th>4</th>
      <td>마이콜</td>
      <td>60</td>
      <td>50</td>
      <td>50</td>
    </tr>
  </tbody>
</table>

</div>


    total과 avg열 추가 --------------



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>kor</th>
      <th>eng</th>
      <th>mat</th>
      <th>total</th>
      <th>avg</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>둘리</td>
      <td>90</td>
      <td>90</td>
      <td>90</td>
      <td>270</td>
      <td>90.00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>또치</td>
      <td>80</td>
      <td>80</td>
      <td>80</td>
      <td>240</td>
      <td>80.00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>도우너</td>
      <td>70</td>
      <td>70</td>
      <td>70</td>
      <td>210</td>
      <td>70.00</td>
    </tr>
    <tr>
      <th>3</th>
      <td>희동이</td>
      <td>90</td>
      <td>80</td>
      <td>70</td>
      <td>240</td>
      <td>80.00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>마이콜</td>
      <td>60</td>
      <td>50</td>
      <td>50</td>
      <td>160</td>
      <td>53.33</td>
    </tr>
  </tbody>
</table>

</div>



```python
# 문제3
df = pd.read_csv('./data/score_header.csv', header=3)
display(df)
print("컬럼명 :", df.columns)
print("인덱스 :", df.index)

df['total'] = df.kor + df.eng + df.mat
df['avg'] = round(df.total / 3, 2)
display(df)
for i in range(0, 3) :
    df.to_csv("C:/Temp/score_result.csv", index=False, header=False, mode='a')
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>kor</th>
      <th>eng</th>
      <th>mat</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>둘리</td>
      <td>90</td>
      <td>90</td>
      <td>90</td>
    </tr>
    <tr>
      <th>1</th>
      <td>또치</td>
      <td>80</td>
      <td>80</td>
      <td>80</td>
    </tr>
    <tr>
      <th>2</th>
      <td>도우너</td>
      <td>70</td>
      <td>70</td>
      <td>70</td>
    </tr>
    <tr>
      <th>3</th>
      <td>희동이</td>
      <td>90</td>
      <td>80</td>
      <td>70</td>
    </tr>
    <tr>
      <th>4</th>
      <td>마이콜</td>
      <td>60</td>
      <td>50</td>
      <td>50</td>
    </tr>
  </tbody>
</table>

</div>


    컬럼명 : Index(['name', 'kor', 'eng', 'mat'], dtype='object')
    인덱스 : RangeIndex(start=0, stop=5, step=1)



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>kor</th>
      <th>eng</th>
      <th>mat</th>
      <th>total</th>
      <th>avg</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>둘리</td>
      <td>90</td>
      <td>90</td>
      <td>90</td>
      <td>270</td>
      <td>90.00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>또치</td>
      <td>80</td>
      <td>80</td>
      <td>80</td>
      <td>240</td>
      <td>80.00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>도우너</td>
      <td>70</td>
      <td>70</td>
      <td>70</td>
      <td>210</td>
      <td>70.00</td>
    </tr>
    <tr>
      <th>3</th>
      <td>희동이</td>
      <td>90</td>
      <td>80</td>
      <td>70</td>
      <td>240</td>
      <td>80.00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>마이콜</td>
      <td>60</td>
      <td>50</td>
      <td>50</td>
      <td>160</td>
      <td>53.33</td>
    </tr>
  </tbody>
</table>

</div>



```python
# 문제4
df = pd.read_excel('./data/score.xlsx', header=0) 
display(df)

df['total'] = df.kor + df.eng + df.mat
df['avg'] = round(df.total / 3, 2)
df.sort_values(by='total', ascending=False, inplace=True)
display(df)

df.to_excel("c:/Temp/score_result1.xlsx")
df.to_excel("c:/Temp/score_result2.xlsx", index=False)
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>kor</th>
      <th>eng</th>
      <th>mat</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>둘리</td>
      <td>90</td>
      <td>90</td>
      <td>90</td>
    </tr>
    <tr>
      <th>1</th>
      <td>또치</td>
      <td>80</td>
      <td>80</td>
      <td>80</td>
    </tr>
    <tr>
      <th>2</th>
      <td>도우너</td>
      <td>70</td>
      <td>70</td>
      <td>70</td>
    </tr>
    <tr>
      <th>3</th>
      <td>희동이</td>
      <td>90</td>
      <td>80</td>
      <td>70</td>
    </tr>
    <tr>
      <th>4</th>
      <td>마이콜</td>
      <td>60</td>
      <td>50</td>
      <td>50</td>
    </tr>
    <tr>
      <th>5</th>
      <td>고길동</td>
      <td>90</td>
      <td>90</td>
      <td>0</td>
    </tr>
  </tbody>
</table>

</div>



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>kor</th>
      <th>eng</th>
      <th>mat</th>
      <th>total</th>
      <th>avg</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>둘리</td>
      <td>90</td>
      <td>90</td>
      <td>90</td>
      <td>270</td>
      <td>90.00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>또치</td>
      <td>80</td>
      <td>80</td>
      <td>80</td>
      <td>240</td>
      <td>80.00</td>
    </tr>
    <tr>
      <th>3</th>
      <td>희동이</td>
      <td>90</td>
      <td>80</td>
      <td>70</td>
      <td>240</td>
      <td>80.00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>도우너</td>
      <td>70</td>
      <td>70</td>
      <td>70</td>
      <td>210</td>
      <td>70.00</td>
    </tr>
    <tr>
      <th>5</th>
      <td>고길동</td>
      <td>90</td>
      <td>90</td>
      <td>0</td>
      <td>180</td>
      <td>60.00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>마이콜</td>
      <td>60</td>
      <td>50</td>
      <td>50</td>
      <td>160</td>
      <td>53.33</td>
    </tr>
  </tbody>
</table>

</div>



```python
# 문제5
df = pd.read_json('./data/mydata.json')  
print("기본정보 보기")
print(df.info())

print("앞에서 부터 5개만 미리 보기")
print(df.head())

print("뒤에서 부터 5개만 미리 보기")
print(df.tail())

print("앞에서 부터 10개만 미리 보기")
print(df.head(10))
print(df.shape)
print('행의 개수 :', df.shape[0], '열의 개수 :', df.shape[1])
```

    기본정보 보기
    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 24 entries, 0 to 23
    Data columns (total 4 columns):
     #   Column  Non-Null Count  Dtype
    ---  ------  --------------  -----
     0   year    24 non-null     int64
     1   item1   24 non-null     int64
     2   item2   24 non-null     int64
     3   item3   24 non-null     int64
    dtypes: int64(4)
    memory usage: 896.0 bytes
    None
    앞에서 부터 5개만 미리 보기
       year  item1  item2  item3
    0  1990     95     20     15
    1  1991     65     10     35
    2  1992     45     30     90
    3  1993     10     40     70
    4  1994     22     50     50
    뒤에서 부터 5개만 미리 보기
        year  item1  item2  item3
    19  2009     99     90     70
    20  2010     75     85     45
    21  2011     22     42     22
    22  2012     63     13     30
    23  2013     80     40     90
    앞에서 부터 10개만 미리 보기
       year  item1  item2  item3
    0  1990     95     20     15
    1  1991     65     10     35
    2  1992     45     30     90
    3  1993     10     40     70
    4  1994     22     50     50
    5  1995     35     70     30
    6  1996     40     80     25
    7  1997     25     90     75
    8  1998     15     57     95
    9  1999     45     79     33
    (24, 4)
    행의 개수 : 24 열의 개수 : 4



```python
# 문제6
df = pd.read_csv('./data/mpgdata.csv', header=0)
print('앞에서 부터 3개만 미리 보기')
display(df.head(3))
print('행의 개수', df.shape[0])
print('열의 개수', df.shape[1])
print('기술통계 정보 요약')
display(df.describe())
```

    앞에서 부터 3개만 미리 보기



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>mpg</th>
      <th>cylinders</th>
      <th>displacement</th>
      <th>horsepower</th>
      <th>weight</th>
      <th>acceleration</th>
      <th>model-year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>18.0</td>
      <td>8</td>
      <td>307.0</td>
      <td>130.0</td>
      <td>3504</td>
      <td>12.0</td>
      <td>70</td>
    </tr>
    <tr>
      <th>1</th>
      <td>15.0</td>
      <td>8</td>
      <td>350.0</td>
      <td>165.0</td>
      <td>3693</td>
      <td>11.5</td>
      <td>70</td>
    </tr>
    <tr>
      <th>2</th>
      <td>18.0</td>
      <td>8</td>
      <td>318.0</td>
      <td>150.0</td>
      <td>3436</td>
      <td>11.0</td>
      <td>70</td>
    </tr>
  </tbody>
</table>

</div>


    행의 개수 398
    열의 개수 7
    기술통계 정보 요약



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>mpg</th>
      <th>cylinders</th>
      <th>displacement</th>
      <th>horsepower</th>
      <th>weight</th>
      <th>acceleration</th>
      <th>model-year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>398.000000</td>
      <td>398.000000</td>
      <td>398.000000</td>
      <td>396.000000</td>
      <td>398.000000</td>
      <td>398.000000</td>
      <td>398.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>23.514573</td>
      <td>5.454774</td>
      <td>193.425879</td>
      <td>104.189394</td>
      <td>2970.424623</td>
      <td>15.568090</td>
      <td>76.010050</td>
    </tr>
    <tr>
      <th>std</th>
      <td>7.815984</td>
      <td>1.701004</td>
      <td>104.269838</td>
      <td>38.402030</td>
      <td>846.841774</td>
      <td>2.757689</td>
      <td>3.697627</td>
    </tr>
    <tr>
      <th>min</th>
      <td>9.000000</td>
      <td>3.000000</td>
      <td>68.000000</td>
      <td>46.000000</td>
      <td>1613.000000</td>
      <td>8.000000</td>
      <td>70.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>17.500000</td>
      <td>4.000000</td>
      <td>104.250000</td>
      <td>75.000000</td>
      <td>2223.750000</td>
      <td>13.825000</td>
      <td>73.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>23.000000</td>
      <td>4.000000</td>
      <td>148.500000</td>
      <td>92.000000</td>
      <td>2803.500000</td>
      <td>15.500000</td>
      <td>76.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>29.000000</td>
      <td>8.000000</td>
      <td>262.000000</td>
      <td>125.000000</td>
      <td>3608.000000</td>
      <td>17.175000</td>
      <td>79.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>46.600000</td>
      <td>8.000000</td>
      <td>455.000000</td>
      <td>230.000000</td>
      <td>5140.000000</td>
      <td>24.800000</td>
      <td>82.000000</td>
    </tr>
  </tbody>
</table>

</div>

