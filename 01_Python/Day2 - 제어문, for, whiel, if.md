

# Day2

> print, for문, input, time

### - 교육내용

```python
v1 = 1
while v1 < 6:
    print("v1 is :", v1)
    v1 += 1
print("*"*20)
for v2 in range(6):
    print("v2 is :", v2)
print("*"*20)
for v3 in range(1, 6):
    print("v3 is :", v3)
print("*"*20)
for v4 in range(1, 6, 2):
    print("v4 is :", v4)
print("*"*20)
for v5 in range(5, 0, -1):
    print("v5 is :", v5)
    
sum = 0
for num in range(1, 101):
    sum += num
print ("sum =",sum)

sum = 0
for num in range(2, 101, 2):
    sum += num
print ("sum =",sum)

for x in range(1, 51):
    if (x % 10 == 0):
        print('+', end= '')
    else:
        print('-', end = '')
print()
for x in range(1, 5):
    print('-' * 9, end = '')
    print('+', end = '')
print()
for x in range(1, 51):
    if (x % 5 == 0):
        print('+', end= '')
    else:
        print('-', end = '')
print()
for x in range(1, 51):
    if (x % 10 == 5):
        print('+', end= '')
    else:
        print('-', end = '')
        
for x in range(1, 51):
    if (x % 10 == 0):
        print('+', end= '')
    else:
        print('-', end = '')

for x in range(1, 5):
    print('-' * 9, end = '')
    print('+', end = '')

x = 1
while x <= 50:
    if (x % 10):
        print('-', end= '')
    else:
        print('+', end = '')
    x += 1

for x in range(1, 51):
    if (x % 5 == 0):
        print('+', end= '')
    else:
        print('-', end = '')

for x in range(1, 51):
    if (x % 10 == 5):
        print('+', end= '')
    else:
        print('-', end = '')
        
startNum = int(input("시작 숫자 : "))
endNum = int(input("종료 숫자 : "))
incNum = int(input("증가치 숫자 : "))

for num in range(startNum, endNum+1, incNum) :
    print(num, end=" ")

for dan in range(2, 10):
    print(dan, "단")
    for num in range(2, 10):
        print(dan, "*", num, "=", dan * num, end="\t")
    print()
    
for dan in range(2, 10):
    for num in range(2, 10):
        result = dan * num
        if result > 30 :
            break
        print(dan, "*", num, "=", result, end="\t")
    print()

endFlag = False
for dan in range(2, 10):
    if endFlag :
        break
    for num in range(2, 10):
        result = dan * num
        if result > 30 :
            endFlag = True
            break
        print(dan, "*", num, "=", result, end="\t")
        
for y in range(1, 10) :
    for x in range(10-y) :
#    for x in range(1, 10):
        print('*', end = '')
    print()
    
#age = int(input('너 몇살이니? '))
age = 1
if age < 19:
    print('애들은 가라')
elif age < 20:
    print('20세')
else :
    print('나이모름')

a = 1
if a == 3:
    print("3이다")
if a > 5:
    print("5보다 크다")
if a < 5:
    print("5보다 작다")
if a != 3:
    print("3이 아니다")
    
country = "Korea"
if country == "Korea":
    print("한국입니다.")
if country == "korea":
    print("대한민국입니다.")

if ("kor" > "japan"):
    print("한국이 더 크다")
if ("korea" < "japan"):
    print("일본이 더 크다")
    
energy = 1
if energy:
    print("열심히 싸운다")

a = 3
if a > 1 and a < 10:
    print("OK")

age = 16
if age < 19:
    print("1 - 애들은 가라")
    print("1 - 공부 열심히 해야지")

age = 22
if age < 19:
    print("2 - 애들은 가라")
print("2 - 공부 열심히 해야지")

if age < 19:
    print("3 - 애들은 가라")
else:
    print("3 - 어서 옵쇼")

age = 12
if age < 19:
    print("4 - 애들은 가라")
    print("4 - 공부 열심히 해야지")
else:
    print("4 - 어서 옵쇼")
    print("4 - 즐거운 시간 되세요")

age = 23
if age < 19:
    print("애들은 가라")
elif age < 19:          #여기는 실행 안됨
    print("19")
elif age < 25:
    print("대학생입니다")
else:
    print("어서 옵쇼")



if age < 19:
    print("애들은 가라")
if age >= 19 and age < 25:
    print("대학생입니다")
if age >= 25:
    print("어서 옵쇼")


age = 24
if age < 19:
    print("3애들은 가라")
elif 19 <= age < 25:
    print("3대학생입니다")
elif 25 <= age:
    print("3어서 옵쇼")
else:
    print("3N/A")
    
money = 6500
if money >= 20000:
    print("탕수육을 먹는다")
elif money >= 10000:
    print("쟁반 짜장을 먹는다")
elif money >= 6000:
    print("짬뽕을 먹는다")
elif money >= 4000:
    print("짜장면을 먹는다")
else:
    print("단무지를 먹는다")
print("뭐든 맛있다!!")


man = True
age = 22
if man == True:
    if age >= 19:
        print("1 - 성인 남자입니다.")


if man == True:
    if age >= 19:
        print("2 - 성인 남자입니다.")
    else:
        print("2 - 소년입니다.")

if man == True:
    if age >= 19:
        print("3 - 성인 남자입니다.")
else:
    print("3 - 소년입니다.")
    
import random
num = random.randint(1, 20)
print('num = ', num)
print("-"*50)

if num % 2 == 0 :
    print(num, "은 짝수", sep="")
else :
    print(num, "은 홀수", sep="")
print("-"*50)

if num % 2 == 0 :
    print(num)
    print("은 짝수")
else :
    print(num)
    print("은 홀수")
print("-"*50)

if num % 2 == 0 :
    print(num, end="")
    print("은 짝수")
else :
    print(num, end="")
    print("은 홀수")
print("-"*50)

import random
num = random.randint(1, 20)

print("num(", num, ") : ", sep="", end="")
if num < 10 :
    print("10보다 작은 수-", end="")
    if num < 5 :
        print("5보다 작은 수-", end="")
    else :
        print("5보다 큰 수-", end="")
else :
    print("10보다 큰 수-", end="")
print("OK?")

data = input("데이터를 입력하세용 : ")
print("[" + data + "]")
if len(data) == 0:
    print("입력한 내용이 없네요")
else:
    print("입력한 내용 :", data)



data = input("데이터를 입력하세용 : ")
print("[" + data + "]")
if not len(data):
    print("입력한 내용이 없네요")
else:
    print("입력한 내용 :", data)


data = input("데이터를 입력하세용 : ")
print("[" + data + "]")
if not (data):
    print("입력한 내용이 없네요")
else:
    print("입력한 내용 :", data)

age = 12
if age < 19:
    print("4 - 애들은 가라")
print("4 - 공부 열심히 해야지")
else:
    print("4 - 어서 옵쇼")
    print("4 - 즐거운 시간 되세요")

print(round(123456789,-1))

print(round(0.23456,4))
print(round(0.23456,3))
print(round(0.23456,2))
print(round(0.23456,1))

student = 1
while student <= 5:
    print(student, "번 학생의 성적을 처리한다.")
    student += 1
print("수행종료")


num = 1
sum = 0
while num <= 100:
    sum += num
    num += 1
print ("sum =", sum)

num = 151
sum = 0
while num <= 300:
    sum += num
    num += 2
print ("sum =",sum)

print("3 + 4 = ?")
while True:
    a = int(input("정답을 입력하시오 : "))
    if (a == 7):
        break
print("참 잘했어요")

import random    # random 모듈을 가져옴

i = 0
count = 0;
while i != 3:    # 3이 아닐 때 계속 반복
    i = random.randint(1, 6)    # randint를 사용하여 1과 6 사이의 난수를 생성
    print(i)
    count += 1
print(count, "회 반복", sep="")
```



