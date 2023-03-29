# 贡献

## 介绍
没有活跃的社区，Tiptap 就毫无意义。我们一直欢迎大家做出贡献。在您提交贡献之前，请务必了解以下信息：

## 欢迎的贡献
* 作为 bug 报告的失败回归测试
* 改进文档，比如修复拼写错误或添加新章节
* 为现有扩展添加新特性，比如新的可配置选项
* 对核心进行解释清晰、非破坏性的更改

## 不会合并的贡献
* 我们需要支持和维护的新扩展

## 提交您的想法
确保您先开一个 Issue 并概述您的想法。我们会尽快回复并告知合并您的贡献是否有机会。

## 配置开发环境
在官方仓库里 tinkering 还不算太难。您需要安装 [Git](https://github.com/git-guides/install-git)、[Node 和 NPM](https://nodejs.org/en/download/)。然后您需要执行以下步骤：

1. 将代码复制到本地：`$ git clone git@github.com:ueberdosis/tiptap.git`
2. 安装依赖：`$ npm install`
3. 启动开发环境：`$ npm run start`
4. 在您喜欢的浏览器中打开 http://localhost:3000。
5. 开始 tinkering！

## 我们的代码风格
我们使用了 eslint，以确保一致的代码风格。要检查错误，运行 `$ npm run lint`。提交 Pull Request 时也会进行检查。提交前确保通过代码风格检查。

## 检查错误
您的 Pull Request 将自动执行所有现有的测试。在发送 Pull Request 之前，请确保它们全部通过。使用 `$ npm run test` 运行所有测试，或使用 `$ npm run test:open` 运行单个测试（例如，当正在编写新测试时）。

## 创建您自己的扩展
如果您想创建和维护自己的扩展，可以使用 `create-tiptap-extension` CLI 工具。它将创建一个新的扩展样板文件，并包含所有必需的文件和构建过程。只需输入以下命令：

```bash
npm init tiptap-extension
```

如果您想让我们知道您的扩展，可以在 [Twitter](https://twitter.com/tiptap_editor) 或 [Discord](https://discord.gg/WtJ49jGshW) 上提醒我们。

## 其他问题
还有其他问题吗？在仓库中创建一个新 Issue 或讨论。我们会回复您。