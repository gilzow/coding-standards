# 2. File Formatting #
## 2.1 Indentation ##
* Indentation **MUST** consist of 4 spaces.
* Tabs **MUST NOT** be used for indentation.

## 2.2 Maximum Line Length ##
* Developers **SHOULD** strive for a target line length of 80 characters.
* Line lengths **MAY** be up to 120 characters in specific situations.

## 2.3 Code Demarcation (aka PHP Code Tags) ##
PHP code **MUST** always be delimited by the full-form, standard PHP tags:

```PHP
<?php

?>

```

This is most portable way to include PHP code on differing operating systems and setups.

* For files that contain only PHP code, the closing tag (?>) **MUST NOT** be used. It is not required by PHP, and omitting it prevents the accidental injection of trailing white space into the response.

**Next**: [Naming Conventions](Coding Standards 3. Naming Conventions.md)

**Previous**: [Conventions](Coding Standards 1. Conventions.md)
