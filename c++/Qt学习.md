# Qt学习

Qt创建一个窗口

```c++
#include <QApplication>
#include <Qwidget>
#include <QDebug>

int main(int argc, char *argv[])
{
    QApplication a(argc, argv);//GUI程序创建
    QDwidget w;//创建窗口对象实例
    w.setWindowTitle("我是标题");
    w.resize(300,200);
    w.move(30,60);
    w.setCursor(Qt::UpArrowCursor);//设置光标向上箭头
    w.show();

    qDebug()<<w.pos()<<w.x()<<w.y();
    qDebug()<<w.frameGeometry();
    qDebug()<<w.geometry();

    return a.exec();
}
```



QDialog类

模态：没有关闭窗口前，用户不能与该程序的其他窗口交互

非模态：用户既能和该窗口交互，也能和该程序的其他窗口交互

| 成员函数                  | 功能                                                         |
| ------------------------- | ------------------------------------------------------------ |
| int exec()                | 模态形式显示对话框，只有在对话框关闭后程序才能往下执行       |
| void setModal(bool modal) | 设置是否为模态，设置后程序往下执行                           |
| void setWindowModality()  | 设置对话框要阻塞的窗口类型：1.Qt::NonModal 2.Qt::WindowModal(只阻塞自己的父窗口，父窗口的父窗口及兄弟窗口) 3.Qt::ApplicationModal(阻塞本程序所有窗口) |



![image-20230908104001457](C:\Users\30992\AppData\Roaming\Typora\typora-user-images\image-20230908104001457.png)

Qt各种属性



设置模态

```c++
 QApplication a(argc,argv);

    QWidget w1,w2;
    w1.setWindowTitle("基本窗口1");
    w1.show();

    w2.setWindowTitle("基本窗口2");
    w2.move(100,100);
    w2.show();

    QDialog dlg(&w1);
    dlg.setWindowTitle("我是对话框");
    dlg.resize(200,100);
    dlg.setWindowModality(Qt::WindowModal);//设置模态
    dlg.show();

    return a.exec();
```



主窗口类：



```c++
#include<QApplication>
#include<QMainWindow>
#include<QMenuBar>

int main(int argc,char *argv[])
{
    QApplication a(argc,argv);

    QMainWindow w;
    QMenuBar menubar(&w);
    QMenu menu1(&menubar),menu2(&menubar),subMenu(&menubar); //创建对象时传入menubar把菜单栏对象作为父类

    //设置菜单内容
    subMenu.setTitle("打开");
    subMenu.addAction("打开项目"); //增加了动作
    subMenu.addAction("打开文件"); //增加了动作
    menu1.setTitle("文件");
    menu1.addMenu("&subMenu"); //传入subMenu进去，
    menu1.addAction("关闭");
    menu2.setTitle("编辑");

    //添加菜单和菜单栏
    menubar.addMenu(&menu1);
    menubar.addMenu(&menu2);
    menubar.addMenu(&subMenu);

    w.show();
    return a.exec();


}

```



部件类：

| 类型                  | 功能                                                         |
| --------------------- | ------------------------------------------------------------ |
| QLabel(标签类)        | 显示文字或对象，不提供交互                                   |
| QPushButton(按钮类)   | 按钮设置文本描述按下的操作                                   |
| QLineEdit(单行文本框) | 允许输入和编辑单行纯文本(不带格式)，提供很多有用的编辑功能，撤销重做，剪切粘贴，拖放 |
| QTextEdit(多行文本框) | 更换HTML,                                                    |
| QFont(字体类)         | 指定文本的字体信息，样式大小，粗体，斜体，下划线             |
| QColor(颜色类)        | 颜色信息，RGB控制颜色，支持透明度                            |
| QPalette(调色板)      | 管理窗口所有部件的所有颜色信息，每个窗口部件都有一个QPalette对象，窗口或部件显示时会按QPalette对象对颜色状态控制 |
| QString(字符串类)     | Unicode字符串，不同于C字符串，（双引号括起来的每个字符8bit，），此字符串每个占16bit |
|                       |                                                              |



信号和槽

```c++
QMetaObject::Connection connect(const QObject *, const char *,const QObject *, const char *,Qt::ConnectionType);

QMetaObject::Connection connect(const QObject *, const QMetaMethod &,const QObject *, const QMetaMethod &,Qt::ConnectionType);

QMetaObject::Connection connect(const QObject *, const char *,const char *,Qt::ConnectionType) const;

QMetaObject::Connection connect(const QObject *, PointerToMemberFunction, const QObject *, PointerToMemberFunction,Qt::ConnectionType)

QMetaObject::Connection connect(const QObject *, PointerToMemberFunction,Functor);
```



```c++
connect(sender,signal,receiver, slot);
//sender是发出信号的对象
//signal是发送对象发出的信号
//receiver是接收信号的对象
//slot是接收对象在接收到信号后需调用的函数
```

![image-20230919200243241](C:\Users\30992\AppData\Roaming\Typora\typora-user-images\image-20230919200243241.png)
