

# Day1

> HTML 문법

### - 실습

```python
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>HTML학습</title>
</head>
<body>
<h1>주요 HTML 태그 학습</h1>
<hr>
<a href="http://java.sun.com/"><h1>ㅋㅋㅋ</h1></a>
<h2>ㅋㅋㅋ</h2>
<h3>ㅋㅋㅋ</h3>
<h4>ㅋㅋㅋ</h4>
<hr>
<a href="http://www.w3.org/">W3C</a><br>
<a href="http://www.w3schools.com/">W3Schools</a><br>
<a href="http://www.python.org/">PYTHON</a>
<hr>
<figure>
<a href="http://java.sun.com/">
    <img src="http://localhost:8000/edu/images/duke.png" width="100"></a>
<img src="/edu/images/sundie.png" width="200">
    <figcaption>듀크 이미지 모음</figcaption>
</figure>
<figure>
    <figcaption>카카오 이미지</figcaption>
<img src="../images/kakao/g1.png" width="300">
</figure>
<hr>
<form method="get" action="......">
    이름<input type="text" name="stname" required><br>
    암호<input type="password" name="stpwd" required><br>
    나이<input type="number" name="stnum"><br>
    칼라<input type="color" name="stcolor"><br>
    날짜<input type="date" name="stdate"><br>
    날짜와 시간<input type="datetime-local" name="stdatetime"><br>
    날짜<input type="date" name="stdate"><br>
    성별<input type='radio' name="gender" value="female">여성
    <input type='radio' name="gender" value="male">남성<br>
    취미<input type='checkbox' name ='hobby' value="등산">등산
    <input type='checkbox' name='hobby' value="수영">수영
    <input type='checkbox' name='hobby' value="골프">골프
    <input type='checkbox' name='hobby' value="여행">여행<br>
    <select name="year">
        <option value="2000">2001</option>
        <option value="2001">2002</option>
        <option value="2002">2003</option>
        <option value="2003">2004</option>
        <option value="2004">2005</option>
        <option value="2005">2006</option>
    </select>
    <br>
    남기고자 하는 글<br>
    <textarea rows="10" cols="100"></textarea>
    <br>
    <input type ="file" name="uploadfile">
    <input type="submit" value="보내기">
    <input type="reset" value="재작성하기">
</form>
<hr>
<h2>좋아하는 음식</h2>
<ol>
    <li>삼겹살</li>
    <li>떡볶이</li>
    <li>치킨</li>
</ol>
<h2>우리가 학습할 웹 클라이언트 기술</h2>
<ul>
    <li>CSS3</li>
    <li>JavaScript</li>
    <li>HTML5</li>
</ul>
<hr>
<table border="1" bgcolor="#00ff00">
    <tr><th>선택자</th><th>기능</th></tr>
    <tr><td>태그선택자</td><td><em>태그명</em>을 가지고 스타일을 적용할 대상을 찾는다.</td></tr>
    <tr><td>ID선택자</td><td>태그에 정의된 <em>Id속성</em>의 값을 가지고 스타일을 적용할 대상을 찾는다.</td></tr>
    <tr><td>CLASS선택자</td><td>태그에 정의된 <em>class속성</em>의 값을 가지고 스타일을 적용할 대상을 찾는다.</td></tr>
</table>
<hr>
오늘은<br><br><br><br>
즐거운<br>
금&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;요일<br>
100 & 100
!@#$%^&*()_+|"{}?><~
<hr>
<h2>우리가 학습할 <span style="color:blue">웹 클라이언트</span> 기술</h2>
<h2>우리가 학습할 <div style="color:blue">웹 클라이언트</div> 기술</h2>
<hr>
<video id="meda" width="720" height="400" controls>
    <source src="trailer.mp4">
    <source src="trailer.ogg">
</video>
</body>
</html>

<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8" name="viewport" content="width=device-width, initial-scale=1">
    <title>HTML5 학습</title>
    <link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons">  
<style>
   	* {
		margin : 0
	    }
    header {
	    height:150px;
        text-align:center;
		margin:auto;
		background-image : linear-gradient(to bottom right, violet, yellow);
        }
    h1 {
	    height:100px;
	    line-height:100px;
		text-shadow: 3px 3px 3px #ffffff
        }
    nav {
        height:50px;
	    line-height:50px;
        word-spacing:120px;
        }
	a {
	    text-decoration:none;
        color: #3333cc;
        display: inline-block;
        transition: 0.5s;
	    }
	a:hover {
        transform: scale(1.7,1.7);
	    }
    article {
		width : 80%;
		height : auto;
		margin-top : 5px;
		margin-bottom : 5px;
		margin-left : auto;
		margin-right : auto;
        border : 2px dotted red;
		border-radius:10px;
		padding-top : 10px;
		padding-bottom : 10px;
		padding-left : 10px;
        }
    table {
        width: 30%;
        border: 1px solid lime;
        border-collapse: collapse;
        }
    th {
		background-color : lime;
        border: 1px solid #000000;
        }
    td {
        text-align:center;
        border: 1px solid #000000;        
        }
    .trclass:hover {
		background-color : #eaebee;
	}
    img {
        width:85%;
        margin-top : 5px;
        }
	figure { text-align: center;
	    }
    aside {
    	width : 80%;
		height : auto;
		margin-top : 5px;
		margin-bottom : 5px;
		margin-left : auto;
		margin-right : auto;
        }
    video {
        margin-top : 5px;
        width:100%;
        }
	footer {
		width : 100%;
		height : 60px;
		background-color : #666666;
		text-align: center;
	    }
	h4 {
	    color:white;
        line-height:60px;
	    }
        .diviconh3 h3, .diviconh3 .material-icons {
            display:inline-block;
            vertical-align:middle;
            margin-bottom: 3px;
        }
</style>
</head>

<body>
<header>
    <h1 style="color:#cc3399">HTML5 학습</h1>
    <nav>
        <a href="http://www.w3.org/">W3C</a>
        <a href="http://www.w3schools.com/">W3Schools</a>
        <a href="https://jquery.com/">JQuery</a>
    </nav>
</header>
<section>
    <article>
        <div class="diviconh3">
            <i class="material-icons" style="color:#cc0099">attachment</i>
            <h3 style="color:#cc0099">나의 소개</h3>
        </div>
        <ul>
            <li>이름 : 김유철</li>
            <li>별명 : 곰</li>
            <li>관심기술 : 파이썬</li>
            <li>취미 : 술마시기</li>
        </ul>
    </article>
    <article>
        <div class="diviconh3">
            <i class="material-icons" style="color:#079e07">favorite</i>
            <h3 style="color:#079e07">올해 재미있게 읽은 책</h3>
        </div>
        <table border="1">
            <tr><th><span style="font-weight:bold">제목</span></th><th><span style="font-weight:bold">장르</span></th></tr>
            <tr class="trclass"><td>넛지</td><td>교양</td></tr>
            <tr class="trclass"><td>어떻게 살 것인가</td><td>교양</td></tr>
            <tr class="trclass"><td>스카이라인</td><td>SF</td></tr>
        </table>
    </article>
    <article>
        <div class="diviconh3">
            <i class="material-icons" style="color:#333399">computer</i>
            <h3 style="color:#333399" >자랑하고싶은 <span style="color:#cc0099">우리동네</span>의 아름다운 곳</h3>
        </div>
            <span>봉화산은 서울의 동북부 외곽인 중랑구 상봉동, 중화동, 묵동, 신내동에 접하여 있고 정상까지 높이는 160.1m 로 평지에 돌출되어 있는 독립구릉이다.
                동쪽에 아차산 주능선이 있는 것을 제외하고는 북쪽으로 불암산, 도봉산과 양주 일대까지 잘 조망 된다.</span>
        <div>
        <figure>
<!--        <img src="/edu/images/bong.jpg">-->
        <img src="./bong.jpg">
            <figcaption style="font-weight:bold">봉화산 봉화대 정상</figcaption>
        </figure>
        </div>
    </article>
</section>
<aside>
    <video controls>
        <source src="./bong_video.mp4">
    </video>
</aside>
<footer>
    <h4>이 문서는 김유철에 의해 윈도우 이미지 캡쳐와 유튜브 링크로 2020-07-27에 작성하였습니다. (Ver 1.0)</h4>
</footer>

</body>
</html>


```

