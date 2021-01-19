

# 분석Day03

>  데이터 수집

### - 교육내용

```python
from bs4 import BeautifulSoup
import urllib.request as req

busNum = '360'
key = '%2BjzsSyNtwmcqxUsGnflvs3rW2oceFvhHR8AFkM3ao%2Fw50hwHXgGyPVutXw04uAXvrkoWgkoScvvhlH7jgD4%2FRQ%3D%3D'
url1 = 'http://ws.bus.go.kr/api/rest/busRouteInfo/getBusRouteList?serviceKey='+key+'&strSrch='+busNum
savename = 'C:/Temp/businfo.xml'
req.urlretrieve(url1, savename)

xml = open(savename, 'r', encoding='utf-8').read()
soup = BeautifulSoup(xml, features="xml")

busRouteId = None
for itemList in soup.find_all('itemList') :
    busRouteId = itemList.find('busRouteId').string
    busRouteNm = itemList.find('busRouteNm').string
    if busRouteNm == busNum :
        break

url2 = 'http://ws.bus.go.kr/api/rest/busRouteInfo/getStaionByRoute?ServiceKey='+key+'&busRouteId='+busRouteId

savename = 'C:/Temp/buspos.xml'
req.urlretrieve(url2, savename)

xml = open(savename, 'r', encoding='utf-8').read()
soup = BeautifulSoup(xml, features="xml")

busPos = []
for itemList in soup.find_all('itemList') :
    gpsY = itemList.find('gpsY').string
    gpsX = itemList.find('gpsX').string

    busPos.append((gpsY, gpsX))

print('[ ' + busNum + '번 버스의 운행 위치 ]')
if len(busPos) != 0 :
    print(busNum + '번 버스 ' + str(len(busPos)) + '대 운행중...')
    for lat,lng in busPos :
        print(lat+','+lng)
else :
    print('현재 운행중인 ' + busNum + '번 버스가 없어요...')


```


```python
from bs4 import BeautifulSoup
import urllib.request as req

key = '796143536a756e69313134667752417a'
contentType = 'xml'
startIndex = '1'
endIndex = '100'
url = 'http://openapi.seoul.go.kr:8088/'+key+'/'+contentType+'/LampScpgmtb/'+startIndex+'/'+endIndex+'/'
savename = 'C:/Temp/edu.xml'
req.urlretrieve(url, savename)

xml = open(savename, 'r', encoding='utf-8').read()
soup = BeautifulSoup(xml, 'xml')

pjList = []
for itemList in soup.find_all('row') :
    up_nm = itemList.find('UP_NM').string
    up_nm = '없음' if up_nm is None else up_nm
    pgm_nm = itemList.find('PGM_NM').string
    pgm_nm = '없음' if pgm_nm is None else pgm_nm
    target_nm = itemList.find('TARGET_NM').string
    target_nm = '없음' if target_nm is None else target_nm
    u_price = itemList.find('U_PRICE').string
    u_price = '없음' if u_price is None else u_price
    pjList.append((up_nm, pgm_nm, target_nm, u_price))

print('[ 서울 청소년 수련관 강좌 리스트 ]')
for up_nm,pgm_nm,target_nm,u_price in pjList :
    print(up_nm+','+pgm_nm+','+target_nm+','+str(u_price))
```


```python
from bs4 import BeautifulSoup
import urllib.request as req
import io

key = '796143536a756e69313134667752417a'
contentType = 'xml'
startIndex = '1'
endIndex = '100'
date = '20201001'

url = 'http://openapi.seoul.go.kr:8088/'+key+'/'+contentType+'/CardSubwayStatsNew/'+startIndex+'/'+endIndex+'/'+date+'/'
savename = 'C:/Temp/subway.xml'
req.urlretrieve(url, savename)

xml = open(savename, 'r', encoding='utf-8').read()
soup = BeautifulSoup(xml, 'xml')

subwayList = []
for itemList in soup.find_all('row') :
    line_num = itemList.find('LINE_NUM').string
    sub_sta_nm = itemList.find('SUB_STA_NM').string
    ride_pasgr_num = itemList.find('RIDE_PASGR_NUM').string
    alight_pasgr_num = itemList.find('ALIGHT_PASGR_NUM').string
    subwayList.append((line_num, sub_sta_nm, ride_pasgr_num, alight_pasgr_num))

print('[ 서울시 지하철호선별 역별 승하차 인원 정보 ]')
for line_num, sub_sta_nm, ride_pasgr_num, alight_pasgr_num in subwayList :
    print(line_num+','+sub_sta_nm+','+ride_pasgr_num+','+alight_pasgr_num)

```


```python
from bs4 import BeautifulSoup
import urllib.request as req
import io

key = '4WQ7X833TXC370SUTDX4'
contentType = 'xml'
startIndex = '1'
endIndex = '100'

url = 'http://ecos.bok.or.kr/api/KeyStatisticList/'+key+'/'+contentType+'/kr/'+startIndex+'/'+endIndex+'/'
savename = 'C:/Temp/ecos.xml'
req.urlretrieve(url, savename)

xml = open(savename, 'r', encoding='utf-8').read()
soup = BeautifulSoup(xml, 'xml')


ecoList = []
for itemList in soup.find_all('row') :
    class_name = itemList.find('CLASS_NAME').string
    class_name = '없음' if class_name is None else class_name
    keystat_name = itemList.find('KEYSTAT_NAME').string
    keystat_name = '없음' if keystat_name is None else keystat_name
    data_value = itemList.find('DATA_VALUE').string
    data_value = '없음' if data_value is None else data_value
    cycle = itemList.find('CYCLE').string
    cycle = '없음' if cycle is None else cycle
    unit_name = itemList.find('UNIT_NAME').string
    unit_name = '없음' if unit_name is None else unit_name
    ecoList.append((class_name, keystat_name, data_value, cycle, unit_name))

print('[ 100대 통계 지표 ]')
for class_name, keystat_name, data_value, cycle, unit_name in ecoList :
    print(class_name+','+keystat_name+','+data_value+','+cycle+','+unit_name)

```


