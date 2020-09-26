

# Day1

> Ajax&jQuery

### - 교육내용

```html
<!DOCTYPE html>
<html>
<head>
<meta charset='utf-8'>
<title>New Web Project</title>
<script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
<script>        
$(document).ready( function() {
   $.ajax('content/sample.xml', {
      success :  function(data) {                    
        $(data).find('testxml').each(function() { 
          $('body').append("<h1>"+$(this).find('name').text() + '</h1>');
          $('body').append("<h1>"+$(this).find('age').text() + '</h1>');
          $('body').append("<h1>"+$(this).find('kind').text() + '</h1>');
        });
      },
      error : function(xhr, textStatus, errorThrown) {
      	alert("오류발생1 : " + textStatus)
      	alert("원인1 : " + errorThrown)
      }
    });
});
</script>
</head>
<body>
	<h1>jQuery 로 구현하는 AJAX 프로그램  - XML</h1>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
<meta charset='utf-8'>
<title>New Web Project</title>
<script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
<script>        
$(document).ready( function() {
   $.ajax('content/sample.xml')
   .done(function(data) {
        $(data).find('testxml').each(function() {
          $('body').append("<h1>"+$(this).find('name').text() + '</h1>');
          $('body').append("<h1>"+$(this).find('age').text() + '</h1>');
          $('body').append("<h1>"+$(this).find('kind').text() + '</h1>');
        });
   }).fail(function(xhr, textStatus, errorThrown) {
      	alert("오류발생2 : " + textStatus)
      	alert("원인2 : " + errorThrown)
    }).always(function() {
      	console.log("항상 수행요....")
    });
});
</script>
</head>
<body>
	<h1>jQuery 로 구현하는 AJAX 프로그램  - XML</h1>
</body>
</html>


<!DOCTYPE html>
<html>
<head> 
<meta charset='utf-8'>
<title>New Web Project</title>
<script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
<script>		
$(document).ready(function() {
	$.ajax('content/samplejson.txt', {
		success :  function(data) {
			alert(data);
		  	var result = JSON.parse(data);
		    $.each(result, function(key, value) { 
               $('body').append("<h1>" +value + '</h1>');
            });
		},
       error : function(xhr, textStatus, errorThrown) {
      	alert("오류발생 : " + textStatus)
      	alert("원인 : " + errorThrown)
       }
	});
});
</script>
</head>
<body>
	<h1>jQuery 로 구현하는 AJAX 프로그램 1 - JSON</h1>
</body>
</html>


<!DOCTYPE html>
<html>
<head> 
<meta charset='utf-8'>
<title>New Web Project</title>
<script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
<script>		
$(document).ready(function() {
	$.ajax('content/samplejson.txt')
	.done(function(data) {
			//alert(data);
		  	var result = JSON.parse(data);
		    $.each(result, function(key, value) { 
               $('body').append("<h1>" +value + '</h1>');
            });
		});
});
</script>
</head>
<body>
	<h1>jQuery 로 구현하는 AJAX 프로그램 1 - JSON</h1>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
<meta charset='utf-8'>
<title>New Web Project</title>
<script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
<script>
$(document).ready(function () {
   	$.getJSON('content/samplejson.txt',  function(data) {
		  $.each(data, function(key, value) { 
		        $('body').append("<h1>" +value + '</h1>');
		  });
	});
});
</script>
</head>
<body>
	<h1>jQuery 로 구현하는 AJAX 프로그램  2 - JSON</h1>
</body>
</html>

<!DOCTYPE html>
<html>
<head>
<meta charset='utf-8'>
<title>XMLHttpRequest</title>
<script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
<script>
$(document).ready(function () {
   // Ajax 이벤트 연결   
   $(document).ajaxComplete(function () {             
        alert('AjaxComplete');
   }).ajaxError(function () {               
       	alert('AjaxError');
   }).ajaxSend(function () {
       	alert('AjaxSend');
   }).ajaxSuccess(function () {
       	alert('AjaxSuccess');
   }).ajaxStart(function () {
      	alert('AjaxStart');
   });
   // Ajax 수행
   $('#wrap').load('content/samplejson.txt');
});
</script>
</head>
<body> 
	<h1>AJAX 수행</h1>
	<hr>
    <h2 id="wrap"></h2>
</body>
</html>


<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
<script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
<script>
$(document).ready(function() {
	$.ajax({
        type : 'get',
        url : 'http://www.kobis.or.kr/kobisopenapi/webservice/rest/boxoffice/searchDailyBoxOfficeList.json?key=75474bdfc6c0a4eb738939dd66c101b5&targetDt=20200730',
        dataType : 'json',
        error: function(xhr, status, error){
            alert(error);
        },
        success : function(json){
            console.log(json)
            $('div').html(JSON.stringify(json))
            console.log(json.boxOfficeResult.dailyBoxOfficeList[0].movieNm)
            
            $.each(json.boxOfficeResult.dailyBoxOfficeList[0], function(key, value) { 
		        $('div').append("<h1>" +value + '</h1>');
            });

        }
    });
});
</script>
</head>
<body>
	<h1>일별 박스 오피스</h1>
    <hr>
    <div></div>
</body>
</html>

<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
<script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
<script>
$(document).ready(function() {
	$.ajax({
        type : 'get',
        url : 'https://dapi.kakao.com/v2/search/image?query=알라딘&sort=accuracy&page=1&size=5',
        dataType : 'json',
        beforeSend : function(xhr){
            xhr.setRequestHeader("Authorization", "KakaoAK f613363f755c6ba58d1e8d2378c8523a");
        },
        error: function(xhr, status, error){
            alert(error);
        },
        success : function(json){
            console.log(json)
            console.log(JSON.stringify(json))
            console.log(json.documents[0].thumbnail_url)
            const dom = document.getElementsByTagName("img")[0];
            dom.src = json.documents[0].thumbnail_url;
        },
    });
});
</script>
</head>
<body>
	<h1>카카오에서 이미지 검색하기</h1>
    <hr>
    <img src="" width="100">
</body>
</html>


<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.5.0/css/bootstrap.min.css">
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.16.0/umd/popper.min.js"></script>
    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.5.0/js/bootstrap.min.js"></script>    
    <script>
    $(document).ready(function() {
        $.ajax({
            type : 'get',
            url : 'http://www.kobis.or.kr/kobisopenapi/webservice/rest/boxoffice/searchDailyBoxOfficeList.json?key=75474bdfc6c0a4eb738939dd66c101b5&targetDt=20200730',
            dataType : 'json',
            error: function(xhr, status, error){
                alert(error);
            },
            success : function(json){
                console.log(json)
                $('div:last').html(JSON.stringify(json))
                console.log(json.boxOfficeResult.dailyBoxOfficeList[0].movieNm)
                
                    $.each(json.boxOfficeResult.dailyBoxOfficeList[0], function(key, value) { 
                        $('div:last').append("<h1>" +value + '</h1>');
                    });

            }
        });
    });
    </script>
</head>
<body>
    <div class="jumbotron text-center">
        <h1>일별 박스 오피스</h1>
        <p>학교 종이 땡땡땡 어서모이자~</p>
    </div>    

    <hr>

    <div class="container">
        <h2>Button Styles</h2>
        <button type="button" class="btn">Basic</button>
        <button type="button" class="btn btn-primary">Primary</button>
        <button type="button" class="btn btn-secondary">Secondary</button>
        <button type="button" class="btn btn-success">Success</button>
        <button type="button" class="btn btn-info">Info</button>
        <button type="button" class="btn btn-warning">Warning</button>
        <button type="button" class="btn btn-danger">Danger</button>
        <button type="button" class="btn btn-dark">Dark</button>
        <button type="button" class="btn btn-light">Light</button>
        <button type="button" class="btn btn-link">Link</button>      
      </div>


    <div class="container">
        <table class="table table-dark table-hover">
          <thead>
            <tr>
              <th>Firstname</th>
              <th>Lastname</th>
              <th>Email</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>John</td>
              <td>Doe</td>
              <td>john@example.com</td>
            </tr>
            <tr>
              <td>Mary</td>
              <td>Moe</td>
              <td>mary@example.com</td>
            </tr>
            <tr>
              <td>July</td>
              <td>Dooley</td>
              <td>july@example.com</td>
            </tr>
          </tbody>
        </table>
      </div>

    <div></div>
</body>
</html>


<!doctype html>
<html lang="ko">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
  <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css" integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm" crossorigin="anonymous">
  <style>
        nav, section {
            margin : 10px;
        }
  </style>
  <title>Hello, world!</title>
</head>
<body>
<header class="jumbotron text-center">
  <h1>일별 박스 오피스</h1>
  <p>영화관 입장권 통합 전산망 오픈  API 를 AJAX 기술로 활용합니다.</p>
</header>
<nav>
  <button type="button" class="btn btn-outline-primary" onclick="displayMovieRanking(1)">1일전</button>
  <button type="button" class="btn btn-outline-info" onclick="displayMovieRanking(2)">2일전</button>
  <button type="button" class="btn btn-outline-success" onclick="displayMovieRanking(3)">3일전</button>
</nav>
<section>
  <table class="table table-hover">
    <thead>
    <tr>
      <th scope="col">영화명</th>
      <th scope="col">해당일 관객수</th>
      <th scope="col">누적 관객수</th>
      <th scope="col">스크린수</th>
    </tr>
    </thead>
    <tbody>
    </tbody>
  </table>
</section>
<!-- Optional JavaScript -->
<!-- jQuery first, then Popper.js, then Bootstrap JS -->
<script src="https://code.jquery.com/jquery-3.2.1.slim.min.js" integrity="sha384-KJ3o2DKtIkvYIK3UENzmM7KCkRr/rE9/Qpg6aAZGJwFDMVNA/GpGFF93hXpG5KkN" crossorigin="anonymous"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.12.9/umd/popper.min.js" integrity="sha384-ApNbgh9B+Y1QKtv3Rn7W3mgPxhU9K/ScQsAP7hUibX39j7fakFPskvXusvfa0b4Q" crossorigin="anonymous"></script>
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/js/bootstrap.min.js" integrity="sha384-JZR6Spejh4U02d8jOt6vLEHfe/JQGiRRSQQxSfFWpi1MquVdAyjUar5+76PVCmYl" crossorigin="anonymous"></script>
<script src="http://code.jquery.com/jquery-2.1.3.min.js"></script>
<script>
function getFormatDate(date){
    var year = date.getFullYear();
    var month = (1 + date.getMonth());
    month = month >= 10 ? month : '0' + month;
    var day = date.getDate();
    day = day >= 10 ? day : '0' + day;
    return  year+month+day;
}
function displayMovieRanking(n) {
  const today = new Date();
  const d = today.getTime() - (n*24*60*60*1000);
  const targetday = new Date(d);
  const targetDt = getFormatDate(targetday);
  alert(targetDt)
  $.getJSON('http://www.kobis.or.kr/kobisopenapi/webservice/rest/boxoffice/searchDailyBoxOfficeList.json?key=75474bdfc6c0a4eb738939dd66c101b5&targetDt='+targetDt,
          function(jsonObj){
              var dom = $('tbody');
              let content="";
              for(var i=0; i < 5; i++) {
                content += "<tr><th scope='row'>"+jsonObj.boxOfficeResult.dailyBoxOfficeList[i].movieNm +
                                        "</th><td>"+jsonObj.boxOfficeResult.dailyBoxOfficeList[i].audiCnt+
                                        "</td><td>"+jsonObj.boxOfficeResult.dailyBoxOfficeList[i].audiAcc+
                                        "</td><td>"+jsonObj.boxOfficeResult.dailyBoxOfficeList[i].scrnCnt+"</td></tr>"
              }
              dom.html(content);
              alert(jsonObj.boxOfficeResult.dailyBoxOfficeList[0].movieNm)
          }
    );
}
</script>
</body>
</html>


<!doctype html>
<html lang="ko">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
  <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css" integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm" crossorigin="anonymous">
  <style>
        nav, section {
            margin : 10px;
        }
  </style>
  <title>Hello, world!</title>
</head>
<body>
<header class="jumbotron text-center">
  <h1>일별 박스 오피스</h1>
  <p>영화관 입장권 통합 전산망 오픈  API 를 AJAX 기술로 활용합니다.</p>
</header>
<nav>
  <button type="button" class="btn btn-outline-primary" onclick="displayMovieRanking(1)">1일전</button>
  <button type="button" class="btn btn-outline-info" onclick="displayMovieRanking(2)">2일전</button>
  <button type="button" class="btn btn-outline-success" onclick="displayMovieRanking(3)">3일전</button>
</nav>
<section>
  <table class="table table-hover">
    <thead>
    <tr>
      <th scope="col">영화썸네일</th>
      <th scope="col">영화명</th>
      <th scope="col">해당일 관객수</th>
      <th scope="col">누적 관객수</th>
      <th scope="col">스크린수</th>
    </tr>
    </thead>
    <tbody>
    </tbody>
  </table>
</section>

<!-- Optional JavaScript -->
<!-- jQuery first, then Popper.js, then Bootstrap JS -->
<script src="https://code.jquery.com/jquery-3.2.1.slim.min.js" integrity="sha384-KJ3o2DKtIkvYIK3UENzmM7KCkRr/rE9/Qpg6aAZGJwFDMVNA/GpGFF93hXpG5KkN" crossorigin="anonymous"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.12.9/umd/popper.min.js" integrity="sha384-ApNbgh9B+Y1QKtv3Rn7W3mgPxhU9K/ScQsAP7hUibX39j7fakFPskvXusvfa0b4Q" crossorigin="anonymous"></script>
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/js/bootstrap.min.js" integrity="sha384-JZR6Spejh4U02d8jOt6vLEHfe/JQGiRRSQQxSfFWpi1MquVdAyjUar5+76PVCmYl" crossorigin="anonymous"></script>
<script src="http://code.jquery.com/jquery-2.1.3.min.js"></script>
<script>
function getFormatDate(date){
    var year = date.getFullYear();
    var month = (1 + date.getMonth());
    month = month >= 10 ? month : '0' + month;
    var day = date.getDate();
    day = day >= 10 ? day : '0' + day;
    return  year+month+day;
}
function displayMovieRanking(n) {
  const today = new Date();
  const d = today.getTime() - (n*24*60*60*1000);
  let targetday = new Date(d);
  const targetDt = getFormatDate(targetday);
   let thumbnail = [];
   let movieNm = [];
   let audiCnt  = [];
   let audiAcc  = [];
   let scrnCnt = [];
   const dom = $('tbody');
   let content = "";
 let aa = $.ajax('http://www.kobis.or.kr/kobisopenapi/webservice/rest/boxoffice/searchDailyBoxOfficeList.json?key=75474bdfc6c0a4eb738939dd66c101b5&targetDt='+targetDt)
    .done(function(jsonObj){
              for(let i=0; i < 10; i++) {
                movieNm[i] = jsonObj.boxOfficeResult.dailyBoxOfficeList[i].movieNm;
                audiCnt[i] = jsonObj.boxOfficeResult.dailyBoxOfficeList[i].audiCnt;
                audiAcc[i] = jsonObj.boxOfficeResult.dailyBoxOfficeList[i].audiAcc;
                scrnCnt[i] = jsonObj.boxOfficeResult.dailyBoxOfficeList[i].scrnCnt;
               }
               console.log("111"+thumbnail);console.log("111"+movieNm); console.log("111"+audiCnt); console.log("111"+audiAcc); console.log("111"+scrnCnt)
     }).always(function() {
            console.log("222"+thumbnail);console.log("222"+movieNm); console.log("222"+audiCnt); console.log("222"+audiAcc); console.log("222"+scrnCnt)
              for(let i=0; i < 10; i++) {
                $.ajax({
               type : 'get',
               url : 'https://dapi.kakao.com/v2/search/image?query='+encodeURIComponent(movieNm[i])+'&sort=accuracy&page=1&size=5',
               async:false,
               dataType : 'json',
               beforeSend : function(xhr){
                   xhr.setRequestHeader("Authorization", "KakaoAK f613363f755c6ba58d1e8d2378c8523a");
               }}).done(function(json){
                   thumbnail[i] = json.documents[0].thumbnail_url;
                   console.log(333+thumbnail[i] + ":::"+ i)
               }).always(function() {
                console.log("333"+thumbnail);console.log("333"+audiCnt); console.log("333"+audiAcc); console.log("333"+scrnCnt)
                      content += "<tr><td scope='row'><img src='"+thumbnail[i]+"' width='50'>"+
                             "</td><td>"+ movieNm[i] +
                             "</td><td>"+ audiCnt[i].toLocaleString() +
                             "</td><td>"+ audiAcc[i].toLocaleString() +
                             "</td><td>"+ scrnCnt[i] +"</td></tr>"
                 }).always(function() {
                              dom.html(content);
                             console.log("555"+thumbnail);console.log("555"+movieNm); console.log("555"+audiCnt); console.log("555"+audiAcc); console.log("555"+scrnCnt);
               });
               }
            });
}

</script>

</body>
</html>
```



### - 실습

```python

```

