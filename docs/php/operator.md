###什么是运算符

什么是运算符？运算符是告诉PHP做相关运算的标识符号。例如，你需要计算123乘以456等于多少，这时候就需要一个符号，告诉服务器，你需要做乘法运算。

PHP中的运算符有哪些？PHP运算符一般分为算术运算符、赋值运算符、比较运算符、三元运算符、逻辑运算符、字符串连接运算符、错误控制运算符。


```php
<?php 
$a = 1;
$b = 1;
$c = $a + $b;
echo $c;
?>
//2
```

###PHP中的算术运算符
```php
<?php 
$english = 110; //英语成绩
$math= 118; //数学成绩
$biological = 80; //生物成绩
$physical = 90; //物理成绩

$sum = $english+$math+$biological+$physical;
$avg = $sum / 4;
$x = $math - $english;
$x2 = $english * $english;

echo "总分:".$sum."<br />";
echo "平均分:".$avg."<br />";
echo "数学比英语高的分数:".$x."<br />";
echo "英语成绩的平方:".$x2."<br />";
?>
//总分:398
//平均分:99.5
//数学比英语高的分数:8
//英语成绩的平方:12100
```

###PHP中的赋值运算符



PHP的赋值运算符有两种，分别是：

(1)“=”：把右边表达式的值赋给左边的运算数。它将右边表达式值复制一份，交给左边的运算数。换而言之，首先给左边的运算数申请了一块内存，然后把复制的值放到这个内存中。

(2)“&”：引用赋值，意味着两个变量都指向同一个数据。它将使两个变量共享一块内存，如果这个内存存储的数据变了，那么两个变量的值都会发生变化。


```php
<?php 
    $a = "你好";
	$b = $a;
	$c = &$a;
	$a = "大家好";
	
	echo $b."<br />";
	echo $c."<br />";
?>
//你好
//大家好
//$b是$a复制的值，之后$a怎么变，$b都不变化。$c和$a指向同一个内存，$a变化，对应内存值也变化，$c也变化。
```

###PHP中的比较运算符


![533a0af30001e75c06600409.jpg.png](http://upload-images.jianshu.io/upload_images/3877962-5c0b17544b4c7bf3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


```php
<?php  
    $a = 1;
	$b = "1";
	var_dump($a == $b);
	echo "<br />";
	var_dump($a === $b);
	echo "<br />";
	var_dump($a != $b);
	echo "<br />";
	var_dump($a <> $b);
	echo "<br />";
	var_dump($a !== $b);
	echo "<br />";
	var_dump($a < $b);
	echo "<br />";
    echo "<br />111<br />";
	$c = 5;
	var_dump($a < $c);
	echo "<br />";
	var_dump($a > $c);
	echo "<br />";
	var_dump($a <= $c);
	echo "<br />";
	var_dump($a >= $b);
	echo "<br />";
	var_dump($a >= $b);
	echo "<br />";
?>
/*
bool(true) 
bool(false) 
bool(false) 
bool(false) 
bool(true) 
bool(false) 

111
bool(true) 
bool(false) 
bool(true) 
bool(true) 
bool(true) 
*/
```

###PHP中的三元运算符

```php
<?php 
    $a = 78;//成绩
	$b = $a >= 60 ? "及格": "不及格"; 
	echo $b;
?>
//及格
```

###PHP中的逻辑运算符

逻辑运算符主用是进行逻辑运算的，例如：逻辑与、逻辑或、逻辑异或、逻辑非等


![533e0fbe0001c56f06080279.jpg.png](http://upload-images.jianshu.io/upload_images/3877962-57cc68802e338933.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


```php
<?php 
    $a = TRUE; //A同意
	$b = TRUE; //B同意
	$c = FALSE; //C反对
	$d = FALSE; //D反对
    //咱顺便复习下三元运算符
	echo ($a and $b)?"通过":"不通过";
	echo "<br />";
	echo($a or $c)?"通过":"不通过";
	echo "<br />";
	echo ($a xor $c xor $d)?"通过":"不通过";
	echo "<br />";
	echo !$c?"通过":"不通过";
	echo "<br />";
    echo $a && $d?"通过":"不通过";
	echo "<br />";
	echo $b || $c || $d?"通过":"不通过";
	
?>
/*
通过
通过
通过
通过
不通过
通过
*/
```

###PHP中的字符串连接运算符



字符串连接运算符是为了将两个字符串进行连接，PHP中提供的字符串连接运算符有：

（1）连接运算符(“.”)：它返回将右参数附加到左参数后面所得的字符串。

（2）连接赋值运算符(“.=”)：它将右边参数附加到左边的参数后。


```php
<?php 
    $a = "黄先生";
	$tip = $a.",你好";
	
    $b = "东边日出西边雨";	
    $b .= ",道是无晴却有晴";
    
	$c = "东边日出西边雨";	
    $c = $c.",道是无晴却有晴";
    
	echo  $tip."<br />";
	echo  $b."<br />";
	echo  $c."<br />";
?>
/*
黄先生,你好
东边日出西边雨,道是无晴却有晴
东边日出西边雨,道是无晴却有晴
*/
```

###PHP中的错误控制运算符



PHP中提供了一个错误控制运算符“@”，对于一些可能会在运行过程中出错的表达式时，我们不希望出错的时候给客户显示错误信息，这样对用户不友好。于是，可以将@放置在一个PHP表达式之前，该表达式可能产生的任何错误信息都被忽略掉；

如果激活了track_error（这个玩意在php.ini中设置）特性，表达式所产生的任何错误信息都被存放在变量$php_errormsg中，此变量在每次出错时都会被覆盖，所以如果想用它的话必须尽早检查。

需要注意的是：错误控制前缀“@”不会屏蔽解析错误的信息，不能把它放在函数或类的定义之前，也不能用于条件结构例如if和foreach等。


```php
<?php  
 $conn = @mysql_connect("localhost","username","password");
 echo "出错了，错误原因是：".$php_errormsg;
?>
/*

Notice: Undefined variable: php_errormsg in D:\phpStudy\WWW\php_Introduction\index.php on line 10
出错了，错误原因是：
*/
```

###PHP中的算术运算符（2）

取模算术符有啥用呢？

假设我们要在一个考场安排了一场考试，对考生从1开始，都进行了编号，那么怎么让服务器帮助我们计算考生在的位置呢，进而打印考场的考生对照表呢？在右边编辑器里输入两条指令，如图所示：

```php
<?php
     $maxLine = 4; //每排人数
	 $no = 17;//学生编号
     $line = ceil($no/$maxLine);//ceil()的作用是向上取整，以这里为例，17除以4等于4.25，所以向上取整就是5。17号的学生要坐在第五排。
	 $row = $no%$maxLine;

	 echo "编号<b>".$no."</b>的座位在第<b>".$line."</b>排第<b>".$row."</b>个位置";
?>
//编号17的座位在第5排第1个位置
```