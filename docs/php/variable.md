###打印一串字符。
```php
<?php
  echo 'PHP学到家，走到哪儿都不怕！';
?>
```

###输出23+6的计算结果
```php
<?php
  echo 23+6;
?>
```

### .连接符
```php
<?php
  echo "Good,"."morning!";
?>
```

###注释
```php
<?php
    //echo "欢迎同学们！";
  echo 1+2+3+4+5;
?>
```

###什么是变量
```php
<?php
    $var = "学PHP";
    echo $var;
  echo "<br />";
  $var = "共同进步";
  echo $var;
?>
```

###”var_dump”函数可以将我们的变量的数据类型显示出来。
```php
<?php
    $var_name = "苹果";
  $n =10;
  var_dump($var_name);
  var_dump($n);
?>
//string(6) "苹果" int(10) 
```



###通过使用“memory_get_usage”获取当前PHP消耗的内存。
```php
<?php 
  echo $m1 = memory_get_usage(); 
  echo "<br />";
  $var_string = "123";
  echo $m2 = memory_get_usage()-$m1; 
  echo "<br />";
  $n=123;
  echo $m3 = memory_get_usage()-$m1-$m2; 
  echo "<br />";
  $f=123.00;
  echo $m4 = memory_get_usage()-$m1-$m2-$m3; 
  echo "<br />";
  $var_array = array("123");
  echo $m5 = memory_get_usage()-$m1-$m2-$m3-$m4; 
?>
//322696
//184
//160
//160
//352
//$m1相当于初始化的时候消耗的内存，memory_get_usage()这个函数是到当前这一步为止一共消耗多少内存。然后，一减就得到当前这一步消耗的内存。
```


###PHP变量的数据类型

var_dump()方法是判断一个变量的类型与长度,并输出变量的数值,如果变量有值输的是变量的值并回返数据类型.

```php
<?php 
  $string = "就是就是";
  var_dump($string);
  echo "<br />";
  $string = 9494;
  var_dump($string);
  echo "<br />";
?>
//string(12) "就是就是" 
//int(9494)
//不必向PHP声明变量的数据类型，PHP会自动把变量转换为自动的数据类型
//通过“var_dump”函数，输出数据类型。
```

###PHP标量类型—布尔类型
```php
<?php 
    $man = "男";
  $flag = $man == "男";
  echo $flag ;
  echo "<br />" ;
  var_dump($flag);
?>
//1
//bool(true)

//$flag = $man == "男";
//php中运算符有优先级，和平时做加减乘除的运算优先级类似，==的优先级高于=，所以先计算$man == "男"，返回结果是TRUE或者FALSE,第二步拿上一步的计算结果给$flag赋值，所以$flag=TRUE或者$flag=FALSE，$flag就是布尔型
```

###PHP标量类型—整型
```php
<?php
  $data_int1 = 123;     //123十进制数
  echo $data_int1;
  echo "<br />";
  $data_int2 = -123;    //-123一个负数
  echo $data_int2;
  echo "<br />";
  $data_int3 = 0123;    //83八进制数
  echo $data_int3;
  echo "<br />";
  $data_int4 = 0x123;   //291十六进制数
  echo $data_int4;
  echo "<br />";
?>
```


###PHP标量类型—浮点型

>e3是10的三次方，E-3是10的-3次方

```php
<?php
  $num_float1=1.234;
  echo $num_float1;
  echo "<br />";
  $num_float2=1.2e3;
  echo $num_float2;
  echo "<br />";
  $num_float3=7.0E-3;
  echo $num_float3;
  echo "<br />";
?>
//1.234
//1200
//0.007
```


###PHP标量类型—字符串（1）
```php
<?php
  $str_string1 = '我是字符串';
  $str_string2 = "我也是字符串哦";
  echo $str_string1;
  echo "<br />";
  echo $str_string2;
?>
//我是字符串
//我也是字符串哦
```

###PHP标量类型—字符串（2）
```php
<?php 
  $str_string1 = '甲问："你在哪里学的PHP？"';
  $str_string2 = "乙毫不犹豫地回答：'菜鸟网'";
  $str_string3 = '甲问:\'能告诉我网址吗？\'';
  $str_string4 = "乙答道:\"http://www.huanghanlian.com/\"";
  echo $str_string1;
  echo "<br />";
  echo $str_string2;
  echo "<br />";
  echo $str_string3;
  echo "<br />";
  echo $str_string4;
  echo "<br />";
?>
//甲问："你在哪里学的PHP？"
//乙毫不犹豫地回答：'菜鸟网'
//甲问:'能告诉我网址吗？'
//乙答道:"http://www.huanghanlian.com/"
```

###PHP标量类型—字符串（3）

>当双引号中包含变量时，变量会与双引号中的内容连接在一起；
当单引号中包含变量时，变量会被当做字符串输出。

```php
<?php
  $love = "I love you!";
  $string1 = "继小鹏,$love";
  $string2 = '继小鹏,$love';
  echo $string1;
  echo "<br />";
  echo $string2;
?>
//继小鹏,I love you!
//继小鹏,$love
```

###PHP标量类型—字符串（4）

>只要用了<<<之后用相同的字母为起点。和结尾都可以了

```php
<?php
$string1=<<<GOD
我有一只小毛驴，我从来也不骑。
有一天我心血来潮，骑着去赶集。
我手里拿着小皮鞭，我心里正得意。
不知怎么哗啦啦啦啦，我摔了一身泥.
GOD;

echo $string1;
?>
```

###PHP第一种特殊类型—资源

资源（resource）：资源是由专门的函数来建立和使用的，例如打开文件、数据连接、图形画布。我们可以对资源进行操作（创建、使用和释放）。任何资源，在不需要的时候应该被及时释放。如果我们忘记了释放资源，系统自动启用垃圾回收机制，在页面执行完毕后回收资源，以避免内存被消耗殆尽。

```php
<?php 
  //首先采用“fopen”函数打开文件，得到返回值的就是资源类型。
  $file_handle = fopen("f.txt","r");
  if ($file_handle){
      //接着采用while循环（后面语言结构语句中的循环结构会详细介绍）一行行地读取文件，然后输出每行的文字
      while (!feof($file_handle)) { //判断是否到最后一行
          $line = fgets($file_handle); //读取一行文本
          echo $line; //输出一行文本
          echo "<br />"; //换行
      }
  }
  fclose($file_handle);//关闭文件
?>

//解释

$a = fopen("打开文件根目录","r");//打开文件
$b = fgets($a);//读取文件中的内容
$c = fclose($a);//关闭文件
```


###PHP第二种特殊类型—空类型

NULL（NULL）：NULL是空类型，对大小写不敏感，NULL类型只有一个取值，表示一个变量没有值，当被赋值为NULL，或者尚未被赋值，或者被unset()，这三种情况下变量被认为为NULL。

>unset是将变量删除，成功则返回 true 值
error_reporting禁止显示php警告提示

```php
<?php
  error_reporting(0); //禁止显示PHP警告提示
  $var;
  var_dump($var);
  $var1 = null;
  var_dump($var1);
  $var2 = NULL;
  var_dump( $var2);
  $var3 = "节日快乐！";
  “unset($var3);
  var_dump($var3);
?>
```

