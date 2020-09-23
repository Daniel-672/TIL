

# Day11

> 데이터 전처리(date, time, string처리)

### - 교육내용

```R
# 데이터 전처리(2) - 날짜와 시간 관련 기능을 지원하는 함수들

(today <- Sys.Date()); str(today)
format(today, "%Y년 %m월 %d일")
format(today, "%Y년%m월")
format(today, "%d일 %B %Y년")
format(today, "%y")
format(today, "%Y")
format(today, "%B")
format(today, "%b")
format(today, "%m")
format(today, "%a")
format(today, "%A")
weekdays(today) 
months(today) 
quarters(today)
unclass(today)  # 1970-01-01을 기준으로 얼마나 날짜가 지났지는 지의 값을 가지고 있다.
Sys.Date()
Sys.time()
Sys.timezone()

as.Date("2019-01-10") 
as.Date('1/15/2018',format='%m/%d/%Y') # format 은 생략 가능
as.Date('4월 26, 2018',format='%B %d, %Y')
as.Date('110228',format='%d%m%y') 
as.Date('11228',format='%d%b%y') 

x1 <- "2019-01-10 13:30:41"
# 문자열을 날짜형으로
as.Date(x1, "%Y-%m-%d %H:%M:%S") 
# 문자열을 날짜+시간형으로
strptime(x1, "%Y-%m-%d %H:%M:%S")
str(strptime(x1, "%Y-%m-%d %H:%M:%S"))  #POSIXlt형
strptime('2019-08-21 14:10:30', "%Y-%m-%d %H:%M:%S")

x2 <- "20200601"
as.Date(x2, "%Y%m%d")
datetime<-strptime(x2, "%Y%m%d")
str(datetime)

as.Date("2020/01/01 08:00:00") - as.Date("2020/01/01 05:00:00")
as.POSIXct("2020/01/01 08:00:00") - as.POSIXct("2020/01/01 05:00:00")
as.POSIXlt("2020/01/01 08:00:00") - as.POSIXlt("2020/01/01 05:00:00")

t<-Sys.time(); str(t)   #POSIXct형
ct<-as.POSIXct(t)
lt<-as.POSIXlt(t)
str(ct) 
str(lt) 
unclass(ct) 
unclass(lt) 
lt$mon+1
lt$hour
lt$year+1900
as.POSIXct(1449894438,origin="1970-01-01")
as.POSIXlt(1449894438,origin="1970-01-01")
as.POSIXlt(1600823984,origin="1970-01-01")

as.POSIXlt("2020/12/25")$wday
as.POSIXlt("1974/02/26")$wday
as.POSIXlt("2020/09/23")$wday
as.POSIXlt("2020/09/24")$wday
as.POSIXlt("2020/09/25")$wday


#올해의 크리스마스 요일 2가지방법(요일명,숫자)
christmas2<-as.POSIXlt("2020-12-25")
weekdays(christmas2)
christmas2$wday
#2020년 1월 1일 어떤 요일
tmp<-as.POSIXct("2020-01-01")
weekdays(tmp)
#오늘은 xxxx년x월xx일x요일입니다 형식으로 출력
tmp<-Sys.Date()
year<-format(tmp,'%Y')
month<-format(tmp,'%m')
day<-format(tmp,'%d')
weekday<-format(tmp,'%A')
paste("오늘은 ",year,"년 ",month,"월 ",day,"일 ",weekday," 입니다.",sep="")

format(tmp,'오늘은 %Y년 %B %d일 %A입니다')

# 데이터 전처리(3) - 문자열 처리 관련 주요 함수들 

x <- "We have a dream"
nchar(x)
length(x)

y <- c("We", "have", "a", "dream", "ㅋㅋㅋ")
length(y)
nchar(y)

letters
sort(letters, decreasing=TRUE)

fox.says <- "It is only with the HEART that one can See Rightly"
tolower(fox.says)
toupper(fox.says)

substr("Data Analytics", start=1, stop=4)
substr("Data Analytics", 6, 14)
substring("Data Analytics", 6); substring("Data Analytics", 6, 14)
substring(x, 1, 5) <- c("..", "+++")


classname <- c("Data Analytics", "Data Mining", 
               "Data Visualization")
substr(classname, 1, 4)

countries <- c("Korea, KR", "United States, US", 
               "China, CN")
substr(countries, nchar(countries)-1, nchar(countries))

head(islands)
landmesses <- names(islands)
landmesses
grep(pattern="New", x=landmesses)

index <- grep("New", landmesses)
landmesses[index]

# 동일
grep("New", landmesses, value=T)


txt <- "Data Analytics is useful. Data Analytics is also interesting."
sub(pattern="Data", replacement="Business", x=txt)
gsub(pattern="Data", replacement="Business", x=txt)

x <- c("test1.csv", "test2.csv", "test3.csv", "test4.csv")
gsub(".csv", "", x)


gsub("[ABC]", "@", "123AunicoBC98ABC")
gsub("ABC", "@", "123AunicoBC98ABC")
gsub("(AB)|C", "@", "123AunicoBC98ABC")
gsub("A|(BC)", "@", "123AunicoBC98ABC")
gsub("A|B|C", "@", "123AunicoBC98ABC")

words <- c("ct", "at", "bat", "chick", "chae", "cat", 
           "cheanomeles", "chase", "chasse", "mychasse", 
           "cheap", "check", "cheese", "hat", "mycat")

grep("che", words, value=T)
grep("at", words, value=T)
grep("[ch]", words, value=T)
grep("[at]", words, value=T)
grep("ch|at", words, value=T)
grep("ch(e|i)ck", words, value=T)
grep("chase", words, value=T)
grep("chas?e", words, value=T)
grep("chas*e", words, value=T)
grep("chas+e", words, value=T)
grep("ch(a*|e*)se", words, value=T)
grep("^c", words, value=T)      # c로 시작하는 단어
grep("t$", words, value=T)      # t로 끝나는 단어
grep("^c.*t$", words, value=T)  # .특정문자 .* 특정문자가 여러개

words2 <- c("12 Dec", "OK", "http//", 
            "<TITLE>Time?</TITLE>", 
            "12345", "Hi there")

grep("[[:alnum:]]", words2, value=TRUE)
grep("[[:alpha:]]", words2, value=TRUE)
grep("[[:digit:]]", words2, value=TRUE)
grep("[[:punct:]]", words2, value=TRUE)
grep("[[:space:]]", words2, value=TRUE)
grep("\\w", words2, value=TRUE)
grep("\\d", words2, value=TRUE); grep("\\D", words2, value=TRUE)
grep("\\s", words2, value=TRUE)



fox.said <- "What is essential is invisible to the eye"
fox.said
strsplit(x= fox.said, split= " ")
strsplit(x= fox.said, split="")

fox.said.words <- unlist(strsplit(fox.said, " "))
fox.said.words
fox.said.words <- strsplit(fox.said, " ")[[1]]
fox.said.words
fox.said.words[3]
p1 <- "You come at four in the afternoon, than at there I shall begin to the  happy"
p2 <- "One runs the risk of weeping a little, if one lets himself be tamed"
p3 <- "What makes the desert beautiful is that somewhere it hides a well"
littleprince <- c(p1, p2, p3)
strsplit(littleprince, " ")
strsplit(littleprince, " ")[[3]] 
strsplit(littleprince, " ")[[3]][5]
unlist(strsplit(littleprince, " "))


```



