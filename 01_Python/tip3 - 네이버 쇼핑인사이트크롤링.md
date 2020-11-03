## *네이버 쇼핑인사이트*
> 1. 네이버 쇼핑 인사이트에서 상품평 코드 및 코드명을 추출하는 함수생성
2. 코드 추출 함수로 모든 코드 생성
3. 기간별 카테고리별 클릭율의 그래프값 추출 로직 작성
4. 기간별 카테고리별 Top500 인기검색어 추출 로직 작성 

### 1. 네이버 쇼핑 인사이트에서 상품평 코드 및 코드명을 추출하는 함수생성


```python
import urllib.request
import requests, json
from bs4 import BeautifulSoup
import pandas as pd

def findProductCode(parentsCode) :
    headers = {
                'accept-language' : 'ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7', 
                'referer' : 'https://datalab.naver.com/shoppingInsight/sCategory.naver', 
                'sec-fetch-dest' : 'empty', 
                'sec-fetch-mode' : 'cors', 
                'sec-fetch-site' : 'same-origin', 
                'user-agent' : 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/86.0.4240.111 Safari/537.36', 
                'x-requested-with' : 'XMLHttpRequest'
    }

    url = 'https://datalab.naver.com/shoppingInsight/getCategory.naver?cid=' + str(parentsCode)

    productpid = []
    productpname = []
    productcid = []
    productcname = []

    data = {'cid': str(parentsCode)}
    # print(url, data)
    
    req = urllib.request.Request(url, headers = headers)
    # print(req)
    data = urllib.request.urlopen(req).read()
    # print(data)
    # page = data.decode('utf-8', 'ignore')
    # print(page)
    res_content = json.loads(data)

    # print(res_content)
    # print('====================================')
    # print(res_content["childList"])
    # print('====================================')
    # print(str(res_content['cid']), res_content['name'])
    # print('====================================')
    # print(len(res_content["childList"]))
    # print('상위', str(res_content['cid']), res_content['name'])
    
    for i in range(len(res_content["childList"])) :
        # print('하위', str(i), res_content["childList"][i]['cid'], res_content["childList"][i]['name'])
        productpid.append(res_content['cid'])
        productpname.append(res_content['name'])
        productcid.append(res_content["childList"][i]['cid'])
        productcname.append(res_content["childList"][i]['name'])
        
    listSet = {'productpid' : productpid,
                'productpname' : productpname,
                'productcid' : productcid,
                'productcname' : productcname}
    df = pd.DataFrame(listSet)        
    return df

print(findProductCode(0))
```

### 2. 코드 추출 함수로 모든 코드 생성


```python
# 1분류코드 추출
L1 = findProductCode(0)
L1['Level'] = 'L1'
print(L1)

# 2분류코드 추출
L2 = pd.DataFrame()
for l in L1.productcid :
    L_temp = findProductCode(l)
    L2 = pd.concat([L2, L_temp])
L2['Level'] = 'L2'
print(L2)

# 3분류코드 추출
L3 = pd.DataFrame()
for l in L2.productcid :
    L_temp = findProductCode(l)
    L3 = pd.concat([L3, L_temp])
L3['Level'] = 'L3'
L3 = L3.astype({'productpid': 'int', 'productcid': 'int'})    # float로 바뀌걸 다시 수정
print(L3)

# 4분류코드 추출
L4 = pd.DataFrame()
for l in L3.productcid :   
    L_temp = findProductCode(l)
    L4 = pd.concat([L4, L_temp])
L4['Level'] = 'L4'

dfProductList = pd.concat([L1, L2, L3, L4], ignore_index=True)
dfProductList = dfProductList.astype({'productpid': 'int', 'productcid': 'int'})    # float로 바뀌걸 다시 수정
dfProductList = dfProductList.astype('str')
dfProductList.to_csv("C:/PyStexam/naverProductList.csv")
# display(dfProductList)
# 5003 rows × 5 columns
```


