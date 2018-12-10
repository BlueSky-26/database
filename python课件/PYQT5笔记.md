# PYQT5笔记

# Eric6+PyQt5环境构建

安装：

1. 安装pyqt5、pyqt5-tools、QScintilla等三个前置库。
2. 下载：eric6-17.08.zip和eric6-i18n-zh_CN-17.08.zip这两个压缩文件，第一个是Eric本体，第二个是汉化包。

2. 解压eric6-17.08.zip和eric6-i18n-zh_CN-17.08.zip到同一文件夹下，在解eric6-i18n-zh_CN-17.08.zip时应该会对eric6-17.08文件夹的部分文件做覆盖操作，点全部替换即可。

3. 进入解压的目录文件夹，如果没改名字的话应该是eric6-17.08文件夹，执行python install.py，或双击install.py执行安装，最好使用管理员权限。

4. 安装完毕。

5. 安装完毕首次打开需要进行配置：

   配置窗口：设置->首选项。

   1.点击编辑器->自动完成->QScintilla。勾上显示单条和使用填充符号。

   2.点击编辑器->API。语言：选择python3。然后导入eric6.api，点击编译api，点击ok。

注意：linux+Anaconda 需要在虚拟环境下，并使用参数 -b 指定api安装目录在python安装目录中。

# PyQt5简介

PyQt5是一套来自Digia的Qt5应用框架和Python的粘合剂。支持Python2.x和Python3.x版本。本教程使用Pyhton 3。Qt库是最强大的GUI支持库的一种。PyQt5的官方主页是www.riverbankcomputing.co.uk/news。是Riverbank Computing开发了PyQt5。

PyQt5以一套Python模块的形式来实现功能。它包含了超过620个类，600个方法和函数。它是一个多平台的工具套件，它可以运行在所有的主流操作系统中，包含Unix，Windows和Mac OS。PyQt5采用双重许可模式。开发者可以在GPL和社区授权之间选择。

PyQt5的类被划分在几个模块中，下面列出了这些模块：

QtCore 模块包含了非GUI的功能设计。这个模块被用来实现时间，文件和目录，不同数据类型，流，URL，mime类型，线程和进程。

QtGui 模块包含的类用于窗口化的系统结构，事件处理，2D绘图，基本图形，字体和文本。

QtWidgets 模块包含的类提供了一套UI元素来创建经典桌面风格用户界面。

QtMultimedia 模块包含的类用于处理多媒体内容和链接摄像头和无线电功能的API。

QtBluetooth 模块包含的类用于扫描蓝牙设备，并且和他们建立连接互动。

QtNetwork 模块包含的类用于网络编程，这些类使TCP/IP和UDP客户端/服务端编程更加容易和轻便。

QtPositioning 模块包含的类用于多种可获得资源的位置限定，包含卫星定位，Wi-Fi，或一个文本文件。

Enginio 模块用于解决客户端访问Qt云服务托管。 

QtWebSockets 模块包含的类用于解决WebSocket通信协议。 

QtWebKit 包含的关于浏览器的类用于解决基于WebKit2的支持库。 

QtWebKitWidgets 模块包含的关于WebKit1的类基本解决浏览器使用基于QtWidgets应用问题。

QtXml 模块包含的类用于解析XML文件。这个模块提供SAX和DOM API解决方法。  

QtSvg 模块提供类用于显示SVG文件内容。Scalable Vector Graphics (SVG) 是一种语言，用XML来描述二维图形和图形应用程序。 

QtSql模块提供类驱动数据库工作。 

QtTest 模块包含了方法提供PyQt5应用的单元测试。

# PyQt5入门

## 第一个窗口

