

# Day14

>  데이터 수집

### - 교육내용

```python
stname = "유니코"; stage=20; stavg=95.869
print(stname+"학생은 나이가 "+str(stage)+"이고 평균은 "+str(stavg)+"입니다")
print(stname, "학생은 나이가 ", stage, "이고 평균은 ", stavg, "입니다", sep="")
print("%s학생은 나이가 %d이고 평균은 %.2f입니다" % (stname, stage, stavg))
print("{}학생은 나이가 {}이고 평균은 {:.2f}입니다".format(stname, stage, stavg))
print(f"{stname}학생은 나이가 {stage}이고 평균은 {stavg:.2f}입니다")
```


```python
v1 = stname+"학생은 나이가 "+str(stage)+"이고 평균은 "+str(stavg)+"입니다"
v2 = "%s학생은 나이가 %d이고 평균은 %.2f입니다" % (stname, stage, stavg)
v3 = "{}학생은 나이가 {}이고 평균은 {:.2f}입니다".format(stname, stage, stavg)
v4 = f"{stname}학생은 나이가 {stage}이고 평균은 {stavg:.2f}입니다"
print(v1)
print(v2)
print(v3)
print(v4)
```


```python
import sys
print(sys.version)
```


```python
import os
print(os.getcwd())
```

    c:\PyStexam



```python
!jupyter kernelspec list
```


```python
!dir
```

     C 드라이브의 볼륨에는 이름이 없습니다.
     볼륨 일련 번호: B6D4-3AF0
    
     c:\PyStexam 디렉터리
    
    2020-10-14  오후 01:09    <DIR>          .
    2020-10-14  오후 01:09    <DIR>          ..
    2020-10-14  오전 10:43    <DIR>          .ipynb_checkpoints
    2020-10-14  오후 01:09            30,927 exam1.ipynb
    2020-10-14  오후 01:07             1,862 test.ipynb
                   2개 파일              32,789 바이트
                   3개 디렉터리  77,910,646,784 바이트 남음



```python
import urllib.request
res = urllib.request.urlopen("http://www.naver.com/")
print(type(res))
print(res.status)
print(res.version)
print(res.msg)
res_header = res.getheaders()
print("[ header 정보 ]----------")
for s in res_header :
    print(s)
```

    <class 'http.client.HTTPResponse'>
    200
    11
    OK
    [ header 정보 ]----------
    ('Server', 'NWS')
    ('Date', 'Wed, 14 Oct 2020 01:59:24 GMT')
    ('Content-Type', 'text/html; charset=UTF-8')
    ('Transfer-Encoding', 'chunked')
    ('Connection', 'close')
    ('Set-Cookie', 'PM_CK_loc=40ae94d20ae3b96716d9b18600847aee8665678b3a66eba699d0d1ac0bd4662a; Expires=Thu, 15 Oct 2020 01:59:24 GMT; Path=/; HttpOnly')
    ('Cache-Control', 'no-cache, no-store, must-revalidate')
    ('Pragma', 'no-cache')
    ('P3P', 'CP="CAO DSP CURa ADMa TAIa PSAa OUR LAW STP PHY ONL UNI PUR FIN COM NAV INT DEM STA PRE"')
    ('X-Frame-Options', 'DENY')
    ('X-XSS-Protection', '1; mode=block')
    ('Strict-Transport-Security', 'max-age=63072000; includeSubdomains')
    ('Referrer-Policy', 'unsafe-url')



```python
import urllib.request
res = urllib.request.urlopen("http://unico2013.dothome.co.kr/crawling/tagstyle.html")
print(res)
print("[ header 정보 ]----------")
res_header = res.getheaders()
for s in res_header :
    print(s)
print("[ body 내용 ]-----------")
print(res.read())
#print(res.read().decode('utf-8'))

```


