

# Day7

> 정적 크롤링, openAPI(네이버, 트윗, 공공)

### - 교육내용

```R
# 한겨레 페이지(XML 패키지 사용)
library(XML)
library(rvest)
imsi <- read_html("http://www.hani.co.kr/")
t <- htmlParse(imsi)
content<- xpathSApply(t,'//*[@id="main-top01-scroll-in"]/div/div/h4/a', xmlValue); 
content
content <- gsub("[[:punct:]]", "", content)
content

# httr 패키지 사용 - GET 방식 요청
library(httr)
http.standard <- GET('http://www.w3.org/Protocols/rfc2616/rfc2616.html')
title2 = html_nodes(read_html(http.standard), 'div.toc h2')
title2 = html_text(title2)
title2


# httr 패키지 사용 - POST 방식 요청
library(httr)
otp_url= 'http://marketdata.krx.co.kr/contents/COM/GenerateOTP.jspx'
parameter = list(
  name = 'fileDown',
  filetype = 'csv',
  url = 'MKD/03/0303/03030103/mkd03030103',
  tp_cd = 'ALL',
  date = '20190607',
  lang = 'ko',
  pagePath = '/contents/MKD/03/0303/03030103/MKD03030103.jsp')

my_otp = POST(otp_url, query = parameter) 

download_url = 'http://file.krx.co.kr/download.jspx'
data = POST(download_url, query = list(code = my_otp),
            add_headers(referer = otp_url)) 

library(readr)
data =  read_html(data) 
data = html_text(data)
data = read_csv(data)
as.data.frame(data)


# 뉴스, 게시판 등 글 목록에서 글의 URL만 뽑아내기 
res = GET('https://news.naver.com/main/list.nhn?mode=LSD&mid=sec&sid1=001')
htxt = read_html(res)
link = html_nodes(htxt, 'div.list_body a'); length(link)
article.href = unique(html_attr(link, 'href'))
article.href


# 이미지, 첨부파일 다운 받기 
# pdf
res = GET('http://cran.r-project.org/web/packages/httr/httr.pdf')
writeBin(content(res, 'raw'), 'c:/Temp/httr.pdf')


# jpg
h = read_html('http://unico2013.dothome.co.kr/productlog.html')
imgs = html_nodes(h, 'img')
img.src = html_attr(imgs, 'src')
for(i in 1:length(img.src)){
  res = GET(paste('http://unico2013.dothome.co.kr/',img.src[i], sep=""))
  writeBin(content(res, 'raw'), paste('c:/Temp/', img.src[i], sep=""))
} 


# SNS의 Open API 활용 - naver blog
library(httr)
library(rvest)
library(XML)

rm(list=ls())
searchUrl<- "https://openapi.naver.com/v1/search/blog.xml"
Client_ID <- "XXXXXXXXXXXXXXXXXXXXXxxxxxx"
Client_Secret <- "XXXXXXXXXXXXXXXXXXXXXxxxxxx"

query <- URLencode(iconv("봄","euc-kr","UTF-8"))
url <- paste0(searchUrl, "?query=", query, "&display=100")
doc <- GET(url, add_headers("Content_Type" = "application/xml",
                            "X-Naver-client-Id" = Client_ID, "X-naver-Client-Secret" = Client_Secret))

# 블로그 내용에 대한 리스트 만들기		
doc2 <- htmlParse(doc, encoding="UTF-8")
text<- xpathSApply(doc2, "//item/description", xmlValue)
text
text <- gsub("</?b>", "", text)
text <- gsub("&.+t;", "", text)
text


# 네이버 뉴스 연동  
searchUrl<- "https://openapi.naver.com/v1/search/news.xml"
Client_ID <- "XXXXXXXXXXXXXXXXXXXXXxxxxxx"
Client_Secret <- "XXXXXXXXXXXXXXXXXXXXXxxxxxx"
query <- URLencode(iconv("코로나","euc-kr","UTF-8"))
url <- paste0(searchUrl, "?query=", query, "&display=100")
doc <- GET(url, add_headers("Content_Type" = "application/xml",
                            "X-Naver-client-Id" = Client_ID, "X-naver-Client-Secret" = Client_Secret))

# 네이버 뉴스 내용에 대한 리스트 만들기		
doc2 <- htmlParse(doc, encoding="UTF-8")
text<- xpathSApply(doc2, "//item/description", xmlValue); 
text
text <- gsub("</?b>", "", text)
text <- gsub("&.+t;", "", text)
text


# 트위터 글 읽어오기
install.packages("rtweet")
library(rtweet) 
appname <- "edu_data_collection"
api_key <- "XXXXXXXXXXXXXXXXXXXXXxxxxxx"
api_secret <- "XXXXXXXXXXXXXXXXXXXXXxxxxxx"
access_token <- "XXXXXXXXXXXXXXXXXXXXXxxxxxx-XXXXXXXXXXXXXXXXXXXXXxxxxxx"
access_token_secret <- "XXXXXXXXXXXXXXXXXXXXXxxxxxx"
twitter_token <- create_token(
  app = appname,
  consumer_key = api_key,
  consumer_secret = api_secret,
  access_token = access_token,
  access_secret = access_token_secret)

key <- "취업"
key <- enc2utf8(key)
result <- search_tweets(key, n=100, token = twitter_token)
str(result)
result$retweet_text
content <- result$retweet_text
content <- gsub("[[:lower:][:upper:][:digit:][:punct:][:cntrl:]]", "", content)   
content


#### bus 데이터 ####
library(XML)      
API_key  <- "XXXXXXXXXXXXXXXXXXXXXxxxxxx"
bus_No <- "402"
url <- paste("http://ws.bus.go.kr/api/rest/busRouteInfo/getBusRouteList?ServiceKey=", API_key, "&strSrch=", bus_No, sep="")
doc <- xmlParse(url, encoding="UTF-8")
top <- xmlRoot(doc)
top
df <- xmlToDataFrame(getNodeSet(doc, "//itemList"))
df
str(df)
View(df)

busRouteId <- df$busRouteId
busRouteId


url <- paste("http://ws.bus.go.kr/api/rest/buspos/getBusPosByRtid?ServiceKey=", API_key, "&busRouteId=", busRouteId, sep="")
doc <- xmlParse(url, encoding="UTF-8")
top <- xmlRoot(doc)
top
df <- xmlToDataFrame(getNodeSet(doc, "//itemList"))
df
View(df)


# 서울시 빅데이터- #### XML 응답 처리 ####
# http://openapi.seoul.go.kr:8088/XXXXXXXXXXXXXXXXXXXXXxxxxxx/xml/LampScpgmtb/1/100/

library(XML)
key = 'XXXXXXXXXXXXXXXXXXXXXxxxxxx'
contentType = 'xml'
startIndex = '1'
endIndex = '200'
url = paste0('http://openapi.seoul.go.kr:8088/',key,'/',contentType,'/LampScpgmtb/',startIndex,'/',endIndex,'/')

con <- url(url, "rb") 
imsi <- read_html(con)
t <- htmlParse(imsi, encoding="UTF-8")
upNm <- xpathSApply(t,"//row/up_nm", xmlValue) 
pgmNm <- xpathSApply(t,"//row/pgm_nm", xmlValue)
targetNm <- xpathSApply(t,"//row/target_nm", xmlValue)
price <- xpathSApply(t,"//row/u_price", xmlValue)

df <- data.frame(upNm, pgmNm, targetNm, price)
View(df)
write.csv(df, "edu.csv")


# 한국은행 결제 통계시스템 Open API - #### JSON 응답 처리 ####
install.packages("jsonlite")
#installed.packages()
library(jsonlite)
key = '/XXXXXXXXXXXXXXXXXXXXXxxxxxx/'
contentType = 'json/'
startIndex = '1'
endIndex = '/100/'

url <- paste0('http://ecos.bok.or.kr/api/KeyStatisticList',key,contentType,'kr/',startIndex,endIndex)
response <- GET(url)
json_data <- content(response, type = 'text', encoding = "UTF-8")
json_obj <- fromJSON(json_data)
df <- data.frame(json_obj)
df <- df[-1, -2]
names(df) <- c("className", "unitName", "cycle", "keystatName", "dataValue")
View(df)


# 정규표현식 사용
word <- "JAVA javascript Aa 가나다 AAaAaA123 %^&*"
gsub(" ", "@", word); sub(" ", "@", word)
gsub("A", "", word) 
gsub("a", "", word) 
gsub("Aa", "", word) 
gsub("(Aa)", "", word) 
gsub("(Aa){2}", "", word);gsub("Aa{2}", "", word) 
# "JAVA javascript Aa 가나다 AAaAaA123 %^&*"
gsub("[Aa]", "", word) 
gsub("[가-힣]", "", word) 
gsub("[^가-힣]", "", word) 
gsub("[&^%*]", "", word) 
gsub("[[:punct:]]", "", word) 
gsub("[[:alnum:]]", "", word) 
gsub("[1234567890]", "", word) 
gsub("[0-9]", "", word) 
gsub("\\d", "", word); gsub("\\D", "", word)
gsub("[[:digit:]]", "", word) 
gsub("[^[:alnum:]]", "", word) 
gsub("[[:space:]]", "", word) 
gsub("[[:punct:][:digit:]]", "", word) 
gsub("[[:punct:][:digit:][:space:]]", "", word) 

word <- "JAVA javascript 가나다 123 %^&*"

gsub("A", "", word) 
gsub("a", "", word) 
gsub("[Aa]", "", word) 
gsub("[가-힣]", "", word) 
gsub("[^가-힣]", "", word) 
gsub("[&^%*]", "", word) 
gsub("[[:punct:]]", "", word) 
gsub("[[:alnum:]]", "", word) 
gsub("[1234567890]", "", word) 
gsub("[[:digit:]]", "", word) 
gsub("[^[:alnum:]]", "", word) 
gsub("[[:space:]]", "", word) 
gsub("[[:space:][:punct:]]", "", word)

```



