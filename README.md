# 总结红队作战工具

**//子域名获取**

subdomain3 https://github.com/yanxiu0614/subdomain3/blob/master/README_ZH.md 

subfinder  https://github.com/projectdiscovery/subfinder 

**//存活验证**

httpx  https://github.com/projectdiscovery/httpx  

**//去重对比**

anew   https://github.com/tomnomnom/anew  

**//获取子域名，对比文件，验证存活**

subfinder -silent -dL domain.txt | anew domians.txt | httpx -title -tech-detect -status-code  -csv  

**网站历史URL获取**

**gau**   https://github.com/lc/gau  

**hakrawler** https://github.com/hakluke/hakrawler  

**waybackurls** https://github.com/tomnomnom/waybackurls



**针对单一网站与文件，调用命令进行打点**


echo domain.com  | gau  --blacklist  png,jpg,gif,html,eot,svg,woff,woff2  | httpx -title -tech-detect -status-code

cat domian.txt  | gau  --blacklist  png,jpg,gif,html,eot,svg,woff,woff2  | httpx -title -tech-detect -status-code 



**针对JS进行提取敏感字段**
https://github.com/machinexa2/Nemesis

**或许你需要一些命令**
cat livejs.txt | grep dev
cat livejs.txt | grep app
cat livejs.txt | grep static



提取器

提取JS命令

https://github.com/tomnomnom/fff
cat jslist.txt | fff | grep 200 | cut -d “ “ -f1 | tee livejs.txt

想法来自@Ratnadip Gajbhiye



**目录FUZZ扫描**
https://github.com/ffuf/ffuf




对UEL进行处理
https://github.com/tomnomnom/gf


隐藏参数枚举
https://github.com/s0md3v/Arjun

**XRAY 命令行批量扫描**

针对单个域名进行子域名爆破，使用GAU提取链接，httpx验证存活，推送到XRAY进行爬虫扫描。

subfinder -d domain.com -silent | gau  --blacklist  png,jpg,gif,html,eot,svg,woff,woff2  | httpx -o 200.txt

for i in $(cat 200.txt);do echo "xray scanning $i" ; ./xray webscan --browser-crawler  $i --html-output vuln.html; done



**XSS扫描**

https://github.com/hahwul/dalfox

 cat url.txt | hakrawler -subs |grep -v key | grep key |grep -v google | grep = | dalfox pipe --silence --skip-bav 


**端口扫描**
https://github.com/projectdiscovery/naabu

**批量目录扫描**
https://github.com/H4ckForJob/dirmap
持续更新





