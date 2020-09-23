

# Day10

> MariaDB연동(DB connection, CRUD), 데이터 전처리(appply시리즈)

### - 교육내용

```R
install.packages("rJava")
install.packages("RJDBC")
install.packages("DBI")

library(rJava)
library(RJDBC)
library(DBI)

# db Connect
getwd() #"C:/Rexam"
drv <- JDBC(driverClass = "org.mariadb.jdbc.Driver" ,"mariadb-java-client-2.6.2.jar")
conn <- dbConnect(drv, 'jdbc:mariadb://127.0.0.1:3303/work', 'scott', 'tiger')

# select
query <- "select * from goods"
goodsAll <- dbGetQuery(conn, query)
goodsAll
dbReadTable(conn, 'goods')

query <- "select * from goods where su >= 3"
goodsOne <- dbGetQuery(conn, query)
goodsOne

query <- "select * from goods order by dan desc"
dbGetQuery(conn, query)

insert.db <- data.frame(code=5, name='식기 세척기', su=1, dan=250000)
dbWriteTable(conn, "goods", insert.db)  # 에러 이미 존재하는 테이블에 insert 안됨
dbWriteTable(conn, "goods1", insert.db) # 새로운 테이블 생성

query <- "select * from goods1"
goodsAll <- dbGetQuery(conn, query)
goodsAll
dbReadTable(conn, 'goods1')

# drop table
query <- "drop table goods2"
goodsAll <- dbGetQuery(conn, query)
query <- "drop table goods2"
goodsAll <- dbGetQuery(conn, query)
goodsAll

# read csv 그리고 테이블 생성
recorde <- read.csv("C:/Rexam/data/recode.csv")
dbWriteTable(conn, "goods2", recorde)
query <- "select * from goods2"
goodsAll <- dbGetQuery(conn, query)
goodsAll
dbReadTable(conn, 'goods2')

# insert
query <- "insert into goods2 values(6, 'test', 1, 1000)"
dbSendUpdate(conn, query)
query <- "select * from goods2"
goodsAll <- dbGetQuery(conn, query)
goodsAll
dbReadTable(conn, 'goods2')

# update
query <- "update goods2 set name ='테스트' where code = 6"
dbSendUpdate(conn, query)
query <- "select * from goods2"
goodsAll <- dbGetQuery(conn, query)
goodsAll
dbReadTable(conn, 'goods2')

# delete
delquery <- "delete from goods2 where code = 6"
dbSendUpdate(conn, delquery)
goodsAll <- dbGetQuery(conn, query)
goodsAll
dbReadTable(conn, 'goods2')

# disconnect DB
dbDisconnect(conn)



dbWriteTable(conn,"book",data.frame(bookname=c("파이썬 정복","하둡 완벽 입문","R 프로그래밍"),
                                    price=c(25000,25000,28000)))
dbGetQuery(conn, "SELECT * FROM book")

head(mtcars)
str(mtcars)
dbWriteTable(conn, "mtcars", mtcars[1:5, ])
dbReadTable(conn, "mtcars")

dbWriteTable(conn, "mtcars", mtcars[6:10, ], append = TRUE)
dbReadTable(conn, "mtcars")

dbWriteTable(conn, "mtcars", mtcars[1:2, ], overwrite = TRUE)
dbReadTable(conn, "mtcars")



dbWriteTable(conn,"cars",head(cars,3))
dbGetQuery(conn, "SELECT * FROM cars")


# 데이터 수정
dbSendUpdate(conn,"INSERT INTO cars(speed, dist) VALUES(1,1)")
dbSendUpdate(conn,"INSERT INTO cars(speed, dist) VALUES(2,2)")
dbReadTable(conn,"cars")
dbSendUpdate(conn,"UPDATE CARS SET DIST=DIST*100 WHERE SPEED = 1")
dbReadTable(conn,"cars")
dbSendUpdate(conn,"UPDATE CARS SET DIST=DIST*3 WHERE SPEED = 1")
dbReadTable(conn,"cars")

# 테이블 삭제
dbRemoveTable(conn,"cars")




# 데이터 전처리(1) - apply 계열의 함수를 알아보자
weight <- c(65.4, 55, 380, 72.2, 51, NA)
height <- c(170, 155, NA, 173, 161, 166)
gender <- c("M", "F","M","M","F","F")
# gender <- factor("M", "F" ,"M" ,"M" ,"F" ,"F")
str(gender)
df <- data.frame(w=weight, h=height)
df

apply(df, 1, sum, na.rm=TRUE)
apply(df, 2, sum, na.rm=TRUE)
lapply(df, sum, na.rm=TRUE)
sapply(df, sum, na.rm=TRUE)
tapply(1:6, gender, sum, na.rm=TRUE)
tapply(df$w, gender, mean, na.rm=TRUE)
mapply(paste, 1:5, LETTERS[1:5], month.abb[1:5])


v<-c("abc", "DEF", "TwT")
sapply(v, function(d) paste("-",d,"-", sep=""))

l<-list("abc", "DEF", "TwT")
sapply(l, function(d) paste("-",d,"-", sep=""))
lapply(l, function(d) paste("-",d,"-", sep=""))

flower <- c("rose", "iris", "sunflower", "anemone", "tulip")
length(flower)
nchar(flower)
sapply(flower, function(d) if(nchar(d) > 5) return(d))
sapply(flower, function(d) if(nchar(d) > 5) d)
sapply(flower, function(d) if(nchar(d) > 5) return(d) else return(NA))
sapply(flower, function(d) paste("-",d,"-", sep=""))

sapply(flower, function(d, n=5) if(nchar(d) > n) return(d))
sapply(flower, function(d, n=5) if(nchar(d) > n) return(d), n=7)
sapply(flower, function(d, n=5) if(nchar(d) > n) return(d), 4)

count <- 1
myf <- function(x, wt=T){
  print(paste(x,"(",count,")"))
#  Sys.sleep(3)
  if(wt) 
    r <- paste("*", x, "*")
  else
    r <- paste("#", x, "#")
  count <<- count + 1;
  return(r)
}
result <- sapply(df$w, myf)
result2 <- sapply(df$w, myf, F)

length(result)
result
sapply(df$w, myf, F)
sapply(df$w, myf, wt=F)
rr1 <- sapply(df$w, myf, wt=F)
str(rr1)

count <- 1
sapply(df, myf)
rr2 <- sapply(df, myf)
str(rr2)
rr2[1,1]
rr2[1,"w"]
```



