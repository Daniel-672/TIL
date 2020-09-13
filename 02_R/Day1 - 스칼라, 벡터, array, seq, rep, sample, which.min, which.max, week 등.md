

# Day1

> 스칼라, 벡터, array, seq, rep, sample, which.min, which.max, week 등

### - 교육내용

```R
v1 <- 1:10
v11 = 1:9
1:10 -> v111
print(v1, v11, v111)
v1

1:100
100:1

v2 <- v1 + 100

print(v2)

(v2 <- v1 + 100); v2

v3 <- v1 * 10; v3
ls()

v4 <- c(10, 5, 7, 4, 15, 1)

v5 <- c(100, 200, 300, '사백')

seq(1, 10)
seq(1, 10, 2)
seq(0, 100, 5)

rep(1, 100)
rep(1:3, 5)
rep(1:3, times=5) # 키워드 파라미터
rep(1:3, each=5)
?rep  #help()

LETTERS
letters
month.name
month.abb
pi

LETTERS;letters;month.name;month.abb;pi

LETTERS[1]; LETTERS[c(3,4,5)]
LETTERS[3:5]; LETTERS[5:3]; LETTERS[26:1]
LETTERS[-1]; LETTERS[c(-2,-4)]

length(LETTERS)
length(month.name)
length(pi)


x <- c(10,2,7,4,15)
x
print(x)
class(x)
rev(x)
range(x)
sort(x)
sort(x, decreasing = TRUE)
sort(x, decreasing = T)
#x <- sort(x)
order(x)



x[3] <- 20
x
x + 1
x <- x + 1
max(x);min(x);mean(x);sum(x)
summary(x)

x[c(2,4)] # x[2], x[4]
x[c(F,T,F,T,F)] # x[c(T,F)] 
x > 5
x[x > 5] 
x[x > 5 & x < 15] # x[x > 5 && x < 15]
#x[x > 5 | x < 15]

names(x)
names(x) <- LETTERS[1:5]
names(x) <- NULL
x[2];x["B"]; #x[B()]


# &, &&
c(T, T, F, F) & c(T, F, T, F)
c(T, T, F, F) | c(T, F, T, F)
c(T, T, F, F) && c(T, F, T, F)
c(T, T, F, F) || c(T, F, T, F)


ls()
rm(x)
x
class(x)

rainfall <- c(21.6, 23.6, 45.8, 77.0, 
              102.2, 133.3,327.9, 348.0, 
              137.6, 49.3, 53.0, 24.9)
rainfall > 100
rainfall[rainfall > 100]
which(rainfall > 100)
month.name[which(rainfall > 100)]
month.abb[which(rainfall > 100)]
month.korname <- c("1월","2월","3월",
                   "4월","5월","6월",
                   "7월","8월","9월",
                   "10월","11월","12월")
month.korname[which(rainfall > 100)]
which.max(rainfall)
which.min(rainfall)
month.korname[which.max(rainfall)]
month.korname[which.min(rainfall)]


sample(1:20, 3)
sample(1:45, 6)
sample(1:10, 7)
sample(1:10, 7, replace=T)

paste("I'm","Duli","!!")
paste("I'm","Duli","!!", sep="")
paste0("I'm","Duli","!!")

fruit <- c("Apple", "Banana", "Strawberry")
food <- c("Pie","Juice", "Cake")
paste(fruit, food)

paste(fruit, food, sep="")
paste(fruit, food, sep=":::")
paste(fruit, food, sep="", collapse="-")
paste(fruit, food, sep="", collapse="")
paste(fruit, food, collapse=",")


# matrix 실습
x1 <-matrix(1:8, nrow = 2)
x1
x1<-x1*3
x1

sum(x1); min(x1);max(x1);mean(x1)

x2 <-matrix(1:8, nrow =3)
x2

(chars <- letters[1:10])

mat1 <-matrix(chars)
mat1; dim(mat1)
matrix(chars, nrow=1)
matrix(chars, nrow=5)
matrix(chars, nrow=5, byrow=T)
matrix(chars, ncol=5)
matrix(chars, ncol=5, byrow=T)
matrix(chars, nrow=3, ncol=5)
matrix(chars, nrow=3)


vec1 <- c(1,2,3)
vec2 <- c(4,5,6)
vec3 <- c(7,8,9)
mat1 <- rbind(vec1,vec2,vec3); mat1
mat2 <- cbind(vec1,vec2,vec3); mat2
mat1[1,1]
mat1[2,];mat1[,3]
mat1[1,1,drop=F]
mat1[2,,drop=F];mat1[,3,drop=F]

rownames(mat1) <- NULL
colnames(mat2) <- NULL
mat1;mat2
rownames(mat1) <- c("row1","row2","row3")
colnames(mat1) <- c("col1","col2","col3")
mat1
ls()
mean(x2)
sum(x2)
min(x2)
max(x2)
summary(x2)

mean(x2[2,])
sum(x2[2,])
rowSums(x2); colSums(x2)

apply(x2, 1, sum); apply(x2, 2, sum)  
?apply
apply(x2, 1, max)
apply(x2, 1, min)
apply(x2, 1, mean)

apply(x2, 2, max)
apply(x2, 2, min)
apply(x2, 2, mean)

#Array 실습
a1 <- array(1:30, dim=c(2,3,5))
a1

a1[1,3,4]
a1[,,3]
a1[,2,]
a1[1,,]
a1[,2,]
```



