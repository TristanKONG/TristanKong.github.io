# SQOOP

## 导入RDBMS表的子集到HDFS：

   ```
   sqoop import --connect jdbc:mysql://[ip]:3306/[database] \
   --username root --password Root123! \
   --table [table] \
   --columns name,id,dept \
   --hive-import --hive-table [database].[table] \
   --target-dir /sqoopIquery \
   --m 1
   ```

##  使用自定义查询语句导入数据：

   ```
   sqoop import --connect jdbc:mysql://[ip]:3306/[database] \
   --username root --password Root123! \
   --query 'SELECT a.name, a.salary, b.city FROM emp a JOIN emp_addr b ON a.id = b.id WHERE $CONDITIONS AND a.salary >= 30000' \
   --hive-import --hive-table [database].[table] \
   --target-dir /sqoopIquery \
   --m 1
   ```

##  增量导入：

   ```
   sqoop import --connect jdbc:mysql://[ip]:3306/[database] \
   --username root --password Root123! \
   --table [table] \
   --incremental append \
   --check-column required_column-in-table \
   --last-value last_seen_or_written_value \
   --hive-import --hive-table [database].[table] \
   --target-dir /sqoopIquery \
   --m 1
   ```

##  使用lastmodified模式增量数据导入：

   ```
   sqoop import --connect jdbc:mysql://[ip]:3306/[database] \
   --username root --password Root123! \
   --table [table] \
   --incremental lastmodified \
   --check-column hire_date --last-value '2019-05-02' \
   --target-dir /sqoopIquery \
   --m 1
   --append
   ```



##  使用安全参数列出所有数据库：

   ```
   sqoop list-databases --connect jdbc:mysql://[ip]:3306 --username root --password Root123! –verbose
   ```

##  在CLI上询问密码以列出所有数据库：

   ```
   sqoop list-databases --connect jdbc:mysql://192.168.172.1:3306 --username root –P
   ```

##  创建MySQL密码文件：

   ```
   echo -n 'Root123!' > /tools/.mysql.password
   ```

##  使用密码文件列出所有数据库：

   ```
   sqoop list-databases --connect jdbc:mysql://192.168.172.1:3306 --username root --password-file file:///tools/.mysql.password
   ```

##  导入所有表到HDFS的/root目录：

   ```
   sqoop import-all-tables -connect jdbc:mysql://192.168.172.1:3306/test -username root -P
   ```



##  导入MySQL数据到HDFS：

   ```
   sqoop import --connect jdbc:mysql://localhost/[database] \
   --username root --password Root123! \
   --table [table] \
   --hive-import --hive-table niit_bd2.h_author \
   --m 1
   ```



##  使用--where标签导入RDBMS表的子集到HDFS：

   ```
   sqoop import --connect jdbc:mysql://192.168.172.152:3306/[database] \
   --username root --password Root123! \
   --table [table] \
   --where "name='Tristan'" \
   --hive-import --hive-table [database].[table] \
   --m 1
   ```

##  使用自由形式查询导入数据：

   ```
   sqoop import --connect jdbc:mysql://192.168.172.152:3306/[database] \
   --username root --password Root123! \
   --query ‘ select a.id, a.name, b.major, b.tech from stu_per a join stu_coll b on a.id=b.id WHERE $CONDITIONS' \
   --hive-import --hive-table [database].[table] \
   --target-dir /bd3 \
   --m 1
   ```

##  导入数据为文本文件格式：

   ```
   sqoop import --connect jdbc:mysql://192.168.172.152:3306/[database] \
   --username root \
   --password Root123! \
   --query 'select * from author where $CONDITIONS' \
   --m 2 \
   --as-textfile \
   --split-by id \
   --target-dir /test/tbl \
   --fields-terminated-by ',' \
   --lines-terminated-by ' '
   ```

##  导入数据为Avro文件格式：

   ```
   sqoop import --connect jdbc:mysql://127.0.0.1:3306/[database] \
   --username root \
   --password Root123! \
   --query 'select * from ttable where $CONDITIONS' \
   --m 2 \
   --as-avrodatafile \
   --split-by id \
   --outdir /tools/files/tblA \
   --target-dir /test/tblA
   ```

##  导入数据为Parquet文件格式：

   ```
   sqoop import --connect jdbc:mysql://127.0.0.1:3306/[database] \
   --username root \
   --password Root123! \
   --table ttable \
   --m 2 \
   --as-parquetfile \
   --split-by id \
   --outdir /tools/files/tblP \
   --target-dir /test/tblP
   ```

##  导入数据为Sequence文件格式：

   ```
   sqoop import --connect jdbc:mysql://[ip]:3306/[database] \
   --username root \
   --password Root123! \
   --table ttable2 \
   --m 1 \
   --as-sequencefile \
   --split-by id \
   --bindir /tools/tblS \
   --target-dir /test/tblS
   ```

这些命令涵盖了Sqoop的基本导入功能，包括导入整个表、导入表的子集、使用自定义查询、增量导入以及不同文件格式的导入。