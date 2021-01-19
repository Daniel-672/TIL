

# 분석Day02

>  데이터 수집

### - 교육내용

```python
from selenium import webdriver
from selenium.webdriver.common.keys import Keys 

driver = webdriver.Chrome('C:/Temp/chromedriver')
print("WebDriver 객체 : ", type(driver))

driver.get('http://www.google.com/ncr') 
target=driver.find_element_by_css_selector("[name = 'q']")
print("찾아온 태그 객체 : ", type(target))
target.send_keys('파이썬')
target.send_keys(Keys.ENTER)
driver.quit()
```


```python
import urllib.request
from bs4 import BeautifulSoup
#서버 접속
server = urllib.request.urlopen("https://www.istarbucks.co.kr/store/store_map.do")

response =server.read().decode()
bs = BeautifulSoup(response, "html.parser")
li = bs.find_all('li', class_="quickResultLstCon")
print(li)
```


```python
driver = webdriver.Chrome('C:/Temp/chromedriver')
driver.implicitly_wait(3)
driver.get("https://www.istarbucks.co.kr/store/store_map.do")
target=driver.find_element_by_class_name("quickResultLstCon")

print(type(target))
print(type(target.text))
print(target.text)
#driver.quit()
```


```python
from selenium import webdriver

driver = webdriver.Chrome('C:/Temp/chromedriver')
driver.implicitly_wait(3)
print('[ webdriver 객체 정보 ]')
print(type(driver)) 
print(driver) 
driver.get('http://unico2013.dothome.co.kr/crawling/exercise_css.html')
print('-----------------------------')
byTagName = driver.find_element_by_tag_name('h1')
print(type(byTagName))
print(byTagName.tag_name, ":", byTagName.text)
print('-----------------------------')
byTagNames = driver.find_elements_by_tag_name('h2')
print(type(byTagNames))
for tagName in byTagNames :
    print(tagName.tag_name, ":", tagName.text)
#driver.quit()
```


```python
from selenium import webdriver

driver = webdriver.Chrome('C:/Temp/chromedriver')
driver.implicitly_wait(3) 

driver.get('http://unico2013.dothome.co.kr/crawling/exercise_css.html')

byClassName = driver.find_element_by_class_name('subtitle')
print(type(byClassName))
print(byClassName.tag_name, ":", byClassName.text)
print('-----------------------------')
byClassNames = driver.find_elements_by_class_name('subtitle')
print(type(byClassNames))
for className in byClassNames :
    print(className.tag_name, ":", className.text)
#driver.quit()

```


```python
from selenium import webdriver

driver = webdriver.Chrome('C:/Temp/chromedriver')
driver.implicitly_wait(3) 

driver.get('http://unico2013.dothome.co.kr/crawling/exercise_css.html')

byId = driver.find_element_by_id('btype')
print(type(byId))
print(byId.tag_name, ":", byId.text)
print('-----------------------------')
byLinkText = driver.find_element_by_link_text('파이썬 학습 사이트')
print(type(byLinkText))
print(byLinkText.tag_name, ":", byLinkText.text)
print('-----------------------------')
byPLinkText = driver.find_elements_by_partial_link_text('사이트')
print(type(byPLinkText))
for linkText in byPLinkText :
    print(linkText.tag_name, ":", linkText.text)
#driver.quit()
```


```python
from selenium import webdriver

driver = webdriver.Chrome('C:/Temp/chromedriver')
driver.implicitly_wait(3) 

driver.get('http://unico2013.dothome.co.kr/crawling/exercise_css.html')

byCss1 = driver.find_element_by_css_selector('section>h2')
print(type(byCss1))
print(byCss1.tag_name, ":", byCss1.text)
print('-----------------------------')
byCss2 = driver.find_element_by_css_selector('aside>h2')
print(type(byCss2))
print(byCss2.tag_name, ":", byCss2.text)
print('-----------------------------')
byCss3 = driver.find_element_by_css_selector('body > section > article > ul > li:nth-child(3)')
print(type(byCss3))
print(byCss3.tag_name, ":", byCss3.text)
print('-----------------------------')
byCss4 = driver.find_elements_by_css_selector('ul>li.atype')
print(type(byCss4))
for byCss in byCss4 :
    print(byCss.tag_name, ":", byCss.text)
#driver.quit()
```


