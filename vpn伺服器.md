# vpn伺服器
## Linux設定
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
```
localip 10.0.10.1
//localip=伺服器跑起來的ip 
remoteip 10.0.10.2-254
//remoteip=撥接起來的ip 
```
#### 4.修改/etc/ppp/options.pptpd
```
gedit /etc/ppp/options.pptpd
```
修改ms-dns
```
ms-dns 8.8.8.8
ms-dns 1.1.1.1
```
#### 5.設定帳號密碼/etc/ppp/chap-secrets
```
username pptpd password *
//帳號名稱 伺服器名稱  密碼 來源ip(*=萬用字元)
```
#### 6.開啟pptpd
```
systemctl start pptpd
```
#### 7.確認pptpd是否開啟
```
systemctl status pptpd
```
## Windows操作部分
#### 1.網路設定(VPN)，按照下圖設定

<img src="https://github.com/syuan0327/linux2/blob/master/vpn.JPG"width="50">

