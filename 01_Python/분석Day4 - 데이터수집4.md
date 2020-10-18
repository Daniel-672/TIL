

# 분석Day04

>  데이터 수집

### - 교육내용

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

