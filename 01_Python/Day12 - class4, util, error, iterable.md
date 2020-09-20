

# Day12

>  class4, util, error, iterable

### - 교육내용

```python
# 모듈을 가져옵니다.
import math
from MyError import NoNegativeNumberError

# 클래스를 선언합니다.
class Circle:
    def __init__(self, radius):
        if radius < 0 :
            raise NoNegativeNumberError("음의 값은 노노!!")
        self.__radius = radius
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
#print("원의 둘레:", circle.get_circumference())
#print("원의 넓이:", circle.get_area())
print()

# 간접적으로 radius에 접근합니다.
print("# radius에 접근합니다.")
#print(circle.get_radius())
print()

# 원의 둘레와 넓이를 구합니다.
circle.set_radius(2)
print("# 반지름을 변경하고 원의 둘레와 넓이를 구합니다.")
print("원의 둘레:", circle.get_circumference())
print("원의 넓이:", circle.get_area())

print("생각해 봅시다!!!")
#circle.set_radius(-3)
circle.radius = 4
print("# 반지름을 변경하고 원의 둘레와 넓이를 구합니다.")
print("원의 둘레:", circle.get_circumference())
print("원의 넓이:", circle.get_area())

#이렇게 넣으면 들어감
circle._Circle__radius = -3
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
    def get_radius(self):
        return self.__radius
    def set_radius(self, value):
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
print(circle.get_radius())
print()

# 원의 둘레와 넓이를 구합니다.
circle.set_radius(2)
print("# 반지름을 변경하고 원의 둘레와 넓이를 구합니다.")
print("원의 둘레:", circle.get_circumference())
print("원의 넓이:", circle.get_area())

print("생각해 봅시다!!!")
#circle.set_radius(-3)
circle.__radius = -3
print("# 반지름을 변경하고 원의 둘레와 넓이를 구합니다.")
print("원의 둘레:", circle.get_circumference())
print("원의 넓이:", circle.get_area())


class Car:
    @staticmethod
    def hello():
        print("오늘도 안전 운행 합시다.")
    count = 0
    def __init__(self, name):
        self.name = name
        Car.count += 1
    @classmethod
    def outcount(cls):
        print(cls.count)

Car.hello()
Car.outcount()
o1 = Car("프라이드")
o2 = Car("코란도")
Car.outcount()
print("-"* 10)
o1.hello()
o2.hello()
Car.hello()
o1.outcount()
o2.outcount()
Car.outcount()

class Human:
    def __init__(self, age, name):
        self.age = age
        self.name = name
    def __eq__(self, other):
        return self.age == other.age and self.name == other.name

kim = Human(29, "김상형")
sang = Human(29, "김상형")
moon = Human(44, "김상형")
print(kim == sang)
print(kim == moon)
print("-"*5+"추가"+"-"*5)
dooly = Human(44, "둘리")
print(moon == dooly)
dooly2 = Human(44, "둘리")
print(dooly == dooly2)
print(dooly is dooly2)

print(1 == 1)


class Human:
    def __init__(self, age, name):
        self.age = age
        self.name = name
    def __eq__(self, other):
        return self.name[0] == other.name[0]

dooly = Human(10, "김둘리")
ddochi = Human(20, "김또치")
douner = Human(30, "이도우너")
print(dooly == ddochi)
print(ddochi == douner)


class Student:
    def __init__(self, name, korean, math, english, science):
        self.name = name
        self.korean = korean
        self.math = math
        self.english = english
        self.science = science

    def get_sum(self):
        return self.korean + self.math +\
            self.english + self.science

    def get_average(self):
        return self.get_sum() / 4

    def __str__(self):
        return "{}\t{}\t{}".format(
            self.name,
            self.get_sum(),
            self.get_average())

    def __eq__(self, value):
        return self.get_sum() == value.get_sum()
    def __ne__(self, value):
        return self.get_sum() != value.get_sum()
    def __gt__(self, value):
        return self.get_sum() > value.get_sum()
    def __ge__(self, value):
        return self.get_sum() >= value.get_sum()
    def __lt__(self, value):
        return self.get_sum() < value.get_sum()
    def __le__(self, value):
        return self.get_sum() <= value.get_sum()

# 학생을 선언합니다.
student_a = Student("윤인성", 87, 98, 88, 95), Student("김유철", 87, 98, 88, 95)
student_b = Student("연하진", 92, 98, 96, 98),

# 출력합니다.
print("student_a == student_b = ", student_a == student_b)
print("student_a != student_b = ", student_a != student_b)
print("student_a >  student_b = ", student_a >  student_b)
print("student_a >= student_b = ", student_a >= student_b)
print("student_a <  student_b = ", student_a <  student_b)
print("student_a <= student_b = ", student_a <= student_b)

print(type(student_a))
print(student_a[0])
print(student_a[0].get_sum())


#print("student_a", student_a.get_sum())


class Human:
    def __init__(self, age, name):
        self.age = age
        self.name = name
#        print('A')
    def __str__(self):
        return "이름 %s, 나이 %d" % (self.name, self.age)
    def __len__(self):
        return self.age

kim = Human(29, "김상형")
print(kim)
print(len(kim))


import sys

print(sys.builtin_module_names)

import math
import time

print(dir(math))
print(dir(time))

import sys
sys.path.append("C:/PyStudy")

from mypack.calc import *
add.outadd(1,2)
multi.outmulti(1,2)


import sys
print(sys.path)

sys.path.append("C:/PyStudy")
print(sys.path)
import mypack.calc.add
mypack.calc.add.outadd(1,2)

import mypack.report.table
mypack.report.table.outreport()



INCH = 2.54

def calcsum(n):
    sum = 0
    for num in range(n + 1):
        sum += num
    return sum

INCH = 2.54

def calcsum(n):
    sum = 0
    for num in range(n + 1):
        sum += num
    return sum

print("인치 =", INCH)
print("합계 =", calcsum(10))

import util1

print("1inch =", util1.INCH)
print("~10 =", util1.calcsum(10))

import util2

print("1inch =", util2.INCH)
print("~10 =", util2.calcsum(10))


import time
import datetime
print(__name__ + ":" + str(datetime.datetime.now()))
print(__name__ + ":" + repr(datetime.datetime.now()))
time.sleep(5)
import B
time.sleep(5)
import C
time.sleep(5)
print(__name__ +":"+ str(datetime.datetime.now()))
print(__name__ +":"+ repr(datetime.datetime.now()))

import datetime
print(__name__ +" : "+ str(datetime.datetime.now()))



nums = [11, 22, 33]

for data in nums :
    print(data)

print("=" * 20)

it = iter(nums)
print(it)
while True:
    try:
        num = next(it)
    except StopIteration:
        break
    print(num)

print("=" * 20)

it2 = iter(nums)
print(next(it2))
print(next(it2))
print(next(it2))


class Alpha :
    def __init__(self, flag):
        self.flag = flag
        self.index = -1

    def __iter__(self):
        return self

    def __next__(self):
       self.index += 1
       if self.index > 25:
           raise StopIteration
       if self.flag :
           return chr(65 + self.index)
       else :
           return chr(97 + self.index)

# for data in Alpha(True) :
#     print(data)

# for data in Alpha(False) :
#     print(data)
#
print([ d for d in Alpha(1)])


class Seq:
    def __init__(self, data):
        self.data = data
        self.index = -2
    def __iter__(self):
        return self
    def __next__(self):
        self.index += 2
        if self.index >= len(self.data):
            raise StopIteration
        return self.data[self.index:self.index + 2]

solarterm = Seq("입춘우수경칩춘분청명곡우입하소만망종하지소서대서")
for k in solarterm:
    print(k, end = ',')


print(next(solarterm))

```



### - 실습

```python

```

