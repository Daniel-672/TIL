

# Day13

> dplyr 패키지, 결측, 이상치 처리

### - 교육내용

```R
install.packages("dplyr") 
library(dplyr)
install.packages("ggplot2")
str(ggplot2::mpg)
head(ggplot2::mpg)
mpg <- as.data.frame(ggplot2::mpg)
str(mpg)
head(mpg)
exam <- read.csv("data/csv_exam.csv")
str(exam)
dim(exam)
head(exam);tail(exam)
View(exam)

# exam에서 class가 1인 경우만 추출하여 출력
exam %>% filter(class == 1) # [참고] 단축키 [Ctrl+Shit+M]으로 %>% 기호 입력
# 2반인 경우만 추출
exam %>% filter(class == 2)
# 1반이 아닌 경우
exam %>% filter(class != 1)
# 3반이 아닌 경우
exam %>% filter(class != 3)
# 수학 점수가 50점을 초과한 경우
exam %>% filter(math > 50)
# 수학 점수가 50점 미만인 경우
exam %>% filter(math < 50)
# 영어점수가 80점 이상인 경우
exam %>% filter(english >= 80)
# 영어점수가 80점 이하인 경우
exam %>% filter(english <= 80)
# 1반 이면서 수학 점수가 50점 이상인 경우
exam %>% filter(class == 1 & math >= 50)
# 2반 이면서 영어점수가 80점 이상인 경우
exam %>% filter(class == 2 & english >= 80)
# 수학 점수가 90점 이상이거나 영어점수가 90점 이상인 경우
exam %>% filter(math >= 90 | english >= 90)
# 영어점수가 90점 미만이거나 과학점수가 50점 미만인 경우
exam %>% filter(english < 90 | science < 50)
# 목록에 해당되는 행 추출하기
exam %>% filter(class == 1 | class == 3 | class == 5)  # 1, 3, 5 반에 해당되면 추출
# %in% 연산자 이용하기
exam %>% filter(class %in% c(1,3,5))  # 1, 3, 5 반에 해당하면 추출
# 추출한 행으로 데이터 만들기
class1 <- exam %>% filter(class == 1)  # class가 1인 행 추출, class1에 할당
class2 <- exam %>% filter(class == 2)  # class가 2인 행 추출, class2에 할당
mean(class1$math)                      # 1반 수학 점수 평균 구하기
mean(class2$math)                      # 2반 수학 점수 평균 구하기


exam %>% select(math)  # math 추출
exam %>% select(english)  # english 추출
# 여러 변수 추출하기
exam %>% select(class, math, english)  # class, math, english 변수 추출
# 변수 제외하기
exam %>% select(-math)  # math 제외
exam %>% select(-math, -english)  # math, english 제외
# dplyr 함수 조합하기
# class가 1인 행만 추출한 다음 english 추출
exam %>% filter(class == 1) %>% select(english)
# 가독성 있게 줄 바꾸기
exam %>% 
  filter(class == 1) %>%  # class가 1인 행 추출
  select(english)         # english 추출
# 일부만 출력하기
exam %>%
  select(id, math) %>%  # id, math 추출
  head                  # 앞부분 6행까지 추출
# 일부만 출력하기
exam %>%
  select(id, math) %>%  # id, math 추출
  head(10)              # 앞부분 10행까지 추출

data(iris)
iris %>% pull(Species)
iris %>% select(Species)
iris %>% select_if(is.numeric)
iris %>% select(-Sepal.Length, -Petal.Length)

# Select column whose name starts with "Petal"
iris %>% select(starts_with("Petal"))
iris %>% select(starts_with("petal"))
iris %>% select(starts_with("Petal", ignore.case=F))
iris %>% select(starts_with("petal", ignore.case=F))

# Select column whose name ends with "Width"
iris %>% select(ends_with("Width"))

# Select columns whose names contains "etal"
iris %>% select(contains("etal"))

# Select columns whose name maches a regular expression
iris %>% select(matches(".t."))

iris %>% select(one_of("aa", "bb", "Petal.Length", "Petal.Width"))


# 오름차순으로 정렬하기
exam %>% arrange(math)  # math 오름차순 정렬
# 내림차순으로 정렬하기
exam %>% arrange(desc(math))  # math 내림차순 정렬
# 정렬 기준 변수 여러개 지정
exam %>% arrange(desc(class), desc(math))  # class 및 math 오름차순 정렬
exam %>% arrange(desc(math)) %>% head(1)

exam %>%
  mutate(total = math + english + science) %>%  # 총합 변수 추가
  head                                          # 일부 추출
#여러 파생변수 한 번에 추가하기
exam %>%
  mutate(total = math + english + science,          # 총합 변수 추가
         mean = (math + english + science)/3) %>%   # 총평균 변수 추가
  head     
exam %>%
  mutate(total = math + english + science,          # 총합 변수 추가
         mean = total/3) %>%   # 총평균 변수 추가
  head 

# 일부 추출
# mutate()에 ifelse() 적용하기
exam %>%
  mutate(test = ifelse(science >= 60, "pass", "fail")) %>%
  head
#추가한 변수를 dplyr 코드에 바로 활용하기
exam %>%
  mutate(total = math + english + science) %>%  # 총합 변수 추가
  arrange(total) %>%                            # 총합 변수 기준 정렬
  head                                          # 일부 추출

# 전체 요약하기

exam %>% summarise(n = n())
exam %>% tally()

exam %>% summarise(mean_math = mean(math))  # math 평균 산출
mean(exam$math)


str(exam %>% summarise(mean_math = mean(math),
                       mean_english = mean(english),
                       mean_science = mean(science))) # 모든 과목의 평균 산출


# 집단별로 요약하기

exam %>%
  group_by(class) %>% summarise(n = n()) 
exam %>%
  group_by(class) %>% tally()   
exam %>% count(class)         # count() is a short-hand for group_by() + tally()
# add_tally() 와 add_count(..) 도 있음

exam %>%
  group_by(class) %>%                # class별로 분리
  summarise(mean_math = mean(math))  # math 평균 산출

exam %>%
  group_by(class) %>%                   # class별로 분리
  summarise(mean_math = mean(math),     # math 평균
            sum_math = sum(math),       # math 합계
            median_math = median(math), # math 중앙값
            n = n())                    # 학생 수

??mpg
str(mpg)

# 각 집단별로 다시 집단 나누기
mpg %>%
  group_by(manufacturer, drv) %>%      # 회사별, 구방방식별 분리
  summarise(mean_cty = mean(cty)) %>%  # cty 평균 산출
  head(10)                             # 일부 출력

#[ 문제 ] 
#회사별로 "suv" 자동차의 도시 및 고속도로 통합 연비 평균을 구해 내림차순으로 정렬하고, 1~5위까지 출력하기
#절차	기능	dplyr 함수
#1	회사별로 분리	group_by()
#2	suv 추출	filter()
#3	통합 연비 변수 생성	mutate()
#4	통합 연비 평균 산출	summarise()
#5	내림차순 정렬	arrange()
#6	1~5위까지 출력	head()
library(ggplot2)
mpg <- as.data.frame(mpg)
str(mpg)
mpg %>%
  group_by(manufacturer) %>%           # 회사별로 분리
  filter(class == "suv") %>%           # suv 추출
  mutate(tot = (cty+hwy)/2) %>%        # 통합 연비 변수 생성
  summarise(mean_tot = mean(tot)) %>%  # 통합 연비 평균 산출
  arrange(desc(mean_tot)) %>%          # 내림차순 정렬
  head(5)                              # 1~5위까지 출력

mpg %>%
  filter(class == "suv") %>%           
  mutate(tot = (cty+hwy)/2) %>% 
  group_by(manufacturer) %>%           
  summarise(mean_tot = mean(tot)) %>%  
  arrange(desc(mean_tot)) %>%          # 내림차순 정렬
  head(5) 


one <- data.frame(x = c(1:1000000), y = c(1:1000000))
two <- data.frame(x = c(1:1000000), y = c(1:1000000))
                  
system.time(rbind(one, two))
system.time(bind_rows(one, two))

# 가로로 합치기
# 중간고사 데이터 생성
test1 <- data.frame(id = c(1, 2, 3, 4, 5, 6),  
                    midterm = c(60, 80, 70, 90, 85, 100))
# 기말고사 데이터 생성
test2 <- data.frame(id = c(1, 5, 3, 4, 2, 7),  
                    final = c(70, 80, 65, 95, 83, 0))

# id 기준으로 합치기
total <- full_join(test1, test2, by = "id")  # id 기준으로 합쳐 total에 할당
# 다른 데이터 활용해 변수 추가하기
# 반별 담임교사 명단 생성
name <- data.frame(class = c(1, 2, 3, 4, 5), teacher = c("kim", "lee", "park", "choi", "jung"))

# class 기준 합치기
exam_new <- left_join(exam, name, by = "class")

# 세로로 합치기
# 학생 1~5번 시험 데이터 생성
group_a <- data.frame(id = c(1, 2, 3, 4, 5),  test = c(60, 80, 70, 90, 85))
# 학생 6~10번 시험 데이터 생성
group_b <- data.frame(id = c(6, 7, 8, 9, 10),  test = c(70, 83, 65, 95, 80))
#세로로 합치기
group_all <- bind_rows(group_a, group_b)  # 데이터 합쳐서 group_all에 할당


# 데이터 정제 : 결측치(NA)와 이상치 처리

df <- data.frame(sex = c("M", "F", NA, "M", "F"), 
                 score = c(5, 4, 3, 4, NA))

# 결측치 확인하기
is.na(df)         # 결측치 확인
table(is.na(df))  # 결측치 빈도 출력
# 변수별로 결측치 확인하기
table(is.na(df$sex))    # sex 결측치 빈도 출력
table(is.na(df$score))  # score 결측치 빈도 출력
# 결측치 포함된 상태로 분석
mean(df$score)  # 평균 산출
sum(df$score)   # 합계 산출
# 결측치 있는 행 제거하기
library(dplyr) # dplyr 패키지 로드
df %>% filter(is.na(score))   # score가 NA인 데이터만 출력
df %>% filter(!is.na(score))  # score 결측치 제거
# 결측치 제외한 데이터로 분석하기
df_nomiss <- df %>% filter(!is.na(score))  # score 결측치 제거
mean(df_nomiss$score)                      # score 평균 산출
sum(df_nomiss$score)                       # score 합계 산출
# 여러 변수 동시에 결측치 없는 데이터 추출하기
# score, sex 결측치 제외
df_nomiss <- df %>% filter(!is.na(score) & !is.na(sex))
df_nomiss  
# 결측치가 하나라도 있으면 제거하기
df_nomiss2 <- na.omit(df)  # 모든 변수에 결측치 없는 데이터 추출

#분석에 필요한 데이터까지 손실 될 가능성 유의
# 함수의 결측치 제외 기능 이용하기 - na.rm = T
mean(df$score, na.rm = T)  # 결측치 제외하고 평균 산출
sum(df$score, na.rm = T)   # 결측치 제외하고 합계 산출
#summarise()에서 na.rm = T사용하기

# 결측치 생성
exam <- read.csv("data/csv_exam.csv")            # 데이터 불러오기
table(is.na(exam))
exam[c(3, 8, 15), "math"] <- NA             # 3, 8, 15행의 math에 NA 할당
#평균 구하기
exam %>% summarise(mean_math = mean(math))             # 평균 산출
exam %>% summarise(mean_math = mean(math, na.rm = T))  # 결측치 제외하고 평균 산출
# 다른 함수들에 적용
exam %>% summarise(mean_math = mean(math, na.rm = T),      # 평균 산출
                   sum_math = sum(math, na.rm = T),        # 합계 산출
                   median_math = median(math, na.rm = T))  # 중앙값 산출
boxplot(exam$math)
mean(exam$math, na.rm = T)  # 결측치 제외하고 math 평균 산출
# 평균으로 대체하기
exam$math <- ifelse(is.na(exam$math), 55, exam$math)  # math가 NA면 55로 대체
table(is.na(exam$math))                               # 결측치 빈도표 생성
mean(exam$math)  # math 평균 산출

# 이상치 포함된 데이터 생성 - sex 3, score 6
outlier <- data.frame(sex = c(1, 2, 1, 3, 2, 1),  score = c(5, 4, 3, 4, 2, 6)) 
# 이상치 확인하기
table(outlier$sex)

table(outlier$score)

# 결측 처리하기 - sex
# sex가 3이면 NA 할당
outlier$sex <- ifelse(outlier$sex == 3, NA, outlier$sex)

#결측 처리하기 - score
# sex가 1~5 아니면 NA 할당
outlier$score <- ifelse(outlier$score > 5, NA, outlier$score)

# 결측치 제외하고 분석
outlier %>%
  filter(!is.na(sex) & !is.na(score)) %>%
  group_by(sex) %>%
  summarise(mean_score = mean(score))

mpg <- as.data.frame(ggplot2::mpg)
View(mpg)
boxplot(mpg$hwy)
boxplot(mpg$hwy, range=2)
summary(mpg$hwy)
#상자그림 통계치 출력
boxplot(mpg$hwy)$stats  # 상자그림 통계치 출력

# 결측 처리하기
# 12~37 벗어나면 NA 할당
mpg$hwy <- ifelse(mpg$hwy < 12 | mpg$hwy > 37, NA, mpg$hwy)
table(is.na(mpg$hwy))
# 결측치 제외하고 분석하기
mpg %>%
  group_by(drv) %>%
  summarise(mean_hwy = mean(hwy, na.rm = T))
```



