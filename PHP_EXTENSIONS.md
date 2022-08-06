# PHP Extensions (PHP Core Extensions)

자주 사용하는 PHP 내장함수 저장소입니다.

<br>

## Contents

## [Ⅰ. PHP Options/Info Functions](#php-optionsinfo-functions)

### - php extension
### [1. extension_loaded]
### [2. get_loaded_extensions]

### - include path
### [3. set_include_path]


### - include files

### - php information

### - php.ini

### - environment variables

<br><br>
## [메인페이지로 돌아가기](README.md)
<br>

-----

<br>

## PHP Options/Info Functions

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

### 6. get_included_files

: Returns an array with the names of included or required files

```
get_included_files(): array
```

<br>

### 7. phpinfo

: Outputs information about PHP's configuration

```
phpinfo(int $flags = INFO_ALL): bool
```

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