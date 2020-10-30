

# 분석Day13

>  분석Day13 - 단일_다중선형회귀, 다중 공선성 확인

### - 교육내용

# 선형회귀 분석을 이용한 데이터 분석

## 1. 단일 선형 회귀 분석

### 두 변수(종속변수, 독립변수) 사이의 함수적 관계를 기술하는 수학적 방정식을 구하는데 사용

### 식은 독립변수의 값이 주어질 때 종속변수의 값을 추정하거나 예측하는데 사용

### 서로 영향을 주고 받는 상관관계를 갖는 두 변수 사이의 관계를 분석

### 분석을 진행하기 전에 두 변수간의 관계를 대략적으로 살펴보기 위해 산점도를 그리거나 상관계수 등을 채크한다.

### **회귀분석은 서로 영향을 주고받으면서 인과관계를 갖는 독립변수와 종속변수 사이의 관계를 분석는데 사용한다.**

---

### **종속변수 : 다른 변수에 의해 영향을 받는 변수로서 독립변수의 값에 따른 값을 예측하려는 변수**

### **독립변수 : 다른 변수에 영향을 주고 그 변수 값을 예측하려는 변수**

### [단일 선형회귀분석 진행 프로세스]

### <span style="color:red">독립변수와 종속변수 선정</span>  --> <span style="color:green">오차를 최소화 하는 단일 선형회귀모델 결정-<mark>최소자승법</mark></span> --> 

### <span style="color:blue">적합도(검정력) 검증-<mark>결정계수</mark></span>  --> <span style="color:magenta">종속변수의 값 예측</span> 

*결정계수는 0과 1사이 숫자로 1에 가까워야 결정력이 좋음 0.5이상은 되어야 쓸만함*

![edu3](C:/Users/Daniel/Downloads/images/edu3.png)

## 단일 선형회귀분석 예제 1


```python
from sklearn import linear_model
import numpy as np
import pandas as pd
import matplotlib
import matplotlib.pyplot as plt

matplotlib.style.use('ggplot')
```


```python
data = {'x' : [13, 19, 16, 14, 15, 14],
        'y' : [40, 83, 62, 48, 58, 43]}

data = pd.DataFrame(data)
data
```


```python
data.plot(kind="scatter",  # 산점도를 그리시오
          x='x',           # 가로축은 x라고 라벨을 붙임
          y='y',           # 세로축은 y라고 라벨을 붙임
          figsize=(5,5),   # 가로 5인치, 세로 5인치 크기의 박스를 설정
          color="blue")    # 산점도 상의 점 색상을 파랑색으로 지정
```


```python
# linear_model 모듈이 포함하고 있는 Linearregression() 함수를 'linear_regression'이라고 하는 변수에 할당
linear_regression = linear_model.LinearRegression()

# Linearregression()의 fit()이라는 함수를 이용하여 선형회귀 모델 훈련 실행
# 이 때 독립변수는 x, 종속변수는 y
linear_regression.fit(X = pd.DataFrame(data["x"]), y = data["y"])

# 선형 회귀식의 세로축 절편 'linear_regression.intercept_'를 구하여 출력한다.
print('a value = ', linear_regression.intercept_)

# 선형 회귀식의 기울기 'linear_regression.coef_'를 구하여 출력한다.
print('b balue =', linear_regression.coef_)
```


```python
# 위에서 만들어진 선형회귀 모델을 적용하여 선형회귀 값을 구해본다.
# 그 값을 prediction에 할당한다.
prediction = linear_regression.predict(X = pd.DataFrame(data["x"]))

# 실제 y값과 예측한 y값을 비교하여 잔차(residuals)를 구한다.
residuals = data["y"] - prediction
print(residuals)

# 변수의 갯수(6개), 잔차의 평균값, 잔차의 표준편차, 최소값, 25% 값, 50% 값, 75% 값, 최대값을 출력한다.
residuals.describe()
```


