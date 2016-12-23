```
server {
 listen 80;
 server_name cailaobo.com;
 rewrite ^/(.*) http://www.cailaobo.com/$1 permanent;
}

```


