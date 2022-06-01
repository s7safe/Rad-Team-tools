# 总结红队作战工具

subfinder  https://github.com/projectdiscovery/subfinder  //子域名获取

httpx  https://github.com/projectdiscovery/httpx  //存活验证

anew   https://github.com/tomnomnom/anew  //去重对比


subfinder -silent -dL domain.txt | anew domians.txt | httpx -title -tech-detect -status-code  -csv  //获取子域名，对比文件，验证存活


gau   https://github.com/lc/gau    // 获取网站以前的路径

hakrawler https://github.com/hakluke/hakrawler  // 获取网站以前的路径(工具链平替)


针对单一网站与文件，调用命令进行打点


echo domain.com  | gau  --blacklist  png,jpg,gif,html,eot,svg,woff,woff2  | httpx -title -tech-detect -status-code

cat domian.txt  | gau  --blacklist  png,jpg,gif,html,eot,svg,woff,woff2  | httpx -title -tech-detect -status-code  -csv  

