Sometimes referred to as the "Jesse Server".  Windows users might also refer to it as the "J Drive".

## For windows 7 ##
1. Open My Computer or Windows Explorer
2. There should be a button at the top that says "Map Network Drive". Click that button ![Screen shot of the My Computer window and the Map Network Drive](http://uamedia.missouri.edu/documentation-images/mapping1.png)
3. Choose a drive letter that you want to use to map to the network share ("J" is often used since people still refer to this share as the "Jesse Server")
4. Next to Folder, type in ```\\col.missouri.edu\files\WC```![Screen shot of the Map Network Drive dialog box](http://uamedia.missouri.edu/documentation-images/mapping2.png)
5. Make sure "Reconnect at logon" is checked
6. In the lower right, click the button labeled "Finished"

A new My Computer/Windows Explorer window should open up for the J: drive.  Your "J" drive is now mapped to the network share.

## For OSX ##
1. Go to/launch the Finder
2. Go to the **Go** menu, and select *Connect to Server...* (alternatively press the apple/command key + K on the keyboard)
3. In the Connect to Server dialog box, for Server Address: type in ```smb://doit-bfs1.col.missouri.edu/WC```![Screen shot of the Connect to Server dialog window in OSX](http://uamedia.missouri.edu/documentation-images/mapping3.png)
4. At the prompt, type in your pawprint (SSOID) and password

The shared network drive is now mounted to your computer.  You will need to repeat this process each time you log on to your machine.  If you would like to have it mount the shared space at login:

1. Open System Preferences and click on “Users & Groups”
2. Select your user name from the list and then click the “Login Items” tab
3. Drag and drop the icon for the WC shared drive into the login items list![Screen shot of the Users & Groups Login Items dialog window in OSX](http://uamedia.missouri.edu/documentation-images/mapping4.png)