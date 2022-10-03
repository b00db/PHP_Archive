# PHP Security

보안을 잊지 마세요.

<br>

## Contents

<br>

## [Ⅰ. Error Reporting](#1-displayerrors--off)

## [Ⅱ. File](#file-uploads)

## [Ⅲ. Sessions](#cookie)

<br>

<br><br>

## [메인페이지로 돌아가기](README.md)

<br>

---

<br>

## ✒️ Error Reporting

<br>

## - PHP.ini.

### 1. display_errors = Off

### 2. error_reporting = 0

<br>

## - ini_set()

### 1. ini_set('display_errors', 'Off');

<br>

## - error_reporting()

### 1. error_reporting(0); // error level

<br>

## - set_error_handler()

### 1. set_error_handler((function () {}));

<br>

<br><br>

## [이 페이지의 맨 위로 이동하기](#contents)

<br><br><br>

## ✒️ File

<br>

### File Uploads

```
switch ($_SERVER['REQUEST_METHOD']) {
    case 'GET':
        echo <<<'HTML'
            <form action="/" method="POST" enctype="multipart/form-data">
                <input type="file" name="uploads">
                <input type="submit">
            </form>
            HTML;
        break;
    case 'POST':
        $file = $_FILES['uploads'];
        $pathinfo = pathinfo($file['name]);
        $accepts = [
            'png', 'jpg'
        ];
        if (in_array(strtolower($pathinfo['extension']), $accepts) && is_uploaded_file($file['tmp_name'])) {
            move_uploaded_file($file['tmp_name'], dirname(__FILE__) . '/uploads/' . $file['name']);
        }
        break;
    default:
        http_response_code(404);
}
```

<br>

### File Downloads

```
$path = filter_input(INPUT_GET, 'path', FILTER_SANITIZE_STRING);
$filepath = realpath(dirname(__DIR__). '/uploads/' . basename($path));

if (file_exists($filepath)) {
    $pathinfo = pathinfo($filepath);
    $accepts = [
        'png', 'jpg'
    ];
    if (in_array(strtolower($pathinfo['extenstion']), $accepts)) {
        header('Content-type: application/octet-stream');
        header('Content-Disposition: attachment; filename= ' . basename($path));
        header('Content-Transfer-Encoding: binary');
        header('Content-Length: ' . filesize($path));

        readfile($path);
    }
}
```

<br>

<br><br>

## [이 페이지의 맨 위로 이동하기](#contents)

<br><br><br>

## ✒️ Sessions

<br>

### Cookie

```
/*
 * php.ini
 *
 * /?PHPSESSID=123456789
 *
 * session.use_strict_mode = 1
 *
 * session.use_cookies = 1
 * session.use_only_cookies = 1
 */
```

<br>

### Javascript Injection

```
/*
 * php.ini
 *
 * session.cookie_httpOnly = 1
 */
echo '<script>document.write(document.cookie)</script>';
```

<br>

### Https

```
/*
 * php.ini
 *
 * session.cookie_secure
 */
```

<br>

### Cookie time, GC

```
/*
 * php.ini
 *
 * session.gc_maxlifetime
 */

session_save_path(dirname(__DIR__) . '/sessions');

ini_set('session.gc_maxlifetime', 3);
session_set_cookie_params(3);

session_start();
session_gc();
```

<br>

### Timestamp based session

```
$_SESSION['timestamp'] = $_SERVER['REQUEST_TIME'];

// sleep(10);
$time = strtotime('+10 seconds');

$diff = $time - $_SESSION['timestamp'];
$sessionTimeOut = 10;

if ($diff >= $sessionTimeOut) {
    echo 'Session Timeout';
    exit;
}
```

<br>

### Renewal session

```
session_regenerate_id();
$_SESSION['timestamp'] = time();
```
