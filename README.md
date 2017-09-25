# VideoJS框架学习
![GitHub](https://camo.githubusercontent.com/0af60e718ce6f8c9f31543c210af3a74e77681c6/687474703a2f2f766964656f6a732e636f6d2f696d672f6c6f676f2e706e67 "Picture")

# [Video.js - HTML5 Video Player](http://videojs.com "VideoJS.com")

# [Github-VideoJS](https://github.com/videojs "Github-VideoJS")
### 一、入门代码

1、导入CSS和JS

```html
<link href="//vjs.zencdn.net/5.19/video-js.min.css" rel="stylesheet">
<script src="//vjs.zencdn.net/5.19/video.min.js"></script>
```
2、Html代码
```html
<video
    id="my-player"
    class="video-js"
    controls
    preload="auto"
    poster="//vjs.zencdn.net/v/oceans.png"
    data-setup='{}'>
  <source src="//vjs.zencdn.net/v/oceans.mp4" type="video/mp4"></source>
  <source src="//vjs.zencdn.net/v/oceans.webm" type="video/webm"></source>
  <source src="//vjs.zencdn.net/v/oceans.ogv" type="video/ogg"></source>
  <p class="vjs-no-js">
    To view this video please enable JavaScript, and consider upgrading to a
    web browser that
    <a href="http://videojs.com/html5-video-support/" target="_blank">
      supports HTML5 video
    </a>
  </p>
</video>
```
3、JS代码
```js
var player = videojs('my-player');
```
```js
var options = {};
var player = videojs('my-player', options, function onPlayerReady() {
  videojs.log('Your player is ready!');

  // In this context, `this` is the player that was created by Video.js.
  this.play();

  // How about an event listener?
  this.on('ended', function() {
    videojs.log('Awww...over so soon?!');
  });
});
```
### 二、播放器组件与初始化

1、对于视频播放来说，常用的功能有：

播放   this.play()

停止   -- video没有stop方法，可以用pause 暂停获得同样的效果

暂停   this.pause()

销毁  this.dispose()

监听  this.on('click',fn)

触发事件this.trigger('dispose')

....

以上的this是指在onPlayerReady函数中执行。

2、默认支持的组件有以下这些：

```Player
Player
    PosterImage   //默认封面
    TextTrackDisplay
    LoadingSpinner
    BigPlayButton    //大播放按钮
    ControlBar    // 控制条
        PlayToggle   //播放暂停
        FullscreenToggle   //全屏
        CurrentTimeDisplay   //当前播放时间
        TimeDivider
        DurationDisplay
        RemainingTimeDisplay   //剩余播放时间
        ProgressControl   //时间轴
               SeekBar
               LoadProgressBar
               PlayProgressBar
               SeekHandle
        VolumeControl   //音量控制
              VolumeBar
              VolumeLevel
              VolumeHandle 
       PlaybackRateMenuButton  //播放速率
```
       
### 三、皮肤
要根据产品风格去设计播放器的样式，所以样式的重置是必不可少的。接下来说下在修改播放器样式时踩到的一些坑。

1.icon及颜色修改
通过覆盖样式去重置样式。比如修改颜色

```css
.vjs-control-bar{
    color:red;
    font-size:20px;
}
```

2.组件顺序
组件放置顺序的修改，在video.js中找到这段代码，将数组里的顺序修改下就可以了。

```
ControlBar.prototype.options_ = {
loadEvent: 'play',
children: ['playToggle', 'volumeMenuButton', 'currentTimeDisplay', 'timeDivider', 'durationDisplay', 'progressControl', 'liveDisplay', 'remainingTimeDisplay', 'customControlSpacer', 'playbackRateMenuButton', 'chaptersButton', 'subtitlesButton', 'captionsButton', 'fullscreenToggle']
};
```

3.hover提示
组件hover提示同理，找到源码修改就好了

```
k.prototype.controlText_ = "Play"     ------>     k.prototype.controlText_ = "播放"
k.prototype.controlText_ = "Fullscreen"   ------>   k.prototype.controlText_ = "全屏"
```

4.音量bar由横的变竖的

```
var options = {
       volumeMenuButton: {
            inline: false,//设置音量bar为竖直
            vertical: true//设置音量bar为竖直
       }
};

//初始化播放器
videojs(('#my-video', options, function() {
console.log('播放器初始化完成');    //回调函数
});
```
