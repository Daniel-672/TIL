## - 모델에서 사진 저장 경로 바꾸기 (models.py)

```python
from django.db import models
import os
from uuid import uuid4
from django.utils import timezone

def date_upload_to(instance, filename):
  # upload_to="%Y/%m/%d" 처럼 날짜로 세분화
  #ymd_path = timezone.now().strftime('%Y/%m/%d')
  # 길이 32 인 uuid 값
  #uuid_name = uuid4().hex
  # 확장자 추출
  uuid_name = 'photo/'
  extension = os.path.splitext(filename)[-1].lower()
  # 결합 후 return
  return '/'.join([
    #ymd_path,
    uuid_name + instance.userEmail + extension,
  ])

class Users(models.Model):
    userEmail = models.EmailField(max_length=30, primary_key=True, verbose_name="이메일(아이디)")
    nickName = models.CharField(max_length=12, verbose_name="닉네임")
    password = models.CharField(max_length=12, verbose_name="비밀번호")
    registerDate = models.DateField(auto_now_add=True, verbose_name="가입시간")
#    photo = models.ImageField(blank=True, height_field=50, width_field=50, upload_to=date_upload_to)
    photo = models.FileField(blank=True, upload_to=date_upload_to)
    guardianName = models.CharField(blank=True, max_length=12, verbose_name="보호자명")
    guardianCallNum = models.CharField(blank=True, max_length=12, verbose_name="보호자전화번호")
    guardianBasicMsg = models.CharField(blank=True, max_length=100, verbose_name="보호자기본메세지")
    def __str__(self):
        return  f"[{self.__class__.__name__}] userEmail={self.userEmail}"
```





## - views.py에서 html로 데이터 전달하기

#### - 함수에서 context를 만들고 던지면

```python
def index(request) :
    context = None
    if 'user' in request.session:
        context = {'loginyn':True, 'nickname':'%s' % request.session['nickname']}
        # return redirect('onlymember')
        return render(request, 'index.html', context)
    else:
        context = {'loginyn': False}
        return render(request, 'index.html', context)
```

#### (2) html에서 받아서 사용

```html
{% if loginyn  %}
                <a class="navbar-brand js-scroll-trigger-left" href="{% url 'logout' %}">logout</a>
                {{nickname}}님 안녕하세요.
{% else %}
                <a class="navbar-brand js-scroll-trigger-left" href="{% url 'login' %}">login</a>
{% endif %}
```





## - 화면 특정 위치로 이동1 (redirect)

```html
<!-- HTML에 이동할 위치 잡아 주기 id값도 동작 -->
<a name="board"></a>
```

```python
# redirect의 경우 resolve_url을 이용해서 문자열을 맞추어 설정
# return redirect('board')
# return redirect('{}#move_{}'.format(resolve_url('board'), 'board'))
return redirect('{}#{}'.format(resolve_url('board'), 'board'))
```





## - 화면 특정 위치로 이동2 (render)

```javascript
<!-- render는 javascript로 처리 -->
{% block javascript %}
$(document).ready(function () {
$('html, body').animate({
scrollTop: $('#board').offset().top
}, 'slow');
});
```





## - SQLite에서 3개 테이블 PK - FK로 연결시 aggregate하기

``` python
#article - comment - comment2 (테이블 간 PK->FK구성 이건 키 기준으로 aggregate)
articles = Article.objects.annotate(cmtcnt=Count("comment__id", distinct=True) + Count("comment__comment2__id", distinct=True)).all()
```

``` python
#article - comment - comment2 (테이블 간 PK->FK구성 이건 스칼라 쿼리 결과값 한줄만)
article3 = Article.objects.filter(id=pk).aggregate(cmtcnt=Count("comment__id", distinct=True) + Count("comment__comment2__id", distinct=True))
```



## - SQLite DBshell

``` python
# SQL로 접속
(djangovenv) C:\Users\Daniel\fordisproject>python manage.py dbshell
# table 리스트, Drop, select 실행
.tables
#참고자료
#http://pythonstudy.xyz/python/article/309-DB-%EC%84%A4%EC%A0%95%EA%B3%BC-Migration
#https://wikidocs.net/9926 <- 전제적으로 잘 정리 됨
```

``` python
#article - comment - comment2 (테이블 간 PK->FK구성 이건 스칼라 쿼리 결과값 한줄만)
article3 = Article.objects.filter(id=pk).aggregate(cmtcnt=Count("comment__id", distinct=True) + Count("comment__comment2__id", distinct=True))
```