```python
import sys
from PyQt5.QtWidgets import QApplication, QWidget

if __name__ == ‘__main__’:
    # 所有的PyQt5应用必须创建一个应用（Application）对象。sys.argv参数是一个来自命令行的参数列表。Python脚本可以在shell中运行。这是我们用来控制我们应用启动的一种方法。
    app = QApplication(sys.argv)
    # Qwidget组件是PyQt5中所有用户界面类的基础类。我们给QWidget提供了默认的构造方法。默认构造方法没有父类。没有父类的widget组件将被作为窗口使用。
    w = QWidget()
    # resize()方法调整了widget组件的大小。它现在是250px宽，150px高。
    w.resize(250, 150)
    # move()方法移动widget组件到一个位置，这个位置是屏幕上x=300,y=300的坐标。
    w.move(300, 300)
    #设置窗口标题
    w.setWindowTitle(‘Simple’)
    #窗口显示
    w.show()
    
    #最后，应用进入主循环。在这个地方，事件处理开始执行。主循环用于接收来自窗口触发的事件，并且转发他们到widget应用上处理。如果我们调用exit()方法或主widget组件被销毁，主循环将退出。sys.exit()方法确保一个不留垃圾的退出。系统环境将会被通知应用是怎样被结束的。exec_()方法有一个下划线。因为exec是Python保留关键字。因此，用exec_()来代替。
    sys.exit(app.exec_())
```

## Qt程序参考格式

```python
import sys
from PyQt5.QtWidgets import QApplication, QWidget
from PyQt5.QtGui import QIcon 
class Example(QWidget): 
    def __init__(self):
		super().__init__()
		self.initUI()
	def initUI(self):
        #setGeometry()做了两件事：将窗口在屏幕上显示，并设置了它的尺寸。setGeometry()方法的前两个参数定位了窗口的x轴和y轴位置。第三个参数是定义窗口的宽度，第四个参数是定义窗口的高度。事实上，这是将resize()和move()方法融合在一个方法内。
		self.setGeometry(300, 300, 300, 220)
        self.setWindowTitle('Icon')
        #设置窗口icon
        self.setWindowIcon(QIcon('logo.jpg'))
        self.show()
if __name__ == '__main__':
    app = QApplication(sys.argv)
    ex = Example()
    sys.exit(app.exec_()) 

```

## QWidgets常用组件使用

### 提示文本

pyqt5的PyQt5.QtWidgets下的QToolTip下的setFont是一个用来设置提示文本的字体的方法。Font（字体）需要使用PyQt5.GUI下的Font类来获取。

可以使用任何可见的QWidget对象的setToolTip方法向该对象设置提示文本。

```python
# 这个静态方法设置了用于提示框的字体。我们使用10px大小的SansSerif字体。
QToolTip.setFont(QFont('SansSerif', 10)) 
# 为了创建提示框，我们调用了setTooltip()方法。我们可以在提示框中使用富文本格式。 
self.setToolTip('This is a <b>QWidget</b> widget')
```

### 关于窗口关闭

任何QWidget对象都有一个close方法用来实现关闭。

### 消息框

消息框可以由PyQt5.QtWidgets下的QMessageBox实现。示例代码如下：

```python
from PyQt5.QtWidgets import QWidget, QMessageBox, QApplication

#显示一个带两个按钮的message box：YES和No按钮。代码中第一个字符串的内容被显示在标题栏上。第二个字符串是对话框上显示的文本。第三个参数指定了显示在对话框上的按钮集合。最后一个参数是默认选中的按钮。这个按钮一开始就获得焦点。返回值被储存在reply变量中。
reply = QMessageBox.question(self, 'Message',"确认退出吗?", QMessageBox.Yes |QMessageBox.No, QMessageBox.No)
```

### 对话框

#### QInputDialog

示例有一个按钮和一个输入框，点击按钮显示对话框，输入的文本会显示在输入框里。

```python
text, ok = QInputDialog.getText(self, 'Input Dialog','Enter your name:')
```

这是显示一个输入框的代码。第一个参数是输入框的标题，第二个参数是输入框的占位符。对话框返回输入内容和一个布尔值，如果点击的是OK按钮，布尔值就返回True。

