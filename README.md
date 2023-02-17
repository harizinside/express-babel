# Express Babel Boilerplate

This project based on express-generator and modifed to BabelJS,
with remove unused package and update version to the lates version.

How to it

```bash
$ git clone https://github.com/harizinside/express-babel.git
$ cd ./express-babel
$ npm install
$ npm run dev
```

You can build for production using 

```bash 
$ npm run build
```

if you are using nginx to handle, you can use this methode

```conf
server {
  listen 80 http2;

  server_name yourdomain.com www.yourdomain.com;
  access_log /var/log/nginx/yourdomain.com.accsess.log;
  error_log /var/log/nginx/yourdomain.com.error.log;

  location / {
    proxy_pass http://localhost:3000;
    proxy_http_version 1.1;
    proxy_set_header Access-Control-Allow-Origin *;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection 'upgrade';
    proxy_set_header Host $host;
    proxy_cache_bypass $http_upgrade;
  }
}
```

For apache2

```conf
<VirtualHost *:80>
  ServerName yourdomain.com
  ServerAlias www.yourdomain.com
  ServerAdmin webmaster@example.com

  ProxyPreserveHost On
  ProxyPass / http://localhost:3000/
  ProxyPassReverse / http://localhost:3000/

  ErrorLog /var/log/apache2/error.log
  CustomLog /var/log/apache2/access.log combined
</VirtualHost>
```

Or using htaccsess

```htaccsess
Options +FollowSymLinks -Indexes
IndexIgnore *
DirectoryIndex
<IfModule mod_rewrite.c>
RewriteEngine on
# Simple URL redirect:
RewriteRule ^(.*)$ http://127.0.0.1:3000/$1 [P]
</IfModule>
```

> please note all of this configuration using proxy pass, so you need anoter service to handle it

Please use this link, https://expressjs.com/en/advanced/best-practice-performance.html#set-node_env-to-production
