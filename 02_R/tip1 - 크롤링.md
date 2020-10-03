# tip들

### - 주식 정보 크롤링 (csv저장)

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

### - 주식 정보 크롤링 (DB 저장)

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
      }

    if (substring(pageData$commentDate[1],1,4) == "2017") {
      dbWriteTable(conn, "NaverComments", pageData100, append = TRUE)
      break
    }
  }
  
}
  
dbDisconnect(conn)



```