```python
from selenium import webdriver

driver = webdriver.Chrome('C:/Temp/chromedriver')
driver.implicitly_wait(3) 

driver.get('http://unico2013.dothome.co.kr/crawling/exercise_css.html')

byXpath1 = driver.find_element_by_xpath('//*[@id="f_subtitle"]')
print(type(byXpath1))
print(byXpath1.tag_name, ":", byXpath1.text)
print('-----------------------------')
byXpath2 = driver.find_element_by_xpath('/html/body/section/article/ul/li[3]')
print(type(byXpath2))
print(byXpath2.tag_name, ":", byXpath2.text)
print('-----------------------------')
byXpath3 = driver.find_elements_by_xpath('//ul/li[@class="atype"]')
print(type(byXpath3))
for byXpath in byXpath3 :
   print(byXpath.tag_name, ":", byXpath.text)
#driver.quit()
```


```python
from selenium import webdriver

driver = webdriver.Chrome('C:/Temp/chromedriver')
driver.implicitly_wait(3) 

driver.get('http://unico2013.dothome.co.kr/crawling/exercise_css.html')

byXpath1 = driver.find_element_by_xpath('//div/img')
print(type(byXpath1))
print(byXpath1.tag_name, ":", byXpath1.get_attribute('src'))
print('-----------------------------')
byXpath2 = driver.find_elements_by_xpath('/html/body/header/nav/a')
print(type(byXpath2))
for byXpath in byXpath2 :
    print(byXpath.tag_name, ":", byXpath.get_attribute('href'))
#driver.quit()
```


```python
from selenium import webdriver

driver = webdriver.Chrome('C:/Temp/chromedriver')
driver.implicitly_wait(3) 

driver.get("http://www.yes24.com/Product/goods/40936880")
import time
time.sleep(2)
readLinks = driver.find_elements_by_css_selector('#infoset_reviewContentList  div.btn_halfMore > a')

for readlink in readLinks :
    readlink.click()
    time.sleep(1)

reviewList = driver.find_elements_by_css_selector('#infoset_reviewContentList div.reviewInfoBot.origin div.review_cont')

temp_list = []
time.sleep(3)

for review in reviewList :    
    temp_list.append(review.text)
    
stopFlag = False
while True :
    for n in range(4, 13) :
        linkurl = '#infoset_reviewContentList > div.review_sort.sortBot > div.review_sortLft > div > a:nth-child('+str(n)+')'
        linkNum = driver.find_element_by_css_selector(linkurl)
        linkNum.click()   
        time.sleep(6)
        readLinks = driver.find_elements_by_css_selector('#infoset_reviewContentList span.review_more')
        ##infoset_reviewContentList > div:nth-child(4) > div.reviewInfoBot.crop > a > div > span
    for readlink in readLinks :
        readlink.click()
        time.sleep(3)

    reviewList = driver.find_elements_by_css_selector('#infoset_reviewContentList div.reviewInfoBot.origin div.review_cont')
    time.sleep(2)

    for review in reviewList :    
        temp_list.append(review.text)
    
    if len(reviewList) < 5 :
        stopFlag = True
        break
      
    if stopFlag == True :
        break
    nextPage = '#infoset_reviewContentList > div.review_sort.sortBot > div.review_sortLft > div > a.bgYUI.next'
    linkNum = driver.find_element_by_css_selector(nextPage)
    linkNum.click()
    time.sleep(2)

for item in temp_list :
    print(item)

wfile = open("c:/Temp/yes24file.txt","w", encoding="utf-8") 
wfile.writelines(temp_list) 
wfile.close()

```


```python
from selenium import webdriver

driver = webdriver.Chrome('C:/Temp/chromedriver')

driver.get('http://www.python.org/')
driver.implicitly_wait(3)
driver.get_screenshot_as_file('c:/Temp/python_main.png')
print('캡쳐 저장 완료')
import time
time.sleep(2)
driver.quit()
```


