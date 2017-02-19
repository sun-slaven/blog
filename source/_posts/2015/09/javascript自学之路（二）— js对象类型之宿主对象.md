---
title: 'js对象类型之宿主对象'
tags:
- js宿主对象
categories:
- javascript
date: 2015-09-23 19:37:16
---

**Js中的宿主对象：**

**包括浏览器中的window（BOM）和document（DOM）对象**

# **一、&nbsp;&nbsp;DOM对象**

**<span style="color:#cc0000">包括：Document、Element、Attribute、Event四大对象</span>**

## **1.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Document**

每个载入浏览器的 HTML 文档都会成为 Document 对象。

Document 对象使我们可以从脚本中对 HTML 页面中的所有元素进行访问。
<!-- more -->
<span style="color:red">提示：</span>Document对象是 Window 对象的一部分，可通过 window.document 属性对其进行访问。

> > > > > > > > > **<span style="white-space:pre"></span>Document 对象属性**
<div align="center">
<table border="1" cellspacing="0" cellpadding="0" style="background:#F9F9F9">
<tbody>
<tr>
<td valign="bottom" style="background:#D5D5D5">

**属性**

</td>
<td valign="bottom" style="background:#D5D5D5">

**描述**

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

<span style="color:#0D0D0D">body</span>

</td>
<td valign="top" style="background:#EFEFEF">

提供对 &lt;body&gt; 元素的直接访问。

对于定义了框架集的文档，该属性引用最外层的 &lt;frameset&gt;。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#00B0F0">cookie</span>](http://www.w3school.com.cn/jsref/prop_doc_cookie.asp)

</td>
<td valign="top" style="background:#EFEFEF">

设置或返回与当前文档有关的所有 cookie。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:black">domain</span>](http://www.w3school.com.cn/jsref/prop_doc_domain.asp)

</td>
<td valign="top" style="background:#EFEFEF">

返回当前文档的域名。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#0D0D0D">lastModified</span>](http://www.w3school.com.cn/jsref/prop_doc_lastmodified.asp)

</td>
<td valign="top" style="background:#EFEFEF">

返回文档被最后修改的日期和时间。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#0D0D0D">referrer</span>](http://www.w3school.com.cn/jsref/prop_doc_referrer.asp)

</td>
<td valign="top" style="background:#EFEFEF">

返回载入当前文档的文档的 URL。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#00B0F0">title</span>](http://www.w3school.com.cn/jsref/prop_doc_title.asp)

</td>
<td valign="top" style="background:#EFEFEF">

返回当前文档的标题。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#00B0F0; background:#D9D9D9">URL</span>](http://www.w3school.com.cn/jsref/prop_doc_url.asp)

</td>
<td valign="top" style="background:#EFEFEF">

返回当前文档的 URL。

