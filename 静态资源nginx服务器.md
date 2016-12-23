```
## The static resource nginx server#

server { 
  listen 80; 
  server_name static.cailaobo.com; 
  root /home/html;
  location ~* \.(eot|ttf|woff)$ { add_header Access-Control-Allow-Origin '*'; }
}


```