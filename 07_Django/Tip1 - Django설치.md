## - DJANGO설치 및 실행

### 1. 가상환경 만들기

```python
c:\python_venv>python -m venv djangovenv
```

### 2. 가상환경 활성

```py
c:\python_venv\djangovenv\Script>activate
```

### 3. 장고설치 (pip버전 해결은 가상환경에서 upgrade)

```python
(djangovenv) C:\python_venv\djangovenv\Script>pip install django 
```

```python
(djangovenv) C:\python_venv\djangovenv\scripts\python.exe -m pip install --upgrade pip
```

### 4. 장고프로젝트 만들기 (원하는 위치로 이동)

```python
(djangovenv) C:\DJANGOexam>django-admin startproject studyproject1
```

### 5. 서버실행 (외부접속시 IP 및 port지정)

```py
(djangovenv) C:\DJANGOexam\studyproject1>python manage.py runserver
```

```python
(djangovenv) C:\DJANGOexam\studyproject1>python manage.py runserver 192.168.0.25:8000
```

### 6. 프로젝트내 app생성

``` python
(djangovenv) C:\DJANGOexam\studyproject1>python manage.py startapp firstapp
```





## - 프로젝트 초기 설정의 예

### 1. 언어 및 timezone 설정(settings.py)

``` python
import os

LANGUAGE_CODE = 'ko-kr'

TIME_ZONE = 'Asia/Seoul'

INSTALLED_APPS = [
    'bbsapp',
```

### 2. mainproject 와 bbsapp에 templates폴더 추가 (settings.py)

```python
import os

TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [os.path.join(BASE_DIR, 'bbsproject', 'templates')],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
```

### 3. 이미지 static 및 session설정 (settings.py)

```python
STATIC_URL = '/static/'

SESSION_EXPIRE_AT_BROWSER_CLOSE = True
SESSION_SAVE_EVERY_REQUEST = True
```



### 4. models.py에 객체 생성 (models.py)

``` python
from django.db import models

class News(models.Model) :
    writer = models.CharField(max_length=6)
    title = models.CharField(max_length=40)
    content = models.TextField()
    cnt = models.IntegerField()
    writedate = models.DateTimeField(auto_now_add=True)
```

### 5. model migration

```python
python manage.py makemigrations bbsapp

python manage.py migrate
```

### 6. urls패턴 추가 (urls.py)

``` python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('bbsapp/', include('bbsapp.urls')),
]

from django.urls import path
from . import views

urlpatterns = [
    path("insert/", views.insert, name="insert"),
    path("delete/", views.delete, name="delete"),
    path("update/", views.update, name="update"),
    path("listAll/", views.listAll, name="listAll"),
    path("listOne/", views.listOne, name="listOne"),
]
```