```python
from selenium import webdriver

options = webdriver.ChromeOptions()
options.add_argument('headless')
options.add_argument('window-size=1920x1080')

driver = webdriver.Chrome('C:/Temp/chromedriver', options=options)

driver.get('http://www.python.org/')
driver.implicitly_wait(3)
driver.get_screenshot_as_file('c:/Temp/main_main_headless.png')
print('캡쳐 저장 완료')
import time
time.sleep(2)
driver.quit()
```


```python
from selenium import webdriver

driver = webdriver.Chrome('C:/Temp/chromedriver')
driver.implicitly_wait(3) 

driver.get("https://www.istarbucks.co.kr/store/store_map.do")
import time
time.sleep(2)
loca = driver.find_element_by_class_name('loca_search')
loca.click()
time.sleep(2)
f_link = driver.find_element_by_css_selector("div.loca_step1_cont > ul > li:nth-child(1) > a")
f_link.click()
time.sleep(2)
s_link = driver.find_element_by_css_selector("#mCSB_2_container > ul > li:nth-child(1) > a")
s_link.click()
time.sleep(2)
shopList = driver.find_elements_by_css_selector("#mCSB_3_container > ul > li")

temp_list = []
time.sleep(3)
count = 0
total = len(shopList)
print(total)
for shop in shopList :    
    count += 1
    #print(count)
    shoplat = shop.get_attribute("data-lat")
    shoplong = shop.get_attribute("data-long")
    shopname = shop.find_element_by_tag_name("strong")
    shopinfo = shop.find_element_by_tag_name("p")
    splitinfo = shopinfo.text.split('\n')
    if(len(splitinfo) == 2):
        addr = splitinfo[0]
        phonenum = splitinfo[1]
    temp_list.append([shopname.text, shoplat, shoplong, addr, phonenum])
    if count != total and count % 3 == 0:
        driver.execute_script("var su = arguments[0]; var dom=document.querySelectorAll('#mCSB_3_container > ul > li')[su]; dom.scrollIntoView();", count)

with open('C:/Temp/starbucks_shop.txt', "wt", encoding="utf-8") as f:
    for item in temp_list :
        f.write(str(item)+'\n')
```


```python
from selenium import webdriver
from selenium.webdriver.common.keys import Keys 

driver = webdriver.Chrome('C:/Temp/chromedriver')
driver.implicitly_wait(3) 
driver.get('https://map.naver.com/') 
import time
time.sleep(2)

target=driver.find_element_by_css_selector(".input_search")

target.send_keys('서울시어린이도서관')
target.send_keys(Keys.ENTER)

time.sleep(2)
# driver.switch_to_frame("searchIframe")
driver.switch_to.frame("searchIframe")
while True :    
    names = driver.find_elements_by_css_selector("span.es3Ot")
    addrs = driver.find_elements_by_css_selector("span.gDzVe")
    if len(names) == 0 :
        print("추출되는 도서관이 더 이상 없슈")
        break
    for i in range(len(names)) :
        print(names[i].text,addrs[i].text, sep=", ", end="\n")
    print("------------------------------------------------")
    linkurl = '#app-root > div > div > div._2gyDX > a:nth-child(7)'
    try :
        linkNum = driver.find_element_by_css_selector(linkurl)
    except :
        print("더 이상 다음 페이지 없음")
        break
    linkNum.click()  
    time.sleep(5)
print("스크래핑 종료")
```


```python
from selenium import webdriver
from selenium.webdriver.common.keys import Keys 

driver = webdriver.Chrome('C:/Temp/chromedriver')
driver.implicitly_wait(3) 
driver.get('https://map.naver.com/') 
import time
time.sleep(2)

target=driver.find_element_by_css_selector(".input_search")

target.send_keys('서울시어린이도서관')
target.send_keys(Keys.ENTER)

time.sleep(2)
driver.switch_to.frame("searchIframe")
while True :
    count = 9
    while True :
        print("스크롤 : " +str(count))
        try :
            driver.execute_script("var su = arguments[0]; var dom=document.querySelectorAll('#_pcmap_list_scroll_container>ul>li')[su]; dom.scrollIntoView();", count)
            time.sleep(2)
        except :        
            break
        count += 10
    names = driver.find_elements_by_css_selector("span.es3Ot")
    addrs = driver.find_elements_by_css_selector("span.gDzVe")
    if len(names) == 0 :
        print("추출되는 도서관이 더 이상 없슈")
        break
    for i in range(len(names)) :
        print(names[i].text,addrs[i].text, sep=", ", end="\n")
    print("------------------------------------------------")
    linkurl = '#app-root > div > div > div._2gyDX > a:nth-child(7)'
    try :
        linkNum = driver.find_element_by_css_selector(linkurl)
    except :
        print("더 이상 다음 페이지 없음")
        break
    linkNum.click()  
    time.sleep(5)
print("스크래핑 종료")
```



