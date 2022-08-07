# PHP Extensions (PHP Core Extensions)

자주 사용하는 PHP 내장함수 저장소입니다.

<br>

## Contents (수정 예정)

<br>

## [Ⅰ. PHP Options/Info Functions](#php-optionsinfo-functions)

<br>

###  - php extension

### 1. extension_loaded
### 2. get_loaded_extensions

<br>

### - include path

### 3. set_include_path
### 4. get_include_path
### 5. restore_include_path

<br>

### - include files

### 6. get_included_files

<br>

### - php information

### 7. phpinfo

<br>

### - php.ini

### 8. ini_set
### 9. ini_get
### 10. ini_restore

<br>

### - environment variables

### 11. putenv
### 12. getenv

<br>

### - assert options / assert

### 13. assert_options
### 14. assert

<br>

## [Ⅱ. Error Handling and Logging](#error-handling-and-logging)

<br>

### - log
### 15. error_reporting
### 16. error_log

### - backtrace



<br>



<br><br>
## [메인페이지로 돌아가기](README.md)
<br>

-----

<br>

## PHP Options/Info Functions

<br>

## - php extension 

<br>

### 1. extension_loaded

: Find out whether an extension is loaded

```
extension_loaded(string $extension): bool
```

<br>

### 2. get_loaded_extensons

: Returns an array with the names of all modules compiled and loaded

```
get_loaded_extensions(bool $zend_extensions = false): array
```

<br>

## - include path

<br>

### 3. set_include_path

: Sets the include_path configuration option

```
set_include_path(string $include_path): string|false
```

<br>

```
** Examples

include 'mylib/HelloWorld.php';

<=>

set_include_path(__DIR__ . 'mylib');
include 'HelloWorld.php';
```

<br>

### 4. get_include_path

: Gets the current include_path configuration option

```
get_include_path(): string|false
```

<br>

### 5. restore_include_path

: restore_include_path — Restores the value of the include_path configuration option

```
restore_include_path(): void
```

<br>

## - include files

<br>

### 6. get_included_files

: Returns an array with the names of included or required files

```
get_included_files(): array
```

<br>

## - php information

<br>

### 7. phpinfo

: Outputs information about PHP's configuration

```
phpinfo(int $flags = INFO_ALL): bool
```

<br>

## - php.ini

<br>

### 8. ini_set

: Sets the value of a configuration option

```
ini_set(string $option, string|int|float|bool|null $value): string|false
```

<br>

### 9. ini_get

: Gets the value of a configuration option

```
ini_get(string $option): string|false
```

<br>

### 10. ini_restore

: Restores the value of a configuration option

```
ini_restore(string $option): void
```

<br>

## - environment variables

<br>

### 11. putenv

: Sets the value of an environment variable

```
putenv(string $assignment): bool
```

<br>

### 12. getenv

: Gets the value of an environment variable

```
getenv(string $varname, bool $local_only = false): string|false
```

<br>

```
** putenv, getenv <-> $_ENV

// Set
putenv('APP_ENV=' . 'production');
// Get
getenv('APP_ENV');

<-> 비슷해보여도 엄연히 다르다. (서로 다르게 인식한다. 즉, 서로 연관이 없다.)

// Set
$_ENV['APP_ENV'] = 'development';
// Get
$_ENV['APP_ENV'];
```

<br>

## - assert options / assert

<br>

### 13. assert_options

: Set/get the various assert flags

```
assert_options(int $what, mixed $value = ?): mixed
```

<br>

### 14. assert

: Checks if assertion is false

```
assert(mixed $assertion, Throwable $exception = ?): bool
```

<br>

```
** Example

// Active
assert_options(ASSERT_ACTIVE, true);
// Stop testing on failure
assert_options(ASSERT_BAIL, false);
// PHP Trace
assert_options(ASSERT_WARNING, true);
// Callback
assert_options(ASSERT_CALLBACK, 'assertfailure');

function assertfailure(...$args) {
    var_dump($args);
}

assert(false);
```

<br><br>

## [이 페이지의 맨 위로 이동](#contents)

<br><br><br>


## Error Handling and Logging

<br> 

## - log

<br>

### 15. error_reporting

: Sets which PHP errors are reported

```
error_reporting(?int $error_level = null): int
```

<br>

### 16. error_log

: Send an error message to the defined error handling routines

```
error_log(
    string $message,
    int $message_type = 0,
    ?string $destination = null,
    ?string $additional_headers = null
): bool
```

<br>

## - backtrace

<br>

### 17. debug_pring_backtrace

: Prints a backtrace

```
debug_print_backtrace(int $options = 0, int $limit = 0): void
```

<br>

### 18. debug_backtrace

: Generates a backtrace

```
debug_backtrace(int $options = DEBUG_BACKTRACE_PROVIDE_OBJECT, int $limit = 0): array
```

<br>

## - ignore errors

<br>

### 19. @

: Ignores PHP errors

```
function foo() {
    메롱;
}

@foo();
```

-> 프로그램이 느려지기 때문에 되도록 사용하지 않는 것이 좋다.

<br>

## - error handling

<br>

### 20. set_error_handler

: Sets a user-defined error handler function

```
set_error_handler(?callable $callback, int $error_levels = E_ALL): ?callable
```

<br>

### 21. restore_error_handler

: Restores the previous error handler function

```
restore_error_handler(): bool
```

<br>

## - trigger custom error

<br>

### 22. trigger_error

: Generates a user-level error/warning/notice message

```
trigger_error(string $message, int $error_level = E_USER_NOTICE): bool
```

<br>

```
** Examples

set_error_handler(function ($errno, $errstr) {
    switch ($errno) {
        case E_USER_ERROR:
            var_dump($errstr);
            break;
    }
});  // -> This is a E_USER_ERROR message.

trigger_error('This is a E_USER_ERROR message.', E_USER_ERROR);
```