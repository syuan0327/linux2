## DHCP(動態主機設定協定)
## 網卡設定
No1 1.nat 2.僅限主機(貼上後關掉) 3.內部

No2 1.內部

`註：`這裡的NO1,NO2代表的是主機的號碼

`註：`這邊第一台主機設僅限主機網卡的原因是因為等下有設定檔要進行修改，而我的虛擬機是沒有安裝可以複製不同台內容的套件，因此這邊是直接用putty進行複製!請記得複製完後要關掉僅限主機網卡的連線!

如果忘記如何用putty，或不會使用，可以參考:[點我](https://github.com/syuan0327/Linux-note/tree/master/%E9%80%A3%E4%B8%8Aputty)

## 實作
#### No1

安裝dhcp
```
yum install dhcp
```
修改設定檔
```
vim /etc/dhcp/dhcpd.conf
```
貼上以下文字進去：
```
ddns-update-style            interim;
ignore client-updates;
default-lease-time           259200;
max-lease-time               518400;

subnet 192.168.100.0 netmask 255.255.255.0 {
    range 192.168.100.101 192.168.100.200;
    option routers               192.168.100.254;
    option domain-name-servers   8.8.8.8, 9.9.9.9;
}
```
設定內部網路網卡

`enp0s9:`內部網路網卡
```
ip addr add 192.168.100.254/24 brd + dev enp0s9
```
重新啟動DHCP
```
systemctl restart dhcpd
```

#### No2
dhclient命令 – 動態獲取或釋放IP位址

`enp0s3:`內部網路網卡
```
dhclient enp0s3
```
查看內部網路網卡是否出現192.168.100.101
```
ifconfig  
```
ping NO1的ip
```
ping 192.168.100.254
```
#### No1
ping NO2的ip
```
Ping 192.168.100.101
```
都可以ping的話，就代表你成功了!
