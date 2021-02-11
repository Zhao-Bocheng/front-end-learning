# HTML基础

## HTML文件基本框架：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    HTML显示的内容
</body>
</html>
```

## 基本标签

### 标题标签

共六级

```html
<h1></h1>
<h2></h2>
<h3></h3>
<h4></h4>
<h5></h5>
<h6></h6>
```

### 段落与换行

```html
<p></p>
<br/>或<br>
```

### 文本格式化标签

一般采用左边的标签，右边标签表意不明显

```html
<strong></strong>  <b></b>
<del></del> <s></s>
<em></em> <i></i>
<ins></ins> <u></u>
```

### “盒子”标签

```html
<div></div>
<span></span>
```

### 图像标签

```html
<img src="imgURL"/>
<!--
	其他非必须属性有：
	alt：替换文本
	title：提示文本
	width：宽度（使用百分比时是指占浏览器宽度的百分比，而非原有宽度缩放的百分比）
	height：高度 （无法使用百分比）
	还有其他属性，不一一列出
-->
```

### 超链接标签

```html
<a href="跳转目标" target=“打开方式”></a>
<!--
	a表示anchor
	target默认为_self，取值可为_blank、_parent、_self、_top、framename
	链接的类型有：
		外部链接
		内部链接
		下载链接：如果href链接中的资源是浏览器无法处理的，将会弹出下载窗口，可在chrome和firefox中使用download属性，但edge
				怎么弄？
		网页元素链接：将网页元素作为链接，例如将图片作为链接
		锚点链接：href="#锚点名称"  使用id属性为目标标签提供锚点名称
		空链接：href="#" 
	链接的默认外观：
		未被访问的链接带有下划线且为蓝色
		已被访问的链接带有下划线且为紫色
		活动链接带有下划线且是红色
	可使用CSS伪类修改默认样式
	还有其他属性，不一一列出
-->
```

### 注释与特殊字符

```html
<!-- -->
```

| \&nbsp;    | 空格     |
| ---------- | -------- |
| \&lt;      | &lt;     |
| \&gt;      | &gt;     |
| \&amp;     | &amp;    |
| \&yen;     | &yen;    |
| \&copy;    | &copy;   |
| \&reg;     | &reg;    |
| \&deg;     | &deg;    |
| \&plussmn; | &plusmn; |
| \&times;   | &times;  |
| \&divide;  | &divide; |
| \&sup2;    | &sup2;   |
| \&sup3;    | &sup3;   |

还有其他特殊字符，不一一列出（[其他符号实体名称](https://www.w3school.com.cn/tags/html_ref_entities.html)，[希腊字母，数学符号等特殊字符实体名称参考](https://www.w3school.com.cn/tags/html_ref_symbols.html)）

### 表格标签（暂且不做深究）

```html
<table>
    <tr>
    	<th></th>
        	....
        <th></th>
    </tr>
	<tr>
    	<td></td>
        	....
    	<td></td>
    </tr>   
    <tr>
    	....
    </tr>
</table>

<thead></thead>
<tfoot></tfoot>
<tbody></tbody>
```

### 列表标签

#### 无序列表

```html
<ul>
    <li></li>
    <li></li>
    <li></li>
</ul>
```

#### 有序列表

```html
<ol>
    <li></li>
    <li></li>
    <li></li>
</ol>
```

#### 自定义列表

```html
<dl>
    <dt></dt>
    <dd></dd>
    <dd></dd>
    <dt></dt>
</dl>
```

无序列表在实际应用中常被用于排版，其样式多通过CSS设置。并且在布局前往往需要去掉无序列表表项的小圆点

```css
li {
	list-style: none;   
}
```

### 表单标签

#### 表单域（待学习）

```html
<form></form>
<!--
	action="url" 定义在提交表单时执行的动作，不使用action属性则默认为当前页面
	method="get/post"
	name="域名称"
-->
```

#### 表单控件

##### input输入表单元素

###### type属性

根据不同的 *type* 属性，`<input>` 元素有很多形态

```html
<input type=""/>
<!--
	button：按钮（配合js），显示value属性的值，默认为空
	submit：提交按钮，用于提交表单
	image：带图像的submit按钮，，显示图像由src属性规定，如果src属性缺失就会显示alt属性
	reset：重置按钮（清空还原）

	checkbox：复选框，可使用 checked 属性默认选中
	radio：单选按钮（配合 name 属性使用，允许多个拥有相同 name 值的选项中选一个）

	file：文件上传域，使用 accept 属性规定控件能选择的文件类型

	hidden：不显示的控件，其值仍会提交到服务器
	
	password：密码输入框（显示掩码），如果站点不安全会警告用户
	text：文本框（文本字段的默认宽度是 20 个字符）。输入中的换行会被自动去除
	email: 编辑邮箱地址的区域，类似text输入，会检查是否为邮箱格式
