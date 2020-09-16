

# Day6

> comprehension, string, keywordargument, format

### - 교육내용

```python
students = dict(둘리=90, 또치=85, 도우너=95, 희동이=75, 마이콜=80)

print(students)

pass_students = { k : v for k, v in students.items()}
print(pass_students)

pass_students = { k : v for k, v in students.items() if v > 80}
print(pass_students)

pass_students = { k : v for k, v in students.items() if len(k) > 2}
print(pass_students)

pass_students = { k : v for k, v in students.items() if len(k) > 2 and v > 80}
print(pass_students)

swap_students = { v : k for k, v in students.items() }
print(swap_students)


score_tuples = [('math', 90), ('history', 80), ('english', 95), ('computer engineering', 100), ('science', 60)]
score_dict = dict(score_tuples)
print(score_dict)

score_dict = {t[0]: t[1] for t in score_tuples}
print(score_dict)

score_dict = {k : v for k, v in score_tuples}
print(score_dict)

score_dict = {k : v for k, v in score_tuples if len(k) > 5}
print(score_dict)

score_dict = {k : v for k, v in score_tuples if v >= 90}
print(score_dict)

score_dict = {k : v + 1 for k, v in score_tuples if v < 70}
print(score_dict)

oddeven= { d : '홀수'   if d % 2  else  '짝수' for d in range(1, 16)  }
print(oddeven)

scores = {'길동': 90, '순희': 60, '영희': 80, '철수': 50}
grades = { name: 'PASS' if value > 70 else 'No-PASS' for name, value in scores.items()}
print(grades)

test = dict(a=2, b=3)

#list comprehension
numlist1 = []
numlist1.append(1)
numlist1.append(2)
numlist1.append(3)
numlist1.append(4)
numlist1.append(5)
print("list1 = {}".format(numlist1))

numlist2 = []
for n in range(1,6) :
    numlist2.append(n)
print("list2 = {}".format(numlist2))

numlist3 =list(range(1,6))
print("list3 = {}".format(numlist3))

numlist4 = [ num for num in range(1, 6) ]
print("list4 = {}".format(numlist4))

#print(range(1,6))

oldlist = [17,2,14,6,10,19,16,12,5]
newlist1 = [ oldlist ]
print(newlist1)

newlist11 = list( oldlist )
print(newlist11)

newlist2 = list( [1,2,3,4,5,6,7,8] )
print(newlist2)

newlist3 = list( (1,2,3,4,5,6,7,8) )
print(newlist3)

newlist4 = list( {1, 2,3,4,5,6,7,8} )
print(newlist4)

newlist5 = list( "ABC")
print(newlist5)

newlist6 = [ x for x in range(10) ]
print(newlist6)

newlist7 = [ x for x in oldlist if x % 2 ]
print(newlist7)

newlist8 = [x for x in oldlist if x > 10]
print(newlist8)

newlist9 = [ x*10 for x in oldlist if x < 10 ]
print(newlist9)

flowernames = ['rose', 'sunflower', 'tulip', 'magnolia', 'goldenbell', 'lily']
newlist10 = [i for i in flowernames if len(i) == 4]
print(newlist10)

r1 = ["Black", "White"]
r2 = ["Red", "Blue", "Green"]
r3 = []
for t in r1 :
    for p in r2 :
        r3.append(t+p)
print(r3)

r3 = [ t + p for t in r1 for p in r2 ]
print(r3)

gugulist1 = [ dan * num for dan in range(1, 10) for num in range(1, 10)]
print(gugulist1)

gugulist2 = [ dan * num for dan in range(1, 10) for num in range(1, 10) if dan * num < 30]
print(gugulist2)

#a = [ dan num dan * num for dan in range(1, 10) for num in range(1, 10)]
#print(a)


list1 = [ chr(d)  for d in range(ord('A'), ord('Z')+1) ]
print(list1)

list2 = [ d  for d in range(1, 16) ]
print(list2)

list3 = [ d  for d in range(1, 16) if not d % 2 ]
print(list3)

list4 = [ d  for d in range(1, 16) if not d % 3 ]
print(list4)

list5 = [ d   if d % 2  else  '짝수' for d in range(1, 16)  ]
print(list5)

list6 = [ '홀수'   if d % 2  else  '짝수' for d in range(1, 16)  ]
print(list6)

list7 = [ 'pass_'+str(d)   if d % 2  else   'fail_'+str(d) for d in range(1, 16) if not d % 3 ]
print(list7)

a = {i for i in range(1, 101) if i % 3 == 0}
b = {i for i in range(1, 101) if i % 5 == 0}

print(a & b)

listv = [dan * num for dan in range(1, 10) for num in range(1, 10)]
setv =  { dan * num for dan in range(1, 10) for num in range(1, 10)}

print(listv)
print(setv)

#keyword argument
def calcstep(**args):
    begin = args['begin']
    end = args['end']
    step = args['step']

    sum = 0
    for num in range(begin, end + 1, step):
        sum += num
    return sum


print("3 ~ 5 =", calcstep(begin=3, end=5, step=1))
print("3 ~ 5 =", calcstep(step=1, end=5, begin=3))
print("3 ~ 5 =", calcstep(3, 5, 1))

def asterisk_test(a, **kargs) :
    print(a, kargs)
    print(type(a), type(kargs))

asterisk_test(1, b=2, c=3, d=4, e=5, f=6)

def calcscore(name, *score, **option):
    print(name)
    sum = 0
    for s in score:
        sum += s
    print("총점 :", sum)
    if (option['avg'] == True ):
        print("평균 :", sum / len(score))

calcscore("김상형", 88, 99, 77, avg = True)
calcscore("김한슬", 99, 98, 95, 89, avg = False)

#string format
# ===== stringcat  =====
price = 500
print("궁금하면 " + str(price) + "원!")

# ===== format  =====
price = 500
print("궁금하면 %d원!" % price)

# ===== format2  =====
month = 8
day = 15
anni = "광복절"
print("%d월 %d일은 %s이다." % (month, day, anni))

# =====width  =====
value = 123
print("###%d###" % value)
print("###%5d###" % value)
print("###%10d###" % value)
print("###%1d###" % value)

# =====align  =====
price = [30, 13500, 2000]
for p in price:
    print("가격:%d원" % p)
for p in price:
    print("가격:%7d원" % p)
print("%d - %d - %d" % tuple(price))

# =====numalign  =====
price = [30, 13500, 2000]
for p in price:
    print("가격:%-7d원" % p)
    print("가격:%7d원" % p)

# =====precision  =====
pie = 3.14159265
print("%10f" % pie)
print("%10.8f" % pie)
print("%10.5f" % pie)
print("%10.2f" % pie)

#===== 1000단위 , 사용 =====
num = 1000000
print('%s' % format(num, ','))

# 파이썬 2.6 과 3.0부터 사용 가능
# =====newformat  =====
name = "한결"
age = 16
height = 162.5
print("이름:{}, 나이:{}, 키:{}".format(name, age, height))

# =====newformat2  =====
name = "한결"
age = 16
height = 162.5
print("이름:{0:s}, 나이:{1:d}, 키:{2:f}".format(name, age, height))

# =====newformat3  =====
name = "한결"
age = 16
height = 162.5
print("이름:{0:10s}, 나이:{1:5d}, 키:{2:8.2f}".format(name, age, height))

# =====newformat4  =====
name = "한결"
age = 16
height = 162.5
print("이름:{0:^10s}, 나이:{1:>5d}, 키:{2:<8.2f}".format(name, age, height))

# =====newformat5  =====
name = "한결"
age = 16
height = 162.5
print("이름:{0:$^10s}, 나이:{1:>05d}, 키:{2:!<8.2f}".format(name, age, height))

#===== 1000단위 , 사용 =====
num = 1000000
print('{:,}'.format(num))

# 파이썬 3.6부터 사용 가능
# ===== newnewformat  =====
name = "한결"
age = 16
height = 162.5
print(f"이름:{name}, 나이:{age}, 키:{height}")

# ===== newnewformat2  =====
name = "한결"
age = 16
height = 162.5
print(f"이름:{name:s}, 나이:{age:d}, 키:{height:f}")

# ===== newnewformat3  =====
name = "한결"
age = 16
height = 162.5
print(f"이름:{name:10s}, 나이:{age:5d}, 키:{height:8.2f}")

# ===== newnewformat4  =====
name = "한결"
age = 16
height = 162.5
print(f"이름:{name:^10s}, 나이:{age:>5d}, 키:{height:<8.2f}")

# ===== newnewformat5  =====
name = "한결"
age = 16
height = 162.5
print(f"이름:{name:$^10s}, 나이:{age:>05d}, 키:{height:!<8.2f}")

#===== 1000단위 , 사용 =====
num = 1000000
print(f'{num:,}')

print('{} and {}'.format('You', 'Me'))
print('{0} and {1} and {0}'.format('You', 'Me'))
print('{var1} are {var2}'.format(var1='You', var2='Niceman'))

print('%s: %d' % ('나이', 30))                   	 #문자열과 정수 출력
print('{}: {}'.format('나이', 30))                            # %[-]폭[.유효자리수]서식

print('%f,%.2f' % (1.123, 1.123))        		 #실수 출력
print('{:f}, {:.2f}'.format(1.123, 1.123))

print('%o, %x, %X' % (10, 10, 10))      		 #진법 출력
print('{:b}, {:o}'.format(10, 10))
print('{:x}, {:X}'.format(10, 10))

print('|%5d|' % 123)      			 #고정 길이 출력
print('|%5s|' % 'abc')
print('|{:5}|'.format(123))
print('|{:5}|'.format('abc'))

print('|%-5d|' % 123)    			 # 고정 길이의 정렬
print('|%5s|' % 'abc')
print('|{:<5}|'.format(123))
print('|{:>5}|'.format('abc'))
print('|{:^5}|'.format('abc'))

print('|%05d|' % 123)           			#여백 채우기
print('|{:05}|'.format(123))
print('|{:_>5}|'.format('abc'))
print('|{:-^5}|'.format('abc'))

print('{:,}'.format(1000000))        		#정수, 실수 단위 구분
print('{:,.2f}'.format(1000000))

# =============== index  ===============
s = "python"
print(s[2])
print(s[-2])

# =============== stringindex  ===============
s = "python"
for c in s:
    print(c, end="")

# =============== slice  ===============
s = "python"
print("\n"+s[2:5])
print(s[3:])
print(s[:4])
print(s[2:-2])
print(s[2:4])

# =============== slice2  ===============
file = "20171224-104830.jpg"
print("촬영 날짜 : " + file[4:6] + "월 " + file[6:8] + "일")
print("촬영 시간 : " + file[9:11] + "시 " + file[11:13] + "분")
print("확장자 : " + file[-3:])

# =============== slice3  ===============
yoil = "월화수목금토일"
print(yoil[::2])
print(yoil[::-1])

# =============== find  ===============
s = "python programming"
print(len(s))
print(s.find('o'))
print(s.rfind('o'))
print(s.index('r'))
print(s.count('n'))

# =============== count  ===============
s = """생각이란 생각할수록 생각나므로 생각하지 말아야 할 생각은 생각하지 
않으려고 하는 생각이 옳은 생각이라고 생각합니다."""
print("생각의 출현 횟수 :", s.count('생각'))

# =============== in  ===============
s = "python programming"
print('a' in s)
print('z' in s)
print('pro' in s)
print('x' not in s)

# =============== startswith  ===============
name = "김한결"
if name.startswith("김"):
    print("김가입니다.")
if name.startswith("한"):
    print("한가입니다.")

file = "girl.jpg"
if file.endswith(".jpg"):
    print("그림 파일입니다.")

# =============== isdecimal  ===============
height = input("키를 입력하세요 :")
if height.isdecimal():
    print("키 =", height)
else:
    print("숫자만 입력하세요.")

# =============== lower  ===============
s = "Good morning. my love KIM."
print(s.lower())
print(s.upper())
print(s)

print(s.swapcase())
print(s.capitalize())
print(s.title())

# =============== strlower  ===============
python = input("파이썬의 영문 철자를 입력하시오 : ")
if python.lower() == "python":
    print("맞췄습니다.")

# =============== strip  ===============
s = "  angel   "
print(s + "님")
print(s.lstrip() + "님")
print(s.rstrip() + "님")
print(s.strip() + "님")

# =============== split  ===============
s = "짜장 짬뽕 탕슉"
print(s.split())

s2 = "서울->대전->대구->부산"
city = s2.split("->")
print(city)
for c in city:
    print(c, "찍고", end = ' ')

# =============== splitlines  ===============
traveler = """강나루 건너서\n밀밭 길을\n\n구름에 달 가듯이\n가는 나그네\n
길은 외줄기\n남도 삼백리\n\n술 익는 마을마다\n타는 저녁놀\n
구름에 달 가듯이\n가는 나그네"""
poet = traveler.splitlines()
for line in poet:
    print(line)

# =============== join  ===============
s = "._."
print(s.join("대한민국"))

# =============== splitjoin  ===============
s2 = "서울->대전->대구->부산"
city = s2.split("->")
print(" 찍고 ".join(city))

# =============== replace  ===============
s = "독도는 일본땅이다. 대마도도 일본땅이다."
print(s)
print(s.replace("일본", "한국"))

# =============== just  ===============
message = "안녕하세요."
print(message.ljust(30))
print(message.rjust(30))
print(message.center(30))

# =============== center  ===============
traveler = """강나루 건너서\n밀밭 길을\n\n구름에 달 가듯이\n가는 나그네\n
길은 외줄기\n남도 삼백리\n\n술 익는 마을마다\n타는 저녁놀\n
구름에 달 가듯이\n가는 나그네"""
poet = traveler.splitlines()
for line in poet:
    print(line.center(30))

text = "Py@12가 나%"

for data in text :
    print(data)

print("-"*20)

for data in text :
    if data.isalpha() :
        print("문자(", data,")", end="", sep="")
    if data.isdigit() :
        print("숫자(", data,")", end="", sep="")
    if data.isascii() :
        print("아스키(", data, ")", end="", sep="")
    if data.islower() :
        print("소문자(", data, ")", end="", sep="")
    if data.isupper() :
        print("대문자(", data, ")", end="", sep="")
    if data.isspace() :
        print("공백문자(", data, ")", end="", sep="")
    if data.isalnum() :
        print("문자 또는 숫자(", data, ")", end="", sep="")
    print("\n------")

str1 = "prettyflower"
str2 = "this is string example....wow!!! this is really string"
print("Capitalize: ", str1.capitalize())
print("endswith?: ", str1.endswith("r"))
print("join str: ", str1.join(["I'm ", "!"]))
print("replace1: ", str1.replace('pretty', 'Good'))
print("replace2: ", str2.replace("is", "was", 3))
print("split: ", str2.split(' '))  # Type 확인
print("sorted: ", sorted(str1))  # reverse=True
print("reversed1: ", reversed(str1)) #list 형 변환
print("reversed2: ", list(reversed(str1)))

# =============== sort  ===============
score = [ 88, 95, 70, 100, 99 ]
score.sort()
print(score)
score.reverse()
print(score)

# =============== sort2  ===============
country = ["Korea", "japan", "CHINA", "america"]
country.sort()
print(country)
country.sort(key = str.lower)
print(country)

# =============== sort3 ===============
country = ["Korea", "japan", "CHINA", "america"]
country.sort()
print(country)
country.sort(key = len)
print(country)

# =============== sorted  ===============
score = [ 88, 95, 70, 100, 99 ]
score2 = sorted(score)
print(score)
print(score2)

# datetime
import datetime

print([4,15,2,30,4].count(4))
listv = [4,15,2,30,4]
print(listv.count(4))

now = datetime.date.today()
print(now, type(now))
print(now.weekday())
print(now.ctime())

christmas = datetime.date(2020, 12, 25)
print(christmas, type(christmas))
print(christmas.weekday())
print(christmas.ctime())
    


```



