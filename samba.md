## Samba
#### 實作
安裝samba
```
yum install samba –y
```
關掉selinux
※永久關閉方法
```
vi /etc/sysconfig/selinux   
找到
SELINUX=enforcing
然後修改為
SELINUX=disabled
```
`註：`要重新開機 `reboot / restart `後才會套用
關掉防火牆
```
systemctl stop firewalld
```
開啟smb和nmb
```
systemctl start smb
systemctl start nmb
```
確認是否開啟smb和nmb
```
systemctl status nmb
systemctl status smb
```
創建samba的帳密
`註：`必須先創一個帳號，這裡使用的是自己本身就有的帳號(user)
```
smbpasswd -a user
```
<img src="https://github.com/syuan0327/linux2/blob/master/samba.jpg" weight=50%>

ifconfig查看ip位址，並在windows左下角搜尋處輸入ip

<img src="https://github.com/syuan0327/linux2/blob/master/samba2.JPG">

進去後就可以輸入帳密進入user，並在裡面新增檔案，如果兩邊檔案有同步就代表成功了。

<img src="https://github.com/syuan0327/linux2/blob/master/samba3.JPG">



