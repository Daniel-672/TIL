

# Day2

> factor, summary, class, plot, levels, names, mean, colnames, rownames, read.csv. subset, print, cat, load, save, scan등

### - 교육내용

```R
getwd() #WorkingDirectory확인

# factor 실습

score <- c(1,3,2,4,2,1,3,5,1,3,3,3)
class(score)
summary(score)

f_score <- factor(score)
class(f_score)
f_score
summary(f_score)
levels(f_score)

plot(score)
plot(f_score)


data1 <- c("월","수","토","월",
           "목","화")
data1
class(data1)
summary(data1)
day1 <- factor(data1)
day1
class(day1)
summary(day1)
levels(day1)

week.korabbname <- c("일", "월", "화",
                     "수", "목", "금", "토")
day2 <- factor(data1, 
               levels=week.korabbname)
day2
summary(day2)
levels(day2)



btype <- factor(
  c("A", "O", "AB", "B", "O", "A"), 
  levels=c("A", "B", "O"))
btype
summary(btype)
levels(btype)

gender <- factor(c(1,2,1,1,1,2,1,2), 
                 levels=c(1,2), 
                 labels=c("남성", "여성"))
gender
summary(gender)
levels(gender)

# 내장 데이터셋
data()
iris; head(iris);tail(iris) 
View(iris)
str(iris)

f_iris <- factor(iris)
f_iris
#Dataframe 실습
no <- c(1,2,3,4)
name <- c('Apple','Banana','Peach','Berry')
qty <- c(5,2,7,9)
price <- c(500,200,200,500)
fruit <- data.frame(no, name, qty, price)
str(fruit)
View(fruit)

fruit[1,]
fruit[-1,]
fruit[,2]
fruit[,3] # fruit[,3, drop=F]
fruit[, c(3,4)]
fruit[3,2]
fruit[3,1:2] #fruit[3,1:2]

fruit[,3]
fruit$qty
fruit[[3]]
fruit[3]  # 데이터프레임 형식 유지

str(fruit$qty)
str(fruit[3])

# dataframe exam1
english <- c(90, 80, 60, 70)
math <- c(50, 60, 100, 20)
classnum <- c(1,1,2,2)
df_midterm <- data.frame(
  english, math, classnum)
df_midterm
str(df_midterm)
colnames(df_midterm)
rownames(df_midterm)
names(df_midterm)
mean(df_midterm$english)
mean(df_midterm$math)

df_midterm2 <- data.frame(
  c(90, 80, 60, 70), 
  c(50, 60, 100, 20), 
  c(1,1,2,2))
colnames(df_midterm2)
rownames(df_midterm2)
names(df_midterm2)
df_midterm2
df_midterm2 <- data.frame(
  영어=c(90, 80, 60, 70), 
  수학=c(50, 60, 100, 20), 
  클래스=c(1,1,2,2))
df_midterm2
df_midterm2$영어

df <- data.frame(var1=c(4,3,8), 
                 var2=c(2,6)) # 오류
df <- data.frame(var1=c(4,3,8), 
                 var2=c(2,6,1))
str(df)
df$var_sum <- df$var1 + df$var2
df$var_mean <- df$var_sum/2
df$result <- ifelse(df$var1>df$var2, 
                    "var1이 크다", "var1이 작다")

getwd() # setwd('xxx')

#csv파일열기
score <- read.csv("data/score.csv")
score
str(score)
score$sum <- 
  score$math+score$english+score$science
score$result <- ifelse(score$sum >= 200, 
                       "pass", "fail")
score

summary(score$result)
table(score$result)
summary(factor(score$result))
score$result = factor(score$result) 
str(score)
summary(score)
score$id = as.character(score$id)
score$class = factor(score$class)

score$grade<-ifelse(score$sum >= 230,"A",
                    ifelse(score$sum >= 215,"B", 
                           ifelse(score$sum >=200,"C","D")))
score

# order() 와 sort()
v <- c(10,3,7,4,8)
sort(v)
order(v)

emp <- read.csv(file.choose())
                #,stringsAsFactors = F)
emp
str(emp)

# emp에서 직원 이름
emp$ename
emp[,2]
emp[,"ename"] 
emp[,2, drop=FALSE] 
emp[,"ename",drop=F] 
emp[2]
emp["ename"] 

# emp에서 직원이름, 잡, 샐러리
emp[,c(2,3,6)]
emp[,c("ename","job","sal")]
subset(emp,select = c(ename, job, sal))
?subset
# emp에서 1,2,3 행 들만
emp[1:3,]
emp[c(1,2,3),]
?head
head(emp)
head(emp, n=1)
# ename이 "KING"인 직원의 모든 정보
emp[9,] 
emp$ename=="KING"
emp[c(F,F,F,F,F,F,F,F,T,F,F,F,
      F,F,F,F,F,F,F,F),]
emp[emp$ename=="KING",]
subset(emp,subset=emp$ename=="KING")
subset(emp,emp$ename=="KING") 



# 커미션을 받는 직원들의 모든 정보 출력
emp[!is.na(emp$comm),]
subset(emp,!is.na(emp$comm)) 
View(emp)
# select ename,sal from emp where sal>=2000
subset(emp, select=c("ename","sal"), 
       subset= emp$sal>= 2000)
subset(emp, emp$sal>= 2000, 
       c("ename","sal"))
emp[emp$sal>=2000,c("ename","sal")]

# select ename,sal from emp where sal between 2000 and 3000
subset(emp, select=c("ename","sal"), subset=(sal>=2000 & sal<=3000))
subset(emp, (sal>=2000 & sal<=3000), c("ename","sal"))

emp[emp$sal>=2000 & emp$sal <=3000, c("ename","sal")]


y <- c(0,25,50,75,100)
z <- c(50, 50, 50, 50,50)
y == z
y != z
y > z
y < z
y >= z
y <= z
y == 50 # c(50, 50, 50, 50, 50)
y > 50

num1 <- 11 # c(11)
num2 <- 3  # c(3)
num1 / num2
num1 %% num2
num1 %/% num2

y <- c(0,25,50,75,100)
z <- c(50, 50, 50, 50,50)
y == z
y != z
y > z
y < z
y >= z
y <= z
y == 50 # c(50, 50, 50, 50, 50)
y > 50

num1 <- 11 # c(11)
num2 <- 3  # c(3)
num1 / num2
num1 %% num2
num1 %/% num2

a[1]
a[[1]] # a[["a"]]
a$a
a[[1]][1]
a$a[1]
a[1]+1
a[[1]]+1
a[[1]][2] <- 100
new_a <- unlist(a[1])
a[1]; new_a
names(a) <- NULL
names(new_a) <- NULL

print(100)
print(pi)
data <- "가나다"
print(data)
print(data, quote=FALSE)
v1 <- c("사과", "바나나", "포도")
a = print(v1)
a
print(v1, print.gap=10)
cat(100)
cat(100,200)
cat(100,200,"\n")
cat("aaa", "bbb", "ccc", "ddd", "\n")
cat(v1, "\n")
cat(v1, sep="-", "\n")

print(paste("R", "은 통계분석", "전용 언어입니다."))
cat("R", "은 통계분석", "전용 언어입니다.", "\n")

ls()
length(ls())
save(list=ls(),file="all.rda") # varience will save in "all.rda" of rexam
rm(list=ls())
ls()
load("all.rda")
ls()

#read file data
nums <- scan("data/sample_num.txt"); nums
word_ansi <- scan("data/sample_ansi.txt",what="")
words_utf8 <- scan("data/sample_utf8.txt", what="",encoding="UTF-8")
words_utf8_new <- scan("data/sample_utf8.txt", what="")
lines_ansi <- readLines("data/sample_ansi.txt")
lines_utf8 <- readLines("data/sample_utf8.txt",encoding="UTF-8")

df2 <- read.table("data/product_click.log", stringsAsFactors = T)
str(df2)
head(df2)
tail(df2, 3)
summary(df2$V1)
summary(df2$V2)
```



