The following is the uber-paranoid method of updating wordpress sites on our campus.  This process will generate one backup on the site itself, one backup on your local machine, a clone of the site on the development server and a backup of the site's database .  This way, if ANY thing happens during or after the upgrade/update, you can quickly revert back to the previous state. These instructions assume your site is on the new departmental web host, commonly referred to as WH.

1. Log into the account via ssh and sftp
2. In both SSH and SFTP, move to `/var/www/html/<yourdomain>.missouri.edu` (where <yourdomain> is the domain of the site)
3. In SSH, cd into backups (if there isn't a backups directory, create it)
4. Download previous backup if you havent already (if applicable)
5. Delete previous backup (if applicable)
6. In SSH type in:

     ```
     tar -zcf <date>.tar.gz /var/www/html/<yourdomain>.missouri.edu/<path-to-wordpress>/
     ```

     For the account muuawebdevjobs it would be

     ``` 
     tar -zcf 20130926.tar.gz /var/www/html/webdevjobs.missouri.edu/www/`
     ```
     
     tar is a linux archive program and will create the archive of our wordpress site. [tar manual](http://www.ss64.com/bash/tar.html). If by chance you need to exclude a directory, you can use *--exclude=/path/to/file*. Using our example above, if we needed to backup everything in the WebDevJobs account except the backup directory, we would do
     ```
     tar -zcf 20131011.tar.gz /var/www/html/webdevjobs.missouri.edu/ --exclude=/var/www/html/webdevjobs.missouri.edu//backup
     ```


7. Once tar finishes, verify there were no errors and that the backup exists. If there were errors, google is your savior.  Or contact the assistant director or the assistant-to-the-assistant director.
8. Download the new backup (save somewhere locally where you can locate it easily)
9. In the SSH session, cd back up one level to  /var/www/html/<domain>.missouri.edu/
10. Type in

    ```
    rsync -a --progress --exclude='www/wp-config.php' www <accountname>@col.missouri.edu@wh-dev-01-mgmt.missouri.edu:/var/www/html/<domain>.missouri.edu/
    ```

    For the account muuawebdevjobs it would be

    ```
    rsync -a --progress --exclude='www/wp-config.php' www muuawebdevjobs@vh-dev.missouri.edu:/sites/muuawebdevjobs/
    ```

11. Type in the account password
12. Verify rsync didn't report any errors. If there were errors, google is your savior.  Or contact the assistant director or the assistant-to-the-assistant director.

13. Launch MySQLWorkbench and log into the admin account for the site
14. Go to **Data Export**
15. Select the site's schema and confirm that all of the wordpress tables are selected
16. Select "Export to Self-Contained File" and name the file "Dump<date>-<accountname>.sql (saving the file some place on your local machine where you can find it). For muuawebdevjobs it would be *Dump20130926-muuawebdevjobs.sql*
17. Click "Start Export"
18. Once the export is complete, log into the site with an admin-level account
19. Find the update notification, and click the link "Please update now"
20. For the Wordpress update, click the button "Update Now"
21. If the update is successful, continue with updating any plugins that are being used and have updates (you can also update any of the default themes if you'd like)
*NOTE* - For multisite installations, make sure you upgrade the network after the core has finished upgrading.
22. Visit the site and verify things look ok
23. Run a link check and verify that there are no broken internal links
24. Fix any broken external links, or assign to the appropriate party

**NOTE1** If you run into an ssl cert issue while upgrading a multinetwork site, [this page](https://wordpress.org/support/topic/failed-update-network-attempt-after-upgrading-to-341) 

**NOTE2** If after upgrading a multisite, the dashboard becomes extremely sluggish, run the following SQL on your database:
```
SELECT * FROM wp_options where option_name = 'db_version';
```
Check the returned value against the [db version number for the wordpress version you just upgraded to](http://codex.wordpress.org/WordPress_Versions). If there is a mismatch, update the value in the database to the correct version. This should fix the sluggishness. 