### - 실습

```R
# 마리아DB 연결 라이브러리 로드
library(rJava)
library(RJDBC)
library(DBI)

drv <- JDBC(driverClass = "org.mariadb.jdbc.Driver" ,"mariadb-java-client-2.6.2.jar")
conn <- dbConnect(drv, 'jdbc:mariadb://127.0.0.1:3303/work', 'scott', 'tiger')

# emp 적재
emp <- dbReadTable(conn, 'emp ')
str(emp)

# dplyr로드
library(dplyr)


# [문제0] comm 컬럼값이 0 보다 적으면 NA 값으로 변경한다.
emp$comm[which(emp$comm < 0)] <- na
emp$comm


# [문제1] 업무가 MANAGER 인 직원들의 정보를 출력한다.
emp %>% filter(job == 'MANAGER')


# [문제2] emp 에서 사번, 이름, 월급을 출력한다.
emp %>% select(empno, ename, sal)


# [문제3] emp 에서 사번만 빼고 출력한다.
emp %>% select(-empno)


# [문제4] emp 에서 ename 과 sal컬럼만 출력한다.
emp %>% select(ename, sal)


# [문제5] 업무별 직원수를 출력한다.
emp %>% group_by(job) %>% summarise(n = n()) 
emp %>% count(job)

# [문제6] 월급이 1000 이상이고 3000이하인 사원들의 이름, 월급, 부서번호를 출력한다.
emp %>% filter(sal >= 1000 & sal <= 3000) %>% select(ename, sal, deptno)


# [문제7] emp 에서 업무이 ANALYST 가 아닌 사원들의 이름, 직업, 월급을 출력한다.
emp %>% filter(job != 'ANALYST') %>% select(ename, job, sal)


# [문제8] emp 에서 업무가 SALESMAN 이거나 ANALYST 인 사원들의 이름, 직업을 출력한다.
emp %>% filter(job %in% c('SALESMAN' ,'ANALYST')) %>% select(ename, job)


# [문제9] 부서별 직원들 월급의 합을 출력한다.
emp %>% group_by(deptno) %>% summarise(sum_sal = sum(sal)) 


# [문제10] 월급이 적은 순으로 모든 직원 정보를 출력한다.
emp %>% arrange(sal)


# [문제11] 월급이 제일 많은 직원의 정보를 출력한다.
emp %>% arrange(desc(sal)) %>% head(1)


# [문제12]
empnew <- emp %>% mutate(salary = sal, commrate = comm) %>% select(-sal, -comm)
empnew

emp %>% rename(emp, sal = salary)


# [문제13] 가장 많은 인원이 일하고 있는 부서 번호를 출력한다.
emp %>% group_by(deptno) %>% summarise(n = n()) %>% 
        arrange(desc(n)) %>% head(1) %>% select(deptno) 


# [문제14]
emp %>% mutate(enamelength = nchar(ename)) %>% arrange(enamelength) %>% select(ename)


# [문제15] 커미션이 정해진 직원들의 명수를 출력한다.
emp %>% filter(comm != 'NA') %>% tally()   
emp %>% filter(!is.na(comm)) %>% tally()


# install.packages("ggplot2")
str(ggplot2::mpg)


# 1
mpg <- as.data.frame(ggplot2::mpg)

# 1-1
str(mpg)

# 1-2
dim(mpg)

# 1-3
head(mpg, 10)

# 1-4
tail(mpg, 10)

# 1-5
View(mpg)

# 1-6
summary(mpg)

# 1-7
mpg %>% count(manufacturer)

# 1-8
mpg %>% count(manufacturer, model)


# 2
# 2-1
mpgCopy <- rename(mpg, city = cty, highway = hwy)
str(mpgCopy)

# 2-2
head(mpgCopy)


# 3
# 3-1
midwest <- as.data.frame(ggplot2::midwest)
str(midwest); head(midwest); summary(midwest)

# 3-2
midwestCopy <- rename(midwest, total = poptotal, asian = popasian)
str(midwestCopy)

# 3-3
# 지역별 아시아인 평균 추가 : perAsian
midwestCopy <- midwestCopy %>% mutate(perAsian = asian / total * 100)
midwestCopy %>% select(total, asian, perAsian) %>% head

# 3-4
# 전체 아시아인 평균 추가 : TAvgPerAsian
midwestCopy <- midwestCopy %>% mutate(TAvgPerAsian = sum(asian) / sum(total) * 100)
midwestCopy %>% select(total, asian, perAsian, TAvgPerAsian) %>% head
# 판별식 추가
midwestCopy <- midwestCopy %>% mutate(sizeAsian = ifelse(perAsian > TAvgPerAsian, "large", "small"))
midwestCopy %>% 
  filter(sizeAsian == 'large') %>% 
  select(total, asian, perAsian, TAvgPerAsian, sizeAsian) %>% head
midwestCopy %>% 
  filter(sizeAsian == 'small') %>% 
  select(total, asian, perAsian, TAvgPerAsian, sizeAsian) %>% head


# 4
mpg <- as.data.frame(ggplot2::mpg)
# 4-1
mpg %>% mutate(catDispl = ifelse(displ <= 4, "배기량4이하", "배기량5이상")) %>% 
  group_by(catDispl) %>% summarise(mean_hwy = mean(hwy))

# 4-2
mpg %>% filter(manufacturer %in% c('audi', 'toyota')) %>% 
  group_by(manufacturer) %>% summarise(mean_cty = mean(cty))

# 4-3
mpg %>% filter(manufacturer %in% c('chevrolet', 'ford', 'honda')) %>% 
  summarise(mean_hwy_3m = mean(hwy))


#5
mpg <- as.data.frame(ggplot2::mpg)
# 5-1
mpgCopy <- mpg %>% select(class, cty)
sample_n(mpgCopy, 5)

# 5-2
mpgCopy %>% filter(class %in% c('suv', 'compact')) %>%
  group_by(class) %>% summarise(mean_cty_2class = mean(cty))


# 6
# audi 모델 중 hwy연비가 좋은 모델
mpg <- as.data.frame(ggplot2::mpg)
mpg %>% filter(manufacturer == 'audi') %>%
  group_by(model) %>% summarise(mean_hwy_audi = mean(hwy)) %>%
  arrange(desc(mean_hwy_audi))

# audi중 hwy연비가 좋은 자동차의 데이터
mpg %>% filter(manufacturer == 'audi') %>%
  arrange(desc(hwy)) %>% head(5)

library(dplyr)
# install.packages("ggplot2")
str(ggplot2::mpg)

# 7
mpg <- as.data.frame(ggplot2::mpg)
# 7-1
mpgCopy <- mpg %>% mutate(sum_cty_hwy = cty + hwy)
head(mpgCopy)

# 7-2
mpgCopy <- mpgCopy %>% mutate(avg_cty_hwy = sum_cty_hwy /2)
head(mpgCopy)

# 7-3
mpgCopy %>% arrange(desc(avg_cty_hwy)) %>% head(3)

# 7-4
mpg %>% mutate(sum_cty_hwy = cty + hwy, avg_cty_hwy = sum_cty_hwy /2) %>%
  arrange(desc(avg_cty_hwy)) %>% head(3)


# 8
# 8-1
mpgCopy <- mpg %>% group_by(class) %>% summarise(mean_cty_class = mean(cty))
mpgCopy

# 8-2
mpgCopy %>% arrange(desc(mean_cty_class))

# 8-3
mpg %>% group_by(manufacturer) %>% summarise(mean_hwy = mean(hwy)) %>% 
  arrange(desc(mean_hwy)) %>% head(3)

# 8-4
mpg %>% filter(class == 'compact') %>% distinct(manufacturer, model) %>% 
  count(manufacturer)  %>% arrange(desc(n))


# 9
fuel <- data.frame(fl = c('c', 'd', 'e', 'p', 'r'),
                   price_fl = c(2.35, 2.38, 2.11, 2.76, 2.22),
                   stringsAsFactors = F)
# 9-1
mpg_fuel <- left_join(mpg, fuel, by = "fl")
dim(mpg); dim(mpg_fuel); head(mpg_fuel, 4)

# 9-2
mpg_fuel %>%  select(model, fl, price_fl) %>% head(5)


# 10
midwest <- as.data.frame(ggplot2::midwest)
# 10-1
midwestCopy <- midwest %>% 
  mutate(perChild = (poptotal - popadults) / poptotal * 100)

# 10-2
midwestCopy %>% arrange(desc(perChild)) %>% 
  select(county, perChild) %>% head(5)

# 10-3
midwestCopy %>% 
  mutate(levelPerChild = ifelse(perChild >= 40, "large",
                         ifelse(perChild >= 30, "middle", 'small'))) %>%
  count(levelPerChild)

# 10-4
midwest %>% mutate(perAsian = popasian / poptotal * 100) %>%
  arrange(perAsian) %>% head(10) %>% select (state, county, perAsian)
  

# 11
mpg <- as.data.frame(ggplot2::mpg)
mpg[c(65, 124, 131, 153, 212), "hwy"] <- NA
# 11-1
is.na(mpg[c('drv', 'hwy')])
table(is.na(mpg$drv)); table(is.na(mpg$hwy))

# 11-2
mpg %>% filter(!is.na(mpg$hwy)) %>%  
  group_by(drv) %>% summarise(mean_hwy = mean(hwy))

na.omit(mpg) %>%  
  group_by(drv) %>% summarise(mean_hwy = mean(hwy))

mpg %>% group_by(drv) %>% 
  summarise(mean_hwy = mean(hwy, na.rm = T))


# 12
mpg <- as.data.frame(ggplot2::mpg)
mpg[c(10, 14, 58, 93), "drv"] <- 'k'
mpg[c(29, 43, 129, 203), "cty"] <-c(3, 4, 39, 42)

# 12-1
table(mpg$drv)
mpg$drv <- ifelse(mpg$drv %in% ('k'), NA, mpg$drv)
table(mpg$drv)

# 12-2
boxplot(mpg$cty)
boxplot(mpg$cty)$stats
mpg$cty <- ifelse(mpg$cty < 9 | mpg$cty > 26, NA, mpg$cty)
boxplot(mpg$cty)

# 12-3
mpg %>% filter(!is.na(mpg$drv)) %>%
  group_by(drv) %>%
  summarise(mean_cty = mean(cty, na.rm = T))

na.omit(mpg) %>%  
  group_by(drv) %>% summarise(mean_cty = mean(cty))

```


