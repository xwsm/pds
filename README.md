# PDS (Proxy Download Server)
PDS -- Proxy Download Server(代理下载服务器)
- 基于PHP Curl实现代理下载服务器，也可以当作 代理请求服务器、中转服务器、透传服务器
- 支持Get、Post代理请求，支持表单、字符串等请求数据
- 支持透传(转发) User-Agent、Content-Type、Authorization、Cookie
- 基于 CURLOPT_WRITEFUNCTION 实现分片输出，避免大文件崩溃，节约内存，可以做PHP大文件下载
- 支持两种方式传入URL参数的功能，支持调试(Debug)模式
- 支持过滤部分header的功能，示例header数组去掉了 Transfer-Encoding: chunked
- 支持github https代理功能，git clone、git pull 经测试可用，git push尚未支持

两种请求方式 (Two Request):

> ① pds.php?url=http://example.com/

> ② pds.php/u/http://example.com/ （针对Github 代理克隆项目新增传参方式）

调试方式 Debug:

> pds.php?url=http://example.com/&debug=1

Github 代理克隆项目

> 必须要用第二次请求方式，示例命令： git clone pds.php/u/http://example.com/


### 使用场景

##### 1. 代理(透传)下载服务器

![image](https://raw.githubusercontent.com/lyaohe/pds/master/images/proxy-download-file.png)

- 代理下载文件
- 代理克隆git项目
- 爬虫代理

有时候会遇到下载一个文件会特别慢，甚至只有几kb/s，不是存放文件的服务器带宽不足，也不是我网络太慢，而是中间走的网络太差，这时候可以自己部署一台代理(中转)服务器来下载，往往下载速度可以翻10倍以上，简直是天堂与地狱的区别，祝你好运。

##### 2. 简单的云存储架构: 业务服务器 + 存放文件的服务器

 ![image](https://raw.githubusercontent.com/lyaohe/pds/master/images/file-download-server.png)

- 业务服务器：处理客户端(浏览器)的请求，先做业务逻辑处理，例如：安全检查、请求频率检查、日志记录，然后再通过PDS请求文件服务器，返回给客户端
- 存放文件的服务器，可以是多台内网服务器，不用外网IP节省带宽，通过内网，提供Http请求获取文件即可


目前只想到2种场景，你们还想什么场景可以用到，欢迎跟我交流，我来补充分享给大家

使用中，遇到什么问题，欢迎提issue

Email:  lyaohe@gmail.com

### 项目灵感
有一次在Github下载软件安装包，国内网络下载超慢，想到了代理下载，或者用中转服务器来下载快很多，就开始设计和调研，并动手写个代理下载服务。


更新时间: 2017.07.24
