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
company.code <- c("005930", "000660", "035420", "051910", "207940", "005935", "005380", "068270", "035720", "006400", "051900", "012330", "028260", "017670", "000270", "036570", "005490", "105560", "066570", "251270")
#company.code <- c("036570")
company.name <- c("삼성전자", "SK하이닉스", "NAVER", "LG화학", "삼성바이오로직스", "삼성전자우", "현대차", "셀트리온", "카카오", "삼성SDI", "LG생활건강", "현대모비스", "삼성물산", "SK텔레콤", "기아차", "엔씨소프트", "POSCO", "KB금융", "LG전자", "넷마블")
yearRange <- c('2018', '2019', '2020')

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
      market_gubun = "STK",
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
delquery <- "delete from StockInfoPERESP"
dbSendUpdate(conn, delquery)
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