```python
if ok:
    self.le.setText(str(text))
```

#### QColorDialog

```python
col = QColorDialog.getColor()

if col.isValid():
    self.frm.setStyleSheet("QWidget { background-color: %s }"% col.name())#设置QFrame背景色
```

#### QFontDialog

创建了一个有一个按钮和一个标签的`QFontDialog`的对话框，我们可以使用这个功能修改字体样式。

```python
font, ok = QFontDialog.getFont()
```

弹出一个字体选择对话框。`getFont()`方法返回一个字体名称和状态信息。状态信息有OK和其他两种。

```python
if ok:
    self.label.setFont(font)
```

#### QFileDialog

这里设置了一个文本编辑框，文本编辑框是基于`QMainWindow`组件的。

```python
fname = QFileDialog.getOpenFileName(self, 'Open file', '/home')
```

弹出`QFileDialog`窗口。`getOpenFileName()`方法的第一个参数是说明文字，第二个参数是默认打开的文件夹路径。默认情况下显示所有类型的文件。

```python
if fname[0]:
    f = open(fname[0], 'r')

    with f:
        data = f.read()
        self.textEdit.setText(data)
```

### 单选框与复选框（未完）

QCheckBox



### 切换按钮（ToggleButton）

切换按钮就是`QPushButton`的一种特殊模式。 它只有两种状态：按下和未按下。我们再点击的时候切换两种状态，有很多场景会使用到这个功能。

创建一个`QPushButton`，然后调用它的`setCheckable()`的方法就把这个按钮编程了切换按钮。

```python
redb = QPushButton('Red', self)
redb.setCheckable(True)
redb.move(10, 10)
```

把点击信号和我们定义好的函数关联起来，这里需要把点击事件转换成布尔值。

```python
redb.clicked[bool].connect(self.setColor)
```

获取被点击的按钮

```python
source = self.sender()
```

### 滑动条控件（QSlider）

`QSlider`是个有一个小滑块的组件，这个小滑块能拖着前后滑动，这个经常用于修改一些具有范围的数值，比文本框或者点击增加减少的文本框（spin box）方便多了。

示例：

创建一个水平的`QSlider`。备注：可以创建垂直滑块

```python
sld = QSlider(Qt.Horizontal, self)
```

创建一个`QLabel`组件并给它设置一个静音图标。

```python
self.label = QLabel(self)
self.label.setPixmap(QPixmap('mute.png'))
```

把`valueChanged`信号跟`changeValue()`方法关联起来。

```python
sld.valueChanged[int].connect(self.changeValue)
```

根据音量值的大小更换标签位置的图片。

```
if value == 0:
    self.label.setPixmap(QPixmap('mute.png'))
...
```

### 进度条（QProgressBar ）

进度条是用来展示任务进度的（我也不想这样说话）。它的滚动能让用户了解到任务的进度。`QProgressBar`组件提供了水平和垂直两种进度条，进度条可以设置最大值和最小值，默认情况是0~99。

新建一个`QProgressBar`构造器。

```
self.pbar = QProgressBar(self)
```

用时间控制进度条。

```python
self.timer = QtCore.QBasicTimer()
```

调用`start()`方法加载一个时间事件。这个方法有两个参数：过期时间和事件接收者。

```python
self.timer.start(100, self)
```

每个`QObject`和又它继承而来的对象都有一个`timerEvent()`事件处理函数。为了触发事件，我们重载了这个方法。

```python
def timerEvent(self, e):
  
    if self.step >= 100:
    
        self.timer.stop()
        self.btn.setText('Finished')
        return
        
    self.step = self.step + 1
    self.pbar.setValue(self.step)
```

里面的`doAction()`方法是用来控制开始和停止的。

```python
def doAction(self):
  
    if self.timer.isActive():
        self.timer.stop()
        self.btn.setText('Start')
        
    else:
        self.timer.start(100, self)
        self.btn.setText('Stop')
```

