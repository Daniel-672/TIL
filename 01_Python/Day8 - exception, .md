

# Day8

> exception,  csv, fileioO

### - 교육내용

```python
str = "89점"
try:
    score = int(str)
    print(score)
except:
    print("예외가 발생했습니다.")
print("작업완료")

while True:
    str = input("점수를 입력하세요 : ")
    try:
        score = int(str)
        print("입력한 점수 :", score)
        break
    except:
        print("점수 형식이 잘못되었습니다.")
    finally:
        print('난 항상 수행하는 코드야')
print("작업완료")

str = "89"
try:
    score = int(str)
    print(score)
    a = str[5]
except ValueError:
    print("점수의 형식이 잘못되었습니다.")
except IndexError:
    print("첨자 범위를 벗어났습니다.")
print("작업완료")

str = "89"
try:
    score = int(str)
    print(score)
    a = str[5]
except ValueError as e:
    print(e)
except IndexError as e:
    print(e)
print("작업완료")

def calcsum(n):
    if (n < 0):
        return -1
    sum = 0
    for i in range(n+1):
        sum = sum + i
    return sum

result = calcsum(10)
if result == -1:
    print("입력값이 잘못되었습니다.")
else:
    print("~10 =", result)

result = calcsum(-5)
if result == -1:
    print("입력값이 잘못되었습니다.")
else:
    print("~10 =", result)
    
dic = { 'boy':'소년', 'school':'학교', 'book':'책' }
try:
    print(dic['girl'])
except:
    print("찾는 단어가 없습니다.")

han = dic.get('girl')
if (han == None):
    print("찾는 단어가 없습니다.")
else:
    print(han)

try:
    print("네트워크 접속")
    a = 2 / 0
    print("네트워크 통신 수행")
finally:
    print("접속 해제")
print("작업 완료")

for i in range(10):
    try:
        print(10 / i)
    except ZeroDivisionError:
        print("Not divided by 0")

print("=" * 20)

for i in range(10):
    try:
        result = 10 / i
    except ZeroDivisionError:
        print("Not divided by 0")
    else:
        print(10 / i)

print("=" * 20)

try:
    for i in range(0, 10):
        result =10 // i
        print(result)
except ZeroDivisionError:
    print("Not divided by 0")
finally:
    print("종료되었다.")
    
line_counter = 0            # 파일의 총 줄 수를 세는 변수
data_header = [ ]           # 데이터의 필드값을 저장하는 리스트
customer_list = [ ]         # customer의 개별 리스트를 저장하는 리스트

with open("customers.csv") as customer_data: # customers.csv 파일을 customer_data 객체에 저장
    while 1:
        data = customer_data.readline()     # customers.csv에 데이터 변수에 한 줄씩 저장
        if not data:break                   # 데이터가 없을 때, 반복문 종료
        if line_counter == 0:               # 첫 번째 데이터는 데이터의 필드
            data_header = data.split(",")   # 데이터의 필드는 data_header 리스트에 저장, 데이터 저장 시 ","로 분리
        else:
            customer_list.append(data.split(",")) # 일반 데이터는 customer_list 객체에 저장, 데이터 저장 시 “,”로 분리
        line_counter +=1

print("Header:", data_header)               # 데이터 필드값 출력
for i in range(0, 10):                      # 데이터 출력(샘플 10개만)
    print("Data",i+1,":",customer_list[i])
print(len(customer_list))                   # 전체 데이터 크기 출력


line_counter = 0
data_header = []
employee = []
customer_USA_only_list = []
customer = None

with open("customers.csv", "r") as customer_data:
    while 1:
        data = customer_data.readline()
        if not data:
            break
        if line_counter == 0:
            data_header = data.split(",")
        else:
            customer = data.split(",")

            if customer[10].upper() == "USA":
                customer_USA_only_list.append(customer)
        line_counter+=1

print("Header:", data_header)
for i in range(0, 10):
    print("Data:",customer_USA_only_list[i])
print(len(customer_USA_only_list))

with open("customers_USA_only.csv","w") as customer_USA_only_csv:
    for customer in customer_USA_only_list:
        customer_USA_only_csv.write(",".join(customer).strip('\n')+"\n")

import csv
line_counter = 0
data_header = [ ]
customer_list = [ ]
rownum = 0
f = open("customers.csv", "r")
csv_data = csv.reader(f,  delimiter=',', quotechar='"' )
print(csv_data)
for row in csv_data:
    if rownum == 0:
        data_header = row
    else :
        customer_list.append(row)
    rownum += 1
print("Header:", data_header)
for i in range(0, 10):
    print("Data",i+1,":",customer_list[i])
print(rownum)


import csv                              # csv 객체 호출

seoung_nam_data = [ ]                   # 기본 변수명 선언
header = [ ]
rownum = 0

with open("korea_floating_population_data.csv", "r", encoding = "cp949") as p_file:
    csv_data = csv.reader(p_file)
    for row in csv_data:
        if rownum == 0:
            header = row
        location = row[7]
        if location.find("성남시")!=-1:
            seoung_nam_data.append(row)
        rownum +=1

with open("seoung_nam_floating_population_data1.csv", "w", encoding="utf8") as s_p_file:
    writer = csv.writer(s_p_file, delimiter=',', quotechar="'")
    writer.writerow(header)
    for row in seoung_nam_data:
        writer.writerow(row)

import csv                              # csv 객체 호출
seoung_nam_data = [ ]                   # 기본 변수명 선언
header = [ ]
rownum = 0

with open("korea_floating_population_data.csv", "r", encoding = "cp949") as p_file: # 불러들일 데이터를 선언함, 한글 처리를 위한 c'p949'
    csv_data = csv.reader(p_file)
    for row in csv_data:
        if rownum == 0:
            header = row
        location = row[7]
        if location.find("성남시")!=-1:
            seoung_nam_data.append(row)
        rownum +=1

with open("newdata.csv", "w", encoding="utf8") as s_p_file:
    writer = csv.writer(s_p_file)
    writer.writerow(header)
    for row in seoung_nam_data:
        writer.writerow(row)

f = open("live.txt", "at", encoding="UTF-8")
print(f, type(f))
f.write("""삶이 그대를 속일지라도
슬퍼하거나 노하지 말라!
우울한 날들을 견디면
믿으라, 기쁨의 날이 오리니\n
""")
f.close()

try:
    f = open("live.txt", "rt", encoding="UTF-8")
    print(f, type(f))
    text = f.read()
    print(text)
except FileNotFoundError:
    print("파일이 없습니다.")
finally:
    f.close()

print("*"*20)
f = None
try:
    f = open("live.txt", "rt", encoding="utf8")
    text = f.read()
    print(text)
except FileNotFoundError:
    print("파일이 없습니다.")
finally:
    if f :
        f.close()
        
        
f = open("live.txt", "rt", encoding="UTF-8")
while True:
    text = f.read(10) # 10문자씩 읽기
    if len(text) == 0: break
    print(text, end = '$')
f.close()

print('-' * 20) #-------------------------
f = open("live.txt", "rt", encoding="UTF-8")
text = ""
line = 1
while True:
    row = f.readline() # 한 행씩 읽기
    if not row: break
    text += str(line) + " : " + row
    line += 1
f.close()
print(text)

print('-' * 20) #-------------------------
f = open("live.txt", "rt", encoding="UTF-8")
rows = f.readlines()  # 모든 행을 읽어서 리스트로 리턴
for row in rows:
    print(row, end = '')
f.close()

print('-' * 20) #-------------------------
f = open("live.txt", "rt", encoding="UTF-8")
for line in f:        # _io.TextIOWrapper 객체도 리터러블함
    print(line, end = '')
f.close()


f = open("live.txt", "rt", encoding="UTF-8", errors='ignore')
print("[seek기능 처리가능]" if f.seekable() else "[seek기능 처리불가]" )
f.seek(12,0)
text = f.read()
f.close()
print(text)

# =============== append  ===============
f = open("live.txt", "at", encoding="UTF-8")
f.write("\n\n[추가]푸쉬킨 형님의 말씀이었습니다.")
f.close()

# =============== withas  ===============
with open("live.txt", "rt", encoding="UTF-8") as f:
   text = f.read()
print(text)


# =============== withas  ===============
with open("live.txt", "rt", encoding="utf8") as f:
   text = f.read()
print(text)

# =============== filecopy  ===============
import shutil

shutil.copy("live.txt", "live2.txt")
print("복사완료!")



# =============== listdir  ===============
import os

files = os.listdir("c:\\Temp")
for f in files:
    print(f)

# =============== listdir2  ===============
import os

def dumpdir(path):
    files = os.listdir(path)
    for f in files:
        fullpath = path + "\\" + f
        if os.path.isdir(fullpath):
            print("[" + fullpath + "]")
            dumpdir(fullpath)
        else:
            print("\t" + fullpath)

dumpdir("c:\\MP3")


import os

path = "c:\\Temp"
files = os.listdir(path)
for f in files:
    if (f.find("-") and f.endswith(".mp3")):
        name = f[0:-4]
        ext = f[-4:]
        part = name.split("-")
        newname = part[1].strip() + "-" + part[0].strip() + ext
        print(newname)
        os.rename(path + "\\" + f, path + "\\" + newname)

```



