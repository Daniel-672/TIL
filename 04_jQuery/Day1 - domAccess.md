

# Day1

> domAccess

### - 교육내용

```html
<!DOCTYPE html>
<html>
<head>
    <script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
    <script>
        $(document).ready(function () {
            alert('First READY');
        });

        $(document).ready(function () {
            alert('Second READY');
        });

        $(document).ready(function () {
            alert('Third READY');
        });   
        
        $(function () {
            alert('Final READY');
        });  
    </script>
</head>
<body>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
    <script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
    <script>
        $(document).ready(function () {
            $('h1').css('color', 'Red');
        });

        $(function () {
            $('h2').css('color', 'blue');
            $('h3').css('color', 'green');
        });


    </script>
</head>
<body>
    <h1>jQuery를 테스트합니다.</h1>
    <h2>jQuery를 테스트합니다.</h2>
    <h3>jQuery를 테스트합니다.</h3>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
    <script>
        $(document).ready(function () {
            $('h1').css('color', 'Orange');
            $('h2, p').css('color', 'green');
        });
    </script>
</head>
<body>
    <h1>Lorem ipsum</h1>
    <h2>Lorem ipsum</h2>
    <p>Lorem ipsum dolor sit amet.</p>
    <h1>Lorem ipsum</h1>
    <h2>Lorem ipsum</h2>
    <p>consectetur adipiscing elit.</p>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
    <script>
        $(document).ready(function () {
            $('#target').css('color', 'Orange');
        });
    </script>
</head>
<body>
    <h1>Header-0</h1>
    <h1 id="target">Header-1</h1>
    <h1>Header-2</h1>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
    <script>
        $(document).ready(function () {
            $('h1#target').css('color', 'Orange');
        });
    </script>
</head>
<body>
    <h1>Header-0</h1>
    <h1 id="target">Header-1</h1>
    <h1>Header-2</h1>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
    <script>
        $(document).ready(function () {
            $('.item').css('color', 'Orange');
            $('h1.item').css('background', 'Red');
            $('.item.select').css('border', '5px solid black');
            $('.item:not(.select)').css('border', '5px solid green');
        });
    </script>
</head>
<body>
    <h1 class="item">Header-0</h1>
    <h1 class="item select">Header-1</h1>
    <h1 class="item">Header-2</h1>
    <h2 class="item">Header-0</h2>
    <h2 class="item select">Header-1</h2>
    <h2 class="item">Header-2</h2>
    <h2 class="select">Header-3</h2>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
<script>
	$(document).ready(function() {
		//$('ul *').css('color', 'red');
		$('ul *').css({'color' : 'red', 'font-weight' : 'bold'});
		$('body > div > div').css('font-weight', 'bold');
	});
</script>
</head>
<body>
	<h1>선택자 테스트</h1>
	<div>
		<ul>
			<li>Apple</li>
			<li>Bag</li>
			<li>Cat</li>
			<li>Dog</li>
			<li>Elephant</li>
		</ul>
		<div>
			<ol>
				<li>Apple</li>
				<li>Bag</li>
				<li>Cat</li>
				<li>Dog</li>
				<li>Elephant</li>
			</ol>
		</div>
	</div>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
	<script src="http://code.jquery.com/jquery-2.1.3.min.js"></script>
    <script>
        $(document).ready(function () {
            // 5초 후에 코드를 실행합니다.
            setTimeout(function () {
                var value = $('select > option:selected').val();
                alert(value);
                $('#valtest').val(function(p1, p2) {
                	return p1+":"+p2+":hahaha";
                }); 
            }, 5000);
        });
    </script>
</head>
<body>
    <select>
        <option>Apple</option>
        <option>Bag</option>
        <option>Cat</option>
        <option>Dog</option>
        <option>Elephant</option>
    </select>
    <input id="valtest" type="text"  value="난디폴트값이야">
</body>
</html>




```


