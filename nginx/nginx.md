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
```