#PHP中PSR[0-4]代码规范
## php-fig
```
1、FIG：PSR[0-4]代码规范的得发明者、规范者，framework interoperability group
2、PSR：提出标准建议，proposing a standards recommendation
```
## PSR-0 Autoloading Standard
### 规范一
一个完全合格的namespace和class必须符合这样的结构："\< Vendor Name>(< Namespace>)*< Class Name>"

```
例如：\China\Jiangxi\School\User.php
China 表示Vendor Name
\Jiangxi\Scholl 表示Namespace
User 表示Class Name
```
### 规范二
每个namespace必须有一个顶层namespace

```
例如：\China\Jiangxi\School\User.php
China 为顶层namespace
```
### 规范三
namespace可以有多个子命名空间

```
例如：\China\Jiangxi\School和\China\Jiangxi\Family
School 和 Family 为\China\Jiangxi的子命名空间
```

### 规范四
文件系统加载时，每个namespace的分隔符要转换成DIRECTORY_SEPARATOR（目录分隔符）

```
例如：\China\Jiangxi\School和\China\Jiangxi\Family
School 和 Family 为\China\Jiangxi的子命名空间
```

### 规范五
在类名中，每个下划线(\_)符号要转换成DIRECTORY\_SEPARATOR(操作系统路径分隔符)。在namespace中，下划线(_)符号是没有（特殊）意义的

```
已经弃用
```

### 规范六
文件后缀必须为.php

### 规范七
vendor name、namespaces、class名可以由大小写组成，且区分字母大小写

## PSR-1 Basic Coding Stantard
### 规范一
php源文件必须只使用<?php或者<?=

### 规范二
源文件必须为不带字节顺序标记（BOM）的UTF-8
### 规范三
一个源文件建议只做声明(class、function、const)或者只做一些引起副作用的操作（输出信息、修改.ini配置等），不建议同时做这两件事
### 规范四
命名空间和类必须遵循PSR-0
### 规范五
类名必须使用骆驼式写法（ClassName）
### 规范六
类中的常量必须只由大写字母和下划线组成
### 规范七
方法名必须使用驼峰式写法（functionName）

## PSR-2 Coding Style Guide
### 源文件
1、文件末尾必须空一行

2、必须使用Unix LF(换行)作为行结束符

3、纯PHP代码的源文件的关闭标签?>必须省略（）

### 缩进
必须使用4个空格来缩进

### 行
一行推荐的是最多写80个字符，多于这个字符就应该换行了，一般的编辑器是可以设置的

### 关键字和 True/False/Null
php的关键字，必须小写，boolean值：true，false，null 也必须小写

```
 '__halt_compiler', 'abstract', 'and', 'array', 'as', 'break',  
 'callable', 'case', 'catch', 'class', 'clone', 'const', 'continue', 
 'declare', 'default', 'die', 'do', 'echo', 'else', 'elseif', 'empty',
 'enddeclare', 'endfor', 'endforeach', 'endif', 'endswitch', 
 'endwhile', 'eval', 'exit', 'extends', 'final', 'for', 'foreach', 
 'function', 'global', 'goto', 'if', 'implements', 'include', 
 'include_once', 'instanceof', 'insteadof', 'interface', 'isset', 
 'list', 'namespace', 'new', 'or', 'print', 'private', 'protected', 
 'public', 'require', 'require_once', 'return', 'static', 'switch', 
 'throw', 'trait', 'try', 'unset', 'use', 'var', 'while', 'xor'
```

### 命名空间、namespace导入
1、命名空间声明之后，必须有一行空行

2、所有的导入（use）必须放在命名空间后面

3、在导入(use)声明代码块后面必须有一行空行

```
<?php
namespace Lib\Databases; // 下面必须空格一行

use FooInterface; // use 必须在namespace 后面声明
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass; // 下面必须空格一行

class Mysql
{
}
```

### 类(class)，属性(property)和方法(method)
1、继承(extends) 和实现(implement) 必须和 class name 写在一行，切花括号要换行写

```
<?php
namespace Lib\Databaes;

class Mysql extends ParentClass implements \PDO, \DB // 写一行
{ // 换行写{
	
}
```
2、属性(property)必须声明其可见性，到底是 public 还是 protected 还是 private，不能省略，也不能使用var, var是php老版本中的什么方式，等用于public

```
<?php
namespace Lib\Databaes;

class Mysql extends ParentClass implements \PDO, \DB // 写一行
{
	public $foo = null;
	private $name = 'yangyi';
	protected $age = '17';
}
```

