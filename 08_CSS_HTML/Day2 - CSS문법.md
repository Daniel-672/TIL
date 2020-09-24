

# Day2

> CSS 문법

### - 교육내용

```html
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<h1>CSS로 무었을 할 수 있을까?</h1>
<hr>
<h2 style="color:green">둘리</h2>
<h2 style="color:red">또치</h2>
<h2>도우너</h2>
<h2>희동이</h2>
<h2>마이콜</h2>
<h2 style="color:#0000ff;background-color:yellow">고길동</h2>
</body>
</html>

<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<h1>CSS로 무었을 할 수 있을까?</h1>
<hr>
<h2>둘리</h2>
<h2>또치</h2>
<h2>도우너</h2>
<h2>희동이</h2>
<h2>마이콜</h2>
<h2>고길동</h2>
</body>
</html>


<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
<style>
    #t2 {
        width: 140px;
        height: 100px;
        background: orange;
        position: relative;
        animation: t1move 5s infinite;
    }

    @keyframes t1move {
        from {top: 0px;}
        to {top: 700px;}
    }

    div {
        background-color:lime;
        margin:5px;
        width:300px;
        height:200px;
        font-size:1.5em;
        padding:10px;
    }

    span {
        background-color:orange;
        margin:5px
        width:300px;
        height:200px;
        font-size:1.5em;
        padding:10px;
    }

    .top {
        color:#808080;
    }

</style>
</head>
<body>
<h1><span class="top">블럭</span> 스타일 태그와 <span class="top">인라인</span> 스타일 태그</h1>
<hr>
<div id="t1">가나다라마바사아</div>
<div>1234356789</div>
<div>abcdefghij</div>
<hr>
<span id="t2">가나다라마바사아</span>
<span>1234356789</span>
<span>abcdefghij</span>
</body>
</html>


<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
<style>
    #t2 {
        width: 140px;
        height: 100px;
        background: orange;
        position: relative;
        animation: t1move 5s infinite;
    }

    @keyframes t1move {
        from {top: 0px;}
        to {top: 700px;}
    }

    div {
        background-color:lime;
        margin:5px;
        width:300px;
        height:200px;
        font-size:1.5em;
        padding:10px;
        text-align:center;
        margin-left:auto;
        margin-right:auto;
        border-radius:20px
    }

    .top {
        color:#ff8080;
    }
    h1 {
        text-align:center;
        text-shadow:-5px -7px 5px gold, -4px -6px 4px red, -3px -5px 3px black;
    }
    h1:hover {
        transform:rotate(4deg);

        transition:transform 2s;
    }
</style>
</head>
<body>
<h1><span class="top">블럭</span> 스타일 태그의 <span class="top">스타일 조정</span></h1>
<hr>
<div id="t">가나다라마바사아</div>
<div>1234356789</div>
<div>abcdefghij</div>

</body>
</html>


<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        #t1 {
            color:green;
        }
        #t2 {
            color:red;
        }
        #t3 {
            color:#0000ff;
            background-color:yellow;
            background-color:transparent;
            background-repeat:repeat
        }
    </style>
</head>
<body>
<h1>CSS로 무엇을 할 수 있을까?</h1>
<hr>
<h2 id="t1">둘리</h2>
<h2>또치</h2>
<h2 id="t2">도우너</h2>
<h2>희동이</h2>
<h2>마이콜</h2>
<h2 id="t3">고길동</h2>
</body>
</html>

<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        a{
        text-decoration: none;
        }
        a:hover{
        font-weight: bold;
        }
        img:hover{
        opacity: 0.5  /*0.0~1.0(완전 불투명)*/
        }
        h1{
        background-color: pink;
        width: 400mm
        }
    </style>
</head>
<body>
<h1>CSS 학습(1)</h1>
<hr>
<a href="http://www.naver.com/">네이버</a>
<a href="http://www.daum.net/">다음</a>
<a href="http://www.google.com/">구글</a>
<hr>
<img src="/edu/images/totoro.png"width="300">
</body>
</html>

<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<h1>블럭 스타일 태그와 인라인 스타일 태그</h1>
<hr>
<div>가나다라마바사아</div>
<div>0123456789</div>
<div>abcdefghij</div>
<hr>
<span>가나다라마바사아</span>
<span>0123456789</span>
<span>abcdefghij</span>
</body>
</html>

<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        div{
        background-color: lime;
        margin: 5px;
        width: 300px;
        height: 200px;
        font-size: 1.5em;
        padding: 10px;
        }
        span{
        background-color: orange;
        margin: 5px;
        width: 300px;
        height: 200px;
        font-size: 1.5em;
        padding: 10px;
        }
        .top{
        color: #6600ff;
        }
    </style>
</head>
<body>
<h1><span class="top">블럭</span>스타일 태그와 <span class="top">인라인</span> 스타일 태그</h1>
<hr>
<div>가나다라마바사아</div>
<div>0123456789</div>
<div>abcdefghij</div>
<hr>
<span>가나다라마바사아</span>
<span>0123456789</span>
<span>abcdefghij</span>
</body>
</html>

<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        div{
        background-color: lime;
        margin: 5px;
        width: 300px;
        height: 200px;
        font-size: 1.5em;
        padding: 10px;
        text-align: center;
        margin-left: auto;
        margin-right: auto;
        border-radius: 100px;
        }
        .top{
        color: #6600ff;
        }
        h1{
        text-align: center;
        text-shadow: 2px 2px 5px pink, -4px -4px 5px red;
        }
        h1:hover{
        transform: rotate(-2deg);
        transition: transform 2s;
        }
    </style>
</head>
<body>
<h1><span class="top">블럭</span>스타일 태그의 <span class="top">스타일 조정</span></h1>
<hr>
<div>가나다라마바사아</div>
<div>0123456789</div>
<div>abcdefghij</div>
</body>
</html>

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>CSS 학습</title>
<style>
	table, th, td {
		border : 1px solid black;
		border-collapse : collapse;
	}
	th {
		background-color : lime;
	}
</style>
</head>
<body>
<h1>테이블 출력하기</h1>
<hr>
<table>
	<tr><th>이름</th><th>고향</th><th>나이</th></tr>  
	<tr><td>둘리</td><td>쌍문동쌍문동쌍문동쌍문동쌍문동</td><td>10</td></tr>  
	<tr><td>도우너</td><td>깐따비아</td><td>9</td></tr>  
	<tr><td>또치</td><td>아프리카</td><td>10</td></tr>  
</table>
</body>
</html>

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>CSS 학습</title>
<style>
	div {
		width : 60%;
		height : 200px;
		margin : 20px auto;
		padding : 10px;
		text-align : center;
	}  
	div:nth-of-type(1) {
		background-color : yellow;
		border : 2px solid red;
		border-radius : 30px;
	}
	div:nth-of-type(2) {
		background-color : lightgreen;
		border : 2px dotted magenta;
		border-radius : 20px 40px 60px 80px;
	}
	div:nth-of-type(3) {
		background-color : #000000;
		border : 5px dashed #ffffff;
	}
	div:nth-of-type(4) {
		background-color : silver;
		border : 15px inset #ffffff;
	}
	div:nth-of-type(5) {
		background-color : gold;
		border : 15px outset #ffffff;
	}
</style>
</head>
<body>
<h1>둥근 보더 만들기</h1>
<div>텍스트를 출력합니다.</div>
<div>텍스트를 출력합니다.</div>
<div>텍스트를 출력합니다.</div>
<div>텍스트를 출력합니다.</div>
<div>텍스트를 출력합니다.</div>
</body>
</html>


<!doctype html>
<html lang="ko">
<head>
<meta charset="utf-8">
<title>CSS 학습</title>
<style>
	div {
		width : 100%;
		height : 100px;
		margin-bottom : 10px;
	}
	div.jbGrad01 {
		background-image : linear-gradient(to bottom, yellow, green)
	}
	div.jbGrad02 {
		background-image : linear-gradient(to top, yellow, white, green)
	}
	div.jbGrad03 {
		background-image : linear-gradient(to right, yellow, white, white, green)
	}
	div.jbGrad04 {
		background-image : linear-gradient(to left, yellow, white, green)
	}
	div.jbGrad05 {
		background-image : linear-gradient(45deg, yellow, white, green)
	}
	div.jbGrad06 {
		background-image : linear-gradient(to right, red, orange, yellow, green, blue, navy, purple);
		font-size : 3em;
		text-align : center;
		text-shadow : 2px 2px 5px white, -2px -2px 5px white;
	}
	div.jbGrad07{
		background-image : url("/edu/images/pink.gif");		
	}
</style>
</head>
<body>
	<h1>백그라운드 그라디언트</h1>
	<hr>
  	<div class="jbGrad01">to bottom</div>
  	<div class="jbGrad02">to top</div>
  	<div class="jbGrad03">to right</div>
  	<div class="jbGrad04">to left</div>
  	<div class="jbGrad05">45deg</div>
  	<div class="jbGrad06">ㅋㅋㅋㅋㅋㅋ</div>
  	<div class="jbGrad07">ㅋㅋㅋㅋㅋㅋ</div>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>CSS 학습</title>
<style>
	h1 {
		width : 240px;
		background-image : linear-gradient(to right, yellow, pink, white, green)

	}
	em {
		background-color:#0000ff;
	}
</style>
</head>

<body>
	<h1>레이아웃 나누기</h1>
	<em>오늘은 즐거운 화요일</em><br>
	<strong>고르세용</strong><br>
	<mark>먹고싶은거</mark>
	<ul>
		<li>메뉴1</li>
		<li>메뉴2</li>
		<li>메뉴3</li>
		<li>메뉴4</li>
	</ul>
	<h2>제목1</h2>
	<p>내용1</p>
	<h2>제목2</h2>
	<p>내용2</p>
	<h3>홈페이지 정보(바닥 글)</h3>	
</body>
</html>


<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>CSS 학습</title>
</head>
<body>
	<header>
		<h1>레이아웃 나누기</h1>
		<em>오늘은 즐거운 월요일</em>
	</header>
	<nav>
		<strong>고르세용</strong><br>
		<mark>먹고싶은거</mark>
		<ul>
			<li>메뉴1</li>
			<li>메뉴2</li>
			<li>메뉴3</li>
			<li>메뉴4</li>
		</ul>
	</nav>
	<section>
		<article>
			<h2>제목1</h2>
			<p>내용1</p>
		</article>
		<article>
			<h2>제목2</h2>
			<p>내용2</p>
		</article>
	</section>
	<footer>
		<h3>홈페이지 정보(바닥 글)</h3>
	</footer>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>CSS 학습</title>
<style>
	header {
		border : 1px dotted red;
	}
	footer {
		border : 1px dotted orange;
	}
	section {
		border : 1px dotted blue;		
	}
	article {
		border : 1px dotted green;
	}
	nav {
		border : 1px dotted magenta;
	}
	aside {
		border : 1px dotted brown;
	}
</style> 
</head>
<body>
	<header>
		<h1>레이아웃 나누기</h1>
		<em>오늘은 즐거운 월요일</em>
	</header>
	<nav>
		<strong>고르세용</strong><br>
		<mark>먹고싶은거</mark>
		<ul>
			<li>메뉴1</li>
			<li>메뉴2</li>
			<li>메뉴3</li>
			<li>메뉴4</li>
		</ul>
	</nav>
	<section>
		<article>
			<h2>제목1</h2>
			<p>내용1</p>
		</article>
		<article>
			<h2>제목2</h2>
			<p>내용2</p>
		</article>
	</section>
	<footer>
		<h3>홈페이지 정보(바닥 글)</h3>
	</footer>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>CSS 학습</title>
<style>
   	* {
		margin : 0
	}

	header {
		width : 100%;
		height : 100px;
		background-color : yellow;
	}
	nav {
		width : 30%;
		height : 500px;
		float : left;
		background-color : pink;
	}
	section {
		width : 70%;
		height : 500px;
		float : right;
		background-color : skyblue;
	}
	article {
		width : 80%;
		height : 200px;
		background-color : magenta;
		margin-left : auto;
		margin-right : auto;
	}
	footer {
		width : 100%;
		height : 50px;
		clear : both;
		background-color : lightgray;
	}

</style>
</head>
<body>
	<header>
		<h1>레이아웃 나누기</h1>
		<em>오늘은 즐거운 월요일</em>
	</header>
	<nav>
		<strong>고르세용</strong><br>
		<mark>먹고싶은거</mark>
		<ul>
			<li>메뉴1</li>
			<li>메뉴2</li>
			<li>메뉴3</li>
			<li>메뉴4</li>
		</ul>
	</nav>
	<section>
		<article>
			<h2>제목1</h2>
			<p>내용1</p>
		</article>
		<article>
			<h2>제목2</h2>
			<p>내용2</p>
		</article>
	</section>
	<footer>
		<h3>홈페이지 정보(바닥 글)</h3>
	</footer>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<link rel="stylesheet"  href="mystyle.css">
</head>
<body>
	<header>
		<h1>레이아웃 나누기(외부 CSS)</h1>
	</header>
	<nav>
		<strong>고르세용</strong><br>
		<mark>먹고싶은거</mark>
		<ul>
			<li>메뉴1</li>
			<li>메뉴2</li>
			<li>메뉴3</li>
			<li>메뉴4</li>
		</ul>
	</nav>
	<section>
		<article>
			<h2>제목1</h2>
			<p>내용1</p>
		</article>
		<article>
			<h2>제목2</h2>
			<p>내용2</p>
		</article>
	</section>
	<footer>
		<h3>홈페이지 정보(바닥 글)</h3>
	</footer>
</body>
</html>


<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>HTML학습</title>
<style>
    h1, h2, h3, h4, a {
        text-align:center;
    }
    #linkarea {
        text-align:center;
    }

</style>
</head>
<body >
<h1>주요 HTML 태그 학습</h1>
<hr>
<a href="http://java.sun.com/"><h1>ㅋㅋㅋ</h1></a>
<h2>ㅋㅋㅋ</h2>
<h3>ㅋㅋㅋ</h3>
<h4>ㅋㅋㅋ</h4>
<hr>
<div id="linkarea">
<a href="http://www.w3.org/">W3C</a><br>
<a href="http://www.w3schools.com/">W3Schools</a><br>
<a href="http://www.python.org/">PYTHON</a>
</div>
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
<html>
<head>
<meta charset="UTF-8">
<title>CSS 학습</title>
<style>
ul.a {
  list-style-type: circle;
}
ul.b {
  list-style-type: square;
}
ul.c {
  list-style-image: url('/edu/images/pink.gif');
}
ol.d {
  list-style-type: upper-roman;
}
ol.e {
  list-style-type: lower-alpha;
}
</style>
</head>
<body>
<h1>CSS 선택자와 속성들 학습(3)</h1>
<hr>
<h2>좋아하는 칼라</h2>
<ul class="a">
	<li>녹색</li>
	<li>보라색</li>
	<li>주황색</li>
</ul>
<ul class="b">
	<li>녹색</li>
	<li>보라색</li>
	<li>주황색</li>
</ul>
<ul class="c">
	<li>녹색</li>
	<li>보라색</li>
	<li>주황색</li>
</ul>
<hr>
<h2>좋아하는 음식</h2>
<ol class="d">
	<li>피자</li>
	<li>떡볶이</li>
	<li>짜장면</li>
</ol>
<ol class="e">
	<li>피자</li>
	<li>떡볶이</li>
	<li>짜장면</li>
</ol>
</body>
</html>

<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        p:nth-child(2) {
            color : red;
        }
        p:nth-of-type(2) {
            color : blue;
        }
       section > h1 {
            color : green;
        }
        section h1 {
            background-color : pink;
        }
        img {
            width : 150px;
        }
        img[src$=gif] {
            border : 1px dotted red;
        }
    </style>
</head>
<body>
<div>
    <h3>어린 왕자</h3>
    <p>1장 </p>
    <p>2장 </p>
</div>
<section>
    <h1>섹션제목</h1>
    <article>
        <h1>아티클제목</h1>
    </article>
</section>
<img src="/edu/images/1.jpg">
<img src="/edu/images/r1.gif">
</body>
</html>

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>CSS 학습</title>
<style>
	div {
		width : 60%;
		height : 200px;
		margin : 20px auto;
		padding : 10px;
		text-align : center;
		background-color : yellow;
		border : 2px solid red;
		border-radius : 30px;
	}
	#one, #three {
	    line-height : 200px;
	}
	#two {
	    display : table;
	}
	#four {
	    display : table;
	}
	p {
	    display : table-cell;
	    vertical-align : middle;
	}
    img {
        vertical-align : middle;
    }
</style>
</head>
<body>
<h1>둥근 보더 만들기</h1>
<div id="one">텍스트를 출력합니다.</div>
<div id="two">
    <p>
        텍스트를 출력합니다.<br>
        텍스트를 출력합니다.<br>
        텍스트를 출력합니다.
    </p>
</div>
<div id="three"><img src ="../images/2.jpg" width="100"></div>
<div id="four"><p>텍스트를 출력합니다.</p></div>
</body>
</html>
```



