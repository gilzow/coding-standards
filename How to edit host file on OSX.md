1. Bring up Terminal
2. Type in the following: `sudo cp /private/etc/hosts ~/Documents/hosts.bckup`
3. Type in your password and hit Enter. This will create a back up of your hosts file before we modify it, just in case you need to restore it later.
4. Now type in the following: `sudo vi /etc/private/hosts`
5. Type in your password and hit Enter. This will bring up the hosts file in vi in order for you to edit. The following steps assume you are going to use vi (these commands should also work for vim).  You can also use vim, or nano, or emacs, or whatever termainl text editor you prefer.
6. Using your arrow keys, scroll down to the last line in the file 
7. Press Shift + A (basically, type in a capital A). This will place you into edit mode at the end of the line.
8. Press Enter to create a new line.
9. Type in `127.0.0.1`
10. Press Tab
11. Enter in the domain of the site you are going to work on
12. Press the Esc key (this will remove you from edit mode)
13. Type in `:x` and press Enter. This will save and exit the file
14. Now when you go to the domain you entered in step 11 into your browser, you'll go to the copy of the site running in vagrant. 
15. If for some reason you are still going to the copy of the site on WH, you might need to flush your cache.  Back in Terminal, type in: `sudo dscacheutil -flushcache` 
16. Press Enter 
17. Type in your password and press Enter, if prompted
18. Hard refresh your browser. If you are *still* not seeing the vagrant copy, it's possible your browser has cached the dns entry and is stubbornly refusing to let it go.  
