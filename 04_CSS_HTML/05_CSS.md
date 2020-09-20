### - 아코디언 박스

```html
<button class="accordion">Section 1</button>
<div class="panel">
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.</p>
</div>

<script>
var acc = document.getElementsByClassName("accordion");
var i;

for (i = 0; i < acc.length; i++) {
  acc[i].addEventListener("click", function() {
    this.classList.toggle("active");
    var panel = this.nextElementSibling;
    if (panel.style.maxHeight) {
      panel.style.maxHeight = null;
    } else {
      panel.style.maxHeight = panel.scrollHeight + "px";
    } 
  });
}
</script>
```



### - 이미지 + text (HTML + CSS)

```html
    <!-- 1라인답글의 작성자 정보 -->
    <div class="c_article">
      <div>
          <a href="#"><img class="image_section" width="100" src="{{ comment.cwriter.photo.url }}" alt="" /></a>
      </div>
      <div>
          <div style="margin-bottom:2px; display: inline-block"><b>[{{ comment.cwriter.nickName }}]님</b><span style="color:red">{% if article.awriter == comment.cwriter %}(작성자){% endif %}</span></div>
          <div>{{ comment.updated_at }}</div>
      </div>
    </div>
```

```html
    .c_article {
      width: auto;
      display: flex;
      align-items: center
    }
```



### - 