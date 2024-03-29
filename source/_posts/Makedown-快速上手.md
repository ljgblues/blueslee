---
title: Makedown 快速上手
tags:
  - Markdown
  - Blog
categories:
  - Blog
  - Markdown
comments: true
date: 2019-11-13 16:19:00
top: 10
sticky: 10
password:
---
# 通用规则

## 文件

### 文件扩展名

使用 .md.
解释: 为什么不使用 .mkd 或者 .markdown?

- 更短
- 更加流行
- 没有明显冲突

<!-- more -->

### 文件名

文件名建议使用如下的风格:
- 用小写代替大写
- 把开头 `the`, `a`, `an` 除去
- 用连字符代替标点和空格
- 用一个连字符代替连续多个连字符，当多个连字符出现时，只使用一个
- 不在文件名前后使用连字符

建议使用:
`file-name.md`
不建议, 多个连续的连字符:
`file--name.md`
不建议, 包围的连字符:
`-file-name-.md`
解释: 为何不使用下划线和驼峰大小写？连字符是现在最流行的网址分隔符，并且 Markdown 文件在上下文中经常使用:
- 可能在同一个项目中有连字符分割的HTML文件使用Markdown相同的目录。
- 文件名会被直接使用到 URL 中. 比如: GitHub blobs.

## 空白

### 新行

- *不要* 使用连续两空行，也就是说，*不要* 连续使用两个换行符，除非是在代码块中不得已而必须出现。
- 以回车换行结束文件。*不要* 在文件结束时留下空行。
- *不要* 在行尾留空格除非是在行尾空出两个空格插入换行符。

建议使用:
```
- list
- list

# Header
```
建议, 代码区块:
```
The markup language X requires you to use triple newlines to separate paragraphs:

    p1


    p2
```
不建议：
```
- list
- list


# Header
```
解释: 多空行占用更多的竖直屏幕空间，并且会严重影响到可读性。

### 句子结束空格

句子结束使用一个空格
建议使用:
```
First sentence. Second sentence.
```
不建议, 使用2个空格:
```
First sentence.  Second sentence.
```
解释: 相比于`使用两个空格`的优点:
- 容易编辑
- 通常不是必须的，如果使用 wrap:inner-sentence or wrap:sentence
- space-sentence:2 对可读性造成一种错误的感觉，因为忽略了输出的 HTML 文件。
- 容易查看一句话的结束

## 自动换行

