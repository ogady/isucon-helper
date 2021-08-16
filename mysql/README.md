# mysql調査方法

## MySQL繋がらないとき

### MySQLに接続できるホスト設定に問題は無いか？

```sh
mysql> select user, host from mysql.user;
+------------------+----------------+
| 対象のuser        | localhost -> % |
| debian-sys-maint | localhost      |
| mysql.session    | localhost      |
| mysql.sys        | localhost      |
| root             | localhost      |
+------------------+----------------+
```

### MySQLの設定ファイルに問題は無いか？

```sh
$sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf
...
#bind-address            = 127.0.0.1
bind-address            = 0.0.0.0
...
```

## slow query取得設定

```/etc/mysql/mysql.conf.d/mysqld.cnf
<!-- /etc/mysql/mysql.conf.d/mysqld.cnfを修正する -->
[mysqld]
slow_query_log         = 1
slow_query_log_file    = /var/log/mysql/mysql-slow.log
long_query_time = 0
```

## slow query集計方法

[公式Doc](https://dev.mysql.com/doc/refman/5.6/ja/mysqldumpslow.html)

```sh
# 平均実行時間でソートする
$sudo mysqldumpslow -s at /var/log/mysql/mysql-slow.log > /home/isucon/slow_query_at.log

# 合計実行時間でソートする
$sudo mysqldumpslow -s t /var/log/mysql/mysql-slow.log > /home/isucon/slow_query_at.log
```
