# 常用 Markdown 语法演示

## 标题
``` html
# H1
## H2
### H3
#### H4
##### H5
###### H6

另外, 对于 H1 和 H2，也可以这么写:

H1 的另一种写法
======

H2 的另一种写法
------
```


## 强调
```html
斜体强调，使用 *单星号* 或者 _单下划线_

加粗强调，使用 **双星号** 或者 __双下划线__

可以组合使用，**双星号 _单下划线_**

删除线，使用 ~~双波浪线~~
```

下面是最终的效果：

斜体强调，使用 *单星号* 或者 _单下划线_

加粗强调，使用 **双星号** 或者 __双下划线__

可以组合使用，**双星号 _单下划线_**

删除线，使用 ~~双波浪线~~


## 列表
```html
1. 有序列表，前面加数字
2. 有序列表，前面加数字

* 无序列表，可以使用星号
* 嵌套列表，使用 TAB 缩进
- 或者使用加号
- 嵌套列表，使用 TAB 缩进
+ 或者使用减号
+ 嵌套列表，使用 TAB 缩进
```

下面是最终的效果：
1. 有序列表，前面加数字
2. 有序列表，前面加数字


* 无序列表，可以使用星号
* 嵌套列表，使用 TAB 缩进
- 或者使用加号
- 嵌套列表，使用 TAB 缩进
+ 或者使用减号
+ 嵌套列表，使用 TAB 缩进


## 链接
```html
[这是一个内联链接](https://www.google.com)

[这是一个有 title 属性的内联链接](https://www.google.com "Google's Homepage")

[这是一个参考链接，地址可以写在文章的最后面][Arbitrary case-insensitive reference text]

[这是一个相对路径的链接](../blob/master/LICENSE)

[也可以使用数字形式的参考链接][1]

或者直接 [只使用文本的参考链接]

尖括号中的文字会自动转换成链接，比如 <http://www.example.com>。

以下是上面文章中使用到的参考链接：

[arbitrary case-insensitive reference text]: https://www.mozilla.org
[1]: http://slashdot.org
[link text itself]: http://www.reddit.com
```

下面是最终的效果：

[这是一个内联链接](https://www.google.com)

[这是一个有 title 属性的内联链接](https://www.google.com "Google's Homepage")

[这是一个参考链接，地址可以写在文章的最后面][任意不区分大小写的文本]

[这是一个相对路径的链接](../blob/master/LICENSE)

[也可以使用数字形式的参考链接][1]

或者直接 [只使用文本的参考链接]

尖括号中的文字会自动转换成链接，比如 <http://www.example.com>。

[任意不区分大小写的文本]: https://www.mozilla.org
[1]: http://slashdot.org
[只使用文本的参考链接]: http://www.reddit.com


## 图片
```html
内联形式： ![alt text](http://doc.hz.netease.com/images/logo/default-space-logo.png "Logo Title Text 1")

参考链接的形式：![alt text][logo]

[logo]: http://doc.hz.netease.com/images/logo/default-space-logo.png
```

下面是最终的效果：

内联形式： ![alt text](http://doc.hz.netease.com/images/logo/default-space-logo.png "Logo Title Text 1")

参考链接的形式：![alt text][logo]

[logo]: http://doc.hz.netease.com/images/logo/default-space-logo.png


## 代码和语法高亮
<pre lang="no-highlight"><code>
内联形式：`let a = 1;`

区块形式：
```js
let a = 1;
let b = 2;
```
</code></pre>

下面是最终的效果：

内联形式：`let a = 1;`

区块形式：

```js
let a = 1;
let b = 2;
```


## 表格
```html
冒号可以用来对齐表格的列：

| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |

外部的竖线（|）是可选的，它们不需要对得很整齐。也可以使用下面的语法：

Markdown | Less | Pretty
--- | --- | ---
*Still* | `renders` | **nicely**
1 | 2 | 3
```

下面是最终的效果：

| Tables        | Are           | Cool |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |

也可以使用下面的语法：

Markdown | Less | Pretty
--- | --- | ---
*Still* | `renders` | **nicely**
1 | 2 | 3

## 引用
```html
> 这是一行引用。在引用中也可以使用强调语法，比如 *星号*、**双星号**。
```

下面是最终的效果：

> 这是一行引用。在引用中也可以使用强调语法，比如 *星号*、**双星号**。

## 内联 HTML
```html
在 Markdown 中，可以直接使用 HTML 代码：
<dl>
  <dt>定义列表</dt>
  <dd>解释</dd>

  <dt>HTML 中的 Markdown 不能正常显示</dt>
  <dd>*单星号*、**双星号**都不可以，此时需要使用 HTML <em>标签</em></dd>
</dl>

```

下面是最终的效果：

<dl>
  <dt>定义列表</dt>
  <dd>解释</dd>

  <dt>HTML 中的 Markdown 不能正常显示</dt>
  <dd>*单星号*、**双星号**都不可以，此时需要使用 HTML <em>标签</em></dd>
</dl>

## 横线
```html
使用三个以上的横线、星号、或者下划线：

-----

***

___

```

下面是最终的效果：

-----

***

___

## 视频
```html
使用 video 标签插入视频：
<video controls="" src="https://www.quirksmode.org/html5/videos/big_buck_bunny.mp4"></video>
```

下面是最终的效果：

<video controls="" src="https://www.quirksmode.org/html5/videos/big_buck_bunny.mp4"></video>