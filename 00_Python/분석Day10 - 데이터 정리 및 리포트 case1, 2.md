

# 분석Day10

>  분석Day10 - 데이터 정리 및 리포트 case1, 2

### - case1

```python
# 경고(worning) 비표시
import warnings
warnings.filterwarnings('ignore')
```

# 제1장 웹에서 주문수를 분석하는 테크닉 

### [분석요청 시나리오]

### 우리 회사는 오랫동안 쇼핑몰 사이트를 운영하고 있습니다. 고객 정보는 전부 쇼핑몰 사이트에서 관리하고 있어 데이터는

### 많습니다. 지금 많은 기업들이 데이터 분석으로 성과를 내고 있다고 들어서 우리 회사도 현재 유행하는 데이터 분석을

### 도입하려고 합니다. 하지만 대부분의 사원이 문과 출신이라 데이터 분석에 어둡고 무엇부터 시작해야 할지 잘 모릅니다.

### 테크닉1 : 데이터를 읽어들이자


```python
import pandas as pd
customer_master = pd.read_csv('customer_master.csv')
customer_master.head()
```


```python
item_master = pd.read_csv('item_master.csv')
item_master.head()
```


```python
transaction_1 = pd.read_csv('transaction_1.csv')
transaction_1.head()
```


```python
transaction_detail_1 = pd.read_csv('transaction_detail_1.csv')
transaction_detail_1.head()
```

### 테크닉2 : 데이터를 결합(유니언)해보자


```python
transaction_2 = pd.read_csv('transaction_2.csv')
transaction = pd.concat([transaction_1, transaction_2], ignore_index=True)
transaction.head()
```


```python
print(len(transaction_1))
print(len(transaction_2))
print(len(transaction))
```


```python
transaction_detail_2 = pd.read_csv('transaction_detail_2.csv')
transaction_detail=pd.concat([transaction_detail_1,transaction_detail_2], ignore_index=True)
transaction_detail.head()
```

### 테크닉3 : 매출 데이터끼리 결합(조인)해보자


```python
join_data = pd.merge(transaction_detail, transaction[["transaction_id", "payment_date", "customer_id"]], 
                     on="transaction_id", how="left")
join_data.head()
```


```python
print(len(transaction_detail))
print(len(transaction))
print(len(join_data))
```

### 테크닉4 : 마스터데이터를 결합(조인)해보자


```python
join_data = pd.merge(join_data, customer_master, on="customer_id", how="left")
join_data = pd.merge(join_data, item_master, on="item_id", how="left")
join_data.head()
```

### 테크닉5 : 필요한 데이터 컬럼을 만들자


```python
join_data["price"] = join_data["quantity"] * join_data["item_price"]
join_data[["quantity", "item_price","price"]].head()
```

### 테크닉6 : 데이터를 검산하자


```python
print(join_data["price"].sum())
print(transaction["price"].sum())
```


```python
join_data["price"].sum() == transaction["price"].sum()
```

### 테크닉7 : 각종 통계량을 파악하자


```python
join_data.isnull().sum()
```


```python
join_data.info()
```


```python
join_data.describe()
```


```python
print(join_data["payment_date"].min())
print(join_data["payment_date"].max())
```

### 테크닉8 : 월별로 데이터를 집계해보자


```python
join_data.dtypes
```


```python
join_data["payment_date"] = pd.to_datetime(join_data["payment_date"])
join_data["payment_month"] = join_data["payment_date"].dt.strftime("%Y%m")
join_data[["payment_date", "payment_month"]].head()
```


```python
join_data.groupby("payment_month").sum()["price"]
```

### 테크닉9 : 월별, 상품별 데이터를 집계해보자


```python
join_data.groupby(["payment_month","item_name"]).sum()[["price", "quantity"]]
```


```python
pd.pivot_table(join_data, index='item_name', columns='payment_month', values=['price', 'quantity'], aggfunc='sum')
```


