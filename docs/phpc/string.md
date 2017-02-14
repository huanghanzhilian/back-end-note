###PHP字符串介绍

PHP开发中，我们遇到最多的可能就是字符串。

字符串变量用于包含字符串的值。

一个字符串 通过下面的3种方法来定义：

1. 单引号
2. 双引号
3. heredoc语法结构

基本用法

单引号定义的字符串：`$hello = 'hello world';`

双引号定义的字符串：`$hello = "hello world";`

heredoc语法结构定义的字符串：

```php
<?php
$hello = <<<TAG
hello world
TAG;
echo $hello;
?>
//hello world
```



###PHP字符串之单引号和双引号的区别

在PHP中，字符串的定义可以使用英文单引号' '，也可以使用英文双引号" "。

但是必须使用同一种单或双引号来定义字符串，如：'Hello World"和"Hello World'为非法的字符串定义。

单引号和双引号到底有啥区别呢？

PHP允许我们在双引号串中直接包含字串变量。

而单引号串中的内容总被认为是普通字符。

比如：

```php
$str='hello';
echo "str is $str"; //运行结果: str is hello
echo 'str is $str'; //运行结果: str is $str
```



###PHP字符串之字符串的连接

PHP中两个字符串如何连接呢，比如我有个字符串$hello='hello',还有一个字符串$world=' world'，我想将这两个字符串连接在一起，跟世界打个招呼。

PHP中用英文的点号`.`来连接两个字符串。

```php
$hello='hello';

$world=' world';

$hi = $hello.$world;

echo $hi;//我们可以用echo函数输出一下这个字符串连接。
```

###PHP字符串之去除字符串首尾的空格


trim去除一个字符串两端空格。
rtrim是去除一个字符串右部空格，其中的r是right的缩写。
ltrim是去除一个字符串左部空格，其中的l是left的缩写。

```php
<?php
echo trim(" 空格 ")."<br>";
echo rtrim(" 空格 ")."<br>";
echo ltrim(" 空格 ")."<br>";
?>
```

###PHP字符串之获取字符串的长度

php中有一个神奇的函数，可以直接获取字符串的长度，这个函数就是`strlen()`。

例子如下：

```php
$str = 'hello';
$len = strlen($str);
echo $len;//输出结果是5
```

strlen函数对于计算英文字符是非常的擅长，但是如果有中文汉字，要计算长度该怎么办？

可以使用`mb_strlen()`函数获取字符串中中文长度。

例子如下：
```php
$str = "我爱你";
echo mb_strlen($str,"UTF8");//结果：3，此处的UTF8表示中文编码是UTF8格式，中文一般采用UTF8编码
```

###PHP字符串之字符串的截取

php中有非常多的字符串处理函数，其中就有字符串截取函数。

1、英文字符串的截取函数substr()

