###什么叫正则表达式

正则表达式是对字符串进行操作的一种逻辑公式，就是用一些特定的字符组合成一个规则字符串，称之为正则匹配模式。

```php
<?php
$p = '/apple/';
$str = "apple banna";
if (preg_match($p, $str)) {
    echo 'matched';
}
?>
```

其中字符串'/apple/'就是一个正则表达式，他用来匹配源字符串中是否存在apple字符串。

PHP中使用PCRE库函数进行正则匹配，比如上例中的preg_match用于执行一个正则匹配，常用来判断一类字符模式是否存在。

```php
<?php
$p = '/苹果/';

$str = "我喜欢吃苹果";
if (preg_match($p, $str)) {
    echo '匹配成功';
}
//匹配成功
?>
```

###正则表达式的基本语法

PCRE库函数中，正则匹配模式使用分隔符与元字符组成，分隔符可以是非数字、非反斜线、非空格的任意字符。经常使用的分隔符是正斜线(/)、hash符号(#) 以及取反符号(~)，例如：

```php
/foo bar/
#^[^0-9]$#
~php~
```

如果模式中包含分隔符，则分隔符需要使用反斜杠（\）进行转义。

```php
/http:\/\//
```

如果模式中包含较多的分割字符，建议更换其他的字符作为分隔符，也可以采用preg_quote进行转义。

```php
$p = 'http://';
$p = '/'.preg_quote($p, '/').'/';
echo $p;
```

分隔符后面可以使用模式修饰符，模式修饰符包括：i, m, s, x等，例如使用i修饰符可以忽略大小写匹配：

```php
$str = "Http://www.imooc.com/";
if (preg_match('/http/i', $str)) {
    echo '匹配成功';
}
```

```php
<?php
$p = '/bbc/i';
$str = "BBC是英国的一个电视台";
if (preg_match($p, $str)) {
    echo '匹配成功';//匹配成功
}
?>
```

###元字符与转义

正则表达式中具有特殊含义的字符称之为元字符，常用的元字符有：

`\ `一般用于转义字符
`^` 断言目标的开始位置(或在多行模式下是行首)
`$` 断言目标的结束位置(或在多行模式下是行尾)
`. `匹配除换行符外的任何字符(默认)
`[ `开始字符类定义
`] `结束字符类定义
`| `开始一个可选分支
`( `子组的开始标记
`) `子组的结束标记
`?` 作为量词，表示 0 次或 1 次匹配。位于量词后面用于改变量词的贪婪特性。 (查阅量词)
`* `量词，0 次或多次匹配
`+ `量词，1 次或多次匹配
`{` 自定义量词开始标记
`} `自定义量词结束标记

```php
//下面的\s匹配任意的空白符，包括空格，制表符，换行符。[^\s]代表非空白符。[^\s]+表示一次或多次匹配非空白符。
$p = '/^我[^\s]+(苹果|香蕉)$/';
$str = "我喜欢吃苹果";
if (preg_match($p, $str)) {
    echo '匹配成功';
}
```

元字符具有两种使用场景，一种是可以在任何地方都能使用，另一种是只能在方括号内使用，在方括号内使用的有：

`\ `转义字符
`^` 仅在作为第一个字符(方括号内)时，表明字符类取反
`-` 标记字符范围

其中^在反括号外面，表示断言目标的开始位置，但在方括号内部则代表字符类取反，方括号内的减号-可以标记字符范围，例如0-9表示0到9之间的所有数字。

```php
//下面的\w匹配字母或数字或下划线。
$p = '/[\w\.\-]+@[a-z0-9\-]+\.(com|cn)/';
$str = "我的邮箱是Spark.eric@imooc.com";
preg_match($p, $str, $match);
echo $match[0];
```

```php
<?php
$p = '/\d+\-\d+/';
$str = "我的电话是010-12345678";
preg_match($p, $str, $match);
echo $match[0];
?>
//010-12345678
```

###贪婪模式与懒惰模式

正则表达式中每个元字符匹配一个字符，当使用+之后将会变的贪婪，它将匹配尽可能多的字符，但使用问号?字符时，它将尽可能少的匹配字符，既是懒惰模式。

贪婪模式：在可匹配与可不匹配的时候，优先匹配

```php
//下面的\d表示匹配数字
$p = '/\d+\-\d+/';
$str = "我的电话是010-12345678";
preg_match($p, $str, $match);
echo $match[0]; //结果为：010-12345678
```

懒惰模式：在可匹配与可不匹配的时候，优先不匹配

```php
$p = '/\d?\-\d?/';
$str = "我的电话是010-12345678";
preg_match($p, $str, $match);
echo $match[0];  //结果为：0-1
```

当我们确切的知道所匹配的字符长度的时候，可以使用{}指定匹配字符数

```php
$p = '/\d{3}\-\d{8}/';
$str = "我的电话是010-12345678";
preg_match($p, $str, $match);
echo $match[0]; //结果为：010-12345678
```

```php
<?php
$p = '/name:([\w\s]+)/';
$str = "name:steven jobs";
preg_match($p, $str, $match);
echo $match[1]; //结果为：steven jobs
?>
```


###使用正则表达式进行匹配

使用正则表达式的目的是为了实现比字符串处理函数更加灵活的处理方式，因此跟字符串处理函数一样，其主要用来判断子字符串是否存在、字符串替换、分割字符串、获取模式子串等。

PHP使用PCRE库函数来进行正则处理，通过设定好模式，然后调用相关的处理函数来取得匹配结果。

preg_match用来执行一个匹配，可以简单的用来判断模式是否匹配成功，或者取得一个匹配结果，他的返回值是匹配成功的次数0或者1，在匹配到1次以后就会停止搜索。

```php
$subject = "abcdef";
$pattern = '/def/';
preg_match($pattern, $subject, $matches);
print_r($matches); //结果为：Array ( [0] => def )
```

上面的代码简单的执行了一个匹配，简单的判断def是否能匹配成功，但是正则表达式的强大的地方是进行模式匹配，因此更多的时候，会使用模式：

```php
$subject = "abcdef";
$pattern = '/a(.*?)d/';
preg_match($pattern, $subject, $matches);
print_r($matches); //结果为：Array ( [0] => abcd [1] => bc )
```






###查找所有匹配结果

preg_match只能匹配一次结果，但很多时候我们需要匹配所有的结果，preg_match_all可以循环获取一个列表的匹配结果数组。

```php
$p = "|<[^>]+>(.*?)</[^>]+>|i";
$str = "<b>example: </b><div align=left>this is a test</div>";
preg_match_all($p, $str, $matches);
print_r($matches);
```

可以使用preg_match_all匹配一个表格中的数据：

```php
$p = "/<tr><td>(.*?)<\/td>\s*<td>(.*?)<\/td>\s*<\/tr>/i";
$str = "<table> <tr><td>Eric</td><td>25</td></tr> <tr><td>John</td><td>26</td></tr> </table>";
preg_match_all($p, $str, $matches);
print_r($matches);
```


```php
<?php
$str = "<ul>
            <li>item 1</li>
            <li>item 2</li>
        </ul>";
//在这里补充代码，实现正则匹配所有li中的数据
$p = "/<li>(.*)<\/li>/i";
$p = "/<li>(.*)<\/li>/i";//解释下这个正则：//后面的i表示不区分大小写，<li>(.*?)<\/li>表示li标签内的匹配的()内的值有多少，括号内的.表示所有单字符,*表示数量为0个或者多个。也就是li标签内有字符就显示出来
preg_match_all($p,$str,$matches);
print_r($matches[1]);

// $p = "|<[^>]+>(.*?)</[^>]+>|i";
// $str = "<b>example: </b><div align=left>this is a test</div>";
// preg_match_all($p, $str, $matches);
// print_r($matches);

// // 可以使用preg_match_all匹配一个表格中的数据：
// $p = "/<tr><td>(.*?)<\/td>\s*<td>(.*?)<\/td>\s*<\/tr>/i";
// $str = "<table> <tr><td>Eric</td><td>25</td></tr> <tr><td>John</td><td>26</td></tr> </table>";
// preg_match_all($p, $str, $matches);
// print_r($matches);
// // echo $matches[1];
?>
```



###正则表达式的搜索和替换

正则表达式的搜索与替换在某些方面具有重要用途，比如调整目标字符串的格式，改变目标字符串中匹配字符串的顺序等。

例如我们可以简单的调整字符串的日期格式：

```php
$string = 'April 15, 2014';
$pattern = '/(\w+) (\d+), (\d+)/i';
$replacement = '$3, ${1} $2';
echo preg_replace($pattern, $replacement, $string); //结果为：2014, April 15
```

其中${1}与$1的写法是等效的，表示第一个匹配的字串，$2代表第二个匹配的。

通过复杂的模式，我们可以更加精确的替换目标字符串的内容。

```php
$patterns = array ('/(19|20)(\d{2})-(\d{1,2})-(\d{1,2})/',
                   '/^\s*{(\w+)}\s*=/');
$replace = array ('\3/\4/\1\2', '$\1 =');//\3等效于$3,\4等效于$4，依次类推
echo preg_replace($patterns, $replace, '{startDate} = 1999-5-27'); //结果为：$startDate = 5/27/1999
//详细解释下结果：(19|20)表示取19或者20中任意一个数字，(\d{2})表示两个数字，(\d{1,2})表示1个或2个数字，(\d{1,2})表示1个或2个数字。^\s*{(\w+)\s*=}表示以任意空格开头的，并且包含在{}中的字符，并且以任意空格结尾的，最后有个=号的。
```

用正则替换来去掉多余的空格与字符：

```php
$str = 'one     two';
$str = preg_replace('/\s+/', ' ', $str);
echo $str; // 结果改变为'one two'
```



```php
<?php
$str = '主要有以下几个文件：index.php, style.css, common.js';
//将目标字符串$str中的文件名替换后增加em标签
$p = '/\w+\.\w+/i';
$str = preg_replace($p, '<em>$0</em>', $str);
echo $str;
?>
```



###正则匹配常用案例

正则匹配常用在表单验证上，一些字段会有一定的格式要求，比如用户名一般都要求必须是字母、数字或下划线组成，邮箱、电话等也都有自己的规则，因此使用正则表达式可以很好的对这些字段进行验证。

```php
<?php
$user = array(
    'name' => 'spark1985',
    'email' => 'spark@imooc.com',
    'mobile' => '13312345678'
);
//进行一般性验证
if (empty($user)) {
    die('用户信息不能为空');
}
if (strlen($user['name']) < 6) {
    die('用户名长度最少为6位');
}
//用户名必须为字母、数字与下划线
if (!preg_match('/^\w+$/i', $user['name'])) {
    die('用户名不合法');
}
//验证邮箱格式是否正确
if (!preg_match('/^[\w\.]+@\w+\.\w+$/i', $user['email'])) {
    die('邮箱不合法');
}
//手机号必须为11位数字，且为1开头
if (!preg_match('/^1\d{10}$/i', $user['mobile'])) {
    die('手机号不合法');
}
echo '用户信息验证成功';
?>
```