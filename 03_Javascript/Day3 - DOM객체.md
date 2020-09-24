

# Day3

> DOM객체

### - 교육내용

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
<h1>컨텐트1</h1>
<h1>컨텐트2</h1>
<h1>컨텐트3</h1>
<h1>컨텐트4</h1>
<h2>컨텐트5</h2>
<script src="../util.js"></script>
<script>
var h1dom = document.getElementsByTagName("h1");
write(h1dom.length, "h3");
for(var i=0; i <h1dom.length; i++) {
	writeColor(h1dom[i].textContent, "h4", "red");
<!--	h1dom[i].textContent = 'test';-->
	}
var h2dom = document.getElementsByTagName("h2");
writeColor(h2dom[0].textContent, "h2", "green");
writeColor(h1dom[0], "h2", "blue");
writeColor(h2dom[0], "h2", "blue");
var h5dom = document.getElementsByTagName("h5");
writeColor(h5dom.length, "h2", "magenta");
</script>
</body>
</html>

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<script>
function myf() {
var h1dom = document.getElementsByTagName("h1");
console.log(h1dom.length);
for(var i=0; i <h1dom.length; i++) {
	console.log(h1dom[i].textContent);
<!--	h1dom[i].textContent = 'test';-->
	}
var h2dom = document.getElementsByTagName("h2");
console.log(h2dom[0].textContent);
console.log(h1dom[0]);
console.log(h2dom[0]);
var h5dom = document.getElementsByTagName("h5");
console.log(h5dom.length);
}
</script>
</head>
<body onload="myf()">

<h1>컨텐트1</h1>
<h1>컨텐트2</h1>
<h1>컨텐트3</h1>
<h1>컨텐트4</h1>
<h2>컨텐트5</h2>

</body>
</html>


<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<script>
//이벤트 핸들러를 사용하기 위해서 function으로 묶어버린다. ---> 이래도 결과값 안나옴
function myf(){
    var h1dom = document.getElementsByTagName("h1");
    console.log(h1dom.length, "h3");
    //이벤트 핸들러 안의 document.write는 write 아래의 dom 내용(현재 document 내용)을 모두 지우고 출력하기 시작함
    //굳이 이렇게 출력하고자 한다면 write 부분을 모두 console.log로 바꾸면 출력됨.
    //대신 색깔 등의 속성은 주기 어려우므로, 그 부분을 지운다. 여기선 색깔 지우면 다른 html 파일(src) 안들고와도 되서 삭제함.

    for(var i=0; i <h1dom.length; i++)
	    console.log(h1dom[i].textContent);
    var h2dom = document.getElementsByTagName("h2");
    console.log(h2dom[0].textContent);
    console.log(h1dom[0]);
    console.log(h2dom[0]);
    var h5dom = document.getElementsByTagName("h5");
    console.log(h5dom.length);
}
</script>
</head>
<body onload="myf()">
<h1>컨텐트1</h1>
<h1>컨텐트2</h1>
<h1>컨텐트3</h1>
<h1>컨텐트4</h1>
<h2>컨텐트5</h2>
</body>
</html>



<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
<script src="../util.js"></script>

<h1 id="t1">컨텐트1</h1>
<h2 id="t2">컨텐트5</h2>
<p id="t3">컨텐트2</p>
<div id="t4">컨텐트2</div>
<img id="t5" src="../../images/totoro.png" width="100">
<hr>
<output id="p"></output>
<hr>
<script>
window.onload = function() {
	var dom1 = document.getElementById("t1");
	console.log(dom1);
	console.log(dom1.textContent);
	var dom2 = document.getElementById("t3");
	console.log(dom2);
	var dom3 = document.getElementById("t4");
	console.log(dom3);
	var dom4 = document.getElementById("t5");
	console.log(dom4);
	console.log(dom4.getAttribute("src"));
	console.log(dom4.src); 
	var dom5 = document.getElementById("p");
	dom5.innerHTML = "<h2>"+new Date().toLocaleString()+"</h2>";
	//dom5.textContent = "<h2>"+new Date().toLocaleString()+"</h2>";
	var dom6
}
</script>

- 인라인 이벤트 모델
  태그 속성으로 구현
<button onclick="console.log('test'); console.log('test2');">테스트</button>
<button id="dom2">테스트2</button>

- 고전 이벤트 모델
  이벤트 핸들러를 등록하려는 DOM객체를 찾아서 변수에 담는다.(dom)
  dom6.onclick = funtion() { action.... }

- 표준 이벤트 모델
  이벤트 핸들러를 등록하려는 DOM객체를 찾아서 변수에 담는다.(dom)
  dom.addEventListener("이벤트타입명", 함수)</body>
</html>