```python
# dfProductList.to_csv("C:/PyStexam/naverProductList.csv")
# display(dfProductList)
# dfProductList_ALL = dfProductList.merge(dfProductList, left_on='productcid', right_on='productpid', how='right' ).merge(dfProductList, left_on='productcid_x', right_on='productcid', how='right' )
# display(dfProductList.loc[0:0, ['Level', 'productcid', 'productcname']])

L4['Level'] = 'L4'

dfProductList = pd.concat([L1, L2, L3, L4], ignore_index=True)
dfProductList = dfProductList.astype({'productpid': 'int', 'productcid': 'int'})    # float로 바뀌걸 다시 수정
dfProductList = dfProductList.astype('str')
dfProductList.to_csv("C:/PyStexam/naverProductList.csv")




```

### 3. 기간별 카테고리별 클릭율의 그래프값 추출 로직 작성


```python
import requests, json
from bs4 import BeautifulSoup

def findTimeSeries(productcid, startDate = '2019-11-01', endDate = '2020-10-31') :
    headers = {
                'accept-language' : 'ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7', 
                'content-length' : '126', 
                'content-type' : 'application/x-www-form-urlencoded; charset=UTF-8', 
                #'cookie' : 'NNB=F33UBEC3XNJV4; NRTK=ag#all_gr#1_ma#-2_si#0_en#0_sp#0; IMAGE_BANNER_MAIL=2020-03-02%2010%3A30%3A56; ASID=5fdf49e800000170bad6415900000048; MM_NEW=1; NFS=2; MM_NOW_COACH=1; _ga_7VKFYR6RV1=GS1.1.1598839250.6.0.1598839250.60; NV_WETR_LOCATION_RGN_M="MDkyNjAxMDI="; NID_AUT=l5Ankb6kx33pzhNLNTB8Ny6iIdgDZ8YyHX1q1P1+fa9BlQIfrUiDkLMyj5LiT7Qo; NID_JKL=FYQTAL5vlP1Aj7iS0fz5dkNu07tvLAzVMyKke3MnhIM=; _fbp=fb.1.1600838941837.1886007518; _ga=GA1.1.1638948181.1583847344; _ga_4BKHBFKFK0=GS1.1.1600838941.1.1.1600839041.60; nx_ssl=2; NV_WETR_LAST_ACCESS_RGN_M="MDkyNjAxMDI="; BMR=s=1604124195035&r=https%3A%2F%2Fpost.naver.com%2Fviewer%2FpostView.nhn%3FvolumeNo%3D27125253%26memberNo%3D23871725%26vType%3DVERTICAL&r2=https%3A%2F%2Fsearch.naver.com%2Fsearch.naver%3Fwhere%3Dnexearch%26sm%3Dtop_hty%26fbm%3D1%26ie%3Dutf8%26query%3D%25ED%258C%258C%25EB%259E%2598%25EB%25AC%25B4%25EC%25B9%25A8; page_uid=UH9mjlprvmsssLTzGTZssssssDR-204565; _datalab_cid=50000006; NID_SES=AAABp/nCIpMQ8ayvFerNHCE3on/e1mxFFXMLKi85UXPDgMVnpwhi5RNmxXLCGEjebalewqKaXgevmYm7KbF+DJQIPkEwIg9y45KHsiNz3aeH3PnGYy3m8wNOPb5wfTjygtHNPncs1zMkBrahKhEt9FIWa3sHl46ekfVgnlgC88k2GgCVgLPYk9rpq9cwXSYS5GO09yan5BE1pJQ4C7/0iUBNDOO7XzA0WCcqIg9GbO6q/AbKRhQWyO8X0MWxbzEdOHdkFAOBv1hbyc1q4h/BYFlD40+dTcJAhBT9A9+D0k4+17Y3vMyozHZhz28wX7XbgdCc5OpFqBeTCJqoH/HzjZ59pVO5t2hd+cxWflcLJLfExQu2Aice8OzDqLajQpW2G0jC9IioKmyy3NZ0eUZr5bsJ2h1rB3i+b6CNY9Wn+mIMqY9+/xFljHWpaJo7jVAP6NvkzFfy8vzWCDQA6spfzFHe9hOtBoYTx4zATQf/r9EKVLJ2M19CLYzbabe6EmZRL94qW8RYMGBl1uhVaNNlUkAnHsRNgrkClZJr6F9zxV6ghWMkK+RyLwBsiXSq34cKEAlJHA==', 
                'origin' : 'https://datalab.naver.com', 
                'referer' : 'https://datalab.naver.com/shoppingInsight/sCategory.naver', 
                'sec-fetch-dest' : 'empty', 
                'sec-fetch-mode' : 'cors', 
                'sec-fetch-site' : 'same-origin', 
                'user-agent' : 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/86.0.4240.111 Safari/537.36', 
                'x-requested-with' : 'XMLHttpRequest'
    }

    url = 'https://datalab.naver.com/shoppingInsight/getCategoryClickTrend.naver'

    data = {
            'cid'       : productcid,
            'timeUnit'  : 'date',
            'startDate' : startDate,
            'endDate'   : endDate,
            'age'       : '10,20,30,40,50,60',
            'gender'    : 'f,m',
            'device'    : 'pc,mo'
            }

    res = requests.post(url, data = data, headers = headers)
    # print(res)
    soup = BeautifulSoup(res.content, 'html.parser')
    # print(soup)
    # print('-----------------------------')
    json_data = json.loads(soup.text)
    # print(json_data)
    # print(json_data['result'][0]['data'])
    # print(type(json_data['result']))

    productDate = []
    productvalue = []

    for i in range(len(json_data['result'][0]['data'])) :
        # print(json_data['result'][0]['data'][i]['period'], json_data['result'][0]['data'][i]['value'])
        productDate.append(json_data['result'][0]['data'][i]['period'])
        productvalue.append(json_data['result'][0]['data'][i]['value'])

    # print(productDate, productvalue)

    dataSet = { 'productDate' : productDate,
                'productcid' : productcid,
                'productvalue' : productvalue}
    df = pd.DataFrame(dataSet)        
    return df

##################### 추출 로직 #####################
prodList = dfProductList.loc[0:2, ['Level', 'productcid', 'productcname']]
# print(prodList)

productClickRate = pd.DataFrame()
for i in range(len(prodList)):
#     print(prodList.loc[i,'Level'])
#     print(prodList.loc[i,'productcid'])
#     print(prodList.loc[i,'productcname'])
    tmpList = findTimeSeries(prodList.loc[i,'productcid'])
    tmpList['Level'] = prodList.loc[i,'Level']
    tmpList['productcname'] = prodList.loc[i,'productcname']
    productClickRate= pd.concat([productClickRate, tmpList])

print(productClickRate)
    
```

