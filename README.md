# 这是一个基于weex的博客项目

>目前 Weex 主要支持 [Vue.js](https://weex.apache.org/zh/guide/use-vue-in-weex.html?spm=a2c7j.-zh-guide-front-end-frameworks.0.0.49c4400eAWFXh9) 和 [Rax](https://alibaba.github.io/rax/?spm=a2c7j.-zh-guide-front-end-frameworks.0.0.49c4400eAWFXh9) 作为其内置的前端框架。这些框架已经集成到了 Weex SDK，你不需要在额外引入。



# 开发环境搭建

* Android Studio SDK 23.02
* 新增变量ANDROID_HOME 变量值 C:\Users\yourUserName\AppData\Local\Android\Sdk
* 系统环境变量path C:\Users\yourUserName\AppData\Local\Android\Sdk\tools C:\Users\[yourUserName\AppData\Local\Android\Sdk\platform-tools
* /c/Users/kacoro/AppData/Roaming/npm/
* android studio v3.3.2 gradle v4.10.1 sdk v28.0.3

* 查看安装过的包
``` bash
npm list -g --depth 0
```
```
npm install -g weex-toolkit webpack 

npm install

#调试
weex debug

npm run serve

# android
weex platform add android
npm run android
npm run pack:android
```

QA

1、无法调试，
A:可能是由于本机有多个ip，我是因为安装了虚拟机，默认的ip与手机的ip网段不一致。禁用虚拟机的适配后解决，不想改config的ip

2、安卓无法正常调试打包，基于android studio v3.3.2 gradle v4.10.1 sdk v28.0.3 解决 [参见](https://www.cnblogs.com/chaichai/p/10087673.html)

3、安装完后 npm run android 居然支持热更新了。先在android studio启动一个模拟器后，android studio关闭

4、npm run pack:android 无法打包，comileReleaseJavaWithJavac报错
A：系统没有配置好javac，[下载](https://download.oracle.com/otn-pub/java/jdk/8u201-b09/42970487e3af4f5aa5bca3f542482c60/jdk-8u201-windows-x64.exe?AuthParam=1553078333_fe4ae5e2ccad0c6e5ba406517c35137e)