### 日历控件（QCalendarWidget ）

`QCalendarWidget`提供了基于月份的日历插件，十分简易而且直观。

创建一个`QCalendarWidget`。

```
cal = QCalendarWidget(self)
```

选择一个日期时，`QDate`的点击信号就触发了，把这个信号和我们自己定义的`showDate()`方法关联起来。

```
cal.clicked[QDate].connect(self.showDate)
```

使用`selectedDate()`方法获取选中的日期，然后把日期对象转成字符串，在标签里面显示出来。

```
def showDate(self, date):     
    
    self.lbl.setText(date.toString())
```

### 像素图像（QPixmap）

`QPixmap`是处理图片的组件。

创建一个`QPixmap`对象，接收一个文件作为参数。

```
pixmap = QPixmap("redrock.png")
```

把`QPixmap`实例放到`QLabel`组件里。

```
lbl = QLabel(self)
lbl.setPixmap(pixmap)
```



### 单行文本框（QLineEdit）

`QLineEdit`组件提供了编辑文本的功能，自带了撤销、重做、剪切、粘贴、拖拽等功能。

创建一个`QLineEdit`对象。

```
qle = QLineEdit(self)
```

如果输入框的值有变化，就调用`onChanged()`方法。

```
qle.textChanged[str].connect(self.onChanged)
```

在`onChanged()`方法内部，我们把文本框里的值赋值给了标签组件，然后调用`adjustSize()`方法让标签自适应文本内容。

```
def onChanged(self, text):
    
    self.lbl.setText(text)
    self.lbl.adjustSize() 
```



### 窗口分割（QSplitter）（未完）

`QSplitter`组件能让用户通过拖拽分割线的方式改变子窗口大小的组件。



### 下拉框（QComboBox）

`QComboBox`组件能让用户在多个选择项中选择一个。

创建一个`QComboBox`组件和五个选项。

```python
combo = QComboBox(self)
combo.addItem("Ubuntu")
combo.addItem("Mandriva")
combo.addItem("Fedora")
combo.addItem("Arch")
combo.addItem("Gentoo")
```

在选中的条目上调用`onActivated()`方法。

```python
combo.activated[str].connect(self.onActivated) 
```

在方法内部，设置标签内容为选定的字符串，然后设置自适应文本大小。

```python
def onActivated(self, text):
  
    self.lbl.setText(text)
    self.lbl.adjustSize() 
```

### 组合框（未完）

## 主窗口相关实现

在PyQt5中，菜单与工具栏只出现在在主应用程序窗口（QMainWindow 类）。在主窗口的框架中包括了“状态栏、工具栏和菜单栏”。

```python
from PyQt5.QtWidgets import QMainWindow, QApplication, QAction
```

### 菜单栏实现

1、定义Action对象。

2、设置Action对象的快捷键【非必需】。

3、设置鼠标悬停时状态栏提示【非必须】。

4、使用Action对象的信号连接槽处理。

5、使用QMainWindow的menuBar方法获取菜单栏对象。

6、使用菜单栏对象的addMenu方法添加并获取菜单项。

7、使用菜单对象的addAction方法将设置好的Action对象附加到菜单上。

示例代码如下：

```python
exitAction = QAction(QIcon('exit.jpg'), '&退出', self)
exitAction.setShortcut('Ctrl+Q')
exitAction.setStatusTip('退出应用程序') 
'''这个抽象动作对象(exitAction)的触发信号(triggered)可以连接(connect)到槽(qApp.quit)，quit()方法将终止该应用程序。 我们下面的代码是用来关闭当前对象的。'''
exitAction.triggered.connect(self.close)

self.statusBar().showMessage('这里是状态栏...')
menubar = self.menuBar()
fileMenu = menubar.addMenu('&文件')
fileMenu.addAction(exitAction)
```

### 工具栏实现

工具栏的实现和菜单栏基本类似只是有menuBar变成了ToolBar

### 状态栏实现

