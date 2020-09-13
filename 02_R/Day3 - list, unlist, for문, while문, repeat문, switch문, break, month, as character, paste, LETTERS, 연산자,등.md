

# Day3

> list, unlist, for문, while문, repeat문, switch문, break, month, as character, paste, LETTERS, %%, %/%, / 등

### - 교육내용

```R
#LIST
v<-c(1,2,3)
l<-list(1,2,3) 
as.character(str(v))
l
v[1] 
l[2] 
l[[2]] 

lds <- list(1,2,3) 
lds
lds+100
unlist(lds)
unlist(lds)+100
lds[1]
lds[1]+10
lds[[1]]+10

names(lds) <- LETTERS[1:3]
lds
lds[[2]]
lds[["B"]]
lds$B


a<-list(
  a = 1:3,
  b = "a string",
  c = pi,
  d = list(-1,-5)
)


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

cat('A', 'B')

# 제어문
for(data in month.name) 
  print(data)

for(data in month.name) 
  cat(data, sep="\n")

sum <- 0
for(i in 5:15){
  if(i%%10==0){   #나머지연산
    break
  }
  sum <- sum + i
  print(paste(i,":",sum))
}

sum <- 0
for(i in 5:15){
  if(i%%10==0){
    break
  }
  sum <- sum + i
  cat(i,":",sum,"\n")
}

sum <-0
for(i in 5:15){
  if(i%%10==0){
    next;  #continue
  }
  sum <- sum + i
  print(paste(i,":",sum))
}

sumNumber <- 0
while(sumNumber <= 20) { 
  i <- sample(1:5, 1) 
  sumNumber <-sumNumber+i; 
  cat("i :", i, ", sumNumber :", sumNumber,"\n")
} 

i <-0
repeat {
  cat("ㅋㅋㅋ\n")
  i = i + 1
  if(i==10)
    break
}


sumNumber <- 0
repeat { 
  i <- sample(1:5, 1) 
  sumNumber <-sumNumber+i; 
  cat(sumNumber,"\n")
  if(sumNumber > 20)
    break;
}

#제어문
#if else
randomNum <-sample(1:10,1)
if(randomNum>5){
  cat(randomNum,":5보다 크군요","\n")
}else{
  cat(randomNum,":5보다 작거나 같군요","\n")
}

if(randomNum%%2 == 1){
  cat(randomNum,";홀수\n")
}else{
  cat(randomNum,";짝수","\n")
}


if(randomNum%%2 == 1){
  cat(randomNum,";홀수","\n")
}else{
  cat(randomNum,";짝수","\n")
}

(score <- sample(0:100, 1))  # 0~100 숫자 한 개를 무작위로 뽑아서
if (score >=90){
  cat(score,"는 A등급입니다","\n")
}else if (score >=80){
  cat(score,"는 B등급입니다","\n")
}else if (score >=70){
  cat(score,"는 C등급입니다","\n")
}else if (score >=60){
  cat(score,"는 D등급입니다","\n")
}else {
  cat(score,"는 F등급입니다","\n")
}
class(score)

#for문
#for 실습
for(data in month.name) 
  print(data)
for(data in month.name)print(data);print("ㅋㅋ")
for(data in month.name){print(data);print("ㅋㅋ")}

for(n in 1:5)
  cat("hello?","\n")

for(i in 1:5){
  for(j in 1:5){
    cat("i=",i,"j=",j,"\n")
  }
}
# 구구단
for(dan in 1:9){
  for(num in 1:9){
    cat(dan,"x",num,"=",dan*num,"\n") # \n : 개행문자, \t : 탭문자
  }
  cat("\n")
}


for(i in 1:9){
  for(j in 1:9){
    if(i*j>30){
      break
    } 
    cat(i,"*",j,"=",i*j,"\n")
  }
  cat("\n")
}

bb <- F
for(i in 1:9){
  for(j in 1:9){
    if(i*j>30){
      bb<-T
      break
    } 
    cat(i,"*",j,"=",i*j,"\n")
  }
  cat("\n")
  if(bb) #bb가 TRUE이면
    break
}

#while문
i<-1
while(i <= 10){
  cat(i,"\n")
  i <- i+1
}
cat("종료 후 :",i,"\n")

i<-1
while (i<=10) {
  cat(i,"\n"); i <- i+1
}

i<-1
while (i<=10) {
  cat(i,"\n")
  i<-i+2
}

i<-1
while (i<=10) {
  cat(i,"\n")
  i<-i+1
}

#switch 문을 대신하는 함수
month <- sample(1:12,1)
month <- paste(month,"월",sep="") # "3월"  "3 월"
result <- switch(EXPR=month,
                 "12월"=,"1월"=,"2월"="겨울",
                 "3월"=,"4월"=,"5월"="봄",
                 "6월"=,"7월"=,"8월"="여름",
                 "가을")
cat(month,"은 ",result,"입니다\n",sep="")

num <- sample(1:10,1)
num
switch(EXPR = num,"A","B","C","D")

for(num in 1:10){
  cat(num,":",switch(EXPR = num,"A","B","C","D"),"\n")
}

for(num in 1:10){
  num <- as.character(num) 
  cat(num,":",switch(EXPR = num,
                     "7"="A","8"="B","9"="C","10"="D","ㅋ"),"\n")
}



```



