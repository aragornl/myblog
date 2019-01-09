---
title: VPS设置及部分软件安装笔记
mathjax: true
date: 2018-03-30 19:58:18
tags:
- 测试
- math
categories:
- 笔记
---

## vps服务器设置
 账号密码什么的 这段就不显示了

## SS一键安装

```
git clone https://github.com/Flyzy2005/ss-fly
ss-fly/ss-fly.sh -i password [port]
```



## 安装jupyter到vps



```
#设置
/home/aero/.jupyter/jupyter_notebook_config.py
# 设定ip访问，允许任意ip访问
c.NotebookApp.ip = '*'
# 不打开浏览器
c.NotebookApp.open_browser = False
# 用于访问的端口，设定一个不用的端口即可，这里设置为7000
c.NotebookApp.port = 7000
# 设置登录密码， 将刚刚复制的内容替换此处的xxx
c.NotebookApp.password = u'sha1:23ae392f285d:aebea62b9b58bad057dc06786907802bb655e28d'

后台运行nohup jupyter notebook >/dev/null 2>&1 &
运行 jupyter notebook

```

## nginx设置

```
配置 
vi /etc/nginx/conf.d/ghost.conf
输入内容：
#jupyter 代理设置有一个什么新技术
server {  
    listen 80;
    server_name xxxxx.aragornl.com; #将 example.com 改为你的域名或ip。
    location / {
        proxy_pass http://127.0.0.1:xxx/;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header Host $host;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_redirect off;
        
    }
}
server {  
    listen 80;
    server_name xxxxx.aragornl.com; #将 example.com 改为你的域名或ip。
    location / {
        proxy_set_header   X-Real-IP $remote_addr;
        proxy_set_header   Host      $http_host;
        proxy_pass         http://xxxxxxxx：xx/;
    }
}

service nginx start # 启动Nginx  
systemctl enable nginx #开机启动Nginx
service nginx restart #重启Nginx

```

## hexo

安装Node.js git

```
修改Npm 源 npm config set registry https://registry.npm.taobao.org
安装Hexo npm install -g hexo-cli
切换到文件夹
hexo init #安装
hexo g 生成文件
hexo s 部署服务
hexo d 上传文件
```

以下数学公式测试
$$
\sum_{i=1}^n a_i=0
$$
然而对于$x>0,$ 有 $f(x)>0.  $

$(x_1,x_x,\ldots,x_n) = x_1^2 + x_2^2 + \cdots + x_n^2$

$f(x,y,z) = 3y^2 z \left( 3 + \frac{7x+5}{1 + y^2} \right).$



$$\frac{\partial u}{\partial t}= h^2 \left( \frac{\partial^2 u}{\partial x^2}\frac{\partial^2 u}{\partial y^2}\frac{\partial^2 u}{\partial z^2}\right)$$ 