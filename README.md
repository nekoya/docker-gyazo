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

## backup images to Amazon S3

This image contains awscli.

- http://aws.amazon.com/jp/cli/

```
sudo docker run -d -p 8080:80 \
    -e AWS_ACCESS_KEY_ID={YOUR_ACCESS_KEY} \
    -e AWS_SECRET_ACCESS_KEY={YOUR_SECRET_ACCESS} \
    -e GYAZO_HOST=https://gyazo.example.com \
    --name gyazo nekoya/gyazo
```

```
sudo docker exec -it gyazo aws s3 sync /opt/gyazo s3://{BACKUP_BUCKET}
```