```python
import urllib.request
print("===========================================================")
url = 'https://www.python.org/'
f = urllib.request.urlopen(url)
print(type(f))
print(type(f.info()))
encoding = f.info().get_content_charset()
print(url, ' 페이지의 인코딩 정보 :', encoding)
text = f.read(500).decode(encoding)
print(text)
print("===========================================================")

url = 'https://www.daum.net/'
f = urllib.request.urlopen(url)
encoding = f.info().get_content_charset()
print(url, ' 페이지의 인코딩 정보 :', encoding)
text = f.read(500).decode(encoding)
print(text)
print("===========================================================")

url = 'https://www.aladin.co.kr/home/welcome.aspx'
f = urllib.request.urlopen(url)
encoding = f.info().get_content_charset()
print(url, ' 페이지의 인코딩 정보 :', encoding)

text = f.read(500).decode(encoding)
print(text)
print("===========================================================")
```

    ===========================================================
    <class 'http.client.HTTPResponse'>
    <class 'http.client.HTTPMessage'>
    https://www.python.org/  페이지의 인코딩 정보 : utf-8
    <!doctype html>
    <!--[if lt IE 7]>   <html class="no-js ie6 lt-ie7 lt-ie8 lt-ie9">   <![endif]-->
    <!--[if IE 7]>      <html class="no-js ie7 lt-ie8 lt-ie9">          <![endif]-->
    <!--[if IE 8]>      <html class="no-js ie8 lt-ie9">                 <![endif]-->
    <!--[if gt IE 8]><!--><html class="no-js" lang="en" dir="ltr">  <!--<![endif]-->
    
    <head>
        <meta charset="utf-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
    
        <link rel="prefetch" href="//ajax.googleapis.com/ajax/libs/jqu
    ===========================================================
    https://www.daum.net/  페이지의 인코딩 정보 : utf-8
    <!DOCTYPE html>
    <html lang="ko" class="">
    <head>
    <meta charset="utf-8"/>
    <title>Daum</title>
    <meta property="og:url" content="https://www.daum.net/">
    <meta property="og:type" content="website">
    <meta property="og:title" content="Daum">
    <meta property="og:image" content="//i1.daumcdn.net/svc/image/U03/common_icon/5587C4E4012FCD0001">
    <meta property="og:description" content="나의 관심 콘텐츠를 가장 즐겁게 볼 수 있는 Daum">
    <meta name="msapplication-task" content="name=Daum;action-
    ===========================================================
    https://www.aladin.co.kr/home/welcome.aspx  페이지의 인코딩 정보 : utf-8
    
    <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.0 Transitional//EN" >
    <html>
      <head>    
          <title id="Title">알라딘</title>
          <meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
    	  <meta content="Microsoft Visual Studio .NET 7.1" name="GENERATOR">
    	  <meta content="C#" name="CODE_LANGUAGE">
    	  <meta content="JavaScript" name="vs_defaultClientScript">
    	  <meta content="http://schemas.microsoft.com/intellisense/ie5" name="vs_targetSchema">
          <meta http-equiv="
    ===========================================================



```python
from urllib.parse import urlparse
from urllib.parse import urlencode
print("[ URL 문자열 정보 추출 1 ]")
url1 = urlparse('https://movie.daum.net/moviedb/main?movieId=93252')
print("타입정보 : ",type(url1))
print("도메인정보 : ",url1.netloc) 
print("패스정보 : ",url1.path)
print("쿼리정보 : ",url1.query) 
print("스킴정보 : ",url1.scheme)
print("포트정보 : ",url1.port)
print("프래그먼트정보 : ",url1.fragment)
print("URL 문자열정보 : ",url1.geturl())
print("urllib.parse.ParseResult 객체정보 : ",url1)
print("\n[ URL 문자열 정보 추출 2 ]")
url2 = urlparse('https://docs.python.org/3/library/urllib.parse.html#urlparse-result-object')
print("도메인정보 : ",url2.netloc) 
print("패스정보 : ", url2.path)  
print("쿼리정보 : ",url2.query)
print("스킴정보 : ",url2.scheme)
print("포트정보 : ",url2.port)
print("프래그먼트정보 : ",url2.fragment)
print("URL 문자열정보 : ",url2.geturl())
print("urllib.parse.ParseResult 객체정보 : ",url2)

print("\n[ Query문자열 또는 요청 파라미터 인코딩 ]")
params1 = urlencode({'number': 12524, 'type': 'issue', 'action': 'show'})
print(params1)
params2 = urlencode({'addr': '서울시 강남구 역삼동'})
print(params2)
```


