## Ios离线包打包过程:

1.编辑projectApp/ios/projectApp/AppDelegate.m文件,取消jsCodeLocation=[[NSBundle mainBundle...这一行的注释;

2.在Xcode中,project的info中,修改Bundle name 为要发布的app名称;

3.在xcode中打开Image.xcassets/AppIcon,将不同icon图片拖进去作为icon图标;

4.在Xcode中,project的Supported ubterface orientations 中选择或删除手机支持的横屏和竖屏模式;

5.在Xcode中,选择Product/Scheme/Edit Scheme 选择编译模式,debug和release,选择release;

6.点击run,打包到手机上,生成release版本的app;