尝试将一行限制在 80 个字符以下，将长段落按照以下的逻辑分开，例如:
- 句子: 一句话结束 . 之后, 问句问号 ? 或者感叹句 ! 之后
- [子句](clauseshttp://www.oxforddictionaries.com/words/clauses): 在单词 and, which, if ... then, 逗号 , 之后
- [短语 phrases](http://www.oxforddictionaries.com/words/phrases)

一行中超过80个字符是可以接受的，但是记住长句子不适合阅读，并且在 git diff 中会很难看。

设置你的文本编辑器对 Markdown 文件一行*不要* 超过80字符，以免忘记。

建议使用:
```
This is a very very very very very very very very very very very very very long not wrapped sentence.
Second sentence of of the paragraph,
third sentence of a paragraph
and the fourth one.
```
解释:

- Diffs 工具看起来更好, 因为一个子句的修改在 diff 工具中显示为一行修改.
- 临时的换行不会降低对 Markdown 文件的可读性， 因为唯一的语言特性，可以缩进表示层次结构的就是嵌套列表。
- 现在除了 GitHub 在 README 和评论中将单独一行解释成回车。 没有其他主流的解释引擎这么做，使用换行是非常安全的。
- 一些工具对较长的一行不友好，比如 Vim 并且 git diff 默认并不换行. 这些不友好都可以通过配置除去，对于git，使用 git config --global core.pager 'less -r' 对于Vim可以使用 set wrap 来自动换行.

缺点:

- 需要在写作时增加顾虑，尤其是在修改代码的时候。
- Markdown 看起来和渲染输出不同, 输出没有换行符。
- 手动的换行可以让 Markdown 比生成的文档更加易读， 当然这样做的同时，也造成了一种虚假的可读性错觉，让人感觉没有长段落。
- 需要用户拥有使用可编程文本编辑器，类似 Vim，可以通过配置来换行。[EditorConfig gave it WONTFIX](https://github.com/editorconfig/editorconfig/issues/168)

## 代码

### Shell中美元符号

*不要* 在 shell 代码前加 $ 符号，除非你想要展示命令的输出。
如果目的是表明确切的语言，那么直接在代码前标明。
解释: 复制粘贴比较困难，不利于阅读。
建议使用:
```
echo a
echo a > file
```
不建议：
```
$ echo a
$ echo a > file
```
建议, 展示输出:
```
$ echo a
a
$ echo a > file
```
建议, 在代码前标明代码语言:
```
Use the following Bash code:
echo a
echo a > file
```
### 标记代码内容

使用代码块，或者行内代码：
- 可执行文件。 比如：
```
`gcc` is the best compiler available.
```
注意将工具名字和项目工程名字区别开来。比如： `gcc` vs GCC.
- 文件路径
- 程序版本号
- 大写的缩写解释:
```
xinetd stands for `eXtended Internet daemon`
```
- 其他和电脑相关的术语，想要单独标明
*不要*标记为代码：
项目名。 比如： GCC
函数库名。比如： libc, glibc

### 拼写和语法
使用正确的拼写和语法。
尽量选用英语，更准确的说美式英语。 解释: 美式英语使用者占有最大的GDP，尤其是在计算机行业。
类似 URL 或者代码，添加代码标记，这样拼写检查程序会自动忽略。
注意大小写敏感的拼写错误，尤其是项目名，品牌名，或者缩写。
- 建议使用: URL, LinkedIn, DoS attack
- 不建议： url, Linkedin, dos attack

一旦有疑惑，尽量选用和维基百科相同的缩写。
避免使用非正式的缩写:

- 建议使用: biography, repository, directory
- 不建议： bio, repo, dir

# 区块

## 换行符

避免使用换行符, 因为他们没有被广泛认可的语义。
在少数确实需要使用的时候，在行尾使用两个空格。

## 标题

### atx风格

建议使用:
```
# Header 1

## Header 2

### Header 3
```
不建议：
```
Header 1
========

Header 2
--------

### Header 3
```

- 解释: 相比 Setex 优势有:
 - 容易书写，因为在 Setex 中，为了好看需要书写和标题相同数量的符号
 - 可以生成所有的等级，而 Setex 只能生成两种等级
 - 只占用一行，而 Setex 占用两行
 - 更加明显。 Not very important if you have syntax highlighting.

- 在 `#` 和标题之间加入一个空格.
建议使用:
```
# Header
```
 不建议：
```
#Header

#..Header
```

- *不要* 使用闭合的`#`.
建议使用:
```
# Header
```
 不建议：
```
# Header #
```

 解释: 容易维护。
- *不要* 在`#`前加入空格.
建议使用:
```
# Header
```
 不建议：
```
.# Header
```

- *不要* 跳跃使用标题等级.
建议使用:
```
# Header 1

## Header 2
```
 不建议：
```
# Header 1

### Header 3
```

- 在标题上下用空行隔开，除非标题在文档开头。
建议使用:
```
Before.

# Header 1

## Header 2

After.
```
 不建议：
```
Before.
# Header 1

## Header 2
After.
```

- 避免 在相同 Markdown 文件中使用相同的标题.
解释: 许多的 Markdown 解释器会依据标题的内容生成标题的IDs。
建议使用:
```
# Dogs

## Anatomy of the dog

# Cats

## Anatomy of the cat
```
 不建议：
```
# Dogs

## Anatomy

# Cats

## Anatomy
```

### 顶级标题

如果你想要 HTML 直接输出，这样唯一的`h1`标记就是输出的第一件事，并且会成为文档的标题。这就是HTML的顶级标题。
`h1`标题的产生受到使用的 Markdown 引擎的直接影响： 一些引擎会从元数据（metadata）中产生标题，比如 Jekyll 就是从 front-matter 中产生标题。
将顶级标题保存为元数据（metadata）可以更加方便的在其他地方使用， 比如，在全局索引中，但也有缺点，比如降低了可读性和移植性。
如果目的不是生成顶级标题， include it in your markdown file. E.g., GitHub.
索引文件中的顶级标题比如`README.md`或者`index.md`应该作为他们父目录的标题。
顶级标题的缺点：

- 占用了一级标题。这就意味只剩下5个层级标题可以使用。 并且这样每一个新的标题就会多使用一个 `# `符号,这样看起来不好。

- 重复了文件名, 通常已经可以直接从 URL 中读到。 在大多数的情况下，文件名可以直接转换成顶级标题， 比如: 从 some-filename.md 到 Some filename.

顶级标题的优点:

- 比URL更加易读，尤其是对非技术出身用户。

### 标题大小写

- 标题开头使用大写字母，除非标题内容总是以小写出现, 例如，计算机代码。
建议使用:
```
# Header
```
 建议使用, 代码通常以小写开始：
```
# int main
```
 不建议：
```
# header
```
- 其他字母按照句子中原始大小写。
建议使用:
```
# The header of the example
```
 不建议：
```
# The Header of the Example
```
例外,[首字大写](http://en.wikipedia.org/wiki/Title_case#Title_case) 对 [顶级标题](http://einverne.github.io/markdown-style-guide/zh.html#top-level-header) 可选择性支持。 请异常谨慎地使用, in cases where typographical perfection is important, 比如：项目的 README .
解释: 为什么对所有标题[首字大写](http://en.wikipedia.org/wiki/Title_case#Title_case)? 如果要决定句子中每一个单词大小写会花费太多精力。

### 标题结尾

显示标题的内容，而不是用新标题和水平线紧随其后：
```
# Header

Content

---

Outside header.
```
### 标题长度

保证标题越短越好。
避免使用长句子，总结长句子作为标题，然后将长句子作为标题下的第一小节。
解释: 以后引用方便，尤其是自动生成 IDs 或者生成 TOC 。
建议使用:
```
# Huge header

Huge header that talks about a complex subject.
```
不建议：
```
# Huge header that talks about a complex subject
```
### 标题结尾标点
*不要* 在标题中以`:`结尾。
解释: 每一个标题都是接下来内容的简介，这也就正是冒号的作用。
*不要* 在标题中以`.`结尾。
解释: 每一个标题都包含一个简短的句子，也就不需要句号来分隔他们。
建议使用:
```
# How to do make omelet
```
不建议：
```
# How to do make omelet:
```
不建议：
```
# How to do make omelet.
```
### 标题同义词
标题用作用户索引的关键词。
正由于这个原因，你可能希望在标题中用多个关键词。
要做到这一点，简单的创建一个同义词标题在主标题之前，并且标题下不包含内容。
比如：
```
# Purchase

# Buy

You give money and get something in return.
```
每一个同层级的空标题都假定是同义的。如果层级不一样，那就是另外的含义：
```
# Animals

## Dog
```

## 引用

- 在符号 `>` 后面接一个空格。
建议使用:
```
> a
```
 不建议：
```
>a
```
 不建议, 2个空格:
```
>  a
```
- 在每一行使用 > 符号，包括换行的句子。
建议使用:
```
> Long line
> that was wrapped.
```
 不建议：
```
> Long line
that was wrapped.
```
- *不要* 在单独的引用中使用空行。
建议使用:
```
> a
>
> b
```
 不建议：
```
> a

> b
```

## 列表

### 标记

#### 无序

使用连字符.
建议使用：
```
- a
- b
```
不建议：
```
* a
* b
+ a
+ b
```
解释:
- 星号 * 可能和加粗和斜体符号产生混淆。
- 加号 + 不流行。

#### 有序

尽量选用 `1. `来标记有序的列表, 除非你打算通过数字在相同 Markdown 文件或者外部文件中引用他们。
尽量使用无序的列表，除非有通过数字引用的需求。
最佳则是从来不通过序号来引用他们：
```
- a
- c
- b
```
较好的方法, 仅仅使用 1.:
```
1. a
1. c
1. b
```
较差的方法, *不要* 通过序号来标注列表项的顺序:
```
1. a
2. c
3. b
```
可接受的, 使用文本引用:
```
The ouput of the `ls` command is of the form:

    drwx------  2 ciro ciro        4096 Jul  5  2013 dir0
    drwx------  4 ciro ciro        4096 Apr 27 08:00 dir1
    1           2

Where:

1. permissions
2. number of files directory contains
```
可接受，通过外部 markdown 文件引用:
```
Terms of use.

1. I will not do anything illegal.
2. I will not do anything that can harm the website.
```
解释:
- 如果你想要改变列表中的一个列表项，你*不要* 修改它下面的列表项。
 Diffs 工具只会显示被修改的重要的内容。
- 如果序列有两位，也不需要额外注意，内容保持一致。 比如：下面不对齐：
```
9. a
10. b
```
- 如果新列表项被加入，引用会破坏。尽量减少这种问题：
 - 保证引用靠近列表，这样作者会更少可能的忘记去更新
 - 当从外部引用时，总是引用到一个固定版本的 markdown 文件
 
### 列表项中的空格

列表项标记前总是留有一个空格。
建议使用:
```
- a

  b

- c
```
不建议, 两个空格:
```
-  a

   b

-  c
```

### 列表内容的缩进

列表中内容的缩进层级必须和第一个列表项一致：
建议(如果符合列表标记之后的空格):
```
- item 1

  Content 1

- item 2

  Content 2
```
不建议：
```
- item 1

    Content 1

- item 2

    Content 2
```

避免开始直接使用缩进的代码列表项，因为这样不容易实现。[CommonMark states that](http://spec.commonmark.org/0.12/#example-176)一个单独的空格需要加入:
```
-     code

  a
```
### 列表中的空行

如果每一个列表项只有一行, *不要* 在列表项之间增加空行，否则，在每一个列表项之间增加空行。
建议使用, single lines:
```
- item 1
- item 2
- item 3
```
不建议, single lines:
```
- item 1

- item 2

- item 3
```
多行情况下，建议使用:
```
- item that
  is wrapped

- item 2

- item 3
```
多行情况下，不建议:
```
- item that
  is wrapped
- item 2
- item 3
```
建议使用, 多行:
```
- item 1

  - item 11
  - item 12
  - item 13

- item 2

- item 3
```
不建议, 多行:
```
- item 1

  - item 11
  - item 12
  - item 13

- item 2
- item 3
```

解释: 如果没有空行，很难分别多行的列表项开始和结束。

### 列表外的空行

列表外建议留有一空行。
建议使用:
```
Before.

- list
- list

After.
```
不建议：
```
Before.
- item
- item
After.
```

### 列表项首字母大小写

每一个 list 使用原来在句子中的大小写.
建议使用:
```
I want to eat:

- apples
- bananas
- grapes
```
因为它可以被如下替换：
```
I want to eat apples
I want to eat babanas
I want to eat grapes
```
建议使用:
```
To ride a bike you have to:

- get on top of the bike. This step is easy.
- put your foot on the pedal.
- push t the pedal. This is the most fun part.
```
因为它可以被如下替换：
```
To ride a bike you have to get on top of the bike. This step is easy.
To ride a bike you have to put your foot on the pedal.
To ride a bike you have to push the pedal. This is the most fun part.
```
建议使用:
```
# How to ride a bike

- Get on top of the bike.
- Put your feet on the pedal.
- Make the pedal turn.
```
因为它可以被如下替换：
```
# How to ride a bike

Get on top of the bike.
Put your feet on the pedal.
Push the the pedal.
```
### 列表项结尾标点

列表项结尾标点，除非:

- 包含多个句子或者短语
- 以大写字母开头

否则, 如果以句号结尾的话，省略标点.
建议使用:
```
- apple
- banana
- orange
```
不建议使用:
```
- apple.
- banana.
- orange.
```
建议使用:
```
- go to the market
- then buy some fruit
- finally eat the fruit
```
建议使用, 不以句号结尾，而是以其他标点结尾：
```
- go to the marked
- then buy fruit?
- of course!
```
不建议, 多个句子时末尾不加标点:
```
- go to the market
- then buy some fruit. Bad for wallet
- finally eat the fruit. Good for tummy
```
建议使用:
```
- go to the market
- then buy some fruit. Bad for wallet.
- finally eat the fruit. Good for tummy.
```
注意：没有任何理由阻止，一个列表项以句号结尾，另一个列表项没有。

不建议, 多段落:
```
- go to the market

- then buy some fruit

  Bad for wallet

- finally eat the fruit

  Good for tummy
```
建议使用:
```
- go to the market

- then buy some fruit.

  Bad for wallet.

- finally eat the fruit.

  Good for tummy.
```
不建议, 如果以大写字母开头，添加标点:
```
- Go to the market
- Then buy some fruit
- Finally eat the fruit
```
建议使用:
```
- Go to the market.
- Then buy some fruit.
- Finally eat the fruit.
```
## 定义列表

*避免* 使用定义列表扩展，因为他并没有被多数实现，也没有出现在 CommonMark.
相反, 使用:

- 格式化列表:

 - 用加粗，链接，或者代码，格式化需要定义的内容
 - 将内容和定义使用冒号和空格分割 `:.`
 - *不要* 对齐定义，这样难以维护，并且不会显示在 HTML 输出

建议使用:
```
- **apple**: red fruit
- **dog**: noisy animal
```
建议使用:
```
- **apple**: red fruit.

  Very tasty.

- **dog**: noisy animal.

 Not tasty.
```
建议使用:
```
- [apple](http://apple.com): red fruit
- [dot](http://dog.com): red fruit
```
建议使用:
```
- `-f`: force
- `-r`: recursive
```
不建议, 没有冒号:
```
- **apple** red fruit
- **dog** noisy animal
```
不建议, 在术语和冒号之间有空格:
```
- **apple** : red fruit
- **dog** : noisy animal
```
不建议, 定义对齐:
```
- **apple**: red fruit
- **dog**:   noisy animal
```
- headers.

建议使用:
```
# Apple

Red fruit

# Dog

Noisy animal
```
## 代码区域

### 可选 code:fenced

仅仅使用 fenced code blocks.
和缩进代码区块比较：

- 不足: 不是标准 markdown 语法, 因此缺少移植性，但是加入到CommonMark.
- 优点: 实现方式多, 包括 GitHub’s, 并且允许指定代码的语言。

*不要* 缩进 fenced code blocks.
总是指定代码的语言。
建议使用:
```ruby
a = 1
```
不建议：
```
a = 1

```
### 可选 code:indented

仅仅使用缩进代码区域。
代码区域缩进4个空格。

代码区块必须以一空行隔开。
尽量在代码块之前使用冒号结束短语`:`。
建议使用:
```
use this code to blow up your PC:

    sudo rm -rf /
```
不建议, 没有冒号
```
use this code to blow up your PC

    sudo rm -rf /
```
## 水平横线

*不要* 使用水平线除非表明[End of a header](http://einverne.github.io/markdown-style-guide/zh.html#end-of-a-header).
解释:

- 标题比区块更好，因为标题就是区块的开始，并且说明了区块的内容。
- 水平线没有可接受的语义。 这份风格指南给了语义。

使用 3 个无空格连字符:
```
---
```
## 表格

扩展.

- 用一空行包围表格。
- *不要* 缩进表格。
- 用 `| `包裹表格的每一行。
- 竖直对齐所有表格边框。
- 将标题和内容用连字符分割，用对齐的 `|`。
- `|` 周围必须要有一个空格，除非是外部的 `|`。
- 列的宽度通过列中最长的单元格确定。

建议表格:
```
Before.

| h    | Long header |
|------|-------------|
| abc  | def         |
| abc2 | def2        |

After.
```
解释:

- 不对齐的表格很容易书写，但是对齐的表格更加易读，并且人们读代码比编辑要更多。
- 开始的 `|` 更加容易看出表格的开始和结束。结尾的` | `让人看起来更加舒服，因为对称。
- 这些工具让表格对齐更加容易。比如，Vim 有 [Tabular plugin](https://github.com/godlygeek/tabular)插件，这个插件让我们可以使用 `:Tabular /| `来使整个表格对齐。
- 为什么在连字符分割行 `|` 没有空格包围, 比如: `|---| `而不是 `| - |`? 没有空格看起来更好，在GitHub可行， 缺点: 编辑器中自动对齐实现困难，因为对于分割行需要特殊的规则。

## 分离相连的列表

分离连续:

- 列表
- 缩进的代码块
- 引用
- 列表之后跟随额外的代码块

使用一个空白的 HTML 注释 `<!-- -->`.
```
- list 1
- list 1

<!-- -->

- list 2
- list 2
```
```
    code 1
    code 1

<!-- -->

    code 2
    code 2
```
```
> blockquote 1
> blockquote 1

<!-- -->

> blockquote 2
> blockquote 2
```
```
- list
- list

<!-- -->

    code outside list
    code outside list
```

# Span元素

*不要* 使用内部空格。
建议使用:
```
**bold**
`code`
[link](http://a.com)
[text][name]
```
不建议：
```
** bold **
` code `
[ link ]( http://a.com )
[text] [name]
```
对于空格至关重要的行内代码：

- 在写作过程中解释空格存在的必要性
- 如果可能在空格之后加入其他内容

建议使用:
`使用连字符并跟随一个空格来表示无序列表。`
解释: 大多数的浏览器不会生成包围的空格，或者复制的时候不会将他们添加到粘贴板。

## 链接

### 参考样式链接

链接:
- 使用结尾的`[]`隐式链接：
 建议使用:
```
[a][]
```
 不建议：
```
[a]
```
解释: 省略`[]`大多数主要的实现都可以使用，但是这种方式并没有在文档中有实现，原始 Markdown 也没有提到。

定义:

- 必须写到文件末
- 必须以ID字符顺序排列
- *不要* 使用尖括号包裹URL
- align URLs and link names as in a table
- 链接 IDs 仅仅使用小写字母. 解释: 因为 IDs 区分大小写,
- 只用小写容易书写，并且可读性比大小写混合单词大很多。

建议使用:
```
[id2]     http://long-url.com
[long id] http://a.com        "name 1"
```
不建议, 没有安装 id 排序:
```
[b] http://a.com
[a] http://b.com
```
不建议, 没有对齐:
```
[id] http://id.com
[long id] http://long-id.com
```
### 单引号或双引号标题

使用双引号，*不要* 使用单引号。
解释: 单引号并不是在所有的实现中都有效，但是双引号可以。

## 强调

### 加粗

使用双星号格式: `**bold**`.
解释: 比双下划线格式`__bold__`更加常见和可读性更高.

### 斜体

使用单星号格式: `*italic*`.
解释:

- 比下划线格式更加常见，易读性更高
- 与加粗格式一致, 同样使用星号标记

### 大写强调

*不要* 使用大写来强调: 使用强调语法例如 **加粗**或者*斜体* 。

解释: CSS 有`text-transform:uppercase`属性,如果你愿意的话，可以轻松在全网站实现相同的效果。

### 强调与标题

*不要* 使用强调元素(加粗或者斜体) 来介绍多行区块: 使用标题代替.

解释: 这个就是确切的标题的语义, 使用强调的并不是必须的。作为结果，许多实现，给标题增加有用的功能，并没有给强调元素，比如自动 `id `来更加容易的引用标题。

建议使用:
```
# How to make omelets

Break an egg.

...

# How to bake bread

Open the flour sack.

...

```
不建议：
```
**How to make omelets:**

Break an egg.

...

**How to bake bread:**

Open the flour sack.

...
```

## 自动链接

### 使用尖括号自动链接

- *不要* 使用不带尖括号的自动链接。
 建议使用:
```
<http://a.com>
```
 不建议：
```
http://a.com
```
解释: 这个扩展中,` <> `容易从键盘敲出，也同样容易读。

- 如果你不想文字链接自动链接，将他们以代码区块方式包裹，例如：
```
`http://not-a-link.com`
```
解释: 许多工具自动将 http 开头的字串解释成链接。

### 内容的自动链接

所有自动链接必须以字串`http`开始。
特别的, *不要* 在相对链接时使用自动链接。如果遇到相对链接，使用括号的方式创建链接。
建议使用:
```
[file.html](file.html)
```
不建议：
```
<file.html>
```
建议使用:
```
<https://github.com>
```
不建议：
```
<github.com>
```
解释: 将自动链接从HTML tags区分开很困难. 如果你想要一个相对的链接指向一个 `script` 的文件？

### 电子邮件自动链接

*不要* 使用电子邮件自动链接 `<address@example.com>`. 使用纯HTML .

解释: 标准 markdown 设计规范这样描述:

> “performs a bit of randomized decimal and hex entity-encoding to help obscure your address from address-harvesting spambots”.

因此, 输出是随机的，丑陋的, 并且像规范中提到的:
> but an address published in this way will probably eventually start receiving spam

# License
Markdown 风格指南 is License
