# FE规范

---

## 项目目录结构

### 项目结构
	--- 
	|---- index.html             页面
	|---- js/                    JS //具体见JS细化结构                 
	|---- css/                   CSS //具体见CSS细化结构

### CSS文件结构
	--- ../css/
	|---- css/base/global.css         公共型样式
	|---- css/plugs/xxx/xx.style      插件1样式
	|---- css/plugs/xxx/xx.style      插件2样式	
 	|---- css/images/                 图片
 	|---- css/xx-style.css            xx的样式表
 	|---- css/xx-scss.scss            xx的scss文件（含sass文件）

### JS文件结构
	---../js/
	|---- js/plugs/plugin-1/     使用到的js插件1
	|---- js/plugs/plugin-2/     使用到的js插件2
 	|---- script.js              单独书写的js
	|---- plugins.js             调用的plugins汇总
	|---- jquery.js/zepto.js     调用的javascript库



---
## Html规范

### 整体结构
---
#### HTML基础设施
- 文件应以```<DOCTYPE html>```顶格开始。
- 必须声明文档的编码```<meta charset="utf-8" />```，且与文件编码保持一致。
- 根据页面的需求填写适当的__keywords__和__description__
```
<!DOCTYPE html>
<html>

	<head>
		<meta charset="utf-8" />
		<title>HTML书写规范</title>
		<meta name="keywords" content="" />
		<meta name="description" content="" />
		<meta name="viewport" content="width=device-width" />
		<link rel="stylesheet" href="css/style.css" />
		<link rel="shortcut icon" href="img/favicon.ico" />
		<link rel="apple-touch-icon" href="img/touchicon.png" />
	</head>

	<body>

	</body>

</html>
```

#### 结构和视觉顺序基本保持一致
- 按照从上至下，从左往右的顺序书写html结构
- 禁止使用table布局，但表现具有明显表格的形式的数据，table还是首选

#### 结构/表现/行为三者进行分离，避免内联
- 使用link将css文件引入，并置于head中。
- 使用script将文件引入，并置于body底部。

#### 其他
- 结构上如果可以做到并列书写，就不要进行嵌套。
> 如果可以写成```<div></div><div></div>```，就不要写成```<div><div></div></div>```。

- 如果结构上已经满足视觉和语义要求，那么就不要有额外的冗余的结构
>比如```<div><h2></h2></div>```已经满足要求，就不要写成```<div><div><h2></h2></div></div>```。

### 代码规范
---
#### 说明文案的注释方法
> 采用类似标签闭合的写法，与html统一格式；
- 开始注释：```<!-- 注释文案 -->```（文案两头空格）。
- 结束注释：```<!-- /注释文案 -->``` 

```
<!-- 头部 -->
<div class="g-hd">
    <!-- LOGO -->
    <h1 class="m-logo"><a href="#">LOGO</a></h1>
    <!-- /LOGO -->
    <!-- 导航 -->
    <ul class="m-nav">
        <li><a href="#">NAV1</a></li>
        <li><a href="#">NAV2</a></li>
    </ul>
    <!-- /导航 -->
</div>
<!-- /头部 -->
```

#### 代码本身的注释方法
> 单行代码的注释保持同行，两端空格；多行代码的起始和结尾都另起一行并左缩进对齐。
```
<!-- <h1 class="m-logo"><a href="#">LOGO</a></h1> -->
<!--
<ul class="m-nav">
    <li><a href="#">NAV1</a></li>
    <li><a href="#">NAV2</a></li>
</ul>
-->
```
#### 严格的嵌套规则
> 待定

#### 严格的属性
- 属性和值全部小写，每个值必须加双引号。
- 可以省略style标签和script标签的type属性。
- html属性顺序按照以下顺序依次排列，确保代码的易读性：
```
class
id,name
data-*
src,for,type,href
title,alt
其他
```

---

## CSS规范

### 分类方法
---

