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
