# Simple docker image of Tengine web server based on Alpine #
***

- [more about Tengine](http://tengine.taobao.org)
- [docs](http://tengine.taobao.org/documentation.html)

in this image added [Upstream check module](http://tengine.taobao.org/document/http_upstream_check.html)

to start just type something like that:
```
docker exec -it -d -v example.com.conf:/etc/nginx/conf.d/example.com.conf \
    -p "80:80" -p 443:443 axizdkr/tengine
```
or if you want rewrite nginx.conf you can type something like that:

```
docker exec -it -d -v example.com.conf:/etc/nginx/conf.d/example.com.conf \
    -v nginx.conf:/etc/nginx/nginx.conf \
    -p "80:80" -p 443:443 axizdkr/tengine
```

[example of conf see on github](https://github.com/Axizdkr/tengine)


## add nginx-module-vts

Modify the file `/etc/nginx/nginx.conf` Make it directly access through the IP
```bash
    vhost_traffic_status_zone;
    server {
        listen 80;
        server_name 192.168.0.123;
        location /status {
            vhost_traffic_status_display;
            vhost_traffic_status_display_format html;
        }
    }
```