#### css文件分类和引用顺序
> 对于较大的项目，需要把CSS文件进行分类。

 按照CSS的性质和用途，将CSS文件分成'公共型样式'／'插件样式'／'站点独有样式'，并以此顺序引用。
1. 公共型样式：‘标签的重置和设置默认值’／‘网站通用布局’／‘通用模块和其他扩展’／‘元件和其扩展‘/‘清除浮动或其他需要统一处理的功能样式’。
2. 插件样式：网站所引入插件所需要的样式，插件默认样式。
3. 站点独有样式：既是站点所需的样式，插件自定义样式也归属这个文件。
```
<link href="css/base/global.css" rel="stylesheet" />
<link href="css/plugs/xxx/xxx.style" rel="stylesheet" />
<link href="css/xx.style" rel="stylesheet" />
```

### 命名规范
---
该命名规范主要解决以下问题：

* 从类名可以清晰区分出其功能作用，使页面结构清晰【命名空间、标识符】；
* 以组件、模块的思想去写一个区块的结构，强化结构的模块化【BEM模块思想、基类、子类、扩展类】；
* 减少多人合作、项目耦合等情况下的命名冲突【命名空间】；

#### 命名思想

**【强制】** 区块、模块、组件等一个整个的结构遵循BEM命名思想；

当你能确定组件内最后一级的结构不会再发生变化时，最后一级可省略类名，使用两层嵌套；

* `.block` 代表了更高级别的抽象或组件；
* `.block__element` 代表`.block`的后代，用于形成一个完整的`.block`的整体；
* `.is-` | `.has-` | `.ext-` 代表`.block`的修饰符，**不使用双中划线`--`**。

相关链接：

* [BEM—源自Yandex的CSS 命名方法论](http://segmentfault.com/a/1190000000391762)
* [BEM官网](http://bem.info/)


#### 多单词连接

**【强制】** （所有的）多个单词使用小驼峰式命名，不允许使用中划线或者下划线连接多个单词；

多个单词使用小驼峰式命名，以提升名称的识别度，例如：`newsList`；

#### 命名空间

**【强制】** 在合适的地方使用命名空间；

* **布局**：以`g`为命名空间，例如：`.g-wrap` 、`.g-header`、`.g-content`、`.g-aside`、`.g-footer` 等；
* **工具**：以`u`为命名空间，**表示不耦合业务逻辑的、可复用的的工具**，例如：`.u-clearfix`、`.u-ellipsis` 等；
* **状态**：以`is`为命名空间，**表示动态的、具有交互性质的状态**，例如：`.is-open`、`.is-active`、`.is-selected` 等；
* **组件**：以`ui`或者`mod`为命名空间，**表示可复用、移植的组件模块**，例如：`.ui-slider`、`.mod-dropMenu`等；
* **扩展**：以`ext`为命名空间，**表示对组件基类的视觉形态的扩展**，例如：`.ext-cover、`、`.ext-alignLeft` 等；

**状态类或扩展类一般出现在组件的父级节点，并且不允许单独使用。举个例子，同一个页面有可能会在不同的地方都会使用`is-active`，并且每个`is-active`所操纵的节点的是不同的，所以要使用`.ui-userCard.is-active` 或 `.ui-userCard .is-active`来定义**

#### 图片命名

* **图标**：以`ico`作为命名空间，例如：`.ico-close` 等；
* **LOGO**：以`logo`作为命名空间，例如：`.logo-duowan` 等；
* **内容图像**：以`img`作为命名空间，例如：`.img-userGuide` 等；

#### 区块命名

**【推荐】** 一般区块都可以划分为头部、身体和尾部，因此建议给你的区块分别以 `hd`、`bd`、`ft`来划分；

示例：

```css
.ui-card__hd {
    margin: 0;
}

.ui-card__bd {
    margin: 0;
}

.ui-card__ft {
    margin: 0;
}
```

#### 附：命名示例

<img src="https://cloud.githubusercontent.com/assets/1295348/7456687/0643f254-f2b9-11e4-9b14-f1b36257f9a3.jpg" alt="命名示例" width="600">
