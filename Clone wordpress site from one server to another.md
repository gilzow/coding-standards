These instructions make several assumptions:

* Your site is on the new departmental web host, commonly referred to as WH
* You are cloning from production to -dev for purposes of pre-update testing or getting -dev resynched with production.  Adjust server names as needed for your situation
* You are using [MySQL Workbench](http://dev.mysql.com/downloads/workbench/)
* You are hosting your database on DoIT's MySql hosting instance
* You have used vi/vim and know the basics of its usage


## Clone your wordpress site ##
1. Log into the account via ssh
2. In your ssh session, move to `/var/www/html/<yourdomain>.missouri.edu` (where <yourdomain> is the domain of the site)
3. Type in

    ```
    rsync -a --progress --exclude='www/wp-config.php' www <accountname>@col.missouri.edu@wh-dev-01-mgmt.missouri.edu:/var/www/html/<domain>.missouri.edu/
    ```

    For the account webdevjobs it would be

    ```
    rsync -a --progress --exclude='www/wp-config.php' www muwhwebdevjobs@col.missouri.edu@wh-dev-01-mgmt.missouri.edu:/var/www/html/webdevjobs.missouri.edu/
    ```
    
    We exclude the `wp-config.php` file because the -dev site is on a different domain and will need to connect to the development database instance and possibly have other config differences.  If this is the **first time** you are cloning the site, you can remove the exclude parameter, but **make sure** to go back and adjust `wp-config.php` on the -dev server **before** you vist the -dev instance in your browser. Additional steps are listed at the bottom of this document.

4. Type in the account password
5. Verify rsync didn't report any errors. If there were errors, google is your savior.  Or contact the assistant director or the assistant-to-the-assistant director. Pay particular attention to error messages related to quota since quota issues can bite you later.
6. Launch MySQLWorkbench and log into the mysql-web1.missouri.edu (production) using the admin account for the site
7. Go to **Data Export**
8. Select the site's schema and confirm that all of the wordpress tables are selected
9. Select "Export to Self-Contained File" and name the file "Dump<date>-<domain>-prod2dev.sql (saving the file some place on your local machine where you can find it). For *webdevjobs* it would be *Dump20160126-webdevjobs-prod2dev.sql*
10. Click "Start Export"
11. Once the export is complete, open the file in a text editor that supports regex
12. First we need to search and replace any instances of the domain that have been serialized.  Using a text editor that supports regex, do a regex search for 

    ```
    s:\d+:"https?://foo.missouri.edu[^"]*";
    ```

    replacing `foo` with the domain you are searching for. If there are no matches, skip to step 15.  If there are, continue.  

13. We now need to update every serialized instance with our new domain.  However, because it is serialized, if we do a regular find & replace, the serialized definition of the information (in this case, the number of characters in the string) will be incorrect and corrupt the entire serialized object.  You can manually make the change to the domain and update the definition if you have only one or two instances, but if you have more, you'll need to use something more powerful.  In terminal, open your *.sql file from step 9 in vim. 
14. Press the Esc and `:`
15. Type or copy and paste the following, changing `foo` to your domain, and possibly`7` to the number of characters you are adding to the domain (7 is being used since we are appending `-wh-dev` to our domain), and `-wh-dev` to whatever your development identifier is if it is different: 

    ```
    %s@s:\(\d\+\):"http\(s\)\=://\(foo\).missouri.edu@\='s:' . (submatch(1) + 7). ':"http' . submatch(2) . '://' . submatch(3) . '-wh-dev.missouri.edu'@g
    ```

16. Press **Enter**.  vim will find and replace all instances of your serialized domain and replace it with the new domain AND update the number of characters in the string in the definition.
17. Save the file, or if you're paranoid save it with a different name (in vim, do Esc `:` and then `w newname.sql`, press Enter).
18. You can now do regular find and replace on your domain using whatever text editor you prefer
19. Once you have all of the instances of the domain updated, save the file
20. In Workbench, log into mysql-webdev.missouri.edu (development) using the admin account for the site 
21. Go to **Data Import/Restore**
22. Select **Import from Self-Contained File**
23. Select your file you saved at step 19
24. Select the correct schema from Default Target Schema
25. Press the **Start Import** button

If this the first time you've cloned the site to this server (as discussed in step 3), see the additional instructions below for adjusting `wp-config.php`.  If not, then the development site should now be an exact clone of your production site.  

If you are cloning to a new server, or if this is the first time to clone to development, log into the development server and change the value for `DB_HOST` in `wp-config.php` to the development instance of the database. If this is a multisite, you will also need to change the value for `DOMAIN_CURRENT_SITE` to the development domain of the site.  Once you've done this, save the file.  Your development site should now be ready.   