Shell

docker run -it -v /opt/shared:/opt/shared 

* sed查找替换

```
 //处理所有json文件，将"font_face" : "MyriadPro-Regular", 替换成"font_face" : "GMSansUI_Global", 源文件备份为.bak
 sed -i .bak -E 's/("font_face" : )(".*")/\1"GMSansUI_Global"/g' ./*.json
 
```



* 查找crash

```shell
$ for f in *-main*gz; do echo $f `gzcat $f| fgrep "Denali-HMI:" | awk '{print $3}'|sort|uniq -c|sort -nk1`; done 

$ for f in *-main*gz; do echo $f.txt `gzcat $f > $f.log`; done
$ grep "pid" ./*.log
```



* 删除当前目录下30天前的旧文件

```shell
find . -mtime +30 -exec rm -rf {} \;
```





* 查找过期的branch

  ```
  git branch -r --sort=committerdate --format='%(HEAD) %(color:yellow)%(refname:short)%(color:reset)|%(color:red)%(objectname:short)%(color:reset)|%(contents:subject)|%(authoremail)|%(color:green)%(committerdate:short)%(color:reset)' | grep -v -E  '/master/|/release/' | grep -E '2018-|2019-01|2019-02|2019-03|2019-04|2019-05' | wc -l
       
  704
  ```

* 将上述branch的创建者邮件转化成一行，可以直接粘贴发送邮件给他们哦

  ```
  git branch -r --sort=committerdate --format='%(HEAD) %(color:yellow)%(refname:short)%(color:reset)|%(color:red)%(objectname:short)%(color:reset)|%(contents:subject)|%(author)|%(color:green)%(committerdate:short)%(color:reset)' | grep -v -E  '/master|/release|/HEAD' | grep -E '2018-|2019-01|2019-02|2019-03|2019-04|2019-05' | cut -d\| -f 4 | cut -d\< -f 2 | cut -d\> -f 1 | sort | uniq | tr '\n' ';'
  
  alpap@telenav.com;andrewc@telenav.com;andreyl@telenav.com;arpits@telenav.com;azhwang@telenav.cn;bbli@telenav.cn;bdgong@telenav.cn;bfzhang@telenav.cn;
  ```

* 列出过期的branch

  ```
   //删除远端已经不存在的本地分支
   git remote prune origin
   
   git branch -r --sort=committerdate --format='%(HEAD) %(color:yellow)%(refname:short)%(color:reset)|%(color:red)%(objectname:short)%(color:reset)|%(contents:subject)|%(authoremail)|%(color:green)%(committerdate:short)%(color:reset)' | grep -v -E  '/master|/release|/HEAD' | grep -E '2018-|2019-01|2019-02|2019-03|2019-04|2019-05' | cut -d\| -f 1 | sed 's/origin\///' > branches.txt
   
  ```

  

* 过滤掉需要保留的branch

  ```
  //filter.txt行首添加空格
  sed 's/^/  &/g' filter.txt > filter2.txt
  sort branches.txt filter2.txt filter2.txt | uniq -u > result.txt
  
  //应该没有输出，如果有输出则表明希望被keep的仍然出现在了待删除列表
  sort filter2.txt result.txt | uniq -d
  ```

* 最后再执行删除

  ```
  cat result.txt | xargs git push origin --delete
  ```

  

[grep 命令](https://mp.weixin.qq.com/s/HmqPpOh684bv6IYC3ssqcA)


