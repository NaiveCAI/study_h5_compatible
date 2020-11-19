# study_h5_compatible

## PX

定义：虚拟像素，可以理解为“直觉”像素，CSS和JS使用的抽象单位。浏览器内的一切长度都是以CSS像素为单位的，CSS像素的单位是px。

## 如何理解PX

它是图像显示的基本单元，不是一个确定的量（比如一厘米），也不是一个点或者一个方块，是一个抽象概念。

不同设备里的的px，采样单元的大小是不一样的。比如一个显示器，一个物理像素等于显示器的点距；而一个打印机，等于一个墨点，这也是不一样的。

衡量显示器的一个`物理单元`点大小的单位叫`ppi`(px per inch)，每英寸多少像素数。

（比如，同样是一英寸的两块屏幕，如果其中一个物理单元点更多，那就说这个屏幕更精细，每个物理单元更小）


## CSS的像素

CSS里面的px，其实也不是一个绝对的单位，是一个相对的单位，因为前面说到，不同设备的物理像素大小是不一样的。

CSS里面的1px，会针对不同的设备不同的物理像素换算，使得浏览器中1css像素的大小在不同物理设备上看上去大小总是差不多 ，目的是为了保证阅读体验一致。

我的理解是：在设备A上，1CSS像素可能有2个物理像素的大小，但是在另一个设备上，可能有3个物理像素的大小。

**这里就体现出了CSS像素的一个相对性：在不同的设备之间，每1个CSS像素所代表的设备像素是可以变化的。**


## 举例说明相对性

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Study h5 compatible</title>
  <link rel="stylesheet" href="src/study.css">
</head>
<body>
  <div class="box"></div>
</body>
</html>
```

```CSS
html, body {
  height: 100%;
}

body {
  display: flex;
  align-items: center;
  margin: 0;
}

.box {
  height: 200px;
  width: 200px;
  background-color: red;
}
```

把浏览器缩小到宽度400px的时候，这个box应该正好占屏幕一半。

但如果我们把页面放大到200%，也就是原来的两倍。此时块状容器则横向占满了整个浏览器。

但是我们其实并没有改变浏览器的大小，也没有改变box的宽度。

**这里就体现出了CSS像素的另一个相对性：在同一个设备上，每1个CSS像素所代表的设备像素是可以变化的。**（因为屏幕放大了之后，inspect这个元素，上面显示的还是200px）


## DP

dip或dp,（device independent pixels，设备独立像素）与屏幕密度有关

dp是指设备能控制显示的最小物理单位，即显示器上的一个物理像素。从屏幕在工厂生产出的那天起，它上面设备像素点就固定不变了，单位pt。

前面提到，不同的设备，每一个物理像素的大小是不同的。比如一个显示器是点距；而一个打印机是一个墨点。


## DP与CSS像素之间的关系

前面说到，css里面的1px，会针对不同的设备不同的物理像素换算，使得浏览器中1css像素的大小在不同物理设备上看上去大小总是差不多 ，目的是为了保证阅读体验一致。

所以，每一个css px与设备的dp之间必定存在一个比例。

**这就是DPR**

设备像素比(device pixel ratio, dpr/DPR): 它描述的是未缩放状态下，**设备像素和CSS像素的初始比例关系**，也可以解释为默认缩放比例。

如何理解这个概念呢？通俗来说，它是指在开发中1个CSS像素占用多少设备像素，如 dpr=2 代表1个CSS像素用2x2个设备像素来绘制，所以，可以理解为1px由多少个设备像素组成。

可以用如下代码获取DPR:
```JavaScript
window.devicePixelRatio
```


## 为什么会有屏幕兼容性问题

就是因为不同屏幕的DPR不一样。

如下图所示，某元素的CSS样式：
```CSS
width: 2px;
height: 2px；
```

在不同的屏幕上，CSS像素所呈现的物理尺寸是一致的，而不同的是CSS像素所对应的物理像素具数是不一致的。

在普通屏幕下1个CSS像素对应1个物理像素，而在Retina屏幕下，1个CSS像素对应的却是4个物理像素。