```python
pvt = pd.pivot_table(join_data, index='item_name', columns='payment_month', values=['price', 'quantity'], aggfunc='sum')
pvt.xs('PC-A')
```

### 테크닉10 : 상품별 매출 추이를 가시화해보자


```python
graph_data = pd.pivot_table(join_data, index='payment_month', columns='item_name', values='price', aggfunc='sum')
graph_data.head()
```


```python
import matplotlib.pyplot as plt
%matplotlib inline
plt.plot(list(graph_data.index), graph_data["PC-A"], label='PC-A')
plt.plot(list(graph_data.index), graph_data["PC-B"], label='PC-B')
plt.plot(list(graph_data.index), graph_data["PC-C"], label='PC-C')
plt.plot(list(graph_data.index), graph_data["PC-D"], label='PC-D')
plt.plot(list(graph_data.index), graph_data["PC-E"], label='PC-E')
plt.legend()  
```


```python
import seaborn as sns
sns.lineplot(graph_data.index, graph_data['PC-A'])
```



# pandas의 pivot_table 익히기


```python
import pandas as pd
import numpy as np
```


```python
df = pd.read_excel("sales-funnel.xlsx")
df.head()
```


```python
pd.pivot_table(df, index=["Name"])
```


```python
pd.pivot_table(df,index=["Name","Rep","Manager"])
```


```python
pd.pivot_table(df,index=["Manager","Rep"])
```


```python
pd.pivot_table(df,index=["Manager","Rep"], values=["Price"])
```


```python
pd.pivot_table(df,index=["Manager","Rep"],values=["Price"],aggfunc=np.sum)
```


```python
pd.pivot_table(df,index=["Manager","Rep"],values=["Price"],aggfunc=[np.mean,len])
```


```python
pd.pivot_table(df,index=["Manager","Rep"], values=["Price"], columns=["Product"],aggfunc=[np.sum])
```


```python
p_t = pd.pivot_table(df,index=["Manager","Rep"], values=["Price"], columns=["Product"],aggfunc=[np.sum])
print(p_t.xs(('Debra Henley', 'John Smith')))
```


```python
pd.pivot_table(df,index=["Manager","Rep"],values=["Price"], columns=["Product"],aggfunc=[np.sum], fill_value=0)
```


```python
pd.pivot_table(df,index=["Manager","Rep","Product"],
               values=["Price","Quantity"],aggfunc=[np.sum],fill_value=0)
```


```python
pd.pivot_table(df,index=["Manager","Rep","Product"],
               values=["Price","Quantity"],
               aggfunc=[np.sum,np.mean],fill_value=0,margins=True)
```





### case 2

```python
import numpy as np
import pandas as pd
```


```python
crime_anal_police = pd.read_csv('crime_in_Seoul.csv', thousands=',', encoding='euc-kr')
crime_anal_police.head()
```


```python
import googlemaps
```


```python
gmaps_key = "AIzaSyDy81EbO46BRSnX1DOgg_F84bhsdbku2z4" # 자신의 key를 사용합니다.
gmaps = googlemaps.Client(key=gmaps_key)
```


```python
gmaps.geocode('서울중부경찰서', language='ko')
```


```python
station_name = []

for name in crime_anal_police['관서명']:
    station_name.append('서울' + str(name[:-1]) + '경찰서')

station_name
```


```python
station_addreess = []
station_lat = []
station_lng = []

for name in station_name:
    tmp = gmaps.geocode(name, language='ko')
    station_addreess.append(tmp[0].get("formatted_address"))
    
    tmp_loc = tmp[0].get("geometry")

    station_lat.append(tmp_loc['location']['lat'])
    station_lng.append(tmp_loc['location']['lng'])
    
    print(name + '-->' + tmp[0].get("formatted_address"))
```


```python
# pd.set_option('display.max_columns', 10)                  # 출력할 최대 열의 개수
# pd.set_option('display.max_colwidth', 20)                 # 출력할 열의 너비
# pd.set_option('display.unicode.east_asian_width', True)   # 유니코드 사용 너비 조정
station_addreess
```


