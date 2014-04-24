The following is the uber-paranoid method of updating wordpress sites on our campus.  This process will generate one backup on the site itself, one backup on your local machine, a clone of the site on the development server and a backup of the site's database .  This way, if ANY thing happens during or after the upgrade/update, you can quickly revert back to the previous state.

1. Log into the account via ssh and sftp to vh.missouri.edu
2. In both SSH and SFTP, move to /sites/<accountname>
3. In SSH, cd into backups (if there isn't a backups directory, create it)
4. Download previous backup if you havent already (if applicable)
5. Delete previous backup (if applicable)
6. In SSH type in:

     ```
     tar -zcf <date>.tar.gz /sites/<accountname>/<path-to-wordpress>
     ```

     For the account muuawebdevjobs it would be

     ``` 
     tar -zcf 20130926.tar.gz /sites/muuawebdevjobs/www
     ```
     
     tar is a linux archive program and will create the archive of our wordpress site. [tar manual](http://www.ss64.com/bash/tar.html). If by chance you need to exclude a directory, you can use *--exclude=/path/to/file*. Using our example above, if we needed to backup everything in /sites/muuawebdevjobs/ except the backup directory, we would do
     ```
     tar -zcf 20131011.tar.gz /sites/muuawebdevjobs --exclude=/sites/muuawebdevjobs/backup
     ```


7. Once tar finishes, verify there were no errors and that the backup exists. If there were errors, google is your savior.  Or contact the assistant director or the assistant-to-the-assistant director.
8. Download the new backup (save somewhere locally where you can locate it easily)
9. In the SSH session, cd back up one level to /sites/<accountname>
10. SFTP into vh-dev.missouri.edu
11. Change to wordpress location
12. Change the name of wp-config.php to wp-config-orig.php (or whatever you like)
13. Delete everything except wp-config-orig.php (this assumes that all development work you are doing is managed via GIT)
14. in your SSH session to vh.missouri.edu, type in 

     ```
     scp -r <path-to-wordpress> <account>@vh-dev.missouri.edu
     ```

     For the account muuawebdevjobs it would be

     ```
     scp -r www/ muuawebdevjobs@vh-dev.missouri.edu:/sites/muuawebdevjobs
     ```
     
     scp stands for Secure CoPy and will securely transfer our files between vh.missouri.edu and vh-dev.missouri.edu. [scp syntax](http://www.hypexr.org/linux_scp_help.php)

15. Type in the account password
16. Verify that scp didn't report any errors. If there were errors, google is your savior.  Or contact the assistant director or the assistant-to-the-assistant director.
17. In SFTP, verify the new files are all there
18. Rename the new wp-config.php file to wp-config-prod.php
19. Rename the wp-config-orig.php file back to wp-config.php
20. Launch MySQLWorkbench and log into the admin account for the site
21. Go to **Data Export**
22. Select the site's schema and confirm that all of the wordpress tables are selected
23. Select "Export to Self-Contained File" and name the file "Dump<date>-<accountname>.sql (saving the file some place on your local machine where you can find it). For muuawebdevjobs it would be *Dump20130926-muuawebdevjobs.sql*
24. Click "Start Export"
25. Once the export is complete, log into the site with an admin-level account
26. Find the update notification, and click the link "Please update now"
27. For the Wordpress update, click the button "Update Now"
28. If the update is successful, continue with updating any plugins that are being used and have updates (you can also update any of the default themes if you'd like)
*NOTE* - For multisite installations, make sure you upgrade the network after the core has finished upgrading.
29. Visit the site and verify things look ok
30. Run a link check and verify that there are no broken internal links
31. Fix any broken external links, or assign to the appropriate party