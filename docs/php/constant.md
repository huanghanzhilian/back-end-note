###PHP-什么是常量

什么是常量？常量可以理解为值不变的量（如圆周率）；或者是常量值被定义后，在脚本的其他任何地方都不可以被改变。PHP中的常量分为自定义常量和系统常量

>$p = "PII";define($p,3.14);等同于define("PI",3.14);

```php
<?php
  $p = "PII";
  define("PI",3.14);
  define($p,3.14);
  echo PI;
  echo "<br />";
  echo PII;
?>
//3.14
//3.14
```





###PHP-常量的作用

常量主要功效是可以避免重复定义，篡改变量值。在我们进行团队开发时，或者代码量很大的时候，对于一些第一次定义后不改变的量，如果我们使用变量，在不知情的情况下，使用同一变量名时，变量值就会被替换掉，从而会引发服务器执行错误的任务。

此外，使用常量还能提高代码的可维护性。如果由于某些原因，常量的值需要变更时候，我们只需要修改一个地方。例如在做计算中，起初我们取圆周率为3.14，于是很多计算中我们都使用3.14进行计算，当要求计算精度提高，圆周率需要取3.142的时候，我们不得不修改所有使用3.14的代码，倘若代码量比较多时，不仅工作量大，还可能遗漏。

```php
<?php
define("PI",3.14);
$r=3;
echo "面积为:".(PI*$r*$r)."<br />";
echo "周长为:".(2*PI*$r)."<br />";
?>
//面积为:28.26
//周长为:18.84
```

###PHP-认识一下系统常量



系统常量是PHP已经定义好的常量，我们可以直接拿来使用，常见的系统常量有：

（1）__FILE__ :php程序文件名。它可以帮助我们获取当前文件在服务器的物理位置。

（2）__LINE__ :PHP程序文件行数。它可以告诉我们，当前代码在第几行。

（3）PHP_VERSION:当前解析器的版本号。它可以告诉我们当前PHP解析器的版本号，我们可以提前知道我们的PHP代码是否可被该PHP解析器解析。

（4）PHP_OS：执行当前PHP版本的操作系统名称。它可以告诉我们服务器所用的操作系统名称，我们可以根据该操作系统优化我们的代码。


```php
<?php
  echo __FILE__;
  echo "<br />";
  echo __LINE__;
  echo "<br />";
  echo PHP_VERSION;
  echo "<br />";
  echo PHP_OS;
  echo "<br />";
?>
//D:\phpStudy\WWW\php_Introduction\index.php
//11
//5.5.30
//WINNT
```

###PHP-常量如何取值

>mixed constant(string constant_name)

第一个参数constant_name为要获取常量的名称，也可为存储常量名的变量。如果成功则返回常量的值，失败则提示错误信息常量没有被定义。

```php
<?php 
$p="";
//定义圆周率的两种取值
define("PI1",3.14);
define("PI2",3.142);
//定义值的精度
$height = "中";
//根据精度返回常量名，将常量变成了一个可变的常量
if($height == "中"){
    $p = "PI1";
}else if($height == "低"){
  $p = "PI2";
}
$r=1;
$area= constant($p)*$r*$r;
echo $area;
?>
//3.14
```

###PHP-如何判定常量是否被定义

如果常量被重复定义以后，PHP解析器会发出“Constant XXX already defined”的警告，提醒我们该常量已经被定义过。那么，在团队开发，或代码量很大的情况下，我们如何去判定一个常量是否被定义呢？

defined()函数可以帮助我们判断一个常量是否已经定义，其语法格式为：

    bool defined(string constants_name)

它只有参数constant_name，指的是要获取常量的名称，若存在则返回布尔类型true，否则返回布尔类型false; （注：bool表示函数返回值类型为布尔类型）

```php
<?php 
define("PI1",3.14);
$p = "PI1";
$is1 = defined($p);
$is2 = defined("PI2");
var_dump($is1);
var_dump($is2);
?>
//bool(true) bool(false)
```