# FramePlayer
序列帧图片播放插件，支持通过Canvas播放，可控制播放速度，可循环播放，甚至倒序播放。
## 如何使用
引入JS核心文件
```html
<script type="text/javascript" src="vframeplayer-min.js"></script>
 ```
在页面中插入DIV标签
```html
<div id="framePlayer"></div>
 ```
实例化vFramePlayer
```JS
//将所有图片放入一个数组
var imgArr = ["img/0.jpg","img/1.jpg","img/2.jpg"];
//实例化vFramePlayer
var framePlayer = new vFramePlayer({
    dom : document.getElementById("framePlayer"),
    imgArr : imgArr
});
```
## Options
实例化对象的时候，你可以使用以下参数配置插件：
- `dom` - 用于存放图片和CANVAS的DOM节点，该项必选
- `imgArr` - 图片序列数组，该项必选。类型：`Array`
- `fps` - 设置动画播放每秒显示帧频，该项可选。类型：`Number`，默认值：`25`
- `useCanvas` - 是否用CANVAS播放动画，该项可选。如果设置为`false`，则使用IMG播放。类型：`Boolean`，默认值：`true`
- `loop` - 循环播放次数，该项可选。不设置则不循环播放。类型：`Number`
- `yoyo` - yoyo球效果，配合`loop`使用，该项可选。如果设置为`true`，循环播放的时候会回播，类型：`Boolean`，默认值：`false`
```JS
//示例
var framePlayer = new vFramePlayer({
    dom : document.getElementById("framePlayer"),
    imgArr : imgArr,
    fps : 30,
    userCanvas : false,
    loop : 10,
    yoyo : true
});
```
## Methods
实例化完成后，你可以使用以下方法进行播放序列图动画：
- `play(start,end,options)` - 播放序列图动画
    - `start` - 播放开始帧，该项可选。类型：`Number`，默认值：`0`
    - `end` - 播放结束帧，该项可选。类型：`Number`，默认值为最后一帧
    - `options` - 播放参数，该项可选。类型：`Object`，参数[Options](#options)及`onComeplete`、`onUpdate`
        - `onComplete()` - 播放完成时执行的方法，该项可选。类型：`Function`
        - `onUpdate(frame,times,asc)` - 播放过程中执行的方法，该项可选。类型：`Function`，回调中的`frame`为当前帧，`times`为已播放次数，`asc`为是否升序播放
- `goto(i)` - 直接跳到第`i`帧，`i`必选。`i`类型：`Number`
- `pause()` - 暂停播放动画
- `stop()` - 停止播放动画，重置数据
- `destroy()` - 清除所有动画及监听事件
```JS
//示例
framePlayer.play(10,100,{
    yoyo:true,
    fps:30,
    loop:10,
    onComplete : function () {
        console.log("播放完成");
    },
    onUpdate : function (frame,times,asc) {
        console.log("当前播放第"+ frame +"帧");
        console.log("已经循环播放"+ times +"次");
        console.log("当前是否是升序播放："+ asc);
    }
)
```
## Events
播放事件的监听及取消监听的方法。
- `on(events,handler)` - 监听事件
    - `events` - 监听事件名称，类型：`String`，包括：
        - `"play"` - 开始播放
        - `"pause"` - 暂停动画
        - `"stop"` - 停止动画
        - `"update"` - 动画播放过程中
    - `handler` - 监听事件执行方法，类型：`Function`
- `one(events,handler)` - 监听一次事件，参数同`on()`
- `off(events,handler)` - 结束监听，参数同`on()`
```JS
//示例
framePlayer.on("play",function () {
    console.log("开始播放");
})
```
## Author
VML-LAB iorilp, RhineLiu
