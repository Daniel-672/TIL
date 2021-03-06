# tip들

### - 댓글 크롤링 (csv저장)

```R
# 네이버 주식 토론방 종목별 크롤링 리스트 제목 및 상세
# 날짜
#content > div.section.inner_sub > table.type2 > tbody > tr:nth-child(3) > td:nth-child(1) > span
# 제목 & 상세 링크
#content > div.section.inner_sub > table.type2 > tbody > tr:nth-child(3) > td.title > a
# 글쓴이
#content > div.section.inner_sub > table.type2 > tbody > tr:nth-child(3) > td.p11
# 조회
#content > div.section.inner_sub > table.type2 > tbody > tr:nth-child(3) > td:nth-child(4) > span
# 공감
#content > div.section.inner_sub > table.type2 > tbody > tr:nth-child(3) > td:nth-child(5) > strong
# 비공감
#content > div.section.inner_sub > table.type2 > tbody > tr:nth-child(3) > td:nth-child(6) > strong
# 마지막 뎃글의 비공감 
#content > div.section.inner_sub > table.type2 > tbody > tr:nth-child(25) > td:nth-child(6) > strong
# 상세 링크의 내용
#body



library(httr)
library(rvest)
company.code <- "005930"
board_tree_map <- c(1:25)[c(-1, -2, -8, -14, -20)]
url_form <-paste0("https://finance.naver.com/item/board.nhn?code=", company.code, "&page=")

comment.df <- NULL

for (page in 1 : 2) {
  sent_url <- paste0(url_form, page)
  url <- sent_url
  ref <- sent_url
  response <- httr::GET(url, httr::add_headers(Referer = ref))
  html_content <- read_html(response, encoding="CP949")
  vect.date <- NULL; vect.writer <- NULL; vect.view <- NULL; vect.good <- NULL; vect.bad <- NULL; vect.href <- NULL; vect.title <- NULL
  for (cmt_line in board_tree_map) {
    # 날짜
    #content > div.section.inner_sub > table.type2 > tbody > tr:nth-child(3) > td:nth-child(1) > span
    nodes.date <- html_nodes(html_content, paste0('#content > div.section.inner_sub > table.type2 > tbody > tr:nth-child(', cmt_line, ") > td:nth-child(1) > span"))
    text.date <- html_text(nodes.date)
    vect.date <- append(vect.date, text.date)
    # 글쓴이
    #content > div.section.inner_sub > table.type2 > tbody > tr:nth-child(3) > td.p11
    nodes.writer <- html_nodes(html_content, paste0('#content > div.section.inner_sub > table.type2 > tbody > tr:nth-child(', cmt_line, ") > td.p11"))
    text.writer <- html_text(nodes.writer)
    vect.writer <- append(vect.writer, gsub("[[:space:]]", "", text.writer))    
    # 조회
    #content > div.section.inner_sub > table.type2 > tbody > tr:nth-child(3) > td:nth-child(4) > span
    nodes.view <- html_nodes(html_content, paste0('#content > div.section.inner_sub > table.type2 > tbody > tr:nth-child(', cmt_line, ") > td:nth-child(4) > span"))
    text.view <- html_text(nodes.view)
    vect.view <- append(vect.view, text.view)    
    # 공감
    #content > div.section.inner_sub > table.type2 > tbody > tr:nth-child(3) > td:nth-child(5) > strong
    nodes.good <- html_nodes(html_content, paste0('#content > div.section.inner_sub > table.type2 > tbody > tr:nth-child(', cmt_line, ") > td:nth-child(5) > strong"))
    text.good <- html_text(nodes.good)
    vect.good <- append(vect.good, text.good)    
    # 비공감
    #content > div.section.inner_sub > table.type2 > tbody > tr:nth-child(3) > td:nth-child(6) > strong
    nodes.bad <- html_nodes(html_content, paste0('#content > div.section.inner_sub > table.type2 > tbody > tr:nth-child(', cmt_line, ") > td:nth-child(6) > strong"))
    text.bad <- html_text(nodes.bad)
    vect.bad <- append(vect.bad, text.bad)  
    cat(page, "page의 ", cmt_line, "번글 완료 \n")
  }
  # 제목 & 상세 링크
  #content > div.section.inner_sub > table.type2 > tbody > tr:nth-child(3) > td.title > a
  nodes.detail <- html_nodes(html_content, "td.title > a")
  vect.href <- html_attr(nodes.detail, "href")
  vect.comentId <- substring(vect.href,38,46)
  vect.title <- html_attr(nodes.detail, "title")
  
  #상세링크별 내용
  all.vect.detail.content <- NULL;
  for (href_line in vect.href) {
    detail_url <- NULL; tetail_text <- NULL; nodes.detail.content <- NULL; vect.detail.content <- NULL
    detail_url <- paste0("https://finance.naver.com", href_line)
    tetail_text <- read_html(detail_url,  encoding="CP949")
    nodes.detail.content <- html_nodes(tetail_text, "#body")
    vect.detail.content <- html_text(nodes.detail.content)
    all.vect.detail.content <- append(all.vect.detail.content, vect.detail.content)
  }
  
  page <- data.frame(company.code, vect.comentId, vect.date, vect.writer, vect.view, vect.good, vect.bad, vect.href, vect.title, all.vect.detail.content)
  comment.df <- rbind(comment.df, page)
}
#View(comment.df)
write.csv(comment.df, "naver_comments.csv")


```



