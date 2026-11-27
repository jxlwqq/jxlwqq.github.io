---
layout: post
title: "小记：为开源项目增加一个新功能的开发历程"
date: 2018-08-23 11:09:00 +0800
categories: open-source php
---

> 本篇文章不是为了记开发流水账，而是想把**开发过程的遇到的问题以及解决思路**和大家进行交流和学习。我是一名普普通通的 PHP 工程师，希望对初级开发同学有所帮助。具体的心得体会见文末的**总结**。

本月初，我在 GitHub 上开源了一个自己的小项目：[chinese-typesetting](https://github.com/jxlwqq/chinese-typesetting)。这是一个纠正中文文案排版的 Composer 包。

[chinese-typesetting](https://github.com/jxlwqq/chinese-typesetting) 包含以下功能：

- 在中文与英文字母/用于数学、科学和工程的希腊字母/数字之间添加空格；
- 有限度的全角转半角（英文、数字、空格以及一些特殊字符等使用半角字符）；
- 修复错误的标点符号；
- 清除 HTML 标签的样式；
- 清除空的 HTML 标签；
- 清除段首缩进；

本周，公司开发事务不多，无加班，于是开始构思新功能**纠正英语专有名词大小写**的实现。

## 英语专有名词的数据来源

首先，面临的第一个问题是：

> 英语专有名词的数据从哪来？

我最先想到的是 Python 有一个自然语言处理的包 [NLTK](https://www.nltk.org/)，这个包有个名为 pos\_tag 的函数，可以用来识别并标注每个单词的词性，其中被标注为 NNP 或 NNPS 的单词就是专有名词（Proper Noun）。我猜想，NLTK 数据包里应该有一个对应的专有名词数据集，但是，苦于能力有限，我一直没有找到。

上述的路径走不通后，我又通过 Google 搜索，发现通过网络字典来获取数据是一条可行的方案。通过这一方法，终于在 [Wiktionary](https://en.wiktionary.org/w/index.php?title=Category:English_proper_nouns) 找到了英语专有名词列表。于是，利用 Python 写了一个[爬虫小脚本](https://github.com/jxlwqq/english-proper-nouns)，爬取了对应的数据。

最后，就是对爬取到的数据进行了一些整理和筛选。

筛选方案如下：

- 使用 `is_numeric()` 方法，剔除诸如 `007` 等词汇；
- 使用 `'/\W/'` 正则，剔除诸如 `ǃXóõ` 等词汇；
- 剔除 `strlen` 方法，剔除 `A` 等单字节词汇；
- 剔除跟 HTML、CSS、JavaScript 保留字冲突的词汇；

## 如何让使用者定制专有名词数据

最初的代码如下：

```php
/**
 * 专有名词使用正确的大小写
 * Correct English proper nouns.
 *
 * @param $text
 *
 * @return null|string|string[]
 */
public function properNoun($text)
{
    $dict = include __DIR__ . '/../data/dict.php';
    foreach ($dict as $noun) {
        $text = preg_replace("/\b{$noun}\b/i", $noun, $text);
    }
    return $text;
}
```

之后想到，如果使用这个方法的开发者想扩展或者忽略某些专有名词，那该怎么办呢？  
于是，我又将 `properNoun()` 方法改造如下：

```php
/**
 * 专有名词使用正确的大小写
 * Correct English proper nouns.
 *
 * @param $text
 * @param array $extend
 * @param array $ignore
 *
 * @return null|string|string[]
 */
public function properNoun($text, array $extend = [], array $ignore = [])
{
    $dict = include __DIR__ . '/../data/dict.php';
    if ($extend) {
        $dict = array_merge($dict, $extend);
    }
    if ($ignore) {
        $dict = array_diff($dict, $ignore);
    }

    foreach ($dict as $noun) {
        $text = preg_replace("/\b{$noun}\b/i", $noun, $text);
    }
    return $text;
}
```

## 如何改进和优化代码逻辑

我在写这个功能的时候，也在研究和参考一些现有开源项目的实现逻辑。在看到开源项目 [auto-correct](https://github.com/NauxLiu/auto-correct) 的一个 [commit](https://github.com/NauxLiu/auto-correct/commit/8e27d48bcd573bccbb2a3cd1b1ad55c094351916#diff-5b2d151c3e574c0d305d912285b01b9b) 上后（PS：这个 PR 是社区大神 [overtrue](https://github.com/overtrue) 提交的。），我又将 `properNoun()` 方法改造如下：

```php
public function properNoun($text, array $extend = [], array $ignore = [])
{
    $dict = include __DIR__ . '/../data/dict.php';
    if ($extend) {
        $dict = array_merge($dict, $extend);
    }
    if ($ignore) {
        $dict = array_diff($dict, $ignore);
    }
    foreach ($dict as $noun) {
        $text = preg_replace("/(?<!\.|[a-z]){$noun}(?!\.|[a-z])/i", $noun, $text);
    }
    return $text;
}
```

## 如何避免过度替换

在我以为就要大功告成的时候，我用之前写好的 PHPUnit 单元测试代码进行了测试，结果报出了错误，在上述方法中，如果传入的参数是包含 HTML 标签的富文本，那么 HTML 的元素、元素属性以及值都有可能会被替换。

如何避免过度替换这个问题呢？也就是说：

> 只替换文本，而忽略 HTML 标签及标签内部的内容？

我尝试写了好几套匹配方案，都失败了。最后还是请出了 Google 大神来帮忙。这里，搜索的**关键字**很重要，最好想把你要搜索的关键词翻译成对应的英文单词，这样搜索出的结果会令你更满意。结果我找到了解决方案：[Matching A Word / Characters Outside Of Html Tags](https://pureform.wordpress.com/2008/01/04/matching-a-word-characters-outside-of-html-tags/)。

通过上面这部文章的提示，我又将 `properNoun()` 方法改造如下：

```php
public function properNoun($text, array $extend = [], array $ignore = [])
{
    $dict = include __DIR__ . '/../data/dict.php';
    if ($extend) {
        $dict = array_merge($dict, $extend);
    }
    if ($ignore) {
        $dict = array_diff($dict, $ignore);
    }
    foreach ($dict as $noun) {
        // Matching proper nouns Outside Of Html Tags
        $text = preg_replace("/(?<!\.|[a-z]){$noun}(?!\.|[a-z])(?!([^<]+)?>)/i", $noun, $text);
    }
    return $text;
}
```

## 开发总结

- 学会\*\*\*\*；
- 善用 Google、Github 和 StackOverflow，这三样“神器”会帮你解决掉开发过程中遇到的绝大部分（或者说**所有**）问题；
- 学会一些 Google 搜索小技巧。例如将搜索关键字翻译成英语单词，这样的搜索结果会令你更满意；
- 英语真的很重要。最起码你应该在 Chrome 浏览器上安装一个 [Google 翻译](https://chrome.google.com/webstore/detail/google-translate/aapbdbdomjkkjkaonfhkkikfgjllcleb?hl=zh-CN) 的插件；
- PHPUnit 真的很有用，特别是在频繁增改功能或者需要代码重构的项目中。
- 不要让自己仅限于一个编程语言，学习另外一门或多门语言作为辅助，有益于拓展思路和开拓眼界。
- 多逛逛 Laravel China 这样的高品质社区；

## 最后的话

如果还有什么需要说的话，那就是求 Star 啦，哈哈哈哈哈。项目地址：<https://github.com/jxlwqq/chinese-typesetting> 。
