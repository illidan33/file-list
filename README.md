# file-list

A tool to beautify directory index of nginx/apache.

美化nginx/apache目录索引的工具，集成了video-js，替换了h5默认video的播放控制。

# install/安装

建议windows系统带有中文的路径目录，使用apache开启目录索引。

### 打开apache的目录索引

1. apache（建议windows系统并且目录带中文路径的使用apache）。
apache 的目录索引样式用的mod_autoindex模块 一般默认为开启状态 
找到httpd.conf文件，查找下面的内容 如果有#号注释则去掉，没有这句话就补上去:LoadModule autoindex_module modules/mod_autoindex.so

2. 配置访问权限，开启目录索引。
```
<Directory />
    Options Indexes FollowSymLinks
    AllowOverride  None
    Order allow,deny
    Allow from all
</Directory>
```

### 打开nginx的目录索引

1. 只需要打开 nginx.conf 或者对应的虚拟主机配置文件，在 server 或 location 段里面中上 autoindex on; 
2. 另外两个配置如下：
```
autoindex_exact_size on;
# 默认为 on，以 bytes 为单位显示文件大小；
# 切换为 off 后，以可读的方式显示文件大小，单位为 KB、MB 或者 GB。
autoindex_localtime on;
# 默认为 off，以 GMT 时间作为显示的文件时间；
# 切换为 on 后，以服务器的文件时间作为显示的文件时间。
```
