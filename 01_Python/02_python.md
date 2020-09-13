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



### - keydown event로 SQLite쿼리해서 결과로 Dom객체 update

```HTML
<div class="form-group">
    <div><label for="nickName" style="margin-right:5px;">닉네임</label><img id="nickimg" style=" display: inline-block; vertical-align: sub;" width="18" src="/static/assets/img/iyes.png"/><span id="nickspan" style="margin-left:3px;color:green">사용가능</span></div>
    <input type="text" class="form-control" id="nickName"  placeholder="사용자 이름" name="nickName" required>
</div>
```

```javascript
jQuery('#nickName').on('input propertychange paste', function() {
    $.getJSON("{% url 'checknick' %}?nickname="+$('#nickName').val().trim(), function(jsonObj) {
        const domnickspan = $('#nickspan');
        const domnickimg = $('#nickimg');

        if (jsonObj.userable) {
            domnickspan.text("사용가능");
            domnickspan.css('color', 'green');
            domnickimg.attr("src", "/static/assets/img/iyes.png");
            document.getElementById("registersubmit").disabled = false;

        } else {
            domnickspan.text("사용중인 닉네임");
            domnickspan.css('color', 'red');
            domnickimg.attr("src", "/static/assets/img/ino.png");
            document.getElementById("registersubmit").disabled = true;
        }

    });
});
```

```python
def checknick(request):
        nickname = request.GET.get("nickname")
        try :
            user = Users.objects.get(nickName=nickname)
        except Users.DoesNotExist :
            userable = True
        else :
            userable = False

        jsonContent = {"userable" : userable}
        return JsonResponse( jsonContent, json_dumps_params={'ensure_ascii': False})
```

