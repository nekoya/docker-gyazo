# Gyazo docker container

## run the container

```
sudo docker run -d -p 8080:80 \
    -e GYAZO_HOST=https://gyazo.example.com \
    nekoya/gyazo
```

### nginx proxy setting

```
server {
    listen 80;
    listen 443 ssl;
    server_name {GYAZO_HOST};
    access_log  /var/log/nginx/gyazo.log;
    location ~ / {
        proxy_pass http://localhost:8080;
    }
}
```
