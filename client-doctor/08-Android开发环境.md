ubuntu14.04安装react-native开发环境

## 安装java运行环境

	tar zxvf jdk-8u65-linux-x64.tar.gz

	sudo vi /etc/profile

		export JAVA_HOME=/home/xwp/soft/react-android/jdk1.8.0_65 
		export JRE_HOME=${JAVA_HOME}/jre   
		export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib   
		export PATH=${JAVA_HOME}/bin:$PATH 

## 安装node环境

移除系统中的node（如果你有）

	tar zxvf node-v5.3.0-linux-x64.tar.gz

	sudo vi /etc/profile

		export NODE_HOME=/home/xwp/soft/react-android/node-v5.3.0-linux-x64
		export PATH=$PATH:$NODE_HOME/bin
		export NODE_PATH=$NODE_HOME/lib/node_modules

## 安装android SDK

	tar zxvf adt-bundle-linux.tar.gz

	把解压后adt-bundle-linux,移到~用户目录下

	sudo vi /etc/profile

		export PATH=$PATH:/home/xwp/adt-bundle-linux/sdk/platform-tools:/home/xwp/adt-bundle-linux/sdk/tools
		#react-native run-android会找此变量ANDROID_HOME	
		export ANDROID_HOME=/home/xwp/adt-bundle-linux/sdk
		export PATH=$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/build-tools
		export USE_GLOBAL_ADK=/home/xwp/adt-bundle-linux/sdk

## 重启电脑

上述环境安装好后，需要重启电脑，使环境变量生效。

## 安装watchman监视器

	unzip watchman-master.zip
	cd watchman	

	sudo apt-get install python-dev	
	sudo apt-get install autoconf

	./autogen.sh
	./configure
	make
	sudo make install

备注：ubuntu下面默认情况下这三个值都很小，react-native start时过一会就自动挂掉了，因为一个react-native下的文件都2万多个了，但默认情况下inotify只能监控8192个文件，所以挂掉了，需要调大系统的默认值

    sudo vi /etc/sysctl.conf

在末尾添加下面三行配置，然后重启

    fs.inotify.max_user_watches=999999
    fs.inotify.max_user_instances=999999
    fs.inotify.max_user_events=1638400



## 安装react-native

	npm config set registry https://registry.npm.taobao.org
	npm config set disturl https://npm.taobao.org/dist
	npm install -g react-native-cli

## 安装virtualbox虚拟机(如果Ubuntu在虚拟机中,为了简易,可不安装此处的虚拟机和的镜像)

genymotion镜像（android）需要虚拟机

	sudo dpkg -i virtualbox-5.0_5.0.12-104815-Ubuntu-trusty_amd64.deb

	安装时报错,执行下面命令，下载所需的依赖软件
	sudo apt-get install -f

	重新执行安装命令
	sudo dpkg -i virtualbox-5.0_5.0.12-104815-Ubuntu-trusty_amd64.deb

## 安装镜像(如果Ubuntu在虚拟机中,为了简易,可不安装此处的虚拟机和的镜像)
赋予执行权限

	chmod 777 genymotion-2.6.0-linux_x64.bin
	./genymotion-2.6.0-linux_x64.bin
	在ubuntu 已安装软件里启动genymotion,并锁定到测边栏里
	到官网注册
	https://www.genymotion.com/

	启动genymotion,在settings里登录账号

	add添加一个新的虚拟机镜像，统一选择Nexus5X API23(1080x1920)

	安装镜像后，start启动镜像

	开发时，需开启wifi模式，否则调试时无法加载JS(切记)

## 创建react-native项目

	创建项目比较耗时间
	react-native init MyProject
	cd MyProject

	react-native start

	此时需要激活一个链接
	http://localhost:8081/index.android.bundle?platform=android

	新开一个终端
	#react-native run-android需要
	sudo apt-get install lib32stdc++6
	sudo apt-get install lib32z1

	第一次运行时，需要下载很多包，比较耗时
	react-native run-android

## 不在Ubuntu中安装模拟器时执行此步(非必须)
	执行完run-android会报错,不用管
	在Windows中安装天天模拟器
	将run-android生成的apk复制出来安装到天天模拟器中
	安装完成后设置IP和端口即可
	apk所在目录: 项目目录/android/app/build/outputs/apk/app-debug.apk
	
	
## Android真机调试



1.识别手机,lsusb查看设备编号,"ID 12d1:1077 Huawei"

     xingwenpeng@xingwenpeng-T420:~/workspace/reactnative/react-native-android-tablayout/example$ lsusb
     Bus 002 Device 014: ID 12d1:1077 Huawei Technologies Co., Ltd. 
     Bus 002 Device 002: ID 8087:0024 Intel Corp. Integrated Rate Matching Hub
     Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
     Bus 001 Device 005: ID 04f2:b221 Chicony Electronics Co., Ltd integrated camera
     Bus 001 Device 004: ID 0a5c:217f Broadcom Corp. BCM2045B (BDC-2.1)
     Bus 001 Device 003: ID 147e:2016 Upek Biometric Touchchip/Touchstrip Fingerprint Sensor
     Bus 001 Device 002: ID 8087:0024 Intel Corp. Integrated Rate Matching Hub
     Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

2.设置adb识别设备属性

     sudo vi /etc/udev/rules.d/51-android.rules

添加下面语句，标示出设备代号

     SUBSYSTEM=="usb", ATTR{idVendor}=="12d1", ATTR{idProduct}=="1073",  MODE="0777"

3.设置端口代理

     adb reverse tcp:8081 tcp:8081

4.启动js传输监控

     react-native start

5.安装app
    
     react-native run-android

### 备注

如果你手机有360，安装好app后，白屏，需要去360里开启这个应用的一些权限；华为x2手机安装失败，目前解决方案是

     /home/xingwenpeng/workspace/reactnative/react-native-android-tablayout/example/android/app/build/outputs/apk

    目录下拷贝app-debug.apk到手机上，然后再安装，同步下载js。

    adb install android/app/build/outputs/apk/app-debug.apk


## Android发布apk

基本上可以参照官方教程里的例子做。有一处路径不一致的地方需要注意。

设置gradle变量
     把my-release-key.keystore文件放到你工程中的android/app文件夹下。
     编辑project/android/gradle.properties，添加如下的代码（注意官网给出的路径不对）

     MYAPP_RELEASE_STORE_FILE=my-release-key.keystore
     MYAPP_RELEASE_KEY_ALIAS=my-key-alias
     MYAPP_RELEASE_STORE_PASSWORD=*****
     MYAPP_RELEASE_KEY_PASSWORD=*****

参照官网翻译帖子。

     http://reactnative.cn/docs/signed-apk-android.html#content
     





