## NFS
做檔案分享用
## 網路卡設定
No1 nat 僅限

No2 nat 僅限
## 實作
#### No1
安裝`nfs-utils`
```
yum install nfs-utils -y
```
開啟
```
systemctl start rpcbind
systemctl start nfs
```
檢查
```
systemctl status rpcbind
systemctl status nfs
```
關防火牆
```
systemctl stop firewalld
```
創建data目錄
```
mkdir -p /data
```
開權限
```
chmod 755 /data 
```
查看檔案權限
```
ls -l -d /data
```
更改/etc/exports
```
vim /etc/exports
```
填入：
```
/data/ 192.168.56.0/24(rw,sync,no_root_squash,no_all_squash)
```
重開nfs
```
systemctl restart nfs
```
查看nfs共用列表
```
showmount -e localhost(會跑出ip)
```
#### No2
```
yum install nfs-utils -y
```
```
mkdir -p /mydata
```
```
showmount -e 192.168.56.112(第一台ip)
```
```
mount -t nfs 192.168.56.112:/data /mydata
```
```
cd /mydata
```
創建檔案
```
touch {a..c}
```
ls
#### No1
```
touch {1..3}
```
#### No2
```
ls
```
## 結果顯示
<img src="https://github.com/syuan0327/linux2/blob/master/nfs.JPG" >