<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<script src="../util.js"></script>
</head>
<body>
<h1 id="test">DOM객체를 찾자</h1>
<h1>ㅋㅋㅋㅋㅋㅋㅋ</h1>
<hr>
<script>
var dom = document.getElementsByTagName("h1");
write(dom, "h2");
write(dom[1], "h2");
write(dom[1].textContent, "h2"); // innerText
write(dom[1].innerHTML, "h2");
hr();
dom = document.getElementById("test");
write(dom, "h2");
write(dom.textContent, "h2");
window.setTimeout(function() {
	dom.innerHTML = "오늘은 불금";
	dom.style.color ="red";
	dom.style.backgroundColor ="lime";
}, 5000);
</script>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
<h1>시간정보 출력하기</h1>
<hr>
<button onclick="startTime()">시간을 알려주라옹...</button>
<button onclick="stopTime()">시간 출력을 종료하라옹...</button>
<output></output>
<script>
var target = document.getElementsByTagName("output")[0];
function startTime() {
	var d = new Date();
	target.innerHTML = "<h2>"+d.toLocaleString()+"</h2>";
}
function stopTime() {
	target.innerHTML = "";
}
</script>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
<h1>시간정보 출력하기</h1>
<hr>
<button onclick="startTime()">시간을 알려주라옹...</button>
<button onclick="stopTime()">시간 출력을 종료하라옹...</button>
<output></output>
<script>
var target = document.getElementsByTagName("output")[0];
var setId;
function startTime() {
	var d = new Date();
	target.innerHTML = "<h2>"+d.toLocaleString()+"</h2>";
	setId = window.setTimeout(startTime, 1000);
}
function stopTime() {
	//target.innerHTML = "";
	window.clearTimeout(setId);
}
</script>
</body>
</html>



<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
<h1>시간정보 출력하기</h1>
<hr>
<button onclick="startTime()">시간을 알려주라옹...</button>
<button onclick="stopTime()">시간 출력을 종료하라옹...</button>
<output></output>
<script>
// setInterval()을 사용하여 동일한 기능 구현
var target = document.getElementsByTagName("output")[0];
var setId;
function startTime() {
	setId = window.setInterval(function(){
		var d = new Date();
		target.innerHTML = "<h2>"+d.toLocaleString()+"</h2>";
	}, 1000);
}
function stopTime() {
	//target.innerHTML = "";
	window.clearInterval(setId);
}
</script>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
<h1 style="text-shadow: 2px 2px 3px gray">세 가지 이벤트 모델</h1>
<hr>
<h2 onclick="f1(this);">인라인 이벤트 모델</h2>
<hr>
<h2 id="t1">고전 이벤트 모델</h2>
<hr>
<h2 id="t2">표준 이벤트 모델</h2>
<hr>
<script>
	function f1(p) {
		alert(p.textContent);
		alert(document.querySelectorAll('h2')[0].textContent);
		//alert(this.textContent);
	}
	var dom2 = document.querySelector('#t1');
    var dom3 = document.querySelector('#t2');
	function f2(e) {
		alert(dom2.textContent);
		alert(this.textContent);
		alert(e.target.textContent);
	}
	function f3(e) {
		alert(dom3.textContent);
		alert(this.textContent);
		alert(e.target.textContent);
	}    
    dom2.onclick = f2;
    dom3.addEventListener("click", f3);
</script>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
<h1>세 가지 이벤트 모델</h1>
<hr>
<h1 onclick="f1();">인라인 이벤트 모델</h1>
<hr>
<h1 id="t1">고전 이벤트 모델</h1>
<hr>
<h1 id="t2">표준 이벤트 모델</h1>
<hr>
<script>
    //console.log(this);
	function f1() {
		alert(document.querySelectorAll('h1')[1].textContent);
	}
	var dom2 = document.querySelector('#t1');
    var dom3 = document.querySelector('#t2');
	function f2(e) {
		alert(e.target.textContent);
		alert(this.textContent);
		//console.log(this);
	} 
    dom2.onclick = f2;
    dom3.addEventListener("click", f2);
</script>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
<h1>고전 이벤트 모델과 표준 이벤트 모델의 차이</h1>
<hr>
<button>고전 이벤트 모델</button>
<button>표준 이벤트 모델</button>
<script>
    var doms = document.querySelectorAll("button");
	var dom1 = doms[0];
	var dom2 = doms[1];
	
	dom1.onclick = function () {
								 alert("첫 번째 핸들러 수행(고전)");
							  };
	dom1.onclick = function () {					
								 alert("두 번째 핸들러 수행(고전)");
							  };

	dom2.addEventListener("click", 
			                 function () { alert("첫 번째 핸들러 수행(표준)");});
	dom2.addEventListener("click", 
            function () { alert("두 번째 핸들러 수행(표준)");});