```python
station_lat
```


```python
station_lng
```


```python
gu_name = []

for name in station_addreess:
    tmp = name.split()
    
    tmp_gu = [gu for gu in tmp if gu[-1] == '구'][0]
    
    gu_name.append(tmp_gu)
    
crime_anal_police['구별'] = gu_name
crime_anal_police.head()
```


```python
crime_anal_police[crime_anal_police['관서명']=='금천서']
```


```python
crime_anal_police.loc[crime_anal_police['관서명']=='금천서', ['구별']] = '금천구'
crime_anal_police[crime_anal_police['관서명']=='금천서']
```


```python
crime_anal_police.to_csv('crime_in_Seoul_include_gu_name.csv',
                         sep=',', encoding='utf-8')
```


```python
crime_anal_police.head()
```



# 범죄 데이터 구별로 정리하기


```python
crime_anal_raw = pd.read_csv('crime_in_Seoul_include_gu_name.csv', 
                             encoding='utf-8')
crime_anal_raw.head()
```


```python
crime_anal_raw = pd.read_csv('crime_in_Seoul_include_gu_name.csv', 
                             encoding='utf-8', index_col=0)
crime_anal_raw.head()
```


```python
crime_anal = pd.pivot_table(crime_anal_raw, index='구별', aggfunc=np.sum)
crime_anal.head()
```


```python
crime_anal['강간검거율'] = crime_anal['강간 검거']/crime_anal['강간 발생']*100
crime_anal['강도검거율'] = crime_anal['강도 검거']/crime_anal['강도 발생']*100
crime_anal['살인검거율'] = crime_anal['살인 검거']/crime_anal['살인 발생']*100
crime_anal['절도검거율'] = crime_anal['절도 검거']/crime_anal['절도 발생']*100
crime_anal['폭력검거율'] = crime_anal['폭력 검거']/crime_anal['폭력 발생']*100

del crime_anal['강간 검거']
del crime_anal['강도 검거']
del crime_anal['살인 검거']
del crime_anal['절도 검거']
del crime_anal['폭력 검거']

crime_anal.head()
```


```python
con_list = ['강간검거율', '강도검거율', '살인검거율', '절도검거율', '폭력검거율']

for column in con_list:
    crime_anal.loc[crime_anal[column] > 100, column] = 100
    
crime_anal.head()
```


```python
crime_anal.rename(columns = {'강간 발생':'강간', 
                             '강도 발생':'강도', 
                             '살인 발생':'살인', 
                             '절도 발생':'절도', 
                             '폭력 발생':'폭력'}, inplace=True)
crime_anal.head()
```


```python
from sklearn import preprocessing

col = ['강간', '강도', '살인', '절도', '폭력']

x = crime_anal[col].values
print(crime_anal[col].values)
min_max_scaler = preprocessing.MinMaxScaler()
print(min_max_scaler)

x_scaled = min_max_scaler.fit_transform(x.astype(float))
crime_anal_norm = pd.DataFrame(x_scaled, columns = col, index = crime_anal.index)

col2 = ['강간검거율', '강도검거율', '살인검거율', '절도검거율', '폭력검거율']
crime_anal_norm[col2] = crime_anal[col2]
crime_anal_norm.head()
```


```python
result_CCTV = pd.read_csv('CCTV_result.csv', encoding='UTF-8', 
                          index_col='구별')
crime_anal_norm[['인구수', 'CCTV']] = result_CCTV[['인구수', '소계']]
crime_anal_norm.head()
```


```python
col = ['강간','강도','살인','절도','폭력']
crime_anal_norm['범죄'] = np.sum(crime_anal_norm[col], axis=1)
crime_anal_norm.head()
```


```python
col = ['강간검거율','강도검거율','살인검거율','절도검거율','폭력검거율']
crime_anal_norm['검거'] = np.sum(crime_anal_norm[col], axis=1)
crime_anal_norm.head()
```


```python
crime_anal_norm
```

# seaborn


