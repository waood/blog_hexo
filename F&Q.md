

# Hexo 使用手册

## 1. 命令

```xml
hexo n 文章名 == hexo new 文章名 #新建文章
hexo p == hexo publish #发布
hexo g == hexo generate #生成
hexo s == hexo server #启动服务预览
hexo d == hexo deploy #部署
hexo b == hexo backup #备份项目文件
hexo c == hexo command #查看可用命令
hexo v == hexo version #查看版本
hexo clean #清空缓存、数据库、本地静态文件等数据
```



---

## 2. 写作	

### 2.1 创建新文章

```xml
hexo new [模板名] 文章名
缺省为: hexo n 文章名 == hexo new 文章名 #新建文章
```



### 2.2 摘要中断

```
<!--more-->
```



### 2.3 文本居中的引用

此标签将生成一个带上下分割线的引用，同时引用内文本将自动居中。 文本居中时，多行文本若长度不等，视觉上会显得不对称，因此建议在引用单行文本的场景下使用。 例如作为文章开篇引用 或者 结束语之前的总结引用。

**使用方式**

- HTML方式：使用这种方式时，给 `img` 添加属性 `class="blockquote-center"` 即可。
- 标签方式：使用 `centerquote` 或者 简写 `cq`。

 **标签调用方法**

```
<!-- HTML方式: 直接在 Markdown 文件中编写 HTML 来调用 -->
<!-- 其中 class="blockquote-center" 是必须的 -->
  <blockquote class="blockquote-center">blah blah blah</blockquote>

  <!-- 标签 方式，要求版本在0.4.5或以上 -->
{% centerquote %}blah blah blah{% endcenterquote %}

  <!-- 标签别名 -->
{% cq %} blah blah blah {% endcq %}
```



### 2.4 突破容器宽度限制的图片

当使用此标签引用图片时，图片将自动扩大 26%，并突破文章容器的宽度。 此标签使用于需要突出显示的图片, 图片的扩大与容器的偏差从视觉上提升图片的吸引力。 此标签有两种调用方式（详细参看底下示例）：

**使用方式**

- HTML方式：使用这种方式时，为 `img` 添加属性 `class="full-image"`即可。
- 标签方式：使用 `fullimage` 或者 简写 `fi`， 并传递图片地址、 `alt` 和 `title` 属性即可。 属性之间以逗号分隔。

此标签要求 NexT 的版本在 0.4.5 或以上。 若你正在使用的版本比较低，可以选择使用 `HTML` 方式。
如果要在图片下显示图片的标题，请使用 标签方式 并给定 `title` 属性。

 标签调用方法

```
<!-- HTML方式: 直接在 Markdown 文件中编写 HTML 来调用 -->
<!-- 其中 class="full-image" 是必须的 -->
<img src="/image-url" class="full-image" />

    <!-- 标签 方式，要求版本在0.4.5或以上 -->
{% fullimage /image-url, alt, title %}

<!-- 别名 -->
{% fi /image-url, alt, title %}
```



### 2.5 引用书上的句子

```
{% blockquote Author,Book Name %}
Contents
{% endblockquote %}
```



### 2.6 **引用网络上的文章**

```
{% blockquote Author url title %}
Contents
{% endblockquote %}
```



### 2.7 字体处理

小写 <small>A</small>

大写 <big>A</big>

图片标题  <center><font color=#818285 size=4><B><I>A</B></I></font></center>

居中<center>A</center>

居右 <div align = right>A</div>

### 2.8 图片渲染

```xml
图片渲染：在七牛图片源尾部增加以下内容，其中'w','gravity','fontsize','text','dx','dy'等均支持自定义
text编码:Base64
?imageView2/2/w/700/interlace/0/q/100|watermark/2/text/d2F0ZXItd29vZC5jb20=/font/Y29taWMgc2FucyBtcw==/fontsize/500/fill/I0VGRUZFRg==/dissolve/64/gravity/SouthEast/dx/30/dy/20
```

Base64在线编码工具：http://tool.css-js.com/base64.html



### 2.9 表情

[表情](E:\Tool_Software\Hexo\Settings\checksheet-emoji.md)

---

## 3. 设置

### 3.1 使图片默认居中

  ```
修改~theme/.next/source/css/_schemes/Mist/_posts-expanded.styl 30行可解决
.post-body img { margin: 0; }   修改为  .post-body img {margin: 0 auto;}
  ```



### 3.2 twemoji表情不现实

不要直接复制表情，手工敲表情代码或者复制表情代码



### 3.3 关闭新建页面的评论功能

