---
title: Hexo搭建博客
date: 2019-05-03 23:50:24
tags: Hexo Github
categories: Technology
---
### 开通Github Pages博客功能
1. 进入Github站点，进行注册，详见[百度经验-注册github](https://jingyan.baidu.com/article/455a9950abe0ada167277864.html)。
2. 创建仓库 (Repository)
    ![](/images/创建repository.png)
3. 开启 Github pages
    ![](/images/开启Github Pages.png)
    ![](/images/打开Github Pages.png)
4. 选择主题
    ![](/images/随意选择主题.png)
5. 下载Github客户端
    [下载Github客户端](https://desktop.github.com/)
    Github客户端安装完毕后，登陆客户端并clone自己的Repository到本地。
    Github Pages 部分完成。

### Node.js 与 Hexo
1. [Node.js安装地址](https://nodejs.org/en/download/)
　　Node.js安装之后会自带npm命令工具，由于国内网络不稳定，需要将npm路径换成国内淘宝的cnpm
　　`npm install -g cnpm --registry=https://registry.npm.taobao.org`
　　随后即可使用与npm相同的方式进行包的控制

2. Hexo安装
　　在需要安装Hexo的目录下打开cmd，输入以下命令:
```angular2html
   $ cnpm install hexo-cli -g
   $ hexo init # 初始化网站
   $ cnpm install
   $ hexo g # 生成或 hexo generate
   $ hexo s # 启动本地服务器或者hexo server，随后就可以通过http://localhost:4000查看
```

　　创建文章
```angular2html
   $ hexo new 文章名
   $ hexo new page 页面名   # 页面就是一个文件夹，可以在里面放文章
```

　　常用简写
```angular2html
   $ hexo n == hexo new
   $ hexo g == hexo generate
   $ hexo s == hexo server
   $ hexo d == hexo deploy
```

### 添加主题
　　主题可以到[Hexo主题](https://hexo.io/themes/)下载，某些主题页面内没有说明使用方法，可以在当前页面内的关于中找到作者的github地址，在其仓库内找相应的Repository。

　　安装主题和渲染器：
```angular2html
    $ git clone https://github.com/tufu9441/maupassant-hexo.git themes/maupassant
    $ npm install hexo-renderer-pug --save
    $ npm install hexo-renderer-sass --save
```
　　编辑Hexo目录下的_config.yml，将theme的值改为maupassant，注意在修改_config.yml时里面的参数必须要按照以下格式进行编写：  
　　`key: value    #冒号后面必须有一个空格`

　　主题相关配置可见[maupassant主题配置](https://www.haomwei.com/technology/maupassant-hexo.html)
　　
### 使用Hexo deploy部署到github  

1. 检查SSH keys的设置
```
	$ 生成ssh keys
		ssh-keygen -t -rsa -C github邮箱地址
		#Enter file in which to save the key (/Users/your_user_directory/.ssh/id_rsa):<回车就好>
		#接下来会让你输入密码
		
	$ 移除已有的SSH key
		cd ~/.ssh
		ls
		mkdir key_backup
		cp id_rsa* key_backup
		rm is_rsa*
```

　　编辑根目录下_config.yml文件  
```angular2html
	deploy:
		type: git
		repo: git@github.com:ylance/ylance.github.io #填写自己的github网址
		branch: master
```

　　以后每次在更新博客的时候需要使用以下命令部署到Github上　　
```angular2html
    hexo g
    hexo d 
```
	
2. 添加SSH key到Github
　　进入Github中这个Repository的settings，选择Deploy keys，点击右上角的 add deploy key。在本地电脑上以文本方式打开C:\User\用户名\.ssh id_rsa.pub,全选复制其中内容。
　　![](/images/github SSH.jpg)
　　![](/images/复制ssh内容.png)　　

　　测试是否成功：
```angular2html
    ssh -T git@github.com
    # 之后会要求输入yes/no , 输入yes即可
```

　　设置账号信息：
```angular2html
    git config --global user.name 名字    #真实名字，不是github用户名
    git config --global user.email 邮箱    # github邮箱
    hexo g
    hexo d  #部署
```