```python
# 잔차를 제곱하여 전체를 합침. 결과값을 SSE라는 변수에 할당
SSE = (residuals**2).sum()
print("SSE = ", SSE)

# y값의 표준편차를 제곱한 것을 모두 합침. 그 결과값을 SST라는 변수에 할당
SST = ((data["y"]-data["y"].mean())**2).sum()
print("SST = ", SST)

# 결정계수 R을 구함
R_squared = 1 - (SSE/SST)
print('R_squared = ', R_squared)
```


```python
data.plot(kind="scatter",x="x",y="y",figsize=(5,5),color="red")

# Plot regression line
plt.plot(data["x"],prediction,color="blue")
```


```python
# sklearn.metrics라는 패키지로부터 mean_squared_error 모듈을 불러들임
from sklearn.metrics import mean_squared_error

# 결정계수 R값을 구함
print('score = ', linear_regression.score(X = pd.DataFrame(data["x"]), y = data["y"]))

# 실제값(data[y])과 회귀식 값(prediction)의 차이의 제곱을 구함
print('Mean_Squared_Error = ', mean_squared_error(prediction, data['y']))

# Mean squared error의 제곱근 값을 구함
print('RMSE = ', mean_squared_error(prediction, data['y'])**0.5)
```

## 단일 선형회귀분석 예제 2


```python
from sklearn import datasets
boston_house_prices = datasets.load_boston()
print(boston_house_prices.keys())
print(boston_house_prices.data.shape)
print(boston_house_prices.feature_names)
```


```python
print(boston_house_prices.DESCR)
```


```python
data_frame = pd.DataFrame(boston_house_prices.data)
data_frame.tail()
```


```python
data_frame.columns = boston_house_prices.feature_names
data_frame.tail()
```


```python
data_frame['Price'] = boston_house_prices.target
data_frame.tail()
```


```python
data_frame.plot(kind="scatter", x="RM", y="Price", figsize=(6,6),
                color="blue", xlim = (4,8), ylim = (10,45))
```


```python
linear_regression = linear_model.LinearRegression()
linear_regression.fit(X = pd.DataFrame(data_frame["RM"]), y = data_frame["Price"])
prediction = linear_regression.predict(X = pd.DataFrame(data_frame["RM"]))
print('a value = ', linear_regression.intercept_)
print('b balue =', linear_regression.coef_)
```


```python
residuals = data_frame["Price"] - prediction
residuals.describe()
```


```python
SSE = (residuals**2).sum()
SST = ((data_frame["Price"]-data_frame["Price"].mean())**2).sum()
R_squared = 1 - (SSE/SST)
print('R_squared = ', R_squared)
```


```python
data_frame.plot(kind="scatter",x="RM",y="Price",figsize=(6,6),
                color="blue", xlim = (4,8), ylim = (10,45))

# Plot regression line
plt.plot(data_frame["RM"],prediction,color="red")
# plt.plot(y=data_frame["Price"].mean(), prediction,color="green")
```


```python
print('score = ', linear_regression.score(X = pd.DataFrame(data_frame["RM"]), y = data_frame["Price"]))
print('Mean_Squared_Error = ', mean_squared_error(prediction, data_frame["Price"]))
print('RMSE = ', mean_squared_error(prediction, data_frame["Price"])**0.5)
```

---

## 2. 다중 선형 회귀 분석

### 두 개 이상의 독립변수들과 하나의 종속변수의 관계를 분석하는 방법(단순 회귀를 확장환 것임)

#### 각 독립변수들과 종속변수간에는 선형성이 있어야 한다.

#### 오차항은 각각의 독립변수에 독립적이다라는 가정을 전제로 한다.

#### 오차항의 기댓값은 0이며 일정한 분산을 갖는 정규분포를 이룬다고 가정한다. - 등분산성

#### 각 오차에 대한 상관관계는 없어야 한다. 즉 공분산 값이 0이어야 한다.

#### 각 독립변수들간에는 강한 상관관계가 없어야 한다. --> 다중공선선 문제 발생

#### 다중공선성 문제를 해결하려면 분산팽창계수(VIF(Variance Inflation Factor, 분산팽창요인)를 계산하여 채크한다. 

### [추가]

