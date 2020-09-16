

# Day1

> print, for문, input, time

### - 교육내용

```python
for y in range(1, 20) :
    for x in range(y) :
        print('@', end  = '')
    print()

    
for y in range(1, 50, 2) :
    print(' '* (50 - y- 1), end='')
    for x in range(y) :
        print('*', end = '')
    print()
    
time = 32140
hour = time // 3600

r_time = time - 3600 * hour
minute = r_time // 60

second = r_time - minute * 60


print (hour, '시간 ', minute, '분 ', second, '초', sep='')


input_char = input('문자 한 개를 입력하세요 : ')

print('\'', input_char,'\'', ' 문자의 코드값은 ', hex(ord(input_char)),'입니다.', sep='')


num1 = input('숫자1 입력: ')
num2 = input('숫자2 입력: ')

print (num1, ' + ', num2, ' = ',  int(num1) +  int(num2))
print (num1, ' * ', num2, ' = ',  int(num1) *  int(num2))
print (num1, ' ** ', num2, ' = ', int(num1) ** int(num2))


num = 20
su = 5

num += su
print (' ',num, '\n', end='-*-'*10)
num *= su
print ('\n', num, '\n', end='-*-'*10)
num -= su
print ('\n', num, '\n', end='-*-'*10)
num /= su
print ('\n', num, '\n', end='-*-'*10)

```



### - 실습

```python
[ 실습 1 ] 
>>> v1 = 100
>>> v2 = 50
>>> r1 = v1 + v2
>>> r2 = v1 - v2
>>> r3 = v1 * v2
>>> r4 = v1 / v2
>>> print ('r1',r1,sep=' = ')
r1 = 150
>>> print ('r2',r2,sep=' = ')
r2 = 50
>>> print ('r3',r3,sep=' = ')
r3 = 5000
>>> print ('r4',r4,sep=' = ')
r4 = 2.0

# for x in range(1,5,1) : print('r' , x ,' = ', r1)

[ 실습 2 ]
>>> name1 = '김'
>>> name2 = '유'
>>> name3 = '철'
>>> print (name1, name2, name3)
김 유 철
>>> print (name1, name2, name3, sep=':::')
김:::유:::철
>>> print (name1, name2, name3, sep='\n')
김
유
철

[ 실습 3 ]
>>> print('합은 ', 10 + 25 + 34, ' 이고 평균은 ', (10 + 25 + 34) / 3, ' 입니다.', sep= '')
합은 69 이고 평균은 23.0 입니다.
```

