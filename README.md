# openvpn


## 下载脚本并安装
``sudo wget https://raw.githubusercontent.com/lemonsterfy/openvpn/main/openvpn-install-advanced.sh``

``sudo bash openvpn-install-advanced.sh``

## rc.local缺失解决办法
*NOTES:The file 'rc.local' is missing in some system release, please create it manually.*

### 1.编写 rc-local.service 文件
``sudo vi /etc/systemd/system/rc-local.service``

``````
[Unit]  
 Description=/etc/rc.local Compatibility  
 ConditionPathExists=/etc/rc.local  
[Service]  
 Type=forking  
 ExecStart=/etc/rc.local start  
 TimeoutSec=0  
 StandardOutput=tty  
 RemainAfterExit=yes  
 SysVStartPriority=99  
[Install]  
 WantedBy=multi-user.target
``````
### 2.激活 rc-local.service
 ``sudo systemctl enable rc-local.service``

### 3.创建 /etc/rc.local，并赋予执行权限
 ``sudo vi /etc/rc.local``

````
#!/bin/bash
# rc.local
#
# This script is executed at the end of each multiuser runlevel.
# Make sure that the script will "exit 0" on success or any other
# value on error.
#
# In order to enable or disable this script just change the execution
# bits.
#
# By default this script does nothing.
 
exit 0
``````
``sudo chmod +x /etc/rc.local``

### 4.启动这个服务并查看它的状态
``sudo systemctl start rc-local.service``  
``sudo systemctl status rc-local.service``
