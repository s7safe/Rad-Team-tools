# 总结红队作战工具

本列表，收集一些在服务器上运行的一些工具，组件自动化，服务器长期挂跑项目 欢迎提issues，来丰富工作流程，比如自己挖洞时候的一些简易流程，工具+调用命令，
在我的日常渗透中，我发现我重复调用几个工具，但是不同的调用组合渗透的工作流程，有时候调用命令会忘记，所以有了这个列表，来达到帮助我记忆一些流程命令的文档，未来还会细化过程，脚本小子福音了

**//子域名获取**

subdomain3 https://github.com/yanxiu0614/subdomain3/blob/master/README_ZH.md 

subfinder  https://github.com/projectdiscovery/subfinder 



**DNS枚举**
https://github.com/projectdiscovery/dnsx



**端口扫描**
https://github.com/projectdiscovery/naabu



**//存活验证**

httpx  https://github.com/projectdiscovery/httpx  



**批量目录扫描**
https://github.com/H4ckForJob/dirmap

命令行调用命令

```
subfinder -silent -dL domain.txt | dnsx -silent | naabu -top-ports 1000 -silent| httpx -title -tech-detect -status-code

subfinder -d domain.net -silent | ksubdomain e --stdin --silent | naabu -top-ports 1000 -silent

subfinder -silent -dL domain.txt | dnsx -silent | httpx -o output.txt

subfinder -d domain.com -silent

subfinder -silent -dL domain.txt  |  dnsx -silent | httpx -mc 200 -timeout 30 -o output.txt 
```



**//去重对比**

anew   https://github.com/tomnomnom/anew  



**//获取子域名，对比文件，验证存活，达到监听新资产的目的**

```
subfinder -silent -dL domain.txt | anew domians.txt | httpx -title -tech-detect -status-code 
```

**视觉侦查**
https://github.com/sensepost/gowitness

```
gowitness file <urlslist.txt>
```

**网站历史URL获取**

**gau**   https://github.com/lc/gau  

**hakrawler** https://github.com/hakluke/hakrawler  

**waybackurls** https://github.com/tomnomnom/waybackurls

**gospider** https://github.com/jaeles-project/gospider

```
爬虫获取链接，运行20个站点每个站点10个爬虫
gospider -S domain.txt -o output.txt -c 10 -d 1 -t 20

通过爬虫获取链接包含子域名
gospider -s "https://google.com/" -o output -c 10 -d 1 --other-source --include-subs

对文件进行处理过滤出js文件
gospider -S urls.txt | grep js | tee -a js-urls.txt
```



**针对单一网站与文件，调用命令进行打点**

```
echo domain.com  | gau  --blacklist  png,jpg,gif,html,eot,svg,woff,woff2  | httpx -title -tech-detect -status-code

cat domian.txt  | gau  --blacklist  png,jpg,gif,html,eot,svg,woff,woff2  | httpx -title -tech-detect -status-code 

此命令也获取了标题，直接操作httpx即可衔接下一个命令运行工具
```

**针对JS进行提取敏感字段**
https://github.com/machinexa2/Nemesis

**或许你需要一些命令**

```
cat livejs.txt | grep dev
cat livejs.txt | grep app
cat livejs.txt | grep static
```

提取器

提取JS命令  https://github.com/tomnomnom/fff

```
cat jslist.txt | fff | grep 200 | cut -d “ “ -f1 | tee livejs.txt
```

**目录FUZZ扫描**
https://github.com/ffuf/ffuf

对UEL进行提取
https://github.com/tomnomnom/gf

```
cat subdomains.txt | waybackurls | gf xss | qsreplace | tee xss.txt
```




**XRAY 命令行批量扫描**

针对单个域名进行子域名爆破，使用GAU提取链接，httpx验证存活，推送到XRAY进行爬虫扫描。

```
subfinder -d domain.com -silent | gau  --blacklist  png,jpg,gif,html,eot,svg,woff,woff2  | httpx -o 200.txt

for i in $(cat 200.txt);do echo "xray scanning $i" ; ./xray webscan --browser-crawler  $i --html-output vuln.html; done
```

**XSS扫描**

https://github.com/hahwul/dalfox

```
 cat url.txt | hakrawler -subs |grep -v key | grep key |grep -v google | grep = | dalfox pipe --silence --skip-bav 
```





隐藏参数枚举
https://github.com/s0md3v/Arjun

```
单目标扫描
arjun -u https://api.example.com/endpoint
单目标扫描输出
arjun -u https://api.example.com/endpoint -oJ result.json
多目标扫描
arjun -i targets.txt

指定方法
arjun -u https://api.example.com/endpoint -m POST

```

欢迎关注我的公众号 渗透云笔记
持续更新
