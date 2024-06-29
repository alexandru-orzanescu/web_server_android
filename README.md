# web_server_android
Run a WebServer on an Android device

## Steps to get the environment ready:
1. Install Termux from Google Play
2. Open Termux
3. Update Termux:
```sh
    pkg update
    pkg upgrade -y
```
4. Install pre-requisites:
```sh
    pkg install wget curl vim git tar -y
    pkg install nginx -y
```
5. Start Nginx
```sh
    nginx
```
6. Verify Nginx is Running:
    Check if Nginx is running by visiting your Android device's local IP address in a web browser on the same network, e.g., http://192.168.1.xxx.

## Clone the git to home folder
```sh
    git clone https://github.com/alexandru-orzanescu/web_server_android.git
```

## Steps to setup nginx:
1. Update nginx.conf:
cp ~/web_server_android/nginx/nginx.conf $PREFIX/etc/nginx/nginx.conf
2. Modify the section by adding <your_domain>:
```
server {
        listen       8443 ssl;
        server_name  <your_domain> www.<your_domain>;

        ssl_certificate /data/data/com.termux/files/home/cert/cert.pem;
        ssl_certificate_key /data/data/com.termux/files/home/cert/key.pem;

        ssl_session_cache    shared:SSL:1m;
        ssl_session_timeout  5m;

    #    ssl_ciphers  HIGH:!aNULL:!MD5;
    #    ssl_prefer_server_ciphers  on;

    #    location /.well-known/acme-challenge {
    #            alias /data/data/com.termux/files/home/www/.well-known/acme-challenge/;
    #    }

        location / {
            root   /data/data/com.termux/files/home/www;                                                                  
            index  index.html index.htm;
        }
    }
```
3. Make sure you have your cert directory
```sh
    mkdir ~/cert
    cp ~/web_server_android/cert ~/cert
```
4. Update the cert.pem and key.pem files with the correct data
```sh
    vim ~/cert/cert.pem
```
```sh
    vim ~/cert/key.pem
```
5. Restart Nginx:
```sh
    nginx -s stop
    nginx
```
6. Create Web Directory
```sh
    mkdir ~/www
```
7. Add Content:
```sh
    cp ~/web_server_android/www ~/www
```
