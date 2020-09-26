

# Day2

> geocoding, geolocation, ggmap

### - 교육내용

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
</head>
<body>
	<h1>주소와 좌표 변환 프로그램</h1>
	<button onclick="addToCoord();">주소를 좌표로</button>
	<button onclick="coordToAddr();">다시 주소로</button>
	<script>
	var latlng;
		function addToCoord() {
			var address = prompt("주소를입력하세요");
			var lat;
			var lng;
			if (address) {
				$.getJSON("https://maps.googleapis.com/maps/api/geocode/json?key=AIzaSyDy81EbO46BRSnX1DOgg_F84bhsdbku2z4&address="+encodeURIComponent(address), function(data) {
					lat = data.results[0].geometry.location.lat;
					lng = data.results[0].geometry.location.lng;
					alert("좌표로 : " + lat + ":" + lng);		
					latlng = encodeURIComponent(lat+","+lng);											
				});		
				
			}
		}
	    function coordToAddr() {
	    	$.getJSON("https://maps.googleapis.com/maps/api/geocode/json?key=AIzaSyDy81EbO46BRSnX1DOgg_F84bhsdbku2z4&latlng="+latlng, function(data) {
				alert("다시 주소로 : " + data.results[0].formatted_address);
			});
	    }
	</script>
</body>
</html>

<!DOCTYPE html>
<html>
<head>
    <meta charset='utf-8'>
</head>
<body>
<p id="demo">위치정보를 추출하려면 실행 버튼을 클릭하세요:</p>
<button onclick="getLocation()">실행</button>
<script>
      var x=document.getElementById("demo");
	  function getLocation() {
         if (navigator.geolocation) {
            navigator.geolocation.getCurrentPosition(showPosition,showError);
         }
         else{x.innerHTML=" 이 브라우저는 geolocation을 지원하지 않습니다.";}
      }
      function showPosition(position) {
          x.innerHTML="위도: " + position.coords.latitude + "<br />경도: " + position.coords.longitude;       
      }
      function showError(error) {
         switch(error.code) {
            case error.PERMISSION_DENIED:
                x.innerHTML="사용자가 위치 기능 사용을 거부했습니다."
                break;
            case error.POSITION_UNAVAILABLE:
                x.innerHTML="위치를 구할 수 없습니다.";
                break;
            case error.TIMEOUT:
                x.innerHTML="사용자가 위치 기능 사용을 거부했습니다.";
                break;
            case error.UNKNOWN_ERROR:
                x.innerHTML="기타 에러";
         }
      }

</script>
</body>
</html>



<!DOCTYPE html>
<html>
  <head>
  	<meta charset='utf-8'>
    <title>Simple Map</title>
     <script src="https://maps.googleapis.com/maps/api/js?key=AIzaSyDy81EbO46BRSnX1DOgg_F84bhsdbku2z4" ></script>
    <style type="text/css">
       #map {
        height: 600px;
        width: 100%; 
      }
    </style>   
  </head>
  <body>
    <h1>구글 지도 출력</h1>
    <hr>
    <div id="map"></div>
     <script>
		var dom = document.getElementById("map");
		if(dom) {
			new google.maps.Map(dom, {
            	center: { lat: 37.5096357, lng: 127.0555218},
            	zoom: 20
          	});
        }     
    </script>
  </body>
</html>

<!DOCTYPE html>
<html>
  <head>
  	<meta charset='utf-8'>
    <title>Simple Map</title>
     <script src="https://maps.googleapis.com/maps/api/js?key=AIzaSyDy81EbO46BRSnX1DOgg_F84bhsdbku2z4" ></script>
    <style type="text/css">
       #map {
        height: 600px;
        width: 100%; 
      }
    </style>   
  </head>
  <body>
    <h1>구글 지도 출력</h1>
    <hr>
    <div id="map"></div>
     <script>
		var dom = document.getElementById("map");
		if(dom) {
			var latlng = { lat: 37.5096357, lng: 127.0555218}
			var map = new google.maps.Map(dom, {
            	center: latlng,
            	zoom: 16
          	});
			new google.maps.Marker({position: latlng, map: map})
        }     
    </script>
  </body>
</html>


<!DOCTYPE html>
<html>
  <head>
  	<meta charset='utf-8'>
    <title>Simple Map</title>
     <script src="https://maps.googleapis.com/maps/api/js?key=AIzaSyDy81EbO46BRSnX1DOgg_F84bhsdbku2z4" ></script>
    <style type="text/css">
       #map {
        height: 600px;
        width: 100%; 
      }
    </style>   
  </head>
  <body>
    <h1>구글 지도 출력</h1>
    <hr>
    <div id="map"></div>
     <script>
		var dom = document.getElementById("map");
		if(dom) {
			var latlng = { lat: 37.5096357, lng: 127.0555218}
			var map = new google.maps.Map(dom, {
            	center: latlng,
            	zoom: 16
          	});
			var marker = new google.maps.Marker({position: latlng, map: map});
			
			var contentString = "<h3>우리가 학습하는 곳이에요ㅎㅎㅎ<img src='../images/clover.png' width='20'></h3>";
			
			var infowindow = new google.maps.InfoWindow({
			    content: contentString
			});
			
			marker.addListener('click', function() {
			    infowindow.open(map, marker);
			});
        }     
    </script>
  </body>
</html>


<!DOCTYPE html>
<html>
<head>
<meta charset='utf-8'>
<title>Simple Map</title>
<script
	src="https://maps.googleapis.com/maps/api/js?key=AIzaSyDy81EbO46BRSnX1DOgg_F84bhsdbku2z4"></script>
