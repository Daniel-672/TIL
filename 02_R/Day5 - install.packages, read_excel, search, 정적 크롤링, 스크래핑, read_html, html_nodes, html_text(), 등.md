

# Day5

> install.packages, read_excel, search, 정적 크롤링, 스크패핑, read_html, html_nodes, html_text(), 등

### - 교육내용

```R
library() # 설치된 패키지 리스트
installed.packages()
search()

read_excel()
install.packages("readxl")
install.packages("rvest") 
install.packages("XML")
install.packages("httr")
install.packages("readr")


library(readxl) # require(readxl)
excel_data_ex <- read_excel("data/data_ex.xlsx")
getwd()
View(excel_data_ex)
search()
str(excel_data_ex)



# 정적 웹 크롤링과 스크래핑
library(rvest)

url <- "http://unico2013.dothome.co.kr/crawling/tagstyle.html"
text <- read_html(url)
text

nodes <- html_nodes(text, "div")
nodes
title <- html_text(nodes)
title

node1 <- html_nodes(text, "div:nth-of-type(1)")
node1
html_text(node1)
html_attr(node1, "style")

node2 <- html_nodes(text, "div:nth-of-type(2)")
node2
html_text(node2)
html_attr(node2, "style")

node3 <- html_nodes(text, "div:nth-of-type(3)")
node3
html_text(node3)
```



### - 실습

```R
library(rvest)
text<- NULL;
url <- "http://unico2013.dothome.co.kr/crawling/exercise_bs.html"
text <- read_html(url)
text

# <h1> 태그의 컨텐츠 
nodes1 <- html_nodes(text, "h1")
nodes1
html_text(nodes1)

# <a> 태그의 컨텐츠와 href 속성값
node2 <- html_nodes(text, "a")
node2
html_attr(node2, "href")

# <img> 태그의 src 속성값
node3 <- html_nodes(text, "body img")
node3
html_attr(node3, "src")

# 첫 번째 <h2> 태그의 컨텐츠
node4 <- html_nodes(text, "h2:first")
node4
html_text(node4)

# <ul> 태그의 자식 태그들 중 style 속성의 값이 green으로 끝나는 태그의 컨텐츠
node5 <- html_nodes(text, CSS="color:green")
node5
html_text(node5)

# 두 번째 <h2> 태그의 컨텐츠
node6 <- html_nodes(text, "body > h2:last")
node6
html_text(node6)

# <ol> 태그의 모든 자식 태그들의 컨텐츠 
node7 <- html_nodes(text, "body > ol > *")
node7
html_text(node7)

# <table> 태그의 모든 자손 태그들의 컨텐츠 
node8 <- html_nodes(text, "body > table *")
node8
html_text(node8)

# name이라는 클래스 속성을 갖는 <tr> 태그의 컨텐츠 
node9 <- html_nodes(text, "body > table > .name")
node9
html_text(node9)

#target이라는 아이디 속성을 갖는 <td> 태그의 컨텐츠
node10 <- html_nodes(text, "#target")
node10
html_text(node10)


```


