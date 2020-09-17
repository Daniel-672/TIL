

# Day6

> 정적 크롤링, 등

### - 교육내용

```R
# 단일 페이지(rvest 패키지 사용)
library(rvest)
text<- NULL; title<-NULL; point<-NULL; review<-NULL; page=NULL
url<- "http://movie.naver.com/movie/point/af/list.nhn?page=2"
text <- read_html(url,  encoding="CP949")
text
# 영화제목
nodes <- html_nodes(text, ".movie")
title <- html_text(nodes)
title
# 영화평점
nodes <- html_nodes(text, ".title em")
point <- html_text(nodes)
point
# 영화리뷰 
nodes <- html_nodes(text, xpath="//*[@id='old_content']/table/tbody/tr/td[2]/text()")
nodes <- html_text(nodes, trim=TRUE)
nodes
review <- nodes[nchar(nodes) > 0]
#review <- nodes[seq(4,50,5)]
review
page <- data.frame(title, point, review)
write.csv(page, "movie_reviews.csv")



text<- NULL; vtitle<-NULL; vpoint<-NULL; vreview<-NULL; page=NULL
url<- "http://movie.naver.com/movie/point/af/list.nhn?page=1"
text <- read_html(url,  encoding="CP949")
text
for (index in 1:10) {
  # 영화제목
  node <- html_nodes(text, paste0("#old_content > table > tbody > tr:nth-child(", index, ") > td.title > a.movie.color_b"))
  title <- html_text(node)
  vtitle[index] <- title
  # 영화평점
  node <- html_nodes(text, paste0("#old_content > table > tbody > tr:nth-child(", index,") > td.title > div > em"))
  point <- html_text(node)
  vpoint <- c(vpoint, point)
  # 영화리뷰 
  node <- html_nodes(text, xpath=paste0('//*[@id="old_content"]/table/tbody/tr[', index,"]/td[2]/text()"))
  node <- html_text(node, trim=TRUE)
  review = node[4]
  vreview <- append(vreview, review)
}
page <- data.frame(vtitle, vpoint, vreview)
write.csv(page, "movie_reviews1.csv")




# 여러 페이지
site<- "http://movie.naver.com/movie/point/af/list.nhn?page="
text <- NULL
movie.review <- NULL
for(i in 1: 10) {
  url <- paste(site, i, sep="")
  text <- read_html(url,  encoding="CP949")
  nodes <- html_nodes(text, ".movie")
  title <- html_text(nodes)
  nodes <- html_nodes(text, ".title em")
  point <- html_text(nodes)
  nodes <- html_nodes(text, xpath="//*[@id='old_content']/table/tbody/tr/td[2]/text()")
  imsi <- html_text(nodes, trim=TRUE)
  
  cat("i=", i, "point=", point, "imsi=", length(imsi), "\n")
  

    review <- imsi[nchar(imsi) > 0] 
  if(length(review) == 10) {
    page <- cbind(title, point)
    page <- cbind(page, review)
    page <- data.frame(title, point, review)
    movie.review <- rbind(movie.review, page)
  } else {
    cat(paste(i," 페이지에는 리뷰글이 생략된 데이터가 있어서 수집하지 않습니다.ㅜㅜ\n"))
  }
}
write.csv(movie.review, "movie_reviews2.csv")

```



### - 실습

```R
library(rvest)
text<- NULL; point<-NULL; review<-NULL; vreview=NULL
url<- "https://movie.daum.net/moviedb/grade?movieId=131576"
text <- read_html(url)
text

# 영화평점
nodes <- html_nodes(text, "div.raking_grade > em")
point <- html_text(nodes)
point

# 영화리뷰 
for (index in 1:10) {
  oneDOM <- paste0("//*[@id='mArticle']/div[2]/div[2]/div[1]/ul/li[", index, "]/div/p/text()")
  nodes <- html_nodes(text, xpath=oneDOM)
  nodes <- html_text(nodes, trim=TRUE)
  review <- paste(nodes, collapse = " ")
  vreview <- append(vreview, review)
}   

page <- data.frame(point, vreview)
write.csv(page, "daummovie1.csv")


library(rvest)
text<- NULL; point<-NULL; review<-NULL; page=NULL; movie.review <- NULL
site<- "https://movie.daum.net/moviedb/grade?movieId=131576&type=netizen&page="

for(i in 1:5) {
  url <- paste(site, i, sep="")
  text <- read_html(url)
  text
  
  # 영화평점
  nodes <- html_nodes(text, "div.raking_grade > em")
  point <- html_text(nodes)
  point
  
  # 영화리뷰 
  vreview <- NULL
  for (index in 1:10) {
    oneDOM <- paste0("//*[@id='mArticle']/div[2]/div[2]/div[1]/ul/li[", index, "]/div/p/text()")
    nodes <- html_nodes(text, xpath=oneDOM)
    nodes <- html_text(nodes, trim=TRUE)
    review <- (if (paste(nodes, collapse = " ") != "") {paste(nodes, collapse = " ")})
    vreview <- append(vreview, review)
  }
  
  page <- data.frame(point, vreview)
  movie.review <- rbind(movie.review, page)
}
write.csv(movie.review, "daummovie2.csv")


library(rvest)
text<- NULL; point<-NULL; review<-NULL; page=NULL; movie.review <- NULL
#site<- "https://movie.daum.net/moviedb/grade?movieId=131576&type=netizen&page="
site<- "https://movie.daum.net/moviedb/grade?movieId=127897&type=netizen&page="

for(i in 1:100000) {
  url <- paste(site, i, sep="")
  text <- read_html(url)
  text
  
  # 영화평점
  nodes <- html_nodes(text, "div.raking_grade > em")
  user <- html_nodes(text, ".link_profile")
  nexepgYN <- html_nodes(text, "div.paging_popcorn > div > a:last-child")
  nexepgYN <- html_attr(nexepgYN, "href")
  point <- html_text(nodes)
  point
  cat("i=", i, "nextpage=", nexepgYN, "usercount=", length(user), "\n")
  # 영화리뷰 
  vreview <- NULL
  for (index in 1:length(user)) {
    oneDOM <- paste0("//*[@id='mArticle']/div[2]/div[2]/div[1]/ul/li[", index, "]/div/p/text()")
    nodes <- html_nodes(text, xpath=oneDOM)
    nodes <- html_text(nodes, trim=TRUE)
    review <- (if (paste(nodes, collapse = " ") != "") {paste(nodes, collapse = " ")})
    vreview <- append(vreview, review)
  }
  
  page <- data.frame(point, vreview)
  movie.review <- rbind(movie.review, page)
  
  if (length(nexepgYN) == 0) {break}
}
write.csv(movie.review, "daummovie3.csv")


```