### - 실습

```R
> # 문제1
> v1 <- 1:10
> v2 <- v1 * 2
> max_v <- max(v2)
> min_v <- min(v2)
> avg_v <- mean(v2)
> sum_v <- sum(v2)
> v3 <- v2[-5]
> v1; v2; v3; max_v; min_v; avg_v; sum_v;
 [1]  1  2  3  4  5  6  7  8  9 10
 [1]  2  4  6  8 10 12 14 16 18 20
[1]  2  4  6  8 12 14 16 18 20
[1] 20
[1] 2
[1] 11
[1] 110
> 
> # 문제2
> v4 <- seq(1, 10, 2)
> v5 <- rep(1, 5)
> v6 <- rep(1:3, 3)
> v7 <- rep(1:4, each=2)  
> 
> # 문제3
> nums <- sample(1:100, 10)
> sort(nums)
 [1] 14 20 35 54 57 59 63 71 79 99
> sort(nums, decreasing = T)
 [1] 99 79 71 63 59 57 54 35 20 14
> nums[nums >50]
[1] 99 63 59 79 54 57 71
> which(nums <= 50)
[1] 1 2 7
> which.max(nums)
[1] 3
> which.min(nums)
[1] 7
> 
> # 문제4
> v8 <- seq(1, 10, 3)
> names(v8) <- LETTERS[1:4]
> v8
 A  B  C  D 
 1  4  7 10 
> 
> # 문제5
> score <- sample(1:20, 5)
> myFriend <- c('둘리', '또치', '도우너', '희동', '듀크' )
> paste(score, myFriend, sep='-')
[1] "13-둘리"  "5-또치"   "7-도우너" "18-희동"  "14-듀크" 
> myFriend[which.max(score)]
[1] "희동"
> myFriend[which.min(score)]
[1] "또치"
> myFriend[which(score > 10)]
[1] "둘리" "희동" "듀크"
> 
> # 문제6
> count <- sample(1:100, 7)
> week.korname <- c('일요일', '월요일', '화요일', '수요일', '목요일', '금요일', '토요일')
> paste(week.korname, count, sep=':')
[1] "일요일:61" "월요일:14" "화요일:82" "수요일:15" "목요일:49" "금요일:39"
[7] "토요일:34"
> week.korname[which.max(count)]
[1] "화요일"
> week.korname[which.min(count)]
[1] "월요일"
> week.korname[which(count > 50)]
[1] "일요일" "화요일"
```