### - 실습

```R
# 문제 1
cname <- '김유철'
weekDayBirth <- format(as.Date("19740226", "%Y%m%d"), "%a")

resultStr <- paste(cname, " 은 ", weekDayBirth, "요일에 태어났어요",sep="")
resultStr


# 문제 2
todayStr <- format(Sys.Date(),'오늘은 %Y년 %m월 %d일 이고')

diffday <- Sys.Date() - as.Date("19740226", "%Y%m%d")
#str(diffday)
#units(diffday) # attr을 보여줌
livedDays <- unclass(diffday)[1]

resultStr <- paste(todayStr, " 내가 태어난지 ", livedDays, "일째되는 날이당",sep="")
resultStr


# 문제 3
resultStr <- format(Sys.time(),'%Y년 %m월 %d일 %H시 %M분 %S초')
resultStr


# 문제 4
datetime <- c('12/25/2020 23:59:59', '1/25/2021 23:59:59', '2/25/2021 23:59:59')
datetimeDf <- data.frame(datetime)
POSIXltList <- strptime(datetimeDf$datetime, format="%m/%d/%Y %H:%M:%S")
POSIXltList
str(POSIXltList)


# 문제 5
oneWeek <- seq(as.Date("2020-06-01"), as.Date("2020-06-07"), 1)
resultStr <-paste(format(oneWeek,'%A'),format(oneWeek,'%m%d'),sep="-")
resultStr


# 문제 6
v1 <- c('Happy', 'Birthday', 'to', 'You')
length(v1)
sum(nchar(v1))


# 문제 7
resultStr <- paste(v1, collapse = " ")
resultStr
length(resultStr)
nchar(resultStr)


# 문제 8
vRange <- seq(1, 10)
resultStr1 <- paste(LETTERS[vRange], vRange, sep = " ")
resultStr2 <- paste(LETTERS[vRange], vRange, sep = "")
resultStr1; resultStr2


# 문제 9
vStr <- 'Good Morning'
vunlistStr <- unlist(strsplit(vStr, " "))
resultStr <- strsplit(vunlistStr, " ")    # list(vunlistStr)
resultStr


# 문제 10
vStr <- c("Yesterday is history, tommrrow is a mystery, today is a gift!", 
          "That's why we call it the present - from kung fu Panda")

vStr <- gsub("[,-]", "", vStr)
vStr <- unlist(strsplit(vStr, " "))
resultStr <- svStr[nchar(vStr) > 0]
resultStr


# 문제 11
ssn  <- c("941215-1234567", "850605-2345678", "760830-1357913")

masking <- function(x) {
  sx <- substr(x, 1, 7)
  result <- paste(sx, "*******", sep='')
  return(result)
}

resultStr <- sapply(ssn, masking)
resultStr


# 문제 12
s1 <- "@^^@Have a nice day!! 좋은 하루!! 오늘도 100점 하루...."

r1 <- gsub("[가-힣]", "", s1) 
r2 <- gsub("[[:punct:]]", "", s1) 
r3 <- gsub("[가-힣][:punct:]", "", s1)    # 안됨 ㅠㅠ
r3p <- gsub("[가-힣]", "", s1) 
r3 <- gsub("[[:punct:]]", "", r3p)
r4 <- gsub("100", "백", s1)
s1; r1; r2; r3; r4



```


