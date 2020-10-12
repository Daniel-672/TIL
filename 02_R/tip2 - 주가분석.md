# tip들

### - table.Drawdowns

```R
library(ggplot2)
library(dplyr)
library(rJava)
library(RJDBC)
library(DBI)
library(xts)
library(PerformanceAnalytics)
library(tidyverse)
library(timetk)
library(timeSeries)
drv <- JDBC(driverClass = "org.mariadb.jdbc.Driver" ,"mariadb-java-client-2.6.2.jar")
conn <- dbConnect(drv, 'jdbc:mariadb://127.0.0.1:3303/work', 'scott', 'tiger')

cmp <- '005930' #삼성전자
#queryString <- paste0("SELECT * FROM stockinfoprice 
#                         WHERE substr(closeDT, 1, 4) IN ('2019', '2020') AND companyCode = '", cmp, "'")
queryString <- paste0("SELECT closeDT as dates, closePrice FROM stockinfoperesp 
                        WHERE substr(closeDT, 1, 4) IN ('2019', '2020') AND companyCode = '", cmp, "' ORDER BY closeDT")


ResultSet <- NULL
ResultSet <- dbGetQuery(conn, queryString)
length(ResultSet[,1])
ResultSet <- na.omit(ResultSet)
# str(ResultSet) dbGetQuery결과는 dataFrame
head(ResultSet)

rownames(ResultSet) <- as.Date(ResultSet$dates) #날짜를 행명으로변경
# date <- as.Date(test$Date, format = "%m/%d/%Y")
ResultSet <- ResultSet[ , 2:dim(ResultSet)[2], drop=FALSE]   # 문자 날자열 날림


plot(xts_ResultSet, main = '삼성전자')
head(xts_ResultSet, 2)

ret = log( x[t] / x[t-1] )
table.Drawdowns(ret, geometric = FALSE)

ret = ROC(xts_ResultSet, type="continuous")
table.Drawdowns(ret)
momentum(xts_ResultSet)


chart.Drawdown(
  ret,
  geometric = TRUE,
  legend.loc = NULL,
  colorset = (1:12),
  plot.engine = "default"
)
```



### - 주가 상승 하락 구간 의 워드 클라우드

