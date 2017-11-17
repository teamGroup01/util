## 1.电子表格 
> [handsontable](https://handsontable.com/community-download.html)
```
html:
<link rel="stylesheet" type="text/css" href="http://docs.handsontable.com/pro/bower_components/handsontable-pro/dist/handsontable.full.min.css">
<link rel="stylesheet" type="text/css" href="http://handsontable.com/static/css/main.css">
<script src="http://docs.handsontable.com/pro/bower_components/handsontable-pro/dist/handsontable.full.min.js"></script>
	<button id="btn">export to csv</button>
	<div id="hot"></div>
js:
		var dataObject = [
	        {
	            id: 22,
	            flag: 'PHP',
	            currencyCode: 'PHP',
	            currency: 'Philippine Peso',
	            level: 46.3108,
	            units: 'PHP / USD',
	            asOf: '08/19/2015',
	            onedChng: 0.0012
	        }
	    ];
        var currencyCodes = ['EUR', 'JPY', 'GBP', 'CHF', 'CAD', 'AUD', 'NZD', 'SEK', 'NOK', 'BRL', 'CNY', 'RUB', 'INR', 'TRY', 'THB', 'IDR', 'MYR', 'MXN', 'ARS', 'DKK', 'ILS', 'PHP'];

        var flagRenderer = function (instance, td, row, col, prop, value, cellProperties) {
            var currencyCode = value;

	        while (td.firstChild) {
	            td.removeChild(td.firstChild);
	        }

	        if (currencyCodes.indexOf(currencyCode) > -1) {
	            var flagElement = document.createElement('DIV');
	            flagElement.className = 'flag ' + currencyCode.toLowerCase();
	            td.appendChild(flagElement);

	        } else {
	            var textNode = document.createTextNode(value === null ? '' : value);
	            td.appendChild(textNode);
	        }
	    };

	    var hotElement = document.querySelector('#hot');
	    var hotElementContainer = hotElement.parentNode;
	    var hotSettings = {
		    data: dataObject,
		    columns: [
		        {
		            data: 'id',
		            type: 'numeric',
		            width: 40
		        },
		        {
		            data: 'flag',
					renderer: flagRenderer
		        },
		        {
		            data: 'currencyCode',
		            type: 'text'
		        },
		        {
		            data: 'currency',
		            type: 'text'
		        },
		        {
		            data: 'level',
		            type: 'numeric',
		            format: '0.0000'
		        },
		        {
		            data: 'units',
		            type: 'text'
		        },
		        {
		            data: 'asOf',
		            type: 'date',
		            dateFormat: 'MM/DD/YYYY'
		        },
		        {
		            data: 'onedChng',
		            type: 'numeric',
		            format: '0.00%'
		        }
		    ],
		    // stretchH: 'all',
		    // width: 806,
		    // autoWrapRow: true,
		    // height: 487,
		    // maxRows: 22,
		    // rowHeaders: true,
		    // colHeaders: [
		    //     'ID',
		    //     'Country',
		    //     'Code',
		    //     'Currency',
		    //     'Level',
		    //     'Units',
		    //     'Date',
		    //     'Change'
		    // ],
		    // manualRowResize: true,
		    // manualColumnResize: true,
		    // manualRowMove: true,
		    // manualColumnMove: true,
		    // contextMenu: true,
		    // filters: true,
		    // dropdownMenu: true
		};

        var hot = new Handsontable(hotElement, hotSettings);
        var exportPlugin = hot.getPlugin('exportFile');
        exportPlugin.exportAsString('csv');
        
        document.getElementById('btn').addEventListener('click', () => {
        	exportPlugin.downloadFile('csv', {filename: 'MyFile'});
        })
```
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

## 4.[videojs](http://videojs.com/) / [参考](http://www.cnblogs.com/afrog/p/6689179.html)
```
<link href="http://vjs.zencdn.net/6.2.8/video-js.css" rel="stylesheet">
<script src="http://vjs.zencdn.net/6.2.8/video.js"></script>
<!-- If you'd like to support IE8 -->
<script src="http://vjs.zencdn.net/ie8/1.1.2/videojs-ie8.min.js"></script>
 1. 初始化
<video id="example_video_1" class="video-js">
    <p class="vjs-no-js">
      To view this video please enable JavaScript, and consider upgrading to a web browser that
    </p>
</video>
//设置参数
var options={
  autoplay: true,//自动播放
  sources: [{
      src: 'https://vjs.zencdn.net/v/oceans.mp4',
      type: 'video/mp4'  
  },{
      src: 'https://vjs.zencdn.net/v/oceans.webm',
      type: 'video/webm'
  }],
  poset: 'https://cdn.pixabay.com/photo/2017/09/01/21/53/blue-2705642__340.jpg',
  width: 800,
  height: 400
}
//设置加载完成的回调函数
var onready=function() {
   videojs.log('播放器装备完成')
   this.on('ended',function(){
     videojs.log('播放结束')
   })
}
var player = videojs('example_video_1',options,onready)

播放的时候自动隐藏标题，用户聚焦到播放器或暂停的时候显示标题？
//index.js
// Get the Component base class from Video.js
// 从Videojs中获取一个基础组件
var Component = videojs.getComponent('Component');

// The videojs.extend function is used to assist with inheritance. In
// an ES6 environment, `class TitleBar extends Component` would work
// identically.
// videojs.extend方法用来实现继承，等同于ES6环境中的class titleBar extends Component用法
var TitleBar = videojs.extend(Component, {

  // The constructor of a component receives two arguments: the
  // player it will be associated with and an object of options.
  // 这个构造函数接收两个参数：
  // player将被用来关联options中的参数
  constructor: function(player, options) {

    // It is important to invoke the superclass before anything else, 
    // to get all the features of components out of the box!
    // 在做其它事之前先调用父类的构造函数是很重要的，
    // 这样可以使父组件的所有特性在子组件中开箱即用。
    Component.apply(this, arguments);

    // If a `text` option was passed in, update the text content of 
    // the component.
    // 如果在options中传了text属性，那么更新这个组件的文字显示
    if (options.text) {
      this.updateTextContent(options.text);
    }
  },

  // The `createEl` function of a component creates its DOM element.
  // 创建一个DOM元素
  createEl: function() {
    return videojs.dom.createEl('div', {

      // Prefixing classes of elements within a player with "vjs-" 
      // is a convention used in Video.js.
      //给元素加vjs-开头的样式名，是videojs内置样式约定俗成的做法
      className: 'vjs-title-bar'
    });
  },

  // This function could be called at any time to update the text 
  // contents of the component.
  // 这个方法可以在任何需要更新这个组件内容的时候调用
  updateTextContent: function(text) {

    // If no text was provided, default to "Text Unknown"
    // 如果options中没有提供text属性，默认显示Text Unknow
    if (typeof text !== 'string') {
      text = 'Text Unknown';
    }

    // Use Video.js utility DOM methods to manipulate the content
    // of the component's element.
    // 使用Video.js提供的DOM方法来操作组件元素
    videojs.dom.emptyEl(this.el());
    videojs.dom.appendContent(this.el(), text);
  }
});

// Register the component with Video.js, so it can be used in players.
// 在videojs中注册这个组件，才可以使用哦.
videojs.registerComponent('TitleBar', TitleBar);


//style.css
.video-js .vjs-title-bar {
  color: red;
  
  /*
    By default, do not show the title bar.
  */
  display: none;
  font-size: 2em;
  padding: .5em;
  position: absolute;
  top: 0;
  right: 0;
  min-width: 80px;
  height: 40px;
  line-height: 40px;
}

/* 
  Only show the title bar after playback has begun (so as not to hide
  the big play button) and only when paused or when the user is 
  interacting with the player.
*/
.video-js.vjs-paused.vjs-has-started .vjs-title-bar,
.video-js.vjs-user-active.vjs-has-started .vjs-title-bar{
  display: block;
}

//设置
player.addChild('TitleBar',{text: '这里是标题'});

```