</td>
</tr>
</tbody>
</table>
</div>
> > > > > > **Document 对象方法**
>
> > > > > > <table border="1" cellspacing="0" cellpadding="0" align="left" style="text-align:left; background:rgb(249,249,249)">
> > > > > >
> > > > > > <tbody>
> > > > > >
> > > > > > <tr>
> > > > > >
> > > > > > <td valign="bottom" style="background:#D5D5D5">
> > > > > >
> > > > > >
> > > > > > **方法**
> > > > > >
> > > > > > </td>
> > > > > >
> > > > > > <td valign="bottom" style="background:#D5D5D5">
> > > > > >
> > > > > >
> > > > > > **描述**
> > > > > >
> > > > > > </td>
> > > > > >
> > > > > > </tr>
> > > > > >
> > > > > > <tr>
> > > > > >
> > > > > > <td valign="top" style="background:#EFEFEF">
> > > > > >
> > > > > >
> > > > > > [<span style="color:#0D0D0D">close()</span>](http://www.w3school.com.cn/jsref/met_doc_close.asp)
> > > > > >
> > > > > > </td>
> > > > > >
> > > > > > <td valign="top" style="background:#EFEFEF">
> > > > > >
> > > > > >
> > > > > > 关闭用 document.open() 方法打开的输出流，并显示选定的数据。
> > > > > >
> > > > > > </td>
> > > > > >
> > > > > > </tr>
> > > > > >
> > > > > > <tr>
> > > > > >
> > > > > > <td valign="top" style="background:#EFEFEF">
> > > > > >
> > > > > >
> > > > > > [<span style="color:#00B0F0">getElementById()</span>](http://www.w3school.com.cn/jsref/met_doc_getelementbyid.asp)
> > > > > >
> > > > > > </td>
> > > > > >
> > > > > > <td valign="top" style="background:#EFEFEF">
> > > > > >
> > > > > >
> > > > > > 返回对拥有指定 id 的第一个对象的引用。
> > > > > >
> > > > > > </td>
> > > > > >
> > > > > > </tr>
> > > > > >
> > > > > > <tr>
> > > > > >
> > > > > > <td valign="top" style="background:#EFEFEF">
> > > > > >
> > > > > >
> > > > > > [<span style="color:#00B0F0">getElementsByName()</span>](http://www.w3school.com.cn/jsref/met_doc_getelementsbyname.asp)
> > > > > >
> > > > > > </td>
> > > > > >
> > > > > > <td valign="top" style="background:#EFEFEF">
> > > > > >
> > > > > >
> > > > > > 返回带有指定名称的对象集合。
> > > > > >
> > > > > > </td>
> > > > > >
> > > > > > </tr>
> > > > > >
> > > > > > <tr>
> > > > > >
> > > > > > <td nowrap="nowrap" valign="top" style="background:#EFEFEF">
> > > > > >
> > > > > >
> > > > > > [<span style="color:#00B0F0">getElementsByTagName()</span>](http://www.w3school.com.cn/jsref/met_doc_getelementsbytagname.asp)
> > > > > >
> > > > > > </td>
> > > > > >
> > > > > > <td valign="top" style="background:#EFEFEF">
> > > > > >
> > > > > >
> > > > > > 返回带有指定标签名的对象集合。
> > > > > >
> > > > > > </td>
> > > > > >
> > > > > > </tr>
> > > > > >
> > > > > > <tr>
> > > > > >
> > > > > > <td valign="top" style="background:#EFEFEF">
> > > > > >
> > > > > >
> > > > > > [<span style="color:#0D0D0D">open()</span>](http://www.w3school.com.cn/jsref/met_doc_open.asp)
> > > > > >
> > > > > > </td>
> > > > > >
> > > > > > <td valign="top" style="background:#EFEFEF">
> > > > > >
> > > > > >
> > > > > > 打开一个流，以收集来自任何 document.write() 或 document.writeln() 方法的输出。
> > > > > >
> > > > > > </td>
> > > > > >
> > > > > > </tr>
> > > > > >
> > > > > > <tr>
> > > > > >
> > > > > > <td valign="top" style="background:#EFEFEF">
> > > > > >
> > > > > >
> > > > > > [<span style="color:#00B0F0">write()</span>](http://www.w3school.com.cn/jsref/met_doc_write.asp)
> > > > > >
> > > > > > </td>
> > > > > >
> > > > > > <td valign="top" style="background:#EFEFEF">
> > > > > >
> > > > > >
> > > > > > 向文档写 HTML 表达式 或 JavaScript 代码。
> > > > > >
> > > > > > </td>
> > > > > >
> > > > > > </tr>
> > > > > >
> > > > > > <tr>
> > > > > >
> > > > > > <td valign="top" style="background:#EFEFEF">
> > > > > >
> > > > > >
> > > > > > [<span style="color:#900B09">writeln()</span>](http://www.w3school.com.cn/jsref/met_doc_writeln.asp)
> > > > > >
> > > > > > </td>
> > > > > >
> > > > > > <td valign="top" style="background:#EFEFEF">
> > > > > >
> > > > > >
> > > > > > 等同于 write() 方法，不同的是在每个表达式之后写一个换行符。
> > > > > >
> > > > > > </td>
> > > > > >
> > > > > > </tr>
> > > > > >
> > > > > > </tbody>
> > > > > >
> > > > > > </table>

&nbsp;

**

**

**

**

**

**

**

**

**

**

**

**

**

**

**

**

**

**

**

**

## **2.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Element**

> 1.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;首先介绍结点node的概念：
> > 在 HTML DOM （文档对象模型）中，每个部分都是节点：
>
> > ·&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;文档本身是文档节点
>
> > ·&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;所有 HTML 元素是元素节点
>
> > ·&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;所有 HTML 属性是属性节点
>
> > ·&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;HTML 元素内的文本是文本节点
>
> > ·&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;注释是注释节点
> 2.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 再来看Element对象
> > 在 HTML DOM 中，Element 对象表示 HTML 元素。
>
> > Element 对象可以拥有类型为元素节点、文本节点、注释节点的子节点。
>
> > NodeList 对象表示节点列表，比如 HTML 元素的子节点集合。
>
> > 下面的属性和方法可用于所有 HTML 元素上：
<div align="center">
<table border="1" cellspacing="0" cellpadding="0" style="background:#F9F9F9">
<tbody>
<tr>
<td valign="bottom" style="background:#D5D5D5">

**属性 / 方法**

</td>
<td valign="bottom" style="background:#D5D5D5">

**描述**

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.accessKey</span>](http://www.w3school.com.cn/jsref/prop_html_accesskey.asp "HTML DOM accessKey 属性")

</td>
<td valign="top" style="background:#EFEFEF">

设置或返回元素的快捷键。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.appendChild()</span>](http://www.w3school.com.cn/jsref/met_node_appendchild.asp "HTML DOM appendChild() 方法")

</td>
<td valign="top" style="background:#EFEFEF">

向元素添加新的子节点，作为最后一个子节点。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.attributes</span>](http://www.w3school.com.cn/jsref/prop_node_attributes.asp "HTML DOM attributes 属性")

</td>
<td valign="top" style="background:#EFEFEF">

返回元素属性的 NamedNodeMap。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.childNodes</span>](http://www.w3school.com.cn/jsref/prop_node_childnodes.asp "HTML DOM childNodes 属性")

</td>
<td valign="top" style="background:#EFEFEF">

返回元素子节点的 NodeList。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.className</span>](http://www.w3school.com.cn/jsref/prop_html_classname.asp "HTML DOM className 属性")

</td>
<td valign="top" style="background:#EFEFEF">

设置或返回元素的 class 属性。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

element.clientHeight

</td>
<td valign="top" style="background:#EFEFEF">

返回元素的可见高度。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

element.clientWidth

</td>
<td valign="top" style="background:#EFEFEF">

返回元素的可见宽度。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.cloneNode()</span>](http://www.w3school.com.cn/jsref/met_node_clonenode.asp "HTML DOM cloneNode() 方法")

</td>
<td valign="top" style="background:#EFEFEF">

克隆元素。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.compareDocumentPosition()</span>](http://www.w3school.com.cn/jsref/met_node_comparedocumentposition.asp "HTML DOM compareDocumentPosition() 方法")

</td>
<td valign="top" style="background:#EFEFEF">

比较两个元素的文档位置。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.contentEditable</span>](http://www.w3school.com.cn/jsref/prop_html_contenteditable.asp "HTML DOM contentEditable 属性")

</td>
<td valign="top" style="background:#EFEFEF">

设置或返回元素的文本方向。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.dir</span>](http://www.w3school.com.cn/jsref/prop_html_dir.asp "HTML DOM dir 属性")

</td>
<td valign="top" style="background:#EFEFEF">

设置或返回元素的文本方向。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.firstChild</span>](http://www.w3school.com.cn/jsref/prop_node_firstchild.asp "HTML DOM firstChild 属性")

</td>
<td valign="top" style="background:#EFEFEF">

返回元素的首个子。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.getAttribute()</span>](http://www.w3school.com.cn/jsref/met_element_getattribute.asp "HTML DOM getAttribute() 方法")

</td>
<td valign="top" style="background:#EFEFEF">

返回元素节点的指定属性&#20540;。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.getAttributeNode()</span>](http://www.w3school.com.cn/jsref/met_element_getattributenode.asp "HTML DOM getAttributeNode() 方法")

</td>
<td valign="top" style="background:#EFEFEF">

返回指定的属性节点。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.getElementsByTagName()</span>](http://www.w3school.com.cn/jsref/met_element_getelementsbytagname.asp "HTML DOM getElementsByTagName() 方法")

</td>
<td valign="top" style="background:#EFEFEF">

返回拥有指定标签名的所有子元素的集合。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

element.getFeature()

</td>
<td valign="top" style="background:#EFEFEF">

返回实现了指定特性的 API 的某个对象。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

element.getUserData()

</td>
<td valign="top" style="background:#EFEFEF">

返回关联元素上键的对象。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.hasAttribute()</span>](http://www.w3school.com.cn/jsref/met_element_hasattribute.asp "HTML DOM hasAttribute() 方法")

</td>
<td valign="top" style="background:#EFEFEF">

如果元素拥有指定属性，则返回true，否则返回 false。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.hasAttributes()</span>](http://www.w3school.com.cn/jsref/met_node_hasattributes.asp "HTML DOM hasAttributes() 方法")

</td>
<td valign="top" style="background:#EFEFEF">

如果元素拥有属性，则返回 true，否则返回 false。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.hasChildNodes()</span>](http://www.w3school.com.cn/jsref/met_node_haschildnodes.asp "HTML DOM hasChildNodes() 方法")

</td>
<td valign="top" style="background:#EFEFEF">

如果元素拥有子节点，则返回 true，否则 false。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.id</span>](http://www.w3school.com.cn/jsref/prop_html_id.asp "HTML DOM id 属性")

</td>
<td valign="top" style="background:#EFEFEF">

设置或返回元素的 id。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#00B0F0">element.innerHTML</span>](http://www.w3school.com.cn/jsref/prop_html_innerhtml.asp "HTML DOM innerHTML 属性")

</td>
<td valign="top" style="background:#EFEFEF">

设置或返回元素的内容。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.insertBefore()</span>](http://www.w3school.com.cn/jsref/met_node_insertbefore.asp "HTML DOM insertBefore() 方法")

</td>
<td valign="top" style="background:#EFEFEF">

在指定的已有的子节点之前插入新节点。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.isContentEditable</span>](http://www.w3school.com.cn/jsref/prop_html_iscontenteditable.asp "HTML DOM isContentEditable 属性")

</td>
<td valign="top" style="background:#EFEFEF">

设置或返回元素的内容。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.isDefaultNamespace()</span>](http://www.w3school.com.cn/jsref/met_node_isdefaultnamespace.asp "HTML DOM isDefaultNamespace() 方法")

</td>
<td valign="top" style="background:#EFEFEF">

如果指定的 namespaceURI 是默认的，则返回 true，否则返回 false。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.isEqualNode()</span>](http://www.w3school.com.cn/jsref/met_node_isequalnode.asp "HTML DOM isEqualNode() 方法")

</td>
<td valign="top" style="background:#EFEFEF">

检查两个元素是否相等。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.isSameNode()</span>](http://www.w3school.com.cn/jsref/met_node_issamenode.asp "HTML DOM isSameNode() 方法")

</td>
<td valign="top" style="background:#EFEFEF">

检查两个元素是否是相同的节点。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.isSupported()</span>](http://www.w3school.com.cn/jsref/met_node_issupported.asp "HTML DOM isSupported() 方法")

</td>
<td valign="top" style="background:#EFEFEF">

如果元素支持指定特性，则返回 true。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.lang</span>](http://www.w3school.com.cn/jsref/prop_html_lang.asp "HTML DOM lang 属性")

</td>
<td valign="top" style="background:#EFEFEF">

设置或返回元素的语言代码。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.lastChild</span>](http://www.w3school.com.cn/jsref/prop_node_lastchild.asp "HTML DOM lastChild 属性")

</td>
<td valign="top" style="background:#EFEFEF">

返回元素的最后一个子元素。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.namespaceURI</span>](http://www.w3school.com.cn/jsref/prop_node_namespaceuri.asp "HTML DOM namespaceURI 属性")

</td>
<td valign="top" style="background:#EFEFEF">

返回元素的 namespace URI。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.nextSibling</span>](http://www.w3school.com.cn/jsref/prop_node_nextsibling.asp "HTML DOM nextSibling 属性")

</td>
<td valign="top" style="background:#EFEFEF">

返回位于相同节点树层级的下一个节点。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.nodeName</span>](http://www.w3school.com.cn/jsref/prop_node_nodename.asp "HTML DOM nodeName 属性")

</td>
<td valign="top" style="background:#EFEFEF">

返回元素的名称。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.nodeType</span>](http://www.w3school.com.cn/jsref/prop_node_nodetype.asp "HTML DOM nodeType 属性")

</td>
<td valign="top" style="background:#EFEFEF">

返回元素的节点类型。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.nodeValue</span>](http://www.w3school.com.cn/jsref/prop_node_nodevalue.asp "HTML DOM nodeValue 属性")

</td>
<td valign="top" style="background:#EFEFEF">

设置或返回元素&#20540;。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.normalize()</span>](http://www.w3school.com.cn/jsref/met_node_normalize.asp "HTML DOM normalize() 方法")

</td>
<td valign="top" style="background:#EFEFEF">

合并元素中相邻的文本节点，并移除空的文本节点。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

element.offsetHeight

</td>
<td valign="top" style="background:#EFEFEF">

返回元素的高度。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

element.offsetWidth

</td>
<td valign="top" style="background:#EFEFEF">

返回元素的宽度。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

element.offsetLeft

</td>
<td valign="top" style="background:#EFEFEF">

返回元素的水平偏移位置。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

element.offsetParent

</td>
<td valign="top" style="background:#EFEFEF">

返回元素的偏移容器。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

element.offsetTop

</td>
<td valign="top" style="background:#EFEFEF">

返回元素的垂直偏移位置。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.ownerDocument</span>](http://www.w3school.com.cn/jsref/prop_node_ownerdocument.asp "HTML DOM ownerDocument 属性")

</td>
<td valign="top" style="background:#EFEFEF">

返回元素的根元素（文档对象）。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.parentNode</span>](http://www.w3school.com.cn/jsref/prop_node_parentnode.asp "HTML DOM parentNode 属性")

</td>
<td valign="top" style="background:#EFEFEF">

返回元素的父节点。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.previousSibling</span>](http://www.w3school.com.cn/jsref/prop_node_previoussibling.asp "HTML DOM previousSibling 属性")

</td>
<td valign="top" style="background:#EFEFEF">

返回位于相同节点树层级的前一个元素。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.removeAttribute()</span>](http://www.w3school.com.cn/jsref/met_element_removeattribute.asp "HTML DOM removeAttribute() 方法")

</td>
<td valign="top" style="background:#EFEFEF">

从元素中移除指定属性。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.removeAttributeNode()</span>](http://www.w3school.com.cn/jsref/met_element_removeattributenode.asp "HTML DOM removeAttributeNode() 方法")

</td>
<td valign="top" style="background:#EFEFEF">

移除指定的属性节点，并返回被移除的节点。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.removeChild()</span>](http://www.w3school.com.cn/jsref/met_node_removechild.asp "HTML DOM removeChild() 方法")

</td>
<td valign="top" style="background:#EFEFEF">

从元素中移除子节点。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.replaceChild()</span>](http://www.w3school.com.cn/jsref/met_node_replacechild.asp "HTML DOM replaceChild() 方法")

</td>
<td valign="top" style="background:#EFEFEF">

替换元素中的子节点。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

element.scrollHeight

</td>
<td valign="top" style="background:#EFEFEF">

返回元素的整体高度。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

element.scrollLeft

</td>
<td valign="top" style="background:#EFEFEF">

返回元素左边缘与视图之间的距离。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

element.scrollTop

</td>
<td valign="top" style="background:#EFEFEF">

返回元素上边缘与视图之间的距离。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

element.scrollWidth

</td>
<td valign="top" style="background:#EFEFEF">

返回元素的整体宽度。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.setAttribute()</span>](http://www.w3school.com.cn/jsref/met_element_setattribute.asp "HTML DOM setAttribute() 方法")

</td>
<td valign="top" style="background:#EFEFEF">

把指定属性设置或更改为指定&#20540;。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.setAttributeNode()</span>](http://www.w3school.com.cn/jsref/met_element_setattributenode.asp "HTML DOM setAttributeNode() 方法")

</td>
<td valign="top" style="background:#EFEFEF">

设置或更改指定属性节点。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

element.setIdAttribute()

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

element.setIdAttributeNode()

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

element.setUserData()

</td>
<td valign="top" style="background:#EFEFEF">

把对象关联到元素上的键。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

element.style

</td>
<td valign="top" style="background:#EFEFEF">

设置或返回元素的 style 属性。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.tabIndex</span>](http://www.w3school.com.cn/jsref/prop_html_tabindex.asp "HTML DOM tabIndex 属性")

</td>
<td valign="top" style="background:#EFEFEF">

设置或返回元素的 tab 键控制次序。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.tagName</span>](http://www.w3school.com.cn/jsref/prop_element_tagname.asp "HTML DOM tagName 属性")

</td>
<td valign="top" style="background:#EFEFEF">

返回元素的标签名。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.textContent</span>](http://www.w3school.com.cn/jsref/prop_node_textcontent.asp "HTML DOM textContent 属性")

</td>
<td valign="top" style="background:#EFEFEF">

设置或返回节点及其后代的文本内容。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">element.title</span>](http://www.w3school.com.cn/jsref/prop_html_title.asp "HTML DOM title 属性")

</td>
<td valign="top" style="background:#EFEFEF">

设置或返回元素的 title 属性。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

element.toString()

</td>
<td valign="top" style="background:#EFEFEF">

把元素转换为字符串。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">nodelist.item()</span>](http://www.w3school.com.cn/jsref/met_nodelist_item.asp "HTML DOM item() 方法")

</td>
<td valign="top" style="background:#EFEFEF">

返回 NodeList 中位于指定下标的节点。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">nodelist.length</span>](http://www.w3school.com.cn/jsref/prop_nodelist_length.asp "HTML DOM length 属性")

</td>
<td valign="top" style="background:#EFEFEF">

返回 NodeList 中的节点数。

</td>
</tr>
</tbody>
</table>
</div>
> <span style="color:red">总结：方法和属性大多是对于</span><span style="color:red">html</span><span style="color:red">元素（或者说是</span><span style="color:red">DOM</span><span style="color:red">结点）的遍历、设置、操作等。</span>

## **3.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Attribute**

> Attr 对象
>
> 在 HTML DOM 中，Attr 对象表示 HTML 属性。
>
> HTML 属性始终属于 HTML 元素。
<div align="center">
<table border="1" cellspacing="0" cellpadding="0" style="background:#F9F9F9">
<tbody>
<tr>
<td valign="bottom" style="background:#D5D5D5">

**属性 / 方法**

</td>
<td valign="bottom" style="background:#D5D5D5">

**描述**

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">attr.isId</span>](http://www.w3school.com.cn/jsref/prop_attr_isid.asp "HTML DOM isId 属性")

</td>
<td valign="top" style="background:#EFEFEF">

如果属性是 id 类型，则返回 true，否则返回 false。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">attr.name</span>](http://www.w3school.com.cn/jsref/prop_attr_name.asp "HTML DOM name 属性")

</td>
<td valign="top" style="background:#EFEFEF">

返回属性的名称。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">attr.value</span>](http://www.w3school.com.cn/jsref/prop_attr_value.asp "HTML DOM value 属性")

</td>
<td valign="top" style="background:#EFEFEF">

设置或返回属性的&#20540;。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">attr.specified</span>](http://www.w3school.com.cn/jsref/prop_attr_specified.asp "HTML DOM specified 属性")

</td>
<td valign="top" style="background:#EFEFEF">

如果已指定属性，则返回 true，否则返回 false。

</td>
</tr>
</tbody>
</table>
</div>

&nbsp;

## **4.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Event**

> Event 对象代表事件的状态，比如事件在其中发生的元素、键盘按键的状态、鼠标的位置、鼠标按钮的状态。
>
> 事件通常与函数结合使用，函数不会在事件发生前被执行！
> > > > > > > > > > > > **事件句柄　(Event Handlers)**
<div align="center">
<table border="1" cellspacing="0" cellpadding="0" width="407" style="background:#F9F9F9">
<tbody>
<tr>
<td valign="bottom" style="background:#D5D5D5">

**属性**

</td>
<td valign="bottom" style="background:#D5D5D5">

**此事件发生在何时...**

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">onabort</span>](http://www.w3school.com.cn/jsref/event_onabort.asp)

</td>
<td valign="top" style="background:#EFEFEF">

图像的加载被中断。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">onblur</span>](http://www.w3school.com.cn/jsref/event_onblur.asp)

</td>
<td valign="top" style="background:#EFEFEF">

元素失去焦点。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">onchange</span>](http://www.w3school.com.cn/jsref/event_onchange.asp)

</td>
<td valign="top" style="background:#EFEFEF">

域的内容被改变。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">onclick</span>](http://www.w3school.com.cn/jsref/event_onclick.asp)

</td>
<td valign="top" style="background:#EFEFEF">

当用户点击某个对象时调用的事件句柄。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">ondblclick</span>](http://www.w3school.com.cn/jsref/event_ondblclick.asp)

</td>
<td valign="top" style="background:#EFEFEF">

当用户双击某个对象时调用的事件句柄。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">onerror</span>](http://www.w3school.com.cn/jsref/event_onerror.asp)

</td>
<td valign="top" style="background:#EFEFEF">

在加载文档或图像时发生错误。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">onfocus</span>](http://www.w3school.com.cn/jsref/event_onfocus.asp)

</td>
<td valign="top" style="background:#EFEFEF">

元素获得焦点。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">onkeydown</span>](http://www.w3school.com.cn/jsref/event_onkeydown.asp)

</td>
<td valign="top" style="background:#EFEFEF">

某个键盘按键被按下。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">onkeypress</span>](http://www.w3school.com.cn/jsref/event_onkeypress.asp)

</td>
<td valign="top" style="background:#EFEFEF">

某个键盘按键被按下并松开。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">onkeyup</span>](http://www.w3school.com.cn/jsref/event_onkeyup.asp)

</td>
<td valign="top" style="background:#EFEFEF">

某个键盘按键被松开。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">onload</span>](http://www.w3school.com.cn/jsref/event_onload.asp)

</td>
<td valign="top" style="background:#EFEFEF">

一张页面或一幅图像完成加载。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">onmousedown</span>](http://www.w3school.com.cn/jsref/event_onmousedown.asp)

</td>
<td valign="top" style="background:#EFEFEF">

鼠标按钮被按下。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">onmousemove</span>](http://www.w3school.com.cn/jsref/event_onmousemove.asp)

</td>
<td valign="top" style="background:#EFEFEF">

鼠标被移动。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">onmouseout</span>](http://www.w3school.com.cn/jsref/event_onmouseout.asp)

</td>
<td valign="top" style="background:#EFEFEF">

鼠标从某元素移开。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">onmouseover</span>](http://www.w3school.com.cn/jsref/event_onmouseover.asp)

</td>
<td valign="top" style="background:#EFEFEF">

鼠标移到某元素之上。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">onmouseup</span>](http://www.w3school.com.cn/jsref/event_onmouseup.asp)

</td>
<td valign="top" style="background:#EFEFEF">

鼠标按键被松开。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">onreset</span>](http://www.w3school.com.cn/jsref/event_onreset.asp)

</td>
<td valign="top" style="background:#EFEFEF">

重置按钮被点击。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">onresize</span>](http://www.w3school.com.cn/jsref/event_onresize.asp)

</td>
<td valign="top" style="background:#EFEFEF">

窗口或框架被重新调整大小。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">onselect</span>](http://www.w3school.com.cn/jsref/event_onselect.asp)

</td>
<td valign="top" style="background:#EFEFEF">

文本被选中。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">onsubmit</span>](http://www.w3school.com.cn/jsref/event_onsubmit.asp)

</td>
<td valign="top" style="background:#EFEFEF">

确认按钮被点击。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">onunload</span>](http://www.w3school.com.cn/jsref/event_onunload.asp)

</td>
<td valign="top" style="background:#EFEFEF">

用户退出页面。

</td>
</tr>
</tbody>
</table>
</div>
> > > > > > > > > > &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**&nbsp;&nbsp; 标准 Event 属性：**
> > > > > > > > > > > > **下面列出了 2 级 DOM 事件标准定义的属性**。
<div align="center">
<table border="1" cellspacing="0" cellpadding="0" width="378">
<tbody>
<tr>
<td valign="bottom" style="background:#D5D5D5">

**属性**

</td>
<td valign="bottom" style="background:#D5D5D5">

**描述**

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">bubbles</span>](http://www.w3school.com.cn/jsref/event_bubbles.asp)

</td>
<td valign="top" style="background:#EFEFEF">

返回布尔&#20540;，指示事件是否是起泡事件类型。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">cancelable</span>](http://www.w3school.com.cn/jsref/event_cancelable.asp)

</td>
<td valign="top" style="background:#EFEFEF">

返回布尔&#20540;，指示事件是否可拥可取消的默认动作。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">currentTarget</span>](http://www.w3school.com.cn/jsref/event_currenttarget.asp)

</td>
<td valign="top" style="background:#EFEFEF">

返回其事件监听器触发该事件的元素。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">eventPhase</span>](http://www.w3school.com.cn/jsref/event_eventphase.asp)

</td>
<td valign="top" style="background:#EFEFEF">

返回事件传播的当前阶段。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#00B0F0">target</span>](http://www.w3school.com.cn/jsref/event_target.asp)

</td>
<td valign="top" style="background:#EFEFEF">

返回触发此事件的元素（事件的目标节点）。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#00B0F0">timeStamp</span>](http://www.w3school.com.cn/jsref/event_timestamp.asp)

</td>
<td valign="top" style="background:#EFEFEF">

返回事件生成的日期和时间。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">type</span>](http://www.w3school.com.cn/jsref/event_type.asp)

</td>
<td valign="top" style="background:#EFEFEF">

返回当前 Event 对象表示的事件的名称。

</td>
</tr>
</tbody>
</table>
</div>

&nbsp;

> > > > > > > > > > > > **标准 Event 方法：**
>
> > > > > > > > > > > > **下面列出了 2 级 DOM 事件标准定义的方法。IE 的事件模型不支持这些方法：**
<div align="center">
<table border="1" cellspacing="0" cellpadding="0" width="378">
<tbody>
<tr>
<td valign="bottom" style="background:#D5D5D5">

**方法**

</td>
<td valign="bottom" style="background:#D5D5D5">

**描述**

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">initEvent()</span>](http://www.w3school.com.cn/jsref/event_initevent.asp)

</td>
<td valign="top" style="background:#EFEFEF">

初始化新创建的 Event 对象的属性。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#00B0F0">preventDefault()</span>](http://www.w3school.com.cn/jsref/event_preventdefault.asp)

</td>
<td valign="top" style="background:#EFEFEF">

通知浏览器不要执行与事件关联的默认动作。

</td>
</tr>
<tr>
<td nowrap="nowrap" valign="top" style="background:#EFEFEF">

[<span style="color:#00B0F0">stopPropagation()</span>](http://www.w3school.com.cn/jsref/event_stoppropagation.asp)

</td>
<td valign="top" style="background:#EFEFEF">

不再派发事件。

</td>
</tr>
</tbody>
</table>
</div>

&nbsp;

# **二、&nbsp;&nbsp;BOM对象**

**包括：Window、Navigator、Screen、History、Location五大对象**

## **1.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Window**

> Window 对象表示浏览器中打开的窗口。
>
> <span style="color:red">如果文档包含框架（</span><span style="color:red">frame </span><span style="color:red">或</span><span style="color:red"> iframe</span><span style="color:red">标签），浏览器会为</span><span style="color:red"> HTML
>
> </span><span style="color:red">文档创建一个</span><span style="color:red"> window</span><span style="color:red">对象，并为每个框架创建一个额外的</span><span style="color:red"> window</span><span style="color:red">对象。</span>
>
> <span style="color:red">注释：</span>没有应用于 window 对象的公开标准，不过所有浏览器都支持该对象。
>
> &nbsp;
>
> Window 对象是全局对象，使用时直接使用它的属性和方法。Window 对象的 window 属性和 self 属性引用的都是它自己。当你想明确地引用当前窗口，而不仅仅是隐式地引用它时，可以使用这两个属性。

&nbsp;

> > > > > > > > > > > > **Window 对象属性**
<div align="center">
<table border="1" cellspacing="0" cellpadding="0" width="378">
<tbody>
<tr>
<td valign="bottom" style="background:#D5D5D5">

属性

</td>
<td valign="bottom" style="background:#D5D5D5">

描述

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">closed</span>](http://www.w3school.com.cn/jsref/prop_win_closed.asp)

</td>
<td valign="top" style="background:#EFEFEF">

返回窗口是否已被关闭。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">defaultStatus</span>](http://www.w3school.com.cn/jsref/prop_win_defaultstatus.asp)

</td>
<td valign="top" style="background:#EFEFEF">

设置或返回窗口状态栏中的默认文本。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#00B0F0">document</span>](http://www.w3school.com.cn/jsref/dom_obj_document.asp)

</td>
<td valign="top" style="background:#EFEFEF">

对 Document 对象的只读引用。请参阅&nbsp;[<span style="color:#900B09">Document</span><span style="color:#900B09">对象</span>](http://www.w3school.com.cn/jsref/dom_obj_document.asp)。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#00B0F0">history</span>](http://www.w3school.com.cn/jsref/dom_obj_history.asp)

</td>
<td valign="top" style="background:#EFEFEF">

对 History 对象的只读引用。请参数&nbsp;[<span style="color:#900B09">History</span><span style="color:#900B09">对象</span>](http://www.w3school.com.cn/jsref/dom_obj_history.asp)。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">innerheight</span>](http://www.w3school.com.cn/jsref/prop_win_innerheight_innerwidth.asp)

</td>
<td valign="top" style="background:#EFEFEF">

返回窗口的文档显示区的高度。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">innerwidth</span>](http://www.w3school.com.cn/jsref/prop_win_innerheight_innerwidth.asp)

</td>
<td valign="top" style="background:#EFEFEF">

返回窗口的文档显示区的宽度。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

length

</td>
<td valign="top" style="background:#EFEFEF">

设置或返回窗口中的框架数量。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#00B0F0">location</span>](http://www.w3school.com.cn/jsref/dom_obj_location.asp)

</td>
<td valign="top" style="background:#EFEFEF">

用于窗口或框架的 Location 对象。请参阅&nbsp;[<span style="color:#900B09">Location</span><span style="color:#900B09">对象</span>](http://www.w3school.com.cn/jsref/dom_obj_location.asp)。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">name</span>](http://www.w3school.com.cn/jsref/prop_win_name.asp)

</td>
<td valign="top" style="background:#EFEFEF">

设置或返回窗口的名称。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">Navigator</span>](http://www.w3school.com.cn/jsref/dom_obj_navigator.asp)

</td>
<td valign="top" style="background:#EFEFEF">

对 Navigator 对象的只读引用。请参数&nbsp;[<span style="color:#900B09">Navigator</span><span style="color:#900B09">对象</span>](http://www.w3school.com.cn/jsref/dom_obj_navigator.asp)。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">opener</span>](http://www.w3school.com.cn/jsref/prop_win_opener.asp)

</td>
<td valign="top" style="background:#EFEFEF">

返回对创建此窗口的窗口的引用。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">outerheight</span>](http://www.w3school.com.cn/jsref/prop_win_outerheight.asp)

</td>
<td valign="top" style="background:#EFEFEF">

返回窗口的外部高度。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">outerwidth</span>](http://www.w3school.com.cn/jsref/prop_win_outerwidth.asp)

</td>
<td valign="top" style="background:#EFEFEF">

返回窗口的外部宽度。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

pageXOffset

</td>
<td valign="top" style="background:#EFEFEF">

设置或返回当前页面相对于窗口显示区左上角的 X 位置。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

pageYOffset

</td>
<td valign="top" style="background:#EFEFEF">

设置或返回当前页面相对于窗口显示区左上角的 Y 位置。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

parent

</td>
<td valign="top" style="background:#EFEFEF">

返回父窗口。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">Screen</span>](http://www.w3school.com.cn/jsref/dom_obj_screen.asp)

</td>
<td valign="top" style="background:#EFEFEF">

对 Screen 对象的只读引用。请参数&nbsp;[<span style="color:#900B09">Screen</span><span style="color:#900B09">对象</span>](http://www.w3school.com.cn/jsref/dom_obj_screen.asp)。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">self</span>](http://www.w3school.com.cn/jsref/prop_win_self.asp)

</td>
<td valign="top" style="background:#EFEFEF">

返回对当前窗口的引用。等价于 Window 属性。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">status</span>](http://www.w3school.com.cn/jsref/prop_win_status.asp)

</td>
<td valign="top" style="background:#EFEFEF">

设置窗口状态栏的文本。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">top</span>](http://www.w3school.com.cn/jsref/prop_win_top.asp)

</td>
<td valign="top" style="background:#EFEFEF">

返回最顶层的先辈窗口。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

window

</td>
<td valign="top" style="background:#EFEFEF">

window 属性等价于 self 属性，它包含了对窗口自身的引用。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

screenLeft

screenTop

screenX

screenY

</td>
<td valign="top" style="background:#EFEFEF">

只读整数。声明了窗口的左上角在屏幕上的的 x 坐标和 y 坐标。IE、Safari 和 Opera 支持 screenLeft 和 screenTop，而 Firefox 和 Safari 支持 screenX 和 screenY。

</td>
</tr>
</tbody>
</table>
</div>

<span style="white-space:pre"></span>**Window 对象方法**

<div align="center">
<table border="1" cellspacing="0" cellpadding="0" width="378">
<tbody>
<tr>
<td valign="bottom" style="background:#D5D5D5">

方法

</td>
<td valign="bottom" style="background:#D5D5D5">

描述

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#00B0F0">alert()</span>](http://www.w3school.com.cn/jsref/met_win_alert.asp)

</td>
<td valign="top" style="background:#EFEFEF">

显示带有一段消息和一个确认按钮的警告框。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">blur()</span>](http://www.w3school.com.cn/jsref/met_win_blur.asp)

</td>
<td valign="top" style="background:#EFEFEF">

把键盘焦点从顶层窗口移开。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#00B0F0">clearInterval()</span>](http://www.w3school.com.cn/jsref/met_win_clearinterval.asp)

</td>
<td valign="top" style="background:#EFEFEF">

取消由 setInterval() 设置的 timeout。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#00B0F0">clearTimeout()</span>](http://www.w3school.com.cn/jsref/met_win_cleartimeout.asp)

</td>
<td valign="top" style="background:#EFEFEF">

取消由 setTimeout() 方法设置的 timeout。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#00B0F0">close()</span>](http://www.w3school.com.cn/jsref/met_win_close.asp)

</td>
<td valign="top" style="background:#EFEFEF">

关闭浏览器窗口。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">confirm()</span>](http://www.w3school.com.cn/jsref/met_win_confirm.asp)

</td>
<td valign="top" style="background:#EFEFEF">

显示带有一段消息以及确认按钮和取消按钮的对话框。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">createPopup()</span>](http://www.w3school.com.cn/jsref/met_win_createpopup.asp)

</td>
<td valign="top" style="background:#EFEFEF">

创建一个 pop-up 窗口。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">focus()</span>](http://www.w3school.com.cn/jsref/met_win_focus.asp)

</td>
<td valign="top" style="background:#EFEFEF">

把键盘焦点给予一个窗口。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">moveBy()</span>](http://www.w3school.com.cn/jsref/met_win_moveby.asp)

</td>
<td valign="top" style="background:#EFEFEF">

可相对窗口的当前坐标把它移动指定的像素。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">moveTo()</span>](http://www.w3school.com.cn/jsref/met_win_moveto.asp)

</td>
<td valign="top" style="background:#EFEFEF">

把窗口的左上角移动到一个指定的坐标。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#00B0F0">open()</span>](http://www.w3school.com.cn/jsref/met_win_open.asp)

</td>
<td valign="top" style="background:#EFEFEF">

打开一个新的浏览器窗口或查找一个已命名的窗口。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">print()</span>](http://www.w3school.com.cn/jsref/met_win_print.asp)

</td>
<td valign="top" style="background:#EFEFEF">

打印当前窗口的内容。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">prompt()</span>](http://www.w3school.com.cn/jsref/met_win_prompt.asp)

</td>
<td valign="top" style="background:#EFEFEF">

显示可提示用户输入的对话框。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">resizeBy()</span>](http://www.w3school.com.cn/jsref/met_win_resizeby.asp)

</td>
<td valign="top" style="background:#EFEFEF">

按照指定的像素调整窗口的大小。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#00B0F0">resizeTo()</span>](http://www.w3school.com.cn/jsref/met_win_resizeto.asp)

</td>
<td valign="top" style="background:#EFEFEF">

把窗口的大小调整到指定的宽度和高度。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">scrollBy()</span>](http://www.w3school.com.cn/jsref/met_win_scrollby.asp)

</td>
<td valign="top" style="background:#EFEFEF">

按照指定的像素&#20540;来滚动内容。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">scrollTo()</span>](http://www.w3school.com.cn/jsref/met_win_scrollto.asp)

</td>
<td valign="top" style="background:#EFEFEF">

把内容滚动到指定的坐标。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#00B0F0">setInterval()</span>](http://www.w3school.com.cn/jsref/met_win_setinterval.asp)

</td>
<td valign="top" style="background:#EFEFEF">

按照指定的周期（以毫秒计）来调用函数或计算表达式。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#00B0F0">setTimeout()</span>](http://www.w3school.com.cn/jsref/met_win_settimeout.asp)

</td>
<td valign="top" style="background:#EFEFEF">

在指定的毫秒数后调用函数或计算表达式。

</td>
</tr>
</tbody>
</table>
</div>

&nbsp;

## **2.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Navigator**

> Navigator 对象包含有关浏览器的信息。

## **3.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Screen**

> Screen 对象包含有关客户端显示屏幕的信息。

## **4.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;History**

> History 对象包含用户（在浏览器窗口中）访问过的 URL。
>
> History 对象是 window 对象的一部分，可通过 window.history 属性对其进行访问。
> > > > > > > > > > > > **History 对象属性**
<div align="center">
<table border="1" cellspacing="0" cellpadding="0" width="378">
<tbody>
<tr>
<td valign="bottom" style="background:#D5D5D5">

属性

</td>
<td valign="bottom" style="background:#D5D5D5">

描述

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">length</span>](http://www.w3school.com.cn/jsref/prop_his_length.asp)

</td>
<td valign="top" style="background:#EFEFEF">

返回浏览器历史列表中的 URL 数量。

</td>
</tr>
</tbody>
</table>
</div>
> > > > > > > > > > > > **History 对象方法**
<div align="center">
<table border="1" cellspacing="0" cellpadding="0" width="378">
<tbody>
<tr>
<td valign="bottom" style="background:#D5D5D5">

方法

</td>
<td valign="bottom" style="background:#D5D5D5">

描述

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#00B0F0">back()</span>](http://www.w3school.com.cn/jsref/met_his_back.asp)

</td>
<td valign="top" style="background:#EFEFEF">

加载 history 列表中的前一个 URL。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#00B0F0">forward()</span>](http://www.w3school.com.cn/jsref/met_his_forward.asp)

</td>
<td valign="top" style="background:#EFEFEF">

加载 history 列表中的下一个 URL。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#00B0F0">go()</span>](http://www.w3school.com.cn/jsref/met_his_go.asp)

</td>
<td valign="top" style="background:#EFEFEF">

加载 history 列表中的某个具体页面。

</td>
</tr>
</tbody>
</table>
</div>

&nbsp;

## **5.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Location**

> Location对象包含有关当前 URL 的信息。
>
> Location对象是 Window 对象的一个部分，可通过 window.location 属性来访问。
> > > > > > > > > > > > **Location 对象属性**
<div align="center">
<table border="1" cellspacing="0" cellpadding="0" width="378">
<tbody>
<tr>
<td valign="bottom" style="background:#D5D5D5">

属性

</td>
<td valign="bottom" style="background:#D5D5D5">

描述

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">hash</span>](http://www.w3school.com.cn/jsref/prop_loc_hash.asp)

</td>
<td valign="top" style="background:#EFEFEF">

设置或返回从井号 (#) 开始的 URL（锚）。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#00B0F0">host</span>](http://www.w3school.com.cn/jsref/prop_loc_host.asp)

</td>
<td valign="top" style="background:#EFEFEF">

设置或返回主机名和当前 URL 的端口号。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#00B0F0">hostname</span>](http://www.w3school.com.cn/jsref/prop_loc_hostname.asp)

</td>
<td valign="top" style="background:#EFEFEF">

设置或返回当前 URL 的主机名。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#00B0F0">href</span>](http://www.w3school.com.cn/jsref/prop_loc_href.asp)

</td>
<td valign="top" style="background:#EFEFEF">

设置或返回完整的 URL。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#00B0F0">pathname</span>](http://www.w3school.com.cn/jsref/prop_loc_pathname.asp)

</td>
<td valign="top" style="background:#EFEFEF">

设置或返回当前 URL 的路径部分。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#00B0F0">port</span>](http://www.w3school.com.cn/jsref/prop_loc_port.asp)

</td>
<td valign="top" style="background:#EFEFEF">

设置或返回当前 URL 的端口号。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#00B0F0">protocol</span>](http://www.w3school.com.cn/jsref/prop_loc_protocol.asp)

</td>
<td valign="top" style="background:#EFEFEF">

设置或返回当前 URL 的协议。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">search</span>](http://www.w3school.com.cn/jsref/prop_loc_search.asp)

</td>
<td valign="top" style="background:#EFEFEF">

设置或返回从问号 (?) 开始的 URL（查询部分）。

</td>
</tr>
</tbody>
</table>
</div>
> > > > > > > > > > > > **Location 对象方法**
<div align="center">
<table border="1" cellspacing="0" cellpadding="0" width="378">
<tbody>
<tr>
<td valign="bottom" style="background:#D5D5D5">

属性

</td>
<td valign="bottom" style="background:#D5D5D5">

描述

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">assign()</span>](http://www.w3school.com.cn/jsref/met_loc_assign.asp)

</td>
<td valign="top" style="background:#EFEFEF">

加载新的文档。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">reload()</span>](http://www.w3school.com.cn/jsref/met_loc_reload.asp)

</td>
<td valign="top" style="background:#EFEFEF">

重新加载当前文档。

</td>
</tr>
<tr>
<td valign="top" style="background:#EFEFEF">

[<span style="color:#900B09">replace()</span>](http://www.w3school.com.cn/jsref/met_loc_replace.asp)

</td>
<td valign="top" style="background:#EFEFEF">

用新的文档替换当前文档。

</td>
</tr>
</tbody>
</table>
</div>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 可以使用window.location.href=”newurl”改变地址栏的地址并跳转。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 注：以上的所有的属性和方法中被蓝色标注的为较为常见的内容。

&nbsp;

&nbsp;

&nbsp;

**<span style="color:#ff0000">附：BOM对象、DOM对象以及元素对象的关系图</span>**

![]()

            <div>
                作者：z893196569 发表于2015/9/23 19:37:16 [原文链接](http://blog.csdn.net/z893196569/article/details/48685701)
            </div>
            <div>
            阅读：67 评论：0 [查看评论](http://blog.csdn.net/z893196569/article/details/48685701#comments)
            </div>
