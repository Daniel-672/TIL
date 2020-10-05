

# Day16

> ggplot2_2

### - 교육내용

```R
library(ggplot2)              

diamonds 
g <- diamonds[order(diamonds$table), ]
head(g)  
tail(g)


gg <- ggplot(diamonds, aes(x=carat, y=price))
gg+geom_point()


gg <- ggplot(diamonds, aes(x=carat, y=price))
gg+geom_point(size=1, shape=2, color="steelblue",stroke=1)


gg <- ggplot(diamonds, aes(x=carat, y=price))
gg+geom_point(aes(size=carat, shape=cut, color=color, stroke=carat))


gg1 <- gg + geom_point(aes(color=color))
gg2 <- gg1 + labs(title="Diamonds", x="Carat Layer", y="Price Layer")



gg1 <- gg +geom_point(aes(color=color))
gg2 <- gg1 + labs(title="Diamonds", x="Carat", y="Price")
gg2 + theme(text=element_text(color="red"))


gg1 <- gg +geom_point(aes(color=color))
gg2 <- gg1 + labs(title="Diamonds", x="Carat", y="Price")
gg3 <- gg2 + theme(plot.title=element_text(size=25), 
                   axis.title.x=element_text(size=20), 
                   axis.title.y=element_text(size=20), 
                   axis.text.x=element_text(size=15), 
                   axis.text.y=element_text(size=15))


gg1 <- gg +geom_point(aes(color=color))
gg2 <- gg1 + labs(title="Diamonds", x="Carat", y="Price")
gg3 <- gg2 + theme(plot.title=element_text(size=25), 
                   axis.title.x=element_text(size=20), 
                   axis.title.y=element_text(size=20), 
                   axis.text.x=element_text(size=15), 
                   axis.text.y=element_text(size=15))


gg3 + labs(title="Plot Title \nSecond Line of Plot Title") + 
  theme(plot.title=element_text(face="bold", color="steelblue", lineheight=1.2))


gg1 <- gg +geom_point(aes(color=color))
gg2 <- gg1 + labs(title="Diamonds", x="Carat", y="Price")
gg3 <- gg2 + theme(plot.title=element_text(size=25), 
                   axis.title.x=element_text(size=20), 
                   axis.title.y=element_text(size=20), 
                   axis.text.x=element_text(size=15), 
                   axis.text.y=element_text(size=15))

gg3+scale_colour_manual(name='칼라',
                        values=c('D'='grey', 'E'='red', 'F'='blue','G'='yellow', 
                                 'H'='black', 'I'='green', 'J'='firebrick'))


gg1 <- gg +geom_point(aes(color=color))
gg2 <- gg1 + labs(title="Diamonds", x="Carat", y="Price")
gg3 <- gg2 + theme(plot.title=element_text(size=25), 
                   axis.title.x=element_text(size=20), axis.title.y=element_text(size=20), 
                   axis.text.x=element_text(size=15), axis.text.y=element_text(size=15))

gg3 + coord_cartesian(xlim=c(0,3), ylim=c(0, 5000)) + geom_smooth()


gg1 <- gg +geom_point(aes(color=color))
gg2 <- gg1 + labs(title="Diamonds", x="Carat", y="Price")
gg3 <- gg2 + theme(plot.title=element_text(size=25), 
                   axis.title.x=element_text(size=20), axis.title.y=element_text(size=20), 
                   axis.text.x=element_text(size=15), axis.text.y=element_text(size=15))

gg3 + coord_flip()


gg1 <- gg +geom_point(aes(color=color))
gg2 <- gg1 + labs(title="Diamonds", x="Carat", y="Price")
gg3 <- gg2 + theme(plot.title=element_text(size=25), 
                   axis.title.x=element_text(size=20), axis.title.y=element_text(size=20), 
                   axis.text.x=element_text(size=15), axis.text.y=element_text(size=15))
#print(gg3)

gg3 + theme(plot.background=element_rect(fill="yellowgreen"),
            plot.margin = unit(c(2, 4, 1, 3), "cm"))


gg1 <- gg +geom_point(aes(color=color))
gg2 <- gg1 + labs(title="Diamonds", x="Carat", y="Price")
gg3 <- gg2 + theme(plot.title=element_text(size=25), 
                   axis.title.x=element_text(size=20), axis.title.y=element_text(size=20), 
                   axis.text.x=element_text(size=15), axis.text.y=element_text(size=15))
#print(gg3)

p1 <- gg3 + geom_hline(yintercept=5000, size=2, linetype="dotted", color="blue")
print(p1)


options(scipen=999)  # turn-off scientific notation like 1e+48
library(ggplot2)
theme_set(theme_bw())  # pre-set the bw theme.
data("midwest", package = "ggplot2")
head(midwest)
# Scatterplot
gg <- ggplot(midwest, aes(x=area, y=poptotal)) + 
  geom_point(aes(col=state, size=popdensity)) + 
  geom_smooth(method="loess", se=F) + 
  xlim(c(0, 0.1)) + 
  ylim(c(0, 500000)) + 
  labs(subtitle="Area Vs Population", 
       y="Population", 
       x="Area", 
       title="Scatterplot", 
       caption = "Source: midwest")

plot(gg)
print(gg)



g <- ggplot(mpg, aes(cty, hwy))
# Scatterplot 그림을 그린다. 아래의 내용은 배치로 만든후에 실행할 것
g + geom_point() + 
  geom_smooth(method="lm", se=F) +
  labs(subtitle="mpg: city vs highway mileage", 
       y="hwy", 
       x="cty", 
       title="Scatterplot with overlapping points", 
       caption="Source: midwest")


g <- ggplot(mpg, aes(cty, hwy))
g + geom_count(col="tomato3", show.legend=F) +
  labs(subtitle="mpg: city vs highway mileage", 
       y="hwy", 
       x="cty", 
       title="Counts Plot")



install.packages("ggExtra")
library(ggExtra) 

mpg_select <- mpg[mpg$hwy >= 35 & mpg$cty > 27, ]
g <- ggplot(mpg, aes(cty, hwy)) +
  geom_count() +
  geom_smooth(method="lm", se=F)

ggMarginal(g, type = "histogram", fill="transparent")
ggMarginal(g, type = "boxplot", fill="transparent")



install.packages("ggcorrplot")
library(ggcorrplot) 
# Correlation matrix
data(mtcars)
corr <- round(cor(mtcars), 1)

# Plot
ggcorrplot(corr, hc.order = TRUE, 
           type = "lower", 
           lab = TRUE, 
           lab_size = 3, 
           method="circle", 
           colors = c("tomato2", "white", "springgreen3"), 
           title="Correlogram of mtcars", 
           ggtheme=theme_bw)



library(ggplot2)

theme_set(theme_bw()) 

data("mtcars") # 데이터를 읽는다.
mtcars$'car name' <- rownames(mtcars) # 차 이름을 위한 칼럼을 만든다.

mtcars$mpg_z <- round((mtcars$mpg - mean(mtcars$mpg))/sd(mtcars$mpg), 2) 

mtcars$mpg_type <- ifelse(mtcars$mpg_z < 0, "below", "above") 
mtcars <- mtcars[order(mtcars$mpg_z), ] # 정렬한다.
mtcars$'car name' <- factor(mtcars$'car name', levels = mtcars$'car name')

ggplot(mtcars, aes(x='car name', y=mpg_z, label=mpg_z)) + 
  geom_bar(stat='identity', aes(fill=mpg_type), width=.5) +
  scale_fill_manual(name="Mileage",
                    labels = c("Above Average", "Below Average"), 
                    values = c("above"="#00ba38", "below"="#f8766d")) + 
  labs(subtitle="Normalised mileage from 'mtcars'", 
       title= "Diverging Bars") + 
  coord_flip()


library(ggplot2)
theme_set(theme_bw())

# plot
g <- ggplot(mpg, aes(class, cty))
g + geom_violin() + 
  labs(title="Violin plot", 
       subtitle="City Mileage vs Class of vehicle",
       caption="Source: mpg",
       x="Class of Vehicle",
       y="City Mileage")


qplot(Sepal.Length, Petal.Length, data=iris)
qplot(Sepal.Length, Petal.Length, data = iris, color = Species, size = Petal.Width)
qplot(Sepal.Length, Petal.Length, data = iris, geom = "line", color = Species)
qplot(age, circumference, data = Orange, geom = "line", colour = Tree, main = "How does orange tree circumference vary with age?")

str(Titanic)
mosaicplot(Titanic, main="Titanic Data, Class,Sex,Age,Survival", col=TRUE)



# EDA 실습
# https://www.kaggle.com/c/titanic/data

train <- read.csv('data/train.csv')
test <- read.csv('data/test.csv')

str(train)
head(train)
tail(train)
dim(train)
View(train)

str(test)
head(test)
tail(test)
dim(test)
View(test)

summary(train)
summary(is.na(train))
summary(train == '')
names(train)

library(ggplot2)



df <- NULL
bar_chart <- function(feature){
  select_v <- c("Survived", feature)
  print(select_v)
  df <<- train[select_v]
  df$Survived <<- ifelse(df$Survived == 1, 'Survived', 'Dead')
  ggplot(df, aes(Survived)) + geom_bar(aes(fill=factor(.data[[feature]])))
}

bar_chart('Sex')

# 성별에 따른 생존 여부
select_v <- c('Survived', 'Sex')
df <- train[select_v]
df$Survived <- ifelse(df$Survived == 1, 'Survived', 'Dead')
ggplot(df, aes(Survived)) + geom_bar(aes(fill=Sex))

mosaicplot(Survived ~ Sex,
           data = df, col = TRUE,
           main = "Survival rate by passengers gender")


# 선실 등급에 따른 생존 여부
select_v <- c('Survived', 'Pclass')
df <- train[select_v]
df$Survived <- ifelse(df$Survived == 1, 'Survived', 'Dead')
ggplot(df, aes(Survived)) + geom_bar(aes(fill=factor(Pclass)))

bar_chart('Pclass')

# 함께 탑승한 형제 또는 배우자 수에 따른 생존 여부
select_v <- c('Survived', 'SibSp')
df <- train[select_v]
df$Survived <- ifelse(df$Survived == 1, 'Survived', 'Dead')
ggplot(df, aes(Survived)) + geom_bar(aes(fill=factor(SibSp)))


# 함께 탑승한 부모 또는 자녀 수에 따른 생존 여부
select_v <- c('Survived', 'Parch')
df <- train[select_v]
df$Survived <- ifelse(df$Survived == 1, 'Survived', 'Dead')
ggplot(df, aes(Survived)) + geom_bar(aes(fill=factor(Parch)))


# 탑승한 항구에 따른 생존 여부
select_v <- c('Survived', 'Embarked')
df <- train[select_v]
df <- df[df$Embarked != '',]
df$Survived <- ifelse(df$Survived == 1, 'Survived', 'Dead')
ggplot(df, aes(Survived)) + geom_bar(aes(fill=Embarked))

library(dplyr)
install.packages("gridExtra")
library(gridExtra)
# 나이에 따른 생존 여부

select_v <- c('Survived', 'Age')
df <- train[select_v]
df$Age <- ifelse(is.na(df$Age), median(df$Age, na.rm=T), df$Age)
#df$Aaeclass <- ifelse(df$Age < 7, '영유아',
#                      ifelse(df$Age < 10, '영유아',)
df$Survived <- ifelse(df$Survived == 1, 'Survived', 'Dead')
ggplot(df, aes(Age, Survived)) + geom_bar()

age.p1 <- df %>% 
  ggplot(aes(Age)) + 
  # 히스토그램 그리기, 설정
  geom_histogram(breaks = seq(0, 80, by = 1), # 간격 설정 
                 col    = "red",              # 막대 경계선 색깔 
                 fill   = "green",            # 막대 내부 색깔 
                 alpha  = .5) +               # 막대 투명도 = 50% 
  # Plot title
  ggtitle("All Titanic passengers age hitogram") +
  theme(plot.title = element_text(face = "bold",    # 글씨체 
                                  hjust = 0.5,      # Horizon(가로비율) = 0.5
                                  size = 15, color = "darkblue"))

age.p2 <- df %>% 
  filter(!is.na(Survived)) %>% 
  ggplot(aes(Age, fill = Survived)) + 
  geom_density(alpha = .5) +
  ggtitle("Titanic passengers age density plot") + 
  theme(plot.title = element_text(face = "bold", hjust = 0.5,
                                  size = 15, color = "darkblue"))

grid.arrange(age.p1, age.p2, nrow = 2)


df <- train %>%
  # 결측치(NA)를 먼저 채우는데 결측치를 제외한 값들의 평균으로 채움.
  mutate(Age = ifelse(is.na(Age), mean(train$Age, na.rm = TRUE), Age),
         # Age 값에 따라 범주형 파생 변수 Age.Group 를 생성
         Age.Group = case_when(Age < 13             ~ "Age.0012",
                               Age >= 13 & Age < 18 ~ "Age.1317",
                               Age >= 18 & Age < 60 ~ "Age.1859",
                               Age >= 60            ~ "Age.60inf"),
         # Chr 속성을 Factor로 변환 
         Age.Group = factor(Age.Group))

df <- df %>% 
  # SibSp, Parch와 1(본인)을 더해서 FamilySize라는 파생변수를 먼저 생성  
  mutate(FamilySize = .$SibSp + .$Parch + 1,
         # FamilySize 의 값에 따라서 범주형 파생 변수 FamilySized 를 생성 
         FamilySized = dplyr::case_when(FamilySize == 1 ~ "Single",
                                        FamilySize >= 2 & FamilySize < 5 ~ "Small",
                                        FamilySize >= 5 ~ "Big"),
         # Chr 속성인 FamilySized를 factor로 변환하고
         # 집단 규모 크기에 따라 levels를 새로 지정
         FamilySized = factor(FamilySized, levels = c("Single", "Small", "Big")))



title <- train$Name


# 정규표현식과 gsub()을 이용해서 성별과 관련성이 높은 이름만 추출해서 title 벡터로 저장 
title <- gsub("^.*, (.*?)\\..*$", "\\1", title)
# .*(.뒤부터 .까지) 와 .*?(처음만나는)는 다름 
df$title <- title
install.packages("descr")
descr::CrossTable(df$title)


# 5개 범주로 단순화 시키는 작업 
df <- df %>%
  # "%in%" 대신 "=="을 사용하게되면 Recyling Rule 때문에 원하는대로 되지 않습니다.
  mutate(title = ifelse(title %in% c("Mlle", "Ms", "Lady", "Dona"), "Miss", title),
         title = ifelse(title == "Mme", "Mrs", title),
         title = ifelse(title %in% c("Capt", "Col", "Major", "Dr", "Rev", "Don",
                                     "Sir", "the Countess", "Jonkheer"), "Officer", title),
         title = factor(title))

# 파생변수 생성 후 각 범주별 빈도수, 비율 확인 
descr::CrossTable(df$title)

head(df)

df <- df %>% 
  select("Pclass", "Sex", "Embarked", "FamilySized",
         "Age.Group", "title", "Survived")

View(df)

```



### - 실습

```R

```


