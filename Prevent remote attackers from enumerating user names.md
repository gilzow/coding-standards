
```
#!php

function scanForEnumerationAttempt($strRedirectionURL, $strRequestedURL) {
	if (1 === preg_match('/\?author=([\d]*)/', $strRequestedURL)) {
		$strRedirectionURL = false;
	} 
   
   return $strRedirectionURL;
} 

add_filter('redirect_canonical','scanForEnumerationAttempt', 10,2); 
```