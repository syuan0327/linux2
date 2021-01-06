## Nat Server
No1網卡：1.nat 2.僅限主機 3.內部網路(代表第一台主機)
No2網卡：1.內部網路(代表第二台主機)
## 實作
關閉防火牆
```
systemctl stop firewalld
```
## No2

清除enp0s3的ip
```
ifconfig enp0s3 0
```
新增一個ip在enp0s3
```
ip addr add 192.168.1.2/24 brd + dev enp0s3
```
路由設定
```
ip route add defaule via 192.168.1.1
```
使用`ip route show`查看是否有設定好

## No1

dhclient命令 – 動態獲取或釋放IP位址
```
dhclient enp0s3
```
清除enp0s9的ip
```
ifconfig enp0s9 0
```
新增一個ip在enp0s3
```
ip addr add 192.168.1.1/24 brd + dev enp0s9
```
接著`ping 192.168.1.2`看能不能通(第二台設定的ip)

啟動ip轉發
```
echo > 1 /proc/sys/net/ipv4/ip_forward
```
iptables設定
```
iptables -A FORWARD -o enp0s3 -i enp0s9 -s 192.168.1.0/24 -m conntrack --ctstate NEW -j ACCEPT
```
```
iptables -A FORWARD -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
```
```
iptables -t nat -A POSTROUTING -o enp0s3 -s 192.168.1.0/24 -j MASQUERADE
```
## No2

輸入vim /etc/resolv.conf，把nameserver改成8.8.8.8

然後ping tw.yahoo.com，如果有通就代表成功！


