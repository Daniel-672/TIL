### *판다스데이터프레임에서 독립/반응변수 입력 함수*
### - 원천 데이터 리스트

```python
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn import preprocessing

# 컬럼별 정규화 함수
def normalize(df):
    result = df.copy()
    for feature_name in df.columns:
        max_value = df[feature_name].max()
        min_value = df[feature_name].min()
        result[feature_name] = (df[feature_name] - min_value) / (max_value - min_value)
    return result

# 회귀실행 및 결정계수 저장
def runLinearRegression(vCity, shiftln, groupR, mergedrv, rCorr): 
    result = pd.DataFrame()
    # display(mergedrv)
    for rv in rCorr.index.tolist():

        X=mergedrv[rCorr.columns.tolist()].reset_index().drop('datetime', axis=1)
        y=mergedrv[rv].reset_index().drop('datetime', axis=1)
        # display(X)
        # display(y)
        X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=10) 

        lr = LinearRegression()  
        lr.fit(X_train, y_train)

        r_square = lr.score(X_test, y_test)

        result = result.append({'City' : vCity , 'Response' : rv,'shiftrow' : shiftln ,'grouprow' : groupR , 'R_square' : r_square, \
                                'Xa' : lr.coef_, 'b' : lr.intercept_, 'dvList' : rCorr.columns.tolist()} , ignore_index=True)
        # print(result)
    return result


# 모함수
def runCorrLR(df, cityLst, dependentVslst, responseVsLst, shiftGap, groupGap):
    result = pd.DataFrame()
    # 1. df에서 도시별로 실행
    for vCity in cityLst:
        
        tmpdf = df[df['city'] == vCity]
        # 종속변수 df (표준화실행)
        dvdf = normalize(tmpdf[dependentVslst])
        # 반응변수 df (표준화실행)
        rvdf = normalize(tmpdf[responseVsLst])
        
        # 2. shift실행
        for shiftln in range(0, shiftGap):
            dvdf.sort_index()
            
            # 3. 컬럼별로 shift
            for d in dependentVslst :
                dvdf['sft_' + d]  = dvdf[d].shift(- shiftln)

            dvdf.drop(dependentVslst, axis=1)
            # shift로 생긴 na제거
            dvdf = dvdf.dropna(how='any',axis=0) 
            
            
            # 4. 범위로 group 묶기
            for groupln in range(1, groupGap + 1): 
                groupR = str(groupln) + 'D'
                gdvdf = dvdf[dependentVslst].resample(groupR).mean()   # 네이버는 비율이므로 평균이 맞음
                grvdf = rvdf[responseVsLst].resample(groupR).mean()    # 온도 및 관련 변수는 평균이 맞음


                mergedrv = pd.merge(gdvdf, grvdf, left_index=True, right_index=True, how='left')
                # print(vCity, shiftln, groupR)
                rCorr = mergedrv.corr().loc[responseVsLst][dependentVslst]
                # display(mergedrv.corr().loc[responseVsLst][dependentVslst])
                rResult = runLinearRegression(vCity, shiftln, groupR, mergedrv, rCorr)
                result = result.append(rResult)
                # print(rCorr.index)
        print(vCity)
    return(result)

```

### - 실행 함수


    # testdf = weatherDis[weatherDis['city'].isin(['서울특별시', '강원도'])]
    testdf = weatherShop_allP
    cityLst = ['서울특별시', '강원도']
    # cityLst = [ '서울특별시',  '부산광역시', '대구광역시', '인천광역시', '광주광역시', '대전광역시', '울산광역시', '경기도', \
    #                        '강원도',  '충청북도',  '충청남도',  '전라북도', '전라남도', '경상북도', '경상남도', '제주도', '세종특별자치시']
    # dependentVslst = ['temp_avg', 'amount_of_rain', 'r_humidity', 'daylight_hour', 'wk0', 'wk1']
    dependentVslst = ['temp_avg', 'amount_of_rain', 'wk0', 'wk1']
    responseVsLst = productList
    shiftGapD = 2
    groupGapD = 2
    
    
    # 주말처리 토일월과 그외
    import datetime
    import time
    
    # 0:월 5:토 6:일
    def get_week(dt):
        cat = ''
        if pd.to_datetime(dt).weekday() == 5 : cat = 1
        elif pd.to_datetime(dt).weekday() == 6 : cat = 1
        elif pd.to_datetime(dt).weekday() == 4 : cat = 1
        elif pd.to_datetime(dt).weekday() == 0 : cat = 1        
        else : cat = 0
        return cat
    
    testdf['wk_bin'] = testdf['dt'].apply(lambda x : get_week(x))
    # testdf[['dt','wk_bin']]
    
    dummy_wk_bin = pd.get_dummies(testdf.wk_bin)
    dummy_wk_bin.columns = ['wk'+ str(z) for z in range(0,2)]
    dummy_wk_bin
    testdf = pd.concat([testdf, dummy_wk_bin], axis=1)
    
    
    
    testdf['datetime'] = testdf['dt'].apply(lambda x: pd.to_datetime(str(x), format='%Y-%m-%d'))
    testdf.set_index(testdf['datetime'], inplace=True)
    # testdf = testdf.drop('dt', 'wk_bin', 1)
    saveList = runCorrLR(testdf, cityLst, dependentVslst, responseVsLst, shiftGapD, groupGapD)
    
    saveList.to_csv("./data/naverRsqareList.csv")
    
    # ㅋㅋ 17city * 7shift * 7group * 2447반응 = 2,038,351
    # 3시20분 시작
        