<style type="text/css">
#map {
	height: 600px;
	width: 100%;
}
</style>
</head>
<body>
	<h1>구글 지도 출력</h1>
	<hr>
	<div id="map" style="width: 800px; height: 600px;"></div>
	<script> 
			window.onload = function() {
				var dom = document.getElementById("map");
				// html5 에서 추가된 geolocation 객체를 사용하여 현재 이 시스템이 존재하는 위치정보(위도,경도) 추출
				navigator.geolocation.getCurrentPosition(function(position) {
					var latlng = { lat: position.coords.latitude, lng: position.coords.longitude }
					var map = new google.maps.Map(dom, {
			           	center: latlng,
			           	zoom: 16
			       	});
						
					var marker = new google.maps.Marker({position: latlng, map: map});
						
					var contentString =
				       "<div><h2 style='color:red;'>JavaScript와 GoogleMap 의 세계로......</h2><hr>우리는 이곳에서<br>HTML, CSS, JavaScript를  공부합니다.</div>";
						
					var infowindow = new google.maps.InfoWindow({
					    content: contentString
					});
						
					marker.addListener('click', function() {
					    infowindow.open(map, marker);
					});
				});
		  };
        </script>
</head>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
<meta charset='utf-8'>
<title>Simple Map</title>
<script
	src="https://maps.googleapis.com/maps/api/js?key=AIzaSyDy81EbO46BRSnX1DOgg_F84bhsdbku2z4"></script>
<style type="text/css">
#map {
	height: 600px;
	width: 100%;
}
</style>
</head>
<script>
	var dom;
	var addr;
	function inputaddress() {
		addr = window.prompt("주소를 입력하세요");
		var url= 'https://maps.googleapis.com/maps/api/geocode/json?key=AIzaSyDy81EbO46BRSnX1DOgg_F84bhsdbku2z4&address='
							+ encodeURIComponent(addr)
					
	   	var request = new XMLHttpRequest();
		request.onload = function(event) {
			if (request.status == 200) {
				var obj = JSON.parse(request.responseText);
				lat = obj.results[0].geometry.location.lat;
				lng = obj.results[0].geometry.location.lng;
				dom.innerHTML = '';
				googlemap(lat, lng);
			}
		};
		request.open('GET', url, true);
		request.send();
	}
	
	function googlemap(latp, lngp) {
		var latlng = { lat: latp, lng: lngp }
		var map = new google.maps.Map(dom, {
	       	center: latlng,
	       	zoom: 16
	   	});
			    
	    var image = {
			  url: '/edu/images/duke.png',
			  size: new google.maps.Size(50, 60),
			  origin: new google.maps.Point(0, 0),
			  anchor: new google.maps.Point(17, 34),
			  scaledSize: new google.maps.Size(25, 25)
		};
						
		var marker = new google.maps.Marker({position: latlng, icon : image, map: map});
		
		
						
		var contentString =
				       "<h2 style='color:red;'>" + addr + "("+lat+":"+lng+")</h2>";
						
		var infowindow = new google.maps.InfoWindow({
		    content: contentString
		});
						
		marker.addListener('click', function() {
		    infowindow.open(map, marker);
		});
	}

	function clickme() {
		dom = document.getElementById('map');
		document.getElementById('btn').onclick = inputaddress;
	}
	window.onload = clickme;
</script>
</head>
<body>
	<h1>주소를 입력받아 지도를 출력하는 프로그램</h1>
	<button id="btn">주소 입력</button>
	<br>
	<br>
	<div id="map" style="width:700px; height:450px;"></div>
</body>
</html>

<!DOCTYPE html>
<html>
<head>
<meta charset='utf-8'>
<title>Simple Map</title>
<script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
<script
	src="https://maps.googleapis.com/maps/api/js?key=AIzaSyDy81EbO46BRSnX1DOgg_F84bhsdbku2z4"></script>
<style type="text/css">
#map {
	height: 600px;
	width: 100%;
}
</style>
</head>
<script>
	let dom;
	let addr;
	function inputaddress() {
		addr = window.prompt("주소를 입력하세요");
		const url= 'https://maps.googleapis.com/maps/api/geocode/json?key=AIzaSyDy81EbO46BRSnX1DOgg_F84bhsdbku2z4&address='
							+ encodeURIComponent(addr)
					
	   	$.getJSON(url, function(obj) {
				const lat = obj.results[0].geometry.location.lat;
				const lng = obj.results[0].geometry.location.lng;
				$('#map').empty();
				googlemap(lat, lng);
			}
		);
	}
	
	function googlemap(latp, lngp) {
		var latlng = { lat: latp, lng: lngp }
		var map = new google.maps.Map(document.getElementById("map"), {
	       	center: latlng,
	       	zoom: 16
	   	});
			    
	    var image = {
			  url: '/edu/images/duke.png',
			  size: new google.maps.Size(50, 60),
			  origin: new google.maps.Point(0, 0),
			  anchor: new google.maps.Point(17, 34),
			  scaledSize: new google.maps.Size(25, 25)
		};
						
		var marker = new google.maps.Marker({position: latlng, icon : image, map: map});

		var contentString =
				       "<h2 style='color:red;'>" + addr + "("+latp+":"+lngp+")</h2>";
						
		var infowindow = new google.maps.InfoWindow({
		    content: contentString
		});
		marker.addListener('click', function() {
		    infowindow.open(map, marker);
		});
	}

	$(function () {
		$('#btn').click(inputaddress);
	});
</script>
</head>
<body>
	<h1>주소를 입력받아 지도를 출력하는 프로그램</h1>
	<button id="btn">주소 입력</button>
	<br>
	<br>
	<div id="map" style="width:700px; height:450px;"></div>
</body>
</html>
```
