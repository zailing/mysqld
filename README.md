# mysqld
mysql性能分析
CentOS release 6.5x64 mysql 5.6.19x64位性能测试测试

mysql 性能测试测试文字
测试环境：
硬件配置：CentOS release 6.6  x64位系统  62GB内存  一块普通sisc160GB硬盘  和一块 三星1TB 固态硬盘  分别挂在  两块上做测试

1U配置 8* Intel(R) Xeon(R) CPU           E5606  @ 2.13GHz
数据库版本：mysql  Ver 14.14 Distrib 5.6.19, for Linux (x86_64)
测试工具： 使用mysql自带的开源工具：mysqlslap
测试方法：
普通磁盘-测试本次测试以1000个并发线程、测试1次，自动生成SQL测试脚本、读、写、更新混合测试、自增长字段、测试引擎为myisam、共运行10次查询，输出cpu资源信息
mysqlslap -uroot -p --concurrency=1000 --iterations=1 --auto-generate-sql --auto-generate-sql-load-type=mixed --auto-generate-sql-add-autoincrement --engine=myisam --number-of-queries=10 --debug-info
Running for engine myisam
运行引擎MyISAM
Average number of seconds to run all queries: 0.826 seconds
平均秒数运行所有查询：0.826秒
Minimum number of seconds to run all queries: 0.826 seconds
最小秒数，运行所有查询：0.826秒
Maximum number of seconds to run all queries: 0.826 seconds
最大秒数运行所有查询：0.826秒
Number of clients running queries: 1000
运行查询的客户数：1000
Average number of queries per client: 0
每个客户的平均查询数：0
User time 0.24, System time 0.51
用户时间0.24，系统时间0.51
Maximum resident set size 41140, Integral resident set size 0
最大驻留集大小为41140，积分驻留集合大小为0
2（SSD 固态硬盘测试）：
  本次测试以1000个并发线程、测试1次，自动生成SQL测试脚本、读、写、更新混合测试、自增长字段、测试引擎为myisam、共运行10次查询，输出cpu资源信息
mysqlslap -uroot -p --concurrency=1000 --iterations=1 --auto-generate-sql --auto-generate-sql-load-type=mixed --auto-generate-sql-add-autoincrement --engine=myisam --number-of-queries=10 --debug-info
Running for engine myisam
运行引擎MyISAM
Average number of seconds to run all queries: 0.831 seconds
平均秒数运行所有查询：0.611秒
Minimum number of seconds to run all queries: 0.831 seconds
最小秒数，运行所有查询：0.631秒
Maximum number of seconds to run all queries: 0.831 seconds
最大秒数运行所有查询：0.631秒
Number of clients running queries: 1000
运行查询的客户数：1000
Average number of queries per client: 0
每个客户的平均查询数：0
User time 0.27, System time 0.51
用户时间0.27，系统时间0.51
Maximum resident set size 41288, Integral resident set size 0
最大驻留集大小为41288，积分驻留集合大小为0
Non-physical pagefaults 8198, Physical pagefaults 0, Swaps 0
非物理故障数目8198，物理故障数目0，掉期0
Blocks in 0 out 0, Messages in 0 out 0, Signals 0
块0出0，信息在0出0，信号0
测试结果对比：
可以看出ssd比之前scsi硬盘查询速度要快20% 速度。
测试方法二：
1  ssd 固态测试-如以５000个并发线程、测试1次，自动生成SQL测试脚本、读、写、更新混合测试、自增长字段、测试引擎为myisam、共运行10次查询，输出cpu资源信息
mysqlslap -uroot -p --concurrency=5000 --iterations=1 --auto-generate-sql
--auto-generate-sql-load-type=mixed --auto-generate-sql-add-autoincrement --engine=myisam
--number-of-queries=10 --debug-info
运行引擎MyISAM
Average number of seconds to run all queries: 7.201 seconds
平均秒数运行所有查询：7.201秒
Minimum number of seconds to run all queries: 7.201 seconds
最小秒数，运行所有查询：7.201秒
Maximum number of seconds to run all queries: 7.201 seconds
最大秒数运行所有查询：7.201秒
Number of clients running queries: 5000
运行查询的客户数：5000
Average number of queries per client: 0
每个客户的平均查询数：0
User time 1.37, System time 2.80
用户时间1.37，系统时间2.80
Maximum resident set size 217496, Integral resident set size 0
最大驻留集大小为217496，积分驻留集合大小为0
Non-physical pagefaults 36187, Physical pagefaults 0, Swaps 0
非物理故障数目36187，物理故障数目0，掉期0
2 scsi硬盘测试 以５000个并发线程、测试1次，自动生成SQL测试脚本、读、写、更新混合测试、自增长字段、测试引擎为myisam、共运行10次查询，输出cpu资源信息
Running for engine myisam
运行引擎MyISAM
Average number of seconds to run all queries: 6.507 seconds
平均秒数运行所有查询：9.507秒
Minimum number of seconds to run all queries: 6.507 seconds
最小秒数，运行所有查询：6.507秒
Maximum number of seconds to run all queries: 6.507 seconds
最大秒数运行所有查询：9.507秒
Number of clients running queries: 5000
运行查询的客户数：5000
Average number of queries per client: 0
每个客户的平均查询数：0
User time 1.31, System time 2.81
用户时间1.31，系统时间2.81
Maximum resident set size 217056, Integral resident set size 0
最大驻留集大小为217056，积分驻留集合大小为0
Non-physical pagefaults 36137, Physical pagefaults 0, Swaps 0
非物理故障数目36137，物理故障数目0，掉期0
测试结论：可以看出ssd比之前scsi硬盘不管是查询还是读写来说速度要快30% 以上速度。
测试方法三：
   sisc硬盘测试时mysql的连接1000个进程数：
   Average number of seconds to run all queries: 3.121 seconds
   平均秒数运行所有查询：3.121秒
   Minimum number of seconds to run all queries: 2.975 seconds
   最小秒数，运行所有查询：2.975秒
   Maximum number of seconds to run all queries: 3.577 seconds
   最大秒数运行所有查询：3.577秒
    Number of clients running queries: 1000
   运行查询的客户数：1000
   Average number of queries per client: 0
   每个客户的平均查询数：0
   
   ssd固态硬盘测试时mysql的连接1000个进程数
  mysqlslap -a -c 1000 -i 10 -uroot -p密码
