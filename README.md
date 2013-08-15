# Coding Guidelines

These guidelines are those that work best for me and I strive to have all my personal projects follow. Additionally, these guidelines should be followed when submitting code in a pull request to any of my projects hosted on GitHub.

> These guidelines were ripped from the [SprayFire](http://github.com/cspray/SprayFire) project; the guidelines are being cleaned up and having all references to SprayFire removed.

## Introduction

Every stable project must have a consistent, clean coding style and convention to survive the eventual refactors and to make for an easily maintained code base. Code style is *very important*.

For the sake of brevity this page is split into two sections: Coding Standards and Documentation Standards.

## Coding Standards

### Indentation and tabs versus spaces

Spaces over tabs. Indentation depth should be 4 spaces per indentation.  Top level indentation should be flush with the left edge of the editor. Generally this will mean `namespace`, `use` statements and `class` declaration at level 1, `class` members at level 2, method implementation at level 3, etc.

The reason for this spaces over tabs is that I like to look at code in a variety of environments; some of those environments I don't necessarily have control over tab width and spaces don't have that problem.

---

### Quotes

There are no hard-set rules in place regarding the use of quotes. Generally though we will use single quotes around values unless it makes sense to have multiple variables expanded in double quotes.

The primary aspect to consider with quotes is that modules should follow a consistent quoting strategy.

---

### Operators

Binary operators should have a space before and after the operator, (e.g. `$foo = 'bar'`).  Unary operators, such as `++`, do not require a space, (e.g. `$foo++`).

---

### Casting

Any time a variable needs to be cast there should be a space between the casting and the variable, (e.g. `(int) $foo`).

---

### Conditionals

Conditional statements should have a space between the keyword and the expression being checked. Conditional statements should *always* have enclosing brackets, even if the statement being executed for that condition is one line. In code statements braces should be used, in framework provided templates PHP's [alternative syntax](http://php.net/manual/en/control-structures.alternative-syntax.php) can be used.  In conditional statements involving `if/elseif` the syntax with no space between `else` and `if` is preferred.

#### Code Conditionals

```php
<?php

    if ($foo === 'something') {
        // do something
    } elseif ($foo === 'something else') {
        // do something else
    } else {
        // do something by default
    }


    switch ($foo) {
        case '1':
            // something
        default:
            // default
    }

?>
```

#### Template Conditionals

```php
<?php

    if ($foo === 'something'):
        // output something
    elseif ($foo === 'something else'):
        // output something else
    else:
        // output some default value
    endif;

?>
```

---

### Method Calls

There should be no space between the function call and the opening parentheses, with arguments being separated by a space after the comma, but no space after the opening parentheses or before the closing parentheses (e.g. `$Class->doSomething($foo, $bar)`).

---

### Class Constructor Calls

These calls should be similar to Method Calls. Additionally, there should always be an opening and closing parantheses, even when no arguments are passed.

---

### Constants

Constants should be all upper-case with words separated by underscore characters, (e.g. `DEUBUG_MODE`). Preferably there will be no global constants, anytime a constant is added it should  belong to some class or interface that makes sense for the constant.

---

### Methods and Variables

Variables and methods should both use `camelCase` style naming and be descriptive of what they are containing or doing.  If a variable holds an object it should be `PascalCase` style. Methods should have their arguments separated by a space after each comma, but not between the arguments and the opening and closing parentheses.

```php
<?php

class MethodVarExample {

    protected $nonObjectProperty;

    private $ObjectProperty;

    public function __construct($nonObject, $Object) {

    }

    public function doSomeFoo($bar, $baz) {

    }

}

?>
```

---

### Brace Style

Brace style should follow the [1TBS](http://en.wikipedia.org/wiki/Indent_style#Variant:_1TBS).

```php
<?php

function fooBar() {
    if ($foo) {
        echo 'foo';
    } else {
        echo 'bar';
    }
}

?>
```
---

## Documentation Standard

### Basic Guidelines

- Document your code in English.
- If a method has a parameter, returns a value or throws an exception it should have a doc-block attached to it with appropriate parameters.
- Simple getter and setter methods do not require a detailed explanation, simply some doc-block saying what the getter returns or setter expects as a parameter.
- Limit inline documentation as much as possible. When it is used it should be to clarify some "clever" code or workaround that doesn't "feel" right but should be kept in place due to a bug fix or some other real-life reasoning.
- If a block of code cannot be reasonably covered by unit tests we should include the appropriate inline PHPUnit annotation to ensure that the code is ignored during code coverage. Typically this should also include the reasoning behind ignoring the block of code.

### Documenting files

All files should be documented immediately after the opening `<?php` and before any code.  The doc-block should be flush to the left margin of the file with `*` separating the opening `/**` and closing `*/` of the block.  An example file doc-bock:

```php
<?php

/**
 * This is a short sentence that tells what code the file is holding.
 *
 * If needed these are more details about the file that may be important to the developer
 * or details some more information about why certain things were done a certain way.
 *
 * @author <Your Name>
 * @license <Details about the license>
 */

// your code starts here
?>

### Documenting classes

Class doc-blocks are not necessary unless the class has some highly specific details that cannot fit into the description of the file level doc.

### Documenting methods

The method level doc-block should provide whatever Javadoc annotations are neccessary to cover all possible method parameters, returns, throws and side effects.

```php
<?php

    // class doc-block and class declaration up here

    /**
     * Do some stuff with $Something that effects the Doohickey to use.
     *
     * We could explain in here some details about the method or why we chose a specific
     * implementation.
     *
     * @param \YourApp\Core\SomethingElse
     * @param boolean $someFlag
     * @return string
     * @throws \InvalidArgumentException
     * @throws \RangeException
     */
    public function doStuffWithSomething(\YourApp\Core\SomethingElse $Something, $someFlag = true) {
        //...
    }

?>
```

### Documenting properties

```php
<?php

    // class declaration up here

    /**
     * If necessary, a description of the property
     *
     * @property array
     */
    protected $someProperty = array();

    /**
     * @property \YourApp\Something\Object
     */
    private $AnObject;

?>
```
