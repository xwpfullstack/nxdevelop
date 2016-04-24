##  Sublime简介

Sublime Text是一个代码编辑器。也是HTML和散文先进的文本编辑器。漂亮的用户界面和非凡的功能，例如：多选择，Python插件，代码段等等。完全可自定义键绑定，菜单和工具栏等等.漂亮的用户界面和非凡的功能，Sublime Text的主要功能包括：拼写检查，书签，完整的 Python API ， Goto 功能，即时项目切换，多选择，多窗口等等。

    sublime 下载网址: http://www.sublimetext.com/3

## 1.安装package管理工具

用反引号，`ctrl+``调出命令输入窗口

```python

import urllib.request,os;pf = 'Package Control.sublime-package';ipp = sublime.installed_packages_path();urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) );open(os.path.join(ipp, pf), 'wb').write(urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ','%20')).read())

```

设置vim模式，Sublime Text 内置 Vim 模式支持，你只需到用户设置文件将 "ignored_packages": ["vintage"] 中的 vintage 删除即可。


快速体验：

```python
#! /usr/bin/python
print "hello world itcast"
```
        快速运行　ctrl+b


## 2.调出installpackage界面

    ctrl + shift + p
    install package

## 3.常用工具包

    AdvancedNewFile
    Djaneiro
    Emmet
    Git
    Side Bar
    HTML/CSS/JS Prettify
    Python PEP8 Autoformat
    SublimeCodeIntel
    ColorPicker
    OmniMarkupPreviewer

## 4.常用包使用说明

### AdvancedNewFile
可以创建文件，也可以连目录和文件都创建
    win+alt+n
### Djaneiro
django一些语法快速补齐功能，参考如下
    https://packagecontrol.io/packages/Djaneiro
### Emmet
快速缩写html,tab补齐,

代码简写扩展神器

   ul#test>li*4
   Ctrl+e展开上述指令


    html:5    补齐html
    p.foo     补齐class
    p#foo     补齐id
    >         子元素符号，表示嵌套的元素
    +         同级标签符号
    ^         可以使该符号前的标签提升一行

更多参考：http://www.iteye.com/news/27580

### Git
集成git
    ctrl+shift+p
    输入git 

### Side Bar
折叠目录树
    ctrl+k   ctrl+b

### HTML/CSS/JS Prettify
格式化代码
    鼠标右键，从里面选

### Python PEP8 Autoformat
格式化python代码
    ctrl+shift+r

### SublimeCodeIntel
自动匹配补全代码
    ctrl+f3    调到变量定义的地方

### ColorPicker
屏幕拾色器
    ctrl+shift+c

    

### OmniMarkupPreviewer
更多插件，设置OmniMarkupPreviewer的package setting中的default。修改里面的extensions
    "extensions": ["extra", "codehilite", "toc", "strikeout", "smarty", "subscript", "superscript"]

安装语法高亮支持插件
    sudo pip install pygments

将标记语言渲染为 HTML 并在浏览器上实时预览，同时支持导出 HTML 源码文件。
    ctrl+alt+o    导出在浏览器上预览
    ctrl+alt+x    导出生成html文件
    ctrl+r          文档标签导航
    [TOC]           文件开头插入，生成页面时自动增加目录标题索引
    mdlink          插入链接
    mdimg           插入图片
    mdacr           插入参考式链接
    mdfn            插入脚注    

OmniMarkupPreviewer更多介绍：http://blog.leanote.com/post/54bfa17b8404f03097000000

设置mkdown插入超链接等快捷键snippet文件，存储到/home/xwp/.config/sublime-text-3/Packages/User下

### ConvertToUTF8
直接在菜单栏中可以转，专为中文设计

### Terminal
Sublime版的在当前文件夹内打开
    ctrl+shift+t

### Side​Bar​Enhancements
右键一下子多处很多选择

### 自带技巧

+ 修改同一个变量,光标放在变量后，两次    `ctrl+d` 
+ 多变量修改，按住ctrl，鼠标点击修改位置
+ 查找 `ctrl+f`
+ 插入注释 `ctrl+shift+/`
+ 注释当前行  `ctrl+/`
+ 分屏
    Alt+Shift+1（非小键盘）窗口分屏，恢复默认1屏
    Alt+Shift+2 左右分屏-2列
    Alt+Shift+3 左右分屏-3列
    Alt+Shift+4 左右分屏-4列
    Alt+Shift+5 等分4屏
    Alt+Shift+8 垂直分屏-2屏
    Alt+Shift+9 垂直分屏-3屏
+ 标签切换 `alt+数字`
+ `Ctrl+Shift+P` 打开命令面板
+ 关闭当前标签文件`ctrl+f4`
+ f11全屏

## 5.脚本一键安装

```bash
cd ~/home/xwp/.config/sublime-text-3/Packages

echo Install...
echo ==================================================

echo === Package Control ===
rm -rf "Package Control"
git clone https://github.com/JustQyx/Sublime-Text-Package-Control.git "Package Control"

echo === Block Cursor Everwhere ===
rm -rf "Block Cursor Everwhere"
git clone https://github.com/ingshtrom/BlockCursorEverywhere.git "Block Cursor Everwhere"
...
```

## 6.ubuntu14.04中文支持
0. 先安装搜狗输入法

    http://pinyin.sogou.com/linux/?r=pinyin

1.下载编译依赖包(如果下载不成功，更新下软件源，用sohu的源)

    sudo apt-get install build-essential libgtk2.0-dev

2.创建sublime-imfix.c文件，放入以下代码

```c
/*
 * sublime-imfix.c
 * Use LD_PRELOAD to interpose some function to fix sublime input method support for linux.
 * By Cjacker Huang <jianzhong.huang at i-soft.com.cn> *
 *
 * gcc -shared -o libsublime-imfix.so sublime_imfix.c  `pkg-config --libs --cflags gtk+-2.0` -fPIC
 * LD_PRELOAD=./libsublime-imfix.so sublime_text
 */
#include <gtk/gtk.h>
#include <gdk/gdkx.h>

typedef GdkSegment GdkRegionBox;

struct _GdkRegion
{
    long size;
    long numRects;
    GdkRegionBox *rects;
    GdkRegionBox extents;
};

GtkIMContext *local_context;

void
gdk_region_get_clipbox (const GdkRegion *region,
                        GdkRectangle    *rectangle)
{
    g_return_if_fail (region != NULL);
    g_return_if_fail (rectangle != NULL);

    rectangle->x = region->extents.x1;
    rectangle->y = region->extents.y1;
    rectangle->width = region->extents.x2 - region->extents.x1;
    rectangle->height = region->extents.y2 - region->extents.y1;
    GdkRectangle rect;
    rect.x = rectangle->x;
    rect.y = rectangle->y;
    rect.width = 0;
    rect.height = rectangle->height;

    //The caret width is 2;
    //Maybe sometimes we will make a mistake, but for most of the time, it should be the caret.
    if (rectangle->width == 2 && GTK_IS_IM_CONTEXT(local_context)) {
        gtk_im_context_set_cursor_location(local_context, rectangle);
    }
}

//this is needed, for example, if you input something in file dialog and return back the edit area
//context will lost, so here we set it again.

static GdkFilterReturn event_filter (GdkXEvent *xevent, GdkEvent *event, gpointer im_context)
{
    XEvent *xev = (XEvent *)xevent;

    if (xev->type == KeyRelease && GTK_IS_IM_CONTEXT(im_context)) {
        GdkWindow *win = g_object_get_data(G_OBJECT(im_context), "window");

        if (GDK_IS_WINDOW(win)) {
            gtk_im_context_set_client_window(im_context, win);
        }
    }

    return GDK_FILTER_CONTINUE;
}

void gtk_im_context_set_client_window (GtkIMContext *context,
                                       GdkWindow    *window)
{
    GtkIMContextClass *klass;
    g_return_if_fail (GTK_IS_IM_CONTEXT (context));
    klass = GTK_IM_CONTEXT_GET_CLASS (context);

    if (klass->set_client_window) {
        klass->set_client_window (context, window);
    }

    if (!GDK_IS_WINDOW (window)) {
        return;
    }

    g_object_set_data(G_OBJECT(context), "window", window);
    int width = gdk_window_get_width(window);
    int height = gdk_window_get_height(window);

    if (width != 0 && height != 0) {
        gtk_im_context_focus_in(context);
        local_context = context;
    }

    gdk_window_add_filter (window, event_filter, context);
}
```

3.编译

    gcc -shared -o libsublime-imfix.so sublime_imfix.c  \`pkg-config --libs --cflags gtk+-2.0\` -fPIC

4.设置共享库加载

    sudo cp libsublime-imfix.so  /usr/lib/

修改/usr/share/applications/sublime_text.desktop文件
    
```
sudo vim /usr/share/applications/sublime_text.desktop
```

打开后将 `Exec=/opt/sublime_text/sublime_text %F` 修改为

```
Exec=bash -c 'LD_PRELOAD=/usr/lib/libsublime-imfix.so /opt/sublime_text/sublime_text' %F
```

将 `Exec=/opt/sublime_text/sublime_text -n` 修改为
```
Exec=bash -c 'LD_PRELOAD=/usr/lib/libsublime-imfix.so /opt/sublime_text/sublime_text' -n
```
这样就通过快捷方式打开SublimeText 3就可以支持中文输入了。
参考链接:http://blog.csdn.net/cywosp/article/details/32350899

## 开发环境

虚拟机vmware运行ubuntu14.04，设置虚拟机网卡为nat模式

编辑->虚拟网络编辑器 -> 查看VMnet8的设置 -> 查看设置，记录网关和ip范围

![vmnet8设置](https://raw.githubusercontent.com/xwpfullstack/nxdevelop/master/media/vmnat.png)

在ubuntu14.04里编辑

    sudo vi /etc/network/interface

     # interfaces(5) file used by ifup(8) and ifdown(8)
     auto lo
     iface lo inet loopback
     
     
     iface eth0 inet static
     address 192.168.169.180
     netmask 255.255.255.0
     gateway 192.168.169.2 #这个地址你要确认下 网关是不是这个地址
     
     dns-nameservers 192.168.169.2
     auto eth0
                      
重启虚拟机

windows下使用sublime,安装sftp插件，下载同步服务器上内容

ctrl+shift+p  ->  install  -> 回车 -> sftp  ->回车




windows下使用xshell远程连接

+ author:xwp
+ Email:xwp_fullstack@163.com
+ qq:1722379944
