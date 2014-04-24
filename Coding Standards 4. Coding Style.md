Table of Contents
9. [Inline Documentation](#inlinedocs)

# 4. Coding Style #
## 4.1 Strings ##
### 4.1.1 String Literals ###
When a string is literal and contains no variable substitutions, a singe quote **SHOULD** be used to demarcate the string.
```
#!php5
<?php
$strExample = 'some string here';
?>
```
### 4.1.2 String Literals containing apostrophes or single quotes ###
When a literal string contains single quotes/apostrophe, double quotes **SHOULD** be used to demarcate the string.
```
#!php5
<?php
$strExample = "There's an apostrophe in this string";
?>
```
### 4.1.3 Variable Substitution ###
If the string contains variable substitution, double quotes **SHOULD** be used to demarcate the string.
```
#!php5
<?php
$strExample = "$strFoo went to $strBar.";
?>
```
### 4.1.4 String Concatenation ###
* Strings **MUST** be concatenated with the "." operator
* If the string being concatenated exceeds the maximum line length, the string **SHOULD** be broken into multiple lines
    * Each successive line **SHOULD** be indented such that the "." operator is alligned with the "=" operator

```
#!php5
<?php
$strSample = 'The ' . $aryArg[4] . ' ran over to the ' . $aryArg[6] . ' which is next to the ' . $aryArg[8];

$strSecondSample    = 'WARNING: An error occurred at line ' . __LINE__ . ' in function ' . __FUNCTION__ . ' in file '
                    . basename(__FILE__) . ' at ' . date('g:i A') . ' on ' . date('l, F j, Y') .'. Running out of '
                    . 'things to add to this concatenation.';
?>
```

### 4.1.5 String concatenation vs variable substitution vs sprintf ###
* Developers ***MAY*** use any method in building strings, but **MUST** be consistent in their code.
```
#!php5
<?php
//concatenation
$strFeedURL .='&start='.$aryOptions['start'].'&end='.$aryOptions['end'];
//vs variable substition
$strFeedURL .= "&start={$aryOptions['start']}&end={$aryOptions['end']}";
//vs sprintf
$strFeedURL .= sprintf('&start=%s&end=%s',$aryOptions['start'],$aryOptions['end']);
?>
```

## 4.2 Arrays ##
### 4.2.1 Indexed Arrays ###
* Indexed arrays **MUST** contain a trailing space after each comma delimiter
* Indexed arrays **MAY** span multiple lines if the array declaration exceeds the maximum line length.
    * Each successive line **MUST** be indented such that the beginning of each line aligns with the initial element of the array.
    * Alternatively, the initial array item **MAY** begin on the following line:
        * Each line **MUST** be indented one indentation level greater than the line containing the array declaration
        * The closing paren **MUST** be on a line by itself at the same indentation level as the line containing the array declaration
```
#!php
<?php
$arySample = array(1, 2, 3);

$arySample = array(1, 2, 3,
                   'Deaton', 'Loftin', 'Wallace',
                   'Truman', 'Fred', 'George');
$arySample = array(
    1, 2, 3,
    'Deaton', 'Loftin', 'Wallace',
    'Truman', 'Fred', 'George'
);
?>
```

### 4.2.2 Associative Arrays ###
* Associative arrays **SHOULD** be broken into multiple lines.
* Each successive line **MUST** be indented such that both keys and values are aligned.
* "=>" operators **SHOULD** be indented such that they align.
* Alternatively, the initial array item **MAY** begin on the following line.
    * Each successive line **MUST** be indented one indentation level greater than the line containing the array declaration.
    * The closing paren **MUST** be on a line by itself at the same indentation level containing the array declaration.
```
#!php
<?php
$arySample = array('date'   => 'datevalue',
                   'age'    => 'agevalue');

$arySample = array(
    'date'  => 'datevalue',
    'age'   => 'agevalue'
);
?>
```

## 4.3 Namespaces ##
### 4.3.1 Namespace Declaration ###
* Files **SHOULD** contain only a single namespace.
* Namespace declarations **MUST** be the first statement in a file.
    * The only code that **SHOULD** precede a namespace declaration is a file level documentation block
    * There **SHOULD** be a single empty line between the docblock and the namespace declaration.
* Namespace declarations **MUST NOT** be indented.
* In the situation where multiple namespace declarations _must_ be placed in the same file
    * Declarations **MUST** utilize blocks and not single line declarations
    * Opening brace **MUST** be placed on the following line at same level of indentation.
    * Code with the namespace block **MUST** be indented one extra level.
```
#!php
<?php
namespace Facebook
{
    // code
}

namespace Twitter
{
    // code
}
?>
```

### 4.3.2 Import Statements ###
* All explicit dependencies used by a class **MUST** be imported.
* There **MUST** be one _use_ keyword per declaration.
* There **MUST** be one blank line after the _use_ block.
* Import statements **SHOULD** be in alphabetical order

## 4.4 Classes ##
### 4.4.1 Class Declaration ###
* The opening brace **MUST** be on its own line beneath the class name, at the same level of indentation as the class declaration.
* All code in the class **MUST** be indented one level in addition the indentation level of the class declaration.
* Every class **MUST** contain a documentation block that precedes the class declaration.
* PHP files declaring classes **MUST** contain a single class only.

```
#!php5
<?php
/**
 * Sample class
 */
class ExampleClass
{
    // code here
}
?>
```

### 4.4.2 Class Member Variables ###
* Member variables **MUST** be declared at the top of the class, above the declaration of any methods.
* The _var_ construct **MUST NOT** be used.
* Member variables **MUST** declare their visibility by using on of the visibility modifiers: _private_, _protected_, or _public_.
* _Public_ member visibility **MAY** be used but is discouraged in favor of accessor methods: _set_ and _get_.

```
#!php5
<?php
/**
 * Sample class
 */
class ExampleClass
{
	protected $strAdminEmail = null;
	protected $strLogFile = null;
	private $_boolLog = false;

    public function __construct($aryOptions) {
		$this->_setConfigurations($aryOptions);
	}
}
?>
```

## 4.5 Functions/Methods Declaration ##
* Class Methods **MUST** declare their visibility by using on of the visibility modifiers: private, protected, or public.
* The opening brace **MUST** be on its own line beneath the function/method name, at the same level of indentation as the method/function declaration.
* A space **MUST NOT** be inserted between the function/method name and the opening parenthesis for the arguments.
* Line breaks **MAY** be used if the argument list exceeds the maximum line length

```
#!php5
<?php
/**
 * Sample class
 */
class ExampleClass
{
	protected $strAdminEmail = null;
	protected $strLogFile = null;
	private $_boolLog = false;

    public function __construct($aryOptions)
    {
        $this->_setConfigurations($aryOptions;
    }

    public function exampleMethod($aryArg1, $aryArg2)
    {
        $this->_exampleProtected($aryArg1, $strArg2);
    }

    protected function _exampleProtected($aryArg1, $strArg2)
    {
        // code here
    }

    private function _setConfigurations($aryOptions)
    {
        // code here
    }
}
?>
```

## 4.6 Function/Method Usage ##
* Function/method arguments **MUST** be separated by a single space after the comma delimiter.

```
#!php5
<?php
$arySample = someFunction($aryArg1, $strArg2, $boolArg3);

$objSample = new ExampleClass($arySample);
$objSample->exampleMethod($aryArg1, $aryArg2);
?>
```

## 4.7 Control Statements ##
* Control statements **MUST** use the logical operators '&&' and '||'
* The opening brace **MUST** be written on the same line as the conditional statement if the conditional statement does not contain a line feed.
* The closing brace **MUST** be written on its own line.
* Opening parentheses for control structures **MUST NOT** have a space after them, and closing parentheses for control structures **MUST NOT** have a space before.
* Any content within the braces **MUST** be indented  four spaces from the control statement.
* Within the conditional statements between the parentheses, operators **MUST** be separated by spaces for readability.
* Control statements **SHOULD** use Yoda notation.
* Inner parentheses **SHOULD** be used to improve logical grouping for larger conditional expressions.
* Long control statements **MAY** be split onto several lines when the character/line limit would be exceeded.
    * The conditions **MUST** be positioned onto the following line, and indented 4 spaces.
    * Logical operators (&&, ||, etc.) **SHOULD** be at the beginning of the line.

```
#!php5
<?php
if(SOME_CONST == $strB){
    $boolA = TRUE;
} else {
    $boolA = FALSE;
}

if(($strA == $strB)
    && ($strC !== $strA)
){
    // code here
} elseif($strD == $strC){
    // code
} else {
    // more code
}

if(    is_int($intA)
    || is_int($intB)
    || is_int($intC)
){
    // code here
}
?>
```

### 4.7.1 Switch ###
* Content within the _switch_ statement **MUST** be indented one indentation level greater than the switch declaration.
* Content within each _case_ statement **MUST** be indented one indentation level greater than the case statement.
* Construct _default_ **MAY** be omitted from a _switch_ statement but **MUST** contain a comment indicating deliberate omission.
* In the case of fallthrough, code **MUST** include a comment indicating that the omission of _break/return_ was intentional.
```
#!php5
<?php
switch($intFoo){
    case 1:
        // code here
        break;
    case 2:
        // break intentionally omitted
    case 3;
        // code here
        break;
    // default intentionally omitted.
}
?>
```

## 4.7.2 Ternary operators ##
* Ternary operators **MAY** be used but **MUST** adhere to the same requirements for other control statements.
* Ternary operators **SHOULD NOT** be nested.
```
#!php5
<?php
$strExample = (empty($strC)) ? $strA : $strB;
?>
```

## 4.8 Exceptions ##
* Exceptions **MUST** follow the same conventions as classes.
* Exceptions **MUST** extend one of PHP's SPL Exception types.

```
#!php5
<?php5
use Exception;

/**
 * Example Exception class
 */
class SampleException extends Exception
{
    // code here
}
?>
```

## <a name="inlinedocs"></a> 4.9 Inline Documentation ##
### 4.9.1 Format ###
* Documentation blocks **MUST** be compatible with phpDoc format (http://phpdoc.org/).
* In addition to docblocks, inline documentation **MAY** be used anywhere in the code
    * Single line comments **SHOULD** use C++ style comments (`//`)
    * Multiline comments **MUST** use block comments (C style `/* */`)

```
#!php5
<?php
// single line comment

/*
* Example of a multiline comment. Lorem ipsum dolor sit amet, error dolore usu ad, his ei tation facilis maluisset,
* nisl tantas invidunt mei ne. Detracto interpretaris ex pri. Qui dicit interpretaris ex. At esse viris pri, sea ei
* novum erroribus. Brute corrumpit ne eum. Te his hinc adolescens.
*/
?>
```

### 4.9.2 Files ###
* Every file containing PHP code **MUST** have a docblock at the top of the file.
* Each file docblock **MUST** contain:
    * Short description
    * `@author <author>, Web Communications, University of Missouri`
    * `@copyright <year> Curators of the University of Missouri`
* Each file docblock **SHOULD** contain:
    * Long description
    * `@version`

```
#!php5
<?php
/**
 * Retrieves events from the Localist instance of the MU calendar and converts them to consumable event objects/arrays
 *
 * @author Truman Tiger, Web Communications, University of Missouri
 * @copyright 2014 Curators of the University of Missouri
 * @version 1.1
 */
?>
```
### 4.9.3 Classes ###
In addition to the file docblock, each class **MUST** have a docblock that contains a Long description.
### 4.9.4 Functions/methods ###
* Every function/method **MUST** have a docblock that contains:
    * Short description
    * `@param` for every argument
    * `@return` (even if set to void)
* Function/method docblocks **SHOULD** contain:
    * Long description
    * `@throws` if the function/method throws an exception

```
#!php5
<?php
	/**
	 * Converts the date to the format as defined in @see this->aryOptions[date_format]
	 *
	 * @param string $strDate
	 * @return string
	 * @throws CalendarException
	 */
	protected function _verifyDate($strDate)
    {
        // code here
    }
?>
```

### 4.9.5 Constants ###
Each constant **SHOULD** have a docblock that contains a short description

```
#!php5
<?php
    /**
    * Container should never be smaller than this number.
    */
    const MINSIZE = 50;
?>
```

### 4.9.6 Variables/members ###
Each variable/member **SHOULD** have a docblock that contains:

* Short description
* `@var` data type

```
#!php5
<?php
    /**
     * Valid methods of querying the localist API
     * @var array
     */
    protected $aryValidMethods = array(
		'search'    => 'search',
		'department'=> 'group_id', //per localist, this should be used for departments
		'type'      => 'type',
		'group'     => 'group_id',
		'keyword'   => 'keyword'

	);
?>
```

**Next**: [Philosophy](Coding Standards 5. Philosophy)

**Previous**: [Naming Conventions](Coding Standards 3. Naming Conventions)