### - 실습

```R
# 문제1
vec1 <- seq(10, 38, 2)
m1 <- matrix(vec1, nrow=3, ncol=5, byrow=T)
m2 <- m1 + 100
m_max_v <- max(m1)
m_min_v <- min(m1)
row_max <- apply(m1, 1, max)
col_max <- apply(m1, 2, max)

m1; m2; m_max_v; m_min_v; row_max; col_max

# 문제2
n1 <- c(1,2,3)
n2 <- c(4,5,6)
n3 <- c(7,8,9)
m2 <- cbind(c1, c2, c3)
m2

num <- c(n1, n2, n3)
num
mm2 = matrix(num, 3, nrow=3)

# 문제3
m3 <-matrix(1:9, nrow =3, byrow=T)
m3

# 문제4
m4 <- m3
rownames(m4) <- c("row1","row2","row3")
colnames(m4) <- c("col1","col2","col3")
m3; m4


# 문제5
alpha <- matrix(letters[1:6], nrow=2)
alpha2 <- rbind(alpha, letters[24:26])
alpha3 <- cbind(alpha, c('s','p'))
alpha; alpha2; alpha3

# 문제6
a <- array(1:24, dim=c(2,3,4)); a
a[2,3,4]
a[2, , ]
a[ ,1, ]
a[ , ,3]
a + 100
a[ , ,4] * 100
a[ 1, -1, ]; a[ 1, 2:3, ]; a[ 1, c(2,3), ]
a[ 2, , 2] <- a[ 2, , 2] + 100; a
a[ , , 1] <- a[ , , 1] - 2; a
a <- a * 10 ; a
rm(a); a

#Additional 실습
# 문제1
str(iris)

# 문제2
x <- seq(1, 5)
y <- x * 2
df1 <- data.frame(x, y)
df1

# 문제3
col1 <- seq(1, 5)
col2 <- letters[1:5]
col3 <- seq(6, 10)
df2 <- data.frame(col1, col2, col3)
df2

# 문제4
제품명 <- c("사과", "딸기", "수박")
가격 <- c(1800, 1500, 3000)
판매량 <- c(24, 38, 13)
df3 <- data.frame(제품명, 가격, 판매량)
df3

# 문제5
mean(df3$가격); mean(df3$판매량)

# 문제6
name <- c("Potter", "Elsa", "Gates", "Wendy", "Ben")
gender <- factor(c("M", "F", "M", "F", "M"))
math <- c(85, 76, 99, 88, 40)
df4 <- data.frame(name, gender, math)
str(df4)
df4$stat <- c(76, 73, 95, 82, 35); df4
df4$score <- df4$math + df4$stat ; df4
df4$grade <-ifelse(df4$score >= 150,"A",
                   ifelse(df4$score >= 100,"B", 
                          ifelse(df4$score >=70,"C","D"))); df4


# [문제7] emp변수에 할당된 데이터프레임 객체의 구조를 점검한다.
emp <- read.csv("data/emp.csv")
str(emp)

# [문제8] emp 에서 3행, 4행 , 5행만 출력한다.
emp
emp[3:5,]

# [문제9] emp 에서 사번열을 제외하고 출력한다.
emp[-4] ; emp[, -4] 

# [문제10] emp 에서 ename컬럼만 출력한다.
emp[,"ename",drop=F] 
emp[,2, drop=F] 

# [문제11] emp 에서 ename 과 sal컬럼만 출력한다.
emp[,c("ename","sal")]
subset(emp, ,c("ename","sal"))

# [문제12] 업무가 SALESMAN 인 사원의 이름, 월급, 직업을 출력한다.
subset(emp, job=="SALESMAN", c("ename", "sal", "job"))

# [문제13] 월급이 1000 이상이고 3000이하인 사원들의 이름, 월급, 부서번호를 출력한다.
subset(emp, sal >= 1000 & sal <= 3000, c("ename", "sal", "deptno"))

# [문제14] emp 에서 직업이 ANALYST 가 아닌 사원들의 이름, 직업, 월급을 출력한다.
emp[emp$job !="ANALYST", c("ename","job", "sal")]

# [문제15] emp 에서 업무가 SALESMAN 이거나 ANALYST 인 사원들의 이름, 직업을 출력한다.
emp[emp$job == "SALESMAN" | emp$job == "ANALYST", c("ename","job")]
emp[emp$job == c("SALESMAN", "ANALYST"), c("ename","job")] #테스트 왔다갔다?

# [문제16] emp 에서 커미션이 정해지지 않은 직원의 이름과 월급 정보를 출력한다.
subset(emp,is.na(emp$comm), c("ename","sal")) 

# [문제17] 월급이 적은 순으로 모든 직원 정보를 출력한다.
emp[order(emp$sal, decreasing = T),][1,]

order(emp$sal, decreasing = T)

# [문제18] emp의 행과 열의 갯수를 점검한다.
str(emp)
colnames(emp)
rownames(emp)
dim(emp)

```


