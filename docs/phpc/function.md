###PHP自定义函数

PHP内置了超过1000个函数，因此函数使得PHP成为一门非常强大的语言。大多数时候我们使用系统的内置函数就可以满足需求，但是自定义函数通过将一组代码封装起来，使代码进行复用，程序结构与逻辑更加清晰。

PHP函数的定义方式：
1. 使用关键字“function”开始
2. 函数名可以是字母或下划线开头：function name()
3. 在大括号中编写函数体：

```php
function name() {
    echo 'Eric';
}
```

通过上面的步骤，我们就定义了一个简单的函数，当我们需要的时候，就可以在代码中调用这个函数，调用方法为函数名+参数，例如：name();

```php
<?php
	function say(){
		echo 'hello world';
	}
	say();
?>
//hello world
```

###PHP函数的参数

PHP的函数可以没有参数，也可以有若干个参数，多个参数称之为参数列表，采用逗号进行分割，参数类似于一个变量，调用时用来传递数据到函数体中。通过传递参数可以使函数实现对参数的运算，得到我们想要的结果。

参数的变量名可以自由指定，但最好能够表达相关的意思，常用的设定参数的方法为：

```php
function sum($a, $b) { 
    return $a+$b; 
}
```

```php
<?php
	function say($a,$b){
		echo $a*$b;
	}
	say(2,3);
?>
//6
```

###PHP函数之返回值

使用return关键字可以使函数返回值，可以返回包括数组和对象的任意类型，如果省略了 return，则默认返回值为 NULL。

```php
<?php
	function say($a,$b){
		return $a*$b;
	}
	$c=say(2,3);
	echo $c;
?>
//6
```

```php
<?php
	function say(){
		return array(1,2,3);
	}
	$c=say();
	print_r($c);
?>
//Array ( [0] => 1 [1] => 2 [2] => 3 )
```

###PHP函数之可变函数

所谓可变函数，即通过变量的值来调用函数，因为变量的值是可变的，所以可以通过改变一个变量的值来实现调用不同的函数。经常会用在回调函数、函数列表，或者根据动态参数来调用不同的函数。可变函数的调用方法为变量名加括号。

```php
<?php
	function name() {
	    echo 'jobs'."<br />";
	}
	$func = 'name';
	$func(); //调用可变函数
	echo $func;
?>
//jobs
//name
```

可变函数也可以用在对象的方法调用上。

```php
<?php
	class book {
	    function getName() {
	        return 'bookname';
	    }
	}
	$func = 'getName';
	$book = new book();
	$book->$func();

	echo $book->$func()."<br />";
	echo $func;
?>
//bookname
//getName

```

PHP 支持可变函数的概念。
这意味着如果一个变量名后有圆括号，PHP 将寻找与变量的值同名的函数，并且尝试执行它。可变函数可以用来实现包括回调函数，函数表在内的一些用途。



###PHP函数之内置函数

内置函数指的是PHP默认支持的函数，PHP内置了很多标准的常用的处理函数，包括字符串处理、数组函数、文件处理、session与cookie处理等。

我们先拿字符串处理函数来举例，通过内置函数str_replace可以实现字符串的替换。下面的例子将“jobs”替换成“steven jobs”：

```php
<?php
	$str = 'i am jobs.';
	$str = str_replace('jobs', 'steven jobs', $str);
	echo $str; //结果为“i am steven jobs”
?>
```

```php
<?php
	$str = '苹果很好吃';
	$str = str_replace('苹果', '香蕉', $str);
	echo $str; 
?>
//香蕉很好吃
```

###PHP函数之判断函数是否存在

当我们创建了自定义函数，并且了解了可变函数的用法，为了确保程序调用的函数是存在的，经常会先使用function_exists判断一下函数是否存在。同样的method_exists可以用来检测类的方法是否存在。

```php
<?php
	function func() {
	}
	if (function_exists('func')){
	    echo 'exists';
	}
?>
//exists
```

类是否定义可以使用class_exists。

```php
<?php
	class MyClass{
	}
	// 使用前检查类是否存在
	if (class_exists('MyClass')) {
	    $myclass = new MyClass();
	}
?>
```

PHP中有很多这类的检查方法，例如文件是否存在file_exists等。

```php
<?php
	$filename = 'f.txt';
	if (!file_exists($filename)) {
	    echo $filename . ' not exists.';
	}else{
		echo $filename . ' existence.';
	}
?>
//f.txt existence.
```


```php
<?php
function func() {
    echo 'exists';
}
$name = 'func';
if (function_exists('func')) { //判断函数是否存在
    echo $name."<br/>";
    $name();
}
?>
/*
func
exists
*/
```