### - 댓글 크롤링 (DB 저장)

```R
# 네이버 주식 토론방 종목별 크롤링 리스트 제목 및 상세
# 날짜
#content > div.section.inner_sub > table.type2 > tbody > tr:nth-child(3) > td:nth-child(1) > span
# 제목 & 상세 링크
#content > div.section.inner_sub > table.type2 > tbody > tr:nth-child(3) > td.title > a
# 글쓴이
#content > div.section.inner_sub > table.type2 > tbody > tr:nth-child(3) > td.p11
# 조회
#content > div.section.inner_sub > table.type2 > tbody > tr:nth-child(3) > td:nth-child(4) > span
# 공감
#content > div.section.inner_sub > table.type2 > tbody > tr:nth-child(3) > td:nth-child(5) > strong
# 비공감
#content > div.section.inner_sub > table.type2 > tbody > tr:nth-child(3) > td:nth-child(6) > strong
# 마지막 뎃글의 비공감 
#content > div.section.inner_sub > table.type2 > tbody > tr:nth-child(25) > td:nth-child(6) > strong
# 상세 링크의 내용
#body

#install.packages("rJava")
#install.packages("RJDBC")
#install.packages("DBI")
#install.packages("rvest") 
#install.packages("XML")
#install.packages("httr")
library(rJava)
library(RJDBC)
library(DBI)
library(httr)
library(rvest)

board_tree_map <- c(1:25)[c(-1, -2, -8, -14, -20)]
company.code <- c("삼성전자", "SK하이닉스", "NAVER", "LG화학", "삼성바이오로직스", "삼성전자우", "현대차", "셀트리온", "카카오", "삼성SDI", "LG생활건강", "현대모비스", "삼성물산", "SK텔레콤", "기아차", "엔씨소프트", "POSCO", "KB금융", "LG전자", "넷마블")

company.name <- c("005930", "000660", "035420", "051910", "207940", "005935", "005380", "068270", "035720", "006400", "051900", "012330", "028260", "017670", "000270", "036570", "005490", "105560", "066570", "251270")

company.list <- data.frame(company.code, company.name)
#company.code <- "005930"
pageData100 <- NULL
dbflag <- 0

drv <- JDBC(driverClass = "org.mariadb.jdbc.Driver" ,"mariadb-java-client-2.6.2.jar")
conn <- dbConnect(drv, 'jdbc:mariadb://127.0.0.1:3303/work', 'scott', 'tiger')

for (company.code in company.list$company.code) {
  
  url_form <-paste0("https://finance.naver.com/item/board.nhn?code=", company.code, "&page=")
  
  for (page in 25201 : 37000) {
    sent_url <- paste0(url_form, page)
    url <- sent_url
    ref <- sent_url
    response <- httr::GET(url, httr::add_headers(Referer = ref))
    html_content <- read_html(response, encoding="CP949")
    vect.date <- NULL; vect.writer <- NULL; vect.view <- NULL; vect.good <- NULL; vect.bad <- NULL; vect.href <- NULL; vect.title <- NULL
    for (cmt_line in board_tree_map) {
      # 날짜
      #content > div.section.inner_sub > table.type2 > tbody > tr:nth-child(3) > td:nth-child(1) > span
      nodes.date <- html_nodes(html_content, paste0('#content > div.section.inner_sub > table.type2 > tbody > tr:nth-child(', 
                                                    cmt_line, ") > td:nth-child(1) > span"))
      text.date <- html_text(nodes.date)
      vect.date <- append(vect.date, text.date)
      # 글쓴이
      #content > div.section.inner_sub > table.type2 > tbody > tr:nth-child(3) > td.p11
      nodes.writer <- html_nodes(html_content, paste0('#content > div.section.inner_sub > table.type2 > tbody > tr:nth-child(', 
                                                      cmt_line, ") > td.p11"))
      text.writer <- html_text(nodes.writer)
      vect.writer <- append(vect.writer, gsub("[[:space:]]", "", text.writer))    
      # 조회
      #content > div.section.inner_sub > table.type2 > tbody > tr:nth-child(3) > td:nth-child(4) > span
      nodes.view <- html_nodes(html_content, paste0('#content > div.section.inner_sub > table.type2 > tbody > tr:nth-child(', 
                                                    cmt_line, ") > td:nth-child(4) > span"))
      text.view <- html_text(nodes.view)
      vect.view <- append(vect.view, text.view)    
      # 공감
      #content > div.section.inner_sub > table.type2 > tbody > tr:nth-child(3) > td:nth-child(5) > strong
      nodes.good <- html_nodes(html_content, paste0('#content > div.section.inner_sub > table.type2 > tbody > tr:nth-child(', 
                                                    cmt_line, ") > td:nth-child(5) > strong"))
      text.good <- html_text(nodes.good)
      vect.good <- append(vect.good, text.good)    
      # 비공감
      #content > div.section.inner_sub > table.type2 > tbody > tr:nth-child(3) > td:nth-child(6) > strong
      nodes.bad <- html_nodes(html_content, paste0('#content > div.section.inner_sub > table.type2 > tbody > tr:nth-child(', 
                                                   cmt_line, ") > td:nth-child(6) > strong"))
      text.bad <- html_text(nodes.bad)
      vect.bad <- append(vect.bad, text.bad)  
      #cat(page, "page의 ", cmt_line, "번글 완료 \n")
    }
    # 제목 & 상세 링크
    #content > div.section.inner_sub > table.type2 > tbody > tr:nth-child(3) > td.title > a
    nodes.detail <- html_nodes(html_content, "td.title > a")
    vect.href <- html_attr(nodes.detail, "href")
    vect.comentId <- substring(vect.href,38,46)
    vect.title <- html_attr(nodes.detail, "title")
    
    #상세링크별 내용
    all.vect.detail.content <- NULL;
    for (href_line in vect.href) {
      detail_url <- NULL; tetail_text <- NULL; nodes.detail.content <- NULL; vect.detail.content <- NULL
      detail_url <- paste0("https://finance.naver.com", href_line)
      tetail_text <- read_html(detail_url,  encoding="CP949")
      nodes.detail.content <- html_nodes(tetail_text, "#body")
      vect.detail.content <- html_text(nodes.detail.content)
      all.vect.detail.content <- append(all.vect.detail.content, vect.detail.content)
    }
    
    pageData <- data.frame(company.code, vect.comentId, vect.date, vect.writer, 
                           vect.view, vect.good, vect.bad, vect.href, vect.title, 
                           all.vect.detail.content)
    colnames(pageData) <- c('companyCode', 'commentID', 'commentDate', 'commentWriter',
                            'commentView', 'commentGood', 'commentBad', 'commentHref', 
                            'commentTitle', 'commentDetail')
    
    pageData100 <- rbind(pageData100, pageData)
    cat(which(company.list$company.code == company.code), 
        company.list$company.name[which(company.list$company.code == company.code)], 
        "의" , page, "page", "저장 완료 \n")
    
    dbflag <- dbflag + 1
    if (dbflag == 100) {
      dbWriteTable(conn, "NaverComments", pageData100, append = TRUE)
      pageData100 <- NULL
      cat("===========", which(company.list$company.code == company.code), 
          company.list$company.name[which(company.list$company.code == company.code)], 
          "의" , dbflag, "page", "DB 저장 완료 =========== \n")  
      dbflag <- 0
      if (substring(pageData$commentDate[1],1,4) == "2017") { break }
      }
  }
  
}
  
dbDisconnect(conn)



```



