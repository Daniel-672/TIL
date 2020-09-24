

# Day2

> BOM객체

### - 교육내용

```html
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<h1>자바스크립트 맛보기</h1>
<hr>
<button onclick="window.alert('클릭하셨군요!!')">클릭해 보세요.</button>
<hr>
<button onclick="displayDate('red')">빨강</button>
<button onclick="displayDate('blue')">파랑</button>
<button onclick="displayDate('yellow')">노랑</button>
<hr>
<output id="target"></output>
<script>
    function displayDate(calorname) {
        var now = new Date();
        var strnow = now.getFullYear() + "년" + (now.getMonth()+1) + "월" + now.getDate() + "일";
        // window.alert(strnow);
        var targetDom = document.getElementById("target");
        console.log(targetDom);
        targetDom.textContent = strnow;
        targetDom.style.color = calorname;

        //document.writeln(strnow + "<br>");
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
<h1>JavaScript의 변수 선언과 활용</h1>
<hr>
<script>
	var v1;
	document.writeln(v1+"<br>");
	v1 = 100;
	document.writeln(v1+"<br>");
	v1 = '가나다';
	document.writeln(v1+"<br>");	
	var v1 = true;
	document.writeln(v1+"<br>");	
	v1 = 123;
	document.writeln(v1+45+"<br>");	
	v1 = '123';
	document.writeln(v1+45+"<br>");	
</script>
<h1>JavaScript의 변수 선언과 활용</h1>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
<h1>자바스크립트의 데이터 타입 채크</h1>
<hr>
<script>
	document.write("<h2>"+ typeof 100 +"</h2>");
	document.write("<h2>"+ typeof 3.14 +"</h2>");
	document.write("<h2>"+ typeof '가' +"</h2>");
	document.write("<h2>"+ typeof "abc" +"</h2>");
	document.write("<h2>"+ typeof '100' +"</h2>");
	document.write("<h2>"+ typeof true +"</h2>");
	document.write("<h2>"+ typeof undefined +"</h2>");
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
<h1>자바스크립트의 변수 선언과 활용(2)</h1>
<hr>
<script>
	document.write("<ul>");
	var v1;
	document.write("<li>"+ v1 +"</li>");
	document.write("<li>"+ typeof v1 +"</li>");
	document.write("<li>"+ (v1+10) +"</li>");
	v1 = 100;
	document.write("<li>"+ v1 +"</li>");
	document.write("<li>"+ typeof v1 +"</li>");
	document.write("<li>"+ (v1+10) +"</li>");
	v1 = true;
	document.write("<li>"+ v1 +"</li>");
	document.write("<li>"+ typeof v1 +"</li>");
	document.write("<li>"+ (v1+10) +"</li>");
	v1 = "가나다";
	document.write("<li>"+ v1 +"</li>");	
	document.write("<li>"+ typeof v1 +"</li>");
	document.write("<li>"+ (v1+10) +"</li>");
	document.write("<ul>");
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
<h1>자바스크립트의 연산자(1)</h1>
<hr>
<pre>
<script>
	document.writeln(10>5);
	document.writeln("abc">"ABC");
	var str = "가나다";
	document.writeln(str == "가나다");
	document.writeln(true == 1);
	document.writeln("100" == 100);
	document.writeln(true === 1);
	document.writeln("100" === 100);	
	document.writeln(10/3);
	document.writeln(10%3);
	var num=10;
	document.writeln(num++);
	document.writeln(--num);
</script>
</pre>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
<h1>자바스크립트의 연산자(2)</h1>
<hr>
<pre>
<script>
	var num=5;
	// num이 짝수이면 "xx는 짝수"
	// num이 홀수이면 "xx는 홀수"
	num % 2 == 0 && document.writeln(num+"는 짝수");
	num % 2 == 0 || document.writeln(num+"는 홀수");
</script>
</pre>
</body>
</html>

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<style>
	span { color : red; }
</style>
</head>
<body>
<h1>자바스크립트의 연산자(2)</h1>
<hr>
<pre>
<script>
	var num=window.prompt("채크하려는 숫자를 입력해 주세요.");
	//window.alert(num+":"+isNaN(num));	
	if(isNaN(num) || num == '' || num == null ) {
		document.writeln("<span>숫자</span>를 입력해 주세요!!!");
	} else {
		num % 2 == 0 && document.writeln(num+"는 짝수");
		num % 2 == 0 || document.writeln(num+"는 홀수");
	}
</script>
</pre>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<style>
	span { color : red; }
</style>
</head>
<body>
<h1>자바스크립트의 연산자(2)</h1>
<hr>
<pre>
<!--  세번 반복  -->
<script>     
	for(var su=1; su < 4 ; su++ ) {
		var num=window.prompt("채크하려는 숫자를 입력해 주세요.");
		//window.alert(num+":"+isNaN(num));	
		if(isNaN(num) || num == '' || num == null ) {
			document.writeln("<span>숫자</span>를 입력해 주세요!!!");
		} else {
			num % 2 == 0 && document.writeln(num+"는 짝수");
			num % 2 == 0 || document.writeln(num+"는 홀수");
		}
	}
</script>
</pre>
</body>
</html>

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<style>
	span { color : red; }
</style>
</head>
<body>
<h1>자바스크립트의 연산자(2)</h1>
<hr>
<pre>
<!--  사용자가 원할 때까지 반복  -->
<script>     
	while(true) {
		var num=window.prompt("채크하려는 숫자를 입력해 주세요.");
		//window.alert(num+":"+isNaN(num));	
		if(isNaN(num) || num == '' || num == null ) {
			document.writeln("<span>숫자</span>를 입력해 주세요!!!");
		} else {
			num % 2 == 0 && document.writeln(num+"는 짝수");
			num % 2 == 0 || document.writeln(num+"는 홀수");
		}
		var result = window.confirm("계속 수행할까요?");
		if(!result)
			break;
	}
</script>
</pre>
</body>
</html>

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
<h1>자바스크립트의 랜덤값 처리</h1>
<hr>
<script>
for(var i=0; i <10; i++){
	var rand = Math.random();// 0.0<= rand < 1.0
	console.log(rand);
	console.log(rand*3);
	console.log(Math.floor(rand*3));
	console.log("-----------------------");	
	document.write(Math.floor(rand*3) +"<br>");
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
<h1>배열 생성과 활용(1)</h1>
<hr>
<script>
var a1 = [];
document.write("<h3>"+ typeof a1 +"</h3>");
document.write("<h3>"+ Array.isArray(a1) +"</h3>");
document.write("<h3>"+ a1.length +"</h3>");
document.write("<h3>"+ a1[0] +"</h3>");
document.write("<hr>");
a1[4] = 100;
document.write("<h3>"+ a1.length +"</h3>");
for(var i=0; i < a1.length; i++)
	document.write("<h4>"+ a1[i] +"</h4>");
document.write("<hr>");
for(var i in a1)  // for(int data : ary)
	document.write("<h4>"+ a1[i] +"</h4>");
document.write("<hr>");
var a2 = [10, '가나다', true, 3.5];
for(var i in a2)  // for(int data : ary)
	document.write("<h4>"+ typeof a2[i] + ":" + a2[i] +"</h4>");
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
<h1>배열 생성과 활용(2)</h1>
<hr>
<script>
var a1 = new Array();  // [ ]
var a2 = new Array(10); // 크기
var a3 = new Array('가'); // 원소값
var a4 = new Array(10, 20); // 원소값
var a5 = new Array(1,2,3,4,5); // 원소값
/* window.alert(a1.length);
window.alert(a2.length);
window.alert(a3.length);
window.alert(a4.length);
window.alert(a5.length); */
document.write(a1 + "<br>");
document.write(a2.toString() + "<br>");
document.write(a3.toString() + "<br>");
document.write(a4.toString() + "<br>");
document.write(a5.toString() + "<br>");
var d = new Date();
document.write(d.toString() + "<br>");
document.write(d + "<br>");
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
<h1>배열 객체의 주요 메서드 활용</h1>
<hr>
<script>
var ary = ['둘리', '또치', '도우너', '희동이', '고길동']
document.write(ary + "<br>");
var ary2 = ary.sort();
document.write(ary + "<br>");
document.write(ary2 + "<br>");
document.write("<hr>");
var ary3 = [30, 11, 5, 27, 9]
document.write(ary3 + "<br>");
var ary4 = ary3.sort(function(a, b){ return a-b;});
document.write(ary3 + "<br>");
document.write(ary4 + "<br>");
document.write("<hr>");
var ary5 = [ ];
ary5.push(100);
ary5.push(200);
ary5.push(500);
document.write(ary5 + "<br>");
document.write(ary5.pop() + "<br>");
document.write(ary5.pop() + "<br>");
document.write(ary5.pop() + "<br>");
document.write(ary5.pop() + "<br>");
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
<h1>함수 정의와 활용(1)-선언적 함수 정의</h1>
<hr>
<script>
function f1() {
	document.write('f1() 호출<br>');	
}
<!--function f2(p1, p2) {-->
<!--	document.write('f2() 호출:'+(p1+p2)+'<br>');-->
<!--}-->

f2 = function(p1, p2) {
	document.write('f2() 호출:'+(p1+p2)+'<br>');
}

f1();
f2(10,20);
document.write('<hr>');
var result1 = f1();
var result2 = f2(100,200);
document.write('result1 : '+result1+' result2 : '+result2);
if(result1 == undefined) {//if(!result1) {
	document.write('<br>리턴값이 없군요!!');
}
document.write('<hr>');
f1(100);
f2(100);
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
<h1>함수 정의와 활용(2)-표현식 함수 정의</h1>
<hr>
<script>
f11();
var f1 = function () {
	document.write('f1() 호출<br>');	
}
var f2 = function (p1, p2) {
	document.write('f2() 호출-'+(p1+p2)+'<br>');	
}
f1();
f2(10,20);
document.write('<hr>');
var result1 = f1();
var result2 = f2(100,200);
document.write('result1 : '+result1+' result2 : '+result2);
if(result1 == undefined) {//if(!result1) {
	document.write('<br>리턴값이 없군요!!');
}
document.write('<hr>');
f1(100);
f2(100);
document.write(typeof f1 + '<br>');	
document.write(typeof f2 + '<br>');	
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
<h2>함수에서 데이터의 타입채크</h2>
<hr>
<button onclick="clickProcess(100);">숫자</button>
<button onclick="clickProcess('100');">문자열</button>
<button onclick="clickProcess(true);">논리값</button>
<button onclick="clickProcess(function(){ });">함수</button>
<button onclick="clickProcess([ ]);">배열</button>
<button onclick="clickProcess({ });">객체</button>
<button onclick="clickProcess();">????</button>
<script>
function clickProcess(p) {
	if (typeof p == "number") {
		alert("숫자 전달!!");
	} else if (typeof p == "string") {
		alert("문자열 전달!!");
	} else if (typeof p == "boolean") {
		alert("논리값 전달!!");
	} else if (typeof p == "function") {
		alert("함수 전달!!");
	} else if (typeof p == "object") {
		if (Array.isArray(p))
			alert("배열객체 전달!!");
		else 
			alert("객체 전달!!");
	} else if (typeof p == "undefined") {  // p == undefined
		alert("전달된 아규먼트 없음!!");
	}	
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
<h1>가변아규먼트 처리 함수 만들기</h1>
<hr>
<script>
function out() {
	document.write("아규먼트 갯수 : "+arguments.length+"<br>");
	for(var i=0; i < arguments.length; i++) 
		console.log(arguments[i]);
	console.log('-----------------------');
}

out();
out(10); out(10,20); out('a', 'b', 'c'); out(1,2,3,4,5,6,7,8);
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
<h1>함수의 아규먼트 처리</h1>
<hr>
<script>
function pr(p) {
	document.write(typeof p + " : " + p + "<br>");	
}
pr(100);
pr("100");
pr(true);
pr(3.5);
pr(new Array(1,2,3));
//prNum(10);
//document.write("ㅋㅋㅋㅋㅋㅋ");
</script>
<hr>
<script>
function prNum(p) {
	if(typeof p == "number")
		document.write("숫자 전달 : " + p + "<br>");
	else if (p == undefined)
		document.write("아규먼트를 전달하시오 : " + p + "<br>");
	else
		document.write(typeof p + " : " + p + "<br>");	
}
prNum(100);
prNum("100");
prNum(true);
prNum(3.5);
prNum(new Array(1,2,3));
prNum();
pr(100000);
</script>
<hr>
<script>
function prAll() {
	for(var i=0; i < arguments.length; i++)
		document.writeln(arguments[i]);
	document.write("<br>");
	return arguments.length;
}
var r1 = prAll(100);
var r2 = prAll(1,2,3,4,5);
var r3 = prAll('a', 'b', '가', true);
var r4 = prAll();
document.write(r1 + "<br>");
document.write(r2 + "<br>");
document.write(r3 + "<br>");
document.write(r4 + "<br>");
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
<h1>아규먼트로 함수 전달하기(고차함수)</h1>
<hr>
<script>
function output(p) {
	if(typeof p == 'function') {
		p("ㅋㅋㅋ");
	} else {
		document.write("<h2>ㅋㅋㅋ : "+p+"</h2>");		
	}	
}
output("둘리");
output(function(param) { console.log(param);})
function myAlert(param) {
//var myAlert = function(param) {	
	window.alert(param);
}
output(myAlert);
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
<h2>고차함수 활용 예</h2>
<hr>
<p>5초후에 이 화면은 바뀝니다..</p> 
<script>
   var displayDate = function () {
		var d = new Date();
		document.write(d.toLocaleString()+"<br>");
	};
	var time = 5000;
	window.setInterval(displayDate, time);
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
<h2>자바스크립트 변수의 스코프(1)</h2>
<hr>
<script>
var i = 100;
var i = 50;
var sum = 0;
document.write("i : " + i + "<br>");
for(var i=0; i < 10; i++) {
	sum += i;
}
document.write("i : " + i + "<br>");
document.write("sum : " + sum + "<br>");
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
<h2>자바스크립트 변수의 스코프(2)</h2>
<hr>
<script src="util.js"></script> 
<script>
var g_v = 100;
function scopeTest() {
	var l_v = 1000;
	writeNewLine("scopeTest() l_v : " + l_v);
	writeNewLine("scopeTest() g_v : " + g_v );
}
scopeTest();
try {
	writeNewLine("l_v : " + l_v  );
} catch(e) {
	writeNewLine(e);
}
writeNewLine("g_v : " + g_v );
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
<h1>자바스크립트의 객체 생성과 사용(객체리터럴)</h1>
<hr>
<script src="util.js"></script>
<script>
	var obj = {
				name : "듀크",
				eat : function(food) {
						writeColor(this.name +"가 "+food+
								                   "를 먹어요!!", "h3", "green");
				}
	}
	obj.eat("바나나");
	obj.eat("딸기");
	hr();
	writeColor(typeof obj, 'h2', "red");
	obj.project = "자바스크립트";
	obj.study = function() {
		writeColor(this.name +"가 "+this.project+
                "를 공부해요!!", "h3", "magenta");
	}
    obj.study();
    hr();
    for(var key in obj)
    	write(key + " : " + obj[key], "h4");
    hr()
    write(obj.project, "h2");
    write(obj["project"], "h2");
    delete obj.study;
    for(var key in obj)
		write(key + " : " + obj[key], "h4");
		
	var me ={
			name:'김유철',
			age:30,
			food:['떡복이', '갈비', '치킨'],
			address: {
					sido:"서울시",
					dong:'상봉동'
			}
	}		
	write(me.food[1], "h2");
	write(me.address.dong)
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
<h1>자바스크립트의 객체 생성과 사용(객체리터럴)</h1>
<hr>
<script src="util.js"></script>
<script>
var student = {
		name : "둘리",
		kor : 90,
		eng : 80,
		math : 95,
		getSum : function() {
			return this.kor + this.eng + this.math;
		},
		getAvg : function() {
			return this.getSum() / 3;
		},
		toString : function() {
			return this.name +"학생의 총점은 "+this.getSum()+
			                              "입니다.";
		}		
}
write("총점 : "+student.getSum(), "h3");
write("평균 : "+student.getAvg(), "h3");
writeColor(student.toString(), "h3", "blue");
writeColor(student, "h3", "blue");
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
<h1>자바스크립트의 객체 생성과 사용(객체리터럴)</h1>
<hr>
<script src="util.js"></script>
<script>
var student1 = {
		name : "둘리",
		kor : 90,
		eng : 80,
		math : 95,
		getSum : function() {
			return this.kor + this.eng + this.math;
		},
		getAvg : function() {
			return this.getSum() / 3;
		},
		toString : function() {
			return this.name +"학생의 총점은 "+this.getSum()+
			                              "입니다.";
		}		
}
var student2 = {
		name : "도우너",
		kor : 85,
		eng : 90,
		math : 95,
		getSum : function() {
			return this.kor + this.eng + this.math;
		},
		getAvg : function() {
			return this.getSum() / 3;
		},
		toString : function() {
			return this.name +"학생의 총점은 "+this.getSum()+
			                              "입니다.";
		}		
}
var student3 = {
		name : "또치",
		kor : 80,
		eng : 90,
		math : 75,
		getSum : function() {
			return this.kor + this.eng + this.math;
		},
		getAvg : function() {
			return this.getSum() / 3;
		},
		toString : function() {
			return this.name +"학생의 총점은 "+this.getSum()+
			                              "입니다.";
		}		
}
writeColor("학생 1 : " + student1, "h3", "blue");
writeColor("학생 2 : " + student2, "h3", "red");
writeColor("학생 3 : " + student3, "h3", "green");
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
<h1>자바스크립트의 객체 생성과 사용(생성자함수)</h1>
<hr>
<script src="util.js"></script>
<script>
function Student(p1, p2, p3, p4) {
	this.name = p1;
	this.kor = p2;
	this.eng = p3;
	this.math = p4;
	this.getSum = function() {
		return this.kor + this.eng + this.math;
	};
	this.getAvg = function() {
		return this.getSum() / 3;
	};
	this.toString = function() {
		return this.name + "학생의 총점은 " + 
		                       this.getSum() + "입니다.";		                                
	};
}

var student1 = new Student('둘리', 90, 80, 95); 
var student2 = new Student('도우너', 80, 90, 95);
var student3 = new Student('또치', 90, 70, 95);

writeColor("학생 1 : " + student1, "h3", "blue");
writeColor("학생 2 : " + student2, "h3", "red");
writeColor("학생 3 : " + student3, "h3", "green");
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
<h1>자바스크립트의 객체 생성과 사용(생성자함수)</h1>
<hr>
<script src="util.js"></script>
<script>
function Student(p1,p2,p3,p4){
			this.name = p1,
			this.kor = p2,
			this.eng = p3,
			this.math = p4
}			
Student.prototype.getSum = function() {
				return this.kor+this.eng+this.math;
};
Student.prototype.getAvg = function() {
				return this.getSum() / 3 ;
};
Student.prototype.toString = function() {
				return this.name+"학생의 총점은 "+
				               this.getSum()+"입니다.";
};
Student.

var student1 = new Student('둘리', 90, 80, 95);
var student2 = new Student('또치', 80, 90, 80);
var student3 = new Student('도우너', 85, 70, 80);

writeColor("학생1 : "+student1.toString(), "h3", "green");
writeColor("학생2 : "+student2, "h3", "blue");
writeColor("학생3 : "+student3, "h3", "red");
</script>
</body>
</html>

<!DOCTYPE html>
<html lang="ko">
  <head>
    <script type="text/javascript" src="https://www.gstatic.com/charts/loader.js"></script>
    <script type="text/javascript">
      google.charts.load('current', {'packages':['corechart']});
      google.charts.setOnLoadCallback(drawChart);

      function drawChart() {

        var data = google.visualization.arrayToDataTable([
          ['Task', 'Hours per Day'],
          ['Work',     20],
          ['Eat',      2],
          ['Commute',  2],
          ['Watch TV', 2],
          ['Sleep',    7]
        ]);

        var options = {
          title: 'My Daily Activities'
        };

        var chart = new google.visualization.PieChart(document.getElementById('piechart'));

        chart.draw(data, options);
      }
    </script>
  </head>
  <body>
    <div id="piechart" style="width: 900px; height: 500px;"></div>
  </body>
</html>

```