```python
import urllib.request
import json

client_key = 'izGsqP2exeThwwEUVU3x'
client_secret = 'WrwbQ1l6ZI'

query = '치맥'
encText = urllib.parse.quote_plus(query)

num = 100
naver_url = 'https://openapi.naver.com/v1/search/blog.json?query=' + encText + '&display=' + str(num)

request = urllib.request.Request(naver_url)
request.add_header("X-Naver-Client-Id",client_key)
request.add_header("X-Naver-Client-Secret",client_secret)
response = urllib.request.urlopen(request)

rescode = response.getcode()

if(rescode == 200):
    response_body = response.read()
    dataList = json.loads(response_body)
    count = 1
    print('[' + query + '에 대한 네이버 블로그 글 ]')
    for data in dataList['items'] :
        print (str(count) + ' : ' + data['title'])
        print ('[' + data['description'] + ']')
        count += 1
else:
    print('오류 코드 : ' + rescode)

```


```python
import urllib.request
import json

client_key = 'izGsqP2exeThwwEUVU3x'
client_secret = 'WrwbQ1l6ZI'
query = '치맥'
encText = urllib.parse.quote_plus(query)

num = 100
naver_url = 'https://openapi.naver.com/v1/search/news.json?query=' + encText + '&display=' + str(num)

request = urllib.request.Request(naver_url)
request.add_header("X-Naver-Client-Id",client_key)
request.add_header("X-Naver-Client-Secret",client_secret)
response = urllib.request.urlopen(request)

rescode = response.getcode()

if(rescode == 200):
    response_body = response.read()
    dataList = json.loads(response_body)
    count = 1
    print('[' + query + '에 대한 네이버 뉴스 글 ]')
    for data in dataList['items'] :
        print (str(count) + ' : ' + data['title'])
        print ('[' + data['description'] + ']')
        count += 1
else:
    print('오류 코드 : ' + rescode)

```


```python
import tweepy

api_key = "RvnZeIl8ra88reu8fm23m0bST"
api_secret = "wTRylK94GK2KmhZUnqXonDaIszwAsS6VPvpSsIo6EX5GQLtzQo"
access_token = "959614462004117506-dkWyZaO8Bz3ZXh73rspWfc1sQz0EnDU"
access_token_secret = "rxDWfg7uz1yXMTDwijz0x90yWhDAnmOM15R6IgC8kmtTe"

auth = tweepy.OAuthHandler(api_key, api_secret)
auth.set_access_token(access_token, access_token_secret)

api = tweepy.API(auth)

keyword = '치맥'   
search = []   

cnt = 1
while(cnt <= 10):   
    tweets = api.search(q=keyword, count=100)
    for tweet in tweets :
        search.append(tweet)
    cnt += 1

data = {}   
i = 1   
print('[' + keyword + '에 대한 트윗 글 ]')    
for tweet in search:
    data['text'] = tweet.text   
    print(i, " : ", data)   
    i += 1
```



### - 실습

```python
from selenium import webdriver
from selenium.webdriver.common.keys import Keys 

driver = webdriver.Chrome('C:/Temp/chromedriver')
print("WebDriver 객체 : ", type(driver))
driver.get('https://www.naver.com/') 
target = driver.find_element_by_css_selector("#query")
print("찾아온 태그 객체 : ", type(target))
target.send_keys('파이썬')
target.send_keys(Keys.ENTER)
#driver.quit()
```

```python
from selenium import webdriver
import time
import re

driver = webdriver.Chrome('C:/Temp/chromedriver')
driver.get("https://hotel.naver.com/hotels/item?hotelId=hotel:Shilla_Stay_Yeoksam&destination_kor=%EC%8B%A0%EB%9D%BC%EC%8A%A4%ED%85%8C%EC%9D%B4%20%EC%97%AD%EC%82%BC&rooms=2")
time.sleep(2)

temp_list_all = []
page = 0
stopFlag = False

while True : 
    page += 1
    
    reviewList = driver.find_elements_by_css_selector('div.article_content > div > p')

    for review in reviewList :   
        temp_list_all.append(review.text.strip())
    print(str(page) + "page 적재")

    # 마지막 페이지이면 정지
    if stopFlag : break  
    linkNum = driver.find_element_by_css_selector('div.hotel_article_review.ng-isolate-scope > div.paginate.ng-scope > a.direction.next')
    # 다음 페이지로
    linkNum.click()
    time.sleep(1)
    # 중지를 위한 flag
    if linkNum.get_attribute('class') == 'direction next disabled' :
        stopFlag = True 
        
with open("c:/Temp/naverhotel.txt","w", encoding="utf-8") as f:
    for item in temp_list_all :
        if len(item) > 0 :
            f.write(str(item)+'\n')
```