```python
import urllib.request
import urllib.parse
params = urllib.parse.urlencode({'name': '유니코', 'age': 10})
print("URL 인코딩 규칙이 적용된 문자열 : %s" % params)
url = "http://unico2013.dothome.co.kr/crawling/get.php?%s" % params
print(url)
with urllib.request.urlopen(url) as f:
    print(f.read().decode('utf-8'))
```

    URL 인코딩 규칙이 적용된 문자열 : name=%EC%9C%A0%EB%8B%88%EC%BD%94&age=10
    http://unico2013.dothome.co.kr/crawling/get.php?name=%EC%9C%A0%EB%8B%88%EC%BD%94&age=10
    ﻿<!DOCTYPE html>
    <html>
      <head>
        <meta charset="utf-8">
        <title>POST TEST</title>
      </head>
      <body>
       <h1>GET : 이름은 유니코이고 나이는 10이네요!!</h1>   </body>
    </html>



```python
import urllib.request
import urllib.parse
data = urllib.parse.urlencode({'name': '유니코', 'age': 10})
print("URL 인코딩 규칙이 적용된 문자열 : %s" % data)
postdata = data.encode('ascii')
print("변환된 바이트 문자열 : %s" % postdata)
url = "http://unico2013.dothome.co.kr/crawling/post.php"
with urllib.request.urlopen(url, postdata) as f:
    print(f.read().decode('utf-8'))
```

    URL 인코딩 규칙이 적용된 문자열 : name=%EC%9C%A0%EB%8B%88%EC%BD%94&age=10
    변환된 바이트 문자열 : b'name=%EC%9C%A0%EB%8B%88%EC%BD%94&age=10'
    ﻿<!DOCTYPE html>
    <html>
      <head>
        <meta charset="utf-8">
        <title>POST TEST</title>
      </head>
      <body>
       <h1>POST : 이름은 유니코이고 나이는 10이네요!!</h1>   </body>
    </html>



```python
import urllib.request
import urllib.parse
data = urllib.parse.urlencode({'name': '유니코', 'age': 10})
postdata = data.encode('ascii')
req = urllib.request.Request(url='http://unico2013.dothome.co.kr/crawling/post.php',
            data=postdata)
print(req)
with urllib.request.urlopen(req) as f:
    print(f.read().decode('utf-8'))
```

    <urllib.request.Request object at 0x00000235EA813188>
    ﻿<!DOCTYPE html>
    <html>
      <head>
        <meta charset="utf-8">
        <title>POST TEST</title>
      </head>
      <body>
       <h1>POST : 이름은 유니코이고 나이는 10이네요!!</h1>   </body>
    </html>



```python
import requests

r = requests.request('get', 'http://unico2013.dothome.co.kr/crawling/exam.html')
r.encoding = 'utf-8'
print(type(r))
if r.text :
    print(r.text)
else :
    print('응답된 콘텐츠가 없어요')
print('----------------------------------------------------------')
r = requests.request('head', 'http://unico2013.dothome.co.kr/crawling/exam.html')
r.encoding = 'utf-8'
print(type(r))
if r.text :
    print(r.text)
else :
    print('응답된 콘텐츠가 없어요')
print('----------------------------------------------------------')
r = requests.request('post', 'http://unico2013.dothome.co.kr/crawling/post.php', data= {'name':'백도', 'age' : 12})
r.encoding = 'utf-8'
print(type(r))
if r.text :
    print(r.text)
else :
    print('응답된 콘텐츠가 없어요')

```

    <class 'requests.models.Response'>
    <!DOCTYPE html>
    <html>
    <head>
    <meta charset="UTF-8">
    <title>테스트</title>
    </head>
    <body>
    <h1>웹 크롤링을 테스트 합니다.</h1>
    </body>
    </html>
    ----------------------------------------------------------
    <class 'requests.models.Response'>
    응답된 콘텐츠가 없어요
    ----------------------------------------------------------
    <class 'requests.models.Response'>
    ﻿<!DOCTYPE html>
    <html>
      <head>
        <meta charset="utf-8">
        <title>POST TEST</title>
      </head>
      <body>
       <h1>POST : 이름은 백도이고 나이는 12이네요!!</h1>   </body>
    </html>



```python
import requests

r = requests.get('http://unico2013.dothome.co.kr/crawling/exam.html')
r.encoding = 'utf-8'
print(type(r))
print(r.headers)
if r.text :
    print(r.text)
else :
    print('응답된 콘텐츠가 없어요')
```


```python
import requests

r = requests.head('http://unico2013.dothome.co.kr/crawling/exam.html')
print(type(r))
print(r.headers)
if r.text :
    print(r.text)
else :
    print('응답된 콘텐츠가 없어요')
```


