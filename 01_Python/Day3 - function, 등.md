

# Day2

> print, for문, input, time 등

### - 교육내용

```python
# 함수의 필요성을 점검하는 예제
sum = 0
for num in range( 5):
    sum += num
print("~ 4 =", sum)

sum = 0
for num in range(11):
    sum += num
print("~ 10 =", sum)

def calcsum(n):
    sum = 0
    for num in range(n + 1):
        sum += num
    return sum

print("~ 4 =", calcsum(4))
print("~ 10 =", calcsum(10))

def calcrange(begin, end):
    sum = 0
    for num in range(begin, end + 1):
        sum += num
    return sum

print("3 ~ 7 =", calcrange(3, 7))

def printsum(n):
    sum = 0
    for num in range(n + 1):
        sum += num
        print(num)
    print("~", n, "=", sum)

printsum(4)
printsum(10)

def print_name() :
    print("유니코")
    return


print("수행시작")
print_name()
print(1)
print_name()
print(2)
print_name()
print(3)
print("수행종료")

def print_name(num) :
    for i in range(num) :
        print("유니코", i)

print("수행시작")
print_name(5)
print("수행종료")

def print_name(num, deco) :
    for i in range(num) :
        print(deco * num, "유니코", deco * num)


print("수행시작")
print_name(1, '#')
print("-" * 10)
print_name(3, '*')
print("-" * 10)
print_name(2, '@')
print("-" * 10)
print_name(int(3.14), '%')
print("수행종료")

def add(num1, num2) :
    return num1 + num2

r1 = add(10, 20)
v1 = 100; v2 = 200
r2 = add(v1, v2)
print(r1)
print(r2)
print(add(1000, 2000))
print(1+add(1000, 2000))

def add(num1, num2) :
    print(num1 + num2)

r1 = add(10, 20)
v1 = 100; v2 = 200
r2 = add(v1, v2)
print(r1)
print(r2)
print(add(1000, 2000))
print(1+add(1000, 2000))

def mul(a, b):
    c = a * b
    return c

def add(a, b):
    c = a + b
    print(c)
    d = mul(a, b)
    print(d)

x = 10
y = 20
add(x, y)

def coffee_machine(button) :
     print()
     print("#1. (자동으로) 뜨거운 물을 준비한다.");
     print("#2. (자동으로) 종이컵을 준비한다.");

     if button == 1 :
          print("#3. (자동으로) 보통커피를 탄다.")
     elif button == 2 :
          print("#3. (자동으로) 설탕커피를 탄다.")
     elif button == 3 :
          print("#3. (자동으로) 블랙커피를 탄다.")
     else :
          print("#3. (자동으로) 아무거나 탄다.\n")

     print("#4. (자동으로) 물을 붓는다.");
     print("#5. (자동으로) 스푼으로 젓는다.");
     print()

coffee = int(input("A손님, 어떤 커피 드릴까요?(1:보통, 2:설탕, 3:블랙)"))
coffee_machine(coffee)
print("A손님~ 커피 여기 있습니다.")

coffee = int(input("B손님, 어떤 커피 드릴까요?(1:보통, 2:설탕, 3:블랙)"))
coffee_machine(coffee)
print("B손님~ 커피 여기 있습니다.")

coffee = int(input("C손님, 어떤 커피 드릴까요?(1:보통, 2:설탕, 3:블랙)"))
coffee_machine(coffee)
print("C손님~ 커피 여기 있습니다.")

def isType(p) :
    if type(p) == int :
        result = "정수를 전달했네요"
    elif type(p) == float :
        result = "실수를 전달했네요"
    elif type(p) == str :
        result = "문자열을 전달했네요"
    elif type(p) == bool :
        result = "논리값을 전달했네요"
    else :
        result = "몰라용^^"
    print(type(p))
    return result

print(isType(100))
print(isType(3.14))
print(isType("100"))
print(isType("aaa"))
print(isType(True))
print(isType([]))

def kim():
    temp = "김과장의 함수"
    print(temp)

def lee():
    temp = 2 ** 10
    return temp

def park(a):
    temp = a * 2
    print(temp)

kim()
print(lee())
park(6)
print(temp)

salerate = 0.9

def kim():
    print("오늘의 할인율 :", salerate)

def lee():
    price = 1000
    print("가격 :", price * salerate)

kim()
salerate = 1.1
lee()

price = 1000

def sale():
    price = 500
    print(price)

sale()
print(price)

price = 1000

def sale():
    global price
    price = 500
    print("sale", id(price))


sale()
print("global", id(price))

#price = 1000


def sale():
    global price
#    price = 500
    print(price)

sale()
print(price)

def calcsum(n):
    """1 ~ n까지의 합계를 구해 리턴한다."""
    sum = 0
    for i in range(n+1):
        sum += i
    return sum

print(calcsum(10))
help(calcsum)

import coffee_machine.py

strReturn = print('test')
print('strRetur =', strReturn)


def calcsum(n):
    sum = 0
    for num in range(1, n+1):
        sum += num
    return sum

#print('sum value from', '1 to 10 is', calcsum(10))

for x in range(1,11):
    print('sum value from', '1 to', x, 'is', calcsum(x))

```



### - 실습

