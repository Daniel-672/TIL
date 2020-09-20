

# Day10

> class

### - 교육내용

```python
balance = 8000

def deposit(money):
    global balance
    balance += money

def inquire():
    print("잔액은 %s원입니다." % format(balance,','))

deposit(1000)
inquire()


def deposit(name, money):
    if name == "둘리" :
        global balancedooly
        balancedooly += money
    elif name == "또치" :
        global balanceddochi
        balanceddochi += money
    elif name == "도우너" :
        global balancedouner
        balancedouner += money

def inquire(name):
    if name == "둘리":
        print("%s의 잔액은 %s원입니다." % (name, format(balancedooly, ',')))
    elif name == "또치":
        print("%s의 잔액은 %s원입니다." % (name, format(balanceddochi, ',')))
    elif name == "도우너":
        print("%s의 잔액은 %s원입니다." % (name, format(balancedouner, ',')))

dooly = "둘리"
ddochi = "또치"
douner = "도우너"

balancedooly = 8000
balanceddochi = 8000
balancedouner = 8000

deposit(dooly, 1000)
inquire(dooly)

deposit(ddochi, 2000)
inquire(ddochi)

deposit(douner, 3000)
inquire(douner)

class Account:
    def __init__(self, name, balance):
        self.name = name
        self.balance = balance

    def deposit(self, money):
        self.balance += money

    def inquire(self):
        print("%s의 잔액은 %s원입니다." % (self.name, format(self.balance, ',')))


obj1 = Account("둘리", 8000)
obj2 = Account("또치", 8000)
obj3 = Account("도우너", 8000)

obj1.deposit(1000)
obj2.deposit(2000)
obj3.deposit(3000)

obj1.inquire()
obj2.inquire()
obj3.inquire()


class Human:
    def __init__(self, age, name):
        self.age = age
        self.name = name

    def intro(self):
        print(str(self.age) + "살 " + self.name + "입니다.")


kim = Human(29, "김상형")
kim.intro()
lee = Human(45, "이승우")
lee.intro()


class Human:
    def __init__(self, age, name):
        self.age = age
        self.name = name

    def intro(self):
        print(str(self.age) + "살 " + self.name + "입니다")

    def eat(self):
        print("밥을 먹는다")


class Student(Human):
    def __init__(self, age, name, stunum):
        super().__init__(age, name)
        self.stunum = stunum

    def intro(self):
        super().intro()
        print("학번 : " + str(self.stunum))

    def study(self):
        print("하늘천 따지 검을현 누를황")


kim = Human(29, "김상형")
kim.intro()
kim.eat()
print("-*-"*10)

lee = Student(34, "이승우", 930011)
lee.intro()
lee.study()
lee.eat()


# 부모 클래스를 선언합니다.
class Parent:
    def __init__(self):
        self.value = "테스트"
        print("Parent 클래스의 __init()__ 메서드가 호출되었습니다.")
    def test(self):
        print("Parent 클래스의 test() 메서드입니다.")

# 자식 클래스를 선언합니다.
class Child(Parent):
    def __init__(self):
        super().__init__()
        print("Child 클래스의 __init()__ 메서드가 호출되었습니다.")

# 자식 클래스의 인스턴스를 생성하고 부모의 메서드 호출
child = Child()
child.test()
print(child.value)



```



### - 실습

```python
class Member:
    def __init__(self):
        self.name = None
        self.account = None
        self.passwd = None
        self.birthyear = None


mem1 = Member()
mem1.name = '둘리'
mem1.account = 'dooly'
mem1.passwd = 'dooly123'
mem1.birthyear = '1988'

mem2 = Member()
mem2.name = '또치'
mem2.account = 'ddochi'
mem2.passwd = 'ddochi123'
mem2.birthyear = '1989'

mem3 = Member()
mem3.name, mem3.account, mem3.passwd, mem3.birthyear ={'도우너', 'douner', 'douner123', '1990'}


print("회원1: %s(%s,%s,%s)" % (mem1.name, mem1.account, mem1.passwd, mem1.birthyear))
print("회원2: %s(%s,%s,%s)" % (mem2.name, mem2.account, mem2.passwd, mem2.birthyear))
print("회원3: %s(%s,%s,%s)" % (mem3.name, mem3.account, mem3.passwd, mem3.birthyear))

class Book:
    def __init__(self, title, author, price):
        self.title = title
        self.author = author
        self.price = price

    def getBookInfo(self):
        return self.title, self.author, format(self.price, ',')
#        return f"{self.title}, {self.author}, {format(self.price, ',')}"

book1 = Book('파이썬 정복', '김상형', 22000)
print(book1.getBookInfo())
# book2 = Book('생활코딩! HTML + CSS + 자바스크립트', '이고잉', 27000)
# book3 = Book('김미경의 리부트', '김미경', 14400)
# book4 = Book('재테크 사부 존리', '존 리', 13500)
# book5 = Book('부의 대이동', '오건영', 15300)

# print("%s\n%s\n%s\n" % (book1.getBookInfo()) + "-" * 10)
# print("%s\n%s\n%s\n" % (book2.getBookInfo()) + "-" * 10)
# print("%s\n%s\n%s\n" % (book3.getBookInfo()) + "-" * 10)
# print("%s\n%s\n%s\n" % (book4.getBookInfo()) + "-" * 10)
# print("%s\n%s\n%s\n" % (book5.getBookInfo()))

# 찍기 test1
# for lst in range(1, 6):
#     callObject = 'book' + str(lst) + '.getBookInfo()'
#     print("%s\n%s\n%s\n" % (eval(callObject)) + "-" * 10)

# 찍기 test2
funcList = []

funcList.append(Book('파이썬 정복', '김상형', 22000))
funcList.append(Book('생활코딩! HTML + CSS + 자바스크립트', '이고잉', 27000))
funcList.append(Book('김미경의 리부트', '김미경', 14400))
funcList.append(Book('재테크 사부 존리', '존 리', 13500))
funcList.append(Book('부의 대이동', '오건영', 15300))


for lst in range(0, len(funcList)):
    if lst != len(funcList) - 1:
        print("%s\n%s\n%s\n" % funcList[lst].getBookInfo() + "-" * 10)
    else:
        print("%s\n%s\n%s\n" % funcList[lst].getBookInfo())




# print("%s\n%s\n%s\n" % funcList[lst].getBookInfo() + "-" * 10 if lst != len(funcList)-1 else "%s\n%s\n%s\n" % funcList[lst].getBookInfo())

```

