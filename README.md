# Modern-Developer-JavaScript-Style-Guide

Or how to write JavaScript (and, by extension, similar programming languages) to make your life easier and other's too.

## Table of Contents

1. [Indentation](#indentation)
1. [Line length](#line-length)
1. [Naming](#naming)
1. [Spacing](#spacing)
1. [Curly braces { }](#curly-braces--)
1. [Compound assignment operators and Unary operators](#compound-assignment-operators-and-unary-operators)
1. [Comparisons](#comparisons)
1. [Quotes](#quotes)
1. [Properties](#properties)
1. [Variable declarations](#variable-declarations)
1. [Functions](#functions)
1. [Comments](#comments)
1. [Code organization](#code-organization)
1. [Break, continue, and return statements](#break-continue-and-return-statements)
1. [Looping array elements and object properties](#looping-array-elements-and-object-properties)
1. [Strict Mode](#strict-mode)
1. [`.editorconfig` file](#editorconfig-file)

## Indentation

* Indent every block `{ }` using 2 spaces (soft tabs).

```js
function addition(max) {
••var sum = 0;
••var i;
••
••for (i = 0; i < max; i++) {
••••sum = sum + i;
••}
••
••return sum;
}
```
## Line length

* The maximum line length should be 80 characters. If the line goes beyond that limit, you can wrap the line immediately after an operator, such as +, -, &&, ||, comma, etc. Vertically align the next line with the items that were interrupted.

```js
function setPreferences( preference1, preference2, preference3, preference4,
                         preference5, preference6 ) {
    var default = 1;

    if (preference1 === 1 && preference2 > 0 && preference3 < preference4 &&
        preference5 < preference6) {
        // Do something
    }
}
```
## Naming

* Use `camelCase` for variable, function, and parameter names. [More info](http://c2.com/cgi/wiki?CamelCase)

```js
var result;
var phoneNumber;
var numberOfCars;
function buildObject() {};
function findNeedleInAHaystack(needle, haystack) {};
```

* Use upper camel case `PascalCase` for function constructor names (i.e. Class names).

```js
function ImageSprite(imageName) {
  this.image = imageName;
}

var tile = new ImageSprite('tile.png');
```

* Avoid leading or trailing underscores in names.

* For file names use the `sneak_case`, all lowercase and `_` instead of spaces:

```
main.js
my_module.js
any_other_possible_file_name.js
```

* This way we will be sure that no case-sensitive/insensitive problems arise between different OS.

## Spacing

* Always 1 space before opening a block `•{`.
* Always 1 space before opening parenthesis in `for•(`, `while•(`, `switch•(` statements.
* No space before opening parenthesis for arguments in functions `function•foo(`.
* Always 1 space between parts in expressions: `x•=•1•+•1`, `text•===•'hello'`, `found•&&•a•<•b`.
* No space after `(` or before `)`: `if ((a === b || c === d) && e === f) {`

Example:

```js
function func(x) {
  var y = x * x;
  
  if (x < 0) {
    y = -y;
  }
  
  return y;
}
```

## Curly braces { }

* Open the curly brace at the same line of a sentence: `for (...) {`, `if (...) {`, etc.
* Close the curly brace always at a new line.
* Write the `else` always right after the `}` without any new line.

```js
function min(x, y, z) {
  var min;
  
  if (x < y) {
    if (x < z) {
      min = x;
    } else {
      min = z;
    }
  } else {
    if (y < z) {
      min = y;
    } else {
      min = z;
    }
  }
  
  return min;
}
```

* Always use curly braces in `if`, `for`, `while`, even if you are only going to include one statement.

```js
// Not recommended:
while (i > 0) i--;

// Recommended:
while (i > 0) {
  i--;
}
```

## Compound assignment operators and Unary operators

Pick whatever you feel more comfortable with, but be consistent:

```js
s = s + "string";
n = n * 100;
d = d / 10;

// or

s += "string";
n *= 100;
d /= 10;
```

```js
i = i + 1;
i = i - 1;

// or

i++;
i--;
```

## Comparisons

* Always use `===` instead of `==`.
* Always use `!==` instead of `!=`.

This will help you maintain data type integrity throughout your code.

More info about the [x == y and x === y](http://www.ecma-international.org/ecma-262/5.1/#sec-11.9.3) algorithms.

As an exception, `==` and `!=` are OK when comparing to `null` because it will be comparing to `undefined` at the same time:

```js
/**
 * This is a function that, given a number x and a number y, it returns x + y.
 * When y is undefined or null, it returns x + 1 as default.
 */
function add(x, y) {
  var result;

  if (y != null) {
    result = x + y;
  } else {
    result = x + 1;
  }
  
  return result;
}

add(5,0); // 5 + 0 = 5
add(5,1); // 5 + 1 = 6
add(5,2); // 5 + 2 = 7
add(5); // 5 + 1 = 6 (y is undefined, takes the default action)
add(5, null); // 5 + 1 = 6 (y is null, takes the default action)
```

## Quotes

* Use simple quotes `'`.
* If you decide to use double quotes `"` for whichever reason, be consistent.

## Properties

* Access properties using dot notation `.`:

```js
var person = {
  name: 'John',
  surname: 'Smith'
};

console.log(person.name + ' ' + person.surname); // John Smith
```

* Access properties with a variable using subscript notation `[]`:

```js
var person = {
  name: 'John',
  surname: 'Smith'
};
var property1 = 'name';
var property2 = 'surname';

console.log(person[property1] + ' ' + person[property2]); // John Smith
```


## Variable declarations

* Declare variables with `var`, always.
* Declare variables at the top of their scope.
* Declare variables with initial values first.
* Declare one variable per line using semicolons.

```js
function intersection(array1, array2) {
  var result = [];
  var length1 = array1.length;
  var length2 = array2.length;
  var i;
  var j;
  
  for (i = 0; i < length1; i++) {
    for (j = 0; j < length2; j++) {
      if (array1[i] === array2[j]) {
        result.push(array1[i]);
      }
    }
  }
  
  return result;
}
```

## Functions

* When writing a function expression, name it: Debugging will be easier because you will identify the function in the stack trace.

```js
// Not recommended
var print = function (message) {
  console.log(message);
}

// Recommended
var print = function print(message) {
  console.log(message);
}
```

## Comments

### FIXME and TODO

* Use `// FIXME:` to highlight problems, and `// TODO:` to highlight solutions or future additions:

```js
function countElements(elements) {

  // TODO: we should return an actual count
  return 10;
}

function countElements(elements) {
  var count = 0;
  
  // FIXME: count result is not good
  while (elements.hasNext()) {
    elements.next();
    count++;
  }

  return count;
}
```

### Add `else` comments

* This is not a must but a recommendation that will save you time when revisiting complex code. Look at these examples:

```js
if (a > 0) {

} else { // (a <= 0)

}
```

```js
if (inbox.hasMessages()) {

} else { // inbox is empty

}
```

* If you find this helpful for you, add comments also to complex conditions because this will be helpful for other humans too.

## Code organization

* Your code should, as long as possible, follow this structure:

```js
// Declarations with initialization (one declaration per line;)
// Declarations without initialization (one declaration per line;)
// Blank line
// Statements...
// [Optionally if you are writing a function and a return is needed, write it at the last line
// Blank line
// Return
// ]
```

Example with comments:

```js
function build(messages) {
  // Declaration with initialization value
  var output = "";
  // Declaration without initialization value
  var i;

  // Statements  
  for (i = 0; i < messages.length; i++) { // Statements
  	output = output + messages[i].body;
  }
  
  // Return (when needed)
  return output;
}
```

## Break, continue, and return statements

* Avoid `break` and `continue` statements. All algorithms can be written without these statements.
* Write as less `return` (exit points) statements as possible. Ideally one `return` at the end of the function would be perfect.

```js
// NOT RECOMMENDED (2 returns):
function isPalindrome(word) {
  var i = 0;
  var j = word.length;
  
  while (i < j) {
    if (word[i] !== word[j]) {
      return false;
    }
    i = i + 1;
    j = j - 1;
  }
  
  return true;
}

// NOT RECOMMENDED (break):
function isPalindrome(word) {
  var i = 0;
  var j = word.length;
  var palindrome = true;
  
  while (i < j) {
    if (word[i] !== word[j]) {
      palindrome = false;
      break;
    }
    i = i + 1;
    j = j - 1;
  }
  
  return palindrome;
}

// RECOMMENDED:
function isPalindrome(word) {
  var i = 0;
  var j = word.length;
  var palindrome = true;
  
  while (palindrome && i < j) {
    if (word[i] !== word[j]) {
      palindrome = false;
    }
    i = i + 1;
    j = j - 1;
  }
  
  return palindrome;
}
```

* `break` can be used in `switch` statements.

## Looping array elements and object properties

* When looping over array elements, use this construct:

```js
var arr = [0,1,2,3,4];

for (var i = 0; i < arr.length; i++) {
  console.log(arr[i]);
  // ...
}
``` 

* When looping over object properties, use this construct:

```js
var person = {
  name: 'John',
  age: 22,
  gender: 'Male'
};

for (var prop in person) {
  console.log(person[prop]);
  // ...
}
```

* Do not iterate over array objects using the `for-in` construct, because arrays may have more properties than just their indexes.

## Strict mode

This directive allows you to improve the overall quality of your code by avoiding minor errors like the use of undeclared variables. 

* The first line of code of every file should be `"use strict";`.
* The strict mode directive should be followed by a blank line.

```js

// content of my_module.js

"use strict";

var myModule = (function() {
  
  // module content
  
})();
```

* Find more information about this directive here: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode

## `.editorconfig` file

* The `.editorconfig` file helps developers define and maintain consistent coding styles between different editors and IDEs.
* It makes cooperation with others programmers seamless because all share the same style rules.
* The `.editorconfig` file is usually placed in the root of your project folder.
* Not all editors require of a plugin to support an `.editorconfig` file.
* Below you have a recommended `.editorconfig` file for you with all configurations mentioned in this style guide:

```ini
root = true

[*.js]
charset = utf-8
end_of_line = lf
indent_style = space
indent_size = 2
indent_brace_style = 1TBS
insert_final_newline = true
continuation_indent_size = 2
curly_bracket_next_line = true
space_after_anonymous_functions = true
space_after_control_statements = true
spaces_around_operators = true
spaces_in_brackets = false
trim_trailing_whitespace = true
quote_type = single
```

* There are universal [properties](https://github.com/editorconfig/editorconfig/wiki/EditorConfig-Properties) (supported by all editors) and others supported only by a few editors.
* Find more information about editor support and plugins visit the official [project website](http://editorconfig.org/).