### - 실습

```python
num = int(input('숫자 하나를 입력하세요...'))
if num > 10 :
    print("[", num, "]", "\n", "OK")
#else :
#    print("[", num, "]", "\n", "Not OK")

colorName = input('칼라 이름을 하나 입력해 주세요...')
if colorName == 'red':
    print("[", colorName, "]", "\n", "#ff0000")
else :
    print("[", colorName, "]", "\n", "#000000")

import random
grade = random.randint(1, 6)

if not(grade != 1 and grade != 2 and grade != 3) :
    print(grade, ' 학년은 저학년입니다.', sep='')
if not(grade != 4 and grade != 5 and grade != 6) :
    print(grade, ' 학년은 고학년입니다.', sep='')

import random
grade = random.randint(1, 6)

if grade == 1 or grade == 2 or grade == 3 :
    print(grade, ' 학년은 저학년입니다.', sep='')
elif grade == 4 or grade == 5 or grade == 6 :
    print(grade, ' 학년은 고학년입니다.', sep='')

    
import random
score = random.randint(0, 100)

if score >= 90 :
    print(score, '점은 A등급입니다.', sep='')
elif score >= 80:
    print(score, '점은 B등급입니다.', sep='')
elif score >= 70:
    print(score, '점은 C등급입니다.', sep='')
elif score >= 60:
    print(score, '점은 D등급입니다.', sep='')
elif score < 60:
    print(score, '점은 F등급입니다.', sep='')
else :
    print(score, '에러', sep='')

import random
score = random.randint(0, 100)

if score >= 90 :
    #print(score, '점은 A등급입니다.', sep='')
    grade = 'A'
elif score >= 80:
    #print(score, '점은 B등급입니다.', sep='')
    grade = 'B'
elif score >= 70:
    #print(score, '점은 C등급입니다.', sep='')
    grade = 'C'
elif score >= 60:
    #print(score, '점은 D등급입니다.', sep='')
    grade = 'D'
elif score < 60:
    #print(score, '점은 F등급입니다.', sep='')
    grade = 'F'
else :
    #print(score, '에러', sep='')
    grade = '에러'

print(score, '점은 ', grade, '등급입니다.', sep='')

num = int(input('1부터 10사이의 숫자를 하나 입력하세요 :'))
if 1 <= num <= 10 :
    if num % 2 == 1 :
        print(num, ' : 홀수')
    elif num % 2 == 0 :
        print(num, ' : 짝수')
    else :
        print(num, ' : ????')
else :
    print('1부터 10사이의 값이 아닙니다.')

print("짝수" if num%2 ==0 else "홀수")

string="짝수" if num%2 ==0 else "홀수"
print(string)

c=[i for i in range(10)]
print(c)


import random
operNum = random.randint(1, 5)

if operNum == 1:
    result = 300 + 50
elif operNum == 2:
    result = 300 - 50
elif operNum == 3:
    result = 300 * 50
elif operNum == 4:
    result = 300 / 50
elif operNum == 5:
    result = 300 % 50
else :
    result = '에러'
#print('선택 값 : \n', operNum, sep='')
print('결과 값 : ', result, sep='')

for cnt in range(1, 11):
    print(cnt, end=' ')
    
for num in range(9, 3, -1):
    print(num, ':', '홀수' if num % 2 == 1 else '짝수')
    
import random
ranNum1 = random.randint(1, 10)
ranNum2 = random.randint(30, 40)
sum = 0

#print(ranNum1, ranNum2)

for num in range(ranNum1, ranNum2+1):
#    print(num, end=" ")
    if num % 2 == 0:
        sum = sum + num

print(ranNum1, '부터', ranNum2, '까지의 짝수의 합 :', sum)

evenNum = 0
oddNum = 0

for sumNum in range(1, 101):
    if sumNum % 2 == 1 :        #홀수
        oddNum = oddNum + sumNum
    else :                                  #짝수
        evenNum = evenNum + sumNum
print('1부터 100까지의 숫자들중에서')
print('짝수의 합은 ', evenNum, ' 이고', '\n', '홀수의 합은 ', oddNum, ' 이다.', sep='')

sumNum = 0

for num in range(1, 51):
    if num % 3 == 0 and not(num % 5 == 0):
        sumNum = sumNum + num
print('결과 =', sumNum)

sumNum = 0

for num in range(1, 51):
    if num % 5 == 0 :
        continue
    if num % 3 == 0:
        sumNum = sumNum + num
print('결과 =', sumNum)

for dan in range(2, 10) :
    print(dan, '단')
    for gop in range(1,10) :
        print(dan, '*', gop, '=', dan * gop)

import random
num = random.randint(5, 10)
x = 1

#for x in range(1, num) :
while x <= num :
    print( x, '->', x**2)
    x += 1
    
import random
while True:
    pairNum1 = random.randint(1, 6)
    pairNum2 = random.randint(1, 6)
#    print(pairNum1, pairNum2)

    if pairNum1 == pairNum2:
        print("게임끝")
        break
    else:
        print('pairNum1이 pairNum2 보다 크다.' if pairNum1 > pairNum2 else 'pairNum1이 pairNum2 보다 작다')

        
import random

count =0
while True:
    ranNum = random.randint(0, 30)

    if ranNum == 0 or (ranNum >= 27 and ranNum <=30):
        print('수행횟수는', count, '번입니다.')
        break
    else:
        print(chr(ranNum+64), '(', ranNum, ')', sep='')

    count += 1

while True:
    mon = int(input('월을 입력하세요...'))
    if mon < 1 or mon > 12:
        print('1~12 사이의 값을 입력하세요!', mon)
        break
    else:
        if mon == 12 or mon <= 2:
            season = '겨울'
        elif 3 <= mon <= 5:
            season = '봄'
        elif 6 <= mon <= 8:
            season = '여름'
        elif 9 <= mon <= 11:
            season = '가을'
        else:
            season = '에러'
        print(mon, '월은 ', season, sep='')

```

