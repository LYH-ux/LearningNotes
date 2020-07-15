---
typora-copy-images-to: figure
typora-root-url: figure
---

# 《Qt自查手册》

## 1.编译相关

##### 1.程序发布 release

- .lib    /   .dll

##### 2.设置应用程序图标

1. create .ico  file, example:  rename  "myico.ico"
2. create .txt  file  , type   IDI_ICON1  ICON   DISCARDABLE     "myico.ico"
3. then save file as   myico.rc
4. append  RC_FILE+= myico.rc   in .pro file

##### 3.文本编码转换

- <QTextCodec>  
- 通过QString进行编码转换，   或是 QObject::tr();

##### 4.qmake

##### 5.前置声明

```
namespace Ui{
	class MyWidget;
}

class{
private:
	Ui::MyWidget  *ui;
}
```

因为只使用了该类对象指针，不需要使用完整定义，可用前置声明。

##### 6.信号与槽

- 类首要加  Q_OBJECT  宏

##### 7.显式构造函数

```
explicit MyWidget(QWidget *parent=0);

.cpp
Mywidget::MyWidget(QWidget *parent):QWidget(parent),ui(new Ui::MyWidget)
{

}
```

explicit关键字的作用就是防止类构造函数的隐式自动转换.

 explicit关键字只对有一个参数的类构造函数有效, 如果类构造函数参数大于或等于两个时, 是不会产生隐式转换的, 所以explicit关键字也就无效了

不希望发生   MyWidget   widget =  otherwidget; 这类的转换，则声明为 explicit

##### 8.help--interacting with the Debugger



## 2.对象模型

- 对象结构树

![image-20200713100133997](image-20200713100133997.png)

- QWidget

  QWidget(QWidget *parent = Q_NULLPTR,Qt::WindowFlags  f=Qt::WindowFlags() )

  Qt::Windowflags 为枚举类型

- QLabel  *label = new QLabel( 0, Qt::SplashScreen| Qt::WindowStaysOnTopHint );

  Qt::Dialog    Qt::FramelessWindowHint  

- setWindowState()       

  - Qt::WindowMaximized
  - Qt::WindowMinimized
  - Qt::WindowFullscreen
  - Qt::WindowNoState  ,  default

- window and Dialog widgets

  ![image-20200713101053451](image-20200713101053451.png)

 For all child widgets, the frame geometry is **equal** to the widget's client geometry.

Including the window frame: x(), y(), frameGeometry(), pos(), and move().
Excluding the window frame: geometry(), width(), height(), rect(), and size().

- <QDebug>

  - qDebug("x:d%",x);
  - qDebug() << "geometry:"<<geometry<<endl;

- QDialog

  - QDialog dialog(this);   若放在窗体构造函数中，该变量只在构造函数中有效。 构造函数结束，对话框会自动释放。 对话框一闪而过。 

  - QDialog *dialog = new QDialog(this);    new 出的对象不会自动释放，指定了父窗口，挂到了对象树上，不用自己delete

  - 模态对话框：没有关闭它之前，阻塞，不能再与其它交互

    类似 ：  QDialog dialog(this);

    ​              dialog.exec();   开启了事件循环阻塞了  

    使用：QDialog *dialog = new QDialog(this);

    ​           dialog->setModal(true);

    ​           diallog->show();

  - 非模态对话框

  - setWindowModality()

    - Qt::WindowModal       阻塞父子窗口
    - Qt::NonModal               
    - Qt::ApplicationModal   阻塞整个应用程序的所有窗口

- 信号与槽

  - 自动关联，适用于Qt部件已经定义的信号。是将关联函数整合到槽的命名中

    on_objectName_clicked()      on + objectname + signal 组成

    对于不是在UI中往界面上添加的部件，要在调用setupUi()前定义该部件，并且要使用setObjectName()函数来指定部件的对象名。 这样才可以使用自动关联。

  - 手动关联。  适用于自己写的信号。