### - 실습

```python
import requests
from bs4 import BeautifulSoup
import re

urlstr = 'http://unico2013.dothome.co.kr/crawling/exercise_bs.html'
r = requests.get(urlstr)
r.encoding = 'utf-8'
html_doc = r.text
# print(html_doc)

bs = BeautifulSoup(html_doc, 'html.parser')

print("[<h1> 태그의 콘텐츠]", bs.find('h1').text)

print("[텍스트 형식으로 내용을 가지고 있는 <a> 태그의 콘텐츠와 href 속성값]")
# atags = bs.find_all('a', len(text)>0)
atags = bs.find_all('a')
for atag in atags :
    if atag.string != None :        # atag.text.strip()
        print(atag.string, ":", atag['href'])
        
print("[<img> 태그의 src 속성값]", bs.img['src'])

print("[첫 번째 <h2> 태그의 콘텐츠]", bs.h2.text)

print("[<ul> 태그의 자식 태그들 중 style 속성의 값이 green으로 끝나는 태그의 콘텐츠]")
print(bs.find('ul').find_all('li', attrs={'style':re.compile("green$")})[0].text )

print("[두 번째 <h2> 태그의 콘텐츠]", bs.find_all('h2')[1].text)

print("[<ol> 태그의 모든 자식 태그들의 콘텐츠]")
for tg in bs.find('ol').find_all('li') :
    print (tg.text)

print("[<table> 태그의 모든 자손 태그들의 콘텐츠]")
for tg in bs.find('table').find_all('tr') :
    print (tg.text)
    
print("[name이라는 클래스 속성을 갖는 <tr> 태그의 콘텐츠]", bs.find('tr', class_="name").text)

print("[target이라는 아이디 속성을 갖는 <td> 태그의 콘텐츠]", bs.find('td', id='target').text)

```

```python
import requests
from bs4 import BeautifulSoup

title = []
media = []
urlstr = 'http://media.daum.net/ranking/popular/'
r = requests.get(urlstr)
r.encoding = "utf-8"
bs = BeautifulSoup(r.text, 'html.parser')
titleList = bs.select('ul.list_news2 > li > div.cont_thumb > strong > a')
mediaList = bs.select('ul.list_news2 > li > div.cont_thumb > strong > span')

for titleDom in titleList:
	title.append(titleDom.string)
for mediaDom in mediaList:
	media.append(mediaDom.string)

#print("-- 뉴스 타이틀 --")
#print(title)
#print("-- 제공 매체 --")
#print(media)

with open('C:/Temp/news.csv', "wt", encoding="utf-8") as f:
    f.write('newstitle,newscomname \n')  
    for i in range(len(title)):
        f.write("\"" + title[i] + "\", \"" + media[i] + "\"" + "\n")  
        print("\"" + title[i] + "\", \"" + media[i] + "\"" + "\n")
```

```python
import requests
from bs4 import BeautifulSoup
import re

grade = []
detail = []
page = 0
urlstr = 'https://movie.daum.net/moviedb/grade'
while True :
    page += 1
    dicdata = {'movieId': '131704', 'type': 'netizen', 'page': page}
    r = requests.get(urlstr, params=dicdata)
    print(r.url)
    r.encoding = "utf-8"

    bs = BeautifulSoup(r.text, 'html5lib')
    gradeList = bs.select('.emph_grade')
    detailList = bs.select('.desc_review')

    if len(gradeList) == 0 :
        break

    for gradeDom in gradeList:
        grade.append(gradeDom.text)
    for detailDom in detailList:
        detail.append(detailDom.text.strip())
    print("================ page" + str(page) + " 담기 ================")

print("================ " + str(len(grade)) + "개 프린트 ================")
for i in range(len(grade)):
    print( grade[i] + "," + detail[i])
    

```



