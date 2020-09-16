

# Day7

> collection, string copy, execption, first class object, lamda func, modules

### - 교육내용

```python
score = [ 88, 95, 70, 100, 99 ]
for no, s in enumerate(score, 1):
    print(str(no) + "번 학생의 성적 :", s)

names = "둘리,고길동,희동이,마이콜,또치,도우너"
namelist = names.split(",")
print(namelist)
namelist.sort()
for num, name in enumerate(namelist) :
    print(f"이름순으로 {name}는 {num+1}번입니다.")
for data in enumerate(namelist) :
    print(f"enumerate를 적용한 결과 : {data}")
for num, name in enumerate(namelist, 100) :
    print(f"이름순으로 {name}는 {num}번입니다.")

yoil = ["월", "화", "수", "목","금", "토", "일"]
food = ["갈비탕", "순대국", "칼국수", "삼겹살"]
menu = zip(yoil, food)
print(menu, type(menu))
for y, f in menu:
    print("%s요일 메뉴 : %s" % (y, f))

print("*"*20)
menu = zip(yoil, food)
d2 = dict(menu)
for y, f in d2.items():
    print("%s요일 메뉴 : %s" % (y, f))
print(d2)

print("*"*20)

zip1 = zip([1, 2, 3], [4, 5, 6])
zip2 = zip([1, 2, 3], [4, 5, 6], [7, 8, 9])
zip3 = zip("abc", "def")

print(list(zip1))
print(list(zip2))
print(list(zip3))
print("이거는 왜 비어있을까?")
print(dict(zip1))
print(dict(zip2))
print(dict(zip3))

# =============== filter  ===============
def flunk(s):
    return s < 60

score = [ 45, 89, 72, 53, 94 ]
for s in filter(flunk, score):
    print(s)

# =============== map  ===============
def half(s):
    return s / 2

score = [ 45, 89, 72, 53, 94 ]
for s in map(half, score):
    print(s, end = ', ')
print(' ')
# =============== map2  ===============
def total(s, b):
    return s + b

score = [ 45, 89, 72, 53, 94 ]
bonus = [ 2, 3, 0, 0, 5 ]
for s in map(total, score, bonus):
    print(s, end=", ")


alist = list(range(1,11))
print(alist)
a,b,c = alist[0:3]
print(f"a={a}, b={b},c={c}")
#a,b,c = alist
a,*b,c = alist
print(f"a={a}, b={b},c={c}")

print("-*"*20)
numList = [0, 1, 2]
engList = ['zero', 'one', 'two']
espList = ['cero', 'uno', 'dos']
print(list(zip(numList, engList, espList)))
for num, eng, esp in zip(numList, engList, espList):
    print(f'{num} is {eng} in English and {esp} in Spanish.')

print(dict(list(zip(numList, zip(engList, espList)))))
lanDict = dict(list(zip(numList, zip(engList, espList))))
print(lanDict)
for num, info in lanDict.items():
    print(f'{num} is {info[0]} in English and {info[1]} in Spanish.')



print("-*"*20)
upperCase = ['A', 'B', 'C', 'D', 'E', 'F']
lowerCase = ['a', 'b', 'c', 'd', 'e', 'f']
enuList = enumerate(zip(upperCase, lowerCase), 1)
print(dict(enuList))
print(dict(enuList))
for i, (upper, lower) in enumerate(zip(upperCase, lowerCase), 1):
    print(f'{i}: {upper} and {lower}.')


# copy string
# =============== varcopy  ===============
a = 3
b = a
print("a = %d, b = %d" % (a, b))
print(id(a), id(b))
a = 5
print("a = %d, b = %d" % (a, b))
print(id(a), id(b))
# =============== listcopy  ===============
list1 = [ 1, 2, 3 ]
list2 = list1

list2[1] = 100
print(list1)
print(list2)
print(id(list1),id(list2))
# =============== listcopy2  ===============
list1 = [ 1, 2, 3 ]
list2 = list1.copy()

list2[1] = 100
print(list1)
print(list2)

# =============== deepcopy  ===============
list0 = [ 'a', 'b' ]
list1 = [ list0, 1, 2 ]
list2 = list1.copy()

list2[0][1] = 'c'
print(list1)
print(list2)

# =============== deepcopy2  ===============
import copy

list0 = [ "a", "b" ]
list1 = [ list0, 1, 2 ]
list2 = copy.deepcopy(list1)

list2[0][1] = "c"
print(list1)
print(list2)

# =============== is  ===============
list1 = [ 1, 2, 3 ]
list2 = list1
list3 = list1.copy()

print("1 == 2" , list1 is list2)
print("1 == 3" , list1 is list3)
print("2 == 3" , list2 is list3)

# =============== varis  ===============
a = 1
b = a
print("a =", a, " b =", b, ":", a is b)
print("a =", id(a), " b =", id(b), ":", a is b)

b = 2
print("a =", a, " b =", b, ":", a is b)
print("a =", id(a), " b =", id(b), ":", a is b)


# exception
str = "89점"
score = int(str)
print(score)
print("작업완료")

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

str = "89점"
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
        raise ValueError
    sum = 0
    for i in range(n+1):
        sum = sum + i
    return sum

try:
    print("~10 =", calcsum(10))
    print("~-5 =", calcsum(-5))
except ValueError:
    print("입력값이 잘못되었습니다.")
    
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

score = 28
assert score <= 100, "점수는 100 이하여야 합니다"
print(score)

def func1(n) :
    return n * 2

def func2() :
    print("func2 호출 - hello")

print(type(func1))
print(type(func2))
print('------')
print(func2())
print('------')
v = func2
print(v)
v()

def say1() :
    print("안녕?")

def say2() :
    print("Hello?")

print("=" * 20)
import types
def callback(fn) :
    if type(fn) == types.FunctionType :
        fn()
    else :
        print("아규먼트로 함수를 주세요")

callback(say1)
callback(say2)
callback(2)

def fct_fac(n) :
    def exp(x) :
        return x**n
    return exp

rtnf1 = fct_fac(2)
rtnf2 = fct_fac(3)

print(type(rtnf1))
print(type(rtnf2))

print(rtnf1(4))
print(rtnf2(4))


score = [ 45, 89, 72, 53, 94 ]
for s in filter(lambda x:x < 60, score):
    print(s)

score = [ 45, 89, 72, 53, 94 ]
for s in map(lambda x:x / 2, score):
    print(s, end=", ")

print(map(lambda x:x / 2, score))


print(score)

func1 = lambda n1, n2 : n1 + n2

print(func1(10, 20))
result = func1(100, 200)
print(result)

func2 = lambda s: len(s)
print(func2('simpe'))

func3 = lambda : print("no argument, no return")
print(func3())

func4 = lambda p1, p2, p3 : print(p1, p2, p3)
func4(10, 20, 30)

func5 = lambda *p : print(sum(p))
func5(1,2,3,4,5)
func5(11,22)


def calc():
    num  = 100
    return lambda : num + 1    # 람다 표현식을 반환

c1 = calc()
print(c1(), c1(), c1())


def calc():
    a = 3
    b = 5
    return lambda x: a * x + b    # 람다 표현식을 반환

c2 = calc()
print(c2(1), c2(2), c2(3), c2(4), c2(5))


def calc():
    a = 3
    b = 5
    def expr(x) :
        return a * x + b

    return expr

c3 = calc()
print(c3(100), c3(200), c3(300), c3(400), c3(500))

#string module
# =============== import  ===============
import math

print(math.sqrt(2))

# =============== fromimport  ===============
from math import sqrt

print(sqrt(2))

# =============== importas  ===============
import math as m

print(m.sqrt(2))

# =============== fromas  ===============
from math import sqrt as sq

print(sq(2))

# =============== sin  ===============
import math

print(math.sin(math.radians(45)))
print(math.sqrt(2))
print(math.factorial(5))

# =============== statistics  ===============
import statistics

score = [30, 40, 60, 70, 80, 90]
print(statistics.mean(score))
print(statistics.harmonic_mean(score))
print(statistics.median(score))
print(statistics.median_low(score))
print(statistics.median_high(score))

# =============== time  ===============
import time

print(time.time())

# =============== ctime  ===============
import time

t = time.time()
print(time.ctime(t))

# =============== structtime  ===============
import time

t = time.time()
print(time.localtime(t))

# =============== localtime  ===============
import time

now = time.localtime()
print("%d년 %d월 %d일" % (now.tm_year, now.tm_mon, now.tm_mday))
print("%d:%d:%d" % (now.tm_hour, now.tm_min, now.tm_sec))

# =============== datetime  ===============
import datetime

now = datetime.datetime.now()
print("%d년 %d월 %d일" % (now.year, now.month, now.day))
print("%d:%d:%d" % (now.hour, now.minute, now.second))


# =============== ellapse  ===============
import time

start = time.time()
for a in range(1000):
    print(a)
end = time.time()
print(end - start)

# =============== sleep  ===============
import time

print("안녕하세요.")
time.sleep(1)
print("밤에 성시경이 두 명 있으면 뭘까요?")
time.sleep(5)
print("야간투시경입니다.")

# =============== sleep2  ===============
import time

for dan in range(2, 10):
    print(dan, "단")
    for hang in range(2, 10):
        print(dan, "*", hang, "=", dan*hang)
        time.sleep(0.2)
    print()
    time.sleep(1)

# =============== calendar  ===============
import calendar

print(calendar.calendar(2018))
print(calendar.month(2019, 1))
#calendar.prcal(2018)
#calendar.prmonth(2019, 1)

# =============== weekday  ===============
import calendar

yoil = ['월', '화', '수', '목', '금', '토', '일']
day = calendar.weekday(2020,8,15)
print("광복절은", yoil[day] + "요일이다." )

# =============== random  ===============
import random

for i in range(5):
    print(random.random())

# =============== randint  ===============
import random

for i in range(5):
    print(random.randint(1,10))

# =============== uniform  ===============
import random

for i in range(5):
    print(random.uniform(1,100))

# =============== choice  ===============
import random

food = ["짜장면", "짬뽕", "탕수육", "군만두"]
print(random.choice(food))

# =============== shuffle  ===============
import random

food = ["짜장면", "짬뽕", "탕수육", "군만두"]
print(food)
random.shuffle(food)
print(food)

# =============== sample  ===============
import random

food = ["짜장면", "짬뽕", "탕수육", "군만두"]
print(random.sample(food, 2))

# =============== lotto  ===============
import random

nums = random.sample(range(1, 46), 6)
nums.sort()
print(nums)

# =============== mathquiz  ===============
import random

a = random.randint(1, 9)
b = random.randint(1, 9)
question = "%d + %d = ? " % (a, b)
c = int(input(question))

if c == a + b:
    print("정답입니다.")
else:
    print("틀렸습니다.")

# =============== mathquiz2  ===============
import random

correct = 0
while True:
    a = random.randint(1, 9)
    b = random.randint(1, 9)
    question = "%d + %d = ?(끝낼 때는 0) " % (a, b)
    c = int(input(question))

    if c == 0:
        break
    elif c == a + b:
        print("정답입니다.")
        correct = correct + 1
    else:
        print("틀렸습니다.")

print("%d 개 맞췄습니다." % correct)

# =============== mathquiz3  ===============
import random

correct = 0
while True:
    a = random.randint(10, 99)
    b = random.randint(10, 99)
    op = random.randint(1, 3)

    if op == 1:
        ans = a + b
        mark = "+"
    elif op == 2:
        if (a < b):
            a, b = b, a
        ans = a - b
        mark = "-"
    else:
        ans = a * b
        mark = "*"

    question = "%d %s %d = ?(끝낼 때는 0) " % (a, mark, b)
    c = int(input(question))

    if c == 0:
        break
    elif c == ans:
        print("정답입니다.")
        correct = correct + 1
    else:
        print("틀렸습니다.")

print("%d 개 맞췄습니다." % correct)

# =============== randnum  ===============
import random

secret = random.randint(1,100)
while True:
    num = int(input("숫자를 입력하세요(끝낼 때 0) : "))
    if num == 0:
        break
    if num == secret:
        print("맞췄습니다")
        break
    elif num > secret:
        print("입력한 숫자보다 더 작습니다.")
    else:
        print("입력한 숫자보다 더 큽니다")

# =============== randnum2  ===============
import random

secret = random.randint(1,100)
count = 0
while True:
    num = int(input("숫자를 입력하세요(끝낼 때 0) : "))
    if num == 0:
        break
    count += 1
    if num == secret:
        print("%d번만에 맞췄습니다" % count)
        break
    elif num > secret:
        print("입력한 숫자보다 더 작습니다.")
    else:
        print("입력한 숫자보다 더 큽니다")
# =============== sys  ===============
import sys

print("버전 :", sys.version)
print("플랫폼 :", sys.platform)
if (sys.platform == "win32"):
    print(sys.getwindowsversion())
print("바이트 순서 :", sys.byteorder)
print("모듈 경로 :", sys.path)
sys.exit(0)

# =============== sysarg  ===============
import sys

print(sys.argv)

# =============== argcal  ===============
import calendar
import time
import sys

if (len(sys.argv) == 1):
    t = time.time()
    tm = time.localtime(t)
    calendar.prmonth(tm.tm_year, tm.tm_mon)
elif (len(sys.argv) == 2):
    print(calendar.calendar(int(sys.argv[1])))
elif (len(sys.argv) == 3):
    calendar.prmonth(int(sys.argv[1]), int(sys.argv[2]))
else:
    print("인수는 2개 이하여야 합니다.")
    
# =============== datecalc  ===============
import sys
import time

if (len(sys.argv) != 2):
    print("시작 날짜를 yyyymmdd로 입력하십시오.")
    sys.exit(0)

birth = sys.argv[1]
if (len(birth) != 8 or birth.isnumeric() == False):
    print("날짜 형식이 잘못되었습니다.")
    sys.exit(0)

tm = (int(birth[:4]), int(birth[4:6]), int(birth[6:8]), 0, 0, 0, 0, 0, 0)
ellapse = int((time.time() - time.mktime(tm)) / (24 * 60 * 60))
print(ellapse, "일")

# =============== ellapsedate2  ===============
import sys
import time

year = int(input("태어난 년도를 입력하세요(4자리) : "))
month = int(input("태어난 월을 입력하세요 : "))
day = int(input("태어난 일을 입력하세요 : "))

tm = (year, month, day, 0, 0, 0, 0, 0, 0)
ellapse = int((time.time() - time.mktime(tm)) / (24 * 60 * 60))
print(ellapse, "일")

import os
if not os.path.isdir("c:/Temp/log"):
    os.mkdir("c:/Temp/log")
    print("c:/Temp/log 폴더 생성")
else :
    print("c:/Temp/log 폴더는 이미 존재!!")



```



