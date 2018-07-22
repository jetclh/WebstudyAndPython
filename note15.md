#GUI
- Tkinter
    - 绑定的是TK GUI工具集，用python包装的tcl代码
- PyGTK
    - Tkinter的替代品
- wxPython
    - 跨平台的Python GUI
- PyQt
    - 跨平台的
    - 商业授权有问题
    
##Tkinter常用组件
- 按钮
    - Button  按钮组件
    - RadioButton  单选框组件
    - CheckButton   选择按钮组件
    - ListBox   列表框组件
- 文本输入组件
    - Entry   单行文本框组件
    - Text    多行文本框组件
- 标签组件
    - Lable    标签组件，可以显示图片和文字
    - Message  标签组件，可以根据内容将文字换行
- 菜单
    - Menu    菜单组件
    - MenuButton    菜单按钮组件，可以使用Menu代替
- 滚动条
    - scale         滑块组件
    - Scrollbar     滚动条组件
- 其他组件
    - Canvas    画布组件
    - Frame     框架组件，将多个组件编组
    - Toplevel    创建子窗口容器组件
    
    
## 组件的大致使用步骤
- 1. 创建总面板
- 2. 创建面板上的各种组件
    - 指定组件的父组件，即依附关系
    - 利用相应的属性对组件进行设置
    - 给组件安排布局
- 3. 同步骤2一样，创建很多组件
- 4. 最后，启动总面板的消息循环


## 组件布局
- 控制组件的摆放方式
- 三种布局
    - pack：按照方位布局
    - place：按照坐标布局
    - grid：网格布局
    
- pack布局：
    - 最简单，代码量最少，挨个摆放，默认从上到下，系统自动设置
    - side：停靠方位，可选值为LEFT，TOP，RIGHT，BOTTOM
    - fill：填充方式，可选值为X,Y,BOTH,NONE
    - expand：YES/NO
    - anchor：N,E,S,W,CENTER
    - ipadx：x方向的内边距
    - ipady：y方向的内边距
    - padx：x方向的外边距
    - pady：y方向的外边距
    
- grid布局
    - 利用row，column编号，都是从0开始
    - sticky：N,E,S,W表示上下左右，用来决定组件从哪个方向开始
    - 支持ipad，padx等参数，跟pack函数含义一样
    - 支持rowspan，columnspan，表示跨行，跨列数量
    
- place布局
    - 明确方位的摆放
    - 相对位置布局，随意改变窗口大小会导致混乱
    - 使用place函数，分为绝对布局和相对布局，绝对布局使用x，y参数


# 消息机制
- 消息的传递机制
    - 自动发出事件/消息
    - 消息有系统负责发送到队列
    - 由相关组件进行绑定/设置
    - 后端自动选择感兴趣的事件并作出反应
- 消息格式：
    - <[modifier-]-type-[-detail]>
    - <Button-1>：button表示一个按钮事件，1表示的是鼠标左键，2表示的是鼠标中键
    - <KeyPress-A>：键盘A键位
    - <Control-Shift-KeyPress-A>：同时按下Control，Shift，A三个键位
    - <F1>：键位F1
    
# Tkinter的绑定
- bind_all：全局范围的绑定，默认的是全局快捷点，比如F1是帮助文档
- bind_class：接收三个参数，第一个是类名，第二个是事件，第三个是操作
    - w.bind_class("Entry", "<Control-V>", my_paste)
- bind：单独对某一个实例绑定
- unbind：解绑，需要一个参数，即你要解绑的事件



# Entry
- 输入框，功能单一
- entry["show"] = "*"，设置遮挡字符


# 菜单
- 1. 普通菜单
    - 第一个Menu类定义的是parent
    - add_command添加菜单项，如果菜单是顶层菜单，则从左向右添加，否则就是下拉菜单
        - lable：指定菜单项名称
        - command：点击后相应的调用函数
        - acceletor：快捷键
        - underline：指定是否菜单信息下有横线
        - menu：属性指定使用哪个为顶级菜单
        
        
# 级联菜单
- add_cascade：级联菜单，作用是引出后面的菜单
- add_cascade的menu属性：指明把菜单级联到哪个菜单上
- label：名称
- 过程：
    - 建立menu实例
    - add_command
    - add_cascade

# 弹出式菜单
- 弹出菜单也叫上下文菜单
- 实现的大致思路
    - 1. 建立菜单并向菜单添加各种功能
    - 2. 监听鼠标右键
    - 3. 如果鼠标右键点击，则根据位置判断弹出
    - 4. 调用Menu的pop方法
- add_separator：添加分隔符
    
    
# canvas画布
- 画布：可以自由地在上面绘制图形的控件
- 在画布上绘制对象，通常用create_xxx，xxx=对象类型，例如line，rectangle
- 画布的作用是把一定组件画到画布上显示出来
- 每次调用create_xxx都会返回一个创建的组件的ID，同时也可以用tag属性指定其标签
- 每次调用canvas.move实现一个一次性动作