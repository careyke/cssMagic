## 文本溢出显示...解决方案
这里的解决方案指的都是**css方案**，个人不推荐使用js方案来解决这类问题，因为需要频繁计算，会增加重排的次数。

### 单行文本溢出显示...
#### 关键属性
- overflow:hidden —— 溢出部分不显示
- white-space:nowrap —— 文字单行显示
- text-overflow:ellipsis —— 文本溢出部分显示...
- word-break:break-all —— 任意字符间断行

#### example
```js
// html
<div class="container">
  一段很长的文本一段很长的文本一段很长的文本一段很长的文本一段很长的文本一段很长的文本一段很长的文本一段很长的文本一段很长的文本
</div>

// css
.container{
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
  word-break: break-all;
}
```  
#### 优点
1. 兼容性很好
2. 省略号响应式显示（有溢出才显示，不溢出不显示）

#### 缺点
1. 只能支持单行文本

### 多行文本溢出显示... —— 未来的解决方案
#### 关键属性
- display: -webkit-box —— 设置为弹性伸缩盒子模型
- -webkit-box-orient: vertical —— 设置弹性盒子中子元素的排列方式
- -webkit-line-clamp：2 —— 设置盒子中显示文本的最大行数，需要**配合上面两个属性才能生效**。
- overflow: hidden —— 溢出内容不显示。

#### example
```js
// html
<div class="container1">
  一段很长的文本一段很长的文本一段很长的文本一段很长的文本一段很长的文本一段很长的文本一段很长的文本一段很长的文本一段很长的文本
</div>

// css
.container1{
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 2;
  overflow: hidden;
}
```  
#### 优点
1. 简单
2. 完美实现多行溢出显示...

#### 缺点
1. 兼容性不好，需要使用在webkit内核的浏览器中，手机端更适用。

### 多行文本溢出显示... —— 现在最完美的方案（联合方案）
#### 关键属性
- float: 需要借助浮动特性
- line-height / max-height: 需要借助最大高度和文本行高属性
- position: relative 相对定位
- tranform: tranform移动位置
- overflow: hidden
- ::before/::after 元素的伪类。

#### example
```js
// html
<div class="container2">
  <div class="text">
    一段很长的文本一段很长的文本一段很长的文本一段很长的文本一段很长的文本一段很长的文本一段很长的文本一段很长的文本一段很长的文本
  </div>
</div>

// css
.container2{
  overflow: hidden;
  max-height: 60px;
  line-height: 20px;
}
.container2::before{
  content: '';
  float: left;  
  height: 60px;
  width: 20px;
}
.container2::after{
  content: '...';
  float: right;
  width: 20px;
  position: relative;
  left: 100%;
  transform: translate(-100%,-100%);
  background-color: #ffffff;
}
.text{
  float: right;
  width: 100%;
  margin-left: -20px;
  word-break: break-all;
}
```  

#### 实现原理（细读）
有 A、B、C 三个盒子，A 左浮动，B、C 右浮动。设置 A 盒子的高度与 B 盒子高度（或最大高度）要保持一致
1. 当的 B 盒子高度低于 A 盒子，C 盒子仍会处于 B 盒子右下方。
2. 如果 B 盒子文本过多，高度超过了 A 盒子，则 C 盒子不会停留在右下方，而是掉到了 A 盒子下。
3. 接下来对 C 盒子进行相对定位，将 C 盒子位置向右侧移动 100%，并向左上方向拉回一个 C 盒子的宽高（不然会看不到哟）。这样在文本未溢出时不会看到 C 盒子，在文本溢出时，显示 C 盒子。

#### 优点
1. 兼容性好
2. 响应式显示...
3. 纯css实现

#### 缺点
1. 省略号稍微优点生硬
2. 写起来比较复杂


### 参考文档
[可能是最全的 “文本溢出截断省略” 方案合集](https://juejin.im/post/5dc15b35f265da4d432a3d10#heading-9)












