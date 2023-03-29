# Typography

[![Version](https://img.shields.io/npm/v/@tiptap/extension-typography.svg?label=version)](https://www.npmjs.com/package/@tiptap/extension-typography)
[![Downloads](https://img.shields.io/npm/dm/@tiptap/extension-typography.svg)](https://npmcharts.com/compare/@tiptap/extension-typography?minimal=true)

此扩展旨在使用正确的排版字符来帮助处理常见的文本模式。在幕后，所有规则都是输入规则。

## 安装

```bash
npm install @tiptap/extension-typography
```

## 规则

| 名称                  | 描述                               |
| ------------------- | ---------------------------------- |
| emDash              | 将双破折号 `--` 转换为短划线符 `—`. |
| ellipsis            | 将三个点 `...` 转换为省略号 `…`.   |
| openDoubleQuote     | “智能”开头的双引号。                  |
| closeDoubleQuote    | “智能”关闭双引号。                   |
| openSingleQuote     | ‘智能’开头的单引号。                  |
| closeSingleQuote    | ‘智能’关闭单引号。                   |
| leftArrow           | 将 <code><&dash;</code> 转换为左箭头 `←`. |
| rightArrow          | 将 <code>&dash;></code> 转换为右箭头`→`. |
| copyright           | 将 `(c)` 转换为版权符号 `©`.              |
| registeredTrademark | 将 `(r)` 转换为注册商标符号 `®`.           |
| trademark           | 将 `(tm)` 转换为注册商标符号 `™`.          |
| servicemark         | 将 `(sm)` 转换为服务商标符号 `℠`.           |
| oneHalf             | 将 `1/2` 转换为一半符号 `½`.               |
| oneQuarter          | 将 `1/4` 转换为四分之一符号 `¼`.           |
| threeQuarters       | 将 `3/4` 转换为四分之三符号 `¾`.            |
| plusMinus           | 将 `+/-` 转换为正负号 `±`.            |
| notEqual            | 将<code style="font-variant-ligatures: none;">!=</code> 转换为不等号 `≠`. |
| laquo               | 将 `<<` 转换为左指向双角引号 `«`.             |
| raquo               | 将 `>>` 转换为右指向双角引号 `»`.             |
| multiplication      | 将 `2 * 3` 或 `2x3` 转换为乘号 `2×3`. |
| superscriptTwo      | 将 `^2` 转换为上标二 `²`.                   |
| superscriptThree    | 将 `^3` 转换为上标三 `³`.                   |

## 键盘快捷键

| 命令             | Windows / Linux | macOS         |
| --------------- | --------------- | ------------- |
| undoInputRule() | `Backspace`     | `Backspace` |

## 源代码

[packages/extension-typography/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-typography/)

## 使用

https://embed.tiptap.dev/preview/Extensions/Typography

### 禁用规则

您可以配置包含的规则，甚至禁用其中一些规则，如下所示。

```js
import { Editor } from '@tiptap/core'
import Typography from '@tiptap/extension-typography'

const editor = new Editor({
  extensions: [
    // 禁用一些包含的规则
    Typography.configure({
      oneHalf: false,
      oneQuarter: false,
      threeQuarters: false,
    }),
  ],
})
```