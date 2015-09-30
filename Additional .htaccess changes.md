In wp-content create an .htaccess file and add the following in it

```
#!

<FilesMatch "\.(?i:php)$">
  <IfModule !mod_authz_core.c>
    Order allow,deny
    Deny from all
  </IfModule>
  <IfModule mod_authz_core.c>
    Require all denied
  </IfModule>
</FilesMatch>
```

In wp-includes create an .htaccess file and add the following in it


```
#!

<FilesMatch "\.(?i:php)$">
  <IfModule !mod_authz_core.c>
    Order allow,deny
    Deny from all
  </IfModule>
  <IfModule mod_authz_core.c>
    Require all denied
  </IfModule>
</FilesMatch>
<Files wp-tinymce.php>
  Allow from all
</Files>
<Files ms-files.php>
  Allow from all
</Files>
```