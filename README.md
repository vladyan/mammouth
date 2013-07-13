# Mammouth - Unfancy PHP #
Mammouth is a small language that compiles into PHP, inspired by CoffeeScript. It's compiled to PHP codes/files that you can run in your PHP server.

## Installation ##
Via npm:
```
npm install mammouth
```

## Usage ##
Once installed, you should have access to the coffee command, which can execute scripts, compile `.mammouth` files into `.php`. The coffee command takes the following options: 
```
Usage: mammouth [options] [dir|file ...]

Options:
  -c, --compile        Compile a ".mammouth"  or  into a .php file of the same name(can compiles a folder).
  -o, --output [DIR]   Write out all compiled PHP files into the specified directory. Use in conjunction with --compile

Examples:

  # Compile 'codes.mammouth' to 'codes.php' in the same folder
  $ mammouth --compile codes.mammouth

  # Compile all mammouth files in 'codes' folder to 'result' folder
  $ mammouth --compile --output /result /codes
```

You can compile mammouth script from browser by adding `mammouth.js` in `/extras` to your html page, and call compile function:
```javascript
mammouth.compile("<your mammouth code as string>"); //return PHP result
```

As node module, you can use the following code:
```javascript
mammouth = require('mammouth');
mammouth.compile("<your mammouth code as string>"); //return PHP result
```

## Syntax ##
###Basic Mammouth Syntax###
A mammouth script can be placed anywhere in the document.
A mammouth script starts with `{{` and ends with `}}`:
```
{{
// Mammouth script
}}
```
for example is converted to `<?php ?>`
The default file extension for PHP files is `.mammouth`, but you can use `.mmt`.
A mammouth file normally contains HTML tags, and some mammouth scripting code.

Below, we have an example of a simple mammouth file, with a mammouth script that sends the text "Hello World!" back to the browser:
```html
<!DOCTYPE html>
<html>
<body>

<h1>My first mammouth page</h1>

{{
echo("Hello World!")
}}

</body>
</html> 
```
This example is compiled to:
```html
<!DOCTYPE html>
<html>
  <body>
    <h1>My first mammouth page</h1>
<?php
echo("Hello World!");
?>
  </body>
</html> 
```

###Variables###
In PHP, a variable starts with the $ sign, followed by the name of the variable, but in mammouth variable is like Javascript:
```
{{
variable1 = true
number1 = 10
number2 = 1
variable2 = (number2-15)/number1
}}
```
The result will be:
```html
<?php 
$variable1 = true;
$number1 = 10;
$number2 = 1;
$variable2 = ($number2 - 15) / $number1;
?>
```
Variable can not take the current name: `and`, `breal`, `case`, `else`, `false`, `true`, `for`, `if`, `in`, `new`, `null`, `of`, `or`, `switch`, `then`, `this` and `while`.

###Array###
The mammouth literals for arrays look very similar to their JavaScript.
```
{{
list = [1,2,3,4,5,6,7,8,9]
}}
```
The result will be:
```html
<?php 
$list = array(1,2,3,4,5,6,7,8,9);
?>
```
###If/Else Assignment###
If/else statements can be written without the use of parentheses and curly brackets. As with functions and other block expressions, multi-line conditionals are delimited by indentation.
```
{{
if(happy and knowsIt)
	clapsHands()
	chaChaCha()
else
	showIt()

date = friday ? sue : jill
}}
```
This example is compiled to:
```html
<?php 
if($happy && $knowsIt) {	
	clapsHands();
	chaChaCha();
} else {	
	showIt();
}
$date = $friday ? $sue : $jill;
?>
```

###Switch statements###
Switch statements in PHP are a bit awkward. You need to remember to break at the end of every case statement to avoid accidentally falling through to the default case. Mammouth prevents accidental fall-through, and can convert the switch into a returnable, assignable expression. The format is: `switch` condition, `case` clauses, `else` the default case.
```
{{
switch day
  case "Mon" 
    go(work)
  case "Tue" 
    go(relax)
  case "Thu" 
    go(iceFishing)
  case "Fri"
    go("girlfriend ;)")
  case "Sun" then 
    go(church)
  else 
    go(work)
}}
```
This example is compiled to:
```html
<?php 
switch($day) {
  case 'Mon': 
    go($work);
    break;
  case 'Tue': 
    go($relax);
    break;
  case 'Thu': 
    go($iceFishing);
    break;
  case 'Fri': 
    go('girlfriend ;)');
    break;
  case 'Sun': 
    go($church);
    break;
  default:  
    go($work);
}
```
##Change Log##
**0.1.0** -12/08/2013
The initial version of Mammouth