### - 일별 EPS, PER등 주식 참고 정보 크롤링 (DB저장)

```R
library(httr)
library(rvest)
library(readr)
library(jsonlite)
library(rJava)
library(RJDBC)
library(DBI)
library(dplyr)

# 마리아DB연동
drv <- JDBC(driverClass = "org.mariadb.jdbc.Driver" ,"mariadb-java-client-2.6.2.jar")
conn <- dbConnect(drv, 'jdbc:mariadb://127.0.0.1:3303/work', 'scott', 'tiger')

# KRX 주식 종목 코드 가져오기
# http://marketdata.krx.co.kr/mdi#document=13020401에서 개별 검색창에 로드된
# json data(개발자 툴에서 MKD99000001.jspx의 response tab 복사)를 파일로 만들어 load
stockCode <- fromJSON("stockCode.json")
stockCodeList <- data.frame(stockCode$block1)
# stockCodeList[which(stockCodeList$marketName == "KOSPI"), ]

# 시총 20개만 추출
# 시총 1 - 20위
#company.code <- c("005930", "000660", "035420", "051910", "207940", "005935", "005380", "068270", "035720", "006400", "051900", "012330", "028260", "017670", "000270", "036570", "005490", "105560", "066570", "251270")
# 시총 21 - 30위
company.code <- c("034730", "055550", "018260", "015760", "096770", "003550", "032830", "033780", "009150")
yearRange <- c('2018', '2019', '2020')

# SK바아오팜은 2020년 만 있음
#company.code <- c("326030")
#yearRange <- c('2020')

targetList <- stockCodeList %>% 
              filter(short_code %in% paste0('A',company.code)) 

gen_otp_url <- 'http://marketdata.krx.co.kr/contents/COM/GenerateOTP.jspx'
down_url <- 'http://file.krx.co.kr/download.jspx'
stockInfoAll <- NULL

for (cmpcnt in 1:length(targetList$full_code)) {
  stockInfo3Y <- NULL
  for (tyear in yearRange) {
    gen_otp_data <- list(
      name = "fileDown",
      filetype = "csv",
      url = "MKD/13/1302/13020401/mkd13020401",
      market_gubun = "ALL",
      gubun = "2",
      isu_cdnm = paste0(targetList$short_code[cmpcnt], "/", targetList$codeName[cmpcnt]),
      isu_cd = targetList$full_code[cmpcnt],
      isu_nm = targetList$codeName[cmpcnt],
      isu_srt_cd = targetList$short_code[cmpcnt],
    #  schdate = "20180903",
      fromdate = paste0(tyear, "0101"),
      todate = paste0(tyear, "1231"),
      pagePath = "/contents/MKD/13/1302/13020401/MKD13020401.jsp"
      )
    
    otp <- POST(gen_otp_url, query = gen_otp_data) %>%
      read_html() %>%
      html_text()
    Sys.sleep(3)
    down_ind <- POST(down_url, query = list(code = otp),
                    add_headers(referer = gen_otp_url)) %>%
                read_html() %>%
                html_text() %>%
                read_csv()
    stockInfo1Y <- data.frame(down_ind)
    stockInfo3Y <- rbind(stockInfo3Y, stockInfo1Y)
    cat(cmpcnt, targetList$codeName[cmpcnt], tyear, "정보", length(stockInfo1Y$EPS), "적재 완료\n")
  }
  stockInfoAll <- rbind(stockInfoAll, stockInfo3Y)

}

colnames(stockInfoAll) <- c('closeDT', 'companyCode', 'companyName', 'controlYN',
                            'closePrice', 'EPS', 'PER', 'BPS', 
                            'PBR', 'DividendPS', 'DividendRate', 'seqNum', 'totCnt')
# DB적재 전 na처리
stockInfoAll$totCnt <- ifelse(is.na(stockInfoAll$totCnt), 0, stockInfoAll$totCnt)
# DB적재 전 '-'처리
stockInfoAll$EPS <- ifelse(stockInfoAll$EPS == "-", 0, stockInfoAll$EPS)
stockInfoAll$PER <- ifelse(stockInfoAll$PER == "-", 0, stockInfoAll$PER)
stockInfoAll$BPS <- ifelse(stockInfoAll$BPS == "-", 0, stockInfoAll$BPS)
stockInfoAll$PBR <- ifelse(stockInfoAll$PBR == "-", 0, stockInfoAll$PBR)
# DB적재 전 '넷마블게임즈'처리
stockInfoAll$companyName <- ifelse(stockInfoAll$companyName == "넷마블게임즈", "넷마블", stockInfoAll$companyName)

# View(stockInfoAll)
#delquery <- "delete from StockInfoPERESP"
#dbSendUpdate(conn, delquery)
dbWriteTable(conn, "StockInfoPERESP", stockInfoAll, append = TRUE)
cat("=========== DB 저장 완료 =========== \n") 
```



