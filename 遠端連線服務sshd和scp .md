## 遠端連線服務sshd和scp 
No1(代表第一台主機)

No2(代表第二台主機)

#### 1.	兩台開啟:sshd
```
systemctl start sshd 
```
#### 2.	確認開啟
```
systemctl status sshd
```
#### 3.	No1

建立test目錄
```
mkdir test
```
進去test目錄建立txt檔
```
touch {a..c}.txt
```
把資料從no1的folder傳到no2的folder
```
scp -r /home/test 192.168.xx.xx:/home/get
```
然後輸入第二台的passwd
<img src="https://github.com/syuan0327/linux2/blob/master/li.JPG">
#### 4.No2
建立get目錄
```
mkdir get
```
進入get目錄，輸入`ls`會發現裡面有test目錄，裡面放又從第一台傳來的txt檔

<img src="https://github.com/syuan0327/linux2/blob/master/li2.JPG">