3、方法(method)，必须 声明其可见性，到底是 public 还是 protected 还是 private，不能省略。并且，花括号{必须换行写。如果有多个参数，第一个参数后紧接, ,再加个空格，且函数name和( 之间必须要有个空格：function_name ($par, $par2, $pa3), 如果参数有默认值，也要用左右空格分开

```
<?php
namespace Lib\Databaes;

class Mysql extends ParentClass implements \PDO, \DB // 写一行
{
	public getInfo ($name, $age, $gender = 1) // 函数名getInfo和(之间有个空格，参数之间也要有空格。默认参数也要左右都有空格
	{ // 必须换行写 {
	}
}
```

4、当用到抽象(abstract)和终结(final)来做类声明时，它们必须放在可见性声明 （public 还是protected还是private）的前面。而当用到静态(static)来做类声明时，则必须放在可见性声明的后面

```
<?php
namespace Vendor\Package;

abstract class ClassName
{
	protected static $foo; // static放后面

	abstract protected function zim(); // abstract放前面

	final public static function bar() // final放前面，static放最后。
	{
		// 方法主体部分
	}
}
```

### 控制结构
1、if，elseif，else写法

```
<?php
if ($expr1) { // 左右空格
	// if body
} elseif ($expr2) { // elesif 连着写
	// elseif body
} else {
	// else body;
}
```

2、switch，case 注意左右空格和换行

```
<?php
switch ($expr) { // 左右空格
	case 0:
		echo 'First case, with a break'; // 对齐
		break; // 换行写break，也对齐。
	case 1:
		echo 'Second case, which falls through';
		// no break
	case 2:
	case 3:
	case 4:
		echo 'Third case, return instead of break';
		return;
	default:
		echo 'Default case';
		break;
}
```

3、while，do while 的写法

```
<?php
while ($expr) { // 左右空格
	// structure body
}

do {
	// structure body; // 左右空格
} while ($expr);
```

4、for的写法

```
<?php
for ($i = 0; $i < 10; $i++) { // 注意几个参数之间的空格
	// for body
}
```
5、foreach的写法

```
<?php
foreach ($iterable as $key => $value) { // 还是空格问题
	// foreach body
}
```
6、try catch的写法

```
<?php
try {
	// try body
} catch (FirstExceptionType $e) { // 同样也是注意空格。
	// catch body
} catch (OtherExceptionType $e) {
	// catch body
}
```
## Logger Interface 规范日志接口
### LoggerInterface

```
<?php

namespace Psr\Log;

/**
 * Describes a logger instance
 *
 * The message MUST be a string or object implementing __toString().
 *
 * The message MAY contain placeholders in the form: {foo} where foo
 * will be replaced by the context data in key "foo".
 *
 * The context array can contain arbitrary data, the only assumption that
 * can be made by implementors is that if an Exception instance is given
 * to produce a stack trace, it MUST be in a key named "exception".
 *
 * See https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-3-logger-interface.md
 * for the full interface specification.
 */
interface LoggerInterface
{
    /**
     * System is unusable.
     *
     * @param string $message
     * @param array $context
     * @return null
     */
    public function emergency($message, array $context = array());

    /**
     * Action must be taken immediately.
     *
     * Example: Entire website down, database unavailable, etc. This should
     * trigger the SMS alerts and wake you up.
     *
     * @param string $message
     * @param array $context
     * @return null
     */
    public function alert($message, array $context = array());

    /**
     * Critical conditions.
     *
     * Example: Application component unavailable, unexpected exception.
     *
     * @param string $message
     * @param array $context
     * @return null
     */
    public function critical($message, array $context = array());

    /**
     * Runtime errors that do not require immediate action but should typically
     * be logged and monitored.
     *
     * @param string $message
     * @param array $context
     * @return null
     */
    public function error($message, array $context = array());

    /**
     * Exceptional occurrences that are not errors.
     *
     * Example: Use of deprecated APIs, poor use of an API, undesirable things
     * that are not necessarily wrong.
     *
     * @param string $message
     * @param array $context
     * @return null
     */
    public function warning($message, array $context = array());

    /**
     * Normal but significant events.
     *
     * @param string $message
     * @param array $context
     * @return null
     */
    public function notice($message, array $context = array());

    /**
     * Interesting events.
     *
     * Example: User logs in, SQL logs.
     *
     * @param string $message
     * @param array $context
     * @return null
     */
    public function info($message, array $context = array());

    /**
     * Detailed debug information.
     *
     * @param string $message
     * @param array $context
     * @return null
     */
    public function debug($message, array $context = array());

    /**
     * Logs with an arbitrary level.
     *
     * @param mixed $level
     * @param string $message
     * @param array $context
     * @return null
     */
    public function log($level, $message, array $context = array());
}
```

### Psr\Log\LoggerAwareInterface
```
<?php

namespace Psr\Log;

/**
 * Describes a logger-aware instance
 */
interface LoggerAwareInterface
{
    /**
     * Sets a logger instance on the object
     *
     * @param LoggerInterface $logger
     * @return null
     */
    public function setLogger(LoggerInterface $logger);
}
```
###Psr\Log\LogLevel

```
<?php

namespace Psr\Log;

/**
 * Describes log levels
 */
class LogLevel
{
    const EMERGENCY = 'emergency';
    const ALERT     = 'alert';
    const CRITICAL  = 'critical';
    const ERROR     = 'error';
    const WARNING   = 'warning';
    const NOTICE    = 'notice';
    const INFO      = 'info';
    const DEBUG     = 'debug';
}
```
##Autoloader
###类名必须要和对应的文件名要一模一样，大小写也要一模一样

###类文件名要以 .php 结尾

###废除了PSR-0中_就是目录分割符的写法，_下划线在完全限定类名中是没有特殊含义

###实例

FULLY QUALIFIED CLASS NAME  | NAMESPACE PREFIX  | BASE DIRECTORY  | RESULTING FILE PATH
------------- | -------------  | -------------  | -------------
\Acme\Log\Writer\File_Writer  | Acme\Log\Writer|./acme-log-writer/lib/|./acme-log-writer/lib/File_Writer.php
\Aura\Web\Response\Status|Aura\Web|/path/to/aura-web/src/|/path/to/aura-web/src/Response/Status.php
\Symfony\Core\Request|Symfony\Core|./vendor/Symfony/Core/|./vendor/Symfony/Core/Request.php
\Zend\Acl| Zend |/usr/includes/Zend/|/usr/includes/Zend/Acl.php







