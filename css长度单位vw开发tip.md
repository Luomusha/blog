# 什么是vw?
vw和vh是视口（viewport units）单位.viewport就是浏览器窗口的大小的单位,不受显示器分辨率的影响.

# vw包括滚动条吗?
当显示内容高度超过浏览器高度时候,在普通的pc端浏览器,
在PC端浏览器如Chrome,IE,Firefox,100vw是包含了滚动条值的,也就是说剩余使用空间为calc(100vw - 15px)
在移动端浏览器,滚动条是覆盖在dom元素之上,并且会自动隐藏的.不会影响实际宽度.实际可用宽度为100vw


# position fixed样式会影响滚动条吗?
有时候为了方便操作滚动条宽度影响,有些架构会这样安排dom元素
```html
<html>
  <head>
    <style>
      html,body{
        height: 100%;
        overflow: hidden;
      }
      #app {
        overflow-y: scroll;
      }
    </style>
  </head>
  <body>
    <div id="app">
    xxx
    xxx
    </div>
  </body>
</html>
```
这样取消了body的滚动,由body下的顶级dom元素app代理滚动.
这样的优点是方便统一控制滚动事件.
缺点是position fixed会覆盖在#app元素上.包括#app的滚动条.




