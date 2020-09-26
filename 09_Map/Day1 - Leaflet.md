

# Day1

> Leaflet

### - 교육내용

```html
<html>
<head>
    <title>A Leaflet map!</title>
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.5.1/dist/leaflet.css"
          integrity="sha512-xwE/Az9zrjBIphAcBb3F6JVqxf46+CDLwfLMHloNu6KEQCAWi6HcDUbeOfBIptF7tcCzusKFjFw2yuvEpDL9wQ=="
          crossorigin=""/>
    <script src="https://unpkg.com/leaflet@1.5.1/dist/leaflet.js"
            integrity="sha512-GffPMF3RvMeYyc1LWMHtK8EbPv0iNZ8/oTtHPx9/cc2ILxQ+u905qIwdpULaqDkyBKgOaB57QTMg7ztg8Jm2Og=="
            crossorigin=""></script>
    <style>
    #mapid{ height: 100% }

    </style>
</head>
<body>
<div id="mapid"></div>
<script>
  // initialize the map
  var mymap = L.map('mapid').setView([37.5096357, 127.0555218], 20);

  // load a tile layer
  L.tileLayer('https://api.tiles.mapbox.com/v4/{id}/{z}/{x}/{y}.png?access_token=pk.eyJ1IjoibWFwYm94IiwiYSI6ImNpejY4NXVycTA2emYycXBndHRqcmZ3N3gifQ.rJcFIG214AriISLbB6B5aw', {
		maxZoom: 18,
		attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, ' +
			'<a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, ' +
			'Imagery <a href="https://www.mapbox.com/">Mapbox</a>',
		id: 'mapbox.streets'
	}).addTo(mymap);

</script>
</body>
</html>

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.5.1/dist/leaflet.css"
   integrity="sha512-xwE/Az9zrjBIphAcBb3F6JVqxf46+CDLwfLMHloNu6KEQCAWi6HcDUbeOfBIptF7tcCzusKFjFw2yuvEpDL9wQ=="
   crossorigin=""/>
<script src="https://unpkg.com/leaflet@1.5.1/dist/leaflet.js"
   integrity="sha512-GffPMF3RvMeYyc1LWMHtK8EbPv0iNZ8/oTtHPx9/cc2ILxQ+u905qIwdpULaqDkyBKgOaB57QTMg7ztg8Jm2Og=="
   crossorigin=""></script>
  
</head>
<body>
<div id="mapid" style="width: 600px; height: 400px;"></div>
<script>
    //서울시청 위도,경도 : 37.5662952,126.97794509999994
	var mymap = L.map('mapid').setView([37.566, 126.978], 18);

	L.tileLayer('https://api.tiles.mapbox.com/v4/{id}/{z}/{x}/{y}.png?access_token=pk.eyJ1IjoibWFwYm94IiwiYSI6ImNpejY4NXVycTA2emYycXBndHRqcmZ3N3gifQ.rJcFIG214AriISLbB6B5aw', {
		maxZoom: 18,
		attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, ' +
			'<a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, ' +
			'Imagery <a href="https://www.mapbox.com/">Mapbox</a>',
		id: 'mapbox.streets'
	}).addTo(mymap);

	L.marker([37.566, 126.978]).addTo(mymap)
		.bindPopup("<b>안녕하세요! 난 팝업이야..</b><br />여기가 서울시청입니다...").openPopup();
	mymap.dragging.disable();
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
	display : inline-block;  
}
</style>
 <link rel="stylesheet" href="https://unpkg.com/leaflet@1.5.1/dist/leaflet.css"
   integrity="sha512-xwE/Az9zrjBIphAcBb3F6JVqxf46+CDLwfLMHloNu6KEQCAWi6HcDUbeOfBIptF7tcCzusKFjFw2yuvEpDL9wQ=="
   crossorigin=""/>
<script src="https://unpkg.com/leaflet@1.5.1/dist/leaflet.js"
   integrity="sha512-GffPMF3RvMeYyc1LWMHtK8EbPv0iNZ8/oTtHPx9/cc2ILxQ+u905qIwdpULaqDkyBKgOaB57QTMg7ztg8Jm2Og=="
   crossorigin=""></script>
  
</head>
<body>
<div id="mapid1" style="width: 600px; height: 400px;"></div>
<div id="mapid2" style="width: 600px; height: 400px;"></div>
<div id="mapid3" style="width: 600px; height: 400px;"></div>
<div id="mapid4" style="width: 600px; height: 400px;"></div>
<script>
	var mymap1 = L.map('mapid1', { center : [37.566, 126.978], zoom : 18});
	var mymap2 = L.map('mapid2').setView([37.566, 126.978], 1);
	var mymap3 = L.map('mapid3').setView([37.566, 126.978], 5);
	var mymap4 = L.map('mapid4').setView([37.566, 126.978], 10);

	L.tileLayer('https://api.tiles.mapbox.com/v4/{id}/{z}/{x}/{y}.png?access_token=pk.eyJ1IjoibWFwYm94IiwiYSI6ImNpejY4NXVycTA2emYycXBndHRqcmZ3N3gifQ.rJcFIG214AriISLbB6B5aw', {
		maxZoom: 18,
		attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, ' +
			'<a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, ' +
			'Imagery <a href="https://www.mapbox.com/">Mapbox</a>',
		id: 'mapbox.streets'
	}).addTo(mymap1);
	
	L.tileLayer('https://api.tiles.mapbox.com/v4/{id}/{z}/{x}/{y}.png?access_token=pk.eyJ1IjoibWFwYm94IiwiYSI6ImNpejY4NXVycTA2emYycXBndHRqcmZ3N3gifQ.rJcFIG214AriISLbB6B5aw', {
		maxZoom: 18,
		attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, ' +
			'<a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, ' +
			'Imagery <a href="https://www.m/* apbox.com/">Mapbox</a>',
		id: 'mapbox.streets'
	}).addTo(mymap2);
	
	L.tileLayer('https://api.tiles.mapbox.com/v4/{id}/{z}/{x}/{y}.png?access_token=pk.eyJ1IjoibWFwYm94IiwiYSI6ImNpejY4NXVycTA2emYycXBndHRqcmZ3N3gifQ.rJcFIG214AriISLbB6B5aw', {
		maxZoom: 18,
		attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, ' +
			'<a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, ' +
			'Imagery <a href="https://www.m/* apbox.com/">Mapbox</a>',
		id: 'mapbox.streets'
	}).addTo(mymap3); 
	
	L.tileLayer('https://api.tiles.mapbox.com/v4/{id}/{z}/{x}/{y}.png?access_token=pk.eyJ1IjoibWFwYm94IiwiYSI6ImNpejY4NXVycTA2emYycXBndHRqcmZ3N3gifQ.rJcFIG214AriISLbB6B5aw', {
		maxZoom: 18,
		attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, ' +
			'<a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, ' +
			'Imagery <a href="https://www.m/* apbox.com/">Mapbox</a>',
		id: 'mapbox.streets'
	}).addTo(mymap4); 

</script>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.5.1/dist/leaflet.css"
   integrity="sha512-xwE/Az9zrjBIphAcBb3F6JVqxf46+CDLwfLMHloNu6KEQCAWi6HcDUbeOfBIptF7tcCzusKFjFw2yuvEpDL9wQ=="
   crossorigin=""/>
<script src="https://unpkg.com/leaflet@1.5.1/dist/leaflet.js"
   integrity="sha512-GffPMF3RvMeYyc1LWMHtK8EbPv0iNZ8/oTtHPx9/cc2ILxQ+u905qIwdpULaqDkyBKgOaB57QTMg7ztg8Jm2Og=="
   crossorigin=""></script>
  
</head>
<body>
<div id="mapid" style="width: 800px; height: 500px;"></div>
<script>
	var mymap = L.map('mapid').setView([37.566, 126.978], 14);

	L.tileLayer('https://api.tiles.mapbox.com/v4/{id}/{z}/{x}/{y}.png?access_token=pk.eyJ1IjoibWFwYm94IiwiYSI6ImNpejY4NXVycTA2emYycXBndHRqcmZ3N3gifQ.rJcFIG214AriISLbB6B5aw', {
		maxZoom: 18,
		attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, ' +
			'<a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, ' +
			'Imagery <a href="https://www.mapbox.com/">Mapbox</a>',
		id: 'mapbox.streets'
	}).addTo(mymap);

	function clickMap(e) {
		 L.popup()	  
		    .setLatLng(e.latlng)
	        .setContent("여기를 클릭했슈!!!  " + e.latlng)
	        .openOn(mymap);
	}

	mymap.on('click', clickMap);

</script>
</body>
</html>



<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
 <link rel="stylesheet" href="https://unpkg.com/leaflet@1.5.1/dist/leaflet.css"
   integrity="sha512-xwE/Az9zrjBIphAcBb3F6JVqxf46+CDLwfLMHloNu6KEQCAWi6HcDUbeOfBIptF7tcCzusKFjFw2yuvEpDL9wQ=="
   crossorigin=""/>
<script src="https://unpkg.com/leaflet@1.5.1/dist/leaflet.js"
   integrity="sha512-GffPMF3RvMeYyc1LWMHtK8EbPv0iNZ8/oTtHPx9/cc2ILxQ+u905qIwdpULaqDkyBKgOaB57QTMg7ztg8Jm2Og=="
   crossorigin=""></script>
  
</head>
<body>
<div id="mapid" style="width: 800px; height: 500px;"></div>
<script>
	var mymap = L.map('mapid').setView([37.566, 126.978], 16);

	L.tileLayer('https://api.tiles.mapbox.com/v4/{id}/{z}/{x}/{y}.png?access_token=pk.eyJ1IjoibWFwYm94IiwiYSI6ImNpejY4NXVycTA2emYycXBndHRqcmZ3N3gifQ.rJcFIG214AriISLbB6B5aw', {
		maxZoom: 18,
		attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, ' +
			'<a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, ' +
			'Imagery <a href="https://www.mapbox.com/">Mapbox</a>',
		id: 'mapbox.streets'
	}).addTo(mymap);
	
	L.marker([37.566, 126.978]).addTo(mymap);
 
	L.circle([37.566, 126.978], 50, {
		color: 'red',
		fillColor: '#f03',
		fillOpacity: 0.4
	}).addTo(mymap).bindPopup("나는 원!");

	L.polygon([
		[37.5672, 126.9735],
		[37.5646, 126.9741],
		[37.5647, 126.9767],
		[37.5661, 126.9768]
	], {
		color: 'blue',
		fillColor: 'skyblue',
		fillOpacity: 0.4
	}).addTo(mymap).bindPopup("나는 다각형");
</script>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
 <link rel="stylesheet" href="https://unpkg.com/leaflet@1.5.1/dist/leaflet.css"
   integrity="sha512-xwE/Az9zrjBIphAcBb3F6JVqxf46+CDLwfLMHloNu6KEQCAWi6HcDUbeOfBIptF7tcCzusKFjFw2yuvEpDL9wQ=="
   crossorigin=""/>
<script src="https://unpkg.com/leaflet@1.5.1/dist/leaflet.js"
   integrity="sha512-GffPMF3RvMeYyc1LWMHtK8EbPv0iNZ8/oTtHPx9/cc2ILxQ+u905qIwdpULaqDkyBKgOaB57QTMg7ztg8Jm2Og=="
   crossorigin=""></script>
 <style>
 	b {
 		color : red;
 	}
 </style> 
</head>
<body>
<div id="mapid" style="width: 800px; height: 500px;"></div>
<script>
	var mymap = L.map('mapid').setView([37.5096357,127.0555218], 16);

	L.tileLayer('https://api.tiles.mapbox.com/v4/{id}/{z}/{x}/{y}.png?access_token=pk.eyJ1IjoibWFwYm94IiwiYSI6ImNpejY4NXVycTA2emYycXBndHRqcmZ3N3gifQ.rJcFIG214AriISLbB6B5aw', {
		maxZoom: 18,
		attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, ' +
			'<a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, ' +
			'Imagery <a href="https://www.mapbox.com/">Mapbox</a>',
		id: 'mapbox.streets'
	}).addTo(mymap);

	var myIcon = L.icon({
	    iconUrl: '/edu/images/duke.png',
	    iconSize: [30, 50]
	});
	var content = "<b>우리가 있는 곳!!</b> <img src='/edu/images/duke.png' width='20'><hr>여기가 멀티캠퍼스입니다...<br>우리는 6층 1호 강의장에서 공부합니다."
	L.marker([37.5096357,127.0555218], {icon: myIcon}).addTo(mymap).bindPopup(content);

</script>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
 <link rel="stylesheet" href="https://unpkg.com/leaflet@1.5.1/dist/leaflet.css"
   integrity="sha512-xwE/Az9zrjBIphAcBb3F6JVqxf46+CDLwfLMHloNu6KEQCAWi6HcDUbeOfBIptF7tcCzusKFjFw2yuvEpDL9wQ=="
   crossorigin=""/>
<script src="https://unpkg.com/leaflet@1.5.1/dist/leaflet.js"
   integrity="sha512-GffPMF3RvMeYyc1LWMHtK8EbPv0iNZ8/oTtHPx9/cc2ILxQ+u905qIwdpULaqDkyBKgOaB57QTMg7ztg8Jm2Og=="
   crossorigin=""></script>
  
</head>
<body>
<div id="mapid" style="width: 800px; height: 500px;"></div>
<script>
    //멀티캠퍼스 위도, 경도 : 37.5096357,127.0555218
	var mymap = L.map('mapid').setView([37.5096357,127.0555218], 16);

	L.tileLayer('https://api.tiles.mapbox.com/v4/{id}/{z}/{x}/{y}.png?access_token=pk.eyJ1IjoibWFwYm94IiwiYSI6ImNpejY4NXVycTA2emYycXBndHRqcmZ3N3gifQ.rJcFIG214AriISLbB6B5aw', {
		maxZoom: 18,
		attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, ' +
			'<a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, ' +
			'Imagery <a href="https://www.mapbox.com/">Mapbox</a>',
		id: 'mapbox.streets'
	}).addTo(mymap);

	var myIcon = L.icon({
	    iconUrl: '/edu/images/duke.png',
	    iconSize: [30, 50]
	});
	L.marker([37.5096357,127.0555218], {icon: myIcon}).addTo(mymap).bindTooltip("우리가 있는 곳!! <br>여기가 멀티캠퍼스입니다...", {direction: 'right', offset :[20,3]})
</script>



</body>
</html>



<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
 <link rel="stylesheet" href="https://unpkg.com/leaflet@1.5.1/dist/leaflet.css"
   integrity="sha512-xwE/Az9zrjBIphAcBb3F6JVqxf46+CDLwfLMHloNu6KEQCAWi6HcDUbeOfBIptF7tcCzusKFjFw2yuvEpDL9wQ=="
   crossorigin=""/>
<script src="https://unpkg.com/leaflet@1.5.1/dist/leaflet.js"
   integrity="sha512-GffPMF3RvMeYyc1LWMHtK8EbPv0iNZ8/oTtHPx9/cc2ILxQ+u905qIwdpULaqDkyBKgOaB57QTMg7ztg8Jm2Og=="
   crossorigin=""></script>
  
</head>
<body>
<div id="mapid" style="width: 800px; height: 500px;"></div>
<script>
    //멀티캠퍼스 위도, 경도 : 37.5096357,127.0555218
	var mymap = L.map('mapid').setView([37.5096357,127.0555218], 16);

	L.tileLayer('https://api.tiles.mapbox.com/v4/{id}/{z}/{x}/{y}.png?access_token=pk.eyJ1IjoibWFwYm94IiwiYSI6ImNpejY4NXVycTA2emYycXBndHRqcmZ3N3gifQ.rJcFIG214AriISLbB6B5aw', {
		maxZoom: 18,
		attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, ' +
			'<a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, ' +
			'Imagery <a href="https://www.mapbox.com/">Mapbox</a>',
		id: 'mapbox.streets'
	}).addTo(mymap);

	var myIcon = L.icon({
	    iconUrl: '/edu/images/duke.png',
	     iconSize: [30, 50]
	});
	
	var m1 = L.marker([37.5115, 127.0500], {icon: myIcon, title:"나 1번이야!!"});
	var m2 = L.marker([37.5094, 127.0503], {icon: myIcon, title:"나 2번이야!!"});
	var m3 = L.marker([37.5080, 127.0600], {icon: myIcon, title:"나 3번이야!!"});
	var m4 = L.marker([37.5110, 127.0590], {icon: myIcon, title:"나 4번이야!!"});
	var m5 = L.marker([37.5088, 127.0560], {icon: myIcon, title:"나 5번이야!!"});
	
	var group = L.layerGroup([m1, m2, m3, m4, m5])

	group.addTo(mymap);
</script>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
 <link rel="stylesheet" href="https://unpkg.com/leaflet@1.5.1/dist/leaflet.css"
   integrity="sha512-xwE/Az9zrjBIphAcBb3F6JVqxf46+CDLwfLMHloNu6KEQCAWi6HcDUbeOfBIptF7tcCzusKFjFw2yuvEpDL9wQ=="
   crossorigin=""/>
<script src="https://unpkg.com/leaflet@1.5.1/dist/leaflet.js"
   integrity="sha512-GffPMF3RvMeYyc1LWMHtK8EbPv0iNZ8/oTtHPx9/cc2ILxQ+u905qIwdpULaqDkyBKgOaB57QTMg7ztg8Jm2Og=="
   crossorigin=""></script>
  
</head>
<body>
<div id="mapid" style="width: 800px; height: 500px;"></div>
<script>
    //서울시청 위도,경도 : 37.5662952,126.97794509999994
	var mymap = L.map('mapid').setView([37.566, 126.978], 18);

	L.tileLayer('https://api.tiles.mapbox.com/v4/{id}/{z}/{x}/{y}.png?access_token=pk.eyJ1IjoibWFwYm94IiwiYSI6ImNpejY4NXVycTA2emYycXBndHRqcmZ3N3gifQ.rJcFIG214AriISLbB6B5aw', {
		maxZoom: 18,
		attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, ' +
			'<a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, ' +
			'Imagery <a href="https://www.mapbox.com/">Mapbox</a>',
		id: 'mapbox.streets-satellite'
	}).addTo(mymap);

	L.marker([37.566, 126.978]).addTo(mymap)
		.bindPopup("<b>안녕하세요! 난 팝업이야..</b><br />여기가 서울시청입니다...").openPopup();   

</script>
</body>
</html>

<html>
<head>
  <title>A Leaflet map!</title>
  <link rel="stylesheet" href="https://unpkg.com/leaflet@1.5.1/dist/leaflet.css"
   integrity="sha512-xwE/Az9zrjBIphAcBb3F6JVqxf46+CDLwfLMHloNu6KEQCAWi6HcDUbeOfBIptF7tcCzusKFjFw2yuvEpDL9wQ=="
   crossorigin=""/>
<script src="https://unpkg.com/leaflet@1.5.1/dist/leaflet.js"
   integrity="sha512-GffPMF3RvMeYyc1LWMHtK8EbPv0iNZ8/oTtHPx9/cc2ILxQ+u905qIwdpULaqDkyBKgOaB57QTMg7ztg8Jm2Og=="
   crossorigin=""></script>
  <style>
    #mapid{ height: 100% }
  </style>
</head>
<body>
	<div id="mapid" style="width: 800px; height: 500px;"></div>
  	<script>
  	var mymap = L.map('mapid').setView([37.566, 126.978], 12);

  	L.tileLayer('https://api.tiles.mapbox.com/v4/{id}/{z}/{x}/{y}.png?access_token=pk.eyJ1IjoibWFwYm94IiwiYSI6ImNpejY4NXVycTA2emYycXBndHRqcmZ3N3gifQ.rJcFIG214AriISLbB6B5aw', {
			maxZoom: 18,
			attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, ' +
			'<a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, ' +
			'Imagery <a href="https://www.mapbox.com/">Mapbox</a>',
			id: 'mapbox.streets'
	}).addTo(mymap);
  	
    var xhr = new XMLHttpRequest();
	xhr.onload =  function() {
		if(xhr.status == 200) {
			var data = JSON.parse(xhr.responseText);
  	  		L.geoJson(data).addTo(mymap).bindPopup(function (layer) {
      			return layer.feature.properties.adm_nm;
  			});
		}
 	 };
    xhr.open("GET", "20190403.geojson", true);
	xhr.send();
  	</script>
</body>
</html>

<html>
<head>
  <title>A Leaflet map!</title>
  <link rel="stylesheet" href="https://unpkg.com/leaflet@1.5.1/dist/leaflet.css"
   integrity="sha512-xwE/Az9zrjBIphAcBb3F6JVqxf46+CDLwfLMHloNu6KEQCAWi6HcDUbeOfBIptF7tcCzusKFjFw2yuvEpDL9wQ=="
   crossorigin=""/>
<script src="https://unpkg.com/leaflet@1.5.1/dist/leaflet.js"
   integrity="sha512-GffPMF3RvMeYyc1LWMHtK8EbPv0iNZ8/oTtHPx9/cc2ILxQ+u905qIwdpULaqDkyBKgOaB57QTMg7ztg8Jm2Og=="
   crossorigin=""></script>
  <style>
    #mapid{ height: 100% }
  </style>
</head>
<body>
	<div id="mapid" style="width: 500px; height: 600px;"></div>
  	<script>
  	var mymap = L.map('mapid').setView([37.566, 126.978], 6);

  	L.tileLayer('https://api.tiles.mapbox.com/v4/{id}/{z}/{x}/{y}.png?access_token=pk.eyJ1IjoibWFwYm94IiwiYSI6ImNpejY4NXVycTA2emYycXBndHRqcmZ3N3gifQ.rJcFIG214AriISLbB6B5aw', {
			maxZoom: 18,
			attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, ' +
			'<a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, ' +
			'Imagery <a href="https://www.mapbox.com/">Mapbox</a>',
			id: 'mapbox.streets'
	}).addTo(mymap);
  	
  	var xhr = new XMLHttpRequest();
	xhr.onload =  function() {
		if(xhr.status == 200) {
			var data = JSON.parse(xhr.responseText);
  	  		L.geoJson(data).addTo(mymap).bindPopup(function (layer) {
      			return layer.feature.properties.CTP_KOR_NM;
  			});
		}
 	 };
    xhr.open("GET", "sido.geojson", true);
	xhr.send();
  	</script>
</body>
</html>

<html>
<head>
  <title>A Leaflet map!</title>
  <link rel="stylesheet" href="https://unpkg.com/leaflet@1.5.1/dist/leaflet.css"
   integrity="sha512-xwE/Az9zrjBIphAcBb3F6JVqxf46+CDLwfLMHloNu6KEQCAWi6HcDUbeOfBIptF7tcCzusKFjFw2yuvEpDL9wQ=="
   crossorigin=""/>
<script src="https://unpkg.com/leaflet@1.5.1/dist/leaflet.js"
   integrity="sha512-GffPMF3RvMeYyc1LWMHtK8EbPv0iNZ8/oTtHPx9/cc2ILxQ+u905qIwdpULaqDkyBKgOaB57QTMg7ztg8Jm2Og=="
   crossorigin=""></script>
  <style>
    #mapid{ height: 100% }
  </style>
</head>
<body>
	<div id="mapid" style="width: 800px; height: 500px;"></div>
  	<script>
  	var mymap = L.map('mapid').setView([37.566, 126.978], 10);

  	L.tileLayer('https://api.tiles.mapbox.com/v4/{id}/{z}/{x}/{y}.png?access_token=pk.eyJ1IjoibWFwYm94IiwiYSI6ImNpejY4NXVycTA2emYycXBndHRqcmZ3N3gifQ.rJcFIG214AriISLbB6B5aw', {
			maxZoom: 18,
			attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, ' +
			'<a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, ' +
			'Imagery <a href="https://www.mapbox.com/">Mapbox</a>',
			id: 'mapbox.streets'
	}).addTo(mymap);

  	var xhr = new XMLHttpRequest();
	xhr.onload =  function() { 
		if(xhr.status == 200) {
			var data = JSON.parse(xhr.responseText);
  	  		L.geoJson(data).addTo(mymap).bindPopup(function (layer) {
  	  			console.log(layer);
      			return layer.feature.properties.SIG_KOR_NM;
  			});
		}
 	 };
    xhr.open("GET", "sigungu.geojson", true);
	xhr.send();  	
  	</script>
</body>
</html>


<html>
<head>
  <title>A Leaflet map!</title>
  <link rel="stylesheet" href="https://unpkg.com/leaflet@1.5.1/dist/leaflet.css"
   integrity="sha512-xwE/Az9zrjBIphAcBb3F6JVqxf46+CDLwfLMHloNu6KEQCAWi6HcDUbeOfBIptF7tcCzusKFjFw2yuvEpDL9wQ=="
   crossorigin=""/>
<script src="https://unpkg.com/leaflet@1.5.1/dist/leaflet.js"
   integrity="sha512-GffPMF3RvMeYyc1LWMHtK8EbPv0iNZ8/oTtHPx9/cc2ILxQ+u905qIwdpULaqDkyBKgOaB57QTMg7ztg8Jm2Og=="
   crossorigin=""></script>
  
  <script src="http://code.jquery.com/jquery-2.1.4.min.js"></script>
  <style>
    #mapid{ height: 100% }
    b {
    	color : red;
    }
  </style>
</head>
<body>
	<div id="mapid" style="width: 800px; height: 500px;"></div>
  	<script>
  	var mymap = L.map('mapid').setView([33.349, 126.58], 9);

  	L.tileLayer('https://api.tiles.mapbox.com/v4/{id}/{z}/{x}/{y}.png?access_token=pk.eyJ1IjoibWFwYm94IiwiYSI6ImNpejY4NXVycTA2emYycXBndHRqcmZ3N3gifQ.rJcFIG214AriISLbB6B5aw', {
			maxZoom: 18,
			attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, ' +
			'<a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, ' +
			'Imagery <a href="https://www.mapbox.com/">Mapbox</a>',
			id: 'mapbox.streets'
	}).addTo(mymap);

  	var xhr = new XMLHttpRequest();
	xhr.onload =  function() { 
		if(xhr.status == 200) {
			var data = JSON.parse(xhr.responseText);
  	  		L.geoJson(data, {style:function(){ return {color:"pink"}}}).addTo(mymap).bindPopup(function (layer) {
  	  			console.log(layer)
  	  			var content = "<b>"+ layer.feature.properties.description+"</b><hr><ul>";
  	  			var items = layer.feature.properties.items;
  	  			for(var data in items)
  	  				content += "<li>"+items[data]+"</li>";
  	  			content += "</ul>";
      			return content;
  			});
		}
 	 };
    xhr.open("GET", "jejumap1.geojson", true);
	xhr.send();  	
  	</script>
</body>
</html>


<html>
<head>
  <meta charset="UTF-8">
  <title>A Leaflet map!</title>
 <link rel="stylesheet" href="https://unpkg.com/leaflet@1.5.1/dist/leaflet.css"
   integrity="sha512-xwE/Az9zrjBIphAcBb3F6JVqxf46+CDLwfLMHloNu6KEQCAWi6HcDUbeOfBIptF7tcCzusKFjFw2yuvEpDL9wQ=="
   crossorigin=""/>
<script src="https://unpkg.com/leaflet@1.5.1/dist/leaflet.js"
   integrity="sha512-GffPMF3RvMeYyc1LWMHtK8EbPv0iNZ8/oTtHPx9/cc2ILxQ+u905qIwdpULaqDkyBKgOaB57QTMg7ztg8Jm2Og=="
   crossorigin=""></script>
  <style>
    #mapid{ height: 100% }
  </style>
</head>
<body>
  <div id="mapid"></div>
  <script>
  // initialize the map
  var mymap = L.map('mapid').setView([42.35, -71.08], 3);

  // load a tile layer
  L.tileLayer('https://api.tiles.mapbox.com/v4/{id}/{z}/{x}/{y}.png?access_token=pk.eyJ1IjoibWFwYm94IiwiYSI6ImNpejY4NXVycTA2emYycXBndHRqcmZ3N3gifQ.rJcFIG214AriISLbB6B5aw', {
		maxZoom: 18,
		attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, ' +
			'<a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, ' +
			'Imagery <a href="https://www.mapbox.com/">Mapbox</a>',
		id: 'mapbox.streets'
	}).addTo(mymap);

    var xhr = new XMLHttpRequest();
	xhr.onload =  function() { 
		if(xhr.status == 200) {
			var data = JSON.parse(xhr.responseText);
			L.geoJson(data).addTo(mymap).bindPopup(function (layer) {
  	  			 return "나라명 : " +layer.feature.properties.name;
  			});
		}
 	 };
    xhr.open("GET", "countries.geojson", true);
	xhr.send();

  </script>
</body>
</html>

<!DOCTYPE html>
<html>
<head>
    <meta charset='utf-8'>
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.5.1/dist/leaflet.css"
   integrity="sha512-xwE/Az9zrjBIphAcBb3F6JVqxf46+CDLwfLMHloNu6KEQCAWi6HcDUbeOfBIptF7tcCzusKFjFw2yuvEpDL9wQ=="
   crossorigin=""/>
<script src="https://unpkg.com/leaflet@1.5.1/dist/leaflet.js"
   integrity="sha512-GffPMF3RvMeYyc1LWMHtK8EbPv0iNZ8/oTtHPx9/cc2ILxQ+u905qIwdpULaqDkyBKgOaB57QTMg7ztg8Jm2Og=="
   crossorigin=""></script>
</head>
<body>
   <p id="demo">위치정보를 추출하려면 실행 버튼을 클릭하세요:</p>
   <button onclick="getLocation()">실행</button>
   <hr>
   <div id="mapid" style="width: 600px; height: 400px;"></div>
   <script>
      var x=document.getElementById("demo");
	  function getLocation() {
         if (navigator.geolocation) {
            navigator.geolocation.getCurrentPosition(showPosition,showError);
         }
         else {
        	 x.innerHTML=" 이 브라우저는 geolocation을 지원하지 않습니다.";        	
       	 }         
      }
      function showPosition(position) {
          x.innerHTML="위도: " + position.coords.latitude + "<br />경도: " + position.coords.longitude;
          var lat = position.coords.latitude;
          var lng = position.coords.longitude;
          var mymap = L.map('mapid').setView([lat, lng], 15)
			L.tileLayer('https://api.tiles.mapbox.com/v4/{id}/{z}/{x}/{y}.png?access_token=pk.eyJ1IjoibWFwYm94IiwiYSI6ImNpejY4NXVycTA2emYycXBndHRqcmZ3N3gifQ.rJcFIG214AriISLbB6B5aw', {
				maxZoom: 18,
				attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, ' +
					'<a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, ' +
					'Imagery <a href="https://www.mapbox.com/">Mapbox</a>',
				id: 'mapbox.streets'
			}).addTo(mymap);

			L.marker([lat, lng]).addTo(mymap)
				.bindPopup("<b>우리가 있는 곳... 쬠 이상하다ㅜ").openPopup();   
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
<meta charset="UTF-8">
<title>Insert title here</title>
<style>
	* {
		font-family : 'THE개이득';
	}
    h3 {
    	color : red;
    }
</style>
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.5.1/dist/leaflet.css"
   integrity="sha512-xwE/Az9zrjBIphAcBb3F6JVqxf46+CDLwfLMHloNu6KEQCAWi6HcDUbeOfBIptF7tcCzusKFjFw2yuvEpDL9wQ=="
   crossorigin=""/>
<script src="https://unpkg.com/leaflet@1.5.1/dist/leaflet.js"
   integrity="sha512-GffPMF3RvMeYyc1LWMHtK8EbPv0iNZ8/oTtHPx9/cc2ILxQ+u905qIwdpULaqDkyBKgOaB57QTMg7ztg8Jm2Og=="
   crossorigin=""></script>
</head>
<body>
	<h1>입력된 주소로 지도를 그리는 프로그램</h1>
	<button onclick="addToCoord();">주소입력</button>
	<hr>
	<div id="mapid" style="width: 800px; height: 500px;"></div>
	<script>
	var mymap;
	function addToCoord() {
		var address = prompt("주소를입력하세요");
		var lat;
		var lng;
		
		if (address) {		
			var xhr = new XMLHttpRequest();
			xhr.onload =  function() { 
				if(xhr.status == 200) {
					var data = JSON.parse(xhr.responseText);
					lat = data.results[0].geometry.location.lat;
					lng = data.results[0].geometry.location.lng;
					alert("좌표로 : " + lat + ":" + lng);
					if(mymap)
						mymap.remove();
					mymap = L.map('mapid').setView([lat, lng], 16)
					L.tileLayer('https://api.tiles.mapbox.com/v4/{id}/{z}/{x}/{y}.png?access_token=pk.eyJ1IjoibWFwYm94IiwiYSI6ImNpejY4NXVycTA2emYycXBndHRqcmZ3N3gifQ.rJcFIG214AriISLbB6B5aw', {
						maxZoom: 18,
						attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, ' +
							'<a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, ' +
							'Imagery <a href="https://www.mapbox.com/">Mapbox</a>',
						id: 'mapbox.streets'
					}).addTo(mymap); 

					L.marker([lat, lng]).addTo(mymap).bindPopup("<h3>여기 찾았지롱?</h3>").openPopup();
				}
			};
			
			xhr.open("GET", "https://maps.googleapis.com/maps/api/geocode/json?key=AIzaSyDy81EbO46BRSnX1DOgg_F84bhsdbku2z4&address="+encodeURIComponent(address), true);
			xhr.send();
		}		
	}
	</script>
</body>
</html>


```
