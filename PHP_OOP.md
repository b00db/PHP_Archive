# OOP(Object Oriented Programming)

PHP OOP Syntax 저장소입니다.

<br>

## Contents

<br>

## [Ⅰ. 클래스 기초](#class)

## [Ⅱ. 정적 메서드와 늦은 정적 바인딩(Static)](#static)

## [Ⅲ. 상속](#생성자와-소멸자)

## [Ⅳ. 추상화](#추상-클래스)

## [Ⅴ. 매직 메서드](#매직-메서드-메서드-관련)

## [Ⅵ. 네임스페이스](#네임스페이스)

## [Ⅶ. 예외](#예외)

## [Ⅷ. 제네레이터](#제네레이터)

## [Ⅸ. 참조](#참조)

## [Ⅹ. 객체 비교와 복사](#객체-비교)

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

<br><br>

## [이 페이지의 맨 위로 이동](#contents)

<br><br><br>

## ✒️ 매직 매서드 (Magic Methods)

<br>

### 매직 메서드 (메서드 관련)

```
/*
 * Magic Methods: Methods
 */

class A {
    public function __call($name, $args) {
        var_dump($name, $args);
    }

    public function __callStatic($name, $args) {
        var_dump($name, $args);
    }

    public function __invoke(...$args) {
        var_dump($args);
    }
}

$a = new A();
$a('Hello, world', 'Who are you?');  // "Hello, world", "Who are you?"

$a->foo('Hello, world');  // "foo", "Hello, world"

A::foo();  // "foo"
```

<br>

### 매직 메서드 (프로퍼티 관련)

```
/*
 * Magic Methods: Property
 */

class A {
    private $message;

    public function _isset($name) {
        return isset($this->$name);
    }

    public function _unset($name) {
        unset($this->$name);
    }

    public function __set($name, $value) {
        $this->$name = $value;
    }

    public function __get($name) {
        return $this->$name;
    }
}

$a = new A();
// isset($a->message);
// unset($a->message);

$a->message = 'Hello, world';
var_dump($a->message);
```

<br>

### 매직 메서드 (직렬화 관련)

```
/*
 * Magic Methods: Serialize
 */

class A {
    private $message = 'Hello, world';

    public function __sleep() {
        return [ 'message' ];
    }

    public function __wakeup() {
        var_dump(__METHOD__);
    }
}

$a = new A();

$serialized = serialize($a);
var_dump($serialized);  // "Hello, world"
var_dump(unserialize($serialized));  // "class A { private $message => "Hello, world" }"


class A implements Serializable {
    private $message = 'Hello, world';

    public function serialize() {
        return serialize($this->message);
    }

    public function unserialize($serialized) {
        $this->message = unserialize($serialized);
    }
}

$b = new B();

$serialized = serialize($b);
var_dump($serialized);  // "Hello, world"
var_dump(unserialize($serialized));  // "class B { private $message => "Hello, world" }"
```

<br>

<br><br>

## [이 페이지의 맨 위로 이동](#contents)

<br><br><br>

## ✒️ 네임스페이스 (Namespaces)

<br>

### 네임스페이스

```
/*
 * Namespaces
 */

namespace A {  // 파일 하나에 여러개의 네임스페이스 가능하긴 하나, 파일 하나당 네임스페이스 하나 권장
    const MESSAGE = __NAMESPACE__;

    class A {
        public function foo() {
            return __METHOD__;
        }
    }

    function foo() {
        return __FUNCTION__;
    }
}

namespace A\B {  // 자식 네임스페이스
    class A {
        public function foo() {
            return __METHOD__;
        }
    }
}

namespace {  // 글로벌 네임스페이스
    use A\A;
    use A\B\A as AB;

    $a = new A\A();
    var_dump($a->foo());  // "A\A::foo"

    $ab = new AB();
    var_dump($ab->foo());  // "A\B\A::foo"

    use function A\foo;
    var_dump(foo());  // "A\foo"

    use const A\MESSAGE;
    var_dump(MESSAGE);  "A"
}
```

<br>

<br><br>

