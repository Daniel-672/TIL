## Javascript tip

### 1. 이미지 선택시 보여주기

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

  