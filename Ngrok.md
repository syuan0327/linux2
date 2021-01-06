Ngrok
安裝httpd
```
yum install httpd
```
打開httpd
```
systemctl start httpd
```
確認是否開啟
```
systemctl status httpd
```
下載ngrok
```
wget https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-linux-amd64.zip
```
解壓縮
```
unzip ngrok-stable-linux-amd64.zip
```
登入ngrok，找到authtoken，在虛擬機輸入自己的token
```
./ngrok authtoken 1jSRufsegdioeprgthyjukiloiuyfthdr
```
然後輸入
```
./ngrok http 80
```
得到網址後，將其貼到網站上就成功了~