```python
import requests

dicdata = {'key1': 'value1', 'key2': 'value2'}
urlstr = 'http://unico2013.dothome.co.kr/crawling/get.php'
r = requests.get(urlstr, params=dicdata)
print(r.url)
print('------------------------------------')
dicdata = {'key1': 'value1', 'key2': ['value2', 'value3']}
r = requests.request('GET', urlstr, params=dicdata)
print(r.url)
print('------------------------------------')
tupledata = [('key1', 'value1'), ('key1', 'value2')]
r = requests.get(urlstr, params=tupledata)
print(r.url)
```

    http://unico2013.dothome.co.kr/crawling/get.php?key1=value1&key2=value2
    ------------------------------------
    http://unico2013.dothome.co.kr/crawling/get.php?key1=value1&key2=value2&key2=value3
    ------------------------------------
    http://unico2013.dothome.co.kr/crawling/get.php?key1=value1&key1=value2



```python
import requests

urlstr = 'http://unico2013.dothome.co.kr/crawling/get.php'
r = requests.get(urlstr)
print(r.text)
print('------------------------------------')
r.encoding = 'utf-8'
print(r.text)
print('------------------------------------')
print(r.content)
print('------------------------------------')
print(r.content.decode('utf-8'))
```

    ï»¿<!DOCTYPE html>
    <html>
      <head>
        <meta charset="utf-8">
        <title>POST TEST</title>
      </head>
      <body>
       <h1>GET : ì´ë¦ê³¼ ëì´ë¥¼ ì ë¬í´ ì£¼ì¸ì!!</h1>   </body>
    </html>
    ------------------------------------
    ﻿<!DOCTYPE html>
    <html>
      <head>
        <meta charset="utf-8">
        <title>POST TEST</title>
      </head>
      <body>
       <h1>GET : 이름과 나이를 전달해 주세요!!</h1>   </body>
    </html>
    ------------------------------------
    b'\xef\xbb\xbf<!DOCTYPE html>\r\n<html>\r\n  <head>\r\n    <meta charset="utf-8">\r\n    <title>POST TEST</title>\r\n  </head>\r\n  <body>\r\n   <h1>GET : \xec\x9d\xb4\xeb\xa6\x84\xea\xb3\xbc \xeb\x82\x98\xec\x9d\xb4\xeb\xa5\xbc \xec\xa0\x84\xeb\x8b\xac\xed\x95\xb4 \xec\xa3\xbc\xec\x84\xb8\xec\x9a\x94!!</h1>   </body>\r\n</html>'
    ------------------------------------
    ﻿<!DOCTYPE html>
    <html>
      <head>
        <meta charset="utf-8">
        <title>POST TEST</title>
      </head>
      <body>
       <h1>GET : 이름과 나이를 전달해 주세요!!</h1>   </body>
    </html>



```python
import requests
from PIL import Image
from io import BytesIO

r = requests.get('http://unico2013.dothome.co.kr/image/flower.jpg')
i = Image.open(BytesIO(r.content))
print(i)
print(type(i))
i.save("c:/Temp/test.jpg")
```

    <PIL.JpegImagePlugin.JpegImageFile image mode=RGB size=1280x853 at 0x235EA771948>
    <class 'PIL.JpegImagePlugin.JpegImageFile'>



```python
html_doc = """
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>Test BeautifulSoup</title>
    </head>
    <body>
        <h1>테스트</h1>
    </body>
</html> """
from bs4 import BeautifulSoup
bs = BeautifulSoup(html_doc, 'html.parser')
print(type(bs))
```

    <class 'bs4.BeautifulSoup'>



```python
html_doc = """
<!DOCTYPE html>
<html>
     <head>
          <meta charset='utf-8'>
          <title>Test BeautifulSoup</title>
     </head>
     <body>
          <p align="center">P태그의 컨텐트</p>
          <img src="http://unico2013.dothome.co.kr/image/flower.jpg" width="300">
     </body>
</html> """
from bs4 import BeautifulSoup
bs = BeautifulSoup(html_doc, 'html.parser')
print(bs.prettify())
```

    <!DOCTYPE html>
    <html>
     <head>
      <meta charset="utf-8"/>
      <title>
       Test BeautifulSoup
      </title>
     </head>
     <body>
      <p align="center">
       P태그의 컨텐트
      </p>
      <img src="http://unico2013.dothome.co.kr/image/flower.jpg" width="300"/>
     </body>
    </html>


​    


