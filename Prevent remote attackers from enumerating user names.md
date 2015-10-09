```
#!php

function scanForEnumerationAttempt($strRedirectionURL, $strRequestedURL) {
	if (1 === preg_match('/\?author=([\d]*)/', $strRequestedURL)) {
		$strRedirectionURL = false;
	} 
   
   return $strRedirectionURL;
} 

add_filter('redirect_canonical','scanForEnumerationAttempt', 10,2); 

/**
 * Removes username from the body class list.  Why does wordpress include the user name in the body class?  So you can
 * add per-user custom classes, but that seems like a very fringe case vs giving hackers all of your user names.
 *
 * @param $aryClasses array of classes to include in the body element
 * @return array filtered list of classes
 */
function mizzouRemoveUserNameFromBodyClass($aryClasses){
    if(is_author() && in_array('author',$aryClasses)){
        /**
         * match all classes of 'author-<username>' but not 'author-id'
         *
         * match: author-admin
         * match: author-gilzowp
         * NO match: author-5
         *
         */
        $aryUserNames = preg_grep('/^author-(?!\d+$).+$/',$aryClasses);
        if(count($aryUserNames) > 0){
            $aryClasses = array_diff($aryClasses,$aryUserNames);
        }
    }
    return $aryClasses;
}
add_filter('body_class','mizzouRemoveUserNameFromBodyClass',100);

```