# Nginx学习

## 1.概念

Nginx是一个高性能的http/反向代理服务器，Nginx可以支持5w并发。消耗资源低，运行稳定.

## 2.应用场景

1.http服务器，nginx可以提供http服务。可以==做静态网页服务器==

2.虚拟主机，可以实现一台服务器虚拟多个网站。可以实现 不同域名都配置80端口，浏览器使用域名就能访问到网站

3.反向代理，负载均衡。使用nginx将请求根据一定的负载策略分发给多个服务器。



## 3.负载均衡配置

    upstream tomcat-hello{
        server 10.0.0.10:8081;
        server 10.0.0.10:8082;
        server 10.0.0.10:8083;
    }
    
    server {
        listen       80;
        server_name  localhost;
     
        #charset koi8-r;
     
        #access_log  logs/host.access.log  main;
     
        location / {
            #root   html;
            proxy_pass http://tomcat-hello;
            index  index.html index.htm;
        }
    }


## 容器

https://hub.docker.com/_/nginx

docker run --name nginx -v /tmp/nginx_config/nginx.conf:/etc/nginx/nginx.conf:ro -v /tmp/logs/nginx/:/var/log/nginx -p 8080:80 -d nginx:1.18.0