-->
```

###### HTML5中新增输入表单

新的`type`取值——新的输入表单

```html
<!--
	url: 用于输入URL的控件。类似text输入，但有 验证参数

	date: 输入日期的控件（年月日，不包括时间），激活时打开日期选择器或年月日的数字滚轮
	datetime-local: 输入日期和时间的控件，不包含时区，激活时打开日期选择器或年月日的数字滚轮
	time: 用于输入时间的控件，不包括时区
	month: 输入年月的控件，没有时区
	week: 用于输入以年和周数组成的日期，不带时区

	number: 只能输入数字，会显示滚动按钮并提供 缺省验证
	tel: 用于输入电话号码的控件

	search: 搜索框。输入文本中的换行会被自动去除，还会有一个清除按钮、

	color: 用于制定颜色的控件，激活时打开取色器

	range: 范围控件。此控件不需要输入精确数字，默认值为正中间的值。同时使用htmlattrdefmin 和 htmlattrdefmax来规定值的范围（这里没懂？？？）
-->
```

**注意：验证上述表单必须使用表单域（`form`）和提交按钮（`submit`）才能看出效果**

###### 其他属性：

|     属性     |                   相关的type                    |                             描述                             |
| :----------: | :---------------------------------------------: | :----------------------------------------------------------: |
|     name     |                      所有                       |      input表单控件的名字，以名字/值对形式随表单一起提交      |
|    value     |                      所有                       |         表单控件的值，以名字/值对形式随表单一起提交          |
|      id      |                      所有                       |       id值用于在链接元素时使用（`<label>`for属性的值）       |
|    title     |                      所有                       |                           提示信息                           |
|   checked    |                 radio，checkbox                 |                    用于控制控件是否被选中                    |
|    accept    |                      file                       | 用于规定上传文件类型。<br />值为一个逗号分隔的列表：<br />1. 以STOP字符开始的文件扩展名<br />2.一个有效的MIME类型，但无扩展名<br />3.`audio/*`表示音频文件，`video/*`表示视频文件，`image/*`表示图片文件 |
|     src      |                      image                      |                    和`<img>`的src属性相同                    |
|     alt      |                      image                      |                 按钮图片无法显示时的替代文本                 |
|    width     |                      image                      |                   和`<img>`的width属性相同                   |
|    height    |                      image                      |                  和`<img>`的height属性相同                   |
| autocomplete |                      所有                       | 用于表单的自动填充功能，取值为off/on等，生效的前提是有name属性且已经提交过 |
|  autofocus   |                      所有                       |                页面加载时自动聚焦到此表单控件                |
|     max      |                    数字type                     |                            最大值                            |
|     min      |                    数字type                     |                            最小值                            |
|  maxlength   |     password, search, tel, text, url, email     |                value的最大长度，最多字符数目                 |
|  minlength   |     password, search, tel, text, url, email     |                value的最小长度，最少字符数目                 |
| placeholder  |     password, search, tel, text, url, email     |              当表单控件为空时，控件中显示的内容              |
|   required   | 绝大部分，当为hidden, image或按钮类型时无法使用 |      布尔值。表示此值为必填项或提交表单前必须先检查该值      |
|   multiple   |                   email, file                   |                    布尔值，是否允许多个值                    |
|     size     |     email, password, tel, text，search, url     |              控件大小。值必须大于0，默认值为20               |

*注：仍有其他属性未列出*

##### label标签

为input元素定义标注（标签）

**用于绑定一个表单元素**，当点击`<label>`标签的文本时，浏览器就会自动将焦点（或光标）转到或选择对应的表单元素上，用来增加用户体验（就是**增加有效点击区域**）

```html
<label for="id值"></label>
<!--
	<input type="radio" name="gender" id="gender"/>
	<label for="gender"></label>
-->
```

##### select下拉表单元素

```html
<select>
    <option selected></option>	<!-- 加上selected属性的选项会被设置为默认选项 -->
    <option></option>
    	....
    <option></option>
</select>
<!-- 一般不一个个列出可选选项，而是通过js脚本实现 -->
```

##### textarea文本域元素

与文本框不同（`<input type="text"/>`）

```html
<textarea></textarea>
<!-- 
	属性cols="colNum"和rows="rowNum"可用于设置文本域大小，但一般使用CSS设置
```

