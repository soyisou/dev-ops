# 一、nginx常用命令

## 拷贝nginx配置文件
``` 
docker container cp Nginx:/etc/nginx/nginx.conf /app/javapro/dev-ops/nginx/conf
```
## 拷贝nginx的默认配置文件
``` 
docker container cp Nginx:/etc/nginx/conf.d/default.conf /app/javapro/dev-ops/nginx/conf/conf.d
```

## 拷贝html文件
``` 
docker container cp Nginx:/usr/share/nginx/html/index.html /app/javapro/dev-ops/nginx/html
```

```
docker run \
--name Nginx \
-p 80:80 \
-v /app/javapro/dev-ops/nginx/conf/nginx.conf:/etc/nginx/nginx.conf \
-v /app/javapro/dev-ops/nginx/conf/conf.d:/etc/nginx/conf.d \
-v /app/javapro/dev-ops/nginx/html:/usr/share/nginx/html \
-v /app/javapro/dev-ops/nginx/logs:/var/log/nginx \
-v /app/javapro/dev-ops/nginx/ssl:/etc/nginx/ssl \
--privileged=true -d --restart=always nginx


## windows docker nginx映射关系
D:/nginx/conf/nginx.conf:/etc/nginx/nginx.conf
D:/nginx/conf/conf.d:/etc/nginx/conf.d
D:/nginx/html:/usr/share/nginx/html
D:/nginx/logs:/var/log/nginx
D:/nginx/ssl:/etc/nginx/ssl
```

# 二、命令解释
## 2.1 解释代码
```
set $query '';
if ($request_uri ~* "[^\?]+\?(.*)$") {
set $query $1;
}
``` 
``` 
这段代码的作用是从请求的 URI 中提取查询参数，并将其存储在 $query 变量中。让我们通过一个示例来解释这段代码的工作原理：

假设有一个请求的 URI 是 /page?param1=value1&param2=value2，我们希望从中提取查询参数部分。

set $query '';：首先，定义一个名为 $query 的 Nginx 变量，并将其初始化为空字符串。

if ($request_uri ~* "[^\?]+\?(.*)$") {：这是一个条件语句，它检查 $request_uri 变量是否匹配指定的正则表达式。在这个正则表达式中，[^\?]+\?(.*)$ 匹配的是以问号 ? 开头的查询字符串。其中：

[^\?]+ 匹配不包含问号的字符（[^...] 表示不包含某个字符）。
\? 匹配问号字符本身。
(.*)$ 匹配问号后面的所有字符，并将其存储在捕获组中。
set $query $1;：如果前面的条件匹配成功，就会执行这行代码。它将正则表达式捕获的内容（即查询参数部分）存储在 $query 变量中。这里的 $1 表示正则表达式中第一个捕获组的内容，即匹配到的查询参数部分。

综合起来，假设以上的请求 URI 被发送到 Nginx 服务器，经过这段代码处理后，$query 变量将包含 param1=value1&param2=value2 这个字符串，即提取到的查询参数部分。
```