### - 실습

```python
# fileio

import os
import calendar
import datetime

weekday = ['월', '화', '수', '목', '금', '토', '일']
writeTxt = ''
fd = None

# 오늘의 정보
current_date = datetime.datetime.now()
writeTxt = '오늘은 ' + str(current_date.isoformat()[0:4]) + '년 ' + str(current_date.isoformat()[5:7]) + '월 ' + str(
    current_date.isoformat()[8:10]) + '일입니다.' + '\n'
writeTxt += '오늘은 ' + weekday[current_date.weekday()] + "요일입니다." + '\n'

# 내 정보
myNickName = '곰'
myBDate = calendar.weekday(1974, 2, 26)
writeTxt += myNickName + '은 ' + weekday[myBDate] + '요일에 태어났습니다.' + '\n'

# 파일처리
try:
    if not os.path.isdir("c:/iotest"):
        os.mkdir("c:/iotest")
    fd = open("c:/iotest/today.txt", "wt", encoding="UTF-8")
    fd.write(writeTxt)

except:
    print("파일생성 또는 입력 에러")

else:
    print("저장이 완료되었습니다.")

finally:
    if fd:
        fd.close()


import datetime

fdr = None
fdw = None

# 파일명 만들기
now = datetime.datetime.now()
# writeFileName = 'sample_' + now.isoformat()[0:10] + '.txt'

writeFileName = 'sample_' + now.isoformat()[0:10].replace('-', '_') + '.txt'

writeFileName = 'sample_' + str(now.isoformat()[0:4]) + '_' + str(now.isoformat()[5:7]) + '_' + str(
    now.isoformat()[8:10]) + '.txt'



# 민영소스
# writeFileName2 = 'sample_'+str(now.year)+'_'+str(f'{now.month:>02d}')+'_'+str(f'{now.day:02d}')
# print(writeFileName2)

try:
    # 파일 처리
    fdr = open("../sample.txt", "rt", encoding="UTF-8")
    fdw = open(writeFileName, "at", encoding="UTF-8")

    # for line in fdr:
    #     fdw.write(line)
    # fdw.write('\n\n')

    fdw.write(fdr.read())
    fdw.write('\n\n')

except FileNotFoundError as e:
    print(e)

else:
    print("저장이 완료되었습니다.")

finally:
    if fdr:
        fdr.close()

    if fdw:
        fdw.close()


fdr = None

try:
    # fdr = open("../yesterday.txt", "rt", encoding="UTF-8")

    # for line in fdr:
    #     ydayCount += line.lower().count('yesterday')

    # ydayCount = fdr.read().lower().count('yesterday')


    with open("../yesterday.txt", "rt", encoding="UTF-8") as fdr:
       ydayCount = fdr.read().lower().count('yesterday')

except FileNotFoundError:
    print("파일을 읽을 수 없어요.")

else:
    print("Number of a Word \'Yesterday\'", ydayCount)

finally:
    if fdr:
        fdr.close()
    print("수행완료!!")
    
    
    
import calendar

while True:
    str_year = input('년도를 입력하세요 : ')
    str_month = input('월 입력하세요 : ')

    try:
        int_year = int(str_year)
        int_month = int(str_month)
        print(calendar.month(int_year, int_month))
        break

    except ValueError:
        print("년,월 형식이 잘못되었습니다.")
```