#### 공선성(collinearity): 하나의 독립변수가 다른 하나의 독립변수로 잘 예측되는 경우, 또는 서로 상관이 높은 경우

#### 다중공선성(multicollinearity): 하나의 독립변수가 다른 여러 개의 독립변수들로 잘 예측되는 경우

#### (다중)공선성이 있으면:

##### 계수 추정이 잘 되지 않거나 불안정해져서 데이터가 약간만 바뀌어도 추정치가 크게 달라질 수 있다.

##### 계수가 통계적으로 유의미하지 않은 것처럼 나올 수 있다.

#### (다중)공선성의 진단

##### 분산팽창계수(VIF, Variance Inflation Factor)를 구하여 판단

##### 엄밀한 기준은 없으나 보통 10보다 크면 다중공선성이 있다고 판단(5를 기준으로 하기도 함)

## 다중 선형회귀분석 예제 1


```python
from sklearn import linear_model
import numpy as np
import pandas as pd
import matplotlib
import matplotlib.pyplot as plt
matplotlib.style.use('ggplot')
```


```python
data = {'x1' : [13, 18, 17, 20, 22, 21],
        'x2' : [9, 7, 17, 11, 8, 10],
        'y' : [20, 22, 30, 27, 35, 32]}
data = pd.DataFrame(data)
X = data[['x1', 'x2']]
y = data['y']
data
```


```python
linear_regression = linear_model.LinearRegression()
linear_regression.fit(X = pd.DataFrame(X), y = y)
prediction = linear_regression.predict(X = pd.DataFrame(X))
print('a value = ', linear_regression.intercept_)
print('b balue = ', linear_regression.coef_)
```


```python
residuals = y-prediction
residuals.describe()
```


```python
SSE = (residuals**2).sum()
SST = ((y-y.mean())**2).sum()
R_squared = 1 - (SSE/SST)
print('R_squared = ', R_squared)
```


```python
from sklearn.metrics import mean_squared_error
print('score = ', linear_regression.score(X = pd.DataFrame(X), y=y))
print('Mean_Squared_Error = ', mean_squared_error(prediction, y))
print('RMSE = ', mean_squared_error(prediction, y)**0.5)
```

## 다중 선형회귀분석 예제 2


```python
from sklearn import datasets
boston_house_prices = datasets.load_boston()
print(boston_house_prices.keys())
print(boston_house_prices.data.shape)
print(boston_house_prices.feature_names)
```


```python
print(boston_house_prices.DESCR)
```


```python
X = pd.DataFrame(boston_house_prices.data)
X.tail()
```


```python
X.columns = boston_house_prices.feature_names
X.tail()
```


```python
X['Price'] = boston_house_prices.target
y = X.pop('Price')
X.tail()
```


```python
linear_regression = linear_model.LinearRegression()
linear_regression.fit(X = pd.DataFrame(X), y = y)
prediction = linear_regression.predict(X = pd.DataFrame(X))
print('a value = ', linear_regression.intercept_)
print('b balue =', linear_regression.coef_)
```


```python
residuals = y-prediction
residuals.describe()
```


```python
SSE = (residuals**2).sum()
SST = ((y-y.mean())**2).sum()
R_squared = 1 - (SSE/SST)
print('R_squared = ', R_squared)
```


```python
print('score = ', linear_regression.score(X = pd.DataFrame(X), y = y))
print('Mean_Squared_Error = ', mean_squared_error(prediction, y))
print('RMSE = ', mean_squared_error(prediction, y)**0.5)
```



# 국내 프로야구 연봉 예측

### 바로가기

