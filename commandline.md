Command line
docker run -it -v /opt/shared:/opt/shared 


mac:OneDrive_2019-04-24-2 yf$ for f in *-main*gz; do echo $f `gzcat $f| fgrep "Denali-HMI:" | awk '{print $3}'|sort|uniq -c|sort -nk1`; done 
100-main.log_2019_4_22_19_8_20.gz 122 2035 125 2300 12619 27346
101-main.log_2019_4_22_19_12_31.gz 40 2035 40 2300 14756 27346
102-main.log_2019_4_22_19_17_31.gz 8 2035 30 2300 18635 27346



[grep 命令](https://mp.weixin.qq.com/s/HmqPpOh684bv6IYC3ssqcA)


