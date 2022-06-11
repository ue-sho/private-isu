
# MySQL

## スロークエリ

* スロークエリ設定
    * /etc/mysql/my.cnf
    * ```[mysqld]
      slow_query_log=1
      slow_query_log_file=/var/log/mysql/mysqlslow.log
      long_query_time=0
      ```
* スロークエリ解析
    * mysqldumpslow /var/log/mysql/mysqlslow.log
* ログの位置を変えたり、消したりしたら行う
    * mysqladmin flush-logs -u root -p

## インデックスを貼る

* テーブルを見る
    * SHOW CREATE TABLE comments;

* インデックスをつける
    * WHERE句で指定するやつにインデックスを貼るのが有効
    * ALTER TABLE comments ADD INDEX post_id_idx(post_id);

* 実行の状況を見る
    * EXPLAIN SELECT * FROM `comments` WHERE `post_id` = 9995 ORDER BY `created_at` DESC LIMIT 3;

+----+-------------+----------+------------+------+---------------+-------------+---------+-------+------+----------+----------------+
| id | select_type | table    | partitions | type | possible_keys | key         | key_len | ref   | rows | filtered | Extra          |
+----+-------------+----------+------------+------+---------------+-------------+---------+-------+------+----------+----------------+
|  1 | SIMPLE      | comments | NULL       | ref  | post_id_idx   | post_id_idx | 4       | const |    6 |   100.00 | Using filesort |
+----+-------------+----------+------------+------+---------------+-------------+---------+-------+------+----------+----------------+
1 row in set, 1 warning (0.00 sec)


# Python

* Flask実行
    * FLASK_APP=app.py flask run -p 8080 --debugger

# ベンチマーカー実行

./benchmarker/bin/benchmarker -t "http://localhost:8080" -u $PWD/benchmarker/userdat

## 並列実行

* ab (Apache Bench)
    * ab -c 1 -t 30
