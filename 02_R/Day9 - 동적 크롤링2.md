

# Day9

> 동적크롤링2

### - 교육내용

```R
# 스크린샷 연습
install.packages("base64enc")
install.packages("magick")
library(base64enc)
library(magick)

remDr <- remoteDriver(remoteServerAddr = "localhost", port=4445, browserName="chrome")
remDr$open()
remDr$navigate("https://google.com")


# this returns a list of base64 characters
screenshot <- remDr$screenshot(display = FALSE)
# converts the base64 characters into a vector
screenshot <- base64decode(toString(screenshot), output = NULL)
# reads the vector as stores it as a PNG
screenshot <- image_read(screenshot)
image_browse(screenshot)


remDr$screenshot(display = FALSE, file="c:/Temp/google.png")
pngdata <- image_read("c:/Temp/google.png")
image_browse(pngdata)



#네이버 북 페이지 이번주 베스트 북정보 크롤링

site <- "https://book.naver.com/"
remDr$navigate(site)

#bestseller_tab

booksitenodes <- remDr$findElements(using='css', '#bestseller_tab > ul.tab_cp_spt > li > a')
booksites <- sapply(booksitenodes, function(x) {x$getElementAttribute("class")})
booksites <- unlist(booksites); 
booksites <- unlist(strsplit(booksites, ' '))
size <- length(booksites)
booksites <- booksites[seq(1, size, 2)]

for (booksite in booksites) {
  booksitenode <- remDr$findElement(using='css', paste0('#tab_cp_spt_',booksite))
  booksitenode$clickElement()
  Sys.sleep(2)
  
  bookthumbenodes <- remDr$findElements(using='css', '#bestseller_list dl>dt:nth-child(1) img')
  bookthumburl <- sapply(bookthumbenodes, function(x) {x$getElementAttribute("src")})
  bookthumburl <- unlist(bookthumburl)
  
  booktitlenodes <- remDr$findElements(using='css', '#bestseller_list dl>dt:nth-child(2)>a')
  booktitle <- sapply(booktitlenodes, function(x) {x$getElementText()})
  booktitle <- gsub("[[:cntrl:]]", "", booktitle)
  
  df <- data.frame(bookthumburl, booktitle)
  if (!dir.exists('book')) 
    dir.create('book')
  print(df)
  write.csv(df, file=paste0('book/', booksite, '.csv'))
}

#gs25 상품명 및 가격 크롤링
site <- 'http://gs25.gsretail.com/gscvs/ko/products/event-goods'
remDr$navigate(site)


eventgoodsnodes <- remDr$findElements(using='css', '#contents > div.cnt > div.cnt_section.mt50 > div > div > div:nth-child(3) > ul > li > div > p.tit')
eventgoodsname <- sapply(eventgoodsnodes, function(x) {x$getElementText()})

eventgoodsnodes <- remDr$findElements(using='css', '#contents > div.cnt > div.cnt_section.mt50 > div > div > div:nth-child(3) > ul > li > div > p.price > span')
eventgoodsprice <- sapply(eventgoodsnodes, function(x) {x$getElementText()})



# [ YES24의 명견만리 댓글 읽어오기 ]

library(RSelenium)
remDr <- remoteDriver(remoteServerAddr = "localhost", port = 4445, browserName = "chrome")
remDr$open()
remDr$navigate("http://www.yes24.com/24/goods/40936880")


webElem <- remDr$findElement("css", "body")
remDr$executeScript("scrollTo(0, 0)", args = list(webElem))
Sys.sleep(1)
remDr$executeScript("scrollBy(0, 3200)", args = list(webElem))
Sys.sleep(1)
remDr$executeScript("scrollBy(0, 3200)", args = list(webElem))
Sys.sleep(1)
remDr$executeScript("scrollBy(0, 3200)", args = list(webElem))
Sys.sleep(3)
repl_v = NULL
endFlag <- FALSE
page <- 3

repeat {
  for(index in 3:7) {
    fullContentLinkCSS <- paste("#infoset_reviewContentList > div:nth-child(",index,") > div.reviewInfoBot.crop > a", sep='')
    fullContentLink<-remDr$findElements(using='css selector',  fullContentLinkCSS)
    if (length(fullContentLink) == 0) {
      cat("종료\n")
      endFlag <- TRUE
      break
    }
    remDr$executeScript("arguments[0].click();",fullContentLink);
    Sys.sleep(1)
    fullContentCSS <- paste("#infoset_reviewContentList > div:nth-child(",index,") > div.reviewInfoBot.origin > div.review_cont > p", sep='')
    fullContent<-remDr$findElements(using='css selector', fullContentCSS)
    repl <-sapply(fullContent,function(x){x$getElementText()})    
    print(repl)
    cat("---------------------\n")
    repl_v <- c(repl_v, unlist(repl))
  }
  if(endFlag)
    break;  
  
  if(page == 10){
    page <- 3
    nextPageCSS <- "#infoset_reviewContentList > div.review_sort.sortTop > div.review_sortLft > div > a.bgYUI.next"
  }
  else{
    page <- page+1;
    nextPageCSS <- paste("#infoset_reviewContentList > div.review_sort.sortBot > div.review_sortLft > div > a:nth-child(",page,")",sep="")
  }
  remDr$executeScript("scrollTo(0, 0)", args = list(webElem))
  nextPageLink<-remDr$findElements(using='css selector',nextPageCSS) 
  remDr$executeScript("arguments[0].click();",nextPageLink);
  #sapply(nextPageLink,function(x){x$clickElement()})  
  Sys.sleep(3)
  print(page)
}
write(repl_v, "yes24.txt")


# [ 스타벅스 서울지역 전체 매장정보1 ]
library(RSelenium)
remDr <- remoteDriver(remoteServerAddr = "localhost", port = 4445, browserName = "chrome")
remDr$open()
remDr$navigate("https://www.istarbucks.co.kr/store/store_map.do?disp=locale")

selectSeoul <- "#container > div > form > fieldset > div > section > article.find_store_cont > article > article:nth-child(4) > div.loca_step1 > div.loca_step1_cont > ul > li:nth-child(1) > a"
nextPageLink<-remDr$findElements(using='css selector',selectSeoul)  
sapply(nextPageLink,function(x){x$clickElement()})


selectAll <- paste("#mCSB_2_container > ul > li:nth-child(1) > a")
nextPageLink<-remDr$findElements(using='css selector',selectAll)  
sapply(nextPageLink,function(x){x$clickElement()})

sizeCss <- "#container > div > form > fieldset > div > section > article.find_store_cont > article > article:nth-child(4) > div.loca_step3 > div.result_num_wrap > span"
size <- remDr$findElements(using='css selector',sizeCss)
limit <-sapply(size,function(x){x$getElementText()})    

nameList <- NULL
addressList <- NULL
phoneList <- NULL
latList <- NULL
longList <- NULL

for(i in 1 : as.numeric(limit)){
  nameCss <- paste("#mCSB_3_container > ul > li:nth-child(",i,")  > strong", sep = '')
  nameLink <- remDr$findElements(using='css selector',nameCss)
  a <- sapply(nameLink,function(x){x$getElementText()})
  nameList <- c(nameList, unlist(a))
  
  infoCss <- paste("#mCSB_3_container > ul > li:nth-child(",i,")  > p", sep = '')
  infoLink <- remDr$findElements(using='css selector',infoCss)
  a <- sapply(infoLink,function(x){x$getElementText()})
  words = strsplit(unlist(a), split="\n")
  addressList <- c(addressList, words[[1]][1])
  phoneList <- c(phoneList, words[[1]][2])
  
  pointCss <- paste("#mCSB_3_container > ul > li:nth-child(",i,")", sep = '')
  pointLink <- remDr$findElements(using='css selector',pointCss)
  latList <- c(latList, sapply(pointLink, function(x){x$getElementAttribute('data-lat')}))
  longList <- c(longList, sapply(pointLink, function(x){x$getElementAttribute('data-long')}))
  
  if(i %% 3 == 0 && i != as.numeric(limit)){
    remDr$executeScript("var su = arguments[0]; var dom = document.querySelectorAll('#mCSB_3_container > ul > li')[su]; dom.scrollIntoView();", list(i))
  }
}

# [ 스타벅스 서울지역 전체 매장정보2 ]
library(RSelenium)
remDr <- remoteDriver(remoteServerAddr = "localhost", port=4445, browserName="chrome")
remDr$open()

site <- paste("https://www.istarbucks.co.kr/store/store_map.do?disp=locale")
remDr$navigate(site)

Sys.sleep(3)

#서울 클릭
btn1Css <- "#container > div > form > fieldset > div > section > article.find_store_cont > article > article:nth-child(4) > div.loca_step1 > div.loca_step1_cont > ul > li:nth-child(1) > a"
btn1Page <- remDr$findElements(using='css',btn1Css)
sapply(btn1Page,function(x){x$clickElement()})
Sys.sleep(3)

#전체 클릭
btn2Css <- "#mCSB_2_container > ul > li:nth-child(1) > a"
btn2Page <- remDr$findElements(using='css',btn2Css)
sapply(btn2Page,function(x){x$clickElement()})
Sys.sleep(3)

index <- 0
starbucks <- NULL
total <- sapply(remDr$findElements(using='css',"#container > div > form > fieldset > div > section > article.find_store_cont > article > article:nth-child(4) > div.loca_step3 > div.result_num_wrap > span"),function(x){x$getElementText()})

repeat{
  index <- index + 1
  print(index)
  
  storeCss <- paste0("#mCSB_3_container > ul > li:nth-child(",index,")")
  storePage <- remDr$findElements(using='css',storeCss)
  if(length(storePage) == 0) 
    break
  storeContent <- sapply(storePage,function(x){x$getElementText()})
  
  #스타벅스 정보 추출
  #strsplit(storeContent, split="\n")
  storeList <- strsplit(unlist(storeContent), split="\n")
  shopname <- storeList[[1]][1]
  addr <- storeList[[1]][2]
  addr <- gsub(",", "", addr)
  telephone <- storeList[[1]][3]
  
  #스타벅스 위도 경도 추출
  lat <- sapply(storePage,function(x){x$getElementAttribute("data-lat")})
  lng <- sapply(storePage,function(x){x$getElementAttribute("data-long")})
  
  #병합
  starbucks <- rbind(starbucks ,cbind(shopname, addr, telephone, lat, lng))
  
  #스크롤 다운
  if(index %% 3 == 0 && index != total)
    remDr$executeScript("var dom=document.querySelectorAll('#mCSB_3_container > ul > li')[arguments[0]]; dom.scrollIntoView();", list(index))
}
write.csv(starbucks, "starbucks.csv")

```



