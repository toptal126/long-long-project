# Configure FrontEnd (React/Typescript)

```
server {

        root /var/www/tezoscollect.io/html;
        index index.html index.htm index.nginx-debian.html;

        server_name tezoscollect.io www.tezoscollect.io;

        location / {
                try_files $uri /index.html;
        }

    listen [::]:443 ssl ipv6only=on; # managed by Certbot
    listen 443 ssl; # managed by Certbot
    ssl_certificate /etc/letsencrypt/live/tezoscollect.io/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/tezoscollect.io/privkey.pem; # managed by Certbot
    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot


}
server {
    if ($host = www.tezoscollect.io) {
        return 301 https://$host$request_uri;
    } # managed by Certbot


    if ($host = tezoscollect.io) {
        return 301 https://$host$request_uri;
    } # managed by Certbot


        listen 80 default_server;
        listen [::]:80 default_server;

        server_name tezoscollect.io www.tezoscollect.io;
    return 404; # managed by Certbot
}
```

# Configure Server (Nest.js/Typescript PM2 Redirect port 4000)

```
server {
    server_name api1.tezoscollect.io; # managed by Certbot

    listen [::]:443 ssl; # managed by Certbot
    listen 443 ssl; # managed by Certbot
    ssl_certificate /etc/letsencrypt/live/api1.tezoscollect.io/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/api1.tezoscollect.io/privkey.pem; # managed by Certbot
    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot


    location / {
        proxy_pass http://localhost:4000;
    }
}
server {
    if ($host = api1.tezoscollect.io) {
        return 301 https://$host$request_uri;
    } # managed by Certbot
        listen 80 ;
        listen [::]:80 ;
    server_name api1.tezoscollect.io;
    return 404; # managed by Certbot
}
```