函数说明：substr(字符串变量,开始截取的位置，截取个数）

例如：

```php
$str='i love you';
//截取love这几个字母
echo substr($str, 2, 4);//为什么开始位置是2呢，因为substr函数计算字符串位置是从0开始的，也就是0的位置是i,1的位置是空格，l的位置是2。从位置2开始取4个字符，就是love。
```

2、中文字符串的截取函数mb_substr()

函数说明：mb_substr(字符串变量,开始截取的位置，截取个数, 网页编码）

例如：

```php
$str='我爱你，中国';

//截取中国两个字

echo mb_substr($str, 4, 2, 'utf8');//为什么开始位置是4呢，和上一个例子一样，因为mb_substr函数计算汉字位置是从0开始的，也就是0的位置是我,1的位置是爱，4的位置是中。从位置4开始取2个汉字，就是中国。中文编码一般是utf8格式
```

###PHP字符串之查找字符串

如果有一个字符串$str = 'I want to study at imooc';，怎么样找到其中的imooc在哪个位置呢？

查找字符串，我们需要用到PHP的查找字符串函数strpos();

函数说明：strpos(要处理的字符串, 要定位的字符串, 定位的起始位置[可选])

例子：

```php
$str = 'I want to study at imooc';
$pos = strpos($str, 'imooc');
echo $pos;//结果显示19，表示从位置0开始，imooc在第19个位置开始出现
```

```php
<?php
//查找字符串
$str = 'What is your name?';
echo strpos($str, 'name');//13
?>
```

###PHP字符串之替换字符串

如果有一个字符串$str = 'I want to learn js';，怎么样将js字符替换成你想学的php字符呢？

替换字符串，我们需要用到PHP的替换函数`str_replace()`

函数说明：`str_replace(要查找的字符串, 要替换的字符串, 被搜索的字符串, 替换进行计数[可选])`

例子：

```php
$str = 'I want to learn js';
$replace = str_replace('js', 'php', $str);
echo $replace;//结果显示I want to learn php
```

```php
<?php
//替换字符串
$str = 'I Love Chian';
echo str_replace('Chian', 'China', $str);//I Love China
?>
```

###PHP字符串之格式化字符串



如果有一个字符串$str = '99.9';，怎么样使这个字符串变成99.90呢？

我们需要用到PHP的格式化字符串函数sprintf()

函数说明：sprintf(格式, 要转化的字符串)

返回：格式化好的字符串

例子：

$str = '99.9';
$result = sprintf('%01.2f', $str);
echo $result;//结果显示99.90

解释下，上面例子中的格式

这个 %01.2f 是什么意思呢？

1、这个 % 符号是开始的意思，写在最前面表示指定格式开始了。 也就是 "起始字符", 直到出现 "转换字符" 为止，就算格式终止。
2、跟在 % 符号后面的是 0， 是 "填空字元" ，表示如果位置空着就用0来填满。
3、在 0 后面的是1，这个 1 是规定整个所有的字符串占位要有1位以上(小数点也算一个占位)。
    如果把 1 改成 6，则 $result的值将为 099.90
    因为，在小数点后面必须是两位，99.90一共5个占位，现在需要6个占位，所以用0来填满。
4、在 %01 后面的 .2 （点2） 就很好理解了，它的意思是，小数点后的数字必须占2位。 如果这时候，$str 的值为9.234,则 $result的值将为9.23.
    为什么4 不见了呢？ 因为在小数点后面，按照上面的规定，必须且仅能占2位。 可是 $str 的值中，小数点后面占了3位，所以，尾数4被去掉了，只剩下 23。
5、最后，以 f "转换字符" 结尾。


```php
<?php
//格式化字符串
$str = '100.1';
$result=sprintf('%01.3f', $str);
echo $result;//100.100
?>
```

###PHP字符串之字符串的合并与分割

1、php字符串合并函数implode()

函数说明：implode(分隔符[可选], 数组)

返回值：把数组元素组合为一个字符串

例子：

```php
$arr = array('Hello', 'World!');
$result = implode('', $arr);
print_r($result);//结果显示Hello World!
```

2、php字符串分隔函数explode()

函数说明：explode(分隔符[可选], 字符串)

返回值：函数返回由字符串组成的数组

例子：

```php
$str = 'apple,banana';
$result = explode(',', $str);
print_r($result);//结果显示array('apple','banana')
```

```php
<?php
//分隔字符串
$str = 'sun-moon-star';
$result = explode('-', $str);
print_r($result);//结果显示array('apple','banana')
?>
/*
Array
(
    [0] => sun
    [1] => moon
    [2] => star
)
*/
```

###PHP字符串之字符串的转义

hp字符串转义函数addslashes()

函数说明：用于对特殊字符加上转义字符，返回一个字符串

返回值：一个经过转义后的字符串

例子：

```php
$str = "what's your name?";
echo addslashes($str);//输出：what\'s your name?
```

```php
<?php
//字符串转义
$str = "what's this?";
echo addslashes($str);//输出：what\'s this?
?>
```