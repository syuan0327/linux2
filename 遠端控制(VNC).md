# 遠端控制
## Vitual Box
#### 1.新增一個新的使用者&設密碼
※密碼需要有英文和數字交雜
```
useradd jacky
```
```
passwd jacky
```
#### 2.複製VNC Server設定檔來建立新的設定檔
※VNC Server 設定檔在 /lib/systemd/system/vncserver@.service
```
cp /lib/systemd/system/vncserver@.service /etc/systemd/system/vncserver@:1.service
```
```
vi /etc/systemd/system/vncserver@:1.service
```
#### 3.修改設定檔
```
[Service]
Type=simple
# Clean any existing files in /tmp/.X11-unix environment
ExecStartPre=/bin/sh -c '/usr/bin/vncserver -kill %i > /dev/null 2>&1 || :'
ExecStart=/usr/sbin/runuser -l jacky -c "/usr/bin/vncserver %i"

# 一般帳號
PIDFile=/home/jacky/.vnc/%H%i.pid

# root 帳號
#PIDFile=/root/.vnc/%H%i.pid

ExecStop=/bin/sh -c '/usr/bin/vncserver -kill %i > /dev/null 2>&1 || :'
```

#### 4.切換至要設定的帳號，並建立 VNC Server 密碼
※和使用者密碼不同
```
su - jacky
```
```
vncpasswd
```

#### 5.切回 root 帳號，更新 systemctl 以使其生效
```
su -
```
```
systemctl daemon-reload
```
#### 6.啟動 VNC Server 
```
systemctl start vncserver@:1.service
```
#### 7.確認是否啟動 VNC Server
```
systemctl status vncserver@:1.service
```
## VNC Server 
#### 1.開啟 VNC Server
#### 2.輸入自己的ip位址+:5901
ip位址查詢：ifconfig
#### 3.成果
<img src="https://github.com/syuan0327/linux2/blob/master/l3.JPG" width=600>
