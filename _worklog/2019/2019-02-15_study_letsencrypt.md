# https

ACME protocol

github/ietf-wg-acme/acme

ACME: Automatic Certificate Management Environment
CA: Certificate Authority
DV: Domain Validation
OV: Organization Validation
EV: Extended Validation

apache
.htaccess
```
<IfModule mod_rewrite.c>
  RewriteEngine On
  RewriteCond %{HTTPS} off
  RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
</IfModule>
```

nginx
````
server {
  listen 80;
  server_name example.com www.example.com;
  return 301 https://example.com$request_uri;
}
```