### - 일별 주가변동 정보 크롤링 (DB저장)

```R
library(httr)
library(rvest)
library(readr)
library(jsonlite)
library(rJava)
library(RJDBC)
library(DBI)
library(dplyr)

# 마리아DB연동
drv <- JDBC(driverClass = "org.mariadb.jdbc.Driver" ,"mariadb-java-client-2.6.2.jar")
conn <- dbConnect(drv, 'jdbc:mariadb://127.0.0.1:3303/work', 'scott', 'tiger')

# KRX 주식 종목 코드 가져오기
# http://marketdata.krx.co.kr/mdi#document=13020401에서 개별 검색창에 로드된
# json data(개발자 툴에서 MKD99000001.jspx의 response tab 복사)를 파일로 만들어 load
stockCode <- fromJSON("stockCode.json")
stockCodeList <- data.frame(stockCode$block1)
# stockCodeList[which(stockCodeList$marketName == "KOSPI"), ]

# 시총 20개만 추출
company.code <- c("005930", "000660", "035420", "051910", "207940", "005935", "005380", "068270", "035720", "006400", "051900", "012330", "028260", "017670", "000270", "036570", "005490", "105560", "066570", "251270")
#company.code <- c("005930")
company.name <- c("삼성전자", "SK하이닉스", "NAVER", "LG화학", "삼성바이오로직스", "삼성전자우", "현대차", "셀트리온", "카카오", "삼성SDI", "LG생활건강", "현대모비스", "삼성물산", "SK텔레콤", "기아차", "엔씨소프트", "POSCO", "KB금융", "LG전자", "넷마블")
yearRange <- c('2018', '2019', '2020')

targetList <- stockCodeList %>% 
              filter(short_code %in% paste0('A',company.code)) 

gen_otp_url <- 'http://marketdata.krx.co.kr/contents/COM/GenerateOTP.jspx'
down_url <- 'http://file.krx.co.kr/download.jspx'
stockPriceAll <- NULL

for (cmpcnt in 1:length(targetList$full_code)) {
  stockPrice3Y <- NULL
  for (tyear in yearRange) {
    gen_otp_data <- list(
      name = "fileDown",
      filetype = "csv",
      url = "MKD/13/1302/13020103/mkd13020103_02",
      isu_cdnm = paste0(targetList$short_code[cmpcnt], "/", targetList$codeName[cmpcnt]),
      isu_cd = targetList$full_code[cmpcnt],
      isu_nm = targetList$codeName[cmpcnt],
      isu_srt_cd = targetList$short_code[cmpcnt],
      fromdate = paste0(tyear, "0101"),
      todate = paste0(tyear, "1231"),
      pagePath = "/contents/MKD/13/1302/13020103/MKD13020103.jsp"
      )
    
    otp <- POST(gen_otp_url, query = gen_otp_data) %>%
      read_html() %>%
      html_text()
    Sys.sleep(2)
    down_ind <- POST(down_url, query = list(code = otp),
                    add_headers(referer = gen_otp_url)) %>%
                read_html() %>%
                html_text() %>%
                read_csv()
    stockPrice1Y <- data.frame(down_ind, companyCode <- substr(targetList$short_code[cmpcnt], 2, 8), companyName <- targetList$codeName[cmpcnt])
    stockPrice3Y <- rbind(stockPrice3Y, stockPrice1Y)
    cat(cmpcnt, targetList$codeName[cmpcnt], tyear, "정보", length(stockPrice1Y[,1]), "적재 완료\n")
  }
  stockPriceAll <- rbind(stockPriceAll, stockPrice3Y)

}

colnames(stockPriceAll) <- c('closeDT', 'closePrice', 'diffPrice', 'volumeCnt', 'volumeAmt', 
                            'startPrice', 'highPrice', 'lowPrice', 'marketTotAmt', 'listedStockCnt', 'companyCode', 'companyName')
# 컬럼 순서 바꾸기
stockPriceAll[, c(2, 3, 11, 12) ] <- 
  stockPriceAll[, c(11, 12, 2, 3) ]
colnames(stockPriceAll) <- c('closeDT', 'companyCode', 'companyName', 'volumeCnt', 'volumeAmt', 
                             'startPrice', 'highPrice', 'lowPrice', 'marketTotAmt', 'listedStockCnt', 'closePrice', 'diffPrice')


# DB적재 전 na처리
#stockPriceAll$totCnt <- ifelse(is.na(stockPriceAll$totCnt), 0, stockPriceAll$totCnt)
# DB적재 전 '-'처리
#stockPriceAll$EPS <- ifelse(stockPriceAll$EPS == "-", 0, stockPriceAll$EPS)
#stockPriceAll$PER <- ifelse(stockPriceAll$PER == "-", 0, stockPriceAll$PER)
#stockPriceAll$BPS <- ifelse(stockPriceAll$BPS == "-", 0, stockPriceAll$BPS)
#stockPriceAll$PBR <- ifelse(stockPriceAll$PBR == "-", 0, stockPriceAll$PBR)
# DB적재 전 '넷마블게임즈'처리
stockPriceAll$companyName <- ifelse(stockPriceAll$companyName == "넷마블게임즈", "넷마블", stockPriceAll$companyName)
# DB적재 전 '-'처리
stockPriceAll$marketTotAmt <- stockPriceAll$marketTotAmt * 1000000

# View(stockPriceAll)
delquery <- "delete from StockInfoPrice"
dbSendUpdate(conn, delquery)
dbWriteTable(conn, "StockInfoPrice", stockPriceAll, append = TRUE)
cat("=========== DB StockInfoPrice테이블 저장 완료 =========== \n") 
```