Statusbar状态栏：statusbar是用于显示控件的状态信息。

```python

#如果要获得QMainWindow 控件的状态信息，就需要先调用QMainWindow 的 statusBar() 方法创建状态栏，然后用showMessage() 显示反馈到状态栏的信息。
self.statusBar().showMessage('这里是状态栏...')

```

## 布局

### 绝对定位

使用对象的move定位，使用resize定大小。或者使用self.setGeometry(x, y, w, h)确定位置。

### 盒子布局

盒子使用QHBoxLayout和QVBoxLayout进行布局，它们分别是水平和垂直对齐控件的基本布局类（注意依赖互相嵌套实现各种布局）。在这个布局中可以使用拉伸因子对剩余位置进行填充。

示例代码：

```python
import sys
from PyQt5.QtWidgets import (QApplication, QWidget,
        QPushButton, QVBoxLayout, QHBoxLayout)
class Example(QWidget):
    def __init__(self):
        super().__init__()
        self.initUI()
    def initUI(self):       
        okButton = QPushButton('确定') # 创建确定按钮
        cancelButton = QPushButton('取消') # 创建 取消按钮        
        '''
        创建一个水平box布局，增加拉伸因子(addStretch)，
        添加(addWidget)两个按钮。在添加两个按钮之前增加了一个拉伸因子，这会将两个按钮推到窗口右侧。
        '''
        hbox = QHBoxLayout()
        hbox.addStretch(1)
        hbox.addWidget(okButton)
        hbox.addWidget(cancelButton)
        '''
        要得到我们想要的布局，还需将横向布局放入垂直的布局中。在垂直框上的拉伸因子会将水平框包括里面的控件推至窗口的底部。
        '''
        vbox = QVBoxLayout()
        vbox.addStretch(1)
        vbox.addLayout(hbox)        
        #最后，我们设置窗口的主布局。
        self.setLayout(vbox)
        self.setGeometry(300, 300, 350, 150)
        self.setWindowTitle('Box布局')        
        self.show()
if __name__ == '__main__':
    app = QApplication(sys.argv)
    ex = Example()
    sys.exit(app.exec_())
```

### 栅格布局

最经常使用的布局类是网格布局。这种布局将该空间分成行和列。要创建一个网格布局，需要使用到QGridLayout 布局类。

实例代码如下：

```python
import sys
from PyQt5.QtWidgets import (QApplication, QWidget, QLabel, 
QTextEdit, QLineEdit, QGridLayout)
class Example(QWidget):
    def __init__(self):
        super().__init__()
        self.initUI()
    def initUI(self):
        title = QLabel('标题')
        author = QLabel('作者')
        review = QLabel('评论')
        titleEdit = QLineEdit()
        authorEdit = QLineEdit()
        reviewEdit = QTextEdit()
        #实例化网格布局和并设置设置间距
        grid  =QGridLayout()
        grid.setSpacing(10)
        grid.addWidget(title, 1, 0)
        grid.addWidget(titleEdit, 1,1)
        grid.addWidget(author, 2, 0)
        grid.addWidget(authorEdit, 2,1)
        grid.addWidget(review, 3, 0)
       '''添加一个控件到网格布局中，我们可以为这个控件使用行跨度
        或列跨度。在我们的例子中，我们要求reviewEdit控件跨度5行'''
        grid.addWidget(reviewEdit, 3,1,5,1)#后四个参数代表起始行，起始列，行占位置、列占位置
        self.setLayout(grid)
        self.setGeometry(300, 300, 350, 300)
        self.setWindowTitle('评论')        
        self.show()
if __name__ == '__main__':
    app = QApplication(sys.argv)
    ex = Example()
    sys.exit(app.exec_())
```

**注意事项：**继承QMainWindow类型时尽量不要使用layout去布局。原因如下图：

![](teached.img/1541078421525.png)

主窗口若要加载布局对象的正确方式如下：

