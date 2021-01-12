## PHP
#### 顯示php頁面
安裝
```
yum install epel-release -y
```
```
yum install php -y
```
```
yum -y install php-gd php-ldap php-odbc php-pear php-xml php-xmlrpc php-mbstring php-snmp php-soap curl curl-devel
```
開啟httpd
```
systemctl start httpd
```
切換路徑
```
cd /var/www/html
```
修改info.php檔
```
vim info.php
```
輸入
```
<?php  phpinfo(); ?>
```
連入 自己的ip/info.php

#### 顯示時間
修改time.php檔
```
vim time.php
```
輸入
```
<?php
header("Refresh:1");
date_default_timezone_set('Asia/Taipei');
$today = date('Y/m/d H:i:s');
echo $today;
?>
```
連入 自己的ip/time.php

img src="<img src="https://github.com/syuan0327/linux2/blob/master/phptime.jpg">