- [<Step1. 탐색> 프로야구 연봉 데이터 살펴보기](#<Step1.-탐색>-프로야구-연봉-데이터-살펴보기)
  - [프로야구 연봉 데이터셋의 기본 정보]
  - [회귀 분석에 사용할 피처 살펴보기]
- [<Step2. 예측> : 투수의 연봉 예측하기](#<Step2.-예측>-:-투수의-연봉-예측하기)
  - [피처들의 단위 맞춰주기 : 피처 스케일링]
  - [피처들의 단위 맞춰주기 : one-hot-encoding]
  - [피처들의 상관관계 분석]
  - [회귀 분석 적용하기]
- [<Step3. 평가> : 예측 모델 평가하기](#<Step3.-평가>-:-예측-모델-평가하기)
  - [어떤 피처가 가장 영향력이 강한 피처일까]
  - [예측 모델의 평가]
  - [회귀 분석 예측 성능을 높이기 위한 방법 : 다중 공선성 확인]
  - [믿을만한 피처로 다시 학습하기]
- [<Step4. 시각화> : 분석 결과의 시각화](#<Step4.-시각화>-:-분석-결과의-시각화)
  - [예상 연봉과 실제 연봉 비교]

-----


```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

import warnings
warnings.filterwarnings("ignore")
```

# <Step1. 탐색> 프로야구 연봉 데이터 살펴보기

### [프로야구 연봉 데이터셋의 기본 정보]


```python
# Data Source : http://www.statiz.co.kr/

picher_file_path = 'data/picher_stats_2017.csv'
batter_file_path = 'data/batter_stats_2017.csv'
picher = pd.read_csv(picher_file_path)
batter = pd.read_csv(batter_file_path)
```


```python
picher.columns
```


```python
picher.head()
```


```python
print(picher.shape)
```


```python
import matplotlib as mpl
set(sorted([f.name for f in mpl.font_manager.fontManager.ttflist])) # 현재 OS 내에 설치된 폰트를 확인합니다.
```


```python
from matplotlib import font_manager, rc
font_path = "data/THEdog.ttf"   #폰트파일의 위치
font_name = font_manager.FontProperties(fname=font_path).get_name()
rc('font', family=font_name)
```

###### 예측할 대상인 '연봉'에 대한 정보


```python
picher['연봉(2018)'].describe()
```


```python
picher['연봉(2018)'].hist(bins=100) # 2018년 연봉 분포를 출력합니다.
```


```python
picher.boxplot(column=['연봉(2018)']) # 연봉의 Boxplot을 출력합니다.
```

-----

### [회귀 분석에 사용할 피처 살펴보기]


```python
picher_features_df = picher[['승', '패', '세', '홀드', '블론', '경기', '선발', '이닝', '삼진/9',
       '볼넷/9', '홈런/9', 'BABIP', 'LOB%', 'ERA', 'RA9-WAR', 'FIP', 'kFIP', 'WAR',
       '연봉(2018)', '연봉(2017)']]
```


```python
# 피처 각각에 대한 histogram을 출력합니다.
def plot_hist_each_column(df):
    plt.rcParams['figure.figsize'] = [20, 16]
    fig = plt.figure(1)
    
    # df의 column 갯수 만큼의 subplot을 출력합니다.
    for i in range(len(df.columns)):
        ax = fig.add_subplot(5, 5, i+1)
        plt.hist(df[df.columns[i]], bins=50)
        ax.set_title(df.columns[i])
    plt.show()
```


```python
plot_hist_each_column(picher_features_df)
```

-----

# <Step2. 예측> : 투수의 연봉 예측하기

### [피처들의 단위 맞춰주기 : 피처 스케일링]


```python
# pandas 형태로 정의된 데이터를 출력할 때, scientific-notation이 아닌 float 모양으로 출력되게 해줍니다.
pd.options.mode.chained_assignment = None
```


```python
# 피처 각각에 대한 scaling을 수행하는 함수를 정의합니다.
def standard_scaling(df, scale_columns):
    for col in scale_columns:
        series_mean = df[col].mean()
        series_std = df[col].std()
        df[col] = df[col].apply(lambda x: (x-series_mean)/series_std)
    return df
```


```python
# 피처 각각에 대한 scaling을 수행합니다.
scale_columns = ['승', '패', '세', '홀드', '블론', '경기', '선발', '이닝', '삼진/9',
       '볼넷/9', '홈런/9', 'BABIP', 'LOB%', 'ERA', 'RA9-WAR', 'FIP', 'kFIP', 'WAR', '연봉(2017)']
picher_df = standard_scaling(picher, scale_columns)
```


```python
picher_df = picher_df.rename(columns={'연봉(2018)': 'y'})
picher_df.head(5)
```

-----

### [피처들의 단위 맞춰주기 : one-hot-encoding]


```python
# 팀명 피처를 one-hot encoding으로 변환합니다.
team_encoding = pd.get_dummies(picher_df['팀명'])
picher_df = picher_df.drop('팀명', axis=1)
picher_df = picher_df.join(team_encoding)
```


```python
team_encoding.head(5)
```


```python
picher_df.head()
```

-----

### [회귀 분석 적용하기]

##### 회귀 분석을 위한 학습, 테스트 데이터셋 분리


```python
from sklearn import linear_model
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error
from math import sqrt

# 학습 데이터와 테스트 데이터로 분리합니다.
X = picher_df[picher_df.columns.difference(['선수명', 'y'])]
y = picher_df['y']
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=19)
```

##### 회귀 분석 계수 학습 & 학습된 계수 출력


```python
# 회귀 분석 계수를 학습합니다 (회귀 모델 학습)
lr = linear_model.LinearRegression()
model = lr.fit(X_train, y_train)
```


```python
# 학습된 계수를 출력합니다.
print(lr.coef_)
```


```python
picher_df.columns
```

-----

# <Step3. 평가> : 예측 모델 평가하기

### [어떤 피처가 가장 영향력이 강한 피처일까]


```python
import statsmodels.api as sm

# statsmodel 라이브러리로 회귀 분석을 수행합니다.
X_train = sm.add_constant(X_train)
model = sm.OLS(y_train, X_train).fit()
model.summary()
```


```python
# 한글 출력을 위한 사전 설정 단계입니다.
#mpl.rc('font', family='AppleGothic')
font_path = "data/THEdog.ttf"   #폰트파일의 위치
font_name = font_manager.FontProperties(fname=font_path).get_name()
rc('font', family=font_name)
plt.rcParams['figure.figsize'] = [20, 16]

# 회귀 계수를 리스트로 반환합니다.
coefs = model.params.tolist()
coefs_series = pd.Series(coefs)

# 변수명을 리스트로 반환합니다.
x_labels = model.params.index.tolist()

# 회귀 계수를 출력합니다.
ax = coefs_series.plot(kind='bar')
ax.set_title('feature_coef_graph')
ax.set_xlabel('x_features')
ax.set_ylabel('coef')
ax.set_xticklabels(x_labels)
```

-----

### [예측 모델의 평가]


```python
# 학습 데이터와 테스트 데이터로 분리합니다.
X = picher_df[picher_df.columns.difference(['선수명', 'y'])]
y = picher_df['y']
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=19)
```


```python
# 회귀 분석 모델을 학습합니다.
lr = linear_model.LinearRegression()
model = lr.fit(X_train, y_train)
```

##### R2 score


```python
# 회귀 분석 모델을 평가합니다.
print(model.score(X_train, y_train)) # train R2 score를 출력합니다.
print(model.score(X_test, y_test)) # test R2 score를 출력합니다.
```

##### RMSE score


```python
# 회귀 분석 모델을 평가합니다.
y_predictions = lr.predict(X_train)
print(sqrt(mean_squared_error(y_train, y_predictions))) # train RMSE score를 출력합니다.
y_predictions = lr.predict(X_test)
print(sqrt(mean_squared_error(y_test, y_predictions))) # test RMSE score를 출력합니다.
```

-----

### [피처들의 상관관계 분석]


```python
import seaborn as sns

# 피처간의 상관계수 행렬을 계산합니다.
corr = picher_df[scale_columns].corr(method='pearson')
show_cols = ['win', 'lose', 'save', 'hold', 'blon', 'match', 'start', 
             'inning', 'strike3', 'ball4', 'homerun', 'BABIP', 'LOB', 
             'ERA', 'RA9-WAR', 'FIP', 'kFIP', 'WAR', '2017']

# corr 행렬 히트맵을 시각화합니다.
plt.rc('font', family='NanumGothicOTF')
sns.set(font_scale=1.5)
hm = sns.heatmap(corr.values,
            cbar=True,
            annot=True, 
            square=True,
            fmt='.2f',
            annot_kws={'size': 15},
            yticklabels=show_cols,
            xticklabels=show_cols)

plt.tight_layout()
plt.show()
```

-----

### [회귀분석 예측 성능을 높이기 위한 방법 : 다중공선성 확인]


```python
from statsmodels.stats.outliers_influence import variance_inflation_factor
```


```python
# 피처마다의 VIF 계수를 출력합니다.
vif = pd.DataFrame()
vif["VIF Factor"] = [variance_inflation_factor(X.values, i) for i in range(X.shape[1])]
vif["features"] = X.columns
vif.round(1)
```

-----

### [적절한 피처로 다시 학습하기]


```python
# 피처를 재선정합니다.
X = picher_df[['FIP', 'WAR', '볼넷/9', '삼진/9', '연봉(2017)']]
y = picher_df['y']
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=19)
```


```python
# 모델을 학습합니다.
lr = linear_model.LinearRegression()
model = lr.fit(X_train, y_train)
```


```python
# 결과를 출력합니다.
print(model.score(X_train, y_train)) # train R2 score를 출력합니다.
print(model.score(X_test, y_test)) # test R2 score를 출력합니다.
```


```python
# 회귀 분석 모델을 평가합니다.
y_predictions = lr.predict(X_train)
print(sqrt(mean_squared_error(y_train, y_predictions))) # train RMSE score를 출력합니다.
y_predictions = lr.predict(X_test)
print(sqrt(mean_squared_error(y_test, y_predictions))) # test RMSE score를 출력합니다.
```


```python
# 피처마다의 VIF 계수를 출력합니다.
X = picher_df[['FIP', 'WAR', '볼넷/9', '삼진/9', '연봉(2017)']]
vif = pd.DataFrame()
vif["VIF Factor"] = [variance_inflation_factor(X.values, i) for i in range(X.shape[1])]
vif["features"] = X.columns
vif.round(1)
```

-----

# <Step4. 시각화> : 분석 결과의 시각화

### [예상 연봉과 실제 연봉 비교]


```python
# 2018년 연봉을 예측하여 데이터프레임의 column으로 생성합니다.
X = picher_df[['FIP', 'WAR', '볼넷/9', '삼진/9', '연봉(2017)']]
predict_2018_salary = lr.predict(X)
picher_df['예측연봉(2018)'] = pd.Series(predict_2018_salary)
```


```python
# 원래의 데이터 프레임을 다시 로드합니다.
picher = pd.read_csv(picher_file_path)
picher = picher[['선수명', '연봉(2017)']]

# 원래의 데이터 프레임에 2018년 연봉 정보를 합칩니다.
result_df = picher_df.sort_values(by=['y'], ascending=False)
result_df.drop(['연봉(2017)'], axis=1, inplace=True, errors='ignore')
result_df = result_df.merge(picher, on=['선수명'], how='left')
result_df = result_df[['선수명', 'y', '예측연봉(2018)', '연봉(2017)']]
result_df.columns = ['선수명', '실제연봉(2018)', '예측연봉(2018)', '작년연봉(2017)']

# 재계약하여 연봉이 변화한 선수만을 대상으로 관찰합니다.
result_df = result_df[result_df['작년연봉(2017)'] != result_df['실제연봉(2018)']]
result_df = result_df.reset_index()
result_df = result_df.iloc[:10, :]
result_df.head(10)
```


```python
# 선수별 연봉 정보(작년 연봉, 예측 연봉, 실제 연봉)를 bar 그래프로 출력합니다.
#mpl.rc('font', family='NanumGothicOTF')
font_path = "data/THEdog.ttf"   #폰트파일의 위치
font_name = font_manager.FontProperties(fname=font_path).get_name()
rc('font', family=font_name)
result_df.plot(x='선수명', y=['작년연봉(2017)', '예측연봉(2018)', '실제연봉(2018)'], kind="bar")
```