1. 创建一个QWidget实例:wig=QWidget()

2. 将布局layout设置到Qwidget上:wig.setLayout(grid)

3. 设置主窗体的CentralWidget为我们刚才设置好的QWidget对象:self.setCentralWidget(wig)

## 事件与信号（未完）

事件驱动模型与信号槽机制

事件重写

信号定制

## 定时器（Qtime）

如果需要在程序中周期性地进行某项操作，比如检测某种设备的状态，就会用到定时器。PyQt5就提供了一个定时器QTimer来实现这种操作

```python
from PyQt5.QtCore import QTimer
```

首先需要引入QTimer模块

```python
self.timer = QTimer(self) #初始化一个定时器
self.timer.timeout.connect(self.operate) #计时结束调用operate()方法
self.timer.start(2000) #设置计时间隔并启动
```

然后实例化一个QTimer对象，将timeout信号连接到operate()信号槽，start(2000)表示设定时间间隔为2秒，并且启动
这里注意：connect中operate方法千万不要加括号，否则会出错

```python
def operate(self):
    #具体操作
```

## 拖拽特效的实现（未完）

### 实现接受拖入

激活组件的拖拽事件。

```
self.setAcceptDrops(True)
```

重构了`dragEnterEvent()`拖入执行事件方法。设定好接受拖拽的数据类型（plain text）。

```
def dragEnterEvent(self, e):
    
    if e.mimeData().hasFormat('text/plain'):
        e.accept()
    else:
        e.ignore() 
```

重构`dropEvent()`拖入事件方法，更改按钮接受鼠标的释放事件的默认行为。

```
def dropEvent(self, e):

    self.setText(e.mimeData().text()) 
```

`QLineEdit`默认支持拖拽操作，所以我们只要调用`setDragEnabled()`方法使用就行了。

```
edit = QLineEdit('', self)
edit.setDragEnabled(True)
```

### 实现拖拽支持

这个例子展示怎么拖放一个button组件。

```
#!/usr/bin/python3
# -*- coding: utf-8 -*-

"""
ZetCode PyQt5 tutorial

In this program, we can press on a button with a left mouse
click or drag and drop the button with  the right mouse click. 

Author: Jan Bodnar
Website: zetcode.com
Last edited: August 2017
"""

from PyQt5.QtWidgets import QPushButton, QWidget, QApplication
from PyQt5.QtCore import Qt, QMimeData
from PyQt5.QtGui import QDrag
import sys

class Button(QPushButton):
  
    def __init__(self, title, parent):
        super().__init__(title, parent)
        

    def mouseMoveEvent(self, e):

        if e.buttons() != Qt.RightButton:
            return

        mimeData = QMimeData()

        drag = QDrag(self)
        drag.setMimeData(mimeData)
        drag.setHotSpot(e.pos() - self.rect().topLeft())

        dropAction = drag.exec_(Qt.MoveAction)


    def mousePressEvent(self, e):
      
        super().mousePressEvent(e)
        
        if e.button() == Qt.LeftButton:
            print('press')


class Example(QWidget):
  
    def __init__(self):
        super().__init__()

        self.initUI()
        
        
    def initUI(self):

        self.setAcceptDrops(True)

        self.button = Button('Button', self)
        self.button.move(100, 65)

        self.setWindowTitle('Click or Move')
        self.setGeometry(300, 300, 280, 150)
        

    def dragEnterEvent(self, e):
      
        e.accept()
        

    def dropEvent(self, e):

        position = e.pos()
        self.button.move(position)

        e.setDropAction(Qt.MoveAction)
        e.accept()
        

if __name__ == '__main__':
  
    app = QApplication(sys.argv)
    ex = Example()
    ex.show()
    app.exec_()
```

上面的例子中，窗口上有一个`QPushButton`组件。左键点击按钮，控制台就会输出`press`。右键可以点击然后拖动按钮。

```
class Button(QPushButton):
  
    def __init__(self, title, parent):
        super().__init__(title, parent)
```

