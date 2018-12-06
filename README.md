# nginx
nginx container for use with https://letsencrypt.org

### Start nginx container
start_nginx.sh
  ```
  #!/bin/bash
  docker run -d --name nginx \
              -v /path/for/nginx/config:/etc/nginx \
              -v /path/for/challenges:/data/letsencrypt \
              -v /path/for/certs:/etc/letsencrypt \
              -p 443:443 -p 80:80 \
              --restart=always \
              havnfun/nginx      
  ```

### Run certbot daily from cron
certbot.sh
  ```
  #!/bin/bash
  docker run -t --rm \
        -v /path/for/challenges:/data/letsencrypt \
        -v /path/for/certs:/etc/letsencrypt \
        -v /path/for/logs:/var/log/letsencrypt \
        certbot/certbot \
        renew \
        --webroot --webroot-path=/data/letsencrypt
  docker kill -s HUP nginx >/dev/null 2>&1
  ```