## [이 페이지의 맨 위로 이동](#contents)

<br><br><br>

## ✒️ 예외 (Exceptions)

<br>

### 예외

```
/*
 * Exception
 */

try {
    throw new Exception('Hello, world');
} catch (Exception $e) {
    var_dump($e->getMessage());  // "Hello, world"
} finally {
    var_dump('Finally');  // "Finally"
}
```

```
set_error_handler(function ($errno, $errstr) {
    throw new ErrorException($errstr, $errno);
});

set_exception_handler(fn (Exception $e) => var_dump($e->getMessage()));
```

```
/*
 * Error
 */
try {
    new MyClass();
} catch (Error $e) {
    var_dump($e->getMessage());  // fatal error 도 처리 가능
}
```

<br>

### 예외 (상속)

```
/*
 * Exception extends
 */

class MyException extends Exception {

}

try {
    throw new MyException('Hello, world');
} catch (Exception $e) {
    var_dump($e->getMessage());  // "Hello, world"
}
```

<br>

<br><br>

## [이 페이지의 맨 위로 이동](#contents)

<br><br><br>

## ✒️ 제네레이터 (Generators)

<br>

### 제네레이터

```
function gen() {
    yield 1;
    yield 2;
    yield 3;
}

$gen = gen();

var_dump($gen->current());  // "1"
$gen->next();
var_dump($gen->current());  // "2"

foreach ($gen as $number) {
    var_dump($number);  // "1", "2", "3"
}

function get2() {
    yield 'message' => 'Hello, world';
}

foreach (get2() as $key => $value) {
    var_dump($key, $value); // "message", "Hello, world"
}

function gen3() {
    $data = yield;
    yield $data;
}

$gen3 = gen3();

var_dump($gen3->current());  // NULL

var_dump($gen3->send('Hello, world'));  // "Hello, world"
var_dump($get3->current());  // "Hello, world"
```

<br>

<br><br>

## [이 페이지의 맨 위로 이동](#contents)

<br><br><br>

## ✒️ 참조 (References)

<br>

### 참조

```
/*
 * References
 */

$message = 'Hello, world';
$sayHello =& $message;

$sayHello = 'Who are you?';
var_dump($message);  // "Who are you?"
```

```
/*
 * Functions and Methods
 */

function foo() {
    // global $message;
    $message =& $GLOBALS['message'];
    $message = 'Bye';
}

foo();
var_dump($message);  // "Bye"

function foo2(&$message) {
    $message = 'Hello, world';
}

foo2($message);
var_dump($message);  // "Hello, world"
```

```
/*
 * Unset
 */

$sayHello =& $message;
unset($sayHello);
var_dump($message);  "Hello, world"  // 참조는 해제한다해서 연결되어있는 변수까지 해체시키는 것은 아니고, 그 이름만 날라간다
```

<br>

### WeakReference

```
/*
 * WeakReference
 */

$class = new stdClass();

$weakRef = WeakReference::create($class);
var_dump($weakRef->get());  // "class stdClass"

unset($class);

var_dump($weakRef->get());  // NULL
```

<br>

<br><br>

## [이 페이지의 맨 위로 이동](#contents)

<br><br><br>

## ✒️ 객체 비교와 복사 (Cloning)

<br>

### 객체 비교

```
/*
 * Compare
 */

$class1 = new stdClass();
$class2 = new stdClass();

var_dump($class1 == $class2);  // bool(true);
var_dump($class1 === $class2);  // bool(flase);
```

<br>

### 객체 복사

```
/*
 * Copy
 */

// $class3 = $class1 = <Object Id>
$class3 = $class1;

$class3->sayHello = 'Hello, world';
var_dump($class1->sayHello);  // "Hello, world"
```

```
/*
 * 참조
 */

// ($class3, $class1) = <Object Id>
$class3 =& $class1;

$class3 = 'Hello, world';
var_dump($class1);  // "Hello, world"  // 객체 복사에선 class1은 안변함.
```

<br>

<br><br>

## [이 페이지의 맨 위로 이동](#contents)

<br><br><br>
