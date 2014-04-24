# 5. Coding Philosophy ##
## 5.1 Separation of components ##
While Web Communications has not adopted an official framework, we do adhere to the philosophy of
separation of components, very similar to the [Model-View-Controller software pattern](http://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller).

* Files **SHOULD** declare new symbols (classes, functions, constants, etc.) or **SHOULD** execute logic with side effects, but it **SHOULD NOT** do both.
* Files that generate output **SHOULD NOT** have direct access to databases or external data sources.
* Code that generates output **SHOULD** be contained in template or view files.
* Display/Presentation logic **SHOULD** be contained in template or view files
* Code that interacts with external data sources **SHOULD NOT** also directly accept user input.

## 5.3 Misc ##
* All code **MUST** be E_STRICT-compatible. This means that it must not produce any warnings or errors when PHP's error reporting level is set to E_ALL | E_STRICT.
* Developers **SHOULD** test again boolean conditions, or conditions that result in a boolean state.
* Developers **SHOULD NOT** rely on php's type juggling in control structures.
```
#!php5
<?php
$arySample = functionThatReturnsAnArray();

// incorrect
if($arySample){
    // code here
}

// correct
if(is_array($arySample)){
    // code here
}
?>
```


**Previous**: [Coding Style](Coding Standards 4. Coding Style)