### - 실습

```R
# [문제1]
L1 <- list(name = "scott", sal = 3000)
result <- L1$sal * 2
result



# [문제2]
L2 <- list("scott", c(100, 200, 300))
L2

# [문제3]
L3 <- list(c(3,5,7), c("A", "B", "C")); L3
L3[[2]][1] <- "Alpha"; L3

# [문제4]
L4 <- list(alpha=0:4, beta=sqrt(1:5), gamma=log(1:5))
L4$alpha + 10
L4[[1]] + 10
L4[["alpha"]] + 10

# [문제5]
L5 <- list( data1 = LETTERS,
            data2 = read.csv("data/emp.csv")[1:3,],
            data3 = L4
          )
L5
L5$data3$gamma
unL5 <- unlist(L5)
unL5["data3.alpha2"]
str(unL5)
names(unL5) <- NULL

L5[["data1"]][1]
L5$data2[,2]
L5$data3$gamma


# [문제6]
L6 <- list(math=list(95, 90), writing=list(90, 85), reading=list(85, 80))
mean(unlist(L6))
str(unlist(L6))

x <- unlist(L6)
names(x) <- NULL
x


# [문제1]
grade <-sample(1:6,1)
if(grade <= 3){
  cat(grade,"학년은 저학년입니다.","\n")
}else{
  cat(grade,"학년은 고학년입니다.","\n")
}


# [문제2]
choice <- sample(1:5,1)
if (choice == 1){
  result <- 300 + 50
}else if (choice == 2){
  result <- 300 - 50
}else if (choice == 3){
  result <- 300 * 50
}else if (choice == 4){
  result <- 300 / 50
}else { #무조건 5
  result <- 300 %% 50
}
switch(EXPR=choice, 300 + 5, 300 - 50, 300 * 50, 300 / 50, 300 %% 50)
#cat("choice :", choice, "결과값 :", result, "\n")
cat("결과값 :", result, "\n")





# [문제3]
count <- sample(3:10,1)
deco <- sample(1:3,1)
#count;deco
for(cnt in 1:count){
  cat(switch(EXPR = deco,"*","$","#"))
}


# [문제4]
# [문제4]-1안
score <- sample(0:100,1)
grade <- switch(EXPR = ifelse(score >= 90,1,
                              ifelse(score >= 80,2, 
                                     ifelse(score >= 70,3,              
                                            ifelse(score >= 60,4,5))))
                ,"A","B","C","D","F")
cat(score, "점은", grade, "등급입니다.\n")

# [문제4]-2안
score <- sample(0:100,1)

if (score < 10){
  ch_score =paste("00", as.character(score), sep='') 
}else if (score < 100){
  ch_score =paste("0", as.character(score), sep='') 
}else {
  ch_score = as.character(score)
}
hd_ch_score <- substr(ch_score, 1, 2)

grade <- switch(EXPR = hd_ch_score, "10"=,"09"="A","08"="B","07"="C","06"="D", "F")
cat(score, "점은", grade, "등급입니다.\n")

# [문제4]-3안
hd_ch_score <- score %/% 10    #몫으로 처리
grade <- switch(EXPR = hd_ch_score, "10"=,"09"="A","08"="B","07"="C","06"="D", "F")
cat(score, "점은", grade, "등급입니다.\n")

# [문제5]
alpha <- paste(LETTERS, letters, sep=""); alpha

```