```python
html_doc = """
<!DOCTYPE html>
<html>
     <head>
          <meta charset='utf-8'>
          <title>Test BeautifulSoup</title>
     </head>
     <body>
          <p align="center">P태그의 컨텐트</p>
          <img src="http://unico2013.dothome.co.kr/image/flower.jpg" width="300">
          <ul>
               <li>테스트1<strong>강조</strong></li>
               <li>테스트2</li>
               <li>테스트3</li>
          </ul>
     </body>
</html> """
from bs4 import BeautifulSoup
bs = BeautifulSoup(html_doc, 'html.parser')
print(type(bs.title), ':', bs.title)
print(type(bs.title.name), ':', bs.title.name)
print(type(bs.title.string), ':', bs.title.string)
print('-------------------------')
print(type(bs.p['align']), ':', bs.p['align'])
print(type(bs.img['src']), ':', bs.img['src'])
print(type(bs.img.attrs), ':', bs.img.attrs)
```


```python
html_doc = """
<!DOCTYPE html>
<html>
     <head>
          <meta charset='utf-8'>
          <title>Test BeautifulSoup</title>
     </head>
     <body>
          <p align="center">P태그의 컨텐트</p>
          <img src="http://unico2013.dothome.co.kr/image/flower.jpg" width="300">
          <ul>
               <li>테스트1<strong>강조</strong></li>
               <li>테스트2</li>
               <li>테스트3</li>
          </ul>
     </body>
</html> """
from bs4 import BeautifulSoup
bs = BeautifulSoup(html_doc, 'html.parser')
print("[ string 속성 ]")
print(type(bs.p.string), ':', bs.p.string)
print(type(bs.ul.string), ':', bs.ul.string)
print(type(bs.ul.li.string), ':', bs.ul.li.string)
print(type(bs.ul.li.strong.string), ':', bs.ul.li.strong.string)
print("[ text 속성 ]")
print(type(bs.p.text), ':', bs.p.text)
print(type(bs.ul.text), ':', bs.ul.string)
print(type(bs.ul.li.text), ':', bs.ul.li.text)
print(type(bs.ul.li.strong.text), ':', bs.ul.li.strong.text)
print("[ contents 속성 ]")
print(type(bs.p.contents), ':', bs.p.contents)
print(type(bs.ul.contents), ':', bs.ul.string)
print(type(bs.ul.li.contents), ':', bs.ul.li.contents)
print(type(bs.ul.li.strong.contents), ':', bs.ul.li.strong.contents)
```

    [ string 속성 ]
    <class 'bs4.element.NavigableString'> : P태그의 컨텐트
    <class 'NoneType'> : None
    <class 'NoneType'> : None
    <class 'bs4.element.NavigableString'> : 강조
    [ text 속성 ]
    <class 'str'> : P태그의 컨텐트
    <class 'str'> : None
    <class 'str'> : 테스트1강조
    <class 'str'> : 강조
    [ contents 속성 ]
    <class 'list'> : ['P태그의 컨텐트']
    <class 'list'> : None
    <class 'list'> : ['테스트1', <strong>강조</strong>]
    <class 'list'> : ['강조']



```python
html_doc="""
<!DOCTYPE html>
<html>
  <head>
     <meta charset='utf-8'>
     <title>Test BeautifulSoup</title>
  </head>
  <body>
     <p align="center"> text contents </p>
     <p align="right">  text contents 2 </p>
     <p align="left">   text contents 3 </p>
     <img src="http://unico2013.dothome.co.kr/image/flower.jpg" width="500">
     <div>
       <p>text contents 4</p> 
     </div>
  </body>
</html> """

from bs4 import BeautifulSoup
bs = BeautifulSoup(html_doc, 'html.parser')
print(type(bs.find('p')))
print(type(bs.find_all('p')))
print("---------------------------------")
print(bs.find('title'))
print(bs.find('p'))
print(bs.find('img'))
print("---------------------------------")
ptags = bs.find_all('p')
print(ptags)
print("----------------")
for tag in ptags :
    print(tag)
```

    <class 'bs4.element.Tag'>
    <class 'bs4.element.ResultSet'>
    ---------------------------------
    <title>Test BeautifulSoup</title>
    <p align="center"> text contents </p>
    <img src="http://unico2013.dothome.co.kr/image/flower.jpg" width="500"/>
    ---------------------------------
    [<p align="center"> text contents </p>, <p align="right">  text contents 2 </p>, <p align="left">   text contents 3 </p>, <p>text contents 4</p>]
    ----------------
    <p align="center"> text contents </p>
    <p align="right">  text contents 2 </p>
    <p align="left">   text contents 3 </p>
    <p>text contents 4</p>



