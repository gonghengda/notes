- [页面渲染](#页面渲染)
- [滚回顶部](#滚回顶部)
- [获取标签](#获取标签)



## 页面渲染

svg标签渲染 `<div dangerouslySetInnerHTML={{__html:text}} />`

## 滚回顶部

  ```
  var gotop = function() {
    if (window.pageYOffset <= 0) {
      return window.cancelAnimationFrame(timer);
    }
    window.scrollTo(0, window.pageYOffset - 200);
    timer = window.requestAnimationFrame(gotop);
  };
  var timer = window.requestAnimationFrame(gotop);
   window.scrollTo(0, 0);
```

## 获取标签
```
  document.getElementById('Id名'); 
  document.getElementsByTagName('标签名');
  document.getElementsByName('name'); 
  document.getElementsByClassName('类名');
  document.querySelectorAll('.address li');
  getAttribute('value')` 获取标签里的属性
  attributes["value"].value;  
```

## 格式化
```
将1000转化为1,000
new Intl.NumberFormat().format(1000); // '1,000'
```
