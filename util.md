## 1.电子表格 
> [handsontable](https://handsontable.com/community-download.html)
***
## 2.Boostrap 3级菜单显示隐藏
```
<li class="dropdown"><a href="<?php echo site_url('features');?>" class="dropdown-toggle" data-toggle="dropdown">安拓网络<span class="caret"></span></a>
<ul class="dropdown-menu" role="menu">
    <li><a href="#">xx</a></li>
    <li><a href="#">xx</a></li>
</ul>
</li>

删除 “a” 上的 data-toggle=”dropdown” 属性，点击时，就可以跳转页面了。
加上样式，实现hover时，显示下拉菜单

ul.nav li.dropdown > a.dropdown-toggle{
	border: none !important;
}
 
ul.nav li.dropdown:hover > ul.dropdown-menu{
    display: block;
    margin: 0;
}
```

## 3.背景视频全屏显示 [参考](http://www.jianshu.com/p/21c538a06845)/[BIDEO.JS](http://codetheory.in/html5-fullscreen-background-video/)
```
/* CSS */
* {
  margin: 0; padding: 0;
}

#container {
  overflow: hidden;
  height: 400px;
  background: #edeae8;
  position: relative;
}

video {
  position: absolute;

  /* Vertical and Horizontal center*/
  left: 50%; top: 50%;
  transform: translate(-50%, -50%);
}

/***html***/
<div id="container">
  <video autoplay muted loop>
    <source src="http://ak4.picdn.net/shutterstock/videos/4170274/preview/stock-footage-beautiful-girl-lying-on-the-meadow-and-dreaming-enjoy-nature-close-up-slow-motion-footage.mp4" type="video/mp4">
  </video>
</div>


// JS
var video = document.querySelector('video')
  , container = document.querySelector('#container');

var setVideoDimensions = function () {
  // 获取视频本身的宽度和高度
  var w = video.videoWidth
    , h = video.videoHeight;

  // 获取视频的比例
  var videoRatio = (w / h).toFixed(2);

  // 获取容器的宽和高
  var containerStyles = window.getComputedStyle(container)
    , minW = parseInt( containerStyles.getPropertyValue('width') )
    , minH = parseInt( containerStyles.getPropertyValue('height') );

//计算和调整容器比例
  var widthRatio = minW / w
    , heightRatio = minH / h;

  //根据比例做调整
  if (widthRatio > heightRatio) {
    var newWidth = minW;
    var newHeight = Math.ceil( newWidth / videoRatio );
  }
  else {
    var newHeight = minH;
    var newWidth = Math.ceil( newHeight * videoRatio );
  }

  video.style.width = newWidth + 'px';
  video.style.height = newHeight + 'px';
};

video.addEventListener('loadedmetadata', setVideoDimensions, false);
window.addEventListener('resize', setVideoDimensions, false);

```
