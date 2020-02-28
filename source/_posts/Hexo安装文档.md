---
title: Hexo 安装文档
date: 2020-02-24 20:00:00
categories:
    - Linux
    - Hexo
tags:
    - Hexo

mp3: http://domain.com/awesome.mp3
cover: http://domain.com/awesome.jpg
---



Hexo

普通用户（非全局）安装nodejs和npm
wget -qO- https://raw.github.com/creationix/nvm/master/install.sh | sh
source .bashrc
nvm install stable
npm install -g hexo-cli
npm install
在库的路径下，配置好主题以后，安装deployer
npm install hexo-deployer-git --save

1、安装Nodejs(Node.js 版本需不低于 8.10，建议使用 Node.js 10.0 及以上版本)
yum install gcc-c++ make -y
curl -sL https://dl.yarnpkg.com/rpm/yarn.repo | sudo tee /etc/yum.repos.d/yarn.repo
 sudo yum install yarn -y

#As root

curl -sL https://rpm.nodesource.com/setup_13.x | bash -

#No root privileges 

curl -sL https://rpm.nodesource.com/setup_13.x | sudo bash -

sudo yum install -y nodejs

node -v
npm -v
npx -v

2、安装git
 yum install git-core

3、安装Hexo 
 (1) 使用npm命令安装Hexo
    npm install -g hexo-cli
    添加进环境变量
    echo 'PATH="$PATH:/usr/lib/node_modules/hexo-cli/bin"'>> ~/.profile
    source  ~/.profile
 (2) 初始化博客网站，
     mkdir blog
     cd blog
     hexo init blog
 (3)测试网站
    hexo new test_my_site
    hexo g
    hexo s   
     安装完成
  (4)常用命令

```
     hexo n "我的博客" == hexo new "我的博客" #新建文章
     hexo g == hexo generate #生成
     hexo s == hexo server #启动服务预览
     hexo d == hexo deploy #部署
```



     hexo server #Hexo会监视文件变动并自动更新，无须重启服务器
     hexo server -s #静态模式
     hexo server -p 5000 #更改端口
     hexo server -i 192.168.1.1 #自定义 IP
     hexo clean #清除缓存，若是网页正常情况下可以忽略这条命令


4、将 Hexo 博客部署到 GitHub Pages 上
   1、hexo 连接github有2种方式：https和git
     (1)用git 配置
          cd ~/.ssh
          sudo ssh-keygen -t rsa -C "你的注册邮箱" #生成ssh

          # 然后连按三下回车

          sudo gedit id_rsa.pub #打开id_rsa.pub文件，并把内容复制到剪切板
        登录github打开设置
        选择SSH and GPG keys，点New SSH
        然后配置SSH，点击Add SSH key完成
        配置SSH
          cd ~/.ssh #进入ssh目录
          sudo touch config #新建ssh的配置文件
          sudo gedit config #修改ssh的配置文件
          sudo chmod 600 config #添加权限
        config文件的内容：
          Host github.com                     
          User 你的注册邮箱                         
          Hostname ssh.github.com             
          PreferredAuthentications publickey  
          IdentityFile ~/.ssh/id_rsa          
          Port 443            
       测试
        sudo ssh git@github.com
       修改_config.yml
       修改deploy下的repo属性
         deploy:                                                               
           type: git                                           
           repo: git@github.com:你的name/你的username.github.io.git
           branch: master           
          
     (2)用https 配置
       修改_config.yml
       修改deploy下的repo属性
         deploy:                                                               
           type: git                                           
           repo: https://username:password@github.com/GreatSage01/GreatSage01.github.io.git
           branch: master     
   2、在网站根目录部署git插件
      npm install hexo-deployer-git --save
     git config --global user.email "1336562495@qq.com"
     git config --global user.name "GreatSage01"
   3、之后配置发布网站 
      hexo clean 
      hexo g 
      hexo d     
      hexo s
   4、访问github中hexo地址
      https://greatsage01.github.io            
      
      
5、使用nginx运行hexo
    修改nginx运行用户
      user root;
   通过hexo的渲染框架生成的静态资源文件放在的是public目录下，
   我们只需要让nginx代理这个目录就可以将hexo部署到nginx上。在ngingx.conf中更改相应的配置路径即可
    location / {
              root   /root/Hexo/blog/public;
              index  index.html index.htm;
           }
    nginx -s reload  重载配置
    
