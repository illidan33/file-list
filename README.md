# file-list

A tool to beautify directory index of nginx/apache.

美化nginx/apache目录索引的工具，集成了video-js，替换了h5默认video的播放控制，适配了手机端和电脑端。局域网开启apache/nginx默认目录之后，可以通过内网访问，浏览局域网内服务器的视频和图片，如果是压缩包或者mkv/avi等浏览器不能识别的文件和视频，不会被播放，只会触发浏览器默认操作，如chrome会下载不能识别的文件到本地。

# install/安装

建议windows系统带有中文的路径目录，使用apache开启目录索引，否则不能使用，nginx暂时不支持windows的中文路径访问。

注意：apache和nginx配置目录索引只需要选择一个配置。

### 1. 打开apache的目录索引

以下配置中的"E:/video"为举例的路径，可以根据需求修改。

1. apache（建议windows系统并且目录带中文路径的使用apache）。
apache 的目录索引样式用的mod_autoindex模块 一般默认为开启状态 
找到httpd.conf文件，查找下面的内容 如果有#号注释则去掉，没有这句话就补上去:LoadModule autoindex_module modules/mod_autoindex.so

2. 配置访问权限，开启目录索引。
```
// httpd.conf修改配置
DocumentRoot "E:/video"
<Directory "E:/video">
    Options Indexes FollowSymLinks // 开启目录所有
    AllowOverride  None
    Order allow,deny
    Allow from all // 配置访问权限
</Directory>

Listen 80 // 配置监听端口（不需要配置serverName）
```

### 1. 打开nginx的目录索引

1. 修改nginx.conf配置
```
server {
	listen       80;
	
	#自动显示目录
	location   / {
		root   E:/video;
		autoindex on;
		autoindex_exact_size off;
		autoindex_localtime on;
	}
}
```
2. 另外两个配置如下：
```
autoindex on; 
# 开启目录索引
autoindex_exact_size on;
# 默认为 on，以 bytes 为单位显示文件大小；
# 切换为 off 后，以可读的方式显示文件大小，单位为 KB、MB 或者 GB。
autoindex_localtime on;
# 默认为 off，以 GMT 时间作为显示的文件时间；
# 切换为 on 后，以服务器的文件时间作为显示的文件时间。
```
### 2. 下载html文件

1. 开启apache/nginx任意一个目录索引功能之后，启动apache/nginx（不要在video目录放置index.html/index.htm等默认首页文件）。
2. 把当前项目的include目录和list.html文件放入你想要分享的video目录。
3. 启动apache或者nginx，访问localhost/list.html。
4. 如果是局域网其他电脑/手机访问 ip/list.html。

### 3. 配置隐藏显示目录或者文件(可省略)

修改list.html文件变量
```
const exceptDirOrFile = [
            "include/", // 目录后面带'/'，不带则是文件
        ];
```

### 4. 访问链接地址

```
// 比如
http://localhost/file-list/
// 或者
http://ip:port/file-list/
```

### 效果如下：
![image](https://github.com/illidan33/file-list/blob/master/show%20(2).jpg)
![image](https://github.com/illidan33/file-list/blob/master/video_show.jpg)