```python
html="""
<!DOCTYPE html>
<html>
  <head>
     <meta charset='utf-8'>
     <title>Test BeautifulSoup</title>
  </head>
  <body>
     <p align="center"> text contents </p>
     <p align="right" class="myp">  text contents 2 </p>
     <p align="left" a="b">   text contents 3 </p>
     <img src="http://unico2013.dothome.co.kr/image/flower.jpg" width="500">
  </body>
</html> """

from bs4 import BeautifulSoup
bs = BeautifulSoup(html, 'html.parser')
print(bs.find('p', align="center"))
print(bs.find('p', class_="myp"))
print(bs.find('p', align="left"))
print("-------------------------------------")
print(bs.find('p', attrs={"align":"center"}))
print(bs.find('p', attrs={"align":"right", "class":"myp"}))
print(bs.find('p', attrs={"align":"left"}))
```


```python
import requests
from bs4 import BeautifulSoup

req = requests.get('http://unico2013.dothome.co.kr/crawling/exercise_css.html')
html = req.content
print(type(html))
html = html.decode('utf-8')
#print(html)
print("==============================")
bs = BeautifulSoup(html, 'html.parser')
title = bs.select('h1')
title1 = bs.select('#f_subtitle')
title2 = bs.select('.subtitle')
title3 = bs.select('aside > h2')
img = bs.select('[src]')
print(type(title))
print(type(title[0]))
print("<h1>태그의 갯수 : %d " %len(title))
print("f_subtitle이라는 id 속성을 갖는 태그 갯수 : %d " %len(title1))
print("subtitle이라는 class 속성을 갖는 태그 갯수 : %d " %len(title2))
print("aside 태그의 <h2> 자식 태그 갯수 : %d " %len(title3))
print("src 속성을 갖는 태그 갯수 : %d " %len(img))

for content in title:
    print(content.string)
print("------------------------------")
for content in title1:
    print(content.text)
print("------------------------------")
for content in title2:
    print(content.text)
print("------------------------------")
for content in title3:
    print(content.text)
print("------------------------------")
for content in img:
   print(content["src"])
```


```python
import requests
from bs4 import BeautifulSoup
import re
req = requests.get('http://movie.naver.com/movie/point/af/list.nhn?page=1')
html = req.text
soup = BeautifulSoup(html, 'html.parser')
titles = soup.select('.movie')
points = soup.select('td.title > div > em')
reviews = soup.select('td.title')
movie_title = []
movie_point = []
movie_review = [] 

for dom in titles:
    movie_title.append(dom.text)
for dom in points:
    movie_point.append(dom.text)
for dom in reviews:
    content = dom.contents[6] 
    content=re.sub("신고", '', content)
    content=re.sub("[\n\t]", '', content)    
    movie_review.append(content)
commentLength = len(movie_title)   
for i in range(commentLength):
    print("영화 제목 : " + movie_title[i])
    print("평점 : " + movie_point[i])
    print("리뷰글 : " + movie_review[i])
    print("-----------------------------------------")   

```


```python
import requests
from bs4 import BeautifulSoup
import re
for n in range(1,31):
    req = requests.get('http://movie.naver.com/movie/point/af/list.nhn?page='+str(n))
    html = req.text
    soup = BeautifulSoup(html, 'html.parser')
    titles = soup.select('.movie' )
    points = soup.select('td.title > div > em')
    reviews = soup.select('td.title')
    movie_title = []
    movie_point = []
    movie_review = [] 
    for dom in titles:
        movie_title.append(dom.text)
    for dom in points:
        movie_point.append(dom.text)
    for dom in reviews:
        content = dom.contents[6]
        content=re.sub("신고", '', content)
        content=re.sub("[\n\t]", '', content)
        movie_review.append(content)

    commentLength = len(movie_title)   
    for i in range(commentLength):
        print(movie_point[i] + "\t"+movie_title[i]+"\t"+movie_review[i])
    print("-----------------------------------------------------")

```


