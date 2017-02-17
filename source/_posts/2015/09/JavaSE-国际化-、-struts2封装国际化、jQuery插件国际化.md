---
title: 'JavaSE 国际化 、 struts2封装国际化、jQuery插件国际化'
tags:
-
categories:
- Java
date: 2015-09-08 13:12:18
---

今天做项目负责i18n国际化，索性总结一下，以下部分来自网络，已注明出处

* * *

**一、    Java 国际化**

**1\.    步骤：**

> 1)    定义国际化资源文件
>
>   2)    根据软件的语言环境取得对应的资源文件
>
>   3)    根据key取得对应的资源文件的对应字段的value值

**2\.    知识内容**

1)  Java程序的国际化主要通过如下3个类完成

> Java.util.ResourceBundle:用于加载资源包
>        Java.util.Locale:对应一个特定的国家/地区、语言环境
>        Java.text.MessageFormat:用于将消息格式化
>     `</pre>

    ![这里写图片描述](http://img.blog.csdn.net/20150908131754018)

    2)  资源文件的命名可以是如下3种形式：

    <pre class="prettyprint">`         baseName_language_country<span class="hljs-preprocessor">.properties</span>
             baseName_language<span class="hljs-preprocessor">.properties</span>
             baseName<span class="hljs-preprocessor">.properties</span>`</pre>

    其中baseName是资源文件的基本名称，用户可以自由定义，而language和country都不可随意变化，必须是Java所支持的语言和国家。

    **3\.    示例**

    《1》首先编写两个资源文件，例如：

                          resource_zh_CN.properties： title=标题

                   resource_en_US.properties：title=title    

    《2》中文的可以使用jdk的native2ascii 命令进行转码Unicode编码。

              命令： native2ascii resource_zh_CN..properties  teme.properties然后在将转好的编码拷贝替换到resource_zh_CN.properties,替换后是：title=\u6807\u9898

    <pre class="prettyprint">` package com.ascent.i18n.test;  
        import java.util.*;  
        <span class="hljs-keyword">public</span> <span class="hljs-keyword">class</span> ResourceBundleTest {  
            <span class="hljs-keyword">public</span> <span class="hljs-keyword">static</span> <span class="hljs-keyword">void</span> <span class="hljs-title">main</span>(String[] args) {  
                <span class="hljs-comment">//设置本地区语言（默认）  </span>
                Locale locale = Locale.getDefault();  
                <span class="hljs-comment">//可以使用Local的常量设置具体的语言环境  </span>
                <span class="hljs-comment">//Locale locale = Locale.US;  </span>
                <span class="hljs-comment">//根据地区不同加载不同的资源文件  </span>
                ResourceBundle rb = ResourceBundle.getBundle(<span class="hljs-string">"resource"</span>, locale);  
                <span class="hljs-comment">//根据key获得value值  </span>
                String title = rb.getString(<span class="hljs-string">"title"</span>);  
                System.<span class="hljs-keyword">out</span>.println(title);  
            }  
        }`</pre>

    《3》Java国际化包含占位符的消息  

    以上在资源文件配置的消息都是简单的消息，假如消息中含有参数，即有参数占位，我们

    如何实现呢？例如下面消息：

    > 英文：hello=Hello,{0}!Today is {1}.  
>
>       中文：hello=你好，{0}!今天是{1}.

    此时，我们需要使用MessageFormat类，该类有个很有用的静态的方法

    **format(String pattern,value1，value2…)**  

    返回后面多个参数值填充前面pattern字符串，其中pattern字符串就是一个带占位符的字符串。Value1代表第一个占位符的实际值，value2代表第二个占位符的值…

    <pre>`package com.ascent.i18n.test;  
    import java.util.Date;  
    import java.util.Locale;  
    import java.util.ResourceBundle;  
    import java.text.*;  
    public class MessageFormatTest {  
        public static void main(String[] args) {  
            Locale locale = Locale.getDefault();  
            ResourceBundle rb = ResourceBundle.getBundle("resource", locale);  
            String hello = rb.getString("hello");  
            String result = MessageFormat.format(hello, "焦学理",new Date());  
            System.out.println(result);  
        }  
    }  
    `</pre>

    * * *

    **二、    struts2封装国际化**

    Struts 2国际化是建立在Java国际化的基础之上，一样也是通过提供不同国家/语言环境的消息资源，然后通过ResourceBundle加载指定Locale对应的资源文件，再取得该资源文件中指定key对应的消息—整个过程与Java程序的国际化完全相同，只是Struts2框架对Java程序国际化进行了进一步封装，从而简化了应用程序的国际化。

    > 1)定义国际化资源文件  
>
>       2)在struts2.xml中配置常量  
>
>       3)在页面中通过struts标签获取资源文件里的值

    **1)    定义国际化资源文件的格式**

    有两种定义格式：

    > 1.  global_en.properties、global_zh.properties定义于全局，放在src目录下。
> 2.  package_en.properties、package_zh.properties定义于某个包下，可以定义多组位于不同的包下。

    **2)    在struts2.xml中配置常量**

    > `&lt;constant name="struts.custom.i18n.resources" value="package" /&gt;`
>
>       `&lt;constant name="struts.custom.i18n.resources" value="global" /&gt;`

    即启用全局和所有包下的i18n的资源文件。两者之间不冲突。

    **3)    在页面中设置local变量**

    往往在登陆页面给用户选择一个语言环境。

    <pre class="prettyprint">`<span class="hljs-tag">&lt;<span class="hljs-title">a</span> <span class="hljs-attribute">href</span>=<span class="hljs-value">"&lt;%=basePath%&gt;?local=zh_CN"</span>&gt;</span>中文<span class="hljs-tag">&lt;/<span class="hljs-title">a</span>&gt;</span>
    <span class="hljs-tag">&lt;<span class="hljs-title">a</span> <span class="hljs-attribute">href</span>=<span class="hljs-value">"&lt;%=basePath%&gt;?local=en_US"</span>&gt;</span>英文<span class="hljs-tag">&lt;/<span class="hljs-title">a</span>&gt;</span>`</pre>

    **_由于struts2的封装，在拦截器栈中有i18n的设置，当发现链接中存在local=x，则将x保存在session中作为local变量的值。所以在登陆页面选择一个语言环境后，所有的页面就会自动选择对应的语言配置文件。不会出现后面的页面和前面的页面的语言环境不统一的情况。_**

    **4)    取值使用**

    a)  JSP页面中通过标签输出国际化消息

    启用struts标签：`&lt;%@ taglib uri="/struts-tags" prefix="s"%&gt;`

1.  `&lt;s:text name="xx"/&gt;`      xx为properties文件里的key。
2.  `&lt;s:label name="xx"/&gt;`
3.  表单元素的name作为提交时的字段名称被使用了，所以要使用key属性：

    <pre class="prettyprint">`        <span class="hljs-tag">&lt;<span class="hljs-title">s:form</span> <span class="hljs-attribute">action</span>=<span class="hljs-value">"Login"</span> <span class="hljs-attribute">method</span>=<span class="hljs-value">"post"</span>&gt;</span>  
            <span class="hljs-tag">&lt;<span class="hljs-title">s:textfield</span> <span class="hljs-attribute">name</span>=<span class="hljs-value">"username"</span> <span class="hljs-attribute">key</span>=<span class="hljs-value">"xx"</span>/&gt;</span>  
            <span class="hljs-tag">&lt;<span class="hljs-title">s:password</span> <span class="hljs-attribute">name</span>=<span class="hljs-value">"password"</span> <span class="hljs-attribute">key</span>=<span class="hljs-value">"xx"</span>/&gt;</span>  
            <span class="hljs-tag">&lt;<span class="hljs-title">s:submit</span> <span class="hljs-attribute">name</span>=<span class="hljs-value">"submit"</span> <span class="hljs-attribute">key</span>=<span class="hljs-value">"xx"</span> /&gt;</span>  
            <span class="hljs-tag">&lt;/<span class="hljs-title">s:form</span>&gt;</span>`</pre>

    4.`&lt;s:property value="getText('xx')"/&gt;`

     5\. 指定properties文件

    <pre class="prettyprint">`<span class="hljs-tag">&lt;<span class="hljs-title">s:i18n</span> <span class="hljs-attribute">name</span>=<span class="hljs-value">"x"</span>&gt;</span>
        <span class="hljs-tag">&lt;<span class="hljs-title">s:text</span> <span class="hljs-attribute">name</span>=<span class="hljs-value">"xx"</span>&gt;</span><span class="hljs-tag">&lt;/<span class="hljs-title">s:text</span>&gt;</span>
    <span class="hljs-tag">&lt;/<span class="hljs-title">s:i18n</span>&gt;</span>`</pre>

    b）在Action类中使用国际化消息

    使用ActionSupport类的getText方法,该方法可以接受一个name 参数,该参数指定了国际化资源文件中的key

    <pre class="prettyprint">`    <span class="hljs-keyword">public</span> <span class="hljs-class"><span class="hljs-keyword">class</span> <span class="hljs-title">LoginAction</span> <span class="hljs-keyword">extends</span> <span class="hljs-title">ActionSupport</span>{</span>  
            <span class="hljs-keyword">public</span> String <span class="hljs-title">execute</span>(){  
                <span class="hljs-keyword">if</span>(getUsername().equals(<span class="hljs-string">"ascent"</span>)&amp;&amp; getPassword().equals(<span class="hljs-string">"ascent"</span>)){  
                ActionContext.getContext().getSession().put(<span class="hljs-string">"user"</span>, <span class="hljs-keyword">this</span>.getUsername());  
                <span class="hljs-keyword">return</span> SUCCESS;  
                }  
                <span class="hljs-keyword">return</span> ERROR;  
            }  
            <span class="hljs-comment">//完成输入校验需要重写的validate方法（读取资源文件getText(String str)）  </span>
            <span class="hljs-keyword">public</span> <span class="hljs-keyword">void</span> <span class="hljs-title">validate</span>(){  
                <span class="hljs-comment">//调用getText方法取出国际化信息  </span>
                <span class="hljs-keyword">if</span>(getUsername()==<span class="hljs-keyword">null</span>||<span class="hljs-string">""</span>.equals(<span class="hljs-keyword">this</span>.getUsername().trim())){  
                    <span class="hljs-keyword">this</span>.addFieldError(<span class="hljs-string">"username"</span>, <span class="hljs-keyword">this</span>.getText(<span class="hljs-string">"username.required"</span>));  
                }  
                <span class="hljs-keyword">if</span>(<span class="hljs-keyword">this</span>.getPassword()==<span class="hljs-keyword">null</span>||<span class="hljs-string">""</span>.equals(<span class="hljs-keyword">this</span>.getPassword().trim())){  
                    <span class="hljs-keyword">this</span>.addFieldError(<span class="hljs-string">"password"</span>, <span class="hljs-keyword">this</span>.getText(<span class="hljs-string">"password.required"</span>));  
                }  
            }  
    }  `</pre>

    c)  参数化国际化字符串 （带有占位符）

    许多情况下，我们都需要在运行时（runtime）为国际化字符插入一些参数，例如在输入验证提示信息的时候。在Struts 2.0中，我们通过可以方便地做到这点。

    **测试：**

    带占位符的国际化信息

        welcomeTip=欢迎，{0},您已经登陆成功！

    《1》.如果需要在JSP页面中填充国际化消息里的占位符，则可以通过在

    <pre class="prettyprint">`<span class="hljs-comment">&lt;!--使用s:text标签输出welcomeTip对应的国际化信息--&gt;</span>  
            <span class="hljs-tag">&lt;<span class="hljs-title">s:text</span> <span class="hljs-attribute">name</span>=<span class="hljs-value">"welcomeTip"</span>&gt;</span>  
                    <span class="hljs-comment">&lt;!--使用s:param为国际化信息的占位符传入参数--&gt;</span>  
                <span class="hljs-tag">&lt;<span class="hljs-title">s:param</span>&gt;</span><span class="hljs-tag">&lt;<span class="hljs-title">s:property</span> <span class="hljs-attribute">value</span>=<span class="hljs-value">"username"</span>/&gt;</span><span class="hljs-tag">&lt;/<span class="hljs-title">s:param</span>&gt;</span>  
             <span class="hljs-tag">&lt;/<span class="hljs-title">s:text</span>&gt;</span>`</pre>

    《2》.如果需要在Action中填充国际化消息里的占位符，则可以通过在调用getText方法时使用getText（String aTextName,List args）或getText(String key, String[] args)方法来填充

    占位符。该方法的第二个参数既可以是一个字符串数组，也可以是字符串组成的List对象，从而完成对占位符，字符串数组、字符串集合中第二个元素将填充第二个占位符，依此类推。

    <pre class="prettyprint">` <span class="hljs-keyword">public</span> String <span class="hljs-title">execute</span>(){  
                <span class="hljs-keyword">if</span>(getUsername().equals(<span class="hljs-string">"ascent"</span>)&amp;&amp; getPassword().equals(<span class="hljs-string">"ascent"</span>)){  
                    <span class="hljs-comment">//调用getText方法取出国际化信息，使用字符串数组传入占位符的参数值（request范围）  </span>
                    ActionContext.getContext().put(<span class="hljs-string">"user"</span>,<span class="hljs-keyword">this</span>.getText(<span class="hljs-string">"welcomeTip"</span>,<span class="hljs-keyword">new</span> String[]{<span class="hljs-keyword">this</span>.getUsername()}));  
                    <span class="hljs-keyword">return</span> SUCCESS;  
                }  
                <span class="hljs-keyword">return</span> ERROR;  
            }  `</pre>

    ## **附：中英文切换 测试项目代码**

    Action

    <pre class="prettyprint">`    package com.lxitedu.ant;  
     <span class="hljs-number">1.</span> import com.opensymphony.xwork2.ActionSupport;  
     <span class="hljs-number">2.</span> import com.opensymphony.xwork2.ModelDriven;  
     <span class="hljs-number">3.</span>   
     <span class="hljs-number">4.</span> <span class="hljs-keyword">public</span> <span class="hljs-class"><span class="hljs-keyword">class</span> <span class="hljs-title">Action</span> <span class="hljs-keyword">extends</span> <span class="hljs-title">ActionSupport</span> <span class="hljs-keyword">implements</span> <span class="hljs-title">ModelDriven</span>&lt;<span class="hljs-title">User</span>&gt; {</span>  
     <span class="hljs-number">5.</span>   <span class="hljs-keyword">private</span> <span class="hljs-keyword">static</span> <span class="hljs-keyword">final</span> long serialVersionUID = <span class="hljs-number">1</span>L;  
     <span class="hljs-number">6.</span>   <span class="hljs-keyword">private</span> User user = <span class="hljs-keyword">new</span> User();  
     <span class="hljs-number">7.</span>   
     <span class="hljs-number">8.</span>   @Override  
     <span class="hljs-number">9.</span>   <span class="hljs-keyword">public</span> String execute() throws <span class="hljs-keyword">Exception</span> {  
     <span class="hljs-number">10.</span>     <span class="hljs-keyword">return</span> SUCCESS;  
     <span class="hljs-number">11.</span>   }  
     <span class="hljs-number">12.</span>   
     <span class="hljs-number">13.</span>   @Override  
     <span class="hljs-number">14.</span>   <span class="hljs-keyword">public</span> User getModel() {  
     <span class="hljs-number">15.</span>     <span class="hljs-keyword">return</span> user;  
     <span class="hljs-number">16.</span>   }  
     <span class="hljs-number">17.</span>     
     <span class="hljs-number">18.</span>   <span class="hljs-keyword">public</span> String run() throws <span class="hljs-keyword">Exception</span> {  
     <span class="hljs-number">19.</span>     System.out.println(<span class="hljs-string">"Action.run()"</span>);  
     <span class="hljs-number">20.</span>     <span class="hljs-keyword">return</span> INPUT;  
     <span class="hljs-number">21.</span>   }  
     <span class="hljs-number">22.</span> }  `</pre>

    user.java

    <pre class="prettyprint">`package com.lxitedu.ant;  
     <span class="hljs-number">1.</span>   
     <span class="hljs-number">2.</span> <span class="hljs-keyword">public</span> <span class="hljs-keyword">class</span> User {  
     <span class="hljs-number">3.</span>    <span class="hljs-keyword">private</span> String name;  
     <span class="hljs-number">4.</span>    <span class="hljs-keyword">private</span> String password;  
     <span class="hljs-number">5.</span>   <span class="hljs-keyword">public</span> String <span class="hljs-title">getName</span>() {  
     <span class="hljs-number">6.</span>     <span class="hljs-keyword">return</span> name;  
     <span class="hljs-number">7.</span>   }  
     <span class="hljs-number">8.</span>   <span class="hljs-keyword">public</span> <span class="hljs-keyword">void</span> <span class="hljs-title">setName</span>(String name) {  
     <span class="hljs-number">9.</span>     <span class="hljs-keyword">this</span>.name = name;  
     <span class="hljs-number">10.</span>   }  
     <span class="hljs-number">11.</span>   <span class="hljs-keyword">public</span> String <span class="hljs-title">getPassword</span>() {  
     <span class="hljs-number">12.</span>     <span class="hljs-keyword">return</span> password;  
     <span class="hljs-number">13.</span>   }  
     <span class="hljs-number">14.</span>   <span class="hljs-keyword">public</span> <span class="hljs-keyword">void</span> <span class="hljs-title">setPassword</span>(String password) {  
     <span class="hljs-number">15.</span>     <span class="hljs-keyword">this</span>.password = password;  
     <span class="hljs-number">16.</span>   }  
     <span class="hljs-number">17.</span>      
     <span class="hljs-number">18.</span> }  `</pre>

    资源文件

    <pre class="prettyprint">`messageResource<span class="hljs-emphasis">_en_</span>US.properties  
    <span class="hljs-bullet">2\.    
    </span><span class="hljs-bullet">3\.  </span>login=login  
    <span class="hljs-bullet">4\.  </span>password=password  
    <span class="hljs-bullet">5\.  </span>sub=submit  
    <span class="hljs-bullet">6\.  </span>cn=Chinese  
    <span class="hljs-bullet">7\.  </span>us= English  
    <span class="hljs-bullet">8\.     
    </span><span class="hljs-bullet">9\.  </span>messageResource<span class="hljs-emphasis">_zh_</span>CN.properties  
    <span class="hljs-bullet">10\.   
    </span><span class="hljs-bullet">11\. </span>login=帐号  
    <span class="hljs-bullet">12\. </span>password=密码  
    <span class="hljs-bullet">13\. </span>sub=提交  
    <span class="hljs-bullet">14\. </span>cn=中文  
    <span class="hljs-bullet">15\. </span>us=英文
    <span class="hljs-bullet">16\.   </span>`</pre>

    struts.xml  

    <pre class="prettyprint">`<span class="hljs-doctype">&lt;!DOCTYPE struts PUBLIC  
    2\.      "-//Apache Software Foundation//DTD Struts Configuration 2.0//EN"  
    3\.      "http://struts.apache.org/dtds/struts-2.0.dtd"&gt;</span>  
    4\.  <span class="hljs-tag">&lt;<span class="hljs-title">struts</span>&gt;</span>  
    5\.      <span class="hljs-tag">&lt;<span class="hljs-title">package</span> <span class="hljs-attribute">name</span>=<span class="hljs-value">"hello"</span> <span class="hljs-attribute">namespace</span>=<span class="hljs-value">"/abc"</span> <span class="hljs-attribute">extends</span>=<span class="hljs-value">"struts-default"</span>&gt;</span>  
    6\.    
    7\.            
    8\.          <span class="hljs-tag">&lt;<span class="hljs-title">action</span> <span class="hljs-attribute">name</span>=<span class="hljs-value">"user"</span> <span class="hljs-attribute">class</span>=<span class="hljs-value">"com.lxitedu.ant.Action"</span>&gt;</span>  
    9\.              <span class="hljs-tag">&lt;<span class="hljs-title">result</span> <span class="hljs-attribute">name</span>=<span class="hljs-value">"success"</span>&gt;</span>/success.jsp<span class="hljs-tag">&lt;/<span class="hljs-title">result</span>&gt;</span>  
    10\.             <span class="hljs-tag">&lt;<span class="hljs-title">result</span> <span class="hljs-attribute">name</span>=<span class="hljs-value">"input"</span>&gt;</span>/index.jsp<span class="hljs-tag">&lt;/<span class="hljs-title">result</span>&gt;</span>  
    11\.         <span class="hljs-tag">&lt;/<span class="hljs-title">action</span>&gt;</span>  
    12\.           
    13\.           
    14\.         <span class="hljs-tag">&lt;<span class="hljs-title">action</span> <span class="hljs-attribute">name</span>=<span class="hljs-value">"input"</span> <span class="hljs-attribute">class</span>=<span class="hljs-value">"com.lxitedu.ant.Action"</span> <span class="hljs-attribute">method</span>=<span class="hljs-value">"run"</span>&gt;</span>  
    15\.             <span class="hljs-tag">&lt;<span class="hljs-title">result</span> <span class="hljs-attribute">name</span>=<span class="hljs-value">"input"</span>&gt;</span>/index.jsp<span class="hljs-tag">&lt;/<span class="hljs-title">result</span>&gt;</span>  
    16\.             <span class="hljs-tag">&lt;<span class="hljs-title">interceptor-ref</span> <span class="hljs-attribute">name</span>=<span class="hljs-value">"i18n"</span> /&gt;</span>  
    17\.         <span class="hljs-tag">&lt;/<span class="hljs-title">action</span>&gt;</span>       
    18\.           
    19\.     <span class="hljs-tag">&lt;/<span class="hljs-title">package</span>&gt;</span>  
    20\.   
    21\. <span class="hljs-tag">&lt;/<span class="hljs-title">struts</span>&gt;</span>`</pre>

    index.jsp  

    <pre class="prettyprint">`<span class="vbscript">&lt;%@ page language=<span class="hljs-string">"java"</span> contentType=<span class="hljs-string">"text/html; charset=UTF-8"</span>  
    <span class="hljs-number">2.</span>      pageEncoding=<span class="hljs-string">"UTF-8"</span>%&gt;</span>  
    3\.  <span class="vbscript">&lt;%@ taglib prefix=<span class="hljs-string">"s"</span> uri=<span class="hljs-string">"/struts-tags"</span> %&gt;</span>  
    4\.  <span class="hljs-doctype">&lt;!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd"&gt;</span>  
    5\.  <span class="hljs-tag">&lt;<span class="hljs-title">html</span>&gt;</span>  
    6\.  <span class="hljs-tag">&lt;<span class="hljs-title">head</span>&gt;</span>  
    7\.  <span class="hljs-tag">&lt;<span class="hljs-title">title</span>&gt;</span>Insert title here<span class="hljs-tag">&lt;/<span class="hljs-title">title</span>&gt;</span>  
    8\.  <span class="hljs-tag">&lt;/<span class="hljs-title">head</span>&gt;</span>  
    9\.  <span class="hljs-tag">&lt;<span class="hljs-title">body</span>&gt;</span>  
    10\.       <span class="hljs-tag">&lt;<span class="hljs-title">a</span> <span class="hljs-attribute">href</span>=<span class="hljs-value">"abc/input.action?request_locale=zh_CN"</span>&gt;</span><span class="hljs-tag">&lt;<span class="hljs-title">s:label</span> <span class="hljs-attribute">key</span>=<span class="hljs-value">"cn"</span>/&gt;</span><span class="hljs-tag">&lt;/<span class="hljs-title">a</span>&gt;</span><span class="hljs-tag">&lt;<span class="hljs-title">br</span>/&gt;</span>    
    11\.       <span class="hljs-tag">&lt;<span class="hljs-title">a</span> <span class="hljs-attribute">href</span>=<span class="hljs-value">"abc/input.action?request_locale=en_US"</span>&gt;</span><span class="hljs-tag">&lt;<span class="hljs-title">s:label</span> <span class="hljs-attribute">key</span>=<span class="hljs-value">"us"</span>/&gt;</span><span class="hljs-tag">&lt;/<span class="hljs-title">a</span>&gt;</span>   
    12\.         
    13\.           
    14\.       <span class="hljs-tag">&lt;<span class="hljs-title">s:form</span> <span class="hljs-attribute">action</span>=<span class="hljs-value">"abc/user.action"</span>&gt;</span>        
    15\.       <span class="hljs-tag">&lt;<span class="hljs-title">s:textfield</span> <span class="hljs-attribute">name</span>=<span class="hljs-value">"name"</span> <span class="hljs-attribute">key</span>=<span class="hljs-value">"login"</span> /&gt;</span><span class="hljs-tag">&lt;<span class="hljs-title">br</span>/&gt;</span>  
    16\.       <span class="hljs-tag">&lt;<span class="hljs-title">s:textfield</span> <span class="hljs-attribute">name</span>=<span class="hljs-value">"password"</span> <span class="hljs-attribute">key</span>=<span class="hljs-value">"password"</span> /&gt;</span><span class="hljs-tag">&lt;<span class="hljs-title">br</span>/&gt;</span>  
    17\.       <span class="hljs-tag">&lt;<span class="hljs-title">s:submit</span> <span class="hljs-attribute">key</span>=<span class="hljs-value">"sub"</span>/&gt;</span>   
    18\.       <span class="hljs-tag">&lt;/<span class="hljs-title">s:form</span>&gt;</span>  
    19\. <span class="hljs-tag">&lt;/<span class="hljs-title">body</span>&gt;</span>  
    20\. <span class="hljs-tag">&lt;/<span class="hljs-title">html</span>&gt;</span>  `</pre>

    success.jsp  

    <pre class="prettyprint">`<span class="vbscript">&lt;%@ page language=<span class="hljs-string">"java"</span> contentType=<span class="hljs-string">"text/html; charset=UTF-8"</span>  
    <span class="hljs-number">2.</span>      pageEncoding=<span class="hljs-string">"UTF-8"</span>%&gt;</span>  
    3\.  <span class="vbscript">&lt;%@ taglib prefix=<span class="hljs-string">"s"</span> uri=<span class="hljs-string">"/struts-tags"</span> %&gt;</span>  
    4\.  <span class="hljs-doctype">&lt;!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd"&gt;</span>  
    5\.  <span class="hljs-tag">&lt;<span class="hljs-title">html</span>&gt;</span>  
    6\.  <span class="hljs-tag">&lt;<span class="hljs-title">head</span>&gt;</span>  
    7\.  <span class="hljs-tag">&lt;<span class="hljs-title">title</span>&gt;</span>Insert title here<span class="hljs-tag">&lt;/<span class="hljs-title">title</span>&gt;</span>  
    8\.  <span class="hljs-tag">&lt;/<span class="hljs-title">head</span>&gt;</span>  
    9\.  <span class="hljs-tag">&lt;<span class="hljs-title">body</span>&gt;</span>  
    10\.       
    11\.     user Name: <span class="hljs-tag">&lt;<span class="hljs-title">s:property</span> <span class="hljs-attribute">value</span>=<span class="hljs-value">"name"</span> /&gt;</span><span class="hljs-tag">&lt;<span class="hljs-title">br</span>/&gt;</span>  
    12\.     password: <span class="hljs-tag">&lt;<span class="hljs-title">s:property</span> <span class="hljs-attribute">value</span>=<span class="hljs-value">"password"</span>/&gt;</span>  
    13\.       
    14\. <span class="hljs-tag">&lt;/<span class="hljs-title">body</span>&gt;</span>  
    15\. <span class="hljs-tag">&lt;/<span class="hljs-title">html</span>&gt;</span>  `</pre>

    **_以上参照 [http://blog.csdn.net/sd0902/article/details/8393182](http://blog.csdn.net/sd0902/article/details/8393182)。_**

    * * *

    **三、    jQuery实现国际化**

    **jQuery.i18n.properties** 是一款轻量级的 jQuery 国际化插件。与 Java 里的资源文件类似，jQuery.i18n.properties 采用 .properties 文件对 JavaScript 进行国际化。

    **jQuery.i18n.properties API**

    jQuery.i18n.properties 的 API 非常简单，只有少数几个 API，即 jQuery.i18n.properties()、jQuery.i18n.prop()、jQuery.i18n.browserLang()。当然，和其他 jQuery 插件一样，我们也可以采用 <span class="MathJax_Preview"></span><span style="" aria-readonly="true" role="textbox" id="MathJax-Element-1-Frame" class="MathJax"><nobr><span style="width: 10.617em; display: inline-block;" id="MathJax-Span-1" class="math"><span style="display: inline-block; position: relative; width: 8.618em; height: 0px; font-size: 123%;"><span style="position: absolute; clip: rect(1.368em, 1000em, 2.743em, -0.41em); top: -2.331em; left: 0em;"><span id="MathJax-Span-2" class="mrow"><span style="font-family: MathJax_Main;" id="MathJax-Span-3" class="mo">.</span><span style="font-family: MathJax_Math; font-style: italic; padding-left: 0.167em;" id="MathJax-Span-4" class="mi">i</span><span style="font-family: MathJax_Main;" id="MathJax-Span-5" class="mn">18</span><span style="font-family: MathJax_Math; font-style: italic;" id="MathJax-Span-6" class="mi">n</span><span style="font-family: MathJax_Main;" id="MathJax-Span-7" class="mo">.</span><span style="font-family: MathJax_Math; font-style: italic; padding-left: 0.167em;" id="MathJax-Span-8" class="mi">p</span><span style="font-family: MathJax_Math; font-style: italic;" id="MathJax-Span-9" class="mi">r</span><span style="font-family: MathJax_Math; font-style: italic;" id="MathJax-Span-10" class="mi">o</span><span style="font-family: MathJax_Math; font-style: italic;" id="MathJax-Span-11" class="mi">p</span><span style="font-family: MathJax_Math; font-style: italic;" id="MathJax-Span-12" class="mi">e</span><span style="font-family: MathJax_Math; font-style: italic;" id="MathJax-Span-13" class="mi">r</span><span style="font-family: MathJax_Math; font-style: italic;" id="MathJax-Span-14" class="mi">t</span><span style="font-family: MathJax_Math; font-style: italic;" id="MathJax-Span-15" class="mi">i</span><span style="font-family: MathJax_Math; font-style: italic;" id="MathJax-Span-16" class="mi">e</span><span style="font-family: MathJax_Math; font-style: italic;" id="MathJax-Span-17" class="mi">s</span><span style="font-family: MathJax_Main;" id="MathJax-Span-18" class="mo">(</span><span style="font-family: MathJax_Main;" id="MathJax-Span-19" class="mo">)</span><span id="MathJax-Span-20" class="texatom"><span id="MathJax-Span-21" class="mrow"><span id="MathJax-Span-22" class="mo"><span style="font-family: STIXGeneral,&quot;Arial Unicode MS&quot;,serif; font-size: 81%; font-style: normal; font-weight: normal;">、</span></span></span></span></span><span style="display: inline-block; width: 0px; height: 2.331em;"></span></span></span><span style="border-left: 0em solid; display: inline-block; overflow: hidden; width: 0px; height: 1.425em; vertical-align: -0.374em;"></span></span></nobr></span><script id="MathJax-Element-1" type="math/tex">.i18n.properties()、</script>.i18n.prop() 和 $.i18n.browserLang() 的形式使用这用这些 API。

    **1\.    jQuery.i18n.properties(settings)**

    该方法加载资源文件，其中 settings 是配置加载选项的一系列键值对，各配置项的具体描述请查阅下面贴出的网址。

    示例：

    <pre class="prettyprint">`jQuery.i18n.properties({
        name:<span class="hljs-string">'strings'</span>,<span class="hljs-comment">// 资源文件名称</span>
        path:<span class="hljs-string">'bundle/'</span>,<span class="hljs-comment">// 资源文件所在目录路径</span>
        mode:<span class="hljs-string">'both'</span>,<span class="hljs-comment">// 模式：变量或 Map </span>
        language:<span class="hljs-string">'pt_PT'</span>,<span class="hljs-comment">// 对应的语言</span>
        cache:<span class="hljs-literal">false</span>,
        encoding: <span class="hljs-string">'UTF-8'</span>,
        callback: <span class="hljs-function"><span class="hljs-keyword">function</span><span class="hljs-params">()</span> {</span><span class="hljs-comment">// 回调方法</span>
        }
     });

**2\. jQuery.i18n.prop(key)**

该方法以 map 的方式使用资源文件中的值，其中 key 指的是资源文件中的 key。当 key 指定的值含有占位符时，可以使用 jQuery.i18n.prop(key,var1,var2 … ) 的形式，其中 var1,var2 …对各占位符依次进行替换。例如资源文件中有“msg_hello= 您好 {0}，今天是 {1}。”的键值对，则我们可以采用“jQuery.i18n.prop( ‘ msg_hello ’ , ’小明’ , ’星期一’ );”的形式使用 msg_hello。

**3\.    jQuery.i18n.browserLang()**  

用于获取浏览浏览器的语言信息，这里不再单独介绍。

详细使用示例请访问：[http://www.ibm.com/developerworks/cn/web/1305_hezj_jqueryi18n/](http://www.ibm.com/developerworks/cn/web/1305_hezj_jqueryi18n/)。

            <div>
                作者：z893196569 发表于2015/9/8 13:12:18 [原文链接](http://blog.csdn.net/z893196569/article/details/48289701)
            </div>
            <div>
            阅读：65 评论：0 [查看评论](http://blog.csdn.net/z893196569/article/details/48289701#comments)
            </div>
