# vpn伺服器
#### 1.安裝yum第三方EPEL套件庫
```
sudo yum install epel-release -y
```
#### 2.安裝PPTP
```
sudo yum install ppp pptpd -y
```
#### 3.修改/etc/pptpd.conf
```
gedit /etc/pptpd.conf
```
進去後，拉到最下面新增
localip=伺服器跑起來的ip 
remoteip=撥接起來的ip 
```
localip 10.0.10.1
remoteip 10.0.10.2-254
```
#### 4.修改/etc/ppp/options.pptpd
```
gedit/etc/ppp/options.pptpd
```
修改ms-dns
```
ms-dns 8.8.8.8
ms-dns 1.1.1.1
