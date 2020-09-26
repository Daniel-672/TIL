

# Day2

>  domEdit

### - 교육내용

```html
<!DOCTYPE html>
<html>
<head>
    <script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
    <script>
        $(document).ready(function () {
            $('h1').addClass('item');
        });
    </script>
    <style>
        .item {
            background-color : yellow;
        }
        .test.item {
            background-color : red;
        }
    </style>
</head>
<body>
    <h1>Header-0</h1>
    <h1 class="test">Header-1</h1>
    <h1>Header-2</h1>
</body>
</html>

<!DOCTYPE html>
<html>
<head>
        <style>
        .class0 {
            color : red;
        }
        .class1 {
            color : green;
        }
        .class2 {
            color : blue;
        }
    </style>
    <script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
    <script>
        $(document).ready(function () {
            $('h1').addClass(function (index, v) {
                console.log("[" + v + "]");
                return 'class' + index;
            });
        });
    </script>
</head>
<body>
    <h1>Header-0</h1>
    <h1>Header-1</h1>
    <h1>Header-2</h1>
</body>
</html>

<!DOCTYPE html>
<html>
<head>
    <script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
    <script>
        $(document).ready(function () {
            $('h1').removeClass('select');
        });
    </script>
</head>
<body>
    <h1 class="item">Header-0</h1>
    <h1 class="item select">Header-1</h1>
    <h1 class="item">Header-2</h1>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
    <script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
    <script>
        $(document).ready(function () {
            $('img').attr('width', 200);
        });
    </script> 
</head>
<body>
    <img src="Chrysanthemum.jpg"/>
    <img src="Desert.jpg"/>
    <img src="Hydrangeas.jpg"/>
</body>
</html>

<!DOCTYPE html>
<html>
<head>
    <script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
    <script>
        $(document).ready(function () {
            $('img').attr('width', function (index) {
                return (index + 1) * 100;
            });
        });
    </script>
</head>
<body>
    <img src="Chrysanthemum.jpg"/>
    <img src="Desert.jpg"/>
    <img src="Hydrangeas.jpg"/>
</body>
</html>

<!DOCTYPE html>
<html>
<head>
    <script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
    <script>
           $(document).ready(function () {
                $('img').attr({
//                    width: function (index) {
//                        return (index + 1) * 100;
//                    },
//                    height: 100
                    {width:50, height:50},
                    {width:100, height:100},
                    {width:150, height:150}
                });
            });
    </script>
</head>
<body>
<img src="Chrysanthemum.jpg"/>
    <img src="Desert.jpg"/>
    <img src="Hydrangeas.jpg"/>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
    <script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
    <script>
        $(document).ready(function () {
            $('h1').removeAttr('data-index');
        });
    </script>
</head>
<body>
    <h1 data-index="0">Header-0</h1>
    <h1 data-index="1">Header-1</h1>
    <h1 data-index="2">Header-2</h1>
</body>
</html>

<!DOCTYPE html>
<html>
<head>
    <style>
        .first { color:Red; }
        .second { color:Pink; }
        .third { color:Orange; }
    </style>
    <script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
    <script>
        $(document).ready(function () {
  /*          $('h1').each(function(index,data) {
        		var color = $(data).css('color');
        		 alert(color); 
        	}); */
         	var color = $('h1').css('color');
        	alert(color);
        });
    </script>
</head>
<body>
    <h1 class="first">Header-0</h1>
    <h1 class="second">Header-1</h1>
    <h1 class="third">Header-2</h1>
</body>
</html>

<!DOCTYPE html>
<html>
<head>
    <script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
    <script>
        $(document).ready(function () {
            // 변수를 선언합니다.
            var color = ['Red', 'White', 'Purple'];

            // 문서 객체의 스타일을 변경합니다.
            $('h1').css('color', function (index) {
                return color[index];
            });
        });
    </script>
</head>
<body>
    <h1>Header-0</h1>
    <h1>Header-1</h1>
    <h1>Header-2</h1>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
    <script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
    <script>
        $(document).ready(function () {
            // 변수를 선언합니다.
            var color = ['Red', 'White', 'Purple'];

            // 문서 객체의 스타일을 변경합니다.
            $('h1').css({
                color: function (index) {
                    return color[index];
                },
                backgroundColor: 'Black'
            });
        });
    </script>
</head>
<body>
    <h1>Header-0</h1>
    <h1>Header-1</h1>
    <h1>Header-2</h1>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
    <script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
    <script>
        $(document).ready(function () {           
           /*  var html = $('h1').html();          
            alert(html);   */
            $('h1').each(function(index, data){
            	var html = $(data).html();          
                alert(html);
            });  
        });
    </script>
</head>
<body>
    <h1>Header-0</h1>
    <h1>Header-1</h1>
    <h1>Header-2</h1>
</body>
</html>

<!DOCTYPE html>
<html>
<head>
    <script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
    <script>
        $(document).ready(function () {
            // 변수를 선언합니다.
            var text = $('h1').text();
            // 출력합니다.
            alert(text);
        });
    </script>
</head>
<body>
    <h1>Header-0</h1>
    <h1>Header-1</h1>
    <h1>Header-2</h1>
</body>
</html>

<!DOCTYPE html>
<html>
<head>
    <script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
    <script>
        $(document).ready(function () {
            $('.g1').html('<h1>$().html() Method</h1>');
            $('.g2').text('<h1>$().html() Method</h1>');
        });
    </script>
</head>
<body>
    <div class='g1'></div>
    <div class='g1'></div>
    <div class='g1'></div>
    <div class='g2'></div>
    <div class='g2'></div>
    <div class='g2'></div>
</body>
</html>

<!DOCTYPE html>
<html>
<head>
    <script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
    <script>
        $(document).ready(function () {
            $('div').html(function (index, dt) {
                return '<h1>Header-' + index + dt +'</h1>';
                console.log(x);
            });
        });
    </script>
</head>
<body>
    <div></div>
    <div></div>
    <div></div>
</body>
</html>

<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
    <script>
     /*    $(document).ready(function () {
            $('h1').html(function (index, html) {
                return '★' + html + '★';   // 결합연산자..
            });
        }); */
        $(document).ready(function () {
        	$('h1').click(function (x, y) {
            	$(this).text(function (a, b) {
            		//alert(a + ":" +b);
                	return '★' + b + '★';   // 결합연산자..
            	});
                console.log(y)
        	});
        });
    </script>
</head>
<body>
    <h1>Header-0</h1>
    <h1>Header-1</h1>
    <h1>Header-2</h1>
</body>
</html>

<!DOCTYPE html>
<html>
<head>
    <script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
    <script>
        $(document).ready(function () {
            $('h1').first().remove();
        	//$('div').remove();
        });
    </script>
</head>
<body>
    <div>
        <h1>Header-0</h1>
        <h1>Header-1</h1>
    </div>
</body>
</html>

<!DOCTYPE html>
<html>
<head>
    <script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
    <script>
        $(document).ready(function () {
            $('div').empty();
        });
    </script>
</head>
<body>
    <div>
        <h1>Header-0</h1>
        <h1>Header-1</h1>
    </div>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
    <script src="http://code.jquery.com/jquery-2.1.3.min.js"></script>
    <script>
        $(document).ready(function () {
            $('<h1></h1>').html('Hello World .. !').appendTo('body');
            $('<h1>안녕하세요.... !</h1>').appendTo('body');
        });
    </script>
</head>
<body>

</body>
</html>


<!DOCTYPE html>
<html>
<head>
<script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
<script>
	$(document).ready(function() {
		$('<img/>', {
			src : 'Jellyfish.jpg',
			width : 350,
			height : 250
		}).appendTo('body');
		$('<img />').attr('src', 'Chrysanthemum.jpg').appendTo('body');

	});
</script>
</head>
<body>

</body>
</html>


<!DOCTYPE html>
<html>
<head>
    <script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
    <script>
        $(document).ready(function () {
            // 변수를 선언합니다.
            var h1 = '<h1>Header1</h1>';
            var h2 = '<h2>Header2</h2>';

            // 문서 객체를 추가합니다.
            $('body').append(h1, h2, h1, h2);
        });
    </script>
</head>
<body>

</body>
</html>
```


