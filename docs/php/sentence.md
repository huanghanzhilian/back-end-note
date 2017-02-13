###PHP-顺序结构

顺序结构就像一条直线，按着顺序一直往下执行。我们编写的代码默认都是按照顺序结构执行的。

```php
<?php
    $shoesPrice = 49; //鞋子单价
    $shoesNum = 1; //鞋子数量
	$shoesMoney = $shoesPrice * $shoesNum;

	$shirtPrice = 99; //衬衣单价
	$shirtNum = 2; //衬衣数量
	$shirtMoney = $shirtPrice * $shirtNum;

	$orderMoney = $shoesMoney +  $shirtMoney;

	echo $orderMoney ;
?>
//247
```

###PHP条件结构之if…else…

条件结构就像一个岔路口，可以向左走，也可以向右走。比如上洗手间，我们知道我们的性别，这时候我们需要根据洗手间提供的条件，左边男洗手间，右边女洗手间，或者正好相反，其中性别就是这个条件结构的条件。再比如，现在的分数都流行使用A、B、C来分级，假设考试成绩是93分，可以将其设置为等级A，考试成绩是87，可以将其设置为等级B，这里分数区间即为条件结构中的条件。

```php
<?php
    date_default_timezone_set('Asia/ShangHai');
    $today = date('m-d',time());//获取当天日期
	$birthday = "09-22";//生日
	$money = 238;//消费金额
	$discount = 0.8;//八折优惠
	if($today == $birthday){
	    $money = $money * $discount;
    }else{
        $money = $money * 1;
    }
    echo $today."<br />";
	echo $money;
?>
/*02-13
238*/
```

###PHP条件结构之if…else if…

```php
<?php
    $totalMoney = 0;//总工资
    $basicMoney =  2000;//基本工资
	$sex = "男";

	if($sex == "男"){
		$totalMoney = $basicMoney  + 0;// 男的没奖金
	}else if($sex == "女"){
		$totalMoney = $basicMoney  + 300;// 女的有奖金300元
	}
	echo $totalMoney;
?>
//2000
```

###PHP条件结构之if…else if…else…

```php
<?php
date_default_timezone_set('asia/shanghai');
$week = date("w");//获取当天星期几
$info = "";//提示信息
if($week == 1){
    $info = "上午有课";
}else if($week == 3){
	$info = "下午有课";	 
}else{
	$info = "今天没课";
}
echo $info; //输出提示信息
?>
//上午有课
```

###PHP条件结构之switch…case…

首先判断条件，若条件的返回值为条件值一，则执行任务一，若条件返回的值为条件值二，则执行任务二，若条件的返回值既不是条件值一也不是条件值二，则执行默认任务。break的作用是结束switch（后面会有专门举例说明），使用 switch 语句可以避免冗长的 “if..else if..else”代码块。

```php
<?php
$num = rand(1,4);//获取1至50的随机数
$info = "";//提示信息
switch($num){
    case 1:
		$info = "恭喜你！中了一等奖！";
		break;
	case 2:
		$info = "恭喜你！中了二等奖！";
		break;
 	case 3:
		$info = "恭喜你！中了三等奖！";
		break;
	default:
		$info = "很遗憾！你没有中奖！";
}
 echo $info."<br><br>"; //输出是否中奖
 echo '<a href="#" onClick="document.location.reload()">重新抽奖</a>';
?>
```

###PHP条件结构之switch…case…中的break

break的作用是阻止代码进入下一个case 中继续执行。

```php
<?php
//A例子
$num = 2;
$sum  = 10; 
switch($num){
    case 1:
		$sum = $sum  + 10;
		break;
	case 2:
		$sum = $sum  + 10;
		break;
 	case 3:
		$sum = $sum  + 10;
		break;
	default:
		$sum = $sum  + 10;
}
 echo "A例子的值是：".$sum."<br />";
//B例子
$num = 2;
$sum  = 10; 

switch($num){
	case 1:
		$sum = $sum  + 10;
	case 2:
		$sum = $sum  + 10;
	case 3:
		$sum = $sum  + 10;
	default:
		$sum = $sum  + 10;
}
 echo "B例子的值是：".$sum."<br />";
?>
/*A例子的值是：20
B例子的值是：40
case的意思是，符合条件，就从这一行开始执行；
所以，如果num=2， A就从case2开始执行，10+10，再执行break，就结束了，就是20；
B就从case2开始执行，10+10，之后继续执行28行的case3，和defalult,，所以就是10+10+10+19=40；
*/
```

###PHP中循环结构之while循环语句

循环结构就像一圈圈地跑足球场，跑完一圈再跑一圈。也就是说，在符合的条件下，重复执行某项任务。像400米一圈的跑道，跑800米的话就跑2圈，当跑完第一圈接着跑第二圈，第二圈结束已经达到800米，终止跑步

