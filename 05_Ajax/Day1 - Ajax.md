

# Day1

> Ajax

### - 교육내용

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>비 ajax 통신과 ajax 통신 비교</title>
</head>
<body>
<h1>AJAX 통신 테스트</h1>
<a href="content/sample.txt">하이퍼링크로요청</a>
<br><br>
<a href="content/sample.txt"><img src="../images/totoro.png" width="100"></a>
<br><br>
<button onclick="location.href='content/sample.txt';">버튼을클릭하여요청</button>
<br><br>
<button onclick="requestAjax();">버튼을클릭하여요청(AJAX사용)</button>
<hr>
<output id="result"></output>
<script>
function requestAjax() {
	var req = new XMLHttpRequest();
	var result = document.getElementById("result");
	req.onreadystatechange = function() {		
		alert("req.status : "+ req.status + "req.readyState : "+ req.readyState);		
		if(req.status == 200 && req.readyState == 4)
			result.innerHTML += "<h3>"+req.responseText+"</h3>"; 
	}	
	req.open("GET", "content/sample.txt", true);	
	req.send();	
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
<h1>JavaScript로 구현하는 Ajax 프로그램-XML</h1>
<hr>
<script>
window.onload = function() {
	var request = new XMLHttpRequest();
	request.onreadystatechange = function() {
		if(request.readyState == 4) {
			if(request.status == 200) {
				var xml = request.responseXML;
				alert(xml);
				var rootE = xml.getElementsByTagName("testxml");
				var output = "";
				alert(rootE[0].childNodes.length);
				for(var i=1 ; i <rootE[0].childNodes.length ; i+=2)
					output += "<h2>"+
					   rootE[0].childNodes[i].firstChild.nodeValue
					   +"</h2>";
				document.body.innerHTML += output;
			}
		}		
	}
	request.open("GET", "content/testxml.xml", true);
	request.send();
}
</script>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
<meta charset='utf-8'>
<title>New Web Project</title>
</head>
<body>
	<h1>JavaScript로 구현하는 Ajax 프로그램-XML</h1>
	<hr>
	<script>
		window.onload = function() {
			var request = new XMLHttpRequest();
			request.onload = function(event) {
				if (request.status == 200) {
					var xml = request.responseXML;
					var rootE = xml.getElementsByTagName('testxml');
					var output = "";
					for (var i = 1; i < rootE[0].childNodes.length; i += 2)
						output += "<h2>"
								+ rootE[0].childNodes[i].firstChild.nodeValue
								+ "</h2>";
					document.body.innerHTML += output;
				}
			};
			request.open('GET', 'content/testxml.xml', true);
			request.send();
		};
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
<h1>JavaScript로 구현하는 Ajax 프로그램-JSON</h1>
<hr>
<script>
window.onload = function() {
	var request = new XMLHttpRequest();
	request.onload = function() {
	    if(request.status == 200) {
				var str = request.responseText;
				alert(str);
				var jsObj = JSON.parse(str);
				alert(jsObj);
				console.log(jsObj);
				var output = "";				
				for(var i in jsObj)
					output += "<h2>"+ jsObj[i] +"</h2>";
				document.body.innerHTML += output;
		}		
	}
	request.open("GET", "content/testjson.txt", true);
	request.send();
}
</script>
</body>
</html>


<!DOCTYPE html>
<html>
    <head>
     <meta charset='utf-8'>
     <title>New Web Project</title>
     <script>	
     window.onload = function() {
 		var request = new XMLHttpRequest();
 		request.onload = function(event) {
 			if (request.status == 200) {
 				//var str = request.responseText;

                var str = request.responseXML;

 				var target = document.getElementById('output');
 				target.innerHTML = str;
 			}
 		};
 		request.open('GET', 'http://ws.bus.go.kr/api/rest/busRouteInfo/getBusRouteList?ServiceKey=%2BjzsSyNtwmcqxUsGnflvs3rW2oceFvhHR8AFkM3ao%2Fw50hwHXgGyPVutXw04uAXvrkoWgkoScvvhlH7jgD4%2FRQ%3D%3D&strSrch=402', true);
   		request.send();
 	};
		
     </script>
    </head>
    <body>
        <h1 style="text-align : center">공공DB에서 가져오는 360번의 버스 정보입니다.</h1>
        <hr>
        <div id="output" style="width:350px; margin : 10px auto"></div>
    </body>
</html>


<!DOCTYPE html>
<html>
    <head>
     <meta charset='utf-8'>
     <title>New Web Project</title>
     <script>	
     window.onload = function() {
 		var request = new XMLHttpRequest();
 		request.onload = function(event) {
 			if (request.status == 200) {
 				var str = request.responseText;
 				var obj = JSON.parse(str);
 				var tree = Number(obj.octastatapi367.row[0].EUNHAENGNAMU);
 				var info =  "서울시의 은행나무는 총 "+tree.toLocaleString()+"그루 입니다."
 				var target = document.getElementById('output');
 				target.innerHTML = info;
 			}
 		};
 	    request.open('GET', 'http://openapi.seoul.go.kr:8088/5772534170756e69313030444563795a/json/octastatapi367/1/5/', true);
 		request.send();
 	};
		
     </script>
    </head>
    <body>
        <h1 style="text-align : center">서울시의 가로수 정보입니다.</h1>
        <div id="output" style="width:350px; margin : 10px auto"></div>
    </body>
</html>


<!DOCTYPE html>
<html>
    <head>
     <meta charset='utf-8'>
     <title>New Web Project</title>
     <script>	
     window.onload = function() {
 		var request = new XMLHttpRequest();
 		request.onload = function(event) {
 			if (request.status == 200) {
 					var str = request.responseText;
 				var obj = JSON.parse(str);
                var total_count = obj.LampScpgmtb.row.length;
                var centerName = "시립서대문청소년센터";
                var program = [];
                for(var i=0; i < total_count; i++) {
                    if(obj.LampScpgmtb.row[i].UP_NM == centerName) {
                        program.push(obj.LampScpgmtb.row[i].PGM_NM)
                    }
                }
 				var info =  "<h3>"+centerName+"의 프로그램 정보</h3><ul>";
 				for(var i in program)
 				    info += "<li>"+program[i]+"</li>";
 				 info += "</ul>";
 				var target = document.getElementById('output');
 				target.innerHTML = info;
 			}
 		};
 		request.open('GET', 'http://openapi.seoul.go.kr:8088/796143536a756e69313134667752417a/json/LampScpgmtb/1/1000/', true);
      	request.send();
 	};
		
     </script>
    </head>
    <body>
        <h1 style="text-align : center">프로그램 정보</h1>
        <hr>
        <div id="output" style="width:350px; margin : 10px auto"></div>
    </body>
</html>
















```



### - 실습

```python

```

