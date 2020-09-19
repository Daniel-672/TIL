# tip들

### - kakao API키로 token받기

```python
#1. 카카오 가입하기 - REST API 키 발급 및 redirect_url등록 
#* REST API key -> <REST API key>
#* redirect_url -> http://localhost:8000/fordisapp/
#
#2. GET방식으로 API key와 redirect_url로 코드 받기
#* 실행
#https://kauth.kakao.com/oauth/authorize?client_id=<REST API key>&redirect_uri=http://localhost:8000/fordisapp/&response_type=code
#* 결과
#http://localhost:8000/fordisapp/?code=<코드>
#
#* 발급된 코드 값 -> <코드>
#
#3. POST방식으로 API key와 redirect_url, 그리고 code값으로 access_token 받기
#
def getaccesstoken(request):
    url = "https://kauth.kakao.com/oauth/token"         # 수정 X
    dataString = "grant_type=authorization_code"        # 수정 X
    dataString += "&client_id=" + "<REST API key>"       # 수정 O  API Key
    dataString += "&redirect_uri=http://localhost:8000/fordisapp/&code="   # 수정 O  redirect_url
    dataString += "<코드>"     # 수정 O  code값
    headers = {
        'Content-Type' : "application/x-www-form-urlencoded",
        'Cache-Control' : "no-cache",
    }
    reponse = requests.request("POST",url,data=dataString, headers=headers)
    access_token = json.loads(((reponse.text).encode('utf-8')))

    # access_token = dataString
    context = {'access_token': access_token}
    return render(request, 'getaccesstoken.html', context)

#* 결과 : token은 그냥 두면됨 이후에는 API를 넣고 사용
#access_token: {'access_token': '<token>', 'token_type': 'bearer', 'refresh_token': '<refresh token>', 'expires_in': 21599, 'refresh_token_expires_in': 5183999}
#
#
#4. 테스트 함수 이후 python에서 돌아감
import json
import requests

def getinfotest():

    result = getLatLng('서울 마포구 모래내로1길 20')

    match_first = result['documents'][0]['address']

    context = {'x': float(match_first['x']), 'y': float(match_first['y'])}
    return (context)


def getLatLng(addr):
    url = 'https://dapi.kakao.com/v2/local/search/address.json?query=' + addr
    headers = {"Authorization": "KakaoAK <REST API key>"}
    result = json.loads(str(requests.get(url, headers=headers).text))
    return result


print(getinfotest())
```



### - 주소를 위경도 변환

```python
import json
import requests

def gotaddress(addressList):
    conResult = []
    for add in addressList:
        try:
            result = getLatLng(add)
            match_first = result['documents'][0]['address']
        except:
            match_first = {'x': '999', 'y': '999'}      #주소가 이상하면 999로 셋팅
        context = {'address': add, 'x': float(match_first['x']), 'y': float(match_first['y'])}
        conResult.append(context)

    return (conResult)

def getLatLng(addr):
    url = 'https://dapi.kakao.com/v2/local/search/address.json?query=' + addr
    headers = {"Authorization": "KakaoAK ####accessess를 받은 REST API key###"}
    result = json.loads(str(requests.get(url, headers=headers).text))
    return result

########################## 아래 테스트 ##########################

orgAddressList = ['서울 마포구 모래내로1길 20',
               '서울시 중랑구 상봉동 101-1',
                '서울시 중랑구 상봉동 101-2',
                '서울시 중랑구 상봉동 101-3']

test = gotaddress(orgAddressList)

for chk in test:
    print(chk['address'], ',', chk['x'], ',', chk['y'])
```





