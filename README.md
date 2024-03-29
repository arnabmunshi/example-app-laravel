## Laravel on Sub-domain

### References
- https://stackoverflow.com/questions/62826905/how-to-deploy-laravel-project-on-the-godaddy-hosting-server-plesk-onyx-cpanel

### Steps
- replace given code `on public/.htaccess`
```
<IfModule mod_rewrite.c>
    <IfModule mod_negotiation.c>
        Options -MultiViews -Indexes
    </IfModule>
    
    RewriteEngine On
    
    # Handle Authorization Header
    RewriteCond %{HTTP:Authorization} .
    RewriteRule .* - [E=HTTP_AUTHORIZATION:%{HTTP:Authorization}]
    
    # Redirect Trailing Slashes If Not A Folder...
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteCond %{REQUEST_URI} (.+)/$
    RewriteRule ^ %1 [L,R=301]
    
    # Send Requests To Front Controller...
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteRule ^ index.php [L]
</IfModule>
```

- create a `.htaccess` on root
- add the given code on it
```
RewriteEngine on

# Check if HTTPS is off
RewriteCond %{HTTPS} off
# Redirect to HTTPS
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]

# Check if the requested URI doesn't start with "public"
RewriteCond %{REQUEST_URI} !^public
# Rewrite the URI to prepend "public/"
RewriteRule ^(.*)$ public/$1 [L]
```
