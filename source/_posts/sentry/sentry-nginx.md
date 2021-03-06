title: sentry-nginx配置
date: 2016-03-01 18:09:53
tags:
---
setry服务使用的nginx配置，sentry默认使用端口是9000，通过nginx映射到这个端口，nginx配置使用https协议，将http访问的永久重定向到https
<!-- more -->
```bash
server {
    listen 80;
    server_name log.sentry.com;
    rewrite ^(.*) https://log.sentry.com$1 permanent;
}

# configuration of the server
server {
    # the port your site will be served on
    listen 443;
    # the domain name it will serve for
    server_name log.sentry.com; # substitute your machine's IP address or FQDN

    ssl on;
    ssl_certificate /home/ubuntu/http_ssl/star_umlife_com/star_umlife_com.full.crt;
    ssl_certificate_key /home/ubuntu/http_ssl/star_umlife_com/star_umlife_com.key;

    gzip on;

    rewrite_log             on;
    charset                 utf8;

    access_log  /home/tlwlmy/log/nginx/log.sentry.com.access.log ;
    #access_log off;
    error_log  /home/tlwlmy/log/nginx/log.sentry.com.error.log;

    proxy_set_header   Host                 $http_host;
    proxy_set_header   X-Real-IP            $remote_addr;
    proxy_set_header   X-Forwarded-For      $proxy_add_x_forwarded_for;
    proxy_set_header   X-Forwarded-Proto    $scheme;
    proxy_redirect     off;

    keepalive_timeout 0;

    #auth_basic "Sentry Log!";
    #auth_basic_user_file /home/tlwlmy/auth/sentry-user;

    location / {
        proxy_pass http://127.0.0.1:9000;
    }
}
```
