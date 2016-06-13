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

<Files readme.html>
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

In both /wp-contents/plugins/ and /wp-contents/themes/ add (or edit, if applicable) an .htaccess file and add the following:

```
#!bash
ErrorDocument 403 /404

RewriteCond %{HTTP_REFERER} !^https?://(www\.)?cellmu-wh-dev\.missouri\.edu/.*$ [NC]
RewriteRule .* - [F,L]

RewriteCond %{HTTP_REFERER} ^https?://(www\.)?cellmu-wh-dev\.missouri\.edu/.*$ [NC]
RewriteCond %{REQUEST_URI} !\.(js(on)?|jpe?g|gif|png|svg|bmp|css|eot|ttf|woff|woff2|xml)$ [NC]
RewriteRule .*  - [F,L]

#if your theme/plugin needs a special exception, comment the above line, uncomment the next line and adjust as needed
#RewriteRule !(specialfilename1|specialfilename2)\.php$ - [NC,F,L]

#OR you could add another RewriteCond to do the same thing
#RewriteCond %{REQUEST_URI} !(specialfilename1|specialfilename2)\.php$


# not needed. keeping for reference
#<IfModule !mod_authz_core.c>
#  Order allow,deny
#  Deny from all
#</IfModule>
#<IfModule mod_authz_core.c>
#  Require all denied
#</IfModule>

#<FilesMatch "\.(css|jpg|gif|png|svg|js|jpeg)$">
#  <IfModule !mod_authz_core.c>
#    Order allow,deny
#    Allow from all
#  </IfModule>
#  <IfModule mod_authz_core.c>
#    Require all granted
#  </IfModule>
#</FilesMatch>
```