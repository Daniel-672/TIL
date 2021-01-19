

# Day4

> pack_unpack, 인자, 시퀀스, 리스트

### - 교육내용

```python
s = "ABC"
l = [10,20,30]
t = (10, 20, 30)

print("---문자열 패킹과 언패킹---")
v1, v2, v3 = s
print(v1);print(v2);print(v3)
s2 = "aa" "bb" "cc"
print(s2)

print("---리스트 언패킹---")
v1, v2, v3 = l
print(v1);print(v2);print(v3)

print("---튜플 패킹과 언패킹---")
v1, v2, v3 = t
print(v1);print(v2);print(v3)
t2 = "aa","bb","cc"
print(type(t2))
print(t2)
t3 = v1, v2, v3
print(t3)
t4 = 10, 20, 30
print(t4)
t5 = 100,
print(t5)
t6 = (100,)
print(t6)

s = "ABC"
l = [10,20,30]
t = (10, 20, 30)

def unpackf(p1, p2, p3) :
    print("p1=", p1," p2=", p2," p3=", p3, sep="")

#unpackf(s)
unpackf(*s)
unpackf(*l)
unpackf(*t)

print("---여러 아규먼트들을 패킹하여 받는 매개변수(가변형 인자)---")
def packf(*p) :
    for data in p :
        print(data)

packf(10, 20, "abc", True)



print("---가변형 인자 함수 정의---")
def sumall(*p) :
    """ 아규먼트로 전달되는 모든 숫자들의 합을 리턴"""
    sum = 0
    for data in p :
        sum += data
    return sum

print(sumall(1,2,3,4,5))
print(sumall(100, 200, 300))
print(sumall(10,20,30,40,50,60,70))

help(sumall)


def printdeco(*p, deco="@") :
    for data in p :
        print(deco, data, deco)
    print()

printdeco(1,2,3,4,5)
printdeco("가", "나")
printdeco(True, "A", 10, deco="$")



def getlist1(times, *nums) :
    newnums = []
    for data in nums :
        newnums.append(data * times)
    return newnums

print(getlist1(2, 1,2,3,4,5))
print(getlist1(3, 1,2,3,4,5,6,7))


def getlist2(times, *nums) :
    newnums = list()
    for data in nums :
        newnums.append(data * times)
    return newnums

print(getlist2(2, 1,2,3,4,5))
print(getlist2(3, 1,2,3,4,5,6,7))



def updatelist(times, listnums) :
    for i in range(len(listnums)) :
        listnums[i] *= times


l1 = [1,2,3,4,5]
print(l1)
updatelist(2, l1)
print(l1)
print("-"*10)
l2 =  [10, 20, 30, 40];
print(l2)
updatelist(3, l2)
print(l2)




s1 = "abcdefgh1abcaa234가나다"
print(s1)
print("---in과 not in 연산자---")
print('a' in s1)
print('a' not in s1)
print('가나' in s1)
print('가다' not in s1)
print("---시퀀스연산---")
s2 = "파이썬"
print(s1+s2)
print(s1)
print(s2)
print(s2 * 3)
print("---인텍싱과 슬라이싱---")
print(s2[0]); print(s2[1]); print(s2[2]); print(s2[-1])
print(s1[:])
print(s1[::1])
print(s1[::2])
print(s1[::-1])
print(s1[0:4:1])
print("---함수들---")
print(len(s1))
print(max(s1)); print(min(s1))
print(s1.count('a'))
print(s1.count('abc'))
print("---for와 함께 사용하는 시퀀스---")
for data in s2 :
    print("#", data, "#")
print("---문자열은 변경불가---")
s2[0] = "가"


list1 = [10, 20, 30, "가나다", "abc", "A", True, 10, 20, 10, [11, 22]]
print(list1)
print("---in과 not in 연산자---")
print('30' in list1)
print(30 not in list1)
print(True in list1)
print(False not in list1)
print("---시퀀스연산---")
list2 = ["파","이","썬"]
print(list1+list2)
print(list1)
print(list2)
print(list2 * 3)
print("---인텍싱과 슬라이싱---")
print(list2[0]); print(list2[1]); print(list2[2]); print(list2[-1])
print(list1[:])
print(list1[::1])
print(list1[::2])
print(list1[::-1])
print(list1[0:4:1])
print("---함수들---")
print(len(list1))
#print(max(list1)); print(min(list1))
print(max([10,20, 30])); print(min([10, 20,30]))
print(max(['a', 'b', 'c'])); print(min(['a', 'b', 'c']))
print(max([True, False])); print(min([True, False]))
print(list1.count(10))
print(list1.count(20))
print("---for와 함께 사용하는 시퀀스---")
for data in list2 :
    print("#", data, "#")
print("---리스트는 변경가능---")
list2[0] = "가"
print(list2)
list2[0:1] = "파"
print(list2)
list2[0:0] = "가"
print(list2)
list2[0:2] = "나"
print(list2)

list2[0:2] = [10, 20, 30, 40, 50, 60, 70]
print(list2)
list2[0] = [10, 20, 30, 40, 50, 60, 70]   #append
print(list2)
list2[0:1] = [10, 20, 30, 40, 50, 60, 70]  #extend
print(list2)
del list2[0]
print(list2)
del list2[0:3]
print(list2)
r1 = list2.remove("썬")
print(list2)
print(r1)
#list2.remove("썬")
#print(list2)
r2 = list2.pop()
print(list2)
print(r2)
list2.append("가")
print(list2)
list2.insert(1,"나")
print(list2)
list2.append([1,2,3])
print(list2)
list2.extend([1,2,3,4,5])
print(list2)


t1 = (10, 20, 30, "가나다", "abc", "A", True, 10, 20, 10, [11, 12])
print(t1)
print("---in과 not in 연산자---")
print('30' in t1)
print(30 not in t1)
print(True in t1)
print(False not in t1)
print("---시퀀스연산---")
t2 = ("파","이","썬")
print(t1+t2)
print(t1)
print(t2)
print(t2 * 3)
print("---인텍싱과 슬라이싱---")
print(t2[0]); print(t2[1]); print(t2[2]); print(t2[-1])
print(t1[:])
print(t1[::1])
print(t1[::2])
print(t1[::-1])
print(t1[0:4:1])
print("---함수들---")
print(len(t1))
#print(max(t1)); print(min(t1))
print(max((10,20, 30))); print(min((10, 20,30)))
print(max(('a', 'b', 'c'))); print(min(('a', 'b', 'c')))
print(max((True, False))); print(min((True, False)))
print(t1.count(10))
print(t1.count(20))
print("---for와 함께 사용하는 시퀀스---")
for data in t2 :
    print("#", data, "#")
print("---튜플은 변경불가---")
t2[0] = "가"
print(t2)


# 리스트, 튜플
# 리스트 자료형(순서O, 중복O, 수정O, 삭제O)
a = []
b = list()
c = [1, 2, 3, 4]
d = [10, 100, 'Pen', 'Cap', 'Plate']
e = list('유니코')

print("리스트데이터의 타입")
print(type(d), d, sep="--->")

print(a)
print(b)
print(c)
print(d)
print(e)

print("리스트데이터의 길이")
print(len(a))
print(len(d))

print("리스트데이터의 인덱싱")
print('d - ', d[1])
print('d - ', d[0] + d[1] + d[1])
print('d - ', d[-1])

# 슬라이싱
print('d - ', d[0:3])
print('d - ', d[2:])



```



