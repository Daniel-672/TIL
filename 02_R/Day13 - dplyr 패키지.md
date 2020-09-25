

# Day13

> dplyr 패키지

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


```


