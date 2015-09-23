1. Go to *Plugins*, *Add New*
2. Search for "Sucuri"
3. Install "Sucuri Security - Auditing, Malware Scanner and Security Hardening"
4. Activate the Plugin (if on a multisite, network activate it)
5. Sucuri should place a banner at the top of the page. On the right hand side, click on the **Generate API Key** button
6. Select the admin user.
7. Uncheck "Enable DNS lookups on startup"
8. Click the **Proceed** button
9. You should receive a "Site registered successfully" modal window. Click the **Go to the dashboard** button
10. The plugin should automatically perform a core integrity check.  If any files have been modified, a **Show files** button should be available on the right side.  Click the button and verify that the files listed were modified by you or another developer (e.g. wp-admin/.htaccess is listed because you already locked down the admin area).
11. Click on the **Hardening** tab
12. Harden the following areas
    * Protect uploads directory
    * Restrict wp-content access
    * Restrict wp-includes access
    * Information leakage (readme.html)
    * Plugin & Theme editor (may require manually adding *define("DISALLOW_FILE_EDIT", TRUE);* to wp-config.php)
13. Click on the **Settings** Tab
14. On **General Settings**, change "Maximum alerts per hour" to Unlimited.
15. Click the **Change** button
16. Click on the **Alert Settings** sub-tab
17. For *Format of Subject*, change it to "Sucuri Alert, :domain, :event, :remoteaddr"
18. Make sure the following are checked:
    * "Receive email alerts for new user registration"
    * "Receive email alerts for password guessing brute force attacks"
    * "Receive email alerts when a plugin is installed"
    * "Receive email alerts when a plugin is activated"
    * "Receive email alerts when a theme is installed"
    * "Receive email alerts when a theme is activated"
19. Make sure the following are unchecked:
    a. Uncheck "Receive email alerts for failed login attempts" 
20. Click **Save** button near the top
21. Click the **Trust IP** sub-tab
22. Add the following entries: 
    * 128.206.0.0/16
    * 161.130.0.0/16

That's it.  At this point, it wouldn't hurt to click the Malware Scan tab and run a scan