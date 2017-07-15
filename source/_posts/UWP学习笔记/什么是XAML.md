---
title: UWP学习笔记 (三)   XAML界面原理和语法
date: 2017-07-10 22:00:00
tags: [UWP,APP开发,学习笔记] 
---
** {{ title }}：** <Excerpt in index | 首页摘要>
学习XAML在UWP 中的原理及语法
<!-- more -->
<The rest of contents | 余下全文>
## 什么是XAML
>XAML是EXtensible Application Markup Language的英文缩写，相应的中文名称为可扩展应用程序标记语言，它是微软公司为构建应用程序用户界面而创建的一种新的描述性语言。XAML提供了一种便于扩展和定位的语法来定义和程序逻辑分离的用户界面，而这种实现方式和ASP.NET中的"代码后置"模型非常类似。XAML是一种解析性的语言，尽管它也可以被编译。它的优点是简化编程式上的用户创建过程，应用时要添加代码和配置等。 --百度百科

### 优点
&#160;&#160;&#160;&#160;XAML简化了.Net Framework 3.0编程模式上的用户界面创建过程，使用XAML开发人员可以对WPF程序的所有用户界面元素(例如文本、按钮、图像和列表框等)进行详细的定置，同时还可以对整个界面进行合理化的布局，这与使用HTML非常相似。但是由于XAML是基于XML的，所以它本身就是一个组织良好的XML文档，而且相对于HTML，它的语法更严谨、更明确。预计以后大部分的XAML都可由相应的软件自动生成，就如同我们现在制作一个静态页面时，几乎不用编写任何HTML代码就可以直接通过Dreamweaver软件生成一个美观的页面。但是最初通过手动编写XAML代码将是一次绝佳的学习体验，虽然实现的过程繁杂了些，但是将加深您对XAML语法和各个元素的理解。
大多数的WPF程序可能同时包含程序代码和 XAML。我们可以使用XAML定义应用程序的初始界面，而后才编写相应的功能实现代码。我们可以将逻辑代码直接嵌入到一个XAML文件中，也可以将它保留在一个单独的文件中。实际上，能够用XAML实现的所有功能我们都可以使用程序代码来完成。因此，我们根本无需使用任何的XAML就可以创建一个完好的WPF程序。一般来说，程序代码的优势在于流程处理和逻辑判断，而不是界面的构建上。而XAML则是集中关注于界面的编程，我们可以将它和其它的.NET语言配合使用，从而构建出一个功能完善、界面美观的WPF程序。XAML是一种纯正的、用来描述用户界面构成元件和编排方式的标记语言。尽管有部分的XAML语法具备程序设计语言的特性(例如XAML中的Trigger和TRansform)，但是XAML并不是一种用于程序设计的语言，它的功能也不是为了执行应用程序逻辑。
&#160;&#160;&#160;&#160;微软推荐XAML被编译成BAML(Binary Application Markup Language-二进制语言程序标记语言)。XAML和BAML都可以被WPF解析，并且将以一种和HTML相似的方式进行界面的呈现。但是和HTML不同的是，XAML是强类型化的。也就是说，HTML会忽略那些它不能识别的元素和属性，而XAML必须在识别所有的元素和属性的情况下，才对页面进行呈现。尽管在XAML中各个属性都是以一个个的字符串(例如Background)表示的，但是这些字符串实际上代表的是WPF中的对象，只有被WPF识别的对象才可以作为元素的属性，所以我们说XAML是强类型化的。
### 新功能
微软Build 2013发布了一些已经被添加到Windows 8.1中的XAML新功能。[1]  
* Hub控件
* 命令栏
* 弹出（Flyout）控件
* 日期/时间选择控件
* 取消StandardStyles.xaml
### 与HTML的区别
&#160;&#160;&#160;&#160;还有一点是我们反复强调的，XAML并不是HTML。尽管XAML在元素的声明、程序样式的设置和指定事件处理程序上都和HTML非常类似，但是XAML是基于XML的，它是WPF的外在表现形式。而HTML只是一种标记语言，仅仅是用来为浏览器呈现页面内容。XAML除了用来呈现信息和请求用户输入等基本的功能外，它还包含了一些高级的特性，例如它提供了对动画和3D众多方面的支持。
XAML是可扩展的，正如它的名字指明的那样。开发人员可以创建自定义的控件、元素和函数来扩展XAML。而且由于XAML各元素在本质上就是WPF类的映射，所以开发人员可以很轻松地使用面向对象的技术对XAML元素进行扩展。也就是说我们可以开发一些自定义控件和组合元素，并将它公开给用户界面设计人员和其它的开发人员使用。

