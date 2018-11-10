 tpc-ds
===
如何使用tpc-ds进行基准测试
1. 解压sourcecode里的编译工具
upzip 7d553f11-d402-4194-9208-30e36a9b188b-tpc-ds-tool.zip
2. 进入tools目录编译
make
3. 准备建表语句
tcp-ds已经准备好了建表的sql，位于tools目录下，具体的文件名为：
tpcds.sql，tpcds_ri.sql，tpcds_source.sql
根据自己的数据源的SQL语法，对上述文件的SQL语句进行修改
4. 创建表
连接数据源，执行第3步的建表SQL
5. 生成数据
进入tools目录下，执行以下命令：
./dsdgen -dir /home/lz/datas -scale 1 -delimiter \t （scale表示产生1G测试数据）
或者./dsdgen -dir /home/lz/datas -scale 1 -parallel 4 -child 1 （并行产生1g数据）
生成的数据字段值是以\t分割的
6. 导入数据
将这些数据导入到对应的表中
7. 增加语法模板
 工具自带提供了ansi.tpl，db2.tpl，netezza.tpl，oracle.tpl模板，定义了limit语句，需要根据自己的数据源提供相应的limit语句模板
8. 生成查询SQL
使用update_query.sh脚本修改query_template下query1-99模板，在行尾加define _END = ""，否则执行生成命令会出错。
该脚本放在query_template目录下执行
9. 执行sql




