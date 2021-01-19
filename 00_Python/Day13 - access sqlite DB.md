

# Day13

>  access DB (sqlite)

### - 교육내용

```python
import sqlite3

con = sqlite3.connect('addr.db')
cursor = con.cursor()

cursor.execute("DROP TABLE IF EXISTS tblAddr")
cursor.execute("""CREATE TABLE tblAddr
    (name CHAR(16) PRIMARY KEY, phone CHAR(16), addr TEXT)""")

cursor.execute("INSERT INTO tblAddr VALUES ('김상형', '123-4567', '오산')")
cursor.execute("INSERT INTO tblAddr VALUES ('한경은', '555-1004', '수원')")
cursor.execute("INSERT INTO tblAddr VALUES ('한주완', '444-1092', '대전')")

con.commit()

cursor.close()
con.close()


import sqlite3

con = sqlite3.connect('addr.db')
cursor = con.cursor()

cursor.execute("SELECT * FROM tblAddr")
table = cursor.fetchall()
for record in table:
    print("이름 : %s, 전화 : %s, 주소 : %s" % record)

cursor.close()
con.close()


import sqlite3

con = sqlite3.connect('addr.db')
cursor = con.cursor()

cursor.execute("DELETE FROM tblAddr WHERE name = '김상형'")
con.commit()

cursor.close()
con.close()



import sqlite3

con = sqlite3.connect('addr.db')
cursor = con.cursor()

cursor.execute("SELECT * FROM tblAddr")
while True:
    record = cursor.fetchone()
    if record == None:
        break
    print("이름 : %s, 전화 : %s, 주소 : %s" % record)

cursor.close()
con.close()

import sqlite3

con = sqlite3.connect('addr.db')
cursor = con.cursor()

cursor.execute("SELECT addr FROM tblAddr WHERE name = '김상형'")
record = cursor.fetchone()
print("김상형은 %s에 살고 있습니다." % record)

cursor.close()
con.close()


import sqlite3

con = sqlite3.connect('addr.db')
cursor = con.cursor()

cursor.execute("SELECT * FROM tblAddr ORDER BY addr")
table = cursor.fetchall()
for record in table:
    print("이름 : %s, 전화 : %s, 주소 : %s" % record)

cursor.close()
con.close()


import sqlite3

con = sqlite3.connect('addr.db')
cursor = con.cursor()

cursor.execute("DELETE FROM tblAddr WHERE name = '김상형'")
con.commit()

cursor.close()
con.close()


import sqlite3

con = sqlite3.connect('addr.db')
cursor = con.cursor()

cursor.execute("UPDATE tblAddr SET addr = '제주도' WHERE name = '김상형'")
con.commit()

cursor.close()
con.close()

import urllib.request
print(urllib.request.urlopen("http://www.example.com").read().decode('utf-8'))
```



### - 실습

```python

```