```php
<?php
$sum = 12;//小宠物当前的饥饿程度
echo "我饿啦:-(";
echo "<br />";
while($sum<100)
{//小宠物的饥饿程度到100，表示小宠物吃饱啦,不用继续喂了，没吃饱继续喂食
    $num = rand(1,20);//随机数，模拟喂食小宠物的小面包
    $sum = $sum + $num; //小宠物吃小面包
    if($sum<=100){
		echo "恢复了<b>".$num."</b>点饥饿值"."<br/>";
	    echo "当前饥饿值为<b>".$sum."</b>";
		echo "<br />";
	}else {
        $num=$num-($sum-100);
        echo "恢复了<b>".$num."</b>点饥饿值"."<br/>";
	    echo "当前饥饿值为<b>"."1000"."</b>";
		echo "<br />";
    }
}
echo "终于吃饱啦^_^";
?>
```

###PHP中循环结构之do while循环语句

在PHP中循环语句还有另一种：do...while循环语句语法如下：

```php
<?php
do{ 
     //执行任务
}while(条件)
?>
```

首先执行任务（上一节的while语句是先判断条件是否成立，再执行任务），执行任务完毕，判断某个条件是否符合（条件返回值是否为TRUE），若符合则再次执行任务，执行完毕任务，继续判定条件。

```php
<?php
$i =  1 ; //从第1圈开始跑
do{  //跑10圈
    echo "在跑第".$i."圈。";
	$i++;
}while($i<=10);
?>
```

###PHP中循环结构之while与do…while语句的区别

while与do…while循环语句的区别是，while先判断条件是否成立，后执行循环，do...while先执行一次任务，再判断是否继续执行循环，也就是说do...while至少会执行一次任务。当条件为FALSE时，while中的任务会一次也不执行，do...while中的任务会执行1次。

```php
<?php
    //A例子
	$num = 2;
	$sum  = 10;
	while($num>3){
		$sum = $sum  + 10;
	}
	echo "A例子的结果：".$sum."<br />";
	//B例子
	$num = 2;
	$sum  = 10;
	do{
		$sum = $sum  + 10;
	}while($num>3);
	echo "B例子的结果：".$sum."<br />";
?>
/*A例子的结果：10
B例子的结果：20*/
```

###PHP中循环结构之do…while语句的运用优势举例

while和do...while可以根据具体情况选用。假设有一种棋类游戏，首先掷骰子，若不为6，前进骰子的点数的步长；若为6，前进骰子的点数的步长，并可以再掷一次。

```php
<?php
    //while例子
	$sum  = 0; 
	$num = rand(1,6); //获取1至6的随机数，模拟掷骰子
	$sum = $sum  + $num;//前进步长
	while($num==6){
		$num = rand(1,6);//获取1至6的随机数，模拟掷骰子
		$sum = $sum  + $num;//前进步长
	};
	echo "while例子执行完毕，前进：".$sum ."<br />";
	//do...while例子
	$sum  = 0; 
	do{
		$num = rand(1,6);//获取1至6的随机数，模拟掷骰子
		$sum = $sum  + $num;//前进步长
	}while($num==6);
	echo "do...while例子执行完毕，前进：".$sum ."<br />";
?>
```

###PHP中循环结构之for循环语句



在PHP中还有一种循环语句，for循环语句结构如下：

```php
<?php
for(初始化;循环条件;递增项){
      //执行任务
}
?>
```

for 语句中，“初始化”在循环开始前无条件求值一次，“循环条件”在每次循环开始前求值。如果值为 TRUE，则继续循环，执行循环体语句（执行任务）。如果值为 FALSE，则终止循环。“递增项”在每次循环之后被求值（执行）。其常用于循环执行代码块指定的次数。


```php
<?php
//for语句写法
for($i = 1,$sum = 0;$i<=100;$i++){
    $sum = $sum + $i; //	累加求和
}
echo "for语句的运行结果：".$sum."<br />" ;

//while语句写法
$i =  1 ; // 从1开始累加
$sum = 0; //初始化和为0
while($i<=100){  //判断是否小于100
	$sum = $sum + $i; //	累加求和
	$i++; //递增1
}
echo "while语句的运行结果：".$sum."<br />" ;
?>
/*for语句的运行结果：5050
while语句的运行结果：5050*/
```

###PHP中循环结构之foreach循环语句(一)

在PHP中foreach循环语句，常用于遍历数组，一般有两种使用方式:不取下标、取下标。

（1）只取值，不取下标

```php
<?php
 foreach (数组 as 值){
//执行的任务
}
?>
```

（2）同时取下标和值