### 4-1. 기간별 카테고리별 Top500 인기검색어 추출 로직 작성 -> 페이지별 20개씩 25번


```python
import requests, json
from bs4 import BeautifulSoup

headers = {
            'accept-language' : 'ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7', 
            'content-length' : '103', 
            'content-type' : 'application/x-www-form-urlencoded; charset=UTF-8', 
#            'cookie' : 'NNB=F33UBEC3XNJV4; NRTK=ag#all_gr#1_ma#-2_si#0_en#0_sp#0; IMAGE_BANNER_MAIL=2020-03-02%2010%3A30%3A56; ASID=5fdf49e800000170bad6415900000048; MM_NEW=1; NFS=2; MM_NOW_COACH=1; _ga_7VKFYR6RV1=GS1.1.1598839250.6.0.1598839250.60; NV_WETR_LOCATION_RGN_M="MDkyNjAxMDI="; NID_AUT=l5Ankb6kx33pzhNLNTB8Ny6iIdgDZ8YyHX1q1P1+fa9BlQIfrUiDkLMyj5LiT7Qo; NID_JKL=FYQTAL5vlP1Aj7iS0fz5dkNu07tvLAzVMyKke3MnhIM=; _fbp=fb.1.1600838941837.1886007518; _ga=GA1.1.1638948181.1583847344; _ga_4BKHBFKFK0=GS1.1.1600838941.1.1.1600839041.60; nx_ssl=2; NV_WETR_LAST_ACCESS_RGN_M="MDkyNjAxMDI="; BMR=s=1604124195035&r=https%3A%2F%2Fpost.naver.com%2Fviewer%2FpostView.nhn%3FvolumeNo%3D27125253%26memberNo%3D23871725%26vType%3DVERTICAL&r2=https%3A%2F%2Fsearch.naver.com%2Fsearch.naver%3Fwhere%3Dnexearch%26sm%3Dtop_hty%26fbm%3D1%26ie%3Dutf8%26query%3D%25ED%258C%258C%25EB%259E%2598%25EB%25AC%25B4%25EC%25B9%25A8; _datalab_cid=50000001; _naver_usersession_=pFQJ4wGs/6FIZ6mlsldz5Yz2; NID_SES=AAABqI87G+wQwHEmn8KI62gDJdRIg0+j0l3co2aAncehuz7MLdygUxokQbURBzCDiwES/tRn+JJkQmuHBt2peYBEW+ehm0haA0LT4zgQ3W9Gkup2rdGlYAAuOBb5rMbWZCv2ZbFa+y0XqWy2wK3kFDzL8ObDuBWtqbPyLCVQ0JiIgL+Ji0NgVxkCrkIrnwBQuK8IF0pYP734DpEQmCzMXZmE2ltHxRZh4E4pKIkjiV0kP/Watv2mjToSfbapG8Z4fzGw9JAUeXHefDadwAX50q6j0QrgRKqyni/GL8WefHIuMIZsuqgd/MQmeuTTaacFDnt43avu1lemkumEGSBTvehUIoK3Diruqg2ZTreo1m2hKWj1jjUmHECF6fHHKXmB+msVfvo+Ps0GUjQYPywPNvdusYKbDc1ZNKJW7Or017OBef4MfCsxW99NGuNjZs/NYc/mm/kzvR5HVjINgMWiE6cCdpb/Fr7jPPfiXKeHAI+uQbfs8lWeDSOBoObps8LQqtY7KMVS4KTDKeJ+vqdy67+hzePcMbeEdne5DtR6sq5CZvN7lWtWTufTqwvVjtagIb7Etw==; page_uid=UH9mjlprvmsssLTzGTZssssssDR-204565', 
            'origin' : 'https://datalab.naver.com', 
            'referer' : 'https://datalab.naver.com/shoppingInsight/sCategory.naver', 
            'sec-fetch-dest' : 'empty', 
            'sec-fetch-mode' : 'cors', 
            'sec-fetch-site' : 'same-origin', 
            'user-agent' : 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/86.0.4240.111 Safari/537.36', 
            'x-requested-with' : 'XMLHttpRequest'
}

url = 'https://datalab.naver.com/shoppingInsight/getCategoryKeywordRank.naver'

productRank = []
productName = []

for page in range(1, 26) :
    data = {
            'cid'       : '50000001',
            'timeUnit'  : 'date',
            'startDate' : '2020-10-01',
            'endDate'   : '2020-11-01',
            'age'       : '10,20,30,40,50,60',
            'gender'    : 'f,m',
            'device'    : 'pc,mo',
            'page'      :  page,
            'count'     : '20',
            }

    res = requests.post(url, data=data, headers = headers)

    soup = BeautifulSoup(res.content, 'html.parser')
    # print(soup)
    # print('-----------------------------')
    json_data = json.loads(soup.text)
    # print(json_data['ranks'])
    # print(type(json_data['ranks']))
    
    
    for i in range(len(json_data['ranks'])) :
        print(json_data['ranks'][i]['rank'], json_data['ranks'][i]['keyword'])
        productRank.append(json_data['ranks'][i]['rank'])
        productName.append(json_data['ranks'][i]['keyword'])

# print(productRank, productName)

```

