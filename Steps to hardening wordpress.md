1. Change the admin account user name
    * Create a second user account that you'll use for admin tasks and then delete the 'admin' account (ideal) OR
    * Go into the database and change the user_login for 'admin' to something else
2. In wp-config.php 
    1. change the $table_prefix from 'wp_' to something else BEFORE you install wordpress
    2. Update the Unique Keys and Salts
        1.  visit https://api.wordpress.org/secret-key/1.1/salt/
        2. Copy and paste the values from the web site into wp-config replacing the default values
        3. Scroll down to `/* That's all, stop editing! Happy blogging. */`. Right before that line, add the following `define('DISALLOW_FILE_EDIT', TRUE);`
    3. Save the file.
    4. Now change the permissions on wp-config.php to 0400 (owner-readable only)
3. In your functions file for your theme, do the following (see note below):
    1. Remove XMLRPC support
        * `add_filter('xmlrpc_enabled', '__return_false');`
    2. Remove the wordpress generator meta information
        * `remove_action( 'wp_head', 'wp_generator' );`
    3. [Prevent remote attackers from enumerating user names](Prevent%20remote%20attackers%20from%20enumerating%20user%20names.md)
4. [Make .htaccess changes](Wordpress .htaccess changes.md)
5. [Install and configure the Sucuri Security plugin](Set up Sucuri Security wordpress plugin.md)

If you would prefer not to use the Sucuri Security plugin, please delete the **readme.html** file from the root of the wordpress install, and [make these additional .htaccess changes](Additional%20.htaccess%20changes.md).

**NOTE**: All of the items in Step 3 above are already incorporated into v3 of the MizzouMVC framework. If you are using the framework, you do not need to add them to your functions file. 