```php
<?php
foreach (数组 as 下标 => 值){
 //执行的任务
}
?>
```

```php
<?php
$students = array(
'2010'=>'令狐冲',
'2011'=>'林平之',
'2012'=>'曲洋',
'2013'=>'任盈盈',
'2014'=>'向问天',
'2015'=>'任我行',
'2016'=>'冲虚',
'2017'=>'方正',
'2018'=>'岳不群',
'2019'=>'宁中则',
);//10个学生的学号和姓名，用数组存储

//使用循环结构遍历数组,获取学号和姓名  

foreach($students as  $v){ 
    echo $v;//输出（打印）姓名
	echo "<br />";
}
?>
```

###PHP中循环结构之foreach循环语句(二)

```php
<?php
$students = array(
'2010'=>'令狐冲',
'2011'=>'林平之',
'2012'=>'曲洋',
'2013'=>'任盈盈',
'2014'=>'向问天',
'2015'=>'任我行',
'2016'=>'冲虚',
'2017'=>'方正',
'2018'=>'岳不群',
'2019'=>'宁中则',
);//10个学生的学号和姓名，用数组存储

//使用循环结构遍历数组,获取学号和姓名  
foreach($students as $key =>$v)
{ 
    echo $key.":".$v;//输出（打印）学号：姓名
	echo "<br />";
}
?>
/*2010:令狐冲
2011:林平之
2012:曲洋
2013:任盈盈
2014:向问天
2015:任我行
2016:冲虚
2017:方正
2018:岳不群
2019:宁中则*/
```

###PHP中结构嵌套之条件嵌套

条件结构嵌套就像回家的路上会遇到多个十字路口。

```php
<?php
    $totalMoney = 0;//总工资
	$basicMoney =  300;//基本工资
	$sex = "男";
	$noHouse = TRUE; //是否有房
	$houseMoney =  150;//住房补贴
	$isPregnancy = TRUE; //是否怀孕
	$pregnancyMoney =  100;//怀孕补贴
	if($sex =="男")
	{
		$totalMoney = $basicMoney  + 0;// 男的没奖金
	    if($noHouse)	
		{
			$totalMoney = $totalMoney  + $houseMoney;
		} 
	}
	else if($sex == "女")
	{
		$totalMoney = $basicMoney  + 300;// 女的有奖金300元
		if($isPregnancy)
		{
			$totalMoney = $totalMoney  + $pregnancyMoney;
		} 
	}
	echo $totalMoney;
?>

//450
```

###PHP中结构嵌套之循环嵌套

循环结构嵌套，就是类似于跑多个足球场，例如假设有两个足球场，一个大足球场，一个小足球场，在大足球场跑一圈后，再到小足球场跑几圈，跑完几圈后，再到大足球场中继续跑。在遍历二维数组中很常用。

```php
<?php
 $students = array(
'2010'=>array('令狐冲',"59"),
'2011'=>array('林平之',"44"),
'2012'=>array('曲洋',"89"),
'2013'=>array('任盈盈',"92"),
'2014'=>array('向问天',"93"),
'2015'=>array('任我行',"87"),
'2016'=>array('冲虚',"58"),
'2017'=>array('方正',"74"),
'2018'=>array('岳不群',"91"),
'2019'=>array('宁中则',"90"),
);//10个学生的学号、姓名、分数，用数组存储
 
foreach($students as $key=>$val)
{ //使用循环结构遍历数组,获取学号 
     echo $key; //输出学号
	 echo ":";
	 //循环输出姓名和分数
	 foreach($val as $v)
	{
		echo $v; 
	 }
	 echo "<br />";
}
?>
/*
2010:令狐冲59
2011:林平之44
2012:曲洋89
2013:任盈盈92
2014:向问天93
2015:任我行87
2016:冲虚58
2017:方正74
2018:岳不群91
2019:宁中则90
*/
```

###PHP中结构嵌套之循环结构与条件结构嵌套

有时候在执行任务时，对于一些特殊的任务还需要进行额外处理，这个时候就会将循环结构与条件结构嵌套使用。

```php
<?php
 $students = array(
'2010'=>'令狐冲',
'2011'=>'林平之',
'2012'=>'曲洋',
'2013'=>'任盈盈',
'2014'=>'向问天',
'2015'=>'任我行',
'2016'=>'冲虚',
'2017'=>'方正',
'2018'=>'岳不群',
'2019'=>'宁中则',
);//10个学生的学号和姓名，用数组存储
$query = '2014';
//使用循环结构遍历数组,获取学号和姓名
foreach($students as $key => $v)
{
    //使用条件结构，判断是否为该学号
	if($key ==$query)
	{
		echo $v;//输出（打印）姓名
		break;//结束循环（跳出循环）
	}
}
?>
//向问天
```