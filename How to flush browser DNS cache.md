## Firefox ##

1. In the address bar, type in `about:config` 
2. Click the *I'll be careful, I promise!* button 
3. Find the entry **network.dnsCacheExpiration** 
4. Double-click on it and set it's value to `0` (zero, not the letter O)  

If **network.dnsCacheExpiration** doesn't exist from step 3 above: 

1. right click and choose **New** -> **Integer** 
2. Enter the preference name `network.dnsCacheExpiration` 
3. click **OK** 
4. Enter a value of `0` (zero, not the letter O) 
5. Click **OK**
6. Refresh the page
7. If you're still getting the old site/address, restart Firefox

## Chrome ##

1. In the address bar, type in `chrome://net-internals/#dns`
2. Scroll down a little and click the *Clear host cache* button next to **Host resolver cache**
3. Refresh the page
4. If you're still getting the old site/address, restart Chrome

## Safari ##
Need to find the instructions

## Internet Explorer ##
Need to find the instructions.

## Microsoft Edge ##
Need to find the instructions.  Is it different than IE?

Good resource: [https://support.opendns.com/entries/26336865-Clearing-the-DNS-Cache-on-Computers-and-Web-Browsers](Link URL)