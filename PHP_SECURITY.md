# PHP Security

보안을 잊지 마세요.

<br>

## Contents

<br>

## [Ⅰ. Error Reporting](#phpini)

<br>

## [Ⅱ. File](#file-uploads)

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

## - File Uploads

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

## - File Downloads

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