### - 실습

```R
###### [ OPEN API 실습 1 ] 
library(httr)
library(rvest)
library(XML)

searchUrl<- "https://openapi.naver.com/v1/search/blog.xml"
Client_ID <- "XXXXXXXXXXXXXXXXXXXXXxxxxxx"
Client_Secret <- "XXXXXXXXXXXXXXXXXXXXXxxxxxx"

query <- URLencode(iconv("맛집","euc-kr","UTF-8"))
url <- paste0(searchUrl, "?query=", query, "&display=100")
doc <- GET(url, add_headers("Content_Type" = "application/xml",
                            "X-Naver-client-Id" = Client_ID, "X-naver-Client-Secret" = Client_Secret))

# 블로그 내용에 대한 리스트 만들기		
doc2 <- htmlParse(doc, encoding="UTF-8")
text<- xpathSApply(doc2, "//item/description", xmlValue)
text
text <- gsub("</?b>", "", text)
blogList <- gsub("&.+t;", "", text)
blogList

df <- data.frame(blogList)
View(df)
write.csv(df, "naverblog.txt")


###### [ OPEN API 실습 2 ]
library(rtweet) 
appname <- "edu_data_collection"
api_key <- "XXXXXXXXXXXXXXXXXXXXXxxxxxx"
api_secret <- "XXXXXXXXXXXXXXXXXXXXXxxxxxx"
access_token <- "XXXXXXXXXXXXXXXXXXXXXxxxxxx-XXXXXXXXXXXXXXXXXXXXXxxxxxx"
access_token_secret <- "XXXXXXXXXXXXXXXXXXXXXxxxxxx"
twitter_token <- create_token(
  app = appname,
  consumer_key = api_key,
  consumer_secret = api_secret,
  access_token = access_token,
  access_secret = access_token_secret
  )

key <- "코로나"
key <- enc2utf8(key)
result <- search_tweets(key, n=100, token = twitter_token)

content <- result$retweet_text
content <- gsub("[[:lower:][:upper:][:punct:]]", "", content) # CR때문에 저장 시 문제
#content <- gsub("[[:lower:][:upper:][:punct:][:cntrl:]]", "", content)   
content <- content[which(!is.na(content))]

df <- data.frame(content)
View(df)
write.csv(df, "twitter.txt")


###### [ OPEN API 실습 3 ] 
library(XML)      
API_key  <- "XXXXXXXXXXXXXXXXXXXXXxxxxxx"
bus_No <- "360"
url <- paste("http://ws.bus.go.kr/api/rest/busRouteInfo/getBusRouteList?ServiceKey=", API_key, "&strSrch=", bus_No, sep="")
doc <- xmlParse(url, encoding="UTF-8")
top <- xmlRoot(doc)
top
df <- xmlToDataFrame(getNodeSet(doc, "//itemList"))
df
df360 <- subset(df, select=c("busRouteId", "length", "stStationNm", "edStationNm", "term"), subset= df$busRouteNm == 360)

cat("[ 360번 버스정보 ]", "\n")
cat("노선ID :", df360$busRouteId, "\n")
cat("노선길이 :", df360$length, "\n")
cat("기점 :", df360$stStationNm, "\n")
cat("종점 :", df360$edStationNm, "\n")
cat("배차간격 :", df360$term, "\n")


###### [ OPEN API 실습 4 ] 
searchUrl<- "https://openapi.naver.com/v1/search/news.json"
Client_ID <- "XXXXXXXXXXXXXXXXXXXXXxxxxxx"
Client_Secret <- "XXXXXXXXXXXXXXXXXXXXXxxxxxx"
query <- URLencode(iconv("빅데이터","euc-kr","UTF-8"))
url <- paste0(searchUrl, "?query=", query, "&display=100")
doc <- GET(url, add_headers("Content_Type" = "application/json",
                            "X-Naver-client-Id" = Client_ID, "X-naver-Client-Secret" = Client_Secret))

json_data <- content(doc, type = 'text', encoding = "UTF-8")
json_obj <- fromJSON(json_data)

text <- json_obj$items$title
text <- gsub("</?b>", "", text)
text <- gsub("&.+t;", "", text)

df <- data.frame(text)
View(df)

write.csv(df, "navernews.txt")



```