### 4-2. 기간별 카테고리별 Top500 인기검색어 추출 로직 작성 -> 한방에 Top 500


```python
import requests, json
from bs4 import BeautifulSoup

headers = {
            'accept-language' : 'ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7', 
            'content-length' : '103', 
            'content-type' : 'application/x-www-form-urlencoded; charset=UTF-8', 
#            'cookie' : 'NNB=F33UBEC3XNJV4; NRTK=ag#all_gr#1_ma#-2_si#0_en#0_sp#0; IMAGE_BANNER_MAIL=2020-03-02%2010%3A30%3A56; ASID=5fdf49e800000170bad6415900000048; MM_NEW=1; NFS=2; MM_NOW_COACH=1; _ga_7VKFYR6RV1=GS1.1.1598839250.6.0.1598839250.60; NV_WETR_LOCATION_RGN_M="MDkyNjAxMDI="; NID_AUT=l5Ankb6kx33pzhNLNTB8Ny6iIdgDZ8YyHX1q1P1+fa9BlQIfrUiDkLMyj5LiT7Qo; NID_JKL=FYQTAL5vlP1Aj7iS0fz5dkNu07tvLAzVMyKke3MnhIM=; _fbp=fb.1.1600838941837.1886007518; _ga=GA1.1.1638948181.1583847344; _ga_4BKHBFKFK0=GS1.1.1600838941.1.1.1600839041.60; nx_ssl=2; NV_WETR_LAST_ACCESS_RGN_M="MDkyNjAxMDI="; BMR=s=1604124195035&r=https%3A%2F%2Fpost.naver.com%2Fviewer%2FpostView.nhn%3FvolumeNo%3D27125253%26memberNo%3D23871725%26vType%3DVERTICAL&r2=https%3A%2F%2Fsearch.naver.com%2Fsearch.naver%3Fwhere%3Dnexearch%26sm%3Dtop_hty%26fbm%3D1%26ie%3Dutf8%26query%3D%25ED%258C%258C%25EB%259E%2598%25EB%25AC%25B4%25EC%25B9%25A8; _datalab_cid=50000001; _naver_usersession_=pFQJ4wGs/6FIZ6mlsldz5Yz2; NID_SES=AAABqI87G+wQwHEmn8KI62gDJdRIg0+j0l3co2aAncehuz7MLdygUxokQbURBzCDiwES/tRn+JJkQmuHBt2peYBEW+ehm0haA0LT4zgQ3W9Gkup2rdGlYAAuOBb5rMbWZCv2ZbFa+y0XqWy2wK3kFDzL8ObDuBWtqbPyLCVQ0JiIgL+Ji0NgVxkCrkIrnwBQuK8IF0pYP734DpEQmCzMXZmE2ltHxRZh4E4pKIkjiV0kP/Watv2mjToSfbapG8Z4fzGw9JAUeXHefDadwAX50q6j0QrgRKqyni/GL8WefHIuMIZsuqgd/MQmeuTTaacFDnt43avu1lemkumEGSBTvehUIoK3Diruqg2ZTreo1m2hKWj1jjUmHECF6fHHKXmB+msVfvo+Ps0GUjQYPywPNvdusYKbDc1ZNKJW7Or017OBef4MfCsxW99NGuNjZs/NYc/mm/kzvR5HVjINgMWiE6cCdpb/Fr7jPPfiXKeHAI+uQbfs8lWeDSOBoObps8LQqtY7KMVS4KTDKeJ+vqdy67+hzePcMbeEdne5DtR6sq5CZvN7lWtWTufTqwvVjtagIb7Etw==; page_uid=UH9mjlprvmsssLTzGTZssssssDR-204565', 
            'origin' : 'https://datalab.naver.com', 
            'referer' : 'https://datalab.naver.com/shoppingInsight/sCategory.naver', 
            'sec-fetch-dest' : 'empty', 
            'sec-fetch-mode' : 'cors', 
            'sec-fetch-site' : 'same-origin', 
            'user-agent' : 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/86.0.4240.111 Safari/537.36', 
            'x-requested-with' : 'XMLHttpRequest'
}

url = 'https://datalab.naver.com/shoppingInsight/getCategoryKeywordRank.naver'

productRank = []
productName = []


data = {
        'cid'       : '50000001',
        'timeUnit'  : 'date',
        'startDate' : '2020-10-01',
        'endDate'   : '2020-11-01',
        'age'       : '10,20,30,40,50,60',
        'gender'    : 'f,m',
        'device'    : 'pc,mo',
        'page'      :  1,
        'count'     : '500',    # 한방에 Top500
        }

res = requests.post(url, data=data, headers = headers)

soup = BeautifulSoup(res.content, 'html.parser')
# print(soup)
# print('-----------------------------')
json_data = json.loads(soup.text)
# print(json_data['ranks'])
# print(type(json_data['ranks']))


for i in range(len(json_data['ranks'])) :
    print(json_data['ranks'][i]['rank'], json_data['ranks'][i]['keyword'])
    productRank.append(json_data['ranks'][i]['rank'])
    productName.append(json_data['ranks'][i]['keyword'])

# print(productRank, productName)

```