```python
import matplotlib.pyplot as plt
%matplotlib inline

import seaborn as sns

x = np.linspace(0, 14, 100)
y1 = np.sin(x)
y2 = 2*np.sin(x+0.5)
y3 = 3*np.sin(x+1.0)
y4 = 4*np.sin(x+1.5)

plt.figure(figsize=(10,6))
plt.plot(x,y1, x,y2, x,y3, x,y4)
plt.show()
```


```python
sns.set_style("white")

plt.figure(figsize=(10,6))
plt.plot(x,y1, x,y2, x,y3, x,y4)

sns.despine()

plt.show()
```


```python
sns.set_style("dark")

plt.figure(figsize=(10,6))
plt.plot(x,y1, x,y2, x,y3, x,y4)
plt.show()
```


```python
sns.set_style("whitegrid")

plt.figure(figsize=(10,6))
plt.plot(x,y1, x,y2, x,y3, x,y4)
plt.show()
```


```python
plt.figure(figsize=(10,6))
plt.plot(x,y1, x,y2, x,y3, x,y4)

sns.despine(offset=10)

plt.show()
```


```python
import matplotlib.pyplot as plt
import numpy as np
import seaborn as sns

sns.set_style("whitegrid")
%matplotlib inline
```


```python
tips = sns.load_dataset("tips")
tips.head(5)
```


```python
sns.set_style("whitegrid")

plt.figure(figsize=(8,6))
sns.boxplot(x=tips["total_bill"])
plt.show()
```


```python
plt.figure(figsize=(8,6))
sns.boxplot(x="day", y="total_bill", data=tips)
plt.show()
```


```python
plt.figure(figsize=(8,6))
sns.boxplot(x="day", y="total_bill", hue="smoker", data=tips, palette="Set3")
plt.show()
```


```python
plt.figure(figsize=(8,6))
sns.swarmplot(x="day", y="total_bill", data=tips, color=".5")
plt.show()
```


```python
plt.figure(figsize=(8,6))
sns.boxplot(x="day", y="total_bill", data=tips)
sns.swarmplot(x="day", y="total_bill", data=tips, color=".25")
plt.show()
```


```python
import matplotlib.pyplot as plt
import seaborn as sns
%matplotlib inline

tips = sns.load_dataset("tips")
tips.head(5)
```


```python
sns.set_style("darkgrid")
sns.lmplot(x="total_bill", y="tip", data=tips, size=7)
plt.show()
```


```python
sns.lmplot(x="total_bill", y="tip", hue="smoker", data=tips, size=7)
plt.show()
```


```python
sns.lmplot(x="total_bill", y="tip", hue="smoker", data=tips, palette="Set1", size=7)
plt.show()
```


```python
uniform_data = np.random.rand(10, 12)
uniform_data
```


```python
sns.heatmap(uniform_data)
plt.show()
```


```python
sns.heatmap(uniform_data, vmin=0, vmax=1)
plt.show()
```


```python
flights = sns.load_dataset("flights")
flights.head(5)
```


```python
flights = flights.pivot("month", "year", "passengers")
flights.head(5)
```


```python
plt.figure(figsize=(10,8))
sns.heatmap(flights)
plt.show()
```


```python
plt.figure(figsize=(10,8))
sns.heatmap(flights, annot=True, fmt="d")
plt.show()
```


```python
sns.set(style="ticks")
iris = sns.load_dataset("iris")
iris.head(10)
```


```python
sns.pairplot(iris)
plt.show()
```


```python
sns.pairplot(iris, hue="species")
plt.show()
```


```python
sns.pairplot(iris, vars=["sepal_width", "sepal_length"])
plt.show()
```


```python
sns.pairplot(iris, x_vars=["sepal_width", "sepal_length"], 
             y_vars=["petal_width", "petal_length"])
plt.show()
```


```python
anscombe = sns.load_dataset("anscombe")
anscombe.head(5)
```


```python
sns.set_style("darkgrid")

sns.lmplot(x="x", y="y", data=anscombe.query("dataset == 'I'"),  ci=None, size=7)
plt.show()
```


