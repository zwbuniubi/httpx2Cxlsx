#  httpx+naabu+nuclei大量资产极速漏扫

原创  二仙桥施工队  [ 戟星安全实验室 ](javascript:void\(0\);)

**戟星安全实验室**

微信号  gh_0a430ebdb179

功能介绍  忆享科技旗下高端的网络安全攻防服务团队.安服内容包括渗透测试、代码审计、应急响应、漏洞研究、威胁情报、安全运维、攻防演练等

__ __

__ _ _

![](https://mmbiz.qpic.cn/mmbiz_png/SE49V9dKJrxvMzibXUdvEsJgsmtFMRdGdIozdib3BWMEJ7X9FB2yjr1dYc54LU1LJKbIMKicSNknD2LMSpDdjre6w/640?wx_fmt=png)

破军安全实验室

  

忆享科技旗下高端的网络安全攻防服务团队.安服内容包括渗透测试、代码审计、应急响应、漏洞研究、威胁情报、安全运维、攻防演练等  

本文约2700字，阅读约需7分钟。

  

  
  

0x00 前言

  

某群老哥介绍的  go  语言三件套，针对上万资产快速漏扫组合，都是  github  上同作者的开源工具，可以魔改

#  

  
  

0x01 httpx

  

##  ** 下载  **

源码地址，  github  上  2.3k  的工具

  * 

    
    
    https://github.com/projectdiscovery/httpx

  

![](https://mmbiz.qpic.cn/mmbiz_png/SE49V9dKJrx0oCVnY24QlpF278JHMibKTuxicAN41qaoUwR8HMc7siacHg8OAGxUN9d1ybRJuG1JbHNpNMAnFyGTA/640?wx_fmt=png)

  

##  ** 参数  **

三个工具作者都是  projectdiscovery.io  ，参数都是按模块分类的，使用时按模块选择参数就行，简洁明了，这里只说一下输出配置

  

![](https://mmbiz.qpic.cn/mmbiz_png/SE49V9dKJrx0oCVnY24QlpF278JHMibKTHIy2oDHKsYtUvZ4bJFZOC9XHZPKUSHriawicZhhWBXF0TBLhcnSgE1Cg/640?wx_fmt=png)

  

看输出模块，使用  -o output.txt  将结果输出到文件，使用  -csv  、  json  可指定便于程序处理的格式，但是会导致  cmd
窗口输出没有颜色，而且内容不友好，  -sr  、  srd  会将服务器响应保存到程序同级目录下，  txt  格式

  

![](https://mmbiz.qpic.cn/mmbiz_png/SE49V9dKJrx0oCVnY24QlpF278JHMibKTXrmHDWS2eicTkmL4V5SbpG4AyywhQYGRL4cUGWG5EVQkAJRdF8kzzCg/640?wx_fmt=png)

  

使用  -csv

  

![](https://mmbiz.qpic.cn/mmbiz_png/SE49V9dKJrx0oCVnY24QlpF278JHMibKTldicqUeMZwqUCSUt1TY1q1JtgwuyDN4IsMvsErIRTJECPuG2iacx7bicQ/640?wx_fmt=png)

  

使用  -json

  

![](https://mmbiz.qpic.cn/mmbiz_png/SE49V9dKJrx0oCVnY24QlpF278JHMibKTatAp3wuftBxxmuWoJD3ZrpmfZauujXKeRygMcd3Hjq94mPB6L2NpIA/640?wx_fmt=png)

  

另一个是  debug  模块，  -nc  去除  cmd  颜色输出，只有黑白，  -debug  可以看更多输出

  

![](https://mmbiz.qpic.cn/mmbiz_png/SE49V9dKJrx0oCVnY24QlpF278JHMibKTwsISfuS5FicWBBfTIZzZKGzcx7GGaz2tBv69em4j5icFKkgwnjZ1iaxDA/640?wx_fmt=png)

  

##  ** 使用  **

对百度收集的目标进行测试，常规的域名扫描，会自动探测  http  、  https  协议（有回滚机制只会保留一个，使用  -nf  参数保留两种协议）

  * 

    
    
    httpx.exe -l test.txt -sc -td -cl -method-server -title -cdn -probe -fr -nf

  

![](https://mmbiz.qpic.cn/mmbiz_png/SE49V9dKJrx0oCVnY24QlpF278JHMibKTtibicXibsExiaLDeC2v2oVOAgfibpAVFaiaicB6zR7sR5Q4TGHiaIVPtmbiagBA/640?wx_fmt=png)

  

使用  ctrl+c  终止扫描后会生成  resume.cfg

  * 

    
    
    httpx.exe -l domains.txt -sc -td -cl-method -server -title -cdn -probe -fr -nf -o ouput.txt

  

![](https://mmbiz.qpic.cn/mmbiz_png/SE49V9dKJrx0oCVnY24QlpF278JHMibKTxmfzlCxRkHvFiaLsC7nCtq8dCv4wpa8ZHa0lVM6WGcHny6LBagsS5Eg/640?wx_fmt=png)

  

挺不错的一个功能，会记录扫描进度，下次可加载  cfg  文件继续扫描

  

![](https://mmbiz.qpic.cn/mmbiz_png/SE49V9dKJrx0oCVnY24QlpF278JHMibKT1VaAxp7jEC21EI57YnhPo9Xqy9y06zicEyTTQLqyibsaeDlXSLicJH4Yg/640?wx_fmt=png)

  

自己写了一个小脚本

  * 

    
    
    https://github.com/moyuwa/httpx2Cxlsx

将  cmder  输出的内容带色彩转换到  xlsx  表格，以便快速梳理资产

  

![](https://mmbiz.qpic.cn/mmbiz_png/SE49V9dKJrx0oCVnY24QlpF278JHMibKTPiaIJWib58DcAicdNd0oDZllsC6VAibcOFL2OD4kdvSibaauCuvpuGd7wyg/640?wx_fmt=png)

  

另一个实用功能，使用  -path  参数带  url  路径探测，如下探测“用友  oa  信息泄露”，使用  -mc 200  匹配响应为  200
的，比较敏感截图就不放了

  * 

    
    
    httpx.exe -l oa.txt -path"/yyoa/ext/https/getSessionList.jsp?cmd=getAll" -sc -td -cl -method-server -title -cdn -probe -fr -nf -mc 200 -csv -o oa.csv

#  

  
  

0x02 nuclei

  

##  ** 下载  **

源码地址，  github  上  5.6k stars  的工具，不多说

  * 

    
    
    https://github.com/projectdiscovery/nuclei

  

![](https://mmbiz.qpic.cn/mmbiz_png/SE49V9dKJrx0oCVnY24QlpF278JHMibKTWJuznmgxJgLybwODdeCaZHnKaLCSHqOb9a4jYZLKJK8Tx7s5ohoAIg/640?wx_fmt=png)

  

漏洞模版地址，运行程序自动下载的漏洞模版就是来自这里

  * 

    
    
    https://github.com/projectdiscovery/nuclei-templates

  

![](https://mmbiz.qpic.cn/mmbiz_png/SE49V9dKJrx0oCVnY24QlpF278JHMibKTGMRSoUOwefe06FxBpULMMNDGPp07lXGgib89fqfTkbCOicCVsfGZtQ5g/640?wx_fmt=png)

  

模版编辑手册

  * 

    
    
    https://nuclei.projectdiscovery.io/templating-guide/

##  

![](https://mmbiz.qpic.cn/mmbiz_png/SE49V9dKJrx0oCVnY24QlpF278JHMibKTw81OQsjy8kNJFib9VSqvicibomV1rqaRktOLCjmsZBbjpibrIfVr8hFYsQ/640?wx_fmt=png)

  

##  ** 配置信息  **

分析源码  main.go

  

![](https://mmbiz.qpic.cn/mmbiz_png/SE49V9dKJrx0oCVnY24QlpF278JHMibKTSlrXqCHukS0Q61KCTgHiaMhibPMp3d5IViaczNSHC8G8pBQk2ePoeNDTQ/640?wx_fmt=png)

  

配置文件地址和扫描模版保存路径

  

![](https://mmbiz.qpic.cn/mmbiz_png/SE49V9dKJrx0oCVnY24QlpF278JHMibKTaIgfKesFQB07FCS2r9LXx6AEzvjKWQiaP9IubaibHyrfNqXtyFfKIKvQ/640?wx_fmt=png)

  

![](https://mmbiz.qpic.cn/mmbiz_png/SE49V9dKJrx0oCVnY24QlpF278JHMibKTITibWckfG557HltgQO2Vy2ic2PJia8r0xKycRxtacH64C5sGiahGIKXGsQ/640?wx_fmt=png)

  

扫描模版保存路径

  

![](https://mmbiz.qpic.cn/mmbiz_png/SE49V9dKJrx0oCVnY24QlpF278JHMibKTukhQ9ricrhxGiaokxNjtqtlJbuvKpuOFp8NNI7K8uTwXqRrXRGsp8yvA/640?wx_fmt=png)

  

##  ** 使用  **

命令参数与  httpx  类似，都是按模块选择，就不细说了

直接运行程序，会自动释放配置文件，下载扫描模版（无法下载可以参考前面的分析，通过浏览器下载模版文件，直接放到对应目录）

  

![](https://mmbiz.qpic.cn/mmbiz_png/SE49V9dKJrx0oCVnY24QlpF278JHMibKTrnC5QmGIJtHHmZVF4T0cQoKEt049rxzOic16fia2QNNUop8AfHy9AtRA/640?wx_fmt=png)

  

直接执行扫描，会调用全部扫描模版进行探测

  

![](https://mmbiz.qpic.cn/mmbiz_png/SE49V9dKJrx0oCVnY24QlpF278JHMibKTtGZBKIOhLjqGvbcYoPE77lyFIdFIibjsqzoaxmfBRtNQulDcCohUbNQ/640?wx_fmt=png)

  

指定模版扫描，对收集的  thinkphp  目标指定  thinkphp-5023-rce  漏洞模版，设置线程数为  100  ，没用漏洞则无任何输出

  * 

    
    
    nuclei.exe -l thinkphp.txt -c 100 -tthinkphp-5023-rce.yaml -o thinkphpout.txt

  

![](https://mmbiz.qpic.cn/mmbiz_png/SE49V9dKJrx0oCVnY24QlpF278JHMibKTibjIZhAz0aEFVd5BL4iaZoOxzo1HIq16cUK8HY2myR4HflSSbscylRuQ/640?wx_fmt=png)

  

另一个常用命令  -s  指定漏洞等级（  info, low, medium, high, critical  ），如下只探测高危和严重类型的漏洞，
2800-  个模版只加载了  1027  个，总计  7w  个请求

  * 

    
    
    nuclei.exe -l wwwschool.txt -shigh,critical -nc -c 100 -o wwwschoolout.txt

#  

![](https://mmbiz.qpic.cn/mmbiz_png/SE49V9dKJrx0oCVnY24QlpF278JHMibKTAF9ogeYUT4odDN9arWZ9UO5Aax4ecbOicYRkztffnBUDZ5rGbIeW9gA/640?wx_fmt=png)

#  

#  

  
  

0x03 naabu

  

##  下载

同样  github  上  1.6k  工具

  * 

    
    
    https://github.com/projectdiscovery/naabu

  

![](https://mmbiz.qpic.cn/mmbiz_png/SE49V9dKJrx0oCVnY24QlpF278JHMibKTYPUb45rkHJng19gCP8mmwe5ic2dVHhNXgfhNV2wSnqgbGKzPeBEZ5kw/640?wx_fmt=png)

  

针对主机端口扫描，可以看作  masscan  的加强版

通过魔改加入  nmap  的服务指纹对端口进行服务识别食用更佳，默认使用  syn  扫描，使用  -verify  参数会对发现的端口  tcp
连接确认，可以在这里加

##  

##  ** 使用  **

常用快速扫描  naabu.exe -l test.txt -c 100

  

![](https://mmbiz.qpic.cn/mmbiz_png/SE49V9dKJrx0oCVnY24QlpF278JHMibKT5nyp5EKxCBL1yNQ10GQjkA4HYOmtxmJUHEztgtodlH3WGhtMctyUXA/640?wx_fmt=png)

  

居然没探测出  443  ，使用  -p  指定端口扫描

  

![](https://mmbiz.qpic.cn/mmbiz_png/SE49V9dKJrx0oCVnY24QlpF278JHMibKTNcm7d25yicKPB2wYztVTza8g4b9UTzCTRyWq9vf9oGMZNLBl591ibaxw/640?wx_fmt=png)

  

使用  -tp  参数测试  nmap  常用端口  1000  （默认是  top 100  ），网络不佳的确会出现遗漏端口的情况

  * 

    
    
    naabu.exe -l test.txt -c 100 -tp 1000

  

![](https://mmbiz.qpic.cn/mmbiz_png/SE49V9dKJrx0oCVnY24QlpF278JHMibKTWnyPdzeuTOhReQzF28Qx6Y1utqOAZibZr9yTYf8ZQ9wPR60xlcwgN2Q/640?wx_fmt=png)

  

比起同类  cmd  工具优势是有格式化输出，但依旧不推荐

#  

  
  

0x04 使用体会

  

httpx+nuclei  可实现快速  web  漏扫，最适合指定漏洞进行批量排查

naabu  更类似  masscan  对内网进行端口发现，虽然可使用  -nmap-cli  参数联动  nmap  ，但我从不这么用  :)

几个常用的命令

  *   *   *   *   *   *   *   *   * 

    
    
    httpx.exe -l domains-sc -td -cl -method-server -title -cdn -probe -fr -nf -o out1.csvhttpx.exe -l oa.txt -path"/yyoa/ext/https/getSessionList.jsp?cmd=getAll" -sc -td -cl -method-server -title -cdn -probe -fr -nf -mc 200 -csv -o oa.csv nuclei.exe -l thinkphp.txt -c 100 -tthinkphp-5023-rce.yaml -o thinkphpout.txtnuclei.exe -l wwwschool.txt -shigh,critical -nc -c 100 -o wwwschool.txt naabu.exe -l test.txtnaabu.exe -l test.txt -p21-25,80-90,443,445,3306,3389,8080-8090 -c 100naabu.exe -l test.txt -c 100 -tp 1000

  
  

  

  

  

  

  

声明

由于传播、利用此文所提供的信息而造成的任何直接或者间接的后果及损失，均由使用者本人负责，破军安全实验室及文章作者不为此承担任何责任。

破军安全实验室拥有对此文章的修改和解释权。如欲转载或传播此文章，必须保证此文章的完整性，包括版权声明等全部内容。未经破军安全实验室允许，不得任意修改或者增减此文章内容，不得以任何方式将其用于商业目的。

  

![](https://mmbiz.qpic.cn/mmbiz_jpg/SE49V9dKJrxvMzibXUdvEsJgsmtFMRdGd4zMdyFHhO32AIibkopcibUOnzYiabroHE01ayHqlu5ZNfAXuSlYj2et2Q/640?wx_fmt=jpeg)

破军安全实验室

# 长按二维码 关注我们 #

  

  

预览时标签不可点

微信扫一扫  
关注该公众号

继续滑动看下一个

#  httpx+naabu+nuclei大量资产极速漏扫

原创  二仙桥施工队  [ 戟星安全实验室 ](javascript:void\(0\);)

轻触阅读原文

![](http://mmbiz.qpic.cn/mmbiz_png/SE49V9dKJrynhicSC9oWDibJEW3BUhEIWMXibjk8hKo5DnaVTgxKSYpOegTsLLqF9jURAHicGXBLN9YyNaGmP6Vu8g/0?wx_fmt=png)

戟星安全实验室

赞  分享  在看

向上滑动看下一个

[ 知道了 ](javascript:;)

微信扫一扫  
使用小程序

****

[ 取消 ](javascript:void\(0\);) [ 允许 ](javascript:void\(0\);)

****

[ 取消 ](javascript:void\(0\);) [ 允许 ](javascript:void\(0\);)

：  ，  。  视频  小程序  赞  ，轻点两下取消赞  在看  ，轻点两下取消在看  分享  留言

