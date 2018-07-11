---
title: nodejs搭建过程

---

nodejs环境搭建步骤
<!-- more -->
### 第一步：下载nodejs并安装，安装成功后使用如下命令查看是否成功：
```html
node -v 
npm -v
```
![](/images/查看nodejs安装你状态.png)

### 第二步：配置npm的全局模块的存放路径以及cache的路径
我们要先配置npm的全局模块的存放路径以及cache的路径，例如我希望将以上两个文件夹放在NodeJS的主目录下，便在NodeJs下建立"node_global"及"node_cache"两个文件夹

```html
npm config set prefix "D:\software\nodejs\node_global"
以及
npm config set cache "D:\software\nodejs\node_cache"
```
### 第三步：npm修改源
由于不可说原因，npm install时，速度总是不尽如人意，解决办法是修改npm的数据源
```html
npm config set registry https://registry.npm.taobao.org 
```
修改后可以通过这个进行测试
```html
npm config get registry
```
上面这两个配置都是可以在C:\Users\xliangcf.npmrc文件下查看
```html
内容如下
```
### 第四步：修改path路径
进入环境变量对话框，在系统变量下新建"NODE_PATH"，输入：
```html
D:\software\nodejs\node_gobal\node_modules“。（ps：这一步相当关键。）
```
2014.4.19新增：由于改变了module的默认地址，所以上面的用户变量都要跟着改变一下（用户变量"PATH"修改为:
```html
D:\software\nodejs\node_gobal\
```
要不使用module的时候会导致输入命令出现“xxx不是内部或外部命令，也不是可运行的程序或批处理文件”这个错误。
