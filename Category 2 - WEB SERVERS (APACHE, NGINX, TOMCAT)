**════════════════════════════════════════════════════════════════════**  
**CATEGORY 2: WEB SERVERS (APACHE, NGINX, TOMCAT)**  
**════════════════════════════════════════════════════════════════════**

**Covering: 9 articles on Apache installation/hardening/security, NGINX hardening, Tomcat setup, SSL/TLS configuration, and production-ready deployments**

**/\* COMMENT: Web servers are the backbone of internet infrastructure. Understanding**  
   **Apache and NGINX is essential for hosting applications, implementing reverse proxies,**  
   **load balancing, and securing web traffic. These skills are critical for DevOps roles. \*/**

**━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━**

**2.1 APACHE WEB SERVER**

**/\* COMMENT: Apache HTTP Server is the most widely deployed web server globally.**  
   **It's highly configurable, supports .htaccess for per-directory configuration,**  
   **and has extensive module support. Perfect for traditional LAMP stacks. \*/**

**INSTALLATION:**

**\# From package manager (easier)**  
**yum install httpd              \# RHEL/CentOS**  
**apt install apache2            \# Debian/Ubuntu**

**\# From source (more control)**  
**wget https://dlcdn.apache.org/httpd/httpd-2.4.58.tar.gz**  
**tar \-xzf httpd-2.4.58.tar.gz**  
**cd httpd-2.4.58**  
**./configure \--prefix=/usr/local/apache2 \--enable-so \--enable-ssl \--enable-rewrite**  
**make**  
**make install**

**KEY CONFIGURATION FILES:**

**RHEL/CentOS:**  
**/etc/httpd/conf/httpd.conf          \# Main config**  
**/etc/httpd/conf.d/\*.conf            \# Additional configs**  
**/etc/httpd/conf.modules.d/          \# Module configs**  
**/var/log/httpd/                     \# Logs**  
**/var/www/html/                      \# Default document root**

**Debian/Ubuntu:**  
**/etc/apache2/apache2.conf           \# Main config**  
**/etc/apache2/sites-available/       \# Virtual host configs**  
**/etc/apache2/sites-enabled/         \# Enabled sites (symlinks)**  
**/etc/apache2/mods-available/        \# Available modules**  
**/etc/apache2/mods-enabled/          \# Enabled modules**  
**/var/log/apache2/                   \# Logs**  
**/var/www/html/                      \# Default document root**

**ESSENTIAL COMMANDS:**

**systemctl start httpd               \# Start Apache**  
**systemctl stop httpd                \# Stop Apache**  
**systemctl restart httpd             \# Restart Apache**  
**systemctl reload httpd              \# Reload config without restart**  
**systemctl enable httpd              \# Enable on boot**  
**systemctl status httpd              \# Check status**

**apachectl configtest                \# Test configuration**  
**apachectl \-t \-D DUMP\_VHOSTS         \# Show virtual hosts**  
**apachectl \-M                        \# List loaded modules**

**\# Debian/Ubuntu specific**  
**a2ensite sitename.conf              \# Enable site**  
**a2dissite sitename.conf             \# Disable site**  
**a2enmod rewrite                     \# Enable module**  
**a2dismod status                     \# Disable module**

**VIRTUAL HOST CONFIGURATION:**

