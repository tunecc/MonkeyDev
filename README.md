#修复了Xcode16的安装
原修复脚本来自：https://github.com/shadow-boy/MonkeyDev/tree/master/bin

```
sudo /bin/sh -c "$(curl -fsSL https://raw.githubusercontent.com/tunecc/MonkeyDev/refs/heads/master/bin/md-install_xcode16fix)"
```


# MonkeyDev支持无根越狱打包



随着 ios 15 越狱的稳定, 无根越狱的使用频率也越来越高, 而原来的MonkeyDev已多年没有更新，现在将MonkeyDev修改并支持无根越狱环境编译打包



## 更新Theos

```
# 安装最新版本的theos, 注意如果原来的theos有自行添加运行时头文件，请自行在复制到新版本的theos里面
git clone --recursive https://github.com/theos/theos.git
```



## 更新本仓库的MonkeyDev

```
下载最新的MonkeyDev的代码放到原来的旧MonkeyDev路径即可，注意保持路径不变
或者
只需要将项目 bin/md 文件替换到 本地MonkeyDev/bin目录下即可，注意可执行权限
```



## 修改项目模板

~/Library/Developer/Xcode/Templates/MonkeyDev/ 指向就是 MonkeyDev安装目录下的/templates

```
# 是否要使用sudo提权，根本自己MonkeyDev安装目录来来决定
# 执行以下命令
sudo /usr/libexec/PlistBuddy -c "Add :Targets:0:SharedSettings:MonkeyDevRootless string YES"  ~/Library/Developer/Xcode/Templates/MonkeyDev/Base.xctemplate/TemplateInfo.plist
sudo /usr/libexec/PlistBuddy -c "Add :Targets:0:SharedSettings:CODE_SIGNING_ALLOWED string NO"  ~/Library/Developer/Xcode/Templates/MonkeyDev/Base.xctemplate/TemplateInfo.plist
sudo /usr/libexec/PlistBuddy -c "Set :Targets:0:SharedSettings:MonkeyDevDeviceIP localhost"  ~/Library/Developer/Xcode/Templates/MonkeyDev/Base.xctemplate/TemplateInfo.plist
sudo /usr/libexec/PlistBuddy -c "Set :Targets:0:SharedSettings:MonkeyDevDevicePassword alpine"  ~/Library/Developer/Xcode/Templates/MonkeyDev/Base.xctemplate/TemplateInfo.plist
sudo /usr/libexec/PlistBuddy -c "Set :Targets:0:SharedSettings:MonkeyDevDevicePort 2222"  ~/Library/Developer/Xcode/Templates/MonkeyDev/Base.xctemplate/TemplateInfo.plist
sudo /usr/libexec/PlistBuddy -c "Set :Targets:0:SharedSettings:MonkeyDevkillProcessOnInstall "  ~/Library/Developer/Xcode/Templates/MonkeyDev/Base.xctemplate/TemplateInfo.plist
```



## 编译DEB

```
根据自己的手机是否是rootless越狱设置Build Setting里的MonekDevRootless为 YES 或 NO 即可 
```



## 感谢MonkeyDev原作者的分享

引用 https://github.com/AloneMonkey/MonkeyDev
