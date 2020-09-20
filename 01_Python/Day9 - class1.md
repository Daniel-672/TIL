

# Day9

> class

### - 교육내용

```python
class Student :
    pass

st1 = Student()
st2 = Student()
st3 = Student()

print(type(st1), id(st1))
print(type(st2), id(st2))
print(type(st3), id(st3))

class Student :
   def __init__(self):
       print("인스턴스 생성!!")

   def __del__(self):
       print("인스턴스 삭제!!")

st1 = Student()
st2 = Student()
st3 = Student()

print(type(st1), id(st1))
print(type(st2), id(st2))
print(type(st3), id(st3))

# del st1

class Student :
   '''
   학생 객체를 생성할 수 있는 Student 클래스입니다.
   인스턴스 생성시에는 학생의 이름, 나이, 과목명을 전달하세요.
   '''
   def __init__(self, name, age, subject):
       self.name = name
       self.age = age
       self.subject = subject

   def printStudentInfo(self):
       print("{}의 나이는 {}세입니다.".format(self.name, self.age))

   def study(self):
       print("{} 학생은 {}과목을 학습합니다.".format(self.name, self.subject))


st1 = Student("둘리", 10, "파이썬")
st2 = Student("도우너", 12, "자바")
st3 = Student("또치", 10, "자바스크립트")

st1.printStudentInfo()
st2.printStudentInfo()
st3.printStudentInfo()

st1.study()
st2.study()
st3.study()

print("\n[ st2=st1 과 st3=st1 연산 수행 ]")
st2 = st1
st3 = st1

st1.printStudentInfo()
st2.printStudentInfo()
st3.printStudentInfo()

help(Student)
```



### - 실습

```python

```

