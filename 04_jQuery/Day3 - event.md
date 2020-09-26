

# Day3

> event

### - 교육내용

```html
<!DOCTYPE html>
<html>
<head>
    <style>
        .reverse {
        background: Black;
        color: White;
        }
    </style>
    <script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
    <script>
        $(document).ready(function () {
            // 이벤트를 연결합니다.
            $('h1').on('click', function () {
                $(this).html(function (index, html) {
                    return html + '+';
                });
            });

            // 이벤트를 연결합니다.
            $('h1').on({
                mouseenter: function () { $(this).addClass('reverse'); },
                mouseleave: function () { $(this).removeClass('reverse'); }
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
    <style>
        .reverse {
            background: Black;
            color: White;
        }
    </style>
    <script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
    <script>
        $(document).ready(function () {
        // 이벤트를 연결합니다.
            $('h1').hover(function () {
                $(this).addClass('reverse');
            }, function () {
                $(this).removeClass('reverse');
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
    <style>
        .reverse {
            background: Black;
            color: White;
        }
    </style>
    <script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
    <script>
        $(document).ready(function () {
            // 이벤트를 연결합니다.
            $('h1').hover(function () {
                $(this).addClass('reverse');
            }, function () {
                $(this).removeClass('reverse');
            });
            // 이벤트를 연결합니다.
            $('#two').click(function () {
                // 문자열의 앞에 별을 추가합니다.
                $(this).html(function (index, html) {
                    return '★' + html;
                });
            });
            $('#two').click(function () {
                // 문자열의 뒤에 별을 추가합니다.
                $(this).html(function (index, html) {
                    return html + '★';
                });
            });
        });
    </script>
</head>
<body>
    <h1>Header-0</h1>
    <h1 id='two'>Header-1</h1>
    <h1>Header-2</h1>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">

    <script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
    <script>
        $(document).ready(function () {
            // 이벤트를 연결합니다.
            $('h1:first').on("click", function () {
                // 출력합니다.
                $(this).html('ONE CLICK');
                alert('이벤트가 발생했습니다.');
                // 이벤트를 제거합니다.
                $(this).off("click");
            });
            $('h1:last').one('click', function () {
                // 출력합니다.
                $(this).html('ONE CLICK');
                alert('이벤트가 발생했습니다.');           
            });
        });
    </script>
</head>
<body>
    <h1>Header-0</h1>
    <h1>Header-1</h1>
    <h1>Header-2</h1>
    <h1>Header-3</h1>
    <h1>Header-4</h1>
    <h1>Header-5</h1>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>exercise9</title>
    <style>
        * { margin:0px; padding:0px }
        div
        {
            margin:5px; padding:3px;
            border-width:3px;
            border-style:solid;
            border-color:Black;
            border-radius:10px;
        }
    </style>
    <script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
    <script>
        $(document).ready(function () {
            // 이벤트를 연결합니다.
            $('div').click(function () {
                // 변수를 선언합니다.
                var header = $('h1', this).text();
                var paragraph = $('p', this).text();
                // 출력합니다.
                alert(header + '\n' + paragraph);
            });
        });
    </script>
</head>
<body>
    <div>
        <h1>Header 1</h1>
        <p>Paragraph</p>
    </div>
    <div>
        <h1>Header 2</h1>
        <p>Paragraph</p>
    </div>
    <div>
        <h1>Header 3</h1>
        <p>Paragraph</p>
    </div>
</body>
</html>



<!DOCTYPE html>
<html>
<head>
<script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
<script>
	var toggle =true;
	$(document).ready(function() {
		// 변수를 선언합니다.
		var canvas = document.getElementById('draw');
		var context = canvas.getContext('2d');

		// 이벤트를 연결합니다.
		$(canvas).click(function(event) {
			// 위치를 얻어냅니다.
			if (toggle) {				
				var position = $(this).offset();
				var x = event.pageX - position.left;
				var y = event.pageY - position.top;
				// 선을 그립니다.
				context.beginPath();
				context.moveTo(x, y);
				toggle = false;
			} else {				
				var position = $(this).offset();
				var x = event.pageX - position.left;
				var y = event.pageY - position.top;
				// 선을 그립니다.
				context.lineTo(x, y);
				context.strokeStyle = 'red';
				context.stroke();
				toggle = true;
			} 
		});
	});
</script>
</head>
<body>
	<canvas id="draw" width="500" height="300"
		style="border: 1px solid black;">

    </canvas>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">    
    <script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
    <script>
        $(document).ready(function (event) {
            $('textarea').keydown(function () {
                // 남은 글자 수를 구합니다.
                var inputLength = $(this).val().length;
                var remain = 150 - inputLength;

                // 문서 객체에 입력합니다.
                $('h1').html(remain);

                // 문서 객체의 색상을 변경합니다.
                if (remain >= 0) {
                    $('h1').css('color', 'Black');
                } else {
                    $('h1').css('color', 'Red');
                }
            }); 
        });
</script>
</head>
<body>
    <div>
        <p>지금 내 생각을</p>
        <h1>150</h1>
        <textarea cols="70" rows="5"></textarea>
    </div>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">    
    <script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
    <script>
        $(document).ready(function () {
            $('#my_form').submit(function (event) {
                // 입력 양식의 value를 가져옵니다.
                var name = $('#name').val();
                var password = $('#password').val();

                // 출력합니다.
                alert(name + ' : ' + password);

                // 기본 이벤트를 제거합니다.
              //  event.preventDefault();
            });
        });
    </script>
</head>
<body>
<body>
    <form id="my_form" action="not.jsp">
        <table>
            <tr>
                <td>이름: </td>
                <td><input type="text" name="name" id="name"/></td>
            </tr>
            <tr>
                <td>비밀번호: </td>
                <td><input type="password" name="password" id="password"/></td>
            </tr>
        </table>
        <input type="submit" value="제출"/>
    </form>
</body>
</html>
```



### - 실습

```HTML
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
    <button data-index='0'>이미지1</button>
    <button data-index='1'>이미지2</button>
    <button data-index='2'>이미지3</button>
    <button data-index='3'>이미지4</button>
    <button data-index='4'>이미지5</button>
</head>
<body>
    <script>
     $('.button).each(function(index){
        $(this).attr('button data-index', index);
    }).click(function(){
        var index = $(this).attr('button-index');
        $('.button[data-index=' + index + ']').addClass('clicked_button');
        $('.button[data-index!=' + index + ']').removeClass('clicked_button');
    });
    });

    $(document).ready(function () {
            $('<img/>', {
			src : '../images/1.jpg',
			width : 350,
			height : 250
		}).appendTo('body');
    });


    </script>
</body>
</html>


```



