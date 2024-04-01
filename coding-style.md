



## PHP Writing Conventions

### Naming Conventions

- Use descriptive and meaningful names for variables, functions, classes, and methods.
- Variable names: camelCase or snake_case.
- Class names: PascalCase.
- Constants: UPPERCASE_WITH_UNDERSCORES.
- File and directory names: lowercase_with_underscores.

### Indentation and Formatting

- Use consistent indentation (4 spaces or tabs).
- Follow a consistent coding style.
- Proper spacing between operators and control structures.

### Comments

- Use comments to explain complex code or non-obvious behavior.
- Write clear and concise comments, focusing on why rather than what.
- Avoid unnecessary comments.

### Error Handling

- Implement proper error handling using try-catch blocks or error functions.
- Use meaningful error messages for debugging.

### Security

- Sanitize user input to prevent security vulnerabilities.
- Use parameterized queries or prepared statements for database interactions.
- Validate and sanitize input data from external sources.

### Documentation

- Document code using PHPDoc comments for classes, methods, and functions.
- Include information about parameters, return types, and exceptions.

### Consistency

- Follow consistent naming conventions, coding styles, and project struct




## WordPress convention
## visit https://developer.wordpress.org/coding-standards/wordpress-coding-standards/php/

- comments

/*********************
* Template
*
**********************/


- Opening and Closing PHP Tags
  When embedding multi-line PHP snippets within an HTML block, the PHP open and close tags must be on a line by themselves.

Correct (Multiline):

```php
function foo() {
    ?>
    <div>
        <?php
        echo esc_html(
            bar(
                $baz,
                $bat
            )
        );
        ?>
    </div>
    <?php
}
```

- No Shorthand PHP Tags
  Important: Never use shorthand PHP start tags. Always use full PHP tags.

Correct:

```php
<?php ... ?>
<?php echo esc_html( $var ); ?>

```

Incorrect:

```php
<? ... ?>
<?= esc_html( $var ) ?>
```

- Naming Conventions
  Use lowercase letters in variable, action/filter, and function names (never camelCase). Separate words via underscores. Don’t abbreviate variable names unnecessarily; let the code be unambiguous and self-documenting.

```php

function some_name( $some_variable ) {}

```

- Class, trait, interface and enum names should use capitalized words separated by underscores. Any acronyms should be all upper case.

```php
class Walker_Category extends Walker {}
class WP_HTTP {}
```

Constants should be in all upper-case with underscores separating words:

```php
define( 'DOING_AJAX', true );
```

visit https://developer.wordpress.org/coding-standards/wordpress-coding-standards/php/
to get the rest