**/\* COMMENT: Virtual hosts allow multiple websites on one server. Name-based virtual**  
   **hosting uses the HTTP Host header to determine which site to serve. \*/**

**\# /etc/httpd/conf.d/example.com.conf**  
**\<VirtualHost \*:80\>**  
    **ServerName example.com**  
    **ServerAlias www.example.com**  
    **DocumentRoot /var/www/example.com/html**  
      
    **\<Directory /var/www/example.com/html\>**  
        **Options \-Indexes \+FollowSymLinks**  
        **AllowOverride All**  
        **Require all granted**  
    **\</Directory\>**  
      
    **ErrorLog /var/log/httpd/example.com-error.log**  
    **CustomLog /var/log/httpd/example.com-access.log combined**  
**\</VirtualHost\>**

**SSL/TLS CONFIGURATION:**

**/\* COMMENT: HTTPS is mandatory for modern web applications. Let's Encrypt provides**  
   **free SSL certificates. Always redirect HTTP to HTTPS in production. \*/**

**\# Install mod\_ssl**  
**yum install mod\_ssl**

**\# SSL Virtual Host**  
**\<VirtualHost \*:443\>**  
    **ServerName example.com**  
    **DocumentRoot /var/www/example.com/html**  
      
    **SSLEngine on**  
    **SSLCertificateFile /etc/ssl/certs/example.com.crt**  
    **SSLCertificateKeyFile /etc/ssl/private/example.com.key**  
    **SSLCertificateChainFile /etc/ssl/certs/ca-bundle.crt**  
      
    **\# Modern SSL configuration**  
    **SSLProtocol all \-SSLv3 \-TLSv1 \-TLSv1.1**  
    **SSLCipherSuite HIGH:\!aNULL:\!MD5:\!3DES**  
    **SSLHonorCipherOrder on**  
      
    **\# HSTS Header**  
    **Header always set Strict-Transport-Security "max-age=31536000; includeSubDomains"**  
**\</VirtualHost\>**

**\# HTTP to HTTPS redirect**  
**\<VirtualHost \*:80\>**  
    **ServerName example.com**  
    **Redirect permanent / https://example.com/**  
**\</VirtualHost\>**

**APACHE SECURITY HARDENING:**

**/\* COMMENT: Security hardening reduces attack surface and protects against common**  
   **vulnerabilities. Always apply security best practices in production. \*/**

**\# Hide Apache version**  
**ServerTokens Prod**  
**ServerSignature Off**

**\# Disable directory listing**  
**Options \-Indexes**

**\# Prevent clickjacking**  
**Header always set X-Frame-Options "SAMEORIGIN"**

**\# XSS protection**  
**Header always set X-XSS-Protection "1; mode=block"**

**\# Prevent MIME sniffing**  
**Header always set X-Content-Type-Options "nosniff"**

**\# Disable unnecessary HTTP methods**  
**\<Directory /var/www/html\>**  
    **\<LimitExcept GET POST HEAD\>**  
        **Require all denied**  
    **\</LimitExcept\>**  
**\</Directory\>**

**\# Disable .htaccess (performance)**  
**AllowOverride None**

**\# Limit request size**  
**LimitRequestBody 10485760  \# 10MB**

**\# Timeout settings**  
**Timeout 60**  
**KeepAlive On**  
**MaxKeepAliveRequests 100**  
**KeepAliveTimeout 5**

**PERFORMANCE TUNING:**

**\# Enable compression**  
**LoadModule deflate\_module modules/mod\_deflate.so**  
**\<IfModule mod\_deflate.c\>**  
    **AddOutputFilterByType DEFLATE text/html text/plain text/xml text/css text/javascript application/javascript**  
**\</IfModule\>**

**\# Enable caching**  
**LoadModule expires\_module modules/mod\_expires.so**  
**\<IfModule mod\_expires.c\>**  
    **ExpiresActive On**  
    **ExpiresByType image/jpg "access plus 1 year"**  
    **ExpiresByType image/jpeg "access plus 1 year"**  
    **ExpiresByType image/png "access plus 1 year"**  
    **ExpiresByType text/css "access plus 1 month"**  
    **ExpiresByType application/javascript "access plus 1 month"**  
**\</IfModule\>**

**\# MPM (Multi-Processing Module) tuning**  
**\<IfModule mpm\_prefork\_module\>**  
    **StartServers        5**  
    **MinSpareServers     5**  
    **MaxSpareServers     10**  
    **MaxRequestWorkers   250**  
    **MaxConnectionsPerChild 1000**  
**\</IfModule\>**

**LOG MANAGEMENT:**

**/\* COMMENT: Proper logging is essential for troubleshooting and security auditing.**  
   **Rotate logs to prevent disk space issues. \*/**

**\# Custom log format**  
**LogFormat "%h %l %u %t \\"%r\\" %\>s %b \\"%{Referer}i\\" \\"%{User-Agent}i\\" %D" combined\_with\_time**  
**CustomLog /var/log/httpd/access.log combined\_with\_time**

**\# Log rotation (/etc/logrotate.d/httpd)**  
**/var/log/httpd/\*log {**  
    **daily**  
    **rotate 14**  
    **compress**  
    **delaycompress**  
    **notifempty**  
    **sharedscripts**  
    **postrotate**  
        **/bin/systemctl reload httpd \> /dev/null 2\>&1 || true**  
    **endscript**  
**}**

**━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━**

**2.2 NGINX WEB SERVER**

