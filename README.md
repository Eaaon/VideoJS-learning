# VideoJS框架学习
![GitHub](https://camo.githubusercontent.com/0af60e718ce6f8c9f31543c210af3a74e77681c6/687474703a2f2f766964656f6a732e636f6d2f696d672f6c6f676f2e706e67 "Picture")

# [Video.js - HTML5 Video Player](http://videojs.com "VideoJS.com")

# [Github-VideoJS](https://github.com/videojs "Github-VideoJS")

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
对于视频播放来说，常用的功能有：

1. 播放   this.play()

2. 停止   -- video没有stop方法，可以用pause 暂停获得同样的效果

3. 暂停   this.pause()

4. 销毁  this.dispose()

5. 监听  this.on('click',fn)

6. 触发事件this.trigger('dispose')

....

以上的this是指在onPlayerReady函数中执行。

```
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
