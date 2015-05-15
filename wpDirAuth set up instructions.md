1. Go to **Plugins**, **Add New**
2. Search for "wpdirauth"
3. in the search results, under the wpDirAuth heading, click *Install Now*
4. Click OK to the "Are you sure you want to install this plugin?" prompt
5. Verify there were 4 steps during the installation (the last should be "successfully installed the plugin wpDirAuth 1.7.6") and then click the *Activate Plugin* link
6. Go to **Settings**, **Directory Auth**.
7. Click *Yes* for **Enable Directory Authentication**
8. Click *Yes* for **Require SSL Login**  -- Note -- unless you are on -dev and don't have an ssl cert set up yet. HOWEVER, you must have ssl set up before moving to production
9. Select *Use TLS* for **Enable SSL Connectivity?**
10. For **Directory Servers (Domain Controllers)**, enter in "col.missouri.edu:3268:"
11. Leave **Account Filter** as "samAccountName"
12. Leave **Account Suffix** blank
13. Leave **Base DN** blank
14. For **Bind DN**, use a valid resource account entered as <resource-account>@missouri.edu (e.g. umcuawebcom@missouri.edu) -- Note -- because the resource account password has to be stored non-encrypted, use a resource account that isn't tied to the site and one that has limited privileges/permissions  
15. For **Bind Password** and **Confirm Password**, enter in the password for the resource account you entered at step 14.
16. If desired, enter in the CN for an authentication group you want to limit authentication to.
17. Enter in "University of Missouri" for **Institution Name**
18. Enter in "Pawprint" for **Marketing name for Institutional Single-Sign-On ID**
19. For **Password Change Message**, we typically use something like 

```
#!html

To change your University of Missouri password, please use the <a href="https://webapps.missouri.edu/revamp/wizards/passwordManager/passwordManager.jsp">Password Manager</a> tool.
```

20. Click *Update Options* button at the bottom of the screen