当集成了评论系统，如 多说 或者 Disqus，所有新建的页面都将自动开启评论。若你不需要评论，请在页面的 Front-matter 里添加`comments` 字段，并将值设置为 `false`。如下所示：

```
comments: false
```



### 3.4 ~~更改字体？~~

~~NexT 从 **5.0.1** 版本开始提供一个 [字体定制特性](http://theme-next.iissnan.com/theme-settings.html#fonts-customization)， 请先查看此特性是否能满足你的需求。以下的修改将覆盖 字体定制 的特性。 编辑主题下的 `source/css/_variables/custom.styl` 文件，新增两个变量：~~

```
// 标题，修改成你期望的字体族
$font-family-headings = Georgia, sans

// 修改成你期望的字体族
$font-family-base = "Microsoft YaHei", Verdana, sans-serif

// 代码字体
$code-font-family = "Input Mono", "PT Mono", Consolas, Monaco, Menlo, monospace

// 正文字体的大小
$font-size-base = 16px

// 代码字体的大小
$code-font-size = 13px
```



### 3.5 开启文章的评论功能

为单篇文章设置评论权限，在Front-matter中设置

```
comments: ture
```



### 3.6 以分类形式为文章设置永久链接

在Hexo配置文件中如下设置：

```
permalink: :category/:title.html
```



### 3.7 最近访客

在需要设置文档的目录底下加上这么一句话即可

```
<div class="ds-recent-visitors" data-num-items="28" data-avatar-size="42" id="ds-recent-visitors"></div>
```



---

___

# Markdown

## 1. Markdown 基础

### 1.1  标题

```x
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题
大标题
=
小标题
-
```



### 1.2 粗体、斜体

```
**粗体**
__粗体__
*斜体*
_斜体_
```



### 1.3 分割线

```
---
***
```



### 1.4 列表

```
- 无序列表项目
- 无序列表项目
- 无序列表项目

* 无序列表项目
* 无序列表项目
* 无序列表项目

1. 有序列表项目
2. 有序列表项目
3. 有序列表项目

- 外层列表项目
 + 内层列表项目
 + 内层列表项目
 + 内层列表项目
- 外层列表项目
```

预览效果：

- 无序列表项目
- 无序列表项目
- 无序列表项目


- 无序列表项目
- 无序列表项目
- 无序列表项目

1. 这是有序列表项目
2. 这是有序列表项目
3. 这是有序列表项目

- 外层列表项目
  - 内层列表项目
  - 内层列表项目
  - 内层列表项目
- 外层列表项目





### 1.5 添加超链接、图片

```
[title]( url )  //文字链接
![title]( url )  //图片链接
```



### 1.6 引用

```
> 引用的文字
> 引用的文字
> 引用的文字

> 引用的文字引用的文字引用的文字引用的文字引用的文字引用的文字引
用的文字引用的文字引用的文字引用的文字引用的文字引用的文字引用
的文字引用的文字引用的文字

> 引用的文字引用的文字引用的文字引用的文字引用的文字
> > 引言内的引言引言内的引言引言内的引言 
> > 引用的文字引用的文字引用的文字引用的文字引用的文字
>
> 引用
```

**预览**

> 引用的文字
> 引用的文字
> 引用的文字



> 引用的文字引用的文字引用的文字引用的文字引用的文字引用的文字引
> 用的文字引用的文字引用的文字引用的文字引用的文字引用的文字引用
> 的文字引用的文字引用的文字



> 引用的文字引用的文字引用的文字引用的文字引用的文字
> > 引言内的引言引言内的引言引言内的引言 
> > 引用的文字引用的文字引用的文字引用的文字引用的文字
>
> 引用





### 1.7 单行长文字

```
在需要以单行长文字显示的文字两段各加三个`~`,即`~~~`
在需要以单行长文字显示的文字段落前加四个空格
```



### 1.8 创建链接

```
< 链接 >
```



### 1.9 转义字符

```
\
```



### 1.10 删除线

```xml
~~文字删除线~~
```





___

## 2. Markdown 高阶

### 2.1 引用目录

```
[toc]
```

   


### 2.2 引用代码

```
​``` + 语言名称
```

   


### 2.3 脚注

```
[^keywords]

[^NO]
[^NO]: 阐释
```

   

### 2.4 标签和分类

    tags: 
      - Markdown
      - 语言
    categories:



### 2.5 待办事宜

    - [ ]
    - [x]



### 2.6 表格

    |        |       |
    |--------|-------|  //这一行是分界线
    |        |       |
    |        |       |
    |        |       |



### 2.7 公式

    行内公式 $公式$  //质量守恒方程：$E=mc^2$
    整行公式 $$公式$$     

---

