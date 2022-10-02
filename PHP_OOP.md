# OOP(Object Oriented Programming)

PHP OOP Syntax 저장소입니다.

<br>

## Contents

<br>

## [Ⅰ. 클래스 기초](#class)

## [Ⅱ. 정적 메서드와 늦은 정적 바인딩(Static)](#static)

<br>

<br><br>

## [메인페이지로 돌아가기](README.md)

<br>

---

<br>

## ✒️ 클래스 기초

<br>

### Class

```
/*
 * Define Class
 */

class A {
    ...
}


/*
 * Create a new Instance
 */

$a = new A();
```

<br>

### Features

```
/*
 * Properties and Methods
 */

class A {
    public $message = 'Hello, world';

    public function foo() {
        return $this->message;
    }
}

$a = new A();
var_dump($a->foo());  // "Hello, world"


/*
 * Inherit
 */

class B extends A {

}

$b = new B();
var_dump($b->foo());  // "Hello, world"


/*
 * in Functions
 */

function foo(A $a) {
    return $a->foo();
}

var_dump(foo($a));  // "Hello, world"
var_dump(foo($b));  // "Hello, world"


/*
 * Context
 */

class C extends A {
    public function foo() {
        return new self();  // C
        // return new static();  // D
        // return new parent();  // A
    }
}

class D extends C {

}

$d = new D();
var_dump($d->foo());


/*
 * Constants
 */

class E {
    const MESSAGE = 'Hello, world';

    public function getConstants() {
        return self::MESSAGE;
    }

    public function getClassName() {
        return __CLASS__;
    }
}

$e = new E();
var_dump($e->getConstants());  // "Hello, world"
var_dump(E::MESSAGE);  // "Hello, world"
var_dump($e->getClassName());  // "E"


/*
 * instanceof
 */

$d = new D();
var_dump($d instanceof C);  // bool(true)
var_dump($d instanceof A);  // bool(true)
var_dump($d instanceof E);  // bool(false)
```

<br>

### Anonymous Classes (익명 클래스)

```
/*
 * Anonymous Classes
 */

class A {
    public function foo() {}
}

class B {
    public function create() {
        return new class extends A {};
    }
}

$b = new B();
var_dump($b->create()->foo());  // NULL
```

<br>

<br><br>

## [이 페이지의 맨 위로 이동](#contents)

<br><br><br>

## ✒️ 정적 메서드와 늦은 정적 바인딩 (Static)

<br>

### Static

```
/*
 * Static
 */

class A {
    public static $message = 'Hello, world';

    public static function foo() {
        return self::$message;
    }
}

var_dump(A::foo());
var_dump(A::$message);
```

<br>

### Static Binding

```
/*
 * Static Binding
 */

class A {
    pubilc static function foo() {
        static::who();
    }

    public static function who() {
        var_dump(__CLASS__);
    }
}

class B extends A {
    public static function test() {
        parent::foo();
    }

    public  static function who() {
        var_dump(__CLASS__);
    }
}

$b = new B();
$b->test();  // "B"
```

<br>
