###cookie简介

Cookie是存储在客户端浏览器中的数据，我们通过Cookie来跟踪与存储用户数据。一般情况下，Cookie通过HTTP headers从服务端返回到客户端。多数web程序都支持Cookie的操作，因为Cookie是存在于HTTP的标头之中，所以必须在其他信息输出以前进行设置，类似于header函数的使用限制。

PHP通过setcookie函数进行Cookie的设置，任何从浏览器发回的Cookie，PHP都会自动的将他存储在$_COOKIE的全局变量之中，因此我们可以通过$_COOKIE['key']的形式来读取某个Cookie值。

PHP中的Cookie具有非常广泛的使用，经常用来存储用户的登录信息，购物车等，且在使用会话Session时通常使用Cookie来存储会话id来识别用户，Cookie具备有效期，当有效期结束之后，Cookie会自动的从客户端删除。同时为了进行安全控制，Cookie还可以设置域跟路径

```php
<?php
setcookie('test', time());
ob_start();//打开输出控制缓冲
print_r($_COOKIE);
$content = ob_get_contents();//复制缓冲区内容到$content中
$content = str_replace(" ", '&nbsp;', $content);
ob_clean();//清空（擦掉）输出缓冲区
header("content-type:text/html; charset=utf-8");
echo '当前的Cookie为：<br/>';
echo nl2br($content);//nl2br 在字符串所有新行之前插入 HTML 换行标记
?>
```



###设置cookie

PHP设置Cookie最常用的方法就是使用setcookie函数，setcookie具有7个可选参数，我们常用到的为前5个：

name（ Cookie名）可以通过$_COOKIE['name'] 进行访问
value（Cookie的值）
expire（过期时间）Unix时间戳格式，默认为0，表示浏览器关闭即失效
path（有效路径）如果路径设置为'/'，则整个网站都有效
domain（有效域）默认整个域名都有效，如果设置了'http://www.huanghanlian.com/',则只在www子域中有效

```php
<?php
$value = 'test';
setcookie("TestCookie", $value);
setcookie("TestCookie", $value, time()+3600);  //有效期一小时
setcookie("TestCookie", $value, time()+3600, "/path/", "huanghanlian.com"); //设置路径与域
?>
```

PHP中还有一个设置Cookie的函数setrawcookie，setrawcookie跟setcookie基本一样，唯一的不同就是value值不会自动的进行urlencode，因此在需要的时候要手动的进行urlencode。


```php
setrawcookie('cookie_name', rawurlencode($value), time()+60*60*24*365); 
```

因为Cookie是通过HTTP标头进行设置的，所以也可以直接使用header方法进行设置。

```php
header("Set-Cookie:cookie_name=value");
```

使用setcookie设置一个名为test，值为$value的Cookie。自己配置PHP环境，写两个页面，第一个页面写入cookie，第二个页面输出cookie。

```php
//页面1
<?php
$value = time();
//$value = 'test';
setcookie('test', $value); 
if (isset($_COOKIE['test'])) {
    echo 'success';
}
?>
```

```php
//页面2
<?php
	print_r($_COOKIE);
?>
//Array ( [test] => 1487095858 )
```


###cookie的删除与过期时间

在PHP中删除cookie也是采用setcookie函数来实现。

```php
setcookie('test', '', time()-1); 
```

可以看到将cookie的过期时间设置到当前时间之前，则该cookie会自动失效，也就达到了删除cookie的目的。之所以这么设计是因为cookie是通过HTTP的标头来传递的，客户端根据服务端返回的Set-Cookie段来进行cookie的设置，如果删除cookie需要使用新的Del-Cookie来实现，则HTTP头就会变得复杂，实际上仅通过Set-Cookie就可以简单明了的实现Cookie的设置、更新与删除。

了解原理以后，我们也可以直接通过header来删除cookie。

```php
header("Set-Cookie:test=1393832059; expires=".gmdate('D, d M Y H:i:s \G\M\T', time()-1));
```

这里用到了gmdate，用来生成格林威治标准时间，以便排除时差的影响。

```php
<?php
setcookie('test', time());

//在这里试着删除test的cookie值
setcookie('test', '', time()-1); 

var_dump($_COOKIE);
?>
```


###cookie的有效路径

cookie中的路径用来控制设置的cookie在哪个路径下有效，默认为'/'，在所有路径下都有，当设定了其他路径之后，则只在设定的路径以及子路径下有效，例如：

```php
setcookie('test', time(), 0, '/path');
```

上面的设置会使test在/path以及子路径/path/abc下都有效，但是在根目录下就读取不到test的cookie值。

一般情况下，大多是使用所有路径的，只有在极少数有特殊需求的时候，会设置路径，这种情况下只在指定的路径中才会传递cookie值，可以节省数据的传输，增强安全性以及提高性能。

当我们设置了有效路径的时候，不在当前路径的时候则看不到当前cookie

```php
setcookie('test', '1',0, '/path');  
var_dump($_COOKIE['test']);  
```



```php
<?php
//补充路径参数，实现有效路径的设置
setcookie('test', '1', 0, '/path');
var_dump($_COOKIE['test']);
?>
```




###session与cookie的异同