### - 실습

```python
def myemail_info(email):
    if '@' not in email:
        return None
    spEmail = email.split('@')

    return tuple(spEmail)



print(myemail_info('kim672772@hotmail.com'))
print(myemail_info('kim@naver.com'))
print(myemail_info('667722@gmail.com'))

s1 = "pythonjavascript"
print(len(s1))

s2 = "010-7777-9999"
print(s2.replace('-', ''))

s3 = "PYTHON"
print(s3[::-1])

s4 = "Python"
print(s4.lower())

s5 = "https://www.python.org/"
print(s5.replace('https://', '').replace('/', ''))

s6 = '891022-2473837'
print('남자' if s6[7] in '1,3' else '여자')

s7 = '100'
s7_1 = int(s7)
print(f'정수형은 {s7_1:d} 이고 실수형은 {s7_1:.2f}')

s8 = ' The Zen of Python'
nCount = s8.count('n')
print(f'n의 개수는 {nCount:d}개')

nPosition = s8.find('Z') + 1
print(f'n의 위치는 {nPosition:d}')

s8List = s8.upper().strip().split(' ')
print(s8List)

listv3 = [ 'p', 'y', 't', 'h', 'o', 'n' ]

#v1, v2, v3, v4, v5, v6 = listv3

v1, v2, v3, *v4 = listv3

# for seq in range(1, 7):
#     eval('print(v' + str(seq) + ')')

print(*listv3)

print(listv3)

print(v1)
print(v2)
print(v3)
print(v4)


def createList(*inData, type=1):
    if len(inData) == 0:
        tempData = [e for e in range(1,31)]
    else:
        tempData = list(inData)


    if type == 1:
        outData = tempData
    elif type == 2:
        outData = [e for e in tempData if not e % 2]
    elif type == 3:
        outData = [e for e in tempData if e % 2]
    elif type == 4:
        outData = [e for e in tempData if e > 10]
    else:
        outData = "에러!"

    return outData



print(createList(1,2,3,4,10,11,type=1))
print(createList())
print(createList(1,2,3,4,10,11,type=2))
print(createList(1,2,3,4,10,11,type=3))
print(createList(1,2,3,4,10,11,type=4))
#문자처리필요
print(createList('A','B','C',type=1))

def mydict(**kwargs):

    return {'my_' + key: value for key, value in kwargs.items()}



print(mydict())
print(mydict(A=1, B=2, C=3))
argTest = {'A': '1', 'B': '2'}
print(mydict(**argTest))

print(mydict(**argTest).keys())

listv1 = ["A", "b", "c", "D", "e", "F", "G", "h"]
#listv2 = [elem for elem in listv1 if 79 <= ord(elem) <=122 ]
listv2 = [elem for elem in listv1 if elem.islower() ]
print(listv2)

import random

scoreList = [random.randint(1, 100) for seq in range(10)]

print(scoreList)

scoreDic = {seq: 'pass' if score >= 60 else 'nopass' for seq, score in enumerate(scoreList, 1)}
scoreDic_1 = {seq: 'pass' if score >= 60 else 'nopass' for seq, score in enumerate(scoreList, 1) if score >= 50}

print(scoreDic)

scoreDic2 = {seq+1: 'pass' if scoreList[seq] >= 60 else 'nopass' for seq in range(10)}
scoreDic2_1 = {seq+1: 'pass' if scoreList[seq] >= 60 else 'nopass' for seq in range(10) if scoreList[seq] >= 50}

print(scoreDic2)

print(scoreDic_1)
print(scoreDic2_1)


import random

scoreList =[]

for cnt in range(10):
    scoreList.append(random.randint(1, 100))

scoreDic = {seq : 'pass' if score >= 60 else 'nopass' for seq, score in enumerate(scoreList, 1)}


print(scoreDic)


```