从`QPushButton`继承一个`Button`类，然后重构`QPushButton`的两个方法:`mouseMoveEvent()`和`mousePressEvent()`.`mouseMoveEvent()`是拖拽开始的事件。

```
if e.buttons() != Qt.RightButton:
    return
```

我们只劫持按钮的右键事件，左键的操作还是默认行为。

```
mimeData = QMimeData()

drag = QDrag(self)
drag.setMimeData(mimeData)
drag.setHotSpot(e.pos() - self.rect().topLeft())
```

创建一个`QDrag`对象，用来传输MIME-based数据。

```
dropAction = drag.exec_(Qt.MoveAction)
```

拖放事件开始时，用到的处理函数式`start()`.

```
def mousePressEvent(self, e):
    
    QPushButton.mousePressEvent(self, e)
    
    if e.button() == Qt.LeftButton:
        print('press')
```

左键点击按钮，会在控制台输出“press”。注意，我们在父级上也调用了`mousePressEvent()`方法，不然的话，我们是看不到按钮按下的效果的。

```
position = e.pos()
self.button.move(position)
```

在`dropEvent()`方法里，我们定义了按钮按下后和释放后的行为，获得鼠标移动的位置，然后把按钮放到这个地方。

```
e.setDropAction(Qt.MoveAction)
e.accept()
```

指定放下的动作类型为moveAction。



## 基本图形绘制（未完）

## 自定义控件示例

# PyQt参考（Pyside）

## 音乐播放参考

https://www.jianshu.com/p/917b2ea7f719

## 设置窗口尺寸的方法：

1.设置宽度和高度。
resize(int w,int h)
resize(QSize s)
2.设置窗口的位置、宽度和高度。
setGeometry(int X,int Y,int W,int H)
setGeometry(QRect r)
3.设置窗口为固定值。
setFixedSize(int w,int h)
setFixedSize(QSize s)
窗口标题栏上的最大化按钮无效；用鼠标无法调整窗口尺寸。
4.设置窗口为固定值。
setFixedWidth(int w)
窗口标题栏上的最大化按钮无效；用鼠标无法调整窗口的宽度。
5.设置窗口为固定值。
setFixedHeight(int h)
窗口标题栏上的最大化按钮无效；用鼠标无法调整窗口的高度。
5.设置窗口的最小尺寸。
setMinimumSize(int w,int h)
setMinimumSize(QSize s)
用鼠标可以让窗口变宽、变高。
设置窗口的最小宽度：
setMinimumWidth(int w)
设置窗口的最小高度：
setMinimumHeight(int h)
6.设置窗口的最大尺寸。
setMaximumSize(int w,int h)
setMaximumSize(QSize s)
用鼠标可以让窗口变宽、变高。
设置窗口的最小宽度：
setMaximumWidth(int w)
设置窗口的最小高度：
setMaximumHeight(int h)
其他的函数还有：
setBaseSize()、adjustSize()、width()、heigth()、minimumSize()、minimumWidth()、minimumHeigth()、maximumSize()、maximumWidth()、maximumHeight()、baseSize()、sizeHint()、minimumSizeHint()、rect()、geometry()。

## 事件示例：

