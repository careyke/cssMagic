## 双飞翼布局
双飞翼布局需要达到的效果和圣杯布局是一样的：
1. 三栏布局，左右两边固定，中间部分自适应
2. 中间部分先渲染

## 实现 —— float + 负margin
```js
// HTML
<div class="container">
  <div class="center">
    <div class="inner"> // 对比圣杯布局多了这一层
      一段很长的文本一段很长的文本一段很长的文本一段很长的文本一段很长的文本一段很长的文本一段很长的文本一段很长的文本一段很长的文本
    </div>
  </div>
  <div class="left"></div>
  <div class="right"></div>
</div>

// CSS
.container {
  overflow: hidden;
}
.center {
  background-color: tomato;
  float: left;
  width: 100%;
}
.inner {
  height: 200px;
  margin-left: 100px;
  margin-right: 100px;
}
.left {
  width: 100px;
  height: 200px;
  background-color: aqua;
  float: left;
  margin-left: -100%;
}
.right {
  width: 100px;
  height: 200px;
  background-color: blueviolet;
  float: right;
  margin-left: -100px;
}

```  
可以看出，代码实现是基本和圣杯布局的实现差不多，而且达到的效果基本上是一样的。那为什么还要实现这种布局呢？


在圣杯布局的文章中，我们提到过圣杯布局的缺陷，就是在宽度缩小到一定程度之后，会出现布局的错乱情况。双飞翼布局的出现，就是为了解决这一个问题。**解决的手段也很简单，多增加一个div，将原来使用padding空出左右空间的方式，改成由margin来完成。就可以解决原来的问题**