```python
def expr(value1, value2, oper):
    if oper == '+':
        return value1 + value2
    elif oper == '-':
        return value1 - value2
    elif oper == '*':
        return value1 * value2
    elif oper == '/':
        return value1 / value2
    else:
        return None

# 저장
def expr2(value1, value2, oper):
    if oper == '+' or oper == '-' or oper == '*' or oper == '/':
        return eval(value1 + ' ' + oper + ' ' + value2)
    else:
        return None


while True:
    value1 = int(input('첫번째 숫자를 입력하세요...'))
    value2 = int(input('두번째 숫자를 입력하세요...'))
    oper = input('연산자를 입력하세요...')

#    print('v1 =', value1, 'v2 =', value2, 'oper =', oper)

    result = expr(value1, value2, oper)

    if result == None:
        print('수행불가')
        break
    else:
        print('연산결과 :', result)
        print('='*20)
        
def print_book_title():
    print('파이썬 정복')


def print_book_publisher():
    print('한빛미디어')


for call in range(3):
    print_book_title()

for call in range(5):
    print_book_publisher()
    
def get_book_title():
    return '파이썬 정복'


def get_book_publisher():
    return '한빛미디어'


name = get_book_title()
for call in range(2):
    print(name)

print(get_book_publisher())

def expr(value1, value2, oper):
    if oper == '+':
        return value1 + value2
    elif oper == '-':
        return value1 - value2
    elif oper == '*':
        return value1 * value2
    elif oper == '/':
        return value1 / value2
    else:
        return None

# 저장
def expr2(value1, value2, oper):
    if oper == '+' or oper == '-' or oper == '*' or oper == '/':
        return eval(value1 + ' ' + oper + ' ' + value2)
    else:
        return None


while True:
    value1 = int(input('첫번째 숫자를 입력하세요...'))
    value2 = int(input('두번째 숫자를 입력하세요...'))
    oper = input('연산자를 입력하세요...')

#    print('v1 =', value1, 'v2 =', value2, 'oper =', oper)

    result = expr(value1, value2, oper)

    if result == None:
        print('수행불가')
        break
    else:
        print('연산결과 :', result)
        print('='*20)
        
def expr(value1, value2, oper):
    if oper == '+' or oper == '-' or oper == '*' or oper == '/':
        return eval(value1 + ' ' + oper + ' ' + value2)
    else:
        return None

while True:
    value1 = input('첫번째 숫자를 입력하세요...')
    value2 = input('두번째 숫자를 입력하세요...')
    oper = input('연산자를 입력하세요...')

    result = expr(value1, value2, oper)

    if result == None:
        print('수행불가')
        break
    else:
        print('연산결과 :', result)

        print('='*20)
        
def print_triangle(lineCount):
    if lineCount < 1 or lineCount > 10:
       print('1~10 사이의 숫자만 넣어주세요...')
    else:
        for line in range(1, lineCount+1):
            print('*'*line)

# 랜덤으로 10번 테스트
import random
for test in range(10):
    num = random.randint(1, 15)
#    print(num)
    print_triangle(num)

def print_triangle(lineCount):
    if lineCount < 1 or lineCount > 10:
       print('1~10 사이의 숫자만 넣어주세요...')
    else:
        for line in range(1, lineCount+1):
            print('@'* (lineCount + 1- line))

# 랜덤으로 10번 테스트
import random
for test in range(10):
    num = random.randint(1, 15)
#    print(num)
    print_triangle(num)


def print_gugudan(matLevel):
    if type(matLevel) != int or matLevel < 1 or matLevel > 9:
        return None
    else:
        for cnt in range(1, 10):
            print(matLevel, 'x', cnt, '=', matLevel*cnt )


import random
for test in range(10):
    num = random.randint(1, 20)
#    print(num)
    print_gugudan(num)
    print('=' * 20)
    
def differtwovalue(value1, value2):
    return abs(value1-value2)


import random
for test in range(5):
    num1 = random.randint(1, 30)
    num2 = random.randint(1, 30)
#    print(num1, num2)
    print(num1, '와', num2, '의 차는', differtwovalue(num1, num2), '입니다.')
    print('=' * 20)
    
    
print("*입력한 숫자만큼 데코문자를 출력하는 프로그램입니다.*")
deco = input("데코문자를 입력하세요 : ")
number = int(input("출력횟수를 입력하세요 : "))
for i in range(number) :
    print(deco, end="")
print()
print("*수행 종료됩니다.*")


def drowDeco():
    deco = input("데코문자를 입력하세요 : ")
    number = int(input("출력횟수를 입력하세요 : "))
    for i in range(number) :
        print(deco, end="")
    print()


print("*입력한 숫자만큼 데코문자를 출력하는 프로그램입니다.*")
for count in range(3):
    drowDeco()
print("*수행 종료됩니다.*")


def drowDeco():
    deco = input("데코문자를 입력하세요 : ")
    number = int(input("출력횟수를 입력하세요 : "))
    for i in range(number) :
        print(deco, end="")
    print()


print("*입력한 숫자만큼 데코문자를 출력하는 프로그램입니다.*")
while True:
    drowDeco()
    ex = input("계속 수행할까요(y/n)?")
    if ex == 'n':
        break
    elif ex == 'y':
        continue
    else:
        print("y 또는 n을 입력하세요.")
        break
print("*수행 종료됩니다.*")

def drowDeco():
    while True:
        deco = input("데코문자를 입력하세요 : ")
        number = int(input("출력횟수를 입력하세요 : "))

        if number < 1:
            print("출력회수는 0보다 큰 숫자를 입력하세요!")
            continue
        else:
            break

    for i in range(number) :
        print(deco, end="")
    print()


print("*입력한 숫자만큼 데코문자를 출력하는 프로그램입니다.*")
while True:
    drowDeco()
    ex = input("계속 수행할까요(y/n)?")
    if ex == 'n':
        break
    elif ex == 'y':
        continue
    else:
        print("y 또는 n을 입력하세요.")
        break
print("*수행 종료됩니다.*")

```

