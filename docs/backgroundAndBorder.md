## 边框与背景

### 1.多重边框
#### box-shadow方案
理论上可以实现无限多层边框
```js
// html
<div class="box">box-shadow unset</div>
<div class="box1">box-shadow inset</div>

// css
.box{
  width: 120px;
  height: 120px;
  background-color: antiquewhite;
  box-shadow: 0 0 0 10px red,
              0 0 0 15px blue;
  margin: 15px;
  display: inline-block;
}
.box1{
  width: 120px;
  height: 120px;
  background-color: antiquewhite;
  box-shadow: 0 0 0 5px blue inset,
              0 0 0 15px red inset;
  padding: 15px;
  display: inline-block;
}
```
![boxShadow.png](./images/boxShadow.jpg)

缺点：
1. box-shadow**本身不占位置**，需要通过设置内边距或者外边距来模拟它的”占位“.
2. unset的投影在元素的外圈，并**不是元素的可点击范围**，无法触发点击事件。可以使用inset的形式来绕过这一个问题。
3. 边框的样式只能是**实线**的。

#### outline方案
可以实现两层边框，而且边框样式可以多样。
```js
// html
<div class="box2">outline dotted</div>
<div class="box3">outline radius</div>
<div class="box4">outline inner</div>

// css
.box2{
  width: 120px;
  height: 120px;
  background-color: antiquewhite;
  border: 10px solid red;
  outline: 5px dotted blue;
  display: inline-block;
}
.box3{
  width: 120px;
  height: 120px;
  background-color: antiquewhite;
  border-radius: 10px;
  border: 10px solid red;
  outline: 5px solid blue;
  display: inline-block;
  margin: 0 20px;
}
.box4{
  width: 120px;
  height: 120px;
  background-color: antiquewhite;
  border: 20px solid red;
  outline: 2px dotted blue;
  outline-offset: -10px;
  display: inline-block;
  margin: 0 20px;
}
```  
![outline.jpg](./images/outline.jpg)

缺点：
1. 只能模拟两层边框的场景。
2. 边框外边的outline也是不占位置的，有被覆盖的风险。
3. 圆角的outline不贴合，outline仍然是矩形的。

### 2.背景图片定位
需要实现背景图片的灵活定位
#### background-position方案
非常灵活的方案，可以定位任意的地方
```js
// html
<div class="box">background-position</div>

// css
.box{
  width: 200px;
  height: 120px;
  background-color: lightcyan;
  background-image: url('./apple.png');
  background-repeat: no-repeat;
  background-position: right 20px bottom 20px;
}
```  
![background-position.jpg](./images/background-position.jpg)

#### background-origin方案
针对三种box-sazing来定位背景图片

```js
// html
<div class="box1">background-position</div>
<div class="box2">background-origin</div>

// css
.box1{
  display: inline-block;
  width: 200px;
  height: 120px;
  background-color: lightcyan;
  background-image: url('./apple.png');
  background-repeat: no-repeat;
  padding: 20px;
  background-position: right 20px bottom 20px;
}
.box2{
  display: inline-block;
  width: 200px;
  height: 120px;
  background-color: lightcyan;
  background-image: url('./apple.png');
  background-repeat: no-repeat;
  background-position: right bottom;
  padding: 20px;
  background-origin: content-box;
}
```  
![backgroud-origin.jpg](./images/backgroud-origin.jpg)

可以看出，在这种场景中，使用backgroud-origin更加贴合，如果以后padding发生改变，这个方法修改的地方更少。

#### calc()方案
计算的方式
```js
// html
<div class="box3">background-position</div>

// css
.box3{
  width: 200px;
  height: 120px;
  background-color: lightcyan;
  background-image: url('./apple.png');
  background-repeat: no-repeat;
  background-position: calc(100% - 20px) calc(100% - 10px);
}
```  
![background-calc.jpg](./images/background-calc.jpg)

### 3.边框内圆角
#### 多个元素组合
这种方式非常灵活，可以借助背景来实现多样的边框效果
```js
// html
<div class="box">
  <div class="inner">两个元素实现</div>
</div>

// css
.box{
  height: 150px;
  width: 200px;
  background-color: antiquewhite;
  padding: 20px;
}
.inner{
  height: 110px;
  padding: 20px;
  border-radius: 20px;
  background-color: aquamarine;
}
```  
![mulBoxes.jpg](./images/mulBoxes.jpg)

#### 借助box-shadow和outline来实现
利用box-shadow和outline对于圆角边框的不同实现，来实现一个元素实现内部圆角的效果
```js
// html
<div class="box1">box-shadow & outline</div>

// css
.box1{
  width: 200px;
  height: 110px;
  padding: 20px;
  border-radius: 20px;
  background-color: aquamarine;
  outline: 20px solid antiquewhite; //不贴合圆角
  box-shadow: 0 0 0 10px antiquewhite; // 贴合圆角
}
```  
![boxShadow_outline.jpg](./images/boxShadow_outline.jpg)

注意点：
1. 圆角半径r、outline宽度m和box-shadow的宽度n必须要满足这个关系：**(Math.sqrt(2)-1)*r < n < m**
2. 这里利用的是outline不贴合圆角的效果来实现的，可以归属为一种hack，未来如果浏览器修正了无法使用这种方式了。





















