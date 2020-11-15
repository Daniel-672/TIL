### - 기상청동네예보가져오기
```python
def getweather(address):

    today = datetime.datetime.today().strftime('%Y%m%d')
    tomorrow = (datetime.datetime.today() + datetime.timedelta(days=1)).strftime('%Y%m%d')
    # print(today)
    # print(tomorrow)

    dicloc = {
        'address': ['서울특별시', '부산광역시', '대구광역시', '인천광역시', '광주광역시', '대전광역시', '울산광역시', '세종특별자치시', '경기도', '강원도', '충청북도',
                    '충청남도', '전라북도', '전라남도', '경상북도', '경상남도', '제주도'],
        'x': [60, 98, 89, 55, 58, 67, 102, 66, 60, 73, 69, 68, 63, 51, 89, 91, 52],
        'y': [127, 76, 90, 124, 74, 100, 84, 103, 120, 134, 107, 100, 89, 67, 91, 77, 38]}

    dfloc = pd.DataFrame(dicloc)
    xyloc = dfloc[dfloc['address'].isin([address])]

    # api = 'http://apis.data.go.kr/1360000/VilageFcstInfoService/getUltraSrtFcst?serviceKey=' #초단기예보
    api = 'http://apis.data.go.kr/1360000/VilageFcstInfoService/getVilageFcst?serviceKey='  # 동네예보
    key = '6TuB1szn0aNUEln7nrp6jgTQuv5WvoOgxRfPqdBtNPKTVIwbPV7SGmirrRyUIU95CP8oFZHn2f2Yr3zOWPiSdA%3D%3D'
    numOfRows = '1000'
    pageNo = '1'
    base_date = today
    base_time = '0200'
    # print(xyloc.iloc[0][1])
    # print(xyloc.iloc[0][2])

    nx = xyloc.iloc[0][1].astype('str')
    ny = xyloc.iloc[0][2].astype('str')

    savename = 'tmpweather.xml'

    url = api + key + '&numOfRows=' + \
          numOfRows + '&pageNo=' + pageNo + '&base_date=' + base_date + '&base_time=' + base_time + '&nx=' + nx + '&ny=' + ny

    req.urlretrieve(url, savename)

    xml = open(savename, 'r', encoding='utf-8').read()
    soup = BeautifulSoup(xml, 'xml')

    # print(soup.find_all('item'))

    weatherList = []
    for itemList in soup.find_all('item'):
        baseDate = itemList.find('baseDate').string
        baseTime = itemList.find('baseTime').string
        category = itemList.find('category').string
        fcstDate = itemList.find('fcstDate').string
        fcstTime = itemList.find('fcstTime').string
        fcstValue = itemList.find('fcstValue').string
        nx = itemList.find('nx').string
        ny = itemList.find('ny').string
        weatherList.append([baseDate, baseTime, category, fcstDate, fcstTime, fcstValue, nx, ny])

    df = pd.DataFrame(weatherList,
                      columns=['baseDate', 'baseTime', 'category', 'fcstDate', 'fcstTime', 'fcstValue', 'nx', 'ny'])

    df['ffcstValue'] = df['fcstValue'].astype('float')
    df_twoday = df[df['fcstDate'].isin([today, tomorrow])].groupby(['fcstDate', 'category']).mean(
        'fcstValue').reset_index()
    pv_towday = df_twoday.pivot(index=['fcstDate'], columns='category', values='ffcstValue').reset_index()
    pv_towday['temp_avg'] = pv_towday[['TMN', 'TMX']].mean(axis=1)
    pv_towday[['fcstDate', 'R06', 'REH', 'temp_avg']]

    returndic = {'today_rain': round(pv_towday[pv_towday['fcstDate'] == today].R06.values[0],1),
                 'today_humidity': round(pv_towday[pv_towday['fcstDate'] == today].REH.values[0],1),
                 'today_temp': round(pv_towday[pv_towday['fcstDate'] == today].temp_avg.values[0],1),
                 'today_ws': round(pv_towday[pv_towday['fcstDate'] == today].WSD.values[0],1),
                 'tomday_rain': round(pv_towday[pv_towday['fcstDate'] == tomorrow].R06.values[0],1),
                 'tomday_humidity': round(pv_towday[pv_towday['fcstDate'] == tomorrow].REH.values[0],1),
                 'tomday_temp': round(pv_towday[pv_towday['fcstDate'] == tomorrow].temp_avg.values[0],1),
                 'tomday_ws': round(pv_towday[pv_towday['fcstDate'] == tomorrow].WSD.values[0],1),
                 'address': address
                 }
    return returndic
```