### - 실습

```python
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>exercise1</title>
</head>
<body>
<script>
		var num=window.prompt("1 ~ 9 사이의 숫자를 입력해 주세요.");

		if((isNaN(num) || num == '' || num == null || num < 1 || num > 9)) {
			document.writeln("<span>1 ~ 9 사이의 숫자</span>를 입력해 주세요!!!");

		} else {
	        document.write("<h1 style=" + "color:#cc3399" + ";" + "margin:0" + ">" + num + " 단 입니다." + "</h1>");
		    document.writeln("--------------------------" + "<br>" )
            for(var inc=1; inc < 10 ; inc++ ) {
                document.write(num + " x " + inc + " = " + num * inc + "<br>");
            }
		}
</script>
</body>
</html>

<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>exercise2</title>
</head>
<body>
<script>
    while(true) {
		var num=window.prompt("1 ~ 9 사이의 숫자를 입력해 주세요.");

		if((isNaN(num) || num == '' || num == null || num < 1 || num > 9)) {
            window.alert("1 ~ 9 사이의 숫자를 입력해 주세요!!!");
		} else {
	        document.write("<h1 style=" + "color:#cc3399" + ";" + "margin:0" + ">" + num + " 단 입니다." + "</h1>");
		    document.writeln("--------------------------" + "<br>" )
            for(var inc=1; inc < 10 ; inc++ ) {
                document.write(num + " x " + inc + " = " + num * inc + "<br>");

            }
            break;
		}
    }
</script>
</body>
</html>


<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>exercise3</title>
</head>
<body>
<script>
    var arr = new Array(10, 5, 7, 21, 4, 8, 18);
    arrSum = 0

    for(var i=0; i < arr.length; i++)
        arrSum += arr[i]
    document.write("<h1>"+ "모든 원소의 합 : " + arrSum +"</h1>");

    arr.sort(function(a, b){ return a-b;});

    document.write("<ul>");
    document.write("<li>"+ "최대값 : " + arr[arr.length-1] +"</li>");
    document.write("<li>"+ "최소값 : " + arr[0] +"</li>");
    document.write("<ul>");
</script>
</body>
</html>


<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>exercise4</title>
</head>
<body>
<script>

function sum(num) {
    var sumValue = 0;
    if (num == undefined)
        return;
    else {
	    for(var i=1; i <= num; i++) {
            sumValue += i;
        }
        return sumValue;
    }
}


var rand = Math.random();
ranNum = Math.floor(rand * 6)
document.write("난수 : " + ranNum + "<br>");

if (ranNum == 0) {
    var result = sum();
	}
else {
    var result = sum(ranNum);
	}

if (result) {
    document.write("호출 결과값 : " + result + "<br>");
	}
else {
    document.write("결과값이 없어요!!" + "<br>");

	}
;
;
</script>
</body>
</html>


<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>exercise5</title>
</head>
<body>
<script>
function calc() {
    var sumValue = 0;
    if (arguments.length == 0)
        sumValue = 0;
    else {
	    for(var i=0; i < arguments.length; i++) {
	        if(isNaN(arguments[i])) {
			sumValue = "숫자만 전달하세요"
			break;
	        }
            else
            sumValue += Number(arguments[i]);
        }

    }
    return sumValue;
}

document.write("<h3>" + calc() + "</h3><br>")
document.write("<h3>" + calc(10, 20, '30') + "</h3><br>")
document.write("<h3>" + calc(10, '가나다', 20) + "</h3><br>")
document.write("<h3>" + calc(1,2,3,4,5) + "</h3><br>")

</script>
</body>
</html>


<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>exercise6</title>
</head>
<body>
<script src="util.js"></script>
<script>
function printObject(p) {
        if (typeof p != "object") return;
        writeColor(p.msg, p.tag, p.color);
    }

var obj ={  'A': {msg:'안녕하세요.',
                tag:'h1',
                color: 'red'},
            'B': {msg:'반갑습니다.',
                tag:'h2',
                color: 'yellow'},
            'C': {msg:'고맙습니다.',
                tag:'h3',
                color: 'black'},
            'D': {msg:'잘지네세요.',
                tag:'h4',
                color: 'pink'},
            'E': {msg:'건강하세요.',
                tag:'h5',
                color: 'lime'}
}

printObject('Hi')

for(var key in obj)
    printObject(obj[key]);

</script>
</body>
</html>


<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>exercise7</title>
</head>
<body>
<script>
var rand = Math.random();
ranNum = Math.floor(rand * 3) + 1

if (window.confirm("선택된 숫자는 " + ranNum + "입니다. 이동 할까요?")) {

    switch (ranNum) {
        case 1:
            location.href = "http://www.daum.net/";
            break;
        case 2:
            location.href = "http://www.naver.com/";
            break;
        case 3:
            location.href = "http://www.google.com/";
            break;
        }
    }
else location.href = "../first.html";

</script>
</body>
</html>

<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Insert title here</title>
    <style>
        button:nth-of-type(1) {
        color : red;
        font-size : 1.5em;
        }
        button:nth-of-type(2) {
        color : blue;
        font-size : 1.5em;
        }
        button:nth-of-type(3) {
        color : green;
        font-size : 1.5em;
        }
    </style>
</head>
<body>
<button onclick="changeColor('red');">빨강색</button>
<button onclick="changeColor('blue');">파랑색</button>
<button onclick="changeColor('green');">녹&nbsp;&nbsp;색</button>
<hr>
<h2></h2>

<script>

    var h2dom = document.getElementsByTagName("h2");

    window.onload = function() {
        var now = new Date();
        h2dom[0].textContent  = "오늘은 " + now.getFullYear() + "년 " + (now.getMonth()+1) + "월 " + now.getDate() + "일입니다.";
    }

    function changeColor(v_color) {
        h2dom[0].style.color =v_color;
    }

</script>
</body>
</html>

<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>exercise9</title>

</head>
<body>

<button onclick="showImg()">이미지 보이기(인라인)</button>
<button onclick="removeImg()">이미지 숨기기(인라인)</button>
<br>
<button>이미지 보이기(고전)</button>
<button>이미지 숨기기(고전)</button>
<br>
<button>이미지 보이기(표준)</button>
<button>이미지 숨기기(표준)</button>

<br>
<img src="" width="200" >
<script>

// 인라인
var target = document.getElementsByTagName("img")[0];

function showImg() {
	target.src = "../images/kakao/g1.png";
    }

function removeImg() {
	target.src = "";
    }

// 고전
var doms = document.querySelectorAll("button");
var dom1 = doms[2];
var dom2 = doms[3];

dom1.onclick = function () {
    target.src = "../images/kakao/g1.png";
    }

dom2.onclick = function () {
    target.src = "";
    }

// 표준
var dom3 = doms[4];
var dom4 = doms[5];

dom3.addEventListener("click", showImg);
dom4.addEventListener("click", removeImg);

</script>

</body>
</html>


<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>exercise10</title>
    <style>
        .classbtn {
            border-radius:5px;
            background-color:white;
            width:18%;
        	margin-bottom:10px;
        }
        div {
            text-align: center;
            border-style:solid;
            border-color:Black;
            border-radius:5px;
            width:50%;
		    margin:auto;
        }

    </style>
</head>

<body>
    <button id="init" data-index="0">이미지1</button>
    <button data-index="1">이미지2</button>
    <button data-index="2">이미지3</button>
    <button data-index="3">이미지4</button>
    <button data-index="4">이미지5</button>

    <div>
        <img src="" width="300" />
    </div>

    <script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
    <script>
        var imglst = ["../images/kakao/g1.png", "../images/kakao/g2.png",
                      "../images/kakao/g3.png", "../images/kakao/g4.png",
                      "../images/kakao/g5.png"];

        $(document).ready(function () {
            $('button').addClass('classbtn');
            $('button').on({"click" : function () {
                $('button').css('background-color','white');
                $(this).css('background-color', 'pink');
                $('img').attr('src',imglst[$(this).attr("data-index")]);
                    }
            });
            $('button#init').click();
        });
    </script>
</body>
</html>
```

