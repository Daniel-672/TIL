# tip들

### - 주식 정보 크롤링

```R
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

board_tree_map <- c(1:25)[c(-1, -2, -8, -14, -20)]

# 네이버 주식 토론방 종목별 크롤링 리스트 제목 및 상세 링크
library(httr)
library(rvest)

url_form <-"https://finance.naver.com/item/board.nhn?code=005930&page="
comment.df <- NULL

for (page in 1 : 10) {
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
  vect.title <- html_attr(nodes.detail, "title")
  
  page <- data.frame(vect.date, vect.writer, vect.view, vect.good, vect.bad, vect.href, vect.title)
  comment.df <- rbind(comment.df, page)
}

View(comment.df)
write.csv(comment.df, "naver_comments.csv")




# 상세 링크의 내용 및 댓글
#body
#cbox_module > div > div.u_cbox_content_wrap > ul > li.u_cbox_comment.cbox_module__comment_208906735._user_id_no_1erCa > div.u_cbox_comment_box > div > div.u_cbox_text_wrap > span
# 네이버 토론방 크롤링 상세링크의 내용
library(rvest)
text<- NULL; title<-NULL; point<-NULL; review<-NULL; page=NULL
url<- "https://finance.naver.com/item/board_read.nhn?code=005930&nid=145625118&st=&sw=&page=1"
text <- read_html(url,  encoding="CP949")
#View(text)
nodes.detail.content <- html_nodes(text, "#body")
vect.detail.content <- html_text(nodes.detail.content)
vect.detail.content

nodes.detail.comments <- html_nodes(text, "#cbox_module > div > div.u_cbox_content_wrap > ul")
vect.detail.comments <- html_text(nodes.detail.comments)
vect.detail.comments

```





