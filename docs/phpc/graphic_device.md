###PHP图形操作之GD库简介

GD指的是Graphic Device，PHP的GD库是用来处理图形的扩展库，通过GD库提供的一系列API，可以对图像进行处理或者直接生成新的图片。

PHP除了能进行文本处理以外，通过GD库，可以对JPG、PNG、GIF、SWF等图片进行处理。GD库常用在图片加水印，验证码生成等方面。

PHP默认已经集成了GD库，只需要在安装的时候开启就行。


```php
<?php
header("content-type: image/png");
$img=imagecreatetruecolor(100, 100);                //创建一个真彩色的空白图片：
$red=imagecolorallocate($img, 0xFF, 0x00, 0x00);    //进行分配画笔颜色
imagefill($img, 0, 0, $red);                        //进行线条的绘制，通过指定起点跟终点来最终得到线条。
imagepng($img);                                     //得到一个图片文件，指定文件名将绘制后的图像保存到文件中。
imagedestroy($img);                                 //销毁图片
?>
```






###PHP图形操作之绘制线条

要对图形进行操作，首先要新建一个画布，通过imagecreatetruecolor函数可以创建一个真彩色的空白图片：


```php
$img = imagecreatetruecolor(100, 100);
```

GD库中对于画笔所用的颜色，需要通过imagecolorallocate函数进行分配，通过参数设定RGB的颜色值来确定画笔的颜色：

```php
$red = imagecolorallocate($img, 0xFF, 0x00, 0x00);
```

然后我们通过调用绘制线段函数imageline进行线条的绘制，通过指定起点跟终点来最终得到线条。

```php
imageline($img, 0, 0, 100, 100, $red);
```

线条绘制好以后，通过header与imagepng进行图像的输出。

```php
header("content-type: image/png");
imagepng($img);
```


最后可以调用imagedestroy释放该图片占用的内存。

```php
imagedestroy($img);
```

通过上面的步骤，可以发现PHP绘制图形非常的简单，但很多时候我们不只是需要输出图片，可能我们还需要得到一个图片文件，可以通过imagepng函数指定文件名将绘制后的图像保存到文件中。

```php
imagepng($img, 'img.png');
```


```php
<?php
ob_clean();//可能图像显示失败，添加这个在开启gd的情况下能解决问题
$img = imagecreatetruecolor(500, 500);
$red = imagecolorallocate($img, 0xFF, 0x00, 0x00);
//在这里使用imageline绘制线条
imageline($img, 0, 0, 500, 500, $red);
header("content-type: image/png");
imagepng($img);
imagedestroy($img);


/*header("content-type: image/png");
$img=imagecreatetruecolor(100, 100);                //创建一个真彩色的空白图片：
$red=imagecolorallocate($img, 0xFF, 0x00, 0x00);    //进行分配画笔颜色
imagefill($img, 0, 0, $red);                        //进行线条的绘制，通过指定起点跟终点来最终得到线条。
imagepng($img);                                     //得到一个图片文件，指定文件名将绘制后的图像保存到文件中。
imagedestroy($img);                                 //销毁图片*/
?>
```



###PHP日期和时间之取得当前的Unix时间戳



```php

```


###PHP日期和时间之取得当前的Unix时间戳



```php

```



###PHP日期和时间之取得当前的Unix时间戳



```php

```



###PHP日期和时间之取得当前的Unix时间戳



```php

```