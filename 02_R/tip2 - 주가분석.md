# tip들

### - Drowdown

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