```python
sns.lmplot(x="x", y="y", data=anscombe.query("dataset == 'I'"),
           ci=None, scatter_kws={"s": 80}, size=7)
plt.show()
```


```python
sns.lmplot(x="x", y="y", data=anscombe.query("dataset == 'II'"),
           order=1, ci=None, scatter_kws={"s": 80}, size=7)
plt.show()
```


```python
sns.lmplot(x="x", y="y", data=anscombe.query("dataset == 'II'"),
           order=2, ci=None, scatter_kws={"s": 80}, size=7)
plt.show()
```


```python
sns.lmplot(x="x", y="y", data=anscombe.query("dataset == 'III'"),
           ci=None, scatter_kws={"s": 80}, size=7)
plt.show()
```

# Visualization using seaborn


```python
import matplotlib.pyplot as plt
import seaborn as sns

from matplotlib import font_manager, rc
font_path = "../data/THEdog.ttf"   #폰트파일의 위치
font_name = font_manager.FontProperties(fname=font_path).get_name()
rc('font', family=font_name)
```


```python
crime_anal_norm.head()
```


```python
sns.pairplot(crime_anal_norm, vars=["강도", "살인", "폭력"], kind='reg', size=3)
plt.show()
```


```python
sns.pairplot(crime_anal_norm, x_vars=["인구수", "CCTV"], 
             y_vars=["살인", "강도"], kind='reg', size=3)
plt.show()
```


```python
sns.pairplot(crime_anal_norm, x_vars=["인구수", "CCTV"], 
             y_vars=["살인검거율", "폭력검거율"], kind='reg', size=3)
plt.show()
```


```python
sns.pairplot(crime_anal_norm, x_vars=["인구수", "CCTV"], 
             y_vars=["절도검거율", "강도검거율"], kind='reg', size=3)
plt.show()
```


```python
tmp_max = crime_anal_norm['검거'].max()
crime_anal_norm['검거'] = crime_anal_norm['검거'] / tmp_max * 100
crime_anal_norm_sort = crime_anal_norm.sort_values(by='검거', ascending=False)
crime_anal_norm_sort.head()
```


```python
target_col = ['강간검거율', '강도검거율', '살인검거율', '절도검거율', '폭력검거율']

crime_anal_norm_sort = crime_anal_norm.sort_values(by='검거', ascending=False)

plt.figure(figsize = (10,10))
sns.heatmap(crime_anal_norm_sort[target_col], annot=True, fmt='f', 
                    linewidths=.5, cmap='RdPu')
plt.title('범죄 검거 비율 (정규화된 검거의 합으로 정렬)')
plt.show()
```


```python
target_col = ['강간', '강도', '살인', '절도', '폭력', '범죄']

crime_anal_norm['범죄'] = crime_anal_norm['범죄'] / 5
crime_anal_norm_sort = crime_anal_norm.sort_values(by='범죄', ascending=False)

plt.figure(figsize = (10,10))
sns.heatmap(crime_anal_norm_sort[target_col], annot=True, fmt='f', linewidths=.5,
                       cmap='RdPu')
plt.title('범죄비율 (정규화된 발생 건수로 정렬)')
plt.show()
```


```python
crime_anal_norm.to_csv('crime_in_Seoul_final.csv', sep=',', 
                       encoding='utf-8')
```

# Folium 


```python
import folium
import pandas as pd
```

# 범죄율에 대한 지도 시각화


```python
import json
geo_path = 'skorea_municipalities_geo_simple.json'
geo_str = json.load(open(geo_path, encoding='utf-8'))
```


```python
map = folium.Map(location=[37.5502, 126.982], zoom_start=11, 
                 tiles='Stamen Toner')

map.choropleth(geo_data = geo_str,
               data = crime_anal_norm['살인'],
               columns = [crime_anal_norm.index, crime_anal_norm['살인']],
               fill_color = 'PuRd', #PuRd, YlGnBu
               key_on = 'feature.id')
map
```