### - 전처리 각 종목별로 형태소 분석 후 단어를 DB에 저장

```R
#installed.packages()
# 한국어 형태소 분석 패키지 설치
# Rtools 설치
# https://cran.r-project.org/bin/windows/Rtools/index.html
# install.packages("Sejong")
# install.packages("hash")
# install.packages("tau")
# install.packages("RSQLite")
# install.packages("devtools")
# install.packages("wordcloud")
# install.packages("wordcloud2")

library(wordcloud)
library(wordcloud2)

# rm(list = ls())
#rm("clrQuerySet3")
library(KoNLP)
useSejongDic()
# github 버전 설치
# install.packages("remotes")
remotes::install_github('haven-jeon/KoNLP', upgrade = "never", INSTALL_opts=c("--no-multiarch"))
# 사전에 사용자 단어 추가
add_words <- c("가즈아", "사고팔고", "매수매도", "가을", "암카오", "네이버")
buildDictionary(user_dic=data.frame(add_words, rep("ncn", length(add_words))), replace_usr_dic=T)

options(java.parameters = "-Xmx8000m")
library(rJava)
library(RJDBC)
library(DBI)

drv <- JDBC(driverClass = "org.mariadb.jdbc.Driver" ,"mariadb-java-client-2.6.2.jar")
conn <- dbConnect(drv, 'jdbc:mariadb://127.0.0.1:3303/work', 'scott', 'tiger')

# "005930", "000660", "035420", "051910", "207940", "005935", "005380", "068270", 
# "035720", "006400", "051900", "012330", "028260", "017670", "000270", "036570", 
# "005490", "105560", "066570", "251270", "034730", "055550", "018260", "015760", 
# "096770", "003550", "326030", "032830", "033780", "009150"


company.code <- c("035420", "051910", "207940", "005935", "005380", "068270", 
              "035720", "006400", "051900", "012330", "028260", "017670", "000270", 
              "036570", "005490", "105560", "066570", "251270", "034730", "055550", 
              "018260", "015760", "096770", "003550", "326030", "032830", "033780", "009150")

for (cmp in company.code) {

  queryString <- paste0("SELECT companyCode, commentID, commentDate, commentDetail FROM navercomments WHERE companyCode = '", cmp, "' ")
  RawQuerySet <- NULL
  RawQuerySet <- dbGetQuery(conn, queryString)
  # 네이버 035420 : 34,353 obs. of  10 variables:
  # str(RawQuerySet)
  cat("DB Load 완료:", length(RawQuerySet$commentDetail), "\n")
  
  clrQuerySet1 <- gsub("[[:lower:][:upper:][:punct:][:cntrl:]]", " ", RawQuerySet$commentDetail) 
  clrQuerySet2 <- gsub("[^가-힣0-9' ']", " ", clrQuerySet1)
  clrQuerySet3 <- gsub("[가-힣]{20, }", " ", clrQuerySet2)
  clrQuerySet6 <- gsub("\\s+", " ", clrQuerySet3)
  # write.csv(clrQuerySet6, "test.csv")
  

  words_data <- NULL
  system.time(words_data <- sapply(clrQuerySet6, extractNoun, USE.NAMES = FALSE))
  length(words_data)
  
  word.list <- NULL
  for (i in 1 : length(words_data)) { 
    word.list <- append(word.list, paste(words_data[[i]],  collapse = '/'))  
    cat("companyCode:", cmp, "for순번:", i, "\n")
  }
  
  uploadWords <- NULL
  cat("companyCode:",length(RawQuerySet$companyCode), "\n")
  cat("commentID:",length(RawQuerySet$commentID), "\n")
  cat("commentDate:",length(RawQuerySet$commentDate), "\n")
  cat("word.list:",length(word.list), "\n")
  uploadWords <- data.frame(companyCode <- RawQuerySet$companyCode,
                            commentID <- RawQuerySet$commentID,
                            commentDate <- RawQuerySet$commentDate,
                            words <- word.list)
  colnames(uploadWords) <- c('companyCode', 'commentID', 'commentDate', 'words')
  
  dbWriteTable(conn, "NaverDetailWords_raw", uploadWords, append = TRUE)
  cat("===========", cmp, 
      "의" , length(uploadWords$companyCode), "개 DB 저장 완료 =========== \n") 

}

dbDisconnect(conn)



```