```R
#install.packages("ggplot2") # ggplot2 패키지 설치
#install.packages("glue") # ggplot2 로드시 이 패키지 오류나면 R3.7이하에서 가능성
#install.packages('PerformanceAnalytics')
#install.packages('tidyverse')
#install.packages('timetk')
#install.packages('timeSeries')
#install.packages("dygraphs")
#install.packages('webshot')
library(ggplot2)
library(dplyr)
library(rJava)
library(RJDBC)
library(DBI)
library(xts)
library(PerformanceAnalytics)
library(tidyverse)
library(timetk)
library(timeSeries)
library(dygraphs)
library(gridExtra)
library(wordcloud2)
library(wordcloud)
library(htmlwidgets)
library(webshot)
webshot::install_phantomjs()

drv <- JDBC(driverClass = "org.mariadb.jdbc.Driver" ,"mariadb-java-client-2.6.2.jar")
conn <- dbConnect(drv, 'jdbc:mariadb://127.0.0.1:3303/work', 'scott', 'tiger')

#30개 회사 리스트
companylistQS <- paste0("SELECT * FROM companylist where companyname <> 'SK바이오팜' ")
                        #AND companyname = '삼성전자' 
companylist <- NULL
companylist <- dbGetQuery(conn, companylistQS)

drawrangebyCmp.from <- NULL; drawrangebyCmp.to <- NULL; pickrangebyCmp.from <- NULL; pickrangebyCmp.to <- NULL
xts_ResultSet_all <- NULL; drawrangebyCmp.depth <- NULL; pickrangebyCmp.depth <- NULL;
for (cmp in companylist$companyCode) {

#queryString <- paste0("SELECT * FROM stockinfoprice 
#                         WHERE substr(closeDT, 1, 4) IN ('2019', '2020') AND companyCode = '", cmp, "'")
queryString <- paste0("SELECT closeDT as dates, closePrice FROM stockinfoperesp 
                        WHERE substr(closeDT, 1, 4) IN ('2019', '2020') AND companyCode = '", cmp, "' ORDER BY closeDT")

ResultSet <- NULL
ResultSet <- dbGetQuery(conn, queryString)
length(ResultSet[,1])
ResultSet <- na.omit(ResultSet)
cat("++++++++++++", cmp, companylist$companyName[which(companylist$companyCode == cmp)],'DB load완료 \n')
# str(ResultSet) dbGetQuery결과는 dataFrame
head(ResultSet)

rownames(ResultSet) <- as.Date(ResultSet$dates) #날짜를 행명으로변경
# date <- as.Date(test$Date, format = "%m/%d/%Y")
ResultSet <- ResultSet[ , 2:dim(ResultSet)[2], drop=FALSE]   # 문자 날자열 날림
# head(ResultSet, 2)
# tail(ResultSet, 2)

# xts객체로 변경
xts_ResultSet <- as.xts(ResultSet)

# 종목별 최대 pick과 down의 구간을 추출 
ret = ROC(xts_ResultSet, type="continuous")
# ret = log( x[t] / x[t-1] )
drawdownList <- head(table.Drawdowns(ret, top = 1, geometric = FALSE),1)
print(drawdownList)
drawrangebyCmp.from <- c(drawrangebyCmp.from, drawdownList[1,]$From)
drawrangebyCmp.to <- c(drawrangebyCmp.to, ifelse(is.na(drawdownList[1,]$To), drawdownList[1,]$Trough, drawdownList[1,]$To))
drawrangebyCmp.depth <- c(drawrangebyCmp.depth, drawdownList[1,]$Depth)

ret2 = ROC(xts_ResultSet, type="continuous") * -1
# ret = log( x[t] / x[t-1] )
drawdownList2 <- head(table.Drawdowns(ret2, top = 1, geometric = FALSE),1)
print(drawdownList2)

pickrangebyCmp.from <- c(pickrangebyCmp.from, drawdownList2[1,]$From)
pickrangebyCmp.to <- c(pickrangebyCmp.to, ifelse(is.na(drawdownList2[1,]$To), drawdownList2[1,]$Trough, drawdownList2[1,]$To))
pickrangebyCmp.depth <- c(pickrangebyCmp.depth, drawdownList2[1,]$Depth)


#maxdrawdownList <- maxDrawdown(ret, geometric = FALSE)
#table.Drawdowns(ret)
#momentum(xts_ResultSet)
#str(rawGraph)

########### for (cmpname in rawGraph$companyName) {

drawdownList.to <- as.POSIXct(ifelse(is.na(drawdownList[1,]$To), drawdownList[1,]$Trough, drawdownList[1,]$To),origin="1970-01-01")
xts_ResultSet.drow <-
  xts_ResultSet[index(xts_ResultSet) >= drawdownList[1,]$From & index(xts_ResultSet) <= drawdownList.to]

drawdownList2.to <- as.POSIXct(ifelse(is.na(drawdownList2[1,]$To), drawdownList2[1,]$Trough, drawdownList2[1,]$To),origin="1970-01-01")
xts_ResultSet.pick <-
  xts_ResultSet[index(xts_ResultSet) >= drawdownList2[1,]$From & index(xts_ResultSet) <= drawdownList2.to]


gg <- ggplot(xts_ResultSet$closePrice, aes(x = Index, y = closePrice))
gg2 <- gg + geom_line(size=1, color="black")

gg5 <- gg2 + labs(title=companylist$companyName[which(companylist$companyCode == cmp)], x="일자", y="주가") + theme(plot.title = element_text(hjust = 0.5))
gg6 <- gg5 + theme(plot.title=element_text(size=20),
                   axis.title.x=element_text(size=10), 
                   axis.title.y=element_text(size=10), 
                   axis.text.x=element_text(size=5), 
                   axis.text.y=element_text(size=5))
gg3 <- gg6 +  geom_line(data = xts_ResultSet.drow , size=1, color="blue")

gg4 <- gg3 +  geom_line(data = xts_ResultSet.pick , size=1, color="red")
gg7 <- gg4 + labs(title=paste0(companylist$companyName[which(companylist$companyCode == cmp)],'의 상승 및 하락 구간' ), x="일자", y="주가") + theme(plot.title = element_text(hjust = 0.5))

# 종목별 워드 클라우드 생성 
rankwordsQS.d <- paste0("SELECT words FROM NaverDetailWords WHERE companyCode = '", 
                        cmp, "' AND substr(commentDate,1,10) BETWEEN '", format(drawdownList[1,]$From, "%Y.%m.%d"),"'"," AND '", format(drawdownList.to, "%Y.%m.%d") ,  "'")

rankwordsQS.p <- paste0("SELECT words FROM NaverDetailWords WHERE companyCode = '", 
                        cmp, "' AND substr(commentDate,1,10) BETWEEN '", format(drawdownList2[1,]$From, "%Y.%m.%d"),"'"," AND '", format(drawdownList2.to, "%Y.%m.%d") ,  "'")

rankwordsQS.d.Set <- NULL
rankwordsQS.d.Set <- dbGetQuery(conn, rankwordsQS.d)
pop_set.d <- strsplit(rankwordsQS.d.Set$words, "/")
pop_set.d <- unlist(pop_set.d)
pop_set.d <- gsub("[0-9]", "", pop_set.d)
cunpop_set.d <- Filter(function(x) {nchar(x) >= 2}, pop_set.d)
cunpop_set.d.table <- table(cunpop_set.d)
wordsrank.d <- head(sort(cunpop_set.d.table, decreasing=T),50)

rankwordsQS.p.Set <- NULL
rankwordsQS.p.Set <- dbGetQuery(conn, rankwordsQS.p)
pop_set.p <- strsplit(rankwordsQS.p.Set$words, "/")
pop_set.p <- unlist(pop_set.p)
pop_set.p <- gsub("[0-9]", "", pop_set.p)
cunpop_set.p <- Filter(function(x) {nchar(x) >= 2}, pop_set.p)
cunpop_set.p.table <- table(cunpop_set.p)
wordsrank.p <- head(sort(cunpop_set.p.table, decreasing=T),50)
getwd()
# 하락구간 클라우드
cmpcld.d <- paste0("./stock_data/", companylist$companyName[which(companylist$companyCode == cmp)],'_하락.png' )
gg.word.d <- wordcloud2(wordsrank.d,size=0.5, col="random-light", backgroundColor = "#475cd3")
saveWidget(gg.word.d, "tmp1.html", selfcontained = F)
webshot("tmp1.html", cmpcld.d, delay=5, vwidth = 480, vheight =  480)

# 상승구간 클라우드 
cmpcld.p <- paste0("./stock_data/", companylist$companyName[which(companylist$companyCode == cmp)],'_상승.png' )
gg.word.p <- wordcloud2(wordsrank.p,size=0.5, col="random-light", backgroundColor = "hotpink")
saveWidget(gg.word.p, "tmp2.html", selfcontained = F)
webshot("tmp2.html", cmpcld.p, delay=5, vwidth = 480, vheight =  480)

# 주가 변동 
cmpcld.s <- paste0("./stock_data/", companylist$companyName[which(companylist$companyCode == cmp)],'_주가.png' )
png(cmpcld.s)
grid.arrange(gg6, gg7,nrow=2, ncol=1,top="주가변동")
dev.off()

Sys.sleep(2)
}

rawGraph <- data.frame(companylist$companyCode, companylist$companyName, 
                       drawrangebyCmp.from, drawrangebyCmp.to, drawrangebyCmp.depth,
                       pickrangebyCmp.from, pickrangebyCmp.to, pickrangebyCmp.depth)
colnames(rawGraph) <- c('companyCode', 'companyName', 
                        'drawfrom', 'drawto', 'drawdepth',
                        'pickfrom', 'pickto', 'pickdepth')


head(rawGraph[order(rawGraph$drawdepth), ], 3)
head(rawGraph[order(rawGraph$pickdepth), ], 3)

dbDisconnect(conn)

#chart.Drawdown(
#  ret,
#  geometric = TRUE,
#  legend.loc = NULL,
#  colorset = (1:12),
#  plot.engine = "default"
#)
```

