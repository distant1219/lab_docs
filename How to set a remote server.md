**本教程只是一个简单的流程，针对校园网内ip屏蔽问题，只能实现CLI，校园网外访问实验室主机，具体步骤可自行搜索**
# 确保计算机开机自联网
使用pppoe连接校园网，用pppoeconf命令设置。
# 一台外网服务器
腾讯云服务器或者阿里云服务器，学生优惠大概10元每月。
# 在本地服务器上配置autossh，并设置开机自启
配置文件如下：
```
[Unit]
Description=Auto SSH Tunnel
After=network-online.target
[Service]
User=your_user_name
Type=simple
ExecStart=/usr/bin/autossh -p 22 -M 44271 -NR '*:44270:localhost:4422' USER@REMOTE_IP -i /home/distant1219/.ssh/id_rsa
ExecReload=/bin/kill -HUP $MAINPID
KillMode=process
Environment=AUTOSSH_GATETIME=0
Restart=always
[Install]
WantedBy=multi-user.target
WantedBy=graphical.target
                         
```
具体步骤参考：[A][1]、[B][2](需翻墙)

[1]:http://arondight.me/2016/02/17/%E4%BD%BF%E7%94%A8SSH%E5%8F%8D%E5%90%91%E9%9A%A7%E9%81%93%E8%BF%9B%E8%A1%8C%E5%86%85%E7%BD%91%E7%A9%BF%E9%80%8F/

[2]:https://blog.windrunner.me/sa/reverse-ssh.html