### - 실습

```python
def print_triangle_withdeco(line, deco="%"):
    if line < 1 or line > 10:
        pass
    else:
        for cnt in range(1, line+1):
            print(' ' * (line - cnt), deco * cnt )


print_triangle_withdeco(9)
print_triangle_withdeco(8, "#")

def sumEven1(*args):
    sum = 0
    value_flag = 0
#    print(args.count)
    if len(args) == 0:
        return -1
    else:
        for data in args :
            if int(data) % 2 == 0:
                value_flag = 1
                sum += int(data)

        if value_flag == 0:
           return 0
        else:
            return sum

#짝수가 없다
print(sumEven1(1, 3, 5, 7, 9))

#아규먼트가 없다
print(sumEven1())

#정상적
print(sumEven1(1, 2, 3, 4, 5))


def sumAll(*args):
    sum = 0
    value_flag = 0
    if len(args) == 0:
        return None
    else:
        for data in args:
            if type(data) == int:
                value_flag = 1
                sum += int(data)

        if value_flag == 0:
            return None
        else:
            return sum

# 숫자가 없다
print(sumAll('A', '가', [4], ('A',)))

# 아규먼트가 없다
print(sumAll())

# 정상적
print(sumAll(1, 2, 3, 4, 5, 'A', '가', [4], ('A',)))


listnum = [10, 5, 7, 21, 4, 8, 18]

big_value = listnum[0]

for cnt in range(1, len(listnum)):
    if big_value < listnum[cnt]:
        big_value = listnum[cnt]

print("최대값 :" , big_value)

print("최대값 :" , max(listnum))

listnum = [10, 5, 7, 21, 4, 8, 18]

small_value = listnum[0]

for cnt in range(1, len(listnum)):
    if small_value > listnum[cnt]:
        small_value = listnum[cnt]

print("최솟값 :" , small_value)

print("최솟값 :", min(listnum))


listnum = [10, 5, 7, 21, 4, 8, 18]

small_value = listnum[0]
big_value = listnum[0]

for cnt in range(1, len(listnum)):
    if big_value < listnum[cnt]:
        big_value = listnum[cnt]
    if small_value > listnum[cnt]:
        small_value = listnum[cnt]

print("최솟값 : ", min(listnum), ", 최대값 : ", max(listnum), sep="")
print("최솟값 : ", small_value, ", 최대값 : ", big_value, sep="")



import random
listnum = []

print("랜덤으로 10개 넣기")
for cnt in range(0, 10):
    listnum.append(random.randint(1, 50))

print("모두출력")
print(listnum)

print("10보다 작으면 100으로 변경")
for cnt in range(0, 10):
    if listnum[cnt] < 10:
        listnum[cnt] = 100

print("모두출력")
print(listnum)

print("첫번째 데이터")
print(listnum[0])

print("마지막 데이터")
print(listnum[-1])

print("슬라이싱 방법으로 listnum의  두 번째 데이터부터 여섯 번째 데이터만 추출")
print(listnum[1:6])

print("슬라이싱 방법으로 listnum의 데이터를 역순으로 출력")
print(listnum[::-1])

print("슬라이싱 방법으로 listnum의 데이터를 모두 출력")
print(listnum[:])

print("인덱싱 방법으로 5번째 데이터를 삭제")
del listnum[4]

print("슬라이싱 방법으로 listnum의 데이터를 모두 출력")
print(listnum[:])

print("슬라이싱 방법으로 2~3번째 데이터를 삭제")
del listnum[1:3]

print("슬라이싱 방법으로 listnum의 데이터를 모두 출력")
print(listnum[:])

```

