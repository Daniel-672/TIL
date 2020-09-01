## Javascript tip

### - 이미지 선택시 보여주기

 - html에 위치 지정

   ```javascript
   <img id="image_section"  width="100" src="#" alt="your image"/>
   ```

- javascript 함수

  ```javascript
  function readURL(input) {
   if (input.files && input.files[0]) {
    var reader = new FileReader();
  
    reader.onload = function (e) {
     $('#image_section').attr('src', e.target.result);
    }
  
    reader.readAsDataURL(input.files[0]);
    }
  }
  
  $("#photo").change(function(){
     readURL(this);
  });
  ```




### - 위경도 찾아서 주소로 변경

```javascript
<script type="text/javascript" src="//dapi.kakao.com/v2/maps/sdk.js?appkey=카카오API키&libraries=services"></script>

function callposi(){
    // BOM의 navigator객체의 하위에 geolocation객체가 새로 추가되었음.
    window.navigator.geolocation.getCurrentPosition( function(position){ //OK
        var lat= position.coords.latitude;
        var lng= position.coords.longitude;

        document.getElementById('target').innerHTML="위경도: "+lat+", "+lng;
        document.getElementById('reportlati').value=lat;
        document.getElementById('reportlong').value=lng;

    var geocoder = new kakao.maps.services.Geocoder();

    var coord = new kakao.maps.LatLng(lat, lng);

    var callback = function(result, status) {
        if (status === kakao.maps.services.Status.OK) {
            var contentText = document.getElementById('reportaddress');
                contentText.innerHTML = result[0].address.address_name
    }
};

geocoder.coord2Address(coord.getLng(), coord.getLat(), callback);

    } ,
    function(error){ //error
        switch(error.code){
            case error.PERMISSION_DENIED:
                str="사용자 거부";
                break;
            case error.POSITION_UNAVAILABLE:
                str="지리정보 없음";
                break;
            case error.TIMEOUT:
                str="시간 초과";
                break;
            case error.UNKNOWN_ERROR:
                str="알수없는 에러";
                break;
        }
        document.getElementById('target').innerHTML=str;
    });

}

{% endblock %}
```



### - 이미지