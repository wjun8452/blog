Shell

docker run -it -v /opt/shared:/opt/shared 



* 查找crash

```shell
$ for f in *-main*gz; do echo $f `gzcat $f| fgrep "Denali-HMI:" | awk '{print $3}'|sort|uniq -c|sort -nk1`; done 

$ for f in *-main*gz; do echo $f.txt `gzcat $f > $f.log`; done
$ grep "pid" ./*.log
```







[grep 命令](https://mp.weixin.qq.com/s/HmqPpOh684bv6IYC3ssqcA)


