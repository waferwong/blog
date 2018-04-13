
# 需求
自动播放
循环
一致界面
控制条定制

```
<video id="player" class="video-js vjs-default-skin vjs-big-play-centered" width="100%" height="240px" controls style="object-fit:fill" webkit-playsinline="true" x-webkit-airplay="true" playsinline="true" x5-video-player-type="h5" x5-video-orientation="h5" x5-video-player-fullscreen="true" preload="auto" src="https://imagedev.pawjzs.com:4443/college/course/video/20161215001.mp4"> </video>
```

## `<video>`
[视频播放的那些事 | Taobao FED | 淘宝前端团队](http://taobaofed.org/blog/2016/05/23/video-player/)
[html5--移动端视频video的android兼容，去除播放控件、全屏等 - 前端填坑 - SegmentFault 思否](https://segmentfault.com/a/1190000006857675)

### iOS
在 iOS 上，APP 都是使用的系统自带的浏览器进行页面渲染，video 播放视频的效果是统一的，只需要考虑不同的 iOS 版本是否有不一致的地方。
iOS10+
playsinline
<iOS10
webkit-playsinline
加了playsinline后，在 iOS 9 的上出现只能听到声音不能看到画面的问题
[https://github.com/bfred-it/iphone-inline-video](https://github.com/bfred-it/iphone-inline-video)
### 微信

## 全屏

## 事件
video 支持的事件很多，但在有些事件在不同的系统上跟预想的表现不一致，在尝试比较之后，使用 timeupdate 和 ended 这两个事件基本可以满足需求



## vedio.js
[videojs/video.js: Video.js - open source HTML5 & Flash video player](https://github.com/videojs/video.js)

主要使用video.min.css、video.min.js这两个文件。
如果是PC，要求兼容到ie9以下，那么需要ie8、video-js.swf这两个文件。
由于主题中有一些字体图标，所以要用到font文件中的字体文件
如果有提示文字相关，做本地化，则要用到lang中的语言文件
videojs 4.9开始支持`<audio>`标签，支持的方式就是，播放的时候封面不会消失。

### 样式
class="video-js vjs-big-play-centered"

[Video.js Default Skin](https://codepen.io/heff/pen/EarCt)
[Video.js Sublime Skin](https://codepen.io/zanechua/pen/GozrNe)

暂停时显示播放按钮
.vjs-paused .vjs-big-play-button,
.vjs-paused.vjs-has-started .vjs-big-play-button {
    display: block;
}

放按钮变○圆形
``` css
.video-js .vjs-big-play-button{
    font-size: 2.5em;
    line-height: 2.3em;
    height: 2.5em;
    width: 2.5em;
    -webkit-border-radius: 2.5em;
    -moz-border-radius: 2.5em;
    border-radius: 2.5em;
    background-color: #73859f;
    background-color: rgba(115,133,159,.5);
    border-width: 0.15em;
    margin-top: -1.25em;
    margin-left: -1.75em;
}
/* 中间的播放箭头 */
.vjs-big-play-button .vjs-icon-placeholder {
    font-size: 1.63em;
}
/* 加载圆圈 */
.vjs-loading-spinner {
    font-size: 2.5em;
    width: 2em;
    height: 2em;
    border-radius: 1em;
    margin-top: -1em;
    margin-left: -1.5em;
}
```

点击屏幕切换播放/暂停
.video-js.vjs-playing .vjs-tech {
    pointer-events: auto;
}

### 宽高
[Creating Intrinsic Ratios for Video · An A List Apart Article](http://alistapart.com/article/creating-intrinsic-ratios-for-video)
{ fluid: true }
css  .vjs-fluid,.vjs-4-3,.vjs-16-9
这个还需要给video元素设置一个起始的宽高，不然开始的图片看不见。

### playlist
[brightcove/videojs-playlist: Playlist plugin for videojs](https://github.com/brightcove/videojs-playlist)

### flash html5 failback
[Playback](http://docs.videojs.com/docs/guides/tech.html)技术用来在浏览器或插件中播放视频或音频文件，如果是h5会使用video或audio元素，如果是flash，会定义一个flash播放器。不止flash，还支持Silverlight、Quicktime等技术播放。可以在元素中直接定义data-setup。指定支持的技术。

```
videojs("videoID", {
  techOrder: ["html5", "flash", "other supported tech"]
});
```

这里默认的规则是，会用第一项技术去播放，不行再使用后面的选项。比如上方html5写在第一位，就会用html5播放所有的视频。如果我们想flash优先，放在前面即可：

```
 data-setup='{ "techOrder": ["flash","html5"] }'
```

在页面元素中你会发现，video.js给我们使用的flash对象了。

### 播放控件
禁用控件
``` javascript
var options = {
    controls: 'control',
    preload: 'none',
    width: '856',
    height: '508',
    controlBar: {
        volumeBar: false,
        playToggle: false
    }
};
```
更改控件顺序
``` javascript
var options = {
    controls: 'control',
    preload: 'none',
    width: '856',
    height: '508',
    controlBar: {
        children: [
            {
                name: 'playToggle'
            },
            {
                name: 'progressControl'
            },
            {
                name: 'currentTimeDisplay'
            },
            {
                name: 'timeDivider',
            },
            {
                name: 'durationDisplay'
            },
            // 竖直的音量面板
            {
                name: 'volumePanel',
                inline: false,
            },
            {
                name: 'fullscreenToggle'
            },
        ]
    }
};
```
