# Tiptap for PHP
[![Packagist 上的最新版本](https://img.shields.io/packagist/v/ueberdosis/tiptap-php.svg)](https://packagist.org/packages/ueberdosis/tiptap-php)
[![总下载量](https://img.shields.io/packagist/dt/ueberdosis/tiptap-php.svg)](https://packagist.org/packages/ueberdosis/tiptap-php)

## 介绍
这是一个用于处理 [Tiptap](https://tiptap.dev/) 内容的 PHP 包。你可以将 Tiptap 兼容的 JSON 转换为 HTML，反之亦然，对你的内容进行清洁化或仅仅进行修改。

## 安装
你可以通过 Composer 安装该包：

```bash
composer require ueberdosis/tiptap-php
```

## 使用方法
该 PHP 包与 JavaScript 包有很多相似之处。如果你了解 Tiptap，PHP 语法会让你很容易上手。下面是一个简单的例子：

```php
(new Tiptap\Editor)
    ->setContent('<p>Example Text</p>')
    ->getDocument();

// 返回值:
// ['type' => 'doc', 'content' => …]
```

## 文档
PHP 包能够做很多事情，请查看 [GitHub 上的仓库](https://github.com/ueberdosis/tiptap-php) 了解更多信息。