# Setup nginx

## Install
```bash
sudo apt install nginx
```

## Commands

```bash
sudo systemctl stop nginx
sudo systemctl start nginx
sudo systemctl restart nginx
sudo systemctl reload nginx
# Startup
sudo systemctl disable nginx
sudo systemctl enable nginx
```

## Configuration

Create file here
`/etc/nginx/sites-available/my-domain`

Edit file
```bash
server {  
    listen 80;
    server_name www.my-domain my-domain;
    location / {  
            proxy_pass http://localhost:8080;  
            proxy_http_version 1.1;  
            proxy_set_header Upgrade $http_upgrade;  
            proxy_set_header Connection 'upgrade';  
            proxy_set_header Host $host;  
            proxy_cache_bypass $http_upgrade;  
    }  
}
```


Link file
```bash
sudo ln -s /etc/nginx/sites-available/my-domain /etc/nginx/sites-enabled/
```


## Get Let's Encrypt certificate for domain by using nginx plugin

Download plugin
```bash
sudo apt install certbot python3-certbot-nginx
```

Get certificate for YOUR-DOMAIN.com
```bash
sudo certbot --nginx -d YOUR-DOMAIN.com -d www.YOUR-DOMAIN.com
```

Create auto-renewal because certificate is only available for 90 days.
```bash
sudo certbot renew --dry-run
```

