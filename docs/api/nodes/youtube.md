# YouTube
[![Version](https://img.shields.io/npm/v/@tiptap/extension-youtube.svg?label=version)](https://www.npmjs.com/package/@tiptap/extension-youtube)
[![Downloads](https://img.shields.io/npm/dm/@tiptap/extension-youtube.svg)](https://npmcharts.com/compare/@tiptap/extension-youtube?minimal=true)

这个扩展程序向编辑器中添加一个新的 YouTube 嵌入节点。

## 安装
```bash
npm install @tiptap/extension-youtube
```

## 设置

### inline
控制节点是否应该处理为内联或块级。

默认值： `false`

```js
Youtube.configure({
  inline: false,
})
```

### width
控制添加的视频的默认宽度。

默认值： `640`

```js
Youtube.configure({
  width: 480,
})
```

### height
控制添加的视频的默认高度。

默认值： `480`

```js
Youtube.configure({
  height: 320,
})
```

### controls
启用或禁用 YouTube 视频控件。

默认值： `true`

```js
Youtube.configure({
  controls: false,
})
```

### nocookie
为 YouTube 嵌入启用 nocookie 模式。

默认值： `false`

```js
Youtube.configure({
  nocookie: true,
})
```

### allowFullscreen
允许以 iframe 全屏播放。

默认值： `true`

```js
Youtube.configure({
  allowFullscreen: false,
})
```

### autoplay
让 iframe 在加载后开始播放视频。

默认值： `false`

```js
Youtube.configure({
  autoplay: true,
})
```

### ccLanguage
指定播放器将用于显示关闭字幕的默认语言。将参数的值设置为 ISO 639-1 两个字母的语言代码。例如，将其设置为 "es" 将使字幕为西班牙语。

默认值： `undefined`

```js
Youtube.configure({
  ccLanguage: 'es',
})
```

### ccLoadPolicy
如果将此参数的值设置为 `true`，即使用户关闭了字幕，也会默认显示关闭字幕。

默认值： `false`

```js
Youtube.configure({
  ccLoadPolicy: 'true',
})
```

### disableKBcontrols
禁用 iframe 播放器的键盘控件。

默认值： `false`

```js
Youtube.configure({
  disableKBcontrols: 'true',
})
```

### enableIFrameApi
通过 IFrame Player API 调用控制播放器。

默认值： `false`

```js
Youtube.configure({
  enableIFrameApi: 'true',
})
```

### origin
此参数为 IFrame API 提供了一个额外的安全措施，并且仅受 IFrame 嵌入支持。如果您使用 IFrame API，这意味着您将 `enableIFrameApi` 参数值设置为 `true`，您应始终将您的域指定为 `origin` 参数值。

默认值： `''`

```js
Youtube.configure({
  origin: 'yourdomain.com',
})
```

### endTime
此参数指定播放器应在视频开始播放后多少秒停止播放时间。例如，将其设置为 15 将使视频在 15 秒标记停止。

默认值： `0`

```js
Youtube.configure({
  endTime: '15',
})
```

### interfaceLanguage
设置播放器的界面语言。参数值是 ISO 639-1 两个字母的语言代码。例如，将其设置为 `fr` 将使界面为法语。

默认值： `undefined`

```js
Youtube.configure({
  interfaceLanguage: 'fr',
})
```

### ivLoadPolicy
将此设置为 1，将默认显示视频注释，而将其设置为 3 则不会默认显示视频注释。

默认值： `0`

```js
Youtube.configure({
  ivLoadPolicy: '3',
})
```

### loop
此参数在 IFrame 嵌入中有限的支持。要循环播放一个视频，请将循环参数值设置为 `true`，并将播放列表参数值设置为与 Player API URL 中已指定的相同视频 ID。

默认值： `false`

```js
Youtube.configure({
  loop: 'true',
})
```

### playlist
此参数指定要播放的视频 ID 的逗号分隔列表。

默认值： `''`

```js
Youtube.configure({
  playlist: 'VIDEO_ID_1,VIDEO_ID_2,VIDEO_ID_3,...,VIDEO_ID_N',
})
```

### modestBranding
在播放器的控制栏上禁用 Youtube 标志。请注意，当用户的鼠标指针悬停在播放器上时，暂停视频时仍将在右上角显示一个小标签。

默认值： `false`

```js
Youtube.configure({
  modestBranding: 'true',
})
```

### progressBarColor
此参数指定播放器视频进度条中将使用的颜色。请注意，将颜色参数设置为'white'将禁用'modestBranding'参数

默认值： `undefined`

```js
Youtube.configure({
  progressBarColor: 'white',
})
```

## Commands

### setYoutubeVideo(options)
在当前位置插入 YouTube iframe 嵌入。

```js
editor.commands.setYoutubeVideo({
  src: 'https://www.youtube.com/watch?v=dQw4w9WgXcQ',
  width: 640,
  height: 480,
})
```

#### Options

| 选项       | 描述                                    | 可选 |
| ---------- | --------------------------------------- | ---- |
| src        | YouTube 视频的 URL，可以是 YouTube 或 YouTube Music 链接 |      |
| width      | 嵌入宽度（覆盖默认选项，可选）                          | ✅   |
| height     | 嵌入高度（覆盖默认选项，可选）                          | ✅   |

## 源代码
[packages/extension-youtube/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-youtube/)

## 用法
https://embed.tiptap.dev/preview/Nodes/YouTube