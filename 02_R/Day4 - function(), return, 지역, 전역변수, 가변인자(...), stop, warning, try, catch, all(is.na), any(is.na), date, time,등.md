

# Day4

> function(), return, 지역, 전역변수, 가변인자(...), stop, warning, try, catch, all(is.na), any(is.na), date, time,등

### - 교육내용

```R
# 함수 정의와 활용

func1 <- function() {
  xx <- 10   # 지역변수
  yy <- 20
  return(xx*yy)
}
func1()
#yy
result <- func1()
result
xx  # 오류발생


func2 <- function(x,y) {
  xx <- x
  yy <- y
  return(sum(xx, yy))
}

func2()  # 오류발생
func2(5,6) # 식 : 연산식, 호출식, 변수, 리터럴

func3 <- function(x,y) {
  #x3 <- x+1
  #y3 <- y+1
  x4 <- func2(x+1, y+1)  # 값(식) : 변수, 리터럴, 연산식, 호출식
  return(x4)
}

func3(9, 19)  # 30

func4 <- function(x=100, y=200, z) {
  return(x+y+z)
}
func4()
func4(10,20,30)
func4(x=1,y=2,z=3)
func4(y=11,z=22,x=33)
func4(z=1000)  

# 쉬트에 있는 함수 코드
#
f1 <- function() print("TEST")
f1()
r <- f1()
r       # return이 없음에도 TEST가 찍힘 f1 <- function() {print("TEST"); return()}
#

f2 <- function(num) {print("TEST"); print(num) }
f2(100)
f2()

f3<- function (p="R") print(p)
f3()
f3(p="PYTHON")
f3("java")

f4 <- function (p1="ㅋㅋㅋ",p2) for(i in 1:p2) print(p1)
f4(p1="abc", p2=3)
f4("abc", 3) 
f4(5) 
f4(p2=5) 

f5<- function(...) { print("TEST"); data <- c(...); print(length(data))}
f5(10, 20, 30)
f5("abc", T, 10, 20)

f6<- function(...) {
  print("수행시작")
  data <- c(...)
  for(item in data) {
    print(item)
  }
  return(length(data))
}
f6()
f6(10)
f6(10,20)
f6(10,20,30)
f6(10,'abc', T, F)
c(10,"abc", T, F, "T", "F")


f7<- function(...) {
  data <- c(...)
  sum <- 0;
  for(item in data) {
    if(is.numeric(item))
      sum <- sum + item
    else
      print(item)
  }
  return(sum)
}
f7(10,20,30)
f7(10,20,'test', 30,40)

f8<- function(...) {
  data <- list(...)
  sum <- 0;
  for(item in data) {
    if(is.numeric(item))
      sum <- sum + item
    else
      print(item)
  }
  return(sum)
}

f8(10,20,30)
f8(10,20,"test", 30,40)



f9 <- function(p1, ..., p2="ㅋ") {
  cat("p1=", p1, "\n")
  cat("가변형 = ", ..., "\n")
  cat("p2=", p2, "\n")
}

f9()   # Error
f9(10)
f9(10,20)
f9(10,20,30)
f9(10,20,30,40)
f9(10,20,30,40,p2=50)
f9(10,20,30,40,p1=50, p2=60)


x <- 70
func5 <- function() {
  x <- 10
  y <- 20
  x <<- 40  # 외부 변수 x 를 수정
  return (x+y)
}
func5()  
x
y

#전역변수/지역변수
a<-3;b<-7;c<-11 
ft<-function(a){
  b<-a+10     
  c<<-a+10   # 전역대입연산 
  d<-a
  print(a);print(b);print(c);print(d)
  return()  # NULL
}
print(ft(100))
print(a);print(b);print(c);print(d) 

#invisible()함수 

ft.1 <- function(x) return()
ft.2 <- function(x) return(x+10)
ft.3 <- function(x) invisible(x+10)

ft.1(100)
ft.2(100)
ft.3(100)

r1 <- ft.1(1000);r1
r2 <- ft.2(1000);r2
r3 <- ft.3(1000);r3


testParamType <- function(x){
  if(is.vector(x)) print("벡터를 전달했군요!")
  if(is.data.frame(x)) print("데이터프레임을 전달했군요!")
  if(is.list(x)) print("리스트를 전달했군요!")
  if(is.matrix(x)) print("매트릭스를 전달했군요!")
  if(is.array(x)) print("배열을 전달했군요!")
  if(is.function(x)) print("함수를 전달했군요!")
}
#dataframe이 list에, list는 vector에 포함 됨 
#list는 원소 1개 짜리 1차원 배열과 같다.
testParamType(100)
testParamType(LETTERS)
testParamType(data.frame())
testParamType(matrix())
testParamType(list())
testParamType(array())
testParamType(mean)


#testParamType
testParamType1 <- function(x){
  result <- NULL
  if(is.vector(x)  && !is.list(x)) result <-"벡터를 전달했군요!"
  else if(is.data.frame(x)) result <- "데이터프레임을 전달했군요!"
  else if(is.list(x)) result <- "리스트를 전달했군요!"
  else if(is.matrix(x)) result <- "매트릭스를 전달했군요!"
  else if(is.array(x)) result <- "배열을 전달했군요!"
  else if(is.function(x)) result <- "함수를 전달했군요!"
  return(result)
}

#dataframe이 list에, list는 vector에 포함 됨 #list는 원소 1개 짜리 1차원 배열과 같다.....?

testParamType1(100)
testParamType1(LETTERS)
testParamType1(data.frame())
testParamType1(matrix())
testParamType1(list())
testParamType1(array())
testParamType1(function(){})

#stop() 함수
testError1 <- function(x){
  if(x<=0)
    stop("양의 값만 전달 하숑!! 더 이상 수행 안할거임..")
  return(rep("테스트",x))
}

testError1(5)
testError1(0)



#warning() 함수
testWarn <- function(x){
  if(x<=0)
    stop("양의 값만 전달 하숑!! 더 이상 수행 안할거임..")
  if(x>5){
    x<-5
    warning("5보다 크면 안됨!! 하여 5로 처리했삼...!!")
  }
  return(rep("테스트",x))
}


testWarn(3)
testWarn(10)

test1 <-function(p){
  cat("난 수행함\n")
  testError1(-1)
  cat("나 수행할 까요? \n")
}
test1()

#try()
test2 <- function(p){
  cat("난 수행함\n")
  try(testError(-1))
  cat("나 수행할 까요? \n")
}
test2()

testAll <-function(p){
  tryCatch({
    if(p=="오류테스트"){
      testError1(-1)
    }else if (p =="경고테스트"){
      testWarn(6)
    }else{
      cat("정상 수행..\n")
      print(testError1(2))
      print(testWarn(3))
    }
  },warning = function(w){
    print(w)
    cat("-.-;;\n")
  },error = function(e){
    print(e)
    cat("ㅠㅠ \n")
  },finally ={
    cat("오류, 경고 발생 여부에 관계없이 반드시 수행되는 부분입니다요..\n")
  })
}

testAll("오류테스트")
testAll("경고테스트")
testAll("아무거나")


f.case1 <- function(x) {
  if(is.na(x)) 
    return("NA가 있슈")
  else
    return("NA가 없슈")
}
f.case1(100)
f.case1(NA)
f.case1(1:6)
f.case1(c(10,20,30))
f.case1(c(NA, 20))
f.case1(c(10, NA, 20))

f.case2 <- function(x) {
  if(any(is.na(x))) 
    return("NA가 있슈")
  else
    return("NA가 없슈")
}
f.case2(100)
f.case2(NA)
f.case2(1:6)
f.case2(c(10,20,30))
f.case2(c(NA, 20))
f.case2(c(10, NA, 20))

f.case3 <- function(x) {
  if(all(is.na(x))) 
    return("모두 NA임")
  else
    return("모두 NA인 것은 아님")
}
f.case3(100)
f.case3(LETTERS)
f.case3(NA)
f.case3(c(NA, NA, NA))
f.case3(c(NA, NA, 10))


#Sys.sleep(초시간) 함수
testSleep <- function(x) {
  for(data in 6:10) {       
    cat(data,"\n")
    if(x)
      Sys.sleep(1)
  }
  return()
}
testSleep(FALSE)
testSleep(TRUE)




# 가변형 인자 테스트
funcArgs <- function(...) {
  p <- c(...)
  data <- 1:10
  #opts <- ifelse(length(p)>0, p, "")
  if(length(p) > 0)
    opts <- p
  else
    opts <- ""
  print(p)
  print(opts)
  if(opts[1] == "")
    print(data)
  else 
    for(opt in opts) {
      switch(EXPR=opt,
             SUM=, Sum=, sum= print(sum(data)),
             MEAN=, Mean=, mean= print(mean(data)),
             DIFF=, Diff=, diff= print(max(data) - min(data)),
             MAX=, Max=, max= print(max(data)),
             MIN=, Min=, min= print(min(data)),
             SORT=, Sort=, sort= print(sort(data))
      )
    }
}

funcArgs()
funcArgs("SUM", "mean", "Min")




# 날짜와 시간 관련 기능을 지원하는 함수들

(today <- Sys.Date())
format(today, "%Y년 %m월 %d일%")
format(today, "%d일 %B %Y년")
format(today, "%y")
format(today, "%Y")
format(today, "%B")
format(today, "%a")
format(today, "%A")
weekdays(today) 
months(today) 
quarters(today)
unclass(today)  # 1970-01-01을 기준으로 얼마나 날짜가 지났지는 지의 값을 가지고 있다.
Sys.Date()
Sys.time()
Sys.timezone()

as.Date('1/15/2018',format='%m/%d/%Y') # format 은 생략 가능
as.Date('4월 26, 2018',format='%B %d, %Y')
as.Date('110228',format='%d%b%y') 

x1 <- "2019-01-10 13:30:41"
# 문자열을 날짜형으로
as.Date(x1, "%Y-%m-%d %H:%M:%S") 
# 문자열을 날짜+시간형으로
strptime(x1, "%Y-%m-%d %H:%M:%S")
strptime('2019-08-21 14:10:30', "%Y-%m-%d %H:%M:%S")

x2 <- "20200601"
as.Date(x2, "%Y%m%d")
datetime<-strptime(x2, "%Y%m%d")
str(datetime)

as.Date("2020/01/01 08:00:00") - as.Date("2020/01/01 05:00:00")
as.POSIXct("2020/01/01 08:00:00") - as.POSIXct("2020/01/01 05:00:00")
as.POSIXlt("2020/01/01 08:00:00") - as.POSIXlt("2020/01/01 05:00:00")

t<-Sys.time()
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

as.POSIXlt("2020/12/25")$wday
as.POSIXlt("2020/12/25")$wday
as.POSIXlt("2020/12/25")$wday
as.POSIXlt("2020/12/25")$wday
as.POSIXlt("2020/12/25")$wday

#즉석실습
#내가 태어난 요일 출력하기
myday<-as.POSIXlt("2020-10-31")
weekdays(myday)
#내가 태어난지 며칠
as.POSIXlt(Sys.Date()) - myday
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


```



