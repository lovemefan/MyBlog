---
title: PowerShell篇 (一) 初识PowerShell
date: 2017-07-05 20:53:23
tags: PowerShell
---
# 初识PowerShell
`作者：lovemefan` `以下资料收集于IT之家和知乎`
## PowerShell的邂逅
&#160;&#160;&#160;&#160;在我搭建我的博客的时候，cmd命令肯定是少不了的。除了cmd我们还可以选择Git Bash和PowerShell。
Git Bash是Git自带的一个命令行工具，用来上传，克隆等一些GitHub的操作。我之前也只知道Power Shell也是命令行，用它部署过离线的[UWP](http://baike.baidu.com/link?url=J5GeaQ_aSSMscd2pdx3O7nv1xTjZ99hw4ppIODqWFTtGFqHuxw13ppv9HviTZ8IglPkdRudcQb4-expkEoxC_a)，但平常不太会用所以没太在意。我只知道是微软为了替代cmd而特意在Windows 10里添加的新功能 。但在我使用Windows 10 创意者 的时候，正如往常使用鼠标右键+Shift ，本来是**“从此处打开命令窗口”**，结果就是没找到。反而这样显示
![mark](http://oskhhyaq3.bkt.clouddn.com/blog/170705/IKDe87048g.jpg?imageslim)
后来发现这是微软故意而为之的
## 什么是PowerShell
>&#160;&#160;&#160;&#160;Windows PowerShell 是一种命令行外壳程序和脚本环境，使命令行用户和脚本编写者可以利用 .NET Framework的强大功能。
&#160;&#160;&#160;&#160;它引入了许多非常有用的新概念，从而进一步扩展了您在 Windows 命令提示符和 Windows Script Host 环境中获得的知识和创建的脚本。
&#160;&#160;&#160;&#160;Windows PowerShell v3将伴随着MicrosoftHyper-V3.0和Windows Server 2012发布。PowerShell v3是一个Windows任务自动化的框架，它由一个命令行shell和内置在这个.NET框架上的编程语言组成。
&#160;&#160;&#160;&#160;PowerShell v3采用新的cmdlet让管理员能够更深入到系统进程中，这些进程可以制作成可执行的文件或脚本（script）。一条cmdlet是一条轻量命令，Windows PowerShell运行时间在自动化脚本的环境里调用它。Cmdlet包括显示当前目录的Get-Location，访问文件内容的Get-Content和结束运行进程的Stop-Process。
&#160;&#160;&#160;&#160;PowerShell v3在Windows Server 8中装载了Windows Management Framework 3.0。PowerShell运行时间也能嵌入到其它应用。——百度百科

[微软PowerShell官网](https://msdn.microsoft.com/en-us/powershell)

&#160;&#160;&#160;&#160;从Windows10创意者更新开始，PowerShell正式上位替换了命令提示符CMD。不论是Windows+X右键超级菜单，还是Shift+文件夹空白处右键，又或在文件资源管理器文件菜单中，都没有命令提示符CMD的身影了，全部都由PowerShell取而代之了。长期使用CMD的Windows系统管理员或Windows命令行极客恐怕一时不能适应，使用CMD都只能去开始菜单-所有应用-Windows系统-命令提示符打开使用，或者Windows+R键然后输入cmd，或者在小娜输入框输入cmd，再或者在PowerShell中输入cmd(看来又绕回来了)。藏得这么深，显然是不想让人用了啊。不仅如此，Power Shell还登陆了Linux和MacOS  
[在Linux下安装PowerShell](https://zhuanlan.zhihu.com/p/26346821?utm_source=qq&utm_medium=social)
PoweShell上位图如下
![mark](http://oskhhyaq3.bkt.clouddn.com/blog/170705/bfiiJCEHd4.jpg?imageslim)
&#160;&#160;&#160;&#160;问题来了，PowerShell这货凭什么力压CMD，强行上位？如果你之前试用过PowerShell，相信它一定没有给你什么好印象。打开慢！反应慢！命令还陌生！还动不动就弹一大堆谁都看不懂错误，PowerShell究竟凭什么在Windows10创意者更新中替代命令提示符CMD呢？微软脑抽了？
微软没有脑抽，PowerShell是凭借其强大的功能替换CMD的。这里要先说明以下PowerShell究竟是什么东西，或者它究竟是不是东西？
&#160;&#160;&#160;&#160;Windows PowerShell不是东西，它是专为系统管理员设计的新Windows命令行shell，它包括交互式提示和脚本环境。PowerShell定义很多命令与操作系统，特别是与文件系统交互，能够启动应用程序，甚至操纵应用程序；PowerShell允许将几个命令组合起来放到文件里执行，实现文件级的重用，也就是说有脚本的性质；PowerShell能够充分利用.Net类型和COM对象，来简单地与各种系统交互，完成各种复杂的、自动化的操作。
&#160;&#160;&#160;&#160;用人话说就是CMD能做的PowerShell都能做，CMD不能做的Powershell也能做。就是这么自信！不信？赶紧打开PowerShell把下面的命令复制进去，看看它干了什么事，然后你用CMD做出来吧！
```powershell
# create new excel instance
$objExcel = New-Object -comobject Excel.Application
$objExcel.Visible = $True
$objWorkbook = $objExcel.Workbooks.Add()
$objWorksheet = $objWorkbook.Worksheets.Item(1)
# write information to the excel file
$i = 0
$first10 = (ps | sort ws -Descending | select -first 10)
$first10 | foreach -Process {$i++; $objWorksheet.Cells.Item($i,1) = $_.name; $objWorksheet.Cells.Item($i,2) = $_.ws}
$otherMem = (ps | measure ws -s).Sum - ($first10 | measure ws -s).Sum
$objWorksheet.Cells.Item(11,1) = "Others"; $objWorksheet.Cells.Item(11,2) = $otherMem
# draw the pie chart
$objCharts = $objWorksheet.ChartObjects()
$objChart = $objCharts.Add(0, 0, 500, 300)
$objChart.Chart.SetSourceData($objWorksheet.range("A1:B11"), 2)
$objChart.Chart.ChartType = 70
$objChart.Chart.ApplyDataLabels(5)
```
![mark](http://oskhhyaq3.bkt.clouddn.com/blog/170705/CJi70f9ahF.png?imageslim)
没错，有点慢，等下吧，接下来它自动打开了excel，如图，我果然还是IT之家老粉丝啊
![mark](http://oskhhyaq3.bkt.clouddn.com/blog/170705/B8IDAdFlm4.png?imageslim)
&#160;&#160;&#160;&#160;上面一段代码是PowerShell界常见的一段神代码，很多初学者被其带入了PowerShell的大门。有效代码不过20来行，作用是把当前系统中最占内存的10个进程的数据发送到Excel中，并绘制成三维饼图。CMD是很难做到了，被替代也理所应当了。
&#160;&#160;&#160;&#160;PowerShell的定位是操作系统和应用程序的管理工具，从这个角度看，它是CMD的升级版，并非简单的对CMD进行扩展，事实上微软也不打算扩展和升级CMD了，以后PowerShell将全方位的替代CMD，目前CMD和PowerShell还是并存状态。
下面正式介绍PowerShell。
### （一）简单的命令
&#160;&#160;&#160;&#160;在CMD中，命令是从非常简单（如attrib.exe）到非常复杂（如netsh.exe）的可执行程序，新入门用户一旦遇到复杂命令，只能束手无策，只能求助搜索引擎，解决当前需求之后，就把命令的用法抛诸脑后，下次使用又要重新学习，极其不便。
![mark](http://oskhhyaq3.bkt.clouddn.com/blog/170705/526ijlFjLJ.png?imageslim)
&#160;&#160;&#160;&#160;PowerShell命令设计非常规范，它的命令由“动词”和“名词”两部分组成，比如“get”表示检索数据，“process”表示系统进程，把“get”和“process”组合起来的PowerShell命令就是“get-process”，意思是获取系统进程列表，这种命令在PowerShell中称为“cmdlet（读作“command-let”）”。
![mark](http://oskhhyaq3.bkt.clouddn.com/blog/170705/CIBlH2i1f7.png?imageslim)
&#160;&#160;&#160;&#160;使用“动词-名词”结构还有一个好处，就是不同的“动词”和“名词”可以自由组合，很少的几个“动词”和“名词”就可以组合出大量的可用命令，使命令记忆量大为降低，只需记住简单的几个词语，就可以使用大量的命令，这是包括命令提示符CMD在内的Shell不具备的，并且不会产生歧义，对新用户非常友好。
### （二）别名系统
&#160;&#160;&#160;&#160;“动词-名词”结构的cmdlet固然对新手友好，但也带来了另一个问题，命令名称过长，在命令行交互使用时不方便，在命令行窗口输入命令可以使用Tab键进行补全，可是经常使用还是需要键入大量的内容，要是能够把命令缩短一些就好了。PowerShell在设计时已经考虑到了，为此创建了别名系统，之所以叫名别系统，是因为PowerShell中的别名非常强大，能够非常方便的对别名进行增加、删除、修改，还为之创建了别名驱动器，可以像访问文件系统驱动器一样方便的访问别名驱动器。
PowerShell非常贴心的为用户创建了大量内置别名，一方面减少了常用命令的输入长度，另一方面也为熟悉其它Shell而不熟悉PowerShell的用户提供了方便，常见Shell如bash、cmd，PowerShell都为用户提供了他们熟悉的别名。下面是可以在Powershell中使用的通用的Cmd.exe和UNIX命令的简短列表。
**在PowerShell下输入**
```powershell
get-alias
```
以下只显示了部分，要想查询所有别名请用`alias`命令查询
![mark](http://oskhhyaq3.bkt.clouddn.com/blog/170705/6AghbjEgAg.png?imageslim)
&#160;&#160;&#160;&#160;PowerShell除了自带别名外，用户自己也可以创建别名，不仅仅可以为cmdlet创建别名，也可以为PowerShell函数、带参数的命令和包含完整路径的命令行程序创建别名。
比如为记事本创建别名，可以使用如下命令
```powershell
New-Alias np c:\windows\notepad.exe
```
&#160;&#160;&#160;&#160;创建别名完成后，在命令行中输入np就能直接打开记事本。在命令行中创建的别名只能在当前命令行窗口中使用，如果想以后也能使用此别名，可以把以上命令保存在PowerShell配置文件中，以后无论是在命令行中，还是使用脚本，都可以在本机使用np别名了。
![mark](http://oskhhyaq3.bkt.clouddn.com/blog/170705/8h0kd2FD21.png?imageslim)
PowrShell配置文件位置可以使用$profile命令查询。

&#160;&#160;&#160;&#160;想查看当前命令行窗口可以使用的别名，可以进入别名驱动器查看，使用dir alias:就能查看所有能用的别名，也可以使用get-alias命令查看别名。
### (三) 管理任务
Windows PowerShell的基本目标是使用户能够以交互方式或通过脚本更好、更容易地对系统进行管理控制，为了达成这个目标，PowerShell提供了大量命令来执行各种管理任务，让用户轻松完成管理系统任务。
#### 1、管理进程
前面已经提过管理系统进程的命令，管理进程常用命令就是get-process命令和stop-process命令，get-process命令获取进程之后可以直接用管道发送给stop-process命令结束进程。比如，关闭之前打开的记事本，可以使用下面的命令很方便的关闭记事本。
```powershell
get-process -Name notepad | stop-process
```
#### 2、处理文件和文件夹
&#160;&#160;&#160;&#160;PowerShell使用Get-ChildItem获取文件夹中直接包含的所有项，它有系统内置别名dir和ls，使用CMD和BASH的用户均可以轻松上手。如果想查看C:中的文件夹和文件，直接使用dir c:，PowerShell立刻就会列出C:中的文件和文件夹。其它处理文件和文件夹的命令有Copy-Item、New-Item、Remove-Item等，具体用法可以使用get-help然后跟命令名称即可查询。
#### 3、处理系统服务
&#160;&#160;&#160;&#160;可以像管理进程一样管理系统服务，Get-Service命令获取服务列表，Stop-Service命令停止服务，Start-Service命令启动服务，Suspend-Service命令挂起服务，Restart-Service命令重启服务，Set-Service服务设置服务属性。如果想一次性启动已经停止的服务，可以使用以下命令：
```powershell
get-service | where-object {$_.Status -eq "Stopped"} -exclude
wisvc | start-service
```
&#160;&#160;&#160;&#160;这行命名会把除wisvc之外的命令都启动，这只是一个示例，不要在自己电脑使用，启动所有服务会消耗大量系统资源。
#### 4、处理注册表
&#160;&#160;&#160;&#160;PowerShell可以非常方便的处理注册表项目，与进程和服务不同的是，PowerShell并未提供专用的注册表命令，而是使用处理文件和文件夹的命令，这并不奇怪，PowerShell为用户提供了注册表驱动器，可以很好的处理注册表项目。由于注册表对系统非常重要，错误处理注册表也许会导致系统出问题，处理注册表，特别是删除注册表项目要非常小心，最好能在处理注册表项目之前先备份要处理的项目。没有管理员权限也能处理部分注册表项目，这与regedit注册表编辑器不同，注册表编辑器必须使用管理员权限打开，然后才能操作项目。
**下面的表格列出了访问注册表所需的所有命令**

![mark](http://oskhhyaq3.bkt.clouddn.com/blog/170705/LcIe6FFlJ4.png?imageslim)
PowerShell只提供了两个注册表驱动器HKCU:和HKLM:，其中HKLM:是HKEY_LOCAL_MACHINE的缩写，HKCU:是HKEY_CURRENT_USER的缩写，如果想要访问所有注册表驱动器，可以进入Microsoft.PowerShell.Core\Registry::。
#### 5、处理其它任务
PowerShell还可以处理证书、防火墙、appx应用、打印机等任务。大家可以使用get-command命令查找相关命令。
























