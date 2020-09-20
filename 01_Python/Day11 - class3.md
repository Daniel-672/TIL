

# Day11

> class3

### - 교육내용

```python
class Student:
    count = 0 # 클래스 변수 초기화

    def __init__(self, name, korean, math, english, science):
        # 인스턴스 변수 초기화
        self.name = name
        self.korean = korean
        self.math = math
        self.english = english
        self.science = science

        # 클래스 변수에 값 설정
        Student.count += 1
        print("{}번째 학생이 생성되었습니다.".format(Student.count))

    def pp():
        print('test')

# 학생 리스트를 선언합니다.
students = [
    Student("윤인성", 87, 98, 88, 95),
    Student("연하진", 92, 98, 96, 98),
    Student("구지연", 76, 96, 94, 90),
    Student("나선주", 98, 92, 96, 92),
    Student("윤아린", 95, 98, 98, 98),
    Student("윤명월", 64, 88, 92, 92)
]

# 출력합니다.
print()
print("현재 생성된 총 학생 수는 {}명입니다.".format(Student.count))

students[1].pp()



class Student:
    ''' 하하하 여기는 doc text '''
    count = 0 # 클래스 변수 초기화
    def __init__(self, name, korean, math, english, science):
        # 인스턴스 변수 초기화
        self.name = name
        self.korean = korean
        self.math = math
        self.english = english
        self.science = science

        # 클래스 변수에 값 설정
        Student.count += 1
        print("{}번째 학생이 생성되었습니다.".format(Student.count))


# 학생 리스트를 선언합니다.
students = [
    Student("윤인성", 87, 98, 88, 95),
    Student("연하진", 92, 98, 96, 98),
    Student("구지연", 76, 96, 94, 90),
    Student("나선주", 98, 92, 96, 92),
    Student("윤아린", 95, 98, 98, 98),
    Student("윤명월", 64, 88, 92, 92)
]

# 출력합니다.
print()
print("현재 생성된 총 학생 수는 {}명입니다.".format(Student.count))

print("Student 클래스의 네임스페이스 영역")
print(Student.__dict__)
for num, data in enumerate(students, 1) :
    print(f"Student 클래스에 의해 생성된 {num}번 객체의 네임스페이스 영역")
    print(data.__dict__)
    


class Student:
    # 클래스 변수
    count = 0
    students = []

    # 클래스 메서드
    @classmethod
    def print(cls):
        print("------ 학생 목록 ------")
        print("이름\t총점\t평균")
        for student in cls.students:
            print(str(student))
        print("------- ------- -------")

    # 초기화 메서드
    def __init__(self, name, korean, math, english, science):
        self.name = name
        self.korean = korean
        self.math = math
        self.english = english
        self.science = science
        Student.count += 1
        Student.students.append(self)

    # 인스턴스 메서드
    def get_sum(self):
        return self.korean + self.math +\
            self.english + self.science

    # 인스턴스 메서드
    def get_average(self):
        return self.get_sum() / 4

    # 인스턴스 메서드 : 오버라이딩
    def __str__(self):
        return "{}\t{}\t{}".format(\
            self.name,\
            self.get_sum(),\
            self.get_average())

# 학생 객체들 생성
Student("윤인성", 87, 98, 88, 95)
Student("연하진", 92, 98, 96, 98)
Student("구지연", 76, 96, 94, 90)
Student("나선주", 98, 92, 96, 92)
Student("윤아린", 95, 98, 98, 98)
Student("윤명월", 64, 88, 92, 92)
Student("김미화", 82, 86, 98, 88)
Student("김연화", 88, 74, 78, 92)
Student("박아현", 97, 92, 88, 95)
Student("서준서", 45, 52, 72, 78)

# 현재 생성된 학생을 모두 출력
Student.print()




class Student:
    # 클래스 변수
    count = 0
    students = []

    # 클래스 메서드
    @classmethod
    def print(cls):
        print("------ 학생 목록 ------")
        print("이름\t총점\t평균")
        for student in cls.students:
            print(str(student))
        print("------- ------- -------")

    # 초기화 메서드
    def __init__(self, name, korean, math, english, science):
        self.name = name
        self.korean = korean
        self.math = math
        self.english = english
        self.science = science
        Student.count += 1
        Student.students.append(self)

    # 인스턴스 메서드
    def get_sum(self):
        return self.korean + self.math +\
            self.english + self.science

    # 인스턴스 메서드
    def get_average(self):
        return self.get_sum() / 4

    # 인스턴스 메서드 : 오버라이딩
    def __str__(self):
        return "{}\t{}\t{}".format(\
            self.name,\
            self.get_sum(),\
            self.get_average())
Student.print()

Student("윤인성", 87, 98, 88, 95)
Student("연하진", 92, 98, 96, 98)
Student("구지연", 76, 96, 94, 90)
Student("나선주", 98, 92, 96, 92)
Student("윤아린", 95, 98, 98, 98)
Student("윤명월", 64, 88, 92, 92)
Student("김미화", 82, 86, 98, 88)
Student("김연화", 88, 74, 78, 92)
s1 = Student("박아현", 97, 92, 88, 95)
s2 = Student("서준서", 45, 52, 72, 78)

# 현재 생성된 학생을 모두 출력합니다.
Student.print()

print(Student.__dict__)
print(s1.__dict__)
print(s2.__dict__)
Student.print()





class Date:
    def __init__(self, month):
        self.month = month
    def getmonth(self):
        return self.month
    def setmonth(self, month):
        if 1 <= month <= 12:
            self.month = month

today = Date(8)
today.setmonth(15)
print(today.getmonth())
print("에고!"*5)
today.month = 20
print(today.getmonth())



class Date:
    def __init__(self, month):
        self.inner_month = month
    def getmonth(self):
        return self.inner_month
    def setmonth(self, month):
        if 1<= month <= 12:
            self.inner_month = month
    month = property(getmonth, setmonth)

today = Date(8)
today.month = 15
print(today.month)

print("에고!"*5)
today.inner_month = 20
print(today.month)



class Date:
    def __init__(self, month):
        self.inner_month = month
    @property
    def month(self):
        return self.inner_month
    @month.setter
    def month(self, month):
        if 1 <= month <= 12:
            self.inner_month = month

today = Date(8)
today.month = 15
print(today.month)

today = Date(8)
today.month = 15
print(today.month)

print("에고!"*5)
today.inner_month = 20
print(today.month)



class Date:
    def __init__(self, month):
        self.__month = month
    def getmonth(self):
        return self.__month
    def setmonth(self, month):
        if 1 <= month <= 12:
            self.__month = month
    month = property(getmonth, setmonth)

today = Date(8)
print(today.month)
today.__month = 15
print(today.month)

print("좋아!"*5)
today.__month = 20
print(today.month)


# 모듈을 가져옵니다.
import math
from MyError import NoNegativeNumberError

# 클래스를 선언합니다.
class Circle:
    def __init__(self, radius):
        if radius < 0 :
            raise NoNegativeNumberError("음의 값은 노노!!")
        self.radius = radius
    def get_circumference(self):
        return 2 * math.pi *  self.radius
    def get_area(self):
        return math.pi * (self.radius ** 2)

    # 겟터와 셋터를 선언합니다.
    def get_radius(self):
        return self.radius
    def set_radius(self, value):
        if value < 0 :
            raise NoNegativeNumberError("음의 값은 노노!!")
        self.radius = value

# 원의 둘레와 넓이를 구합니다.
circle = Circle(10)
print("# 원의 둘레와 넓이를 구합니다.")
print("원의 둘레:", circle.get_circumference())
print("원의 넓이:", circle.get_area())
print()

# 간접적으로 __radius에 접근합니다.
print("# radius에 접근합니다.")
print(circle.get_radius())
print()

# 원의 둘레와 넓이를 구합니다.
circle.set_radius(2)
print("# 반지름을 변경하고 원의 둘레와 넓이를 구합니다.")
print("원의 둘레:", circle.get_circumference())
print("원의 넓이:", circle.get_area())

print("생각해 봅시다!!!")
#circle.set_radius(-3
circle.radius = -3
print("# 반지름을 변경하고 원의 둘레와 넓이를 구합니다.")
print("원의 둘레:", circle.get_circumference())
print("원의 넓이:", circle.get_area())


# 모듈을 가져옵니다.
import math
from MyError import NoNegativeNumberError

# 클래스를 선언합니다.
class Circle:
    def __init__(self, __radius):
        if __radius < 0 :
            raise NoNegativeNumberError("음의 값은 노노!!")
        self.__radius = __radius
    def get_circumference(self):
        return 2 * math.pi *  self.__radius
    def get_area(self):
        return math.pi * (self.__radius ** 2)

    # 겟터와 셋터를 선언합니다.
    def get__radius(self):
        return self.__radius
    def set__radius(self, value):
        if value < 0 :
            raise NoNegativeNumberError("음의 값은 노노!!")
        self.__radius = value

# 원의 둘레와 넓이를 구합니다.
circle = Circle(10)
print("# 원의 둘레와 넓이를 구합니다.")
print("원의 둘레:", circle.get_circumference())
print("원의 넓이:", circle.get_area())
print()

# 간접적으로 ___radius에 접근합니다.
print("# __radius에 접근합니다.")
print(circle.get__radius())
print()

# 원의 둘레와 넓이를 구합니다.
circle.set__radius(2)
print("# 반지름을 변경하고 원의 둘레와 넓이를 구합니다.")
print("원의 둘레:", circle.get_circumference())
print("원의 넓이:", circle.get_area())

print("생각해 봅시다!!!")
circle.set__radius(-3)
#circle.__radius = -3
print("# 반지름을 변경하고 원의 둘레와 넓이를 구합니다.")
print("원의 둘레:", circle.get_circumference())
print("원의 넓이:", circle.get_area())


import time
class A:
    def __str__(self):
        return 'str method is called'

    def __repr__(self):
        return 'repr method is called'

a = A()

print(str(time.localtime()))

print(repr(time.localtime()))


class NoNegativeNumberError(Exception) :
    def __init__(self, msg):
        super().__init__("내가 만든 에러당  : " +msg) 
```