### - 실습

```R
# [ 문제 1 ]
exam1 <- function(){
  return(paste(LETTERS, letters, sep=""))
}
print(exam1())


# [ 문제 2 ]
exam2 <- function(inNum1){
  if(is.numeric(inNum1)){
    sumAmt <- 0
    for(i in 1:inNum1){
      sumAmt <- sumAmt + i
    }
    return(sumAmt)
  }else{
    return('숫자 하나만... ')
  }
}
print(exam2(10))
print(exam2('10'))


# [ 문제 3 ]
exam3 <- function(inNum1, inNum2){
  if(is.numeric(inNum1) && is.numeric(inNum2)){
    diffNum <- abs(inNum1 - inNum2)
    return(diffNum)
  }else{
    return('숫자 두개 만... ')
  }
}
print(exam3(10, 20))
print(exam3(20, 10))
print(exam3('10', 20))
print(exam3(20, '10'))
print(exam3('20','10'))

exam3_1 <- function(inNum1, inNum2){
  if(is.numeric(inNum1) && is.numeric(inNum2)){
    if ((inNum1 - inNum2) == 0){
      diffNum <- 0
    } else if ((inNum1 - inNum2) > 0){
      diffNum <- inNum1 -inNum2
    } else {
      diffNum <- inNum2 -inNum1
    }
    return(diffNum)
  }else{
    return('숫자 두개 만... ')
  }
}
print(exam3_1(10, 20))
print(exam3_1(20, 10))
print(exam3_1('10', 20))
print(exam3_1(20, '10'))
print(exam3_1('20','10'))

# [ 문제 4 ]
exam4 <- function(inNum1, inOpr, inNum2){
  if(is.numeric(inNum1) && is.numeric(inNum2)){                 #숫자정상
    if(switch(EXPR = inOpr,"SUM"=, "+"=,"-"=,"*"=,"%/%"=,"%%"= F, T)){ #OP이상
      return("규격의 연산자만 전달하세요")
    }else if(switch(EXPR = inOpr, "%/%"=,"%%"= T, F)) {         #OP중 0사용이상
      if (inNum1 == 0){                                         #OP중 0사용앞뒤확인
        return("오류1")
      } else if (inNum2 == 0){
        return("오류2")
      } 
    }
                                                                #여기부턴 숫자 OP 다 정상
    result <- switch(EXPR = inOpr, SUM=inNum1+inNum2,"-"=inNum1-inNum2,"*"=inNum1*inNum2,"%/%"=inNum1%/%inNum2,"%%"=inNum1%%inNum2)
    return(result)
  }else{                                                         #숫자이상
    return('숫자 이상... ')
  }
}

print(exam4(100, "SUM", 10))
print(exam4(100, "+", '10'))
print(exam4('100', "+", '10'))

print(exam4(100, "&", 10))

print(exam4(0, "%/%", 10))
print(exam4(0, "%%", 10))

print(exam4(100, "%/%", 0))
print(exam4(100, "%%", 0))

print(exam4(100, "+", 10))
print(exam4(100, "-", 10))
print(exam4(100, "*", 10))
print(exam4(100, "%/%", 10))
print(exam4(100, "%%", 10))
print(exam4(100, "%%", 9))


# [ 문제5 ]
exam5 <- function(inNum1, deco="#"){
  if(is.numeric(inNum1)){
    if(inNum1 > 0) {
      cat(rep(deco, inNum1), "\n")
    } else {
      cat("", "\n")
    }
  }else{
    return('숫자 이상... ')
  }
  return()
}

print(exam5(10,"*"))
exam5(10)
exam5(-10,"*")


# [ 문제6 ]
exam6 <- function(...) {
  #inScoreList <- c(...)
  #inScoreList <- list(...)[[1]]
  inScoreList <- unlist(list(...))
  for(score in inScoreList) {
    if(!is.na(score)) {
      grade <- switch(EXPR = ifelse(score >= 85,1,
                                ifelse(score >= 70,2, 
                                    ifelse(score < 69,3,4)))
                      ,"상","중","하","에러")
      print(paste(score, " 점은 ", grade, '등급 입니다.',sep=""))
    }else{
      print("NA 는 처리불가")
    }
  }
  return()
}


exam6(c(80, 50, 70, 66, NA, 35)) # 이경우 리스트로 받으면 [[1]]

exam6(80, 50, 70, 66, NA, 35) 





options("digits") # 현재 설정된 유효 숫자 범위 

```


