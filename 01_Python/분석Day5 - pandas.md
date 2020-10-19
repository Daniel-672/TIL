

# 분석Day05

>  데이터 수집 & pandas

### - 교육내용

```python

```



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