### - 실습

```R
# (1) R이 내장하고 있는 iris 데이터셋의 구조와 상위 데이터 6개를 확인한다.
str(iris)
head(iris)

# (2) iris 데이터셋의 변수명을 다음과 같이 변경한다.
#변수명 : slength, swidth, plength, pwidth, species
colnames(iris) <- c('slength', 'swidth', 'plength', 'pwidth', 'species')
str(iris)

# (3) 변수명을 변경한 iris 를 MariaDB 서버에 iris 라는 테이블 명으로 저장한다.
library(rJava)
library(RJDBC)
library(DBI)

drv <- JDBC(driverClass = "org.mariadb.jdbc.Driver" ,"mariadb-java-client-2.6.2.jar")
conn <- dbConnect(drv, 'jdbc:mariadb://127.0.0.1:3303/work', 'scott', 'tiger')

dbWriteTable(conn, "iris", iris)
dbReadTable(conn, "iris")

# (4) iris 테이블의 모든 데이터를 읽어서 iris_all 에 저장한다.
query <- "select * from iris"
iris_all <- dbGetQuery(conn, query)
iris_all

# (5) iris 테이블에서 species 가 ‘setosa’ 인 데이터들만 추출하여 iris_setosa 에 저장한다.
query <- "select * from iris where species = 'setosa'"
iris_setosa <- dbGetQuery(conn, query)
iris_setosa


# (6) iris 테이블에서 species 가 ‘versicolor’ 인 데이터들만 추출하여 iris_versicolor 에 저장한다.
query <- "select * from iris where species = 'versicolor'"
iris_versicolor <- dbGetQuery(conn, query)
iris_versicolor


# (7) iris 테이블에서 species 가 ‘virginica’ 인 데이터들만 추출하여 iris_virginica 에 저장한다.
query <- "select * from iris where species = 'virginica'"
iris_virginica <- dbGetQuery(conn, query)
iris_virginica

# (8) "data/product_click.log" 데이터 파일을 읽어서 productdf 라는 데이터 프레임을 생성한다.
productdb <- read.table("data/product_click.log", stringsAsFactors = T)
str(productdb)

# (9) productdf 데이터셋의 변수명을 다음과 같이 변경한다.
# 변수명 : clicktime, pid
colnames(productdb) <- c('clicktime', 'pid')
str(productdb)

# (10) 변수명을 변경한 productdb 를 MariaDB 서버에 productlog 라는 테이블 명으로 저장한다.
dbWriteTable(conn, "productlog", productdb)
dbReadTable(conn, "productlog")

# (11) 상품 id  가 ‘p003’ 인 데이터들만 추출하여 p003 이라는 변수에 저장한다.
query <- "select * from productlog where pid = 'p003'"
p003 <- dbGetQuery(conn, query)
p003

# (12) "data/emp.csv" 데이터 파일을 읽어서 emp 라는 데이터 프레임을 생성한다.
emp <- read.csv("C:/Rexam/data/emp.csv")
emp$mgr; emp$comm
emp$mgr[which(is.na(emp$mgr))] <- '0000'
emp$comm[which(is.na(emp$comm))] <- 0
emp$mgr; emp$comm

# (13) emp 를 MariaDB 서버에 emp 라는 테이블 명으로 저장한다.
dbRemoveTable(conn, "emp")
dbWriteTable(conn, "emp", emp)
dbReadTable(conn, "emp")

# (14) emp 테이블에서 월급이 높은 순으로 데이터를 읽어와서 result1 에 저장한다.
query <- "select * from emp order by sal desc"
result1 <- dbGetQuery(conn, query)
result1

# (15) emp 테이블에서 입사한지 오래된 순으로 데이터를 읽어와서 result2 에 저장한다.
query <- "select * from emp order by hiredate "
result2 <- dbGetQuery(conn, query)
result2

# (16) emp 테이블에서 월급이 2000 이상인 데이터를 읽어와서 result3 에 저장한다.
query <- "select * from emp where sal >= 2000"
result3 <- dbGetQuery(conn, query)
result3

# (17) emp 테이블에서 월급이 2000 이상이고 3000 미만인 데이터를 읽어와서 result4 에 저장한다.
query <- "select * from emp where sal >= 2000 and sal < 3000"
result4 <- dbGetQuery(conn, query)
result4

# [ 문제 1 ]
v <- sample(1:26, 10)
v 
sapply(v, function(x) return (LETTERS[x]))
# [ 문제 2 ]

lines_memo <- readLines("data/memo.txt",encoding="UTF-8")
lines_memo <- lines_memo[nchar(lines_memo) > 0]
memo_new <- NULL

cline <- gsub("[&$!#@%]", "", lines_memo[1])
# gsub("[[:punct:]]", "", lines_memo[1]) 마침표도 날라감
memo_new <- append(memo_new, cline)

#cline <- gsub("[[:lower:]]", "[[:upper:]]", lines_memo[2]) #안되겠지..
cline <- gsub("e", "E", lines_memo[2])
memo_new <- append(memo_new, cline)

cline <- gsub("[[:digit:]]", "", lines_memo[3])
cline <- gsub("[0-9]", "", lines_memo[3])
cline <- gsub("\\d", "", lines_memo[3])
memo_new <- append(memo_new, cline)

cline <- gsub("[[:lower:][:upper:]]", "", lines_memo[4])
cline <- gsub("[A-z]", "", lines_memo[4])
memo_new <- append(memo_new, cline)

cline <- gsub("[!><0-9]", "", lines_memo[5])
memo_new <- append(memo_new, cline)

cline <- gsub(" ", "", lines_memo[6])
memo_new <- append(memo_new, cline)

cline <- gsub("YOU", "you", lines_memo[7])
cline <- gsub("OK", "ok", cline)
memo_new <- append(memo_new, cline)

write(memo_new,"data/memo_new.txt")


```