```python
#!/usr/bin/env python3
import sys
from PyQt5.QtCore import (QEvent, QTimer, Qt)
from PyQt5.QtWidgets import (QApplication, QMenu, QWidget)
from PyQt5.QtGui import QPainter

class Widget(QWidget):

    def __init__(self, parent=None):
        super(Widget, self).__init__(parent)
        self.justDoubleClicked = False
        self.key = ""
        self.text = ""
        self.message = ""
        self.resize(400, 300)
        self.move(100, 100)
        self.setWindowTitle("Events")
        QTimer.singleShot(0, self.giveHelp) # Avoids first resize msg


    def giveHelp(self):
        self.text = "Click to toggle mouse tracking"
        self.update()


    def closeEvent(self, event):#关闭事件
        print("Closed")


    def contextMenuEvent(self, event):
        menu = QMenu(self)
        oneAction = menu.addAction("&One")
        twoAction = menu.addAction("&Two")
        oneAction.triggered.connect(self.one)
        twoAction.triggered.connect(self.two)
        if not self.message:
            menu.addSeparator()
            threeAction = menu.addAction("Thre&e")
            threeAction.triggered.connect(self.three)
        menu.exec_(event.globalPos())


    def one(self):
        self.message = "Menu option One"
        self.update()


    def two(self):
        self.message = "Menu option Two"
        self.update()


    def three(self):
        self.message = "Menu option Three"
        self.update()


    def paintEvent(self, event):#图形绘制事件
        text = self.text
        i = text.find("\n\n")
        if i >= 0:
            text = text[0:i]
        if self.key:
            text += "\n\nYou pressed: {0}".format(self.key)
        painter = QPainter(self)
        painter.setRenderHint(QPainter.TextAntialiasing)
        painter.drawText(self.rect(), Qt.AlignCenter, text)
        if self.message:
            painter.drawText(self.rect(), Qt.AlignBottom|Qt.AlignHCenter,
                             self.message)
            QTimer.singleShot(5000, self.clearMessage)
            QTimer.singleShot(5000, self.update)

    def clearMessage(self):
        self.message=""
        
    def resizeEvent(self, event):#尺寸变化事件
        self.text = "Resized to QSize({0}, {1})".format(
                            event.size().width(), event.size().height())
        self.update()

        
    def mouseReleaseEvent(self, event):#鼠标释放事件
        if self.justDoubleClicked:
            self.justDoubleClicked = False
        else:
            self.setMouseTracking(not self.hasMouseTracking())
            if self.hasMouseTracking():
                self.text = "Mouse tracking is on.\n"+\
                        "Try moving the mouse!\n"+\
                        "Single click to switch it off"
            else:
                self.text = "Mouse tracking is off.\n"+\
                                           "Single click to switch it on"
            self.update()


    def mouseMoveEvent(self, event):#鼠标移动事件
        if not self.justDoubleClicked:
            globalPos = self.mapToGlobal(event.pos())
            self.text = "The mouse is at\nQPoint({0}, {1}) "+\
                    "in widget coords, and\n"+\
                    "QPoint({2}, {3}) in screen coords".format(
                    event.pos().x(), event.pos().y(), globalPos.x(),
                    globalPos.y())
            self.update()


    def mouseDoubleClickEvent(self, event):#鼠标双击事件
        self.justDoubleClicked = True
        self.text = "Double-clicked."
        self.update()


    def keyPressEvent(self, event):#键盘按下事件
        self.key = ""
        if event.key() == Qt.Key_Home:
            self.key = "Home"
        elif event.key() == Qt.Key_End:
            self.key = "End"
        elif event.key() == Qt.Key_PageUp:
            if event.modifiers() & Qt.ControlModifier:
                self.key = "Ctrl+PageUp"
            else:
                self.key = "PageUp"
        elif event.key() == Qt.Key_PageDown:
            if event.modifiers() & Qt.ControlModifier:
                self.key = "Ctrl+PageDown"
            else:
                self.key = "PageDown"
        elif Qt.Key_A <= event.key() <= Qt.Key_Z:
            if event.modifiers() & Qt.ShiftModifier:
                self.key = "Shift+"
            self.key += event.text()
        if self.key:
            self.key = self.key
            self.update()
        else:
            QWidget.keyPressEvent(self, event)


    def event(self, event):
        if (event.type() == QEvent.KeyPress and
            event.key() == Qt.Key_Tab):
            self.key = "Tab captured in event()"
            self.update()
            return True
        return QWidget.event(self, event)

if __name__ == "__main__":
    app = QApplication(sys.argv)
    form = Widget()
    form.show()
    app.exec_()
```

