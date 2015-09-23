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
```