### - 실습

```python
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>CSS실습1</title>
<style>
    h1 {
        width:300px;
        height:100px;
		border-radius:10px;
        text-align:center;
	    line-height:100px;
		margin:auto;
		background-image : linear-gradient(to right, red, orange, yellow, green, blue, navy, purple);
    }
    div {
		margin:auto;
        width:650px;
        height:215px;
    }
    img {
		width:200px;
		height:200px;
		margin:5px;
    	background-color : #ffffff;
		border:1px solid red;
		box-shadow: 3px 3px 3px pink, 5px 5px 5px red
		}
    img:hover {
        opacity:0.3;
    }
</style>
</head>
<body>
<h1 style="color:white"><span style="color:blue">날씨</span>의 종류</h1>
<hr>
<div>
    <img src="../images/sun.png">
    <img src="../images/rain.png">
    <img src="../images/cloud.png">
</div>
<div>
    <img src="../images/cloud_sun.png">
    <img src="../images/snow.png">
    <img src="../images/etc.png">
</div>

</body>
</html>


<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>CSS실습2</title>
<style>
    h1 {
        width:400px;
        height:100px;
		border-radius:10px;
        text-align:center;
	    line-height:100px;
		margin:auto;
		background-image : linear-gradient(45deg, yellow, green);
    }
    hr {
        height:3px;
		background-image : linear-gradient(to right, red, orange, yellow, green, blue, navy, purple);
    }
    div {
		margin:auto;
        width:890px;
        height:220px;
    }
    img {
		width:200px;
		height:200px;
		border-radius:10px;
		margin:5px;
    	background-color : #ffffff;
		border:2px solid #40ff00;
		box-shadow: 3px 3px 3px #40ff00, 5px 5px 5px #40ff00
		}
    img.cimg1:hover {
        transform:rotate(10deg);
        transition:transform 2s;
    }
    img.cimg2:hover {
        transform:rotate(-10deg);
        transition:transform 2s;
    }

</style>
</head>
<body>
<h1 style="color:white">
    <span style="color:#ff00ff">과일</span>의
    <span style="color:orange">종류</span>
</h1>
<hr>
<div>
    <img class="cimg1" src="../images/r1.gif">
    <img class="cimg1" src="../images/r2.gif">
    <img class="cimg1" src="../images/r3.jpg">
    <img class="cimg1" src="../images/r4.gif">
</div>
<div>
    <img class="cimg2" src="../images/r5.png">
    <img class="cimg2" src="../images/r6.png">
    <img class="cimg2" src="../images/r7.png">
    <img class="cimg2" src="../images/r8.jpg">
</div>

</body>
</html>
```

