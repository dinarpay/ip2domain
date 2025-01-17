[![Tweet](https://img.shields.io/twitter/url/http/Hktalent3135773.svg?style=social)](https://twitter.com/intent/follow?screen_name=Hktalent3135773) [![Follow on Twitter](https://img.shields.io/twitter/follow/Hktalent3135773.svg?style=social&label=Follow)](https://twitter.com/intent/follow?screen_name=Hktalent3135773) [![GitHub Followers](https://img.shields.io/github/followers/hktalent.svg?style=social&label=Follow)](https://github.com/hktalent/)
# What is
Sometimes, we need to know what connections our local machine has, and what are their IP, domain name, program and parameters?
- get ip to domain
- Know the domian corresponding to the local network connection IP
## How get Local network connection
```
# pid ip domain cmdAndArgs
./getCurNetConn.sh f
```
<img width="726" alt="image" src="https://user-images.githubusercontent.com/18223385/138234250-3ee416cd-d890-4f99-87a4-c4cc85aae8c5.png">

# How install for macos
```bash
brew install mysql tmux
brew services start mysql
brew services list|grep mysql
pip3 install mysql-connector-python scapy pysnooper

ln -s `which python3`  /usr/local/bin/py3
```

## How init mysql
```sql
create database sgdb_51pwn default charset 'utf8';
create user 'sgdb_51pwn'@'%' identified by 'sgdb_51pwn';
grant all on sgdb_51pwn.* to 'sgdb_51pwn'@'%';
flush privileges;

CREATE TABLE `ip2domain` (
  `id1` varchar(100) NOT NULL,
  `id2` varchar(100) NOT NULL,
  KEY `NewTable_id1_IDX` (`id1`) USING BTREE,
  KEY `NewTable_id2_IDX` (`id2`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

```

# How run
```bash
tmux
sudo py3 ip2domain.py

```
## run for centos vps  
```bash
python3 ip2domain2.py
rm -rf ip2d.txt
scp -i ~/.ssh/id_rsa -r -P $myVpsPort root@51pwn.com:/root/ip2d.txt ./
sort -u ip2d.txt|uniq >ip2domain.txt
rm -rf ip2d.txt
mysqlimport -u sgdb_51pwn -psgdb_51pwn --local sgdb_51pwn  `pwd`/ip2domain.txt
rm -rf ip2domain.txt

#  or

mysql -u sgdb_51pwn -psgdb_51pwn
use sgdb_51pwn;
SET GLOBAL local_infile=1;
LOAD DATA LOCAL INFILE '/ip2domain/ip2domain.txt' INTO TABLE ip2domain FIELDS TERMINATED BY ' ' LINES TERMINATED BY '\n';
exit
rm -rf ip2domain.txt
```

# How query ips
```bash
py3 ip2d4query.py -i 52.35.195.250,17.57.145.167
```
## Know the domian corresponding to the local network connection IP
```bash
./getCurNetConn.sh f|awk '{print $2}'|xargs -I % py3 ip2d4query.py -i %
# Now you can see: 
# pid ip domain cmd & args
./getCurNetConn.sh f
```

# other
```
cat ~/MyWork/ip2region/data/ip.merge.txt|grep 泰国|sed -E 's/\|泰国.*//g'|sed -E 's/\|/\-/g'>taiguo.txt
cat ~/MyWork/ip2region/data/ip.merge.txt|grep 日本|sed -E 's/\|日本.*//g'|sed -E 's/\|/\-/g'>reben.txt
cat ~/MyWork/ip2region/data/ip.merge.txt|grep 美国|sed -E 's/\|美国.*//g'|sed -E 's/\|/\-/g'>meiguo.txt

masscan -iL taiguo.txt --max-rate 30000 -p0-65535 -oX taiguo.xml
masscan -iL meiguo.txt --max-rate 10000 -p0-65535 -oX meiguo.xml

```
<!--
https://github.com/metowolf/iplist/blob/master/docs/cncity.md
http://ip.soshoulu.com/shengshiip.aspx
-->



#### 比masscan更快的扫描器
```
alias rustscan1='docker run -it --rm --name rustscan rustscan/rustscan:latest rustscan'
brew install rustscan
```
#### 找许多免费代理
```
proxybroker find --types HTTP HTTPS --lvl High --countries CN --strict -l 1000 --outfile ./proxiesCN.txt
proxybroker find --types HTTP HTTPS --lvl High --countries US --strict -l 1000 --outfile ./proxies.txt
```