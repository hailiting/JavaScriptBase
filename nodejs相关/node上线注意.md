## Nginx反向代理与负载均衡.md
### HTTP Upstrean 模块
nginx -t
nginx -c
~~~
http{
  upstream firsttest{
    server 192.168.0.21
    server 192.168.0.31
  }
  server{
    listen 8080;
    location / {
      proxy_pass http://firsttest
    }
  }
}
~~~

#### npm install --production 只管上线环境
#### PM2
