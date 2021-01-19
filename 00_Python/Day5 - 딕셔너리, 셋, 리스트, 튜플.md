

# Day5

> 딕셔너리, 셋, 리스트, 튜플

### - 교육내용

```python
#dictionary
dic_v = { 'boy':'소년', 'school':'학교', 'book':'책' }
print(dic_v)

print(dic_v['boy'])
print(dic_v['book'])
#print(dic_v['student'])
print(dic_v.get('student'))
print(dic_v.get('student', '사전에 없는 단어'))

if 'student' in dic_v:
    print("사전에 있는 단어입니다.")
else:
    print("이 단어는 사전에 없습니다.")

dic_v['boy'] = '남자애'
dic_v['girl'] = '소녀'
del dic_v['book']
print(dic_v)

dic_v = { 'boy':'소년', 'school':'학교', 'book':'책' }
print(dic_v.keys())
print(dic_v.values())
print(dic_v.items())

keylist = dic_v.keys()
for key in keylist:
    print(key)

valuelist = dic_v.values()
for value in valuelist:
    print(value)

itemlist = dic_v.items()
for item in itemlist:
    print(item)

itemlist = dic_v.items()
for key,value in itemlist:
    print(key, value, sep="-")
    
maria = {'korean': 94, 'english': 91, 'mathematics': 89, 'science': 83}
print(maria)
average = sum(maria.values()) / len(maria)
print(average)


list1 = [ ['boy', '소년'], ['school', '학교'], ['book', '책'] ]
dic_v = dict(list1)
print(dic_v)

list2 = [ ('boy', '소년'), ('school', '학교'), ('book', '책') ]
dic_v = dict(list2)
print(dic_v)

list3 = dict(boy= '소년', school='학교', book='책')
dic_v = dict(list3)
print(dic_v)


x = {'a': 10, 'b': 20, 'c': 30, 'd': 40}
print(x)

item = x.items()
# for key, value in item:
#     if value == 20:
#         del x[key]

for key, value in list(item):
    if value == 20:
        del x[key]

print(x)


dictionary = {
    "name": "7D 건조 망고",
    "type": "당절임",
    "ingredient": ["망고", "설탕", "메타중아황산나트륨", "치자황색소"],
    "origin": "필리핀"
}

# 사용자로부터 입력을 받습니다.
key = input("> 접근하고자 하는 키: ")

# 출력합니다.
if key in dictionary:
    print(dictionary[key])
else:
    print("존재하지 않는 키에 접근하고 있습니다.")


score_of_class = {
    "class1": (77, 85, 67, 80, 90),
    "class2": (60, 80, 75, 98, 82),
    "class3": (72, 77, 65, 83, 95),
    "class4": (92, 70, 85, 67, 88)
}

print("class3 :", score_of_class["class3"])
for key, value in score_of_class.items() :
    print("[", key, "반]")
    print("총점 :", sum(value))
    print("최고점 :", max(value))
    print("최저점 :", min(value))

    
dictionary = {}

print("요소 추가 이전:", dictionary)

dictionary["name"] = "새로운 이름"
dictionary["head"] = "새로운 정신"
dictionary["body"] = "새로운 몸"

print("요소 추가 이후:", dictionary)

dictionary = {
    "name": "7D 건조 망고",
    "type": "당절임"
    }

print("요소 제거 이전:", dictionary)

del dictionary["name"]
del dictionary["type"]

print("요소 제거 이후:", dictionary)

terrestrial_planet = {
    'Mercury': {
        'mean_radius': 2439.7,
        'mass': 3.3022E+23,
        'orbital_period': 87.969
    },
    'Venus': {
        'mean_radius': 6051.8,
        'mass': 4.8676E+24,
        'orbital_period': 224.70069,
    },
    'Earth': {
        'mean_radius': 6371.0,
        'mass': 5.97219E+24,
        'orbital_period': 365.25641,
    },
    'Mars': {
        'mean_radius': 3389.5,
        'mass': 6.4185E+23,
        'orbital_period': 686.9600,
    }
}

print(terrestrial_planet['Venus']['mean_radius'])    # 6051.8


#keyword arguments
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
    print(kargs.keys())
    print(kargs.values())
    print(kargs.items())
    for key, value in kargs.items() :
        print(key, value, sep="->")

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

#list
# 인덱스로 리스트를 대입 할 경우 리스트 자체 가 추가됨 = append 메소드로 처리해도 됨
print("-- 리스트 뒤에 또 다른 리스트 데이터 확장 --")
list1 = [1, 2, 3, 4, 5]
list2 = [10, 11]
list1.append(list2)
print(list1)

print("-- 리스트 뒤에 또 다른 리스트 데이터 확장2 --")
list11 = [1, 2, 3, 4, 5]
list22 = [10, 11]
list11[4] = list22
print(list11)

print("-- 슬라이싱 --")
nums = [0,1,2,3,4,5,6,7,8,9]
print(nums[2:5])        # 2~5까지
print(nums[:4])         # 처음부터 4까지
print(nums[6:])         # 6에서 끝까지
print(nums[1:7:2])      # 1~7까지 하나씩 건너뛰며
print("-- 인덱스를 사용한 대입 --")
score = [ 88, 95, 70, 100, 99 ]
print(score[2])
score[2] = 55
print(score)
score[2] = [55, 66]
print(score)
print("-- 슬라이싱을 사용한 대입 --")
nums = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
print(nums)
nums[0:0] = [100]
print(nums)
nums[2:5] = [20, 30, 40]
print(nums)
nums[6:8] = [90, 91, 92, 93, 94]
print(nums)
print("-- 슬라이싱을 사용한 제거 --")
nums = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
print(nums)
nums[2:5] = []
print(nums)
del nums[4]
print(nums)
print("-- 리스트 연산 --")
list1 = [1, 2, 3, 4, 5]
list2 = [10, 11]
listadd = list1 + list2
print(listadd)
listmulti = list2 * 3
print(listmulti)

print("-- 중첩 리스트1 --")
lol = [ [1, 2, 3], [4, 5], [6, 7, 8, 9]]
print("이차원 리스트 인덱싱[행][열]")
print(lol[0])
print(type(lol[0]))
print(lol[2][1])
print(type(lol[2][1]))
print("이차원 리스트의 행 갯수와 각 행마다의 열 갯수")
print(len(lol))
print(len(lol[0]))
print(len(lol[1]))
print(len(lol[2]))
print("for문을 이용한 이차원 리스트 데이터 추출")
for sub in lol:
    for item in sub:
        print(item, end=' ')
    print()

print("-- 중첩 리스트2 --")
score = [
    [88, 76, 92, 98],
    [65, 70, 58, 82],
    [82, 80, 78, 88]
    ]

total = 0
totalsub = 0
for student in score:
    sum = 0
    for subject in student:
        sum += subject
    subjects = len(student)
    print("총점 :", sum, "평균 :", sum / subjects)
    total += sum
    totalsub += subjects
print("전체평균 :", total / totalsub)

print("-- 리스트에 데이터 추가 --")
nums = [1, 2, 3, 4]
print(nums)
nums.append(5)
print(nums)
nums.insert(2, 99)
print(nums)

print("-- 리스트에 범위를 지정하여 데이터 추가 --")
nums = [1, 2, 3, 4]
print(nums)
nums[2:2] = [90, 91, 92]
print(nums)

nums = [1, 2, 3, 4]
nums[2] = [90, 91, 92]
print(nums)

print("-- 리스트 뒤에 또 다른 리스트 데이터 확장 --")
list1 = [1, 2, 3, 4, 5]
list2 = [10, 11]
list1.extend(list2)
print(list1)

print("-- 리스트 뒤에 또 다른 리스트 데이터 확장2 --")
list11 = [1, 2, 3, 4, 5]
list22 = [10, 11]
list11[5:0] = list22
print(list11)


print("-- 리스트의 데이터를 삭제하는 다양한 방법 --")
score = [ 88, 95, 70, 100, 99, 80, 78, 50 ]
score.remove(100)
print(score)
del score[2]
print(score)
score[1:4] = []
print(score)

print("-- pop() 메서드로 ㄹ스트 데이터 지우고 꺼내기 --")
score = [ 88, 95, 70, 100, 99 ]
print(score.pop())
print(score.pop())
print(score.pop(1))
print(score)

print("-- 리스트에서 데이터 위치(인덱스) 찾기와 갯수 카운팅 --")
score = [ 88, 95, 70, 100, 99, 80, 78, 50 ]
perfect = score.index(100) + 1
print("만점 받은 학생은 " + str(perfect) + "번입니다.")
pernum = score.count(100)
print("만점자 수는 " + str(pernum) + "명입니다")

print("-- in 연산자를 사용하여 리스트에 데이터 존재여부 채크 --")
ans = input("결제 하시겠습니까? ")
if ans in ['yes', 'y', 'ok', '예', '당근']:
    print("구입해 주셔서 감사합니다.")
else:
    print("안녕히 가세요.")

surname = ['김', '이', '박', '최', '강', '윤', '장', '임', '오']
import random
for x in range(20):
    print(random.choice(surname) + '서방')
    
#set
a = set()
b = set([1, 2, 3, 3,4])
c = {1, 4, 5, 6, 1, 4}
d = set([1, 2, 'Pen', 'Cap', 'Plate'])
e = set((10,))
f = {100,}
print('a - ', type(a), a)
print('b - ', type(b), b)
print('c - ', type(c), c)
print('d - ', type(d), d)
print('e - ', type(e), e)
print('f - ', type(f), f)
# for 문으로 데이터 추출
for data in d :
    print(data)

# 튜플 로 변환
t = tuple(b)
print('tuple - ', type(t), t)
print('tuple - ', t[0], t[1:3])

# 리스트로 변환
l = list(c)
print('list - ', type(l), l)
print('list - ', l[0], l[1:3])

print("----set 의 집합 연산----")
s1 = set([1, 2, 3, 4, 5, 6])
s2 = set([4, 5, 6, 7, 8, 9])
print(s1, s2)
print('intersect - ', s1 & s2)
print('union - ', s1 | s2)
print('difference - ', s1 - s2)
print('exclusive - ', s1 ^ s2)

print("----추가 & 제거 & 갯수 채크----")
s1 = set()
s1.add(10);s1.add(20);s1.add(30);s1.add(40);s1.add(50)
print('s1(10,20,30,40,50추가) - ', s1)
s1.add(10)
print('s1(10추가실패) - ', s1)
s1.update([40,50,60,70])
print('s1(40,50,60,70변경) - ', s1)
s1.remove(30)
print('s1(30삭제) - ', s1)
print('length - ', len(s1))

mammal = { '코끼리', '고릴라', '사자', '고래', '사람', '원숭이', '개' }
primate = { '사람', '원숭이', '고릴라' }

if '사자' in mammal:
    print("사자는 포유류이다")
else:
    print("사자는 포유류가 아니다.")

print(primate <= mammal)
print(primate < mammal)
print(primate <= primate)
print(primate < primate)

print(type(mammal))

#tuple
# 튜플 자료형(순서O, 중복O, 수정X,삭제X)
# 선언
a = ()
b = (1,)
c = (1, 2, 3, 4)
d = (10, 100, 'Pen', 'Cap', 'Plate')
print('d - ', type(d), d)

# 인덱싱
print('d - ', d[1])
print('d - ', d[0] + d[1] + d[1])
print('d - ', d[-1])

# 슬라이싱
print('d - ', d[0:3])
print('d - ', d[2:])

# 튜플 연산
print('c + d - ', c + d)
print('c * 3 - ', c * 3)
print("'hi' + c[0] - ", 'hi' + str(c[0]))

# 튜플 함수
a = (5, 2, 3, 1, 4)

print('a - ', a)
print('a - ', a.index(5))
print('a - ', a.count(4))

# 괄호가 없는 튜플
tuple_test = 10, 20, 30, 40
print("# 괄호가 없는 튜플의 값과 자료형 출력")
print("tuple_test:", tuple_test)
print("type(tuple_test):", type(tuple_test))
print()

# 괄호가 없는 튜플 활용
a, b, c = 10, 20, 30
print("# 괄호가 없는 튜플을 활용한 할당")
print("a:", a)
print("b:", b)
print("c:", c)

a, b = 10, 20

print("# 교환 전 값")
print("a:", a)
print("b:", b)
print()

# 값을 교환합니다.
a, b = b, a

print("# 교환 후 값")
print("a:", a)
print("b:", b)
print()

import time
def gettime():
    now = time.localtime()
    print(now, type(now))
    return now.tm_hour, now.tm_min

result = gettime()
print("지금은 %d시 %d분입니다" % (result[0], result[1]))

# =============== divmod  ===============
d, m = divmod(7, 3)
print("몫", d)
print("나머지", m)
```



