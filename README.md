此仓库用来发布个人使用的MIUI EU (Hyper OS) magisk 本地化模块，原作者为[MinaMichita](https://github.com/MinaMichita/MiuiEULocalizationToolsBox)，我在TA的基础上为我自用的小米13 (fuxi)进行了修改：
- 从国内版系统提取并更新了部分系统应用到新版
- 添加了适用于Android 14 (API 34)的钱包应用
- 部分功能修改为默认开启

<details>

Fonts=true
  
Mipay=true

ContentExtension=true

VirtualSim=true

PersonalAssistant=true

Calendar=true

MiuiIme=true

SogouInput=true

Mms=true

YellowPage=true

AiAsst=true

VoiceAssist=true

VoiceTrigger=true

Weather=true

ThemeManager=true

GboardTheme=true

VideocallBeautify=true

NotificationFilter=true

SoundRecorder=true

RemoveMod=true
</details>

在修改和制作此模块时，我使用的系统包版本为：
- EU: `xiaomi.eu_FUXI_OS1.0.24.5.6.DEV_14`
- 国内版: `miui_FUXI_OS1.0.24.4.22.DEV_51a9c7ee89_14.0`

不确定原作者模块是否绑定版本，故此修改版没有修改模块版本号，仍为`V14.0.7.0.TKHCNXM`

## 注意事项
- 此模块未在其他机型、其他系统版本上进行过测试，使用此模块代表你接受并自行承担可能的风险
- 建议提前做好数据备份工作

## 安装和使用

建议先阅读[原作者的使用说明](https://blog.minamigo.moe/archives/184)

1. [从Release页面下载模块](https://github.com/Patrick-Ze/MiuiEULocalizationToolsBox/releases/latest/download/MiuiLocalization.zip)然后使用magisk刷入

2. 你可能需要[下载生活黄页的apk](https://github.com/Patrick-Ze/MiuiEULocalizationToolsBox/releases/latest/download/MIUIYellowPage.apk)并执行一次手动安装，见后文的已知问题

## 已知问题

刷入此模块后，可能会因生活黄页缺少权限而无法启用“智能识别陌生号码”功能。如果你遇到此问题，可以尝试下面的步骤：

1. 在lxposed中启用“本地化工具箱”并打开设置，点击“允许安装系统应用”
2. 手动安装一次生活黄页的apk
3. 去通话设置里重新尝试打开“智能识别陌生号码”功能，此时会要求你授予权限：允许所有请求的权限

如果上面的办法仍然无法解决问题，你可能需要自行制作一个magisk模块：

1. 提取你的系统里的`system/product/etc/permissions/privapp-permissions-product.xml`文件
2. 打开此文件，找到对`com.miui.yellowpage`的授权部分，修改xml以确保授予了下面所有的权限
```xml
   <privapp-permissions package="com.miui.yellowpage">
      <permission name="android.permission.CALL_PRIVILEGED" />
      <permission name="com.android.voicemail.permission.READ_VOICEMAIL" />
      <permission name="com.android.voicemail.permission.WRITE_VOICEMAIL" />
      <permission name="android.permission.WRITE_SECURE_SETTINGS" />
      <permission name="android.permission.READ_PHONE_STATE" />
      <permission name="android.permission.POST_NOTIFICATIONS" />
      <permission name="android.permission.READ_CALL_LOG" />
      <permission name="android.permission.READ_EXTERNAL_STORAGE" />
      <permission name="android.permission.WRITE_CALL_LOG" />
      <permission name="android.permission.WRITE_EXTERNAL_STORAGE" />
   </privapp-permissions>
```
4. 刷入你制作好的模块，然后重新尝试前面小节的1-3步骤

由于xml提取自系统镜像，而不同版本的系统xml中预置的权限配置可能不同，因此不提供我这边的magisk模块，以免刷入后破坏其他系统应用的权限