**/\* COMMENT: NGINX excels at handling concurrent connections with minimal resource usage.**  
   **It's the preferred choice for reverse proxies, load balancers, and high-traffic sites.**  
   **Many modern applications use NGINX in front of application servers. \*/**

**INSTALLATION:**

**yum install nginx              \# RHEL/CentOS**  
**apt install nginx              \# Debian/Ubuntu**

**KEY CONFIGURATION FILES:**

**/etc/nginx/nginx.conf          \# Main config**  
**/etc/nginx/conf.d/\*.conf       \# Additional configs**  
**/etc/nginx/sites-available/    \# Virtual host configs (Debian/Ubuntu)**  
**/etc/nginx/sites-enabled/      \# Enabled sites**  
**/var/log/nginx/                \# Logs**  
**/usr/share/nginx/html/         \# Default document root**

**BASIC NGINX CONFIGURATION:**

**\# /etc/nginx/conf.d/example.com.conf**  
**server {**  
    **listen 80;**  
    **server\_name example.com www.example.com;**  
    **root /var/www/example.com;**  
    **index index.html index.php;**  
      
    **\# Security headers**  
    **add\_header X-Frame-Options "SAMEORIGIN" always;**  
    **add\_header X-Content-Type-Options "nosniff" always;**  
    **add\_header X-XSS-Protection "1; mode=block" always;**  
      
    **\# PHP processing**  
    **location \~ \\.php$ {**  
        **fastcgi\_pass unix:/var/run/php-fpm/php-fpm.sock;**  
        **fastcgi\_index index.php;**  
        **fastcgi\_param SCRIPT\_FILENAME $document\_root$fastcgi\_script\_name;**  
        **include fastcgi\_params;**  
    **}**  
      
    **\# Static file caching**  
    **location \~\* \\.(jpg|jpeg|png|gif|ico|css|js)$ {**  
        **expires 1y;**  
        **add\_header Cache-Control "public, immutable";**  
    **}**  
**}**

**REVERSE PROXY CONFIGURATION:**

**/\* COMMENT: NGINX reverse proxy sits in front of application servers, providing**  
   **load balancing, SSL termination, and caching. Essential for microservices. \*/**

**upstream backend {**  
    **server 192.168.1.10:8080;**  
    **server 192.168.1.11:8080;**  
    **server 192.168.1.12:8080;**  
**}**

**server {**  
    **listen 80;**  
    **server\_name api.example.com;**  
      
    **location / {**  
        **proxy\_pass http://backend;**  
        **proxy\_set\_header Host $host;**  
        **proxy\_set\_header X-Real-IP $remote\_addr;**  
        **proxy\_set\_header X-Forwarded-For $proxy\_add\_x\_forwarded\_for;**  
        **proxy\_set\_header X-Forwarded-Proto $scheme;**  
          
        **\# Timeouts**  
        **proxy\_connect\_timeout 60s;**  
        **proxy\_send\_timeout 60s;**  
        **proxy\_read\_timeout 60s;**  
    **}**  
**}**

**LOAD BALANCING METHODS:**

**\# Round-robin (default)**  
**upstream backend {**  
    **server server1.example.com;**  
    **server server2.example.com;**  
**}**

**\# Least connections**  
**upstream backend {**  
    **least\_conn;**  
    **server server1.example.com;**  
    **server server2.example.com;**  
**}**

**\# IP hash (session persistence)**  
**upstream backend {**  
    **ip\_hash;**  
    **server server1.example.com;**  
    **server server2.example.com;**  
**}**

**SSL/TLS WITH NGINX:**

**server {**  
    **listen 443 ssl http2;**  
    **server\_name example.com;**  
      
    **ssl\_certificate /etc/ssl/certs/example.com.crt;**  
    **ssl\_certificate\_key /etc/ssl/private/example.com.key;**  
      
    **\# Modern SSL configuration**  
    **ssl\_protocols TLSv1.2 TLSv1.3;**  
    **ssl\_ciphers HIGH:\!aNULL:\!MD5;**  
    **ssl\_prefer\_server\_ciphers on;**  
      
    **\# OCSP Stapling**  
    **ssl\_stapling on;**  
    **ssl\_stapling\_verify on;**  
      
    **\# HSTS**  
    **add\_header Strict-Transport-Security "max-age=31536000" always;**  
**}**

**\# Redirect HTTP to HTTPS**  
**server {**  
    **listen 80;**  
    **server\_name example.com;**  
    **return 301 https://$server\_name$request\_uri;**  
**}**