```python
map = folium.Map(location=[37.5502, 126.982], zoom_start=11, 
                 tiles='Stamen Toner')

map.choropleth(geo_data = geo_str,
               data = crime_anal_norm['강간'],
               columns = [crime_anal_norm.index, crime_anal_norm['강간']],
               fill_color = 'PuRd', #PuRd, YlGnBu
               key_on = 'feature.id')
map
```


```python
map = folium.Map(location=[37.5502, 126.982], zoom_start=11, 
                 tiles='Stamen Toner')

map.choropleth(geo_data = geo_str,
               data = crime_anal_norm['범죄'],
               columns = [crime_anal_norm.index, crime_anal_norm['범죄']],
               fill_color = 'PuRd', #PuRd, YlGnBu
               key_on = 'feature.id')
map
```


```python
tmp_criminal = crime_anal_norm['살인'] /  crime_anal_norm['인구수'] * 1000000

map = folium.Map(location=[37.5502, 126.982], zoom_start=11, 
                 tiles='Stamen Toner')

map.choropleth(geo_data = geo_str,
               data = tmp_criminal,
               columns = [crime_anal.index, tmp_criminal],
               fill_color = 'PuRd', #PuRd, YlGnBu
               key_on = 'feature.id')
map
```


```python
tmp_criminal = crime_anal_norm['범죄'] /  crime_anal_norm['인구수'] * 1000000

map = folium.Map(location=[37.5502, 126.982], zoom_start=11, 
                 tiles='Stamen Toner')

map.choropleth(geo_data = geo_str,
               data = tmp_criminal,
               columns = [crime_anal.index, tmp_criminal],
               fill_color = 'PuRd', #PuRd, YlGnBu
               key_on = 'feature.id')
map
```


```python
map = folium.Map(location=[37.5502, 126.982], zoom_start=11, 
                 tiles='Stamen Toner')

map.choropleth(geo_data = geo_str,
               data = crime_anal_norm['검거'],
               columns = [crime_anal_norm.index, crime_anal_norm['검거']],
               fill_color = 'YlGnBu', #PuRd, YlGnBu
               key_on = 'feature.id')
map
```

# 경찰서별 검거현황과 구별 범죄발생 현황을 표현하기


```python
crime_anal_raw['lat'] = station_lat
crime_anal_raw['lng'] = station_lng

col = ['살인 검거', '강도 검거', '강간 검거', '절도 검거', '폭력 검거']
tmp = crime_anal_raw[col] / crime_anal_raw[col].max()
    
crime_anal_raw['검거'] = np.sum(tmp, axis=1)

crime_anal_raw.head()
```


```python
map = folium.Map(location=[37.5502, 126.982], zoom_start=11)

for n in crime_anal_raw.index:
    folium.Marker([crime_anal_raw['lat'][n], 
                   crime_anal_raw['lng'][n]]).add_to(map)
    
map
```


```python
map = folium.Map(location=[37.5502, 126.982], zoom_start=11)

for n in crime_anal_raw.index:
    folium.CircleMarker([crime_anal_raw['lat'][n], crime_anal_raw['lng'][n]], 
                        radius = crime_anal_raw['검거'][n]*10, 
                        color='#3186cc', fill_color='#3186cc', fill=True).add_to(map)
    
map
```


```python
map = folium.Map(location=[37.5502, 126.982], zoom_start=11)

map.choropleth(geo_data = geo_str,
               data = crime_anal_norm['범죄'],
               columns = [crime_anal_norm.index, crime_anal_norm['범죄']],
               fill_color = 'PuRd', #PuRd, YlGnBu
               key_on = 'feature.id')

for n in crime_anal_raw.index:
    folium.CircleMarker([crime_anal_raw['lat'][n], crime_anal_raw['lng'][n]], 
                        radius = crime_anal_raw['검거'][n]*10, 
                        color='#3186cc', fill_color='#3186cc', fill=True).add_to(map)
    
map
```