```python
#파일명 : exam5_3.py
import urllib.request
from bs4 import BeautifulSoup
data = urllib.request.urlopen('https://comic.naver.com/genre/bestChallenge.nhn')
bs = BeautifulSoup(data, 'html.parser')
title = []
summary = []
rating = []
titleList = bs.select('.challengeTitle > a')
for titleDom in titleList:
	title.append(titleDom.string.strip())
summaryList = bs.select('.summary')
for summaryDom in summaryList:
	summary.append(summaryDom.text.strip())
ratingList = bs.select('.rating_type > strong')
for ratingDom in ratingList:
	rating.append(ratingDom.get_text(strip=True))
print(title)
print(summary)
print(rating)
```


```python
import urllib.request
from bs4 import BeautifulSoup
title = []
summary = []
rating = []
for n in range(1,31):
	data = urllib.request.urlopen('https://comic.naver.com/genre/bestChallenge.nhn?&page='+str(n))
	bs = BeautifulSoup(data, 'html.parser')
	titleList = bs.select('.challengeTitle > a')	
	for titleDom in titleList:
		title.append(titleDom.string.strip())

	summaryList = bs.select('.summary')	
	for summaryDom in summaryList:
		summary.append(summaryDom.text.strip())

	ratingList = bs.select('.rating_type > strong')	
	for ratingDom in ratingList:
		rating.append(ratingDom.get_text(strip=True))
print(title)
print(summary)
print(rating)
```


```python
import requests
from bs4 import BeautifulSoup
title = []
link = []
urlstr = 'http://www.yes24.com/SearchCorner/Search?domain=BOOK&query=python'
r = requests.get(urlstr)
#r.encoding = "utf-8"
bs = BeautifulSoup(r.text, 'html.parser')
titleList = bs.select('p.goods_name.goods_icon > a > strong')
linklList = bs.select('p.goods_name.goods_icon > a')

for titleDom in titleList:
	title.append(titleDom.string)
for linkDom in linklList:
	link.append(linkDom["href"])

print("-- 도서 제목 --")
print(title)
print("-- 도서 링크 URL --")
print(link)
with open('C:/Temp/booklink.csv', "wt", encoding="utf-8") as f:
    f.write('booktitle,booklink\n')  
    for i in range(len(title)):
        f.write(title[i]+","+link[i]+'\n')  
```


```python
from bs4 import BeautifulSoup
import urllib.request as req
import io

url = "http://www.kma.go.kr/weather/forecast/mid-term-rss3.jsp?stnId=108"
savename = "C:/Temp/forecast.xml"
req.urlretrieve(url, savename)

xml = open(savename, "r", encoding="utf-8").read()
soup = BeautifulSoup(xml, 'html.parser')

info = {}
for location in soup.find_all("location"):
    loc = location.find('city').string
    min_w = location.find_all('tmn')
    max_w = location.find_all('tmx')
    weather = [a.string+"~"+b.string for a, b in zip(min_w, max_w)]

    if not (loc in info):
        info[loc] = []
    for data in weather:
        info[loc].append(data)
print(info)

with open('C:/Temp/forecast.txt', "wt", encoding="utf-8") as f:
    for loc in sorted(info.keys()):
        f.write(str(loc)+'\n')
        for name in info[loc]:
            f.write('\t'+str(name)+'\n')
```


```python
import json
import urllib.request

#User-Agent를 조작하는 경우 
hdr = {'User-Agent':'Mozilla/5.0 (Windows NT 10.0; Win64; x64) '+ 
        'AppleWebKit/537.36 (KHTML, like Gecko) Chrome/75.0.3770.80 Safari/537.36'}

req = urllib.request.Request('http://unico2013.dothome.co.kr/crawling/header.php', headers = hdr)
#req = urllib.request.Request('http://unico2013.dothome.co.kr/crawling/header.php')
data = urllib.request.urlopen(req).read()
#page = data.decode('utf-8', 'ignore')
res_content = json.loads(data)

print(res_content["result"])

```



### - 실습

```python
import urllib.request
import urllib.parse
params = urllib.parse.urlencode({'category': '역사', 'page': 25})
url = "http://unico2013.dothome.co.kr/crawling/exercise.php?%s" % params
print("URL params : ", params)
print("URL 문자열 : ", url)
with urllib.request.urlopen(url) as f:
    print(f.read().decode('utf-8'))
```

```python
import requests
dicdata = {'category': '여행', 'page': 100}
urlstr = 'http://unico2013.dothome.co.kr/crawling/exercise.php'
r = requests.get(urlstr, params=dicdata)
r.encoding = 'utf-8'
#print(type(r))
#print(r.headers)
if r.text :
    print(r.text)
else :
    print('응답된 콘텐츠가 없어요')
```

