

# Day17

> 회귀분석

### - 교육내용

```R
# 회귀분석 학습

options()
options(scipen=999)
# 학습 데이터 작성
x <- c(10, 22, 35, 40, 52, 64, 71, 83, 92, 100)
y <- c(41, 45, 62, 75, 85, 90, 110, 115, 125, 140)

# 선형관계 확인
plot(x, y, xlim=c(0, max(x)), ylim=c(0, max(y)))

# 초기치 설정
a         <- 25.5
b         <- 0.8
da        <- 0.1
db        <- 0.1
f.min    <- 1000000

# a, b 수정
A <- NULL
B <- NULL
F <- NULL
i <- 0

while(TRUE) { 
  i <- i + 1
  # 비용함수 f(a, b)
  err.sum <- 0
  for(k in 1:length(x)) {
    y_hat <- b*x[k] + a
    err   <- (y_hat - y[k])^2
    print(paste(k, "a, b: ", round(err, 1)))
    err.sum <- err.sum + err
  }
  f <- round(err.sum / 2, 1)    
  
  print(paste(i, "단계 #####", sep=""))
  print(paste("a = ", a, ", b = ", b, sep=""))
  print(paste("f.min = ", round(f.min, 1), ", f = ", round(f, 1), sep=""))
  
  # 종료여부 결정
  if (f >= f.min) {
    break 
  } else { 
    f.min <- f
    a.min <- a
    b.min <- b
  } 
  
  A <- c(A, a)
  B <- c(B, b)
  F <- c(F, f)
  
  # a의 변화와 비용함수 값, f(a+da, b)
  err.sum <- 0
  for(k in 1:length(x)) {
    y_hat <- b*x[k] + (a + da)
    err   <- (y_hat - y[k])^2
    print(paste(k, "a+da, b: ", round(err, 1)))
    err.sum <- err.sum + err
  }        
  f.da <- round(err.sum / 2, 1)    
  
  slope.da <- (f.da - f) / da
  print(paste("f.da = ", round(f.da, 1), ", slope.da = ", round(slope.da, 1), ", da = ", da, ", a = ", a, sep=""))
  
  da <- -sign(slope.da)*abs(da)
  
  # 비용함수 f(a, b+db)
  err.sum <- 0
  for(k in 1:length(x)) {
    y_hat <- (b + db)*x[k] + a
    err   <- (y_hat - y[k])^2
    print(paste(k, "a, b+db: ", round(err, 1)))
    err.sum <- err.sum + err
  }
  f.db <- round(err.sum / 2, 1) 
  
  slope.db <- (f.db - f) / db
  
  print(paste("f.db = ", round(f.db, 1), ", slope.db = ", round(slope.db, 1), ", db = ", db, ", b = ", b, sep=""))
  
  db <- -sign(slope.db)*abs(db)
  
  # a, b의 수정 
  a <- round(a + da, 2)
  b <- round(b + db, 2)
  
  print(paste("da = ", da, ", db = ", db, ", a = ", a, ", b = ", b, sep=""))
}

a.min
b.min

# 회귀선 그리기
plot(x, y, xlim=c(0, max(x)), ylim=c(0, max(y)))
abline(b=b.min, a=a.min, col="red", lty=2)

# 수리적 모형으로 해 구하기
lm(y~x)

# 비용 함수 값의 변화
par(mfrow = c(1,3))
plot(1:4, A, 
     xlab="반복 수", ylab="y절편", 
     main="y절편의 변화",
     type='o')
plot(1:4, B, 
     xlab="반복 수", ylab="기울기", 
     main="기울기의 변화",
     type='o')
plot(1:4, F, 
     xlab="반복 수", ylab="비용함수 값", 
     main="비용함수 값의 변화",
     type='o')
par(mfrow = c(1,1))

# 비용함수 값의 변화 (3차원 비교)
install.packages("scatterplot3d") 
library("scatterplot3d") # load
s3d <- scatterplot3d(x=A, y=B, z=F/1000,
                     pch=19,
                     cex.symbols=1.5,
                     color="steelblue",
                     type="h", 
                     main="비용함수의 변화",
                     xlab = "y절편",
                     ylab = "기울기",
                     zlab = "비용함수(X1000)")
text(s3d$xyz.convert(A, B, F/1000+0.3), 
     labels = 1:4,
     cex= 0.8, col = "red")

# 예측
x <- 30
y.hat <- b.min*x + a.min # 회귀방정식
y.hat

# R에 내장된 women 데이터셋으로 키에 따른 몸무게 예측 분석
# 학습 데이터 작성
str(women)
View(women)
x <- women$height
y <- women$weight

# 선형관계 확인
plot(x, y, xlab="키(in)", ylab="몸무게(lbs)")

plot(x, y, xlim=c(0, max(x)), ylim=c(0, max(y)),
     xlab="키(in)", ylab="몸무게(lbs)")

# 초기치 설정
a <- -90
b <- 3
da <- 0.01
db <- 0.01
f.min <- 100000

# a, b의 수정
A <- NULL
B <- NULL
F <- NULL
i <- 0
while(TRUE) {
  i <- i + 1
  
  # 비용함수 f(a, b)
  err.sum <- 0
  for(k in 1:length(x)) {
    y_hat <- b*x[k] + a
    err   <- (y_hat - y[k])^2
    #print(paste(k, "a, b: ", round(err, 1)))
    err.sum <- err.sum + err
  }
  f <- round(err.sum / 2, 1)      
  
  print(paste(i, "단계 #####", sep=""))
  print(paste("a = ", a, ", b = ", b, sep=""))
  print(paste("f.min = ", round(f.min, 1), ", f = ", round(f, 1), sep=""))
  
  # 종료여부 결정
  if (f >= f.min) {
    break 
  } else { 
    f.min <- f
    a.min <- a
    b.min <- b
  } 
  
  A <- c(A, a)
  B <- c(B, b)
  F <- c(F, f)
  
  # a의 변화와 비용함수 값, f(a+da, b)
  err.sum <- 0
  for(k in 1:length(x)) {
    y_hat <- b*x[k] + (a + da)
    err   <- (y_hat - y[k])^2
    #print(paste(k, "a+da, b: ", round(err, 1)))
    err.sum <- err.sum + err
  }        
  f.da <- round(err.sum / 2, 1)    
  
  slope.da <- (f.da - f) / da
  #print(paste("f.da = ", round(f.da, 1), ", slope.da = ", round(slope.da, 1), ", da = ", da, ", a = ", a, sep=""))
  
  da <- -sign(slope.da)*abs(da)
  
  # 비용함수 f(a, b+db)
  err.sum <- 0
  for(k in 1:length(x)) {
    y_hat <- (b + db)*x[k] + a
    err   <- (y_hat - y[k])^2
    #print(paste(k, "a, b+db: ", round(err, 1)))
    err.sum <- err.sum + err
  }
  f.db <- round(err.sum / 2, 1) 
  
  slope.db <- (f.db - f) / db
  
  print(paste("f.db = ", round(f.db, 1), ", slope.db = ", round(slope.db, 1), ", db = ", db, ", b = ", b, sep=""))
  
  db <- -sign(slope.db)*abs(db)
  
  # a, b의 수정 
  a <- round(a + da, 2)
  b <- round(b + db, 2)
  
  print(paste("da = ", da, ", db = ", db, ", a = ", a, ", b = ", b, sep=""))
}

a.min
b.min

# 회귀선 그리기
plot(x, y, xlab="키(in)", ylab="몸무게(lbs)")
abline(b=b.min, a=a.min, col="red", lty=2)

# 수리적 모형으로 해 구하기
lm(y~x)

# 비용함수 값의 변화
par(mfrow = c(1,3))
plot(1:length(A), A,
     xlab="반복 수", ylab="y절편",
     main="y절편의 변화",
     type='o')
plot(1:length(B), B,
     xlab="반복 수", ylab="기울기",
     main="기울기의 변화",
     type='o')
plot(1:length(F), F,
     xlab="반복 수", ylab="비용함수 값",
     main="비용함수 값의 변화",
     type='o')
par(mfrow = c(1,1))

# 비용함수의 변화 (3차원 비교)
# install.packages("scatterplot3d")
library(scatterplot3d)
s3d <- scatterplot3d(x=A, y=B, z=F/10000,
                     angle=30,
                     pch=21,
                     cex.symbols=1,
                     color="steelblue",
                     bg="yellow",
                     type="h",
                     main="비용함수의 변화",
                     xlab = "y절편",
                     ylab = "기울기",
                     zlab = "비용함수(X10,000)")
text(s3d$xyz.convert(A, B, F/10000+0.05),
     labels = c(1, rep(NA, length(A)-2), length(A)),
     cex= 0.8, col = "red")

# 예측
x <- 65
y.hat <- b.min*x + a.min # 회귀방정식
y.hat 






# R에 내장된 cars 데이터셋으로 자동차 속력에 따른 정지 거리 예측

str(cars)
View(cars)

x <- cars$speed
y <- cars$dist

# 선형관계 확인
plot(x, y, xlab="속력", ylab="정지 거리")




# 수리적 모형으로 해 구하기
cars.lm <- lm(y~x)
summary(cars.lm)
str(cars.lm)
names(cars.lm)
intercept <- cars.lm$coefficients[1]
slope <- cars.lm$coefficients[2]

# 회귀선 그리기
plot(x, y, xlab="키(in)", ylab="몸무게(lbs)")
abline(b=slope, a=intercept, col="red", lty=2)


# 예측
x <- 35
y.hat <- slope*x + intercept
y.hat 



fdata <- read.csv("data/factory.csv")
str(fdata)
detach(fdata)
#1.1 fdata의 산점도
plot(fdata$age, fdata$cost, xlab="사용연도", ylab="정비비용", pch=19, col="blue", cex.lab=1.5)
title("사용연도와 정비비용", cex.main=2, col.main="red") 

factory.lm <- lm(fdata$cost ~ fdata$age, data=fdata)
abline(factory.lm, col="red")

summary(factory.lm)

# 회귀 방정식으로 예측
13.637 * 4 + 29.107
predict(factory.lm, newdata=data.frame(age=4) )

names(factory.lm)
sum(factory.lm$residuals) # 잔차들의 합

cbind(fdata, factory.lm$residuals, factory.lm$fitted.values)

sum(fdata[,1]*factory.lm$residuals)
sum(factory.lm$fitted.values*factory.lm$residuals)


# 데이터들을 표준화 시켜서 

st_fdata <- cbind(fdata, st_age=(age-mean(age))/sd(age), st_cost=(cost-mean(cost))/sd(cost))
attach(st_fdata)
st_factory.lm <- lm(st_cost ~ st_age, data=st_fdata)  
plot(st_age, st_cost, xlab="사용연도", ylab="정비비용", pch=19, col="blue", cex.lab=1.5)
title("변수 표준화 후의 사용연도와 정비비용", cex.main=2, col.main="red") 
abline(st_factory.lm, col="red")
summary(st_factory.lm)
detach(st_fdata)
```



### - 실습

```R

```