### - 형태소로 분리되어 저장된 정보를 불러 월별 단어 카운트

```R
#options(java.parameters = "-Xmx8000m")
library(rJava)
library(RJDBC)
library(DBI)
rm(list = ls())

drv <- JDBC(driverClass = "org.mariadb.jdbc.Driver" ,"mariadb-java-client-2.6.2.jar")
conn <- dbConnect(drv, 'jdbc:mariadb://127.0.0.1:3303/work', 'scott', 'tiger')

# "005930", "000660", "035420", "051910", "207940", "005935", "005380", "068270", 
# "035720", "006400", "051900", "012330", "028260", "017670", "000270", "036570", 
# "005490", "105560", "066570", "251270", "034730", "055550", "018260", "015760", 
# "096770", "003550", "326030", "032830", "033780", "009150"


company.code <- c("005930", "000660", "035420", "051910", "207940", "005935", "005380", "068270", 
                  "035720", "006400", "051900", "012330", "028260", "017670", "000270", "036570", 
                  "005490", "105560", "066570", "251270", "034730", "055550", "018260", "015760", 
                  "096770", "003550", "326030", "032830", "033780", "009150")

for (cmp in company.code) {

  rqueryString <- paste0("SELECT distinct substr(commentDate,1,7) AS commentMonth FROM NaverDetailWords 
                         WHERE companyCode = '", cmp, "' ORDER BY substr(commentDate,1,7)")
  looplist <- NULL
  looplist <- dbGetQuery(conn, rqueryString)
  #length(looplist$commentMonth)
    
    all_save_rank <- NULL; all_oneMonth <- NULL; all_companyCode <- NULL; all_type <- NULL
    
    for (oneMonth in looplist$commentMonth) {
      cat(cmp, oneMonth, "DB load 시작",  "\n")
      queryString <- paste0("SELECT words FROM NaverDetailWords WHERE companyCode = '", cmp, "' AND ", 
                            "substr(commentDate,1,7) = ", "'", oneMonth , "'" )
      RawQuerySet <- NULL
      RawQuerySet <- dbGetQuery(conn, queryString)
      cat(cmp, oneMonth, "DB load 완료",  "\n")
      
      cleanSet <- RawQuerySet$words
      pop_set <- strsplit(cleanSet, "/")

      unpop_set <- unlist(pop_set)
      unpop_set1 <- gsub("들이|같이|비공감공감비공감|하기", "", unpop_set)
      unpop_set2 <- gsub("[0-9]", "", unpop_set1)
      cunpop_set <- Filter(function(x) {nchar(x) >= 2}, unpop_set2)
      
      cunpop_set.table <- table(cunpop_set)
      
      wordsrank <- head(sort(cunpop_set.table, decreasing=T),10)

      save_rank <- paste(names(wordsrank), wordsrank, sep=':', collapse = '/')
      
      cat(cmp, oneMonth, "append 시작",  "\n")
      all_companyCode <- c(all_companyCode, cmp)      
      all_oneMonth <- c(all_oneMonth, oneMonth)
      all_save_rank <- c(all_save_rank, save_rank)
      all_type <- c(all_type, "M")
      cat(cmp, oneMonth, "append 완료",  "\n")
    }

    uploadResult <- data.frame(all_companyCode <- all_companyCode,
                               all_oneMonth <- all_oneMonth,
                               all_save_rank <- all_save_rank,
                               all_type <- all_type)
    colnames(uploadResult) <- c('companyCode', 'timeBase', 'wordsRank', 'type')
    
    dbWriteTable(conn, "NaverWordsRank", uploadResult, append = TRUE)
    cat("===========", cmp, 
        "의" , length(uploadResult$companyCode), "개 DB 저장 완료 =========== \n") 
  
}


# disconnect DB
dbDisconnect(conn)

```

