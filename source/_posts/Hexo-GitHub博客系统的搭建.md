---
title: Hexo+GitHub博客系统的搭建
date: 2020-03-21 14:25:13
tags: [Hexo]
---

如果单是作为笔记功能，那么由`Hexo`提供的页面框架，`GitHub`提供网络访问环境。`Hexo+GitHub`搭建的博客系统无疑是最好的选择。

---

### 环境搭建

1. 安装git,通过**git \-\-version**,检查是否安装成功
2. 安装nodejs,通过**node -v**、**npm -v**,检查是否安装成功
3. 安装hexo

```cmd
#安装命令
npm install -g hexo-cli

#检查是否安装成功
hexo -v

顺便一说一下

卸载命令
npm uninstall hexo-cli -g

```

如果安装时出现了一下警告

![安全警告.png](https://httpsvn.github.io/images/0.png "安全警告")  

是因为mac下需要 fsevents，在windows或linux环境下，请忽略这个错误。

### 搭建博客
```cmd

#初始化hexo，myblog名字随意
hexo init myblog

#进入myblog
npm install
```

#### 搭建完毕后文件目录
* node_modules: 依赖包
* public：存放生成的页面
* scaffolds：生成文章的一些模板
* source：用来存放你的文章
* themes：主题
* _config.yml: 博客的配置文件

本地查看

```cmd
hexo g
hexo server
```
打开hexo的服务，在浏览器输入localhost:4000就可以看到你生成的博客了。

### GitHub创建个人仓库

1. 在你的GitHub下新建一个应用, <font color=#00FFFF >XXX.github.io</font>
2. 生成SSH添加到GitHub
```
git config --global user.name "yourname"
git config --global user.email "youremail"

#检查是否输入正确
git config user.name
git config user.email

#创建
ssh-keygen -t rsa -C "youremail"
```
完成后会生成连个文件 *id_rsa*这台电脑的私人秘钥和*id_rsa.pub*公钥，把公钥信息保存到你的github账号下面，
*github -> setting -> 找到SSH -> 点击New SSH key -> 添加公钥信息*
```
查看是否成功
ssh -T git@github.com
```
### 将Github与Hexo建立联系

在博客配置文件 *_config.yml*

```
deploy:
  type: git
  repo: https://github.com/YourgithubName/YourgithubNamhexoe.github.io.git
  branch: master
```
安装deploy-git，也就是安装部署命令,这样你才能用命令部署到GitHub。
```
npm install hexo-deployer-git --save
```
部署命令

```
#清除了你之前生成的东西
hexo clean

#生成静态文章
hexo generate

#部署文章
hexo deploy
```

完成以上步驟，博客就搭建好好了，访问自己的链接就可以看到成果了。

### 访问404情况

将链接改成`.com`访问一次，在正常访问就可以了，是服务缓存的问题，尤其是你以前搭建过的情况



### 主题更换

[主题传送门](https://hexo.io/themes/)

以next主题为列：
```
git clone https://github.com/iissnan/hexo-theme-next themes/next

```
clone下来方到博客目录 *themes* 中，配置博客根目录中的 *_config.yml*。
```
#修改
theme: next

```
在主题next目录下面还有一个 *_config.yml* 找到Scheme Settings 这里可以切换样式


### 更换设备

你不可能只在一个台电脑上写博客，如果更换设备后怎么实现继续开发博客。
首先，我们post到github上的不是源文件，是编译后到文件，是用来生成网页的。为了解决这个问题，我们可以把博客源文件保存到GitHub上这样换了电脑也可以继续写。
为了方便为博客项目创建一个分支，这个分支不要合并,并把这个分支设置为默认分支，clone下分支。
<font color=#ff0000 >注意：</font>

1. 先把clone 下来的文件除了.git 文件夹外的所有文件都删掉
2. 拷贝博客源文件，除了.deploy_git，注意一定要把主题下面的.git文件删除，如果过没有.gitignore,创建一个
```
.DS_Store
Thumbs.db
db.json
*.log
node_modules/
public/
.deploy*/
```
提交分支，用GitHub Desktop操作跟方便。

3. 更换电脑后

    1. 安装git
    2. 安装nodejs
    3. 添加ssh key
    4. 安装hexo
    5. clone 博客源文件
    6. 进入克隆的文件夹
    ```
    npm install
    npm install hexo-deployer-git --save
    ```
可以开始写文章了

### 写文章的一些命令

新建文章
hexo new post var、val和const的解释
