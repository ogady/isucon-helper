# alpの使い方

## install

```sh
$wget https://github.com/tkuchiki/alp/releases/download/v1.0.7/alp_linux_amd64.zip
$unzip alp_linux_amd64.zip
$sudo install alp /usr/local/bin/alp
```

## nginx alp ltsv用config

```
user  www-data;
worker_processes  auto;

error_log  /var/log/nginx/error.log warn;
pid        /run/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

<!-- 略 -->

  log_format ltsv "time:$time_local"
    "\thost:$remote_addr"
    "\tforwardedfor:$http_x_forwarded_for"
    "\treq:$request"
    "\tmethod:$request_method"
    "\turi:$request_uri"
    "\tstatus:$status"
    "\tsize:$body_bytes_sent"
    "\treferer:$http_referer"
    "\tua:$http_user_agent"
    "\treqtime:$request_time"
    "\truntime:$upstream_http_x_runtime"
    "\tapptime:$upstream_response_time"
    "\tcache:$upstream_http_x_cache"
    "\tvhost:$host";

  access_log  /var/log/nginx/access.log ltsv;

<!-- 略 -->
}
```

## 基本的な使い方

[zenn-alpの使い方(基本編)](https://zenn.dev/tkuchiki/articles/how-to-use-alp)

```sh
#　降順で表示(-r)
$sudo cat /var/log/nginx/access.log | alp ltsv -r

# 正規表現にマッチしたURIをひとつのURIとして集計する(-m)
$sudo cat /var/log/nginx/access.log | alp ltsv -r -m '/api/hoge/[0-9]+,/api/fuga/[0-9]+'

# queryストリングまでみたい場合(-q)
$sudo cat /var/log/nginx/access.log | alp ltsv -r -q -m '/api/hoge/[0-9]+,/api/fuga/[0-9]+'
```
