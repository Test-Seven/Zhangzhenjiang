Zhangzhenjiang

# 1. 反编译任意apk，并且截图；
（1） 下载 易果生鲜.apk，改名.zip，解压后得到classes.dex
![img](https://github.com/Test-Seven/Zhangzhenjiang/blob/master/%E7%AC%AC3%E6%AC%A1Homework_20160306/image/01/1.png)

（2）下载dex2jar 工具，并解压，执行d2j-dex2jar.bat com.yiguo.appclasses.dex，得到com.yiguo.appclasses-dex2jar.jar 文件
![img](https://github.com/Test-Seven/Zhangzhenjiang/blob/master/%E7%AC%AC3%E6%AC%A1Homework_20160306/image/01/2.png)
 
（3）下载JD-GUI，并打开com.yiguo.appclasses-dex2jar.jar 文件
![img](https://github.com/Test-Seven/Zhangzhenjiang/blob/master/%E7%AC%AC3%E6%AC%A1Homework_20160306/image/01/3.png)


#2、使用aapt的命令查询权限，并且截图；
执行aapt dump permissions com.yiguo.app-1.apk
![img](https://github.com/Test-Seven/Zhangzhenjiang/blob/master/%E7%AC%AC3%E6%AC%A1Homework_20160306/image/02/01.png)
 
注：aapt.exe要添加环境变量
D:\7thTesting\Android\android-sdk\build-tools\23.0.2


#3、编写3种不同切入点的Android monkey的命令，并成功运行，同时说明切入点是什么；
(1)多点击，多滑动的操作
adb  shell monkey -p  com.yiguo.app  -p com.android.mms  -p com.android.browser --pct-motion 50  --pct-trackball 0  --pct-touch 50 --ignore-timeouts --ignore-crashes --throttle 500  -v 500

(2)多应用切换
adb  shell monkey -p  com.yiguo.app  -p com.android.mms  -p com.android.browser --pct-motion 10  --pct-trackball 0  --pct-touch 10  --pct-appswitch 80 --ignore-timeouts --ignore-crashes --throttle 500  -v 500

(3)手机硬件按钮（home power 音量键）
adb  shell monkey -p  com.yiguo.app  -p com.android.mms  -p com.android.browser --pct-motion 10 --pct-trackball 0  --pct-touch 5   --pct-syskeys 80 --pct-appswitch 5--ignore-timeouts --ignore-crashes --throttle 500  -v 500


#4、请找出Android monkey中motion和touch对应的源码里的方法，并找出monkey工具实现点击的最基础的方法是什么；
（1）motion 对应源码里的方法：MonkeyMotionEvent

![img](https://github.com/Test-Seven/Zhangzhenjiang/blob/master/%E7%AC%AC3%E6%AC%A1Homework_20160306/image/04/01.png)
 
（2）touch 对应源码里的方法：MonkeyTouchEvent
![img](https://github.com/Test-Seven/Zhangzhenjiang/blob/master/%E7%AC%AC3%E6%AC%A1Homework_20160306/image/04/02.png)

（3）monkey工具实现点击的最基础的方法是
monkey是在pc上执行的shell命令，通过把点击事件传给系统内“com.android.commands.monkey”这个进程实现的

#5、找到任意一个apk or ipa，然后去寻找里面的db，并打开，上传截图；
![img](https://github.com/Test-Seven/Zhangzhenjiang/blob/master/%E7%AC%AC3%E6%AC%A1Homework_20160306/image/05/01.png)
