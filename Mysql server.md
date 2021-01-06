## Mysql Server
#### 介紹
這篇會講述怎麼使用mysql寫表格，並顯示在網頁上。
## 實作
安裝 `mariadb-server`
```
yum install mariadb-server
```
開啟 `mariadb-server`
```
systemctl start mariadb.service
```
確認是否開啟 `mariadb-server`
```
systemctl status mariadb.service
```
進行檢測後輸入
```
mysql_secure_installation
```
之后按enter  再按y，設定密碼後接下来按顺序按n 按n 按n 按y

登入资料库系统
```
mysql -u root -p
```
输入之前設定的密碼

MariaDB [(none)]> show databases;
<img src='https://github.com/syuan0327/linux2/blob/master/mysql.jpg'>

然後輸入
```
create database testdb;
use testdb;
create table Persons (
  PersonID int,
  LastName varchar(255),
  FirstName varchar(255),
  Address varchar(255),
  City varchar(255)
);
```
MariaDB [testdb]> show tables;
<img src='https://github.com/syuan0327/linux2/blob/master/tables.'>

接著做以下動作
```
MariaDB [(none)]> drop table Persons;
MariaDB [(none)]> drop database testdb;
MariaDB [(none)]> create database testdb;
MariaDB [(none)]> use testdb;
MariaDB [(testdb)]> create table Persons(name char(11), age int(10), city varchar(255));
MariaDB [(testdb)]> insert into Persons(name, age, city) values ("syuan", 12, "Kaohsiung");
MariaDB [(testdb)]> insert into Persons(name, age, city) values ("peter", 32, "Taipei");
MariaDB [(testdb)]> insert into Persons(name, age, city) values ("mindy", 22, "Kinmen");
MariaDB [(testdb)]> show tables;
MariaDB [(testdb)]> select * from Persons;
```
結果：
<img src='https://github.com/syuan0327/linux2/blob/master/result.jpg'>

## 將結果顯示在網頁上
下載`php-mysql`
```
yum install php-mysql
```
邊test.php
```
gedit /var/www/html/test.php
```
輸入：
```
<?php
$server = "localhost";         # MySQL/MariaDB 伺服器
$dbuser = "root";       # 使用者帳號
$dbpassword = "centos"; # 使用者密碼
$dbname = "testdb";    # 資料庫名稱

# 連接 MySQL/MariaDB 資料庫
$connection = new mysqli($server, $dbuser, $dbpassword, $dbname);

# 檢查連線是否成功
if ($connection->connect_error) {
  die("連線失敗：" . $connection->connect_error);
}


$sqlQuery ="SELECT * from Persons;";

if ($result = $connection->query($sqlQuery)) {
  # 取得結果
  while ($row = $result->fetch_row()) {
    printf ("%s：%d\n", $row[0], $row[1]);
  }

  # 釋放資源
  $result->close();
} else {
  echo "執行失敗：" . $connection->error;
}

$connection->close();
?>
```