## XAML代码在UWP中的角色
* Page是UWP的用户界面主体。传统桌面程序是由一个个窗口组成的，而UWP是由一个Page（页面）组成的
*  Page是一个partial类
*  我们的任务是扩展Page这个类
	* 微软预制的Page为一个空的界面，没有内容
	* 我们只能扩展它
*  XAML代码是界面部分，用来实例化.NET对象的标记语言。它可以非常简单的创建对象。
如下图，这段XAML代码创建了一个Button 对象
![XAML代码](http://oskhhyaq3.bkt.clouddn.com/blog/170711/L1H43BAcC0.jpg?imageslim)
同样的用C#实现会怎么样呢？
![C#代码](http://oskhhyaq3.bkt.clouddn.com/blog/170711/Cabge4dJHj.jpg?imageslim)
&#160;&#160;&#160;&#160;&#160;XAML中的Margin是直接等于一个字符串，而C#中是需要给Margin赋值一个Thickness对象的。这归功于XAML的类型转换器。XAML在编译的时候，XAML语法分析器将字符串转换为对应的对象或枚举值，这样的话，我们可以直接用一个非常简单的值来代替冗长的类型名和枚举值来提高效率。
## XAML语法
### Content Property （内容属性）
每个标签都有自己的默认的内容属性。比如`<Grid/>`的默认属性是`<Grid.Children><Grid.Children/>`,`<Button>`的默认属性是`<Button.Content>`.通常内容属性可省略。
### self-closing 
XAML标签与其他标签类似有两种开闭形式
*  `<xxx><xxx/>`
* `<xxx/>`
### Attribute 与简单的property
可以直接在标签内定义该控件的一些简单属性，比如
```xml
<Button Name="button" Height="200" Width="200"/>
```
### 复杂的property与property标签
标签里的属性对象很复杂的时候，编译器无法将字符转化成对象是，就需要使用属性标签。
比如说，当我要设置背景颜色时，如果时简单的颜色可以直接这样
```xml
<Grid Background="red">
</Grid>
```
当然，我们肯定不能满足这种单一色调的背景，我想要一个渐变的漂亮的背景怎么做呢？
```xml
<Grid>
        <Grid.Background>
	        <!--LinearGradientBrush为线性笔刷-->
            <LinearGradientBrush EndPoint="0.5,1" StartPoint="0.5,0">
				<!--从#FFAC6CC开始 偏移量为0，#FF2D7099 结束偏移量为1-->            
                <GradientStop Color="#FFACD6CC" Offset="0"/>
                <GradientStop Color="#FF2D7099" Offset="1"/>
            </LinearGradientBrush>
        </Grid.Background>
 </Grid>

```

### 特殊属性（UWP，WPF特有）
* Dependency Property 依赖属性
依赖属性就是自己自己没有值，通过Binding从数据源获得值，就是依赖在别人身上，拥有依赖属性的对象称为依赖对象。
几种应用依赖属性的场景： 
 1. 希望可在样式中设置属性。 
2. 希望属性支持数据绑定。 
3. 希望可使用动态资源引用设置属性。 
4. 希望从元素树中的父元素自动继承属性值。 
5. 希望属性可进行动画处理。 
6. 希望属性系统在属性系统、环境或用户执行的操作或者读取并使用样式更改了属性以前的值时报告。 
7. 希望使用已建立的、WPF 进程也使用的元数据约定，例如报告更改属性值时是否要求布局系统重新编写元素的可视化对象。 
依赖对象创建时并不包含存储数据空间。WPF中必须使用依赖对象作为依赖属性的宿主。
 ```xml
 
 <TextBox x:Name="textBox1" Margin="10"  Text="{Binding Path=Title}"/>
 ```
* Attached Property 附加属性 。附加属性为本不应该是该控件的属性而在该控件下设置的属性。
比如
```xml
<Grid>
	<!--声明该Grid有三行-->
	<Grid.RowDefinitions>
            <RowDefinition Height="auto"/>
            <RowDefinition Height="auto"/>
            <RowDefinition Height="auto"/>
       </Grid.RowDefinitions>
    <!--这里的Grid.row本来是Grid的属性，却被当做是Button的属性。Grid.Row为Button的附加属性-->  
	<Button Grid.Row="2"/>
</Grid>
```