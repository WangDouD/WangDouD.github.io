---
title: 手动刷入GAPPS
date:  2017/5/2
tags: [Android,Course]

---

> GMS：在安卓智能机进入中国早期，国内大多数人习惯把 Google 服务包又叫做 GMS （ Googel Mobile Service ）服务包。但其实从严格意义上来讲， GMS 只存在于那些经过了 Google认证的手机厂商发售的 Android 设备当中，而Android 玩家一直以来乐此不疲地折腾的东西叫做 GAPPS。

<!--more-->

## GAPPS 介绍 ##
> GAPPS：全称Google Apps，一般是由国外某些 ROM 大神或是 ROM 团队为了完善他们的ROM体验而单独制作的Google应用和服务的整合包。GAPPS 不仅包含了Google服务的基本框架，根据版本的不同，也包含诸多 Google 自家的优秀应用。GAPPS 依旧是那些想要拥有完善 Android 体验的非 Nexus 手机用户和 Google 服务重度依赖者们的不二之选。

网络上常见的 GAPPS 主要有 ：
`PA GApps（已停更，版本稍旧）`，`Kang GApps`，`tk GApps`，`bank GApps`，`OpenGApps`等。
目前使用最广泛的是[OpenGApps][1]，大家熟知的CyanogenMod ROM（已停更），其使用的谷歌服务框架就是Open GApps，使用方便，操作简单。

以OpenGApps为例，提供的 GApps 主要包含以下几个版本：

### 1. aroma
值得一提，它是Open GApps 最近放出的一种版本，该版本具备图形化安装界面，在刷入过程中可自行选择需要安装的 GApps 组件，十分好用。（仅支持可以触摸操作的recovery下刷入，一般不建议使用。）

### 2. super
究极体，完整包里面包含了Nexus手机里所有的谷歌服务,也就是谷歌的核心服务，包含了所有的Google应用。（如果不是谷粉，一般都不刷这个包，因为实在太大了Orz）

### 3. stock
完整包里面包含了Nexus手机里所有的谷歌服务,也就是谷歌的核心服务，包含了所有的Google应用，并且会替换一部分原生应用，如`Chrome`、`日历`、`相机`、`谷歌输入法`、`Google Now 即时桌面`等等。

### 4. full
与 stock 所包含的内容相同，但是不包含：相机、谷歌输入法、Google Gallery, 并且不会替换掉`Chrome`、`日历`、`相机`、`谷歌输入法`、`Google Now 即时桌面`或者`Pico TTS服务`。
如果你想体验Nexus手机的谷歌服务，并且想继续使用原手机自带的启动器等服务，full 是最好的选择。

### 5. mini
包含了完整的 Google 服务框架和主流 Google 应用，去掉了 Google Docs 等文档处理应用，适合不太经常使用谷歌应用的人。包含有：`谷歌核心服务`、`通讯录日历同步服务`、`Google Now 即时桌面`、`Google Play services服务`、`Google 搜索`、`Google Text-to-Speech`、`Gmail`、`Google+`、`YouTube`、`Hangouts`、`谷歌地图`、`谷歌地图街景服务`。

### 6. micro
这个包是专为喜欢简约的用户准备的。它包含有：`谷歌核心服务`、 `通讯录日历同步服务`、`Google Play 商店` 、`Google Now 即时桌面`、`Google Play services服务`、`Google 搜索`、`Google Text-to-Speech`、`Gmail`。

### 7. nano
虽说是超小，但也包含了完整的 Google 服务框架，并不包含多余的 Google 应用。这个包适合那些不想占用太大内存，但是又想体验到原生的谷歌搜索服务的机友。包含有：`谷歌核心服务`、`通讯录日历同步服务`、`Google Play 商店`、`Google Play services服务`、`Google 搜索`。

### 8. pico
包含了最基础的 Google 服务框架，体积最小，适合仅仅想给系统装个Play商店的同学，其他的 Google 应用可以自己下载。**非常推荐**这个包，其他像Gmail、Youtube都可以到Google Play里下，还可以卸载。包含有：`谷歌核心服务`、 `通讯录日历同步服务`、`Google Play services服务`、`Google Play 商店`。

### 9. tvstock
电视专用服务包，不详。

## 安装 ##
### OpenGApps APP智能下载安装 （推荐） ###
下载 OpenGApps APP 后，选择上方推荐的相应服务包，自动进入第三方 Recovery 模式刷入。
OpenGApps APP 下载地址：https://play.google.com/store/apps/details?id=org.opengapps.app  （需科学上网，不过都刷服务包了，肯定有梯子的吧）

### 自行到 [OpenGApps][2] 下载服务包 ###
1. 参考上方推荐，下载相应服务包，放置到手机内置存储或外置SD卡，无需解压。
2. 进入第三方 Recovery 模式，选择服务包，刷入，无需双清或三清，重启。

## 问题集锦 ##