</script>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
<h1>자바스크립트의 이벤트 모델</h1>
<hr>
<button onmouseover="test1();">인라인이벤트모델</button>
<button id="b1">고전이벤트모델</button>
<button id="b2">표준이벤트모델</button>
<script>
function test1() {
	alert("인라인이벤트모델 버튼 클릭");
}
function test2() {
	alert("고전이벤트모델 버튼 클릭");
	btn1.onmouseover = null;
}
function test3() {
	alert("표준이벤트모델 버튼 클릭");
	btn2.removeEventListener("mouseover", test3);
}
var btn1 = document.querySelector("#b1");
var btn2 = document.getElementById("b2");
btn1.onmouseover = test2;  // 고전
btn2.addEventListener("mouseover", test3);
</script>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
<h1>디폴트 이벤트 핸들러</h1>
<hr>
<a href="http://www.w3schools.com/" onclick="test1(); return false;">HTML5 학습하기(인라인)</a><hr>
<a id="t1" href="http://www.w3schools.com/">HTML5 학습하기(고전)</a><hr>
<a id="t2" href="http://www.w3schools.com/">HTML5 학습하기(표준)</a>
<script>
function test1() {
	alert("인라인이벤트모델 버튼 클릭");	
}
function test2() {
	alert("고전이벤트모델 버튼 클릭");	
	return false;
}
function test3(e) {
	alert("표준이벤트모델 버튼 클릭");
	e.preventDefault();
}
var link1 = document.querySelector("#t1");
var link2 = document.getElementById("t2");
link1.onclick = test2;  // 고전
link2.addEventListener("click", test3);



</script>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<style>
	section {
		border : 1px solid lime;	
		padding :10%;
		margin : 0px auto;	
	}
	div {
		border : 1px solid blue;	
		width : 80%;
		padding :10%;
		margin : 0px auto;	
	}
	h1 {
		border : 1px solid red;	
		width : 80%;
		padding :10%;
		margin : 0px auto;		
	}
</style>

</head>
<body>
  <section>
	<div>
		<h1>테스트</h1>
	</div>
  </section>
<script>
function clickHandler() {
	var dom1 = document.getElementsByTagName("h1")[0];
	var dom2 = document.getElementsByTagName("div")[0];
	var dom3 = document.getElementsByTagName("section")[0];
	var dom4 = document.getElementsByTagName("body")[0];
	dom1.addEventListener("click", displayAlert);	
	dom2.addEventListener("click", displayAlert);	
	dom3.addEventListener("click", displayAlert);	
	dom4.addEventListener("click", displayAlert);	
}
function displayAlert(e) {
	window.alert(e.target+"\n"+e.currentTarget+"\n"+this);
	//e.stopPropagation();
}
window.addEventListener("load", clickHandler);
</script>
</body>
</html>



<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<style>
	section {
		border : 1px solid lime;	
		padding :10%;
		margin : 0px auto;	
	}
	div {
		border : 1px solid blue;	
		width : 80%;
		padding :10%;
		margin : 0px auto;	
	}
	h1 {
		border : 1px solid red;	
		width : 80%;
		padding :10%;
		margin : 0px auto;		
	}
</style>

</head>
<body onclick="alert('body태그');">
  <section onclick="alert('section태그');">
	<div onclick="alert('div태그');">
		<h1>테스트</h1>
	</div>
  </section>
<script>
function clickHandler() {
	var list = document.getElementsByTagName("h1");
	list[0].addEventListener("click", displayAlert);	
	list = document.getElementsByTagName("section");
	list[0].addEventListener("click", displayAlert);	
}
function displayAlert(e) {
	window.alert("h1 태그가 클릭됨!!"+this+e.target+e.currentTarget);
	//e.stopPropagation();  	
}
window.addEventListener("load", clickHandler);
</script>
</body>
</html>



<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<style>
	div {
		border : 1px solid blue;	
		width : 80%;
		padding :10%;
		margin : 0px auto;	
	}
	h1 {
		border : 1px solid green;	
		background : #b3ffb3;
		width : 80%;
		padding :10%;
		margin : 0px auto;		
	}
</style>
</head>
<body>
<div>
<h1>테스트</h1>
</div>
<script>
function clickHandler() {
	var h1Tag = document.getElementsByTagName("h1")[0];
	h1Tag.addEventListener("click", displayAlert);
}
function displayAlert(e) {	
	window.alert("클릭 : " + e.pageX + ", " + e.pageY);
	window.alert("클릭 : " + e.screenX + ", " + e.screenY);
	
}
window.addEventListener("load", clickHandler);
</script>
</body>
</html>




<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
<p id="demo" onclick="myFunction()">Click me to change my text color.</p>

<script>
function myFunction() {
    var pdom = document.getElementById("demo");
    alert(pdom.getAttribute("id"));
    alert(pdom.id);
    pdom.style.color = "red";
    // 백그라운드 칼라를 "lime" 으로 설정한다.
     pdom.style.backgroundColor = "lime";
    // 텍스트 굵기는 굵게 한다.
     pdom.style.fontWeight = "bold";
}
</script>
</body>
</html>







```



### - 실습

```python

```

