## Install Linux-lts

   
## 1. Install docker
```
sudo su
masukin password
systemctl enable docker
systemctl start docker
systemctl status docker
```
## 2. Install docker swarm 
```
ip a
docker swarm init --advertise-addr (ip manager)
docker node ls
```
 ## 3. Label node
 ```
docker node update \
  --label-add role=frontend \
  khai (sebagai manager)
docker node update \
  --label-add role=backend \
  fatma (sebagai worker)
```
```
docker node inspect khai (manager) --pretty
docker node inspect fatma (worker) --pretty
```

## 4. Buat repository Opendocman
```
sudo mkdir -p /opt/stacks
cd /opt/stacks

git clone https://github.com/opendocman/opendocman.git

cd opendocman
```
## 5. Generate environment 
```
./scripts/generate-env-secrets.sh
```
## 6. Buld image
```
docker build -t opendocman:pathched

docker images | grep opendocman
```
## 7. Overlay Network
```
docker network create \
--drive overlay \
opendocman-net

docker networks ls
```
## 8. Direktori
```
sudo mkdir -p /srv/opendocman/mysql
sudo mkdir -p /srv/opendocman/files
sudo mkdir -p /srv/opendocman/config


sudo chmod -R 755 /srv/opendocman
```
## 9. Stack yml
```
nvim stack.yml

```
## 10 Deploy stack
```
docker stack deploy -c stack.yml opendocman
```
## 11 Verifikasi service
```
docker stack services opendocman
```
## 12 Install Apache 
```
sudo pacman -S apache
sudo systemctl enable --now httpd
systemctl status httpd
```
## 13 Module reverse proxy
```
sudo nvim /etc/httpd/conf/httpd.conf

LoadModule proxy_module modules/mod_proxy.so
LoadModule proxy_http_module modules/mod_proxy_http.so
LoadModule headers_module modules/mod_headers.so
LoadModule rewrite_module modules/mod_rewrite.so
```
## 14 Virtual host opendocman
```
sudo nvim /etc/httpd/conf/conf.d/opendocman.conf

<VirtualHost *:80>

    ServerName [khaifatma.local.test]

    ProxyPreserveHost On
    ProxyRequests Off

    ProxyPass / http://127.0.0.1:8080/
    ProxyPassReverse / http://127.0.0.1:8080/

    ErrorLog "/var/log/httpd/opendocman-error.log"
    CustomLog "/var/log/httpd/opendocman-access.log" combined

</VirtualHost>
```
## 15 Include host
```
sudo nvim /etc/httpd/conf/httpd.conf

Include conf/conf.d/opendocman.conf
```
## 16 Konfigurasi Apache
```
sudo apachectl configtest

sudo systemctl restart httpd
```
## Firewall
```
sudo firewall-cmd --permanent --add-service=http

sudo firewall-cmd --permanent --add-service=https

sudo firewall-cmd --reload
```
## DNS atau host
```
(no ip a manager) khaifatma.local.test
```
## Akses web Opwndocman
http://khaifatma.local.test/install/setup-config

## FINISH