### 刷完开机后，一直弹“Google Play服务”已停止运行。 ###
![“Google Play服务”已停止运行][3]
解决方法：
a. 点确定后，趁第二次弹窗出来之前到设置-应用，找到Google相关的所有应用，把权限全都勾上，然后重启。（此方法可能无效，无效的话看b方法）
b. 手机开启USB调试，连接电脑，需要下载ADB包，[下载链接][4]， 密码: 7358。解压后运行包内的cmd，或者运行命令提示符，CD到ADB目录，输入命令并回车 `adb shell` ，
![连接电脑运行cmd][5]
如图，连接成功会出现类似字符串，之后输入以下命令并回车：
```
pm grant com.google.android.gms android.permission.BODY_SENSORS
pm grant com.google.android.gms android.permission.READ_SMS
pm grant com.google.android.gms android.permission.RECEIVE_MMS
pm grant com.google.android.gms android.permission.READ_EXTERNAL_STORAGE
pm grant com.google.android.gms android.permission.WRITE_EXTERNAL_STORAGE
pm grant com.google.android.gms android.permission.READ_CALENDAR
pm grant com.google.android.gms android.permission.CAMERA
pm grant com.google.android.gms android.permission.READ_CONTACTS
pm grant com.google.android.gms android.permission.WRITE_CONTACTS
pm grant com.google.android.gms android.permission.GET_ACCOUNTS
pm grant com.google.android.gms android.permission.ACCESS_FINE_LOCATION
pm grant com.google.android.gms android.permission.ACCESS_COARSE_LOCATION
pm grant com.google.android.gms android.permission.RECORD_AUDIO
pm grant com.google.android.gms android.permission.READ_PHONE_STATE
pm grant com.google.android.gms android.permission.CALL_PHONE
pm grant com.google.android.gms android.permission.READ_CALL_LOG
pm grant com.google.android.gms android.permission.PROCESS_OUTGOING_CALLS
pm grant com.google.android.gms android.permission.SEND_SMS
pm grant com.google.android.gms android.permission.RECEIVE_SMS
pm grant com.google.android.gms android.permission.READ_SMS
pm grant com.google.android.gms android.permission.RECEIVE_MMS
pm grant com.google.android.gms android.permission.READ_EXTERNAL_STORAGE
pm grant com.google.android.gms android.permission.WRITE_EXTERNAL_STORAGE
```
运行后，重启手机即可。

### 刷完开机后，不显示桌面一直弹“开机向导”已停止运行。 ###
解决方法：
a. 进入第三方Recovery模式，进入文件管理，删除 /system/priv-app/SetupWizard 目录。注：部分第三方Recovery需要挂载system目录才能看到内容，如果电脑可以进入此目录也可以，只要能删就可以，不一定非要在Recovery下。
b. 手机开启USB调试，连接电脑，需要下载ADB包，[下载链接][4]， 密码: 7358。解压后运行包内的cmd，或者运行命令提示符，CD到ADB目录，输入命令并回车 `adb shell` ，
![连接电脑运行cmd][5]
如图，连接成功会出现类似字符串，之后输入以下命令并回车：

```
pm grant com.google.android.setupwizard android.permission.READ_PHONE_STATE
pm grant com.google.android.setupwizard android.permission.CALL_PHONE
pm grant com.google.android.setupwizard android.permission.WRITE_CONTACTS
pm grant com.google.android.setupwizard android.permission.PROCESS_OUTGOING_CALLS
pm grant com.google.android.setupwizard android.permission.GET_ACCOUNTS
pm grant com.google.android.setupwizard android.permission.READ_CONTACTS
```
运行后，重启手机即可。

## 其他“系统” ##

>能刷第三方Recovery的尽量都采取上述方法刷入，其他安装器都多多少少容易出现问题。

小米机型：下载`Google Play商店`，[下载地址][6]，安装时会提示需要Google服务框架，点击确定下载，按照提示安装完毕后，重启即可。
![安装Google服务框架](https://ooo.0o0.ooo/2017/05/01/59074bcc1c8b4.png)
华为机型：在华为自带应用市场内搜索`Google Play Store`，安装即可。
三星机型：Android 7.0可以安装`Google Play商店`，[下载地址][6]，直接可以使用。Android 7.0以下的版本未root的情况下暂无方法，root的可以采用通用机型方法。
魅族机型：在魅族自带应用市场内搜索`谷歌安装器魅族专版`，或点[下载地址][7]，安装后，按照应用内提示安装，重启即可。
通用机型：推荐使用`GO谷歌安装器`，[下载地址][8]，或者`谷歌安装器`，[下载地址][9]。测试都可以正确安装GMS。

---
梯子就不推荐了，我知道反正你们都有办法哒。


  [1]: http://opengapps.org/
  [2]: http://opengapps.org/
  [3]: https://ooo.0o0.ooo/2017/04/28/59034cd127f0a.jpg
  [4]: https://pan.baidu.com/s/1cq11Iu
  [5]: https://ooo.0o0.ooo/2017/04/28/59035e8c46e9c.jpg
  [6]: https://www.coolapk.com/apk/com.android.vending
  [7]: http://app.meizu.com/apps/public/detail?package_name=com.howie.gserverinstall
  [8]: https://www.coolapk.com/apk/com.goplaycn.googleinstall
  [9]: https://www.coolapk.com/apk/com.ericxiang.googleinstaller
