In the .htaccess file in the root of wordpress, add the following to the top of the file


```
#!bash

# block access to login page from all external addresses
<Files wp-login.php>
 order deny,allow
 deny from all
 allow from 128.206.
 allow from 161.130.
 allow from 10.7.
 allow from 10.8.
</Files>

# completely disable xmlrpc
<Files xmlrpc.php>
order deny,allow
deny from all
</Files>

#https://www.owasp.org/index.php/List_of_useful_HTTP_headers
<IfModule mod_headers.c> 
	Header set X-XSS-Protection "1; mode=block" 
	Header set X-Content-Type-Options nosniff
</IfModule>
```

Now, add an .htaccess file inside of /wp-admin/ and add the following to the top of the file

```
#!bash

order deny,allow
deny from all
allow from 128.206.
allow from 161.130.
allow from 10.7.
allow from 10.8.
```

In /wp-includes/ add (or edit, if applicable) an .htaccess file and add the following:

```
#!bash
<FilesMatch "\.(?i:php)$">
  <IfModule !mod_authz_core.c>
    Order allow,deny
    Deny from all
  </IfModule>
  <IfModule mod_authz_core.c>
    Require all denied
  </IfModule>
</FilesMatch>
<FilesMatch "^(wp-tinymce|ms-files).php$">
  <IfModule !mod_authz_core.c>
    Allow from all
  </IfModule>
  <IfModule mod_authz_core.c>
    Require all granted
  </IfModule>
</FilesMatch>
```