### - 실습

```python
class Card:
    '''이것은 카드 클래스 독 텍스트 하하하'''
    # 클래스 변수
    width = 100
    height = 200

    def __init__(self, kind, number):
        # 인스턴스 변수
        self.kind = kind
        self.number = number

    def __str__(self):
        # 형변환 오버라이딩
        return f"카드 종류 :\"{self.kind}\", 카드 숫자 :{self.number}, 카드의 크기 :({Card.width}, {Card.height})"


cards = [
        Card('Heart', 5),
        Card('Spade', 9),
        Card('Clover', 2),
        Card('Diamond', 10)
]

for obj in cards:
    print(obj)


# A = Card('Heart', 5)
# print(A , str(1), )


class Person:
    def __init__(self, name):
        self.name = str(name)

    def getInfo(self):
        return self.name


class Friend(Person):
    def __init__(self, name, phonenum, email):
        super().__init__(name)
        self.phonenum = phonenum
        self.email = email

    def getInfo(self):
        return (self.name, self.phonenum, self.email)
        # return super.getInfo, self.phonenum, self.email


friends = [
    Friend('둘리', '0101231234', 'dooly@naver.com'),
    Friend('또치', '0101112222', 'ttochi@naver.com'),
    Friend('고길동', '0101113333', 'gogildong@naver.com'),
    Friend('이수정', '0101114444', 'leesujung@naver.com'),
    Friend('마이콜', '0101115555', 'machele@naver.com')
]

# ojt = Friend('둘리', '0101231234', 'dooly@naver.com'),

# print(type(ojt))
# print(ojt[0])

print('{0:10}{1:12}{2:10}'.format('이름', '전화번호', '메일주소'))
print('-' * 50)
for obj in friends:
    name, phone, email = obj.getInfo()
    print(f"{name:<10s}{phone:<15s}{email:<10s}")
    print('{0:10}{1:15}{2:10}'.format(*obj.getInfo()))
#    print("{0:10s}{1:15s}{2:10s}".format(name, phone, email))

```

