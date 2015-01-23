# 3. Naming Conventions #
## 3.1 Filenames ##
* Filenames **MUST** only use alphanumeric characters, and the dash character.
* Filenames **MUST NOT** use spaces.
* Files that contain php code **SHOULD** end in '.php'.

```
#!php5
FrontController.php
```

## 3.2 Namespaces ##
* Namespaces **MUST** have a 1:1 relationship to the filesystem
* Namespaces **MUST** contain only alphanumeric characters, the underscore, and, the namespace separator
* Namespaces, and acronyms in the namespace **SHOULD** use StudlyCaps.
* Each namespace **MUST** have a top-level namespace of _Mizzou_.
* A fully-qualified namespace and class **MUST** have the following structure: \\Mizzou\\(<Namespace>\\)<Class Name>
* Each namespace **MAY** have as many sub-namespaces as it wishes.
* Each namespace separator is converted to a DIRECTORY_SEPARATOR when loading from the file system.
* Each _ character in the CLASS NAME is converted to a DIRECTORY_SEPARATOR. The _ character has no special meaning in the namespace.
* The fully-qualified namespace and class is suffixed with .php when loading from the file system.
* Alphabetic characters in namespaces and class names may be of any combination of lower case and upper case.

```
#!php5
<?php
namespace Mizzou\CalendarTranslator;
?>
```

## 3.3 Namespace Aliases ##
* If aliasing a namespace, you **MUST** use the final segment of the namespace as the alias.
* If aliasing a class, you **MUST** use the class name as the alias.

```
#!php5
<?php
use Mizzou\CalendarTranslator\CalendarException as CalendarException;
?>
```

## 3.4 Classes ##
* Class names **MUST** contain only alphanumeric characters.
* Class names **MUST** use StudlyCaps
* In most cases, class names **SHOULD NOT** contain numbers

```
#!php5
<?php
class ExampleTranslator extends AbstractTranslator
{
    // code here
}
?>
```

## 3.5 Abstract Classes ##
* Abstract classes **MUST** use the same naming conventions as Classes.
* Abstract classes **MUST** must being with "Abstract"

```
#!php5
<?php
abstract class AbstractTranslator
{
    // code here
}
?>
```

## 3.6 Interfaces ##
* Interface names **MUST** use the same naming conventions as Classes.
* Interface names **MUST** be nouns or adjectives.
* Interface names **SHOULD** end with the word "Interface"

```
#!php5
<?php
interface TranslatorInterface
{
    // code here
}
?>
```

### 3.7 Exceptions ##
* Exception classes **MUST** use the same naming conventions as Classes.
* Exception classes **MUST** end with the word "Exception".

```
#!php5
<?php
class CalendarException extends Exception
{
    // code here
}
?>
```

## 3.8 Functions and Methods ##
* Functions/Methods **MUST** contain only alphanumeric characters.
* Functions/Methods **MUST NOT** contain underscores.
* Class methods that are declared protected or private **MAY** start an underscore
* Class methods declared public **MUST NOT** start with an underscore
* Functions/Methods **MUST** follow camelCaps capitalization

```
#!php5
<?php
function getData()
{
    //code
}
?>
```
```
#!php5
<?php
class ExampleClass
{

    public function getData()
    {
        //code
    {

    private function _initiateConnection()
    {
        //code
    }

}
?>
```

## 3.9 Variables ##
* Variable **MUST** contain only alphanumeric characters.
* Variables **MUST NOT** contain underscores.
* Class members that are declared protected or private **MAY** contain an underscore as the first character
* Variables **MUST** follow camelCaps capitalization
* Variables **MUST** prefix the name with a descriptor of the data type
* Developers **MUST** use the following data type descriptors. Developers **MAY** use either the short or long form:
    * String: str/s
    * Boolean: bool/b
    * Integers: int/i
    * Floating point numbers: flt/f
    * Arrays: ary/a
    * Object: obj/o
    * Resource: rsc/r
    * Mixed: /mxd/m

```
#!php
<?php
//Strings
$strSomeVar = 'text';
$sSomeVar   = 'text';

//Booleans
$boolIsPage = FALSE;
$bIsPage    = FALSE;

//Integers
$intPeople  = 10;
$iPeople    = 10;

//Floats
$fltTotal   = 3093.13;
$fTotal     = 3093.13;

//Arrays
$aryChancellors = array('Wallace', 'Deaton', 'Loftin');
$$aChancellors  = array('Wallace', 'Deaton', 'Loftin');

//Objects
$objChancellor  = new Chancellor('Loftin');
$oChancellor    = new Chancellor('Loftin');

//Resources
$rscLog     = fopen('data.log','r');
$rLog       = fopen('data.log','r');

//Mixed
$mxdCase    = reset($aryValues);
$mCase      = reset($aValues);
?>
```

## 3.10 Constants ##
* Constants **MAY** contain both alphanumeric characters and underscores.
* All letters **MUST** be capitalized and words **MUST** be separated by underscores.
* Constants **MUST** be defined as class members with the "const" modifier.
* Constants **MAY** be defined in the global scope or within namespaces
Examples
```
#!php5
<?php
define('EXAMPLE_CONST',true);

class ExampleClass
{
    const EXAMPLE_CONST = true;
}
?>
```

**Next**: [Coding Style](Coding Standards 4. Coding Style)

**Previous**: [File Formatting](Coding Standards 2. File Formatting)