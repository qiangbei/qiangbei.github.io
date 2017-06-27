
###  命中规则如下所示：
06/26/2017-20:13:48.873364  [**] [1:2014702:9] ET DNS Non-DNS or Non-Compliant DNS traffic on DNS port Opcode 8 through 15 set [**] [Classification: Potential Corporate Privacy Violation] [Priority: 1] {UDP} 172.14.20.17:53518 -> 172.14.30.27:53

06/26/2017-20:13:49.882497  [**] [1:2101948:8] GPL DNS zone transfer UDP [**] [Classification: Attempted Information Leak] [Priority: 2] {UDP} 172.14.20.17:19077 -> 172.14.30.27:53

06/26/2017-22:12:27.656601  [**] [1:2013028:4] ET POLICY curl User-Agent Outbound [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 172.14.20.17:45825 -> 172.14.30.27:80

06/26/2017-22:17:49.446865  [**] [1:2014701:12] ET DNS Non-DNS or Non-Compliant DNS traffic on DNS port Opcode 6 or 7 set [**] [Classification: Potential Corporate Privacy Violation] [Priority: 1] {UDP} 172.14.20.17:62496 -> 172.14.30.27:53

06/26/2017-20:18:49.447825  [**] [1:2101948:8] GPL DNS zone transfer UDP [**] [Classification: Attempted Information Leak] [Priority: 2] {UDP} 172.14.20.17:19077 -> 172.14.30.27:53


### 需求：
提取命中的所有规则，统计不同规则命中的次数。以及总的命中规则数。（去除重复）

### 去除重复的行，进行统计，如下：

需要提取第3列中字段。其格式[gid:sid:rev]

awk '{print $3}' fast.log.bk > fast.log.sidgroup

awk -F":" '{print $2}' fast.log.sidgroup  > fast.log.sid

sort  fast.log.sid | uniq -c  >> fast.log.sid.uniq

wc -l fast.log.sid.uniq

此处给予记录。方便使用
