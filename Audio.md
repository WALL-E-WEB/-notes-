### audio的方法

```
addTextTrack()    为音视频加入一个新的文本轨迹    
canPlayType()    检查指定的音视频格式是否得到支持    
load()    重新加载音视频标签    
play()    播放音视频    
pause()    暂停播放当前的音视频
```

### audio的属性

```js
audioTracks    返回可用的音轨列表（MultipleTrackList对象）    
autoplay    媒体加载后自动播放    
buffered    返回缓冲部件的时间范围(TimeRanges对象)    
controller    返回当前的媒体控制器（MediaController对象）    
controls    显示播控控件    
crossOrigin    CORS设置    
currentSrc    返回当前媒体的URL    
currentTime    当前播放的时间，单位秒    
defaultMuted    缺省是否静音    
defaultPlaybackRate    播控的缺省倍速    
duration    返回媒体的播放总时长，单位秒    
ended    返回当前播放是否结束标志    
error    返回当前播放的错误状态    
initialTime    返回初始播放的位置    
loop    是否循环播放    
mediaGroup    当前音视频所属媒体组 (用来链接多个音视频标签)    
muted    是否静音    
networkState    返回当前网络状态    
paused    是否暂停    
playbackRate    播放的倍速    
played    当前播放部件已经播放的时间范围(TimeRanges对象)    
preload    页面加载时是否同时加载音视频    
readyState    返回当前的准备状态 {
&emsp;&emsp;&emsp;&emsp;0: HAVE_NOTHING 没有准备就绪的状态
&emsp;&emsp;&emsp;&emsp;1: HAVE_METADATA 关于音频就绪的元数据
&emsp;&emsp;&emsp;&emsp;2: HAVE_CURRENT_DATA 当前可用，但下一帧不确定
&emsp;&emsp;&emsp;&emsp;3: HAVE_FUTURE_DATA 当前和下一帧可用
&emsp;&emsp;&emsp;&emsp;4: HAVE_ENOUGH_DATA 有足够的数据支持播放
}   
seekable    返回当前可跳转部件的时间范围(TimeRanges对象)    
seeking    返回用户是否做了跳转操作    
src    当前音视频源的URL    
startOffsetTime    返回当前的时间偏移(Date对象)    
textTracks    返回可用的文本轨迹(TextTrackList对象)    
videoTracks    返回可用的视频轨迹(VideoTrackList对象)    
volume    音量值

```

### audio的钩子

```js
abort    当音视频加载被异常终止时产生该事件    
canplay    当浏览器可以开始播放该音视频时产生该事件    
canplaythrough    当浏览器可以开始播放该音视频到结束而无需因缓冲而停止时产生该事件    
durationchange    当媒体的总时长改变时产生该事件    
emptied    当前播放列表为空时产生该事件    
ended    当前播放列表结束时产生该事件    
error    当加载媒体发生错误时产生该事件    
loadeddata    当加载媒体数据时产生该事件    
loadedmetadata    当收到总时长，分辨率和字轨等metadata时产生该事件    
loadstart    当开始查找媒体数据时产生该事件    
pause    当媒体暂停时产生该事件    
play    当媒体播放时产生该事件    
playing    当媒体从因缓冲而引起的暂停和停止恢复到播放时产生该事件    
progress    当获取到媒体数据时产生该事件    
ratechange    当播放倍数改变时产生该事件    
seeked    当用户完成跳转时产生该事件    
seeking    当用户正执行跳转时操作的时候产生该事件    
stalled    当试图获取媒体数据，但数据还不可用时产生该事件    
suspend    当获取不到数据时产生该事件    
timeupdate    当前播放位置发生改变时产生该事件    
volumechange    当前音量发生改变时产生该事件    
waiting    当视频因缓冲下一帧而停止时产生该事件

```



# 音频相关名词解释

## 音频:

```
耳可以听到的声音频率在20HZ~20kHz之间的声波
```

## 采样频率:

```
指每秒钟取得声音样本的次数。
采样频率越高,声音的质量也就越好,声音的还原也就越真实，但同时它占的资源比较多。
22050Hz 的采样频率是常用的, 
44100Hz 是CD音质, 
超过48000或96000的采样对人耳已经没有意义.
双声道(stereo), 采样就是双份的, 文件也差不多要大一倍.
```

## 采样位数:

```js
用来衡量声音波动变化的一个参数，
也可以说是声卡的分辨率;
每个采样数据记录的是振幅, 采样精度取决于采样位数的大小:
1 字节(也就是8bit) 只能记录 256 个数, 也就是只能将振幅划分成 256 个等级;
2 字节(也就是16bit) 可以细到 65536 个数, 这已是 CD 标准了;
4 字节(也就是32bit) 能把振幅细分到 4294967296 个等级, 实在是没必要了

```