cookie将数据存储在客户端，建立起用户与服务器之间的联系，通常可以解决很多问题，但是cookie仍然具有一些局限：

cookie相对不是太安全，容易被盗用导致cookie欺骗
单个cookie的值最大只能存储4k
每次请求都要进行网络传输，占用带宽

session是将用户的会话数据存储在服务端，没有大小限制，通过一个session_id进行用户识别，PHP默认情况下session id是通过cookie来保存的，因此从某种程度上来说，seesion依赖于cookie。但这不是绝对的，session id也可以通过参数来实现，只要能将session id传递到服务端进行识别的机制都可以使用session。


```php
<?php
//开始使用session
session_start();
//设置一个session
$_SESSION['test'] = time();
//显示当前的session_id
echo "session_id:".session_id();
echo "<br>";

//读取session值
echo $_SESSION['test'];

//销毁一个session
unset($_SESSION['test']);
echo "<br>";
var_dump($_SESSION);
?>
```


###使用session

在PHP中使用session非常简单，先执行session_start方法开启session，然后通过全局变量$_SESSION进行session的读写。

```php
session_start();
$_SESSION['test'] = time();
var_dump($_SESSION);
```

session会自动的对要设置的值进行encode与decode，因此session可以支持任意数据类型，包括数据与对象等。

```php
session_start();
$_SESSION['ary'] = array('name' => 'jobs');
$_SESSION['obj'] = new stdClass();
var_dump($_SESSION);
```

默认情况下，session是以文件形式存储在服务器上的，因此当一个页面开启了session之后，会独占这个session文件，这样会导致当前用户的其他并发访问无法执行而等待。可以采用缓存或者数据库的形式存储来解决这个问题


```php
session_start();
$_SESSION['name'] = 'jobs';
echo $_SESSION['name'];
?>
//jobs
```




###删除与销毁session

删除某个session值可以使用PHP的unset函数，删除后就会从全局变量$_SESSION中去除，无法访问。

```php
session_start();
$_SESSION['name'] = 'jobs';
unset($_SESSION['name']);
echo $_SESSION['name']; //提示name不存在
```

如果要删除所有的session，可以使用session_destroy函数销毁当前session，session_destroy会删除所有数据，但是session_id仍然存在。

```php
session_start();
$_SESSION['name'] = 'jobs';
$_SESSION['time'] = time();
session_destroy();
```

值得注意的是，session_destroy并不会立即的销毁全局变量$_SESSION中的值，只有当下次再访问的时候，$_SESSION才为空，因此如果需要立即销毁$_SESSION，可以使用unset函数。

```php
session_start();
$_SESSION['name'] = 'jobs';
$_SESSION['time'] = time();
unset($_SESSION);
session_destroy(); 
var_dump($_SESSION); //此时已为空
```

如果需要同时销毁cookie中的session_id，通常在用户退出的时候可能会用到，则还需要显式的调用setcookie方法删除session_id的cookie值。

```php
?php
session_start();
$_SESSION['name'] = 'jobs';
//在这里删除name的session值
unset($_SESSION['name']);
if (isset($_SESSION['name'])) {
    echo $_SESSION['name'];
}
?>
```



###使用session来存储用户的登录信息

session可以用来存储多种类型的数据，因此具有很多的用途，常用来存储用户的登录信息，购物车数据，或者一些临时使用的暂存数据等。

用户在登录成功以后，通常可以将用户的信息存储在session中，一般的会单独的将一些重要的字段单独存储，然后所有的用户信息独立存储。


```php
$_SESSION['uid'] = $userinfo['uid'];
$_SESSION['userinfo'] = $userinfo;
```


一般来说，登录信息既可以存储在sessioin中，也可以存储在cookie中，他们之间的差别在于session可以方便的存取多种数据类型，而cookie只支持字符串类型，同时对于一些安全性比较高的数据，cookie需要进行格式化与加密存储，而session存储在服务端则安全性较高。


```php
<?php
session_start();
//假设用户登录成功获得了以下用户数据
$userinfo = array(
    'uid'  => 10000,
    'name' => 'spark',
    'email' => 'spark@imooc.com',
    'sex'  => 'man',
    'age'  => '18'
);
header("content-type:text/html; charset=utf-8");

/* 将用户信息保存到session中 */
$_SESSION['uid'] = $userinfo['uid'];
$_SESSION['name'] = $userinfo['name'];
$_SESSION['userinfo'] = $userinfo;

//* 将用户数据保存到cookie中的一个简单方法 */
$secureKey = 'imooc'; //加密密钥
$str = serialize($userinfo); //将用户信息序列化
//用户信息加密前
$str = base64_encode(mcrypt_encrypt(MCRYPT_RIJNDAEL_256, md5($secureKey), $str, MCRYPT_MODE_ECB));
//用户信息加密后
//将加密后的用户数据存储到cookie中
setcookie('userinfo', $str);

//当需要使用时进行解密
$str = mcrypt_decrypt(MCRYPT_RIJNDAEL_256, md5($secureKey), base64_decode($str), MCRYPT_MODE_ECB);
$uinfo = unserialize($str);
echo "解密后的用户信息：<br>";
print_r($uinfo);
?>
```