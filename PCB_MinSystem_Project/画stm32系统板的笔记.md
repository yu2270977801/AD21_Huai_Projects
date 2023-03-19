# 基于Stm32画的最小系统板

参考视频：[Altium Designer 1小时（貌似不够）速成（可能不止一小时*~* 但我觉得仨小时肯定够了---来自up猪的自信!!）_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV17E411x7dR/)



## 1. 原理图库绘制

● 注意引脚的小白点(指焊点)向外

● 利用向导 Tools→ Symbal Wizard...

注意改引脚属性→Passive

● 自己找资源:立创EDA

Design→ Make Schematic/PCB Library

## 2. PCB封装库绘制

● 最关键:焊盘的大小和距离

● 孔径比插针大0.1-0.2mm

● 焊盘比孔径大0.45-0.5mm

● 看芯片手册

● 快捷键G/ctrl+shift+G 改变焊盘距离

● 灰色覆铜，紫色阻焊层

● 改变原点在中心或一脚

Edit→ Set Refeience

● 更改元器件名称

● 原理图元件库文件 + PCB元件库文件添加到*.Libpkg，编译后就会出现*.IntLib 元件集成库文件



##  3. 原理图绘制

*翻转板子 VB,CTRL+F*

● 元器件放置

● X水平/Y竖直/空格 翻转

● 连线

● 快捷键 CTRL+W,空格把线变直

● Place→Deirectives→给引脚打上红叉

不进行DRC检查

● 网络编号

● 元器件编号

● Tools→Annotation

● 封装添加

● 可以借助"Find Similar Objects..."批量添加封装

● 取消阴影 shift+C

右键元器件"Find Similar Objects...",可以查找同类型元器件,会出现阴影.

● 封装管理器 T+G

用于检查封装的问题

● 编译

右键Project编译，检查error

● 导入到PCB

### 交互 | 原理图与PCB之间

● 原理图中选中模块，按shift+ctrl+x，PCB中才能选中我们需要的模块

## 4.PCB绘制

shift+s单独查看每层

### 4.1 布局

● 隐藏飞线 N

布线时再用

● 逐个模块布局

● 用Tools→Component Placement把元器件选出来

● 元器件放底层:要在移动中按L，按空格旋转

### 4.2 布线

#### 4.2.1 手动布线 

●  隐藏Top/Bottom Overlay

可视性管理面板快捷键L进行恢复

●  快捷键N,调出飞线，并隐藏GND飞线

●  普通布线10mil，电源线15mil

●  打开可见性管理面板ctrl+D

如隐藏文字，方便布线;还可调节布线时的亮度 Dimmed objects 

●  Design→Rules...改为6mil

→Electrical 电气属性 →Manufacturing

●  ctrl+W调出布线(十字架)

●  布线不能有锐角/直角

●  键调出过孔，连接顶层和底层

过孔一般12mil/24mil 

#### 4.2.2 自动布线

●  先去设置规则Design→Rules...

●  Electrical 电气属性

●  Clearance 间距

改6mil

●  Routing 布线

●  Widrh 线宽

Design→Rule Wizard 添加电源线改线宽15mil 

●  Routing Via Style 过孔

12mil/24mil

●  快捷键TE， 画泪滴

Tools→Teardrops...

●  Route→Auto Route→All...

●  过孔Tab→Find Similiar Objects→去掉阻焊层 Solder Mask Expansion 改0mil

●  按g改网格单位

●  短路:打过孔Tab→自动移除回路Automatically Remove Loops

### 5. 覆铜

● 快捷键 F3

● Tab

●  Net选GND

●  勾选 Remove Dead Copper 移除死铜(会全部报错)

●  Tools→ Polygon Pours→ Repout All 全部重覆

● 顶层/底层都要覆铜

● *键切换底层查看

● Design→ Rules...→ Electrical 电气属性→Clearance间距→Advanced → Poly 那一行改10mil

报错重覆 →0Repout All

● 放置小过孔:连接两层覆铜;加固

Design→ Rules...→Plane→Polygon Connect Style→最右Via Connection 改成直连，就不是十字架形了

● 丝印层

● 重新调出丝印

● 调出Tab

● 改文字高度，字体

● 三维模式下，直接拖文字改位置

### 6. 电气规则检查(规则设置)

可以与覆铜转换顺序

● Tools→ Design RuleCheck...→ Run

● 调出Messages→双击可以定位

● 一定要重新覆铜

● 再更新错误，改错...