### - 실습

```R
library(RSelenium)
remDr <- remoteDriver(remoteServerAddr = "localhost" , port = 4445, browserName = "chrome")
remDr$open()
site <- 'http://gs25.gsretail.com/gscvs/ko/products/event-goods'
remDr$navigate(site)
Sys.sleep(3)

# 2+1행사 페이지로 이동
moveTwotoonePage <- remDr$findElement(using='css', '#TWO_TO_ONE')
moveTwotoonePage$clickElement()
Sys.sleep(2)

previousPage <- 0
goodsname <- NULL
goodsprice <- NULL

repeat{
# 현재페이지 Check
currentPagenodes <- remDr$findElements(using='css', '#pageNum')
currentPage <- unlist(sapply(currentPagenodes, function(x){x$getElementAttribute('value')}))

cat("현재페이지:", currentPage)
if( previousPage == currentPage)  {
  cat(" 하지만 이미 읽은 페이지라서 종료함~ \n")
  break; 
}
previousPage <- currentPage

eventgoodsnodes <- remDr$findElements(using='css', '#contents > div.cnt > div.cnt_section.mt50 > div > div > div:nth-child(5) > ul > li > div > p.tit')
ceventgoodsname <- sapply(eventgoodsnodes, function(x) {x$getElementText()})
ceventgoodsname <- unlist(ceventgoodsname)

eventgoodsnodes <- remDr$findElements(using='css', '#contents > div.cnt > div.cnt_section.mt50 > div > div > div:nth-child(5) > ul > li > div > p.price > span')
ceventgoodsprice <- sapply(eventgoodsnodes, function(x) {x$getElementText()})
ceventgoodsprice <- as.numeric(gsub("\\D", "", ceventgoodsprice))

goodsname <- append(goodsname, ceventgoodsname)
goodsprice <- append(goodsprice, ceventgoodsprice)

moveTwotooneNextPage <- remDr$findElements(using='css', '#contents > div.cnt > div.cnt_section.mt50 > div > div > div:nth-child(5) > div > a.next')
remDr$executeScript("arguments[0].click();",moveTwotooneNextPage)
Sys.sleep(2)

cat(" 상품수:", length(ceventgoodsname), "가격수:", length(ceventgoodsprice), "\n")

}

cat(" 마지막페이지:", currentPage, "총상품수:", length(goodsname), "총가격수:", length(goodsprice), "\n")
df <- data.frame(goodsname, goodsprice)
# duplicated(df); library(plyr); count(df)
write.csv(df, "gs25_twotoone.csv")
```