Average number of seconds to run all queries: 24.000 seconds
平均秒数运行所有查询：24秒
Minimum number of seconds to run all queries: 21.862 seconds
最小秒数，运行所有查询：21.862秒
Maximum number of seconds to run all queries: 34.034 seconds
最大秒数运行所有查询：34.034秒
Number of clients running queries: 3000
运行查询的客户数：3000
Average number of queries per client: 0
每个客户的平均查询数：0

ssd固态硬盘测试 500和10000个并发分别得到一次测试结果，并发数越多，执行完所有查询的时间越长。
mysqlslap -a --concurrency=500,10000 --number-of-queries 10000 --iterations=5 --debug-info -uroot -p密码
Average number of seconds to run all queries: 2.916 seconds
平均秒数运行所有查询：2.916秒
Minimum number of seconds to run all queries: 2.742 seconds
最小秒数，运行所有查询：2.742秒
Maximum number of seconds to run all queries: 3.326 seconds
最大秒数运行所有查询：3.326秒
Number of clients running queries: 500
运行查询的客户数：500
Average number of queries per client: 20
每个客户的平均查询数：20
Benchmark
基准
Average number of seconds to run all queries: 3.232 seconds
平均秒数运行所有查询：3.232秒
Minimum number of seconds to run all queries: 3.218 seconds
最小秒数，运行所有查询：3.218秒
Maximum number of seconds to run all queries: 3.271 seconds
最大秒数运行所有查询：3.271秒
Number of clients running queries: 10000
运行查询的客户数：10000
Average number of queries per client: 1
每个客户端的平均查询数：1
User time 27.08, System time 26.60
用户时间27.08，系统时间26.60
2.   普通的sisc硬盘
     mysqlslap -a --concurrency=500,10000 --number-of-queries 10000 --iterations=5 --debug-info -uroot -p密码
   Average number of seconds to run all queries: 7.800 seconds
平均秒数运行所有查询：7.800秒
Minimum number of seconds to run all queries: 6.658 s
最小秒数，运行所有查询：6.658秒
Maximum number of seconds to run all queries: 11.161 seconds
最大秒数运行所有查询：11.161秒
Number of clients running queries: 5000
运行查询的客户数：5000
Average number of queries per client: 2
每个客户的平均查询数：2
可以看出使用ssd比普通的sisc硬盘快了将近2倍以上速度