### - 실습

```python
colorDic={
  'red':'#FF0000',
  'blue':'#0000FF',
  'green':'#008000',
  'yellow':'#FFFF00',
  'orange':'#FFA500',
  'black':'#000000',
  'white':'#FFFFFF',
  'violet':'#EE82EE',
  'pink':'#FFC0CB',
  'lime':'#00FF00'
}

choiceColor = input('칼라명을 영문으로 입력하세요 : ')

if choiceColor in colorDic:
    print(choiceColor, '칼라의 RGB 값은', colorDic[choiceColor],'입니다.')
else:
    print(choiceColor, '칼라의 RGB 값을 찾을 수 없습니다.')

    
weatherDic={
           '월':(22, 25),
           '화':(22, 31),
           '수':(22, 32),
           '목':(21, 24),
           '금':(21, 26),
           '토':(21, 28),
           '일':(21, 28)
}

weekDay = input('요일명을 한글로 입력하세요. : ')

if weekDay in weatherDic:
    lowTemp, highTemp = weatherDic[weekDay]
    print(weekDay, '요일의 최저온도는 ', lowTemp, ' 이고 최고온도는 ', highTemp,'입니다.', sep='')
else:
    print(weekDay, '요일의 정보를 찾을 수 없습니다.')


    
teamMember={
'김민영' : ('26', '통계학', '강동구', 'sgm02101@hanmail.net', '드라이브'),
'김유철' : ('47', '컴공',  '중랑구', 'kim672772@hotmail.com', '술'),
'박주희' : ('28', '경영정보', '관악구', 'jhpark3816@naver.com', '영화보기'),
'이동화' : ('28', '경제학', '구리시', 'donghwa3908@gmail.com', '야구직관')
}

for name, info in teamMember.items():
    print('=' * 5, name, '=' * 5)
    print('* 나이 :', info[0])
    print('* 전공 :', info[1])
    print('* 동네 :', info[2])
    print('* 메일 :', info[3])
    print('* 취미 :', info[4])
    print('')
    a, b, c, d, e = info
    print(a)
    print(b)

#print(teamMember['김유철'][0][0])


import random

lotto = set()
chrTemp = ''

while len(lotto) != 6:
    lotto.add(random.randint(1, 45))

print('행운의 로또번호 : ', end='')
for lottoNum in lotto:
   chrTemp += str(lottoNum) + ', '

print(chrTemp[0:-2])

import random

set1 = set()
set2 = set()

while len(set1) != 10:
    set1.add(random.randint(1, 20))

while len(set2) != 10:
    set2.add(random.randint(1, 20))


print('집합 1 :', set1)
print('집합 2 :', set2)
print('두 집합에 모두 있는 데이터 :', set1 & set2)
print('집합1 또는 집합2에 있는 데이터 :', set1 | set2)
print('집합1에는 있고 집합2에는 없는 데이터 :', (set1 - set2))
print('집합2에는 있고 집합1에는 없는 데이터 :', (set2 - set1))
print('집합1과 집합2가 각자 가지고 있는 데이터 :', (set1 | set2) - (set1 & set2))
print('집합1과 집합2가 각자 가지고 있는 데이터 :', (set1 ^ set2))


import random

lotto = []
#cnt = 0
chrTemp = ''

#while cnt != 6:
while len(lotto) != 6:

    lottoNum = random.randint(1, 45)

    if lottoNum not in lotto:
#       cnt += 1
       lotto.append(lottoNum)

print('행운의 로또번호 : ', end='')
for lottoNum in lotto:
   chrTemp += str(lottoNum) + ', '

print(chrTemp[0:-2])


pop = [
      [10, 12, 14, 16],
      [18, 20, 22, 24],
      [26, 28, 30, 32],
      [34, 36, 38, 40]
      ]

print('1행 1열의 데이터 :', pop[0][0])
print('3행 4열의 데이터 :', pop[2][3])
print('행의 갯수 :', len(pop))
print('열의 갯수 :', len(pop[0]))
print('3행의 데이터들 : ', end='')
for atom in pop[2]:
    print(atom, end=' ')
print('')
print('2열의 데이터들 : ', end='')
for row in range(0,len(pop)):
    print(pop[row][1], end=' ')
print('')
print('왼쪽 대각선 데이터들 : ', end='')
for rowcol in range(0,len(pop)):
    print(pop[rowcol][rowcol], end=' ')
print('')
print('오른쪽 대각선 데이터들 : ', end='')
for rowcol in range(0,len(pop)):
    print(pop[rowcol][(len(pop) - 1) - rowcol], end=' ')
print('')


pop = [
      [10, 20, 30, 40, 50],
      [ 5, 10, 15],
      [11, 22, 33, 44],
      [ 9,  8,  7, 6, 5, 4, 3, 2, 13]
	  ]
rowCount = 1

for rowSet in pop:
    print(rowCount, '행의 합은 ', sum(rowSet), ' 입니다.', sep='')
    rowCount += 1


    
pop = [
      ['B', 'C', 'A', 'A'],
      ['C', 'C', 'B', 'B'],
      ['D', 'A', 'A', 'D'],
]


alphCount = []
charCount = 0

for alph in range(65,69):
    charCount = 0
    for row in range(0, len(pop)):
        charCount += pop[row].count(chr(alph))

    alphCount.append((chr(alph), charCount))

for char, cnt in alphCount:
    print(char, ' 는 ', cnt, '개 입니다.', sep='')
```