### - 실습

```python
def mydict(**kwargs):
    returnDic = {}

#    if len(kwargs.keys()) == 0:
#        return returnDic

#    for keyValue in kwargs.items():
#        key, value = keyValue

    for key, value in kwargs.items():
        returnDic['my' + key] = value

    return returnDic


print(mydict())
print(mydict(A=1, B=2, C=3))
argTest = {'A': '1', 'B': '2'}
print(mydict(**argTest))

def myprint(*args, **kwargs):
    deco = '**'
    sep = ','
    tempPrint = ''

    if len(args) == 0 and len(kwargs.keys()) == 0:
        print('Hello Python')

    else:
        if kwargs.get('deco'):
            deco = kwargs['deco']

        if 'sep' in kwargs.keys():      # get으로 value가 None은 처리 안됨
            sep = kwargs['sep']

        print(deco, sep='', end='')
        for charPrint in args:
            tempPrint += str(charPrint)
            tempPrint += str(sep)
        print(tempPrint[0:-1], sep='', end='')
        print(deco, sep='')

        print(*args, sep=sep)

myprint(10, 20, 30, deco="@", sep="-")
myprint("python", "javascript", "R", deco="$")
myprint("가", "나", "다")
myprint(100)
myprint(True, 111, False, "abc", deco="&", sep="")
myprint()

arg1 = (10, 20, 30, 40, 50)
arg2 = {'deco': '*', 'sep' : '-'}

#print(type(arg1))
#print(type(arg2))

myprint(*arg1, **arg2)
```

