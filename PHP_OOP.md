# OOP(Object Oriented Programming)

PHP OOP Syntax 저장소입니다.

<br>

## Contents

<br>

## [Ⅰ. 클래스 기초](#class)

## [Ⅱ. 정적 메서드와 늦은 정적 바인딩(Static)](#static)

## [Ⅲ. 상속](#생성자와-소멸자)

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
```

```
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

<br><br>

## [이 페이지의 맨 위로 이동](#contents)

<br><br><br>

## ✒️ 상속 (Inheritance)

<br>

### 생성자와 소멸자

```
/*
 * Constructor, Destructor
 */

class A {
    public function __construct() {
        var_dump(__METHOD__);
    }

    public function __destruct() {
        var_dump(__METHOD__);
    }
}

$a = new A();
var_dump('Hello, world');

/*
 * "A::__construct"
 * "Hello, world"
 * "A::__destruct"
 */


 $a = new A();
 unset($a);
 var_dump('Hello, world');

/*
 * "A::__construct"
 * "A::__destruct"
 * "Hello, world"
 */
```

```
/*
 * Constructor Parameters
 */

class B {
    public $message;

    public function __construct($message) {
        $this->message = $message;
    }
}

$b =  new B('Hello, world');
```

```
/*
 * Inherit
 */

class C extends A {
    public function __construct() {
        parent::__construct();
    }

    public function __destruct() {
        parent::__destruct();
    }
}

$c = new C();
```

<br>

### Final

```
/*
 * Final
 */

class A {
    public $message;

    public final function foo() {
        // 상속 시 오버라이드(재정의) 금지
    }
}

final class B {
    // 상속 금지 (상속을 막을 때 사용)
}
```

<br>

### 가시성

```
/*
 * Visibility
 */

class A {
    public $public = 'public';
    protected $protected = 'protected';
    private $private = 'private';
}

$a = new A();
var_dump($a->public);  // (o)
var_dump($a->protected);  // (x)
var_dump($a->private);  // (x)

class B extends A {
    public function foo() {
        return $this->protected;
    }
}

$b = new B();
var_dump($b->foo());  // (o)

class C {
    private $message = 'Hello, world';
    private static $instance;

    private function __construct() {
        var_dump($this->message);
    }

    public static function getInstance() {
        return new self();
    }
}

$c = C::getInstance();
```

<br>

<br><br>

## [이 페이지의 맨 위로 이동](#contents)

<br><br><br>

## ✒️ 추상화 (Abstraction)

<br>

### 추상 클래스

```
/*
 * Class Abstraction
 */

absctract class A {
    protected $message = 'Hello, world';

    public function sayHello() {
        return $this->message;
    }

    abstract public function foo();
}

// new A();  // (x) : 추상 클래스는 인스턴스화 시킬 수 없음. 상속을 받아서 처리.

class B extends A {
    public function foo() {
        return __CLASS__;
    }
}

$b = new B();
var_dump($b->foo());  // "B"
var_dump($b->sayHello());  // "Hello, world"
```

<br>

### 인터페이스

```
/*
 * Interface
 */

interface A {
    public function foo();

}

class B implements A {
    public function foo() {
        return __CLASS__;
    }
}

function foo(A $a) {
    return $a->foo();
}

$b = new B();
var_dump(foo($b));  // "B"
```

<br>

### 트레이트

: PHP는 다중 상속을 지원하지 않음. 대신 트레이트를 지원함.

```
/*
 * Trait
 */

trait A {
    public $message = 'Hello, world';

    public function sayHello() {
        return $this->message;
    }
}

trait AA {
    public function sayHello() {
        return __TRAIT__;
    }
}

trait AAA {
    use A, AA {
        A::sayHello insteadof AA;
    }
}

class B {
    // use A;
    use AAA;
}

$b = new B();
var_dump($b->sayHello());

/*
 * 우선 순위
 */

class C {
    private $message = 'Hello, world';

    public function sayHello() {
        return $this->message;
    }
}

trait D {
    public function sayHello() {
        return __TRAIT__;
    }
}

class E extends C {
    use D;

    public function sayHello() {
        return __CLASS__;
    }
}

$e = new E();
var_dump($e->sayHello());  // "E" // 여기서의 우선순위 : 재정의 -> 트레이트 -> 상속
```

<br>
