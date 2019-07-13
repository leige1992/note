

## java

### java语言的简介

<center><h2>第一章</h2></center>

#### 	java简单介绍

​		+1995年sun公司创建，后被甲骨文（oracle）收购

#### 	java主要做什么 为什么学java

​		+ 可以做桌面应用和互联网软件（重点） 为了爱情

#### 	常用的dos命令

​		+ cd\,cd..,d:,dir,cls,ipconfig

	#### 	下载jdk配置环境变量 

​		+ 自己去下载

	#### 	注释和标识符，关键字

​		关键字：小写，被java强制占用，相当于命令

​		标识符：自己定义的东西，有a-z，A-Z,$,_,不能以数字开头

​		注释：//，/*  内容 */

#### 基本数据类型

+ 基本类型
  + 整数（100 ， 30）
    + 二进制（0b开头）
    + 十进制
    + 八进制（0开头）
    + 十六进制（0x开头）
  + 布尔类型
  + 字符类型
  + 浮点数

+ 引用数据类型
  + 数组
  + 类
  + 接口

##### 常量和变量

常量： 不变的数据

变量： 存放数据的容器

##### 数据存储

+ 硬盘永久存储，内存是零时存储

+ 计算机最小的信息单元为bit，但是储存数据的最小单元为字节B（8bit）

##### 四类八种数据类型

+ 整数
  + byte类型（范围 -128~127）（1字节）
  + short类型（两个字节）
  + int类型（整形数据默认为int类型）（4字节）
  + long（申请为long类型需要加L 如：long AA=8L）（8字节）
    + 不加l的情况 long a = 31231231231232;设计到隐式类型转换  范围是int类型
+ 小数
  + double(默认的小数类型)（8字节）
  + float（4字节）
+ 字符
+ 布尔
+ String类型 

##### 变量定义的三要素

+ 变量类型  变量名  数据值（int aa = 20）

##### 数据类型转换

+ 自动类型转换（byte->int->long>float>double）
  + （byte a=1;byte a += 1;）（对的）
  + （byte a=1; a=a+1;）（编译报错 1是int类型）
+ 强制类型转换（由大的数据到小的数据）（int a = 3; byte b = (byte) a; ）

##### 运算符

+ 计算运算符

  + - * /  %

+ 赋值

  =，+=，-=

+ 逻辑

  ！ ^,|,&,&&,||（短路或）

+ 三元运算符

  例：2==3? "haha":"hehe"

+ 比较运算符

  <,>,>=,<=,==

#### 引用数据类型

1：导包

2：创建（类型名  名称 = new 类型()）

3：使用

+ Scanner（nextInt()接受键盘输入整数    next()接受字符串）
+ Random（随机产生随机数）伪随机数    方法：nextInt(20):产生0-19的整数随机数  nextDouble()：0-1之间的随机数 不包含1；

<center><h2>第二章</h2></center>

#### 流程控制语句

+ if条件语句

+ while

+ do{}while()

+ break

+ continue

+ switch(变量){case 1: 。。}

  

  ~~~javascript
  //switch的穿透性
  switch(e) {
      case 1:
      case 2:
      case 3:
         .......
  }
  
  ~~~

#### 数组

##### 定义

+ 数据集合，数据的容器 只能存储同一个类型数据的容器

##### 定义数组的公式

~~~~~~java
//数据类型[] 数据名称 = new 数据类型(个数) 个数指定将不再改变
1. int[] arr = new int[12]; //动态初始化 （）内写的是数组的长度
2. int[] arr2 = new int[]{1,2,3} //静态初始化
3. int[] arr3 = {1, 2,3 4}//最常用的数组定义方法
~~~~~~

##### 属性 length

##### jvm运行时内存的划分

当虚拟机运行时，操作系统会划分默认64兆空间给虚拟机，然后虚拟机来管理分配的空间，基本可以分为五类

+ 寄存器：cpu和内存之间发生的事情
+ 本地方法栈：jvm调用系统中的功能  
+ 数据和方法共享区： 程序运行时期 class文件进入的地方
+ 方法栈：所有方法运行时候进去的内存
+ 堆：存储的是容器和对象

##### 数组中常见的两个异常

+ 越界异常

  ~~~~~~java
  int[] arr = {2,3} sop(arr[3])
  ~~~~~~

  

+ 空指针异常 

  ~~~~~~java
  int[] arr = {1,2} arr = null; //再用arr操作数组 会报空指针异常
  ~~~~~~

##### 二维数组定义和遍历

~~~~~~java
int[][] arr = {{1,2},{3,4}} //这是推荐的方法
//不推荐：
int[][] arr = new int[3][];
arr[1][] = new int(3);
//3
int[][] arr = new int[2][3];
~~~~~~

### 方法

##### 概念

+ 解决事情或者实现功能的代码集合

##### 定义和使用

~~~~~~java
/*
	修饰符 返回值类型 方法名 参数 方法体	
*/
public static int get(int x, int y) {//形参   // 
    。。。。。
        return //会把返回值 返回给方法的调用者
}
~~~~~~

##### 注意事项

+ 方法不能写在另一个方法的里面

##### 方法的重载

+ 方法名相同，方法列表不同（其他不要考虑）

#### 引用类型

##### 类的定义与使用

+ 使用类的形式， 对现实的事物进行描述   包含属性和方法

~~~~~~java
//创建类的格式
/*
    修饰符 class 类名 {
        属性定义：
            修饰符 数据类型 变量名 = 值
        方法定义：
            修饰符 返回值类型 方法名(参数列表){

        }
	}
 */
public class Phone {
    int haha;
    public int haha() {
        
    }
}
//使用
Phone p = new Phone()
//默认会p.haha=0;
sop(p.haha);
~~~~~~

##### 类 ArrayList           集合中只可以放引用类型数据

**八种基本类型  对应八种引用类型**

~~~~~~
//申明和基本使用方法
// ArrayList<数据类型> 变量名 = new ArrayList<数据类型>();
~~~~~~

+ add(int, 值)  两个参数  第一个参数是位置  第二个是值  不写第一个默认顺序添加元素
+ get() 获取值
+ size() 返回 集合中元素个数
+ set(index, 值) 设置值
+ iterator 迭代
+ remove(index)
+ clear()

##### ASCII 编码表  美国标准信息交换代码

+ a-z对应 97-122，  A-Z 对应 65-90，  0-9对应 48-57
+ char的取值范围 65535

#### 一些经典算法

##### 选择排序和冒泡排序

~~~~~java
//选择排序
//选择排序就是一个元素和每一元素都要比较  出最终结果
......(int[] arr){
    for(int i=0;i<arr.length-1;i++) {
        for(j=i+1;j<arr.length;j++) {
            if(arr[i]>arr[j]) {
                //调换位置
            }
        }
    }
}
//冒泡排序  相邻的元素在排序
for(int i=0;i<arr.length-1;i++) {
    for(int j=0;j<arr.length-i-1;j++) {
        if(arr[j]>arr[j+1]) {
            ........//调换位置
        }
    }
}
~~~~~

##### 折半查找

~~~~~~Java
//折半查找
//1.定义三个指针 2.判断如果是大于midle 3.如果小于midle 3.等于输出下标
public static int binarySearch(int[] arr, int val) {
    int min = 0, max = arr.length-1;
    int mid = (min + max) / 2;
    while(max >= min) {
        if(val > arr[mid]) {
            min = mid + 1;
            mid = (min + max) / 2;
        }else if(val< arr[mid]) {
            max = mid - 1;
            mid = (min + max) / 2;
        }else {
            return mid;
        }
    }
    return -1;
}
~~~~~~

#### 用eclipce编写java

##### 熟悉配置

- alt+// 代码自动补全（syso, for）
- ctrl + shift + f 格式化
- ctrl + shift + /多行注释
- ctrl + shift + o 导包的快捷键
- ctrl + alt + 上下 复制当前行
- 遇到ctrl+1提示意见  解决小叉号
- ctrl+2键rename 接收返回值
- ctrl+t 展开类的继承关系图
- ctrl+alt+m 快速利用代码块创建方法

##### 断点调试

+ f5 step into
+ f6 单行执行

##### 导入删除（import）

#### 面向对象开发

#####  世间万物皆对象（自己是是世界的指挥者）

+ 变量和方法都属于类的成员（成员方法  成员变量）

##### 局部变量和成员变量的不同点

+ 定义位置不同 
  + 成员变量：定义在类中，方法外
  + 局部变量：方法内 语句内

+ 作用域不同
  + 成员变量：作用在整个类里面
  + 局部变量：方法内 语句内
+ 默认值不同
  + 成员变量：有自己的默认值
  + 局部变量： 没有默认值
+ 生命周期不同
  + 成员变量：跟随对象在堆内存中存储，内存等待jvm清理，生命相对较长
  + 局部变量：跟随方法出栈，生命相对较短
+ 内存位置不同
  + 成员变量： 跟随方法在堆中存储
  + 局部变量： 跟随方法进入栈内存

##### 三大特征

+ 封装（private 修饰只是其中一个方式   只能在自己类中访问）

  + this关键字（本类的对象引用） 来区分成员变量和局部变量

+ 继承（extends关键字）

  + 代码复用性提高 提升了代码的效率
  +  java只支持单继承 只能有一个父类  多继承会造成安全性问题    比如多个类中成员变量和方法名称一样时
  + 可以多层继承
  + 字类的共性抽取 形成了父类

+ 多态

  <center><h2>第三章</h2></center>

#### 继承

##### 方法重写

+ 子类中，出现和父类一模一样的方法的时候，字类重回写父类的方法（覆盖）
+ 子类重写方法  要权限大于等于父类（public protect defult private）

##### 子类和父类

+ 祖宗类  Object

+ 父类， 内容最共性
+ 子类， 不单有公共性，还拥有自己的特性
+ 在子类中，调用父类的成员，关键字是super，调用父类的成员（超类，基类） 子类（派生类）

##### 抽象类（类在共性抽取时  形成的父类描述时越来越抽象  说不明白）

~~~~~~java
public abstract class {
    public abstract void work(); //共性抽取 怎样工作已经变的很抽象  所以没有方法主体
}
**不可以被实例化***
**字类必须实现抽象类的方法** 保证程序设计的完整性
~~~~~~

####  接口

+ 比抽象类还要抽象的类   描述所应该具备的方法，并没有具体的实现，具体的实现由接口实现类实现(也是class文件)
+ 一切事物均有功能  即一切事物均有接口

##### 接口大的定义（同样不能实例化）

~~~~~~java
public interface JieKou {
	  **必须全是抽象方法**
      //固定模板
      public static final int i = 0;//不管你怎么写 不会报错  然而虽然你不写  结果默认都是这个
      public abstract void haha();//同上
}
~~~~~~

##### 实现接口（同时可以继承类  实现多个接口）

+ implements
+ 必须覆盖掉接口中所有的抽象方法  否则实现类还是一个抽象类
+ 接口的多实现（多个接口同时实现不能由 方法名一样返回值类型不一样的时候  这样会造成实现类方法重复定义）

##### static关键字（用static修饰的东西可以直接用类名点的形式调用）

##### 接口的多继承（接口直接可以多继承）

##### 接口的思想

+ 降低耦合度
+ 增加扩展性
+ 满足暴露出来的规则

##### 接口和抽象类的区区别

+ 相同点：
  + 都位于继承的顶端，用于被其他类继承或实现
  + 都不能被实例化
  + 都包含抽象方法，字类必须实现这些抽象方法
+ 不同点：
  + 抽象类为部分方法提供实现，避免子类重复实现这些方法，提高复用性，接口只包含抽象方法
  + 一个类只能继承一个直接父类（可能是抽象类 ），但可以实现多个接口
  + 抽象类 is...a的关系   接口 is...like的关系

#### 多态（三种方式   普通类，抽象类，接口）

+ 父类引用变量可以指向子类的对象
+ 多态的前提是必须有子父类关系或者类实现接口关系，否则无法实现多态
+ 在使用多态后的父类引用变量调用方法是，会调用子类重写后的方法

~~~~~~java
//成员变量 
Person p = new Student();
成员变量 在编译和运行的时候全看父类
//方法先找子类的重写方法   找不到再找父类    如果父类不定义就会编译失败
//编译看父类   运行看子类
~~~~~~

##### 比较运算符（instanceof）（对有继承关系的类进行判断）

~~~~~~java
Person p = new Student();
boolean b = p instanceof Student;
syso(b) //true
~~~~~~

#### 构造函数

+ 在new的同时 对象的属性初始化赋值
+ 权限 方法名(参数）{} 不能写返回值类型   名称类名一样
+ 不写构造函数，编写编译器自动生成
+ 加private不给外面 类 创造对象
+ this在构造方法之间调用    this( ...)需要写在第一行;  
+ 继承子类 在new的时候 会默认在构造函数第一句加super()

#### final关键字（除了构造方法以外的都可以修饰）

+ 修饰数据类型只能被赋值一次
+ 修饰成员变量  必须在创建对象之前赋值

#### static 关键字（修饰对象的共有属性和方法）

+ 可以用类名直接调用
+ 类进入方法区后， 先加载自己的静态成员，静态属于自己的类 开始执行main jvm到静态区将main方法复制一份压栈执行   
+ 静态的生命周期要早于非静态的存在

+ 静态成员在运行的时候进入数据共享区的静态区

##### 注意事项

+ 不能写this和super
+ 静态的生命周期要早于非静态的存在  所以静态不可以调用非静态

##### 是否加静态

+ 看共性  共性
+ 方法看是否使用了 非静态成员
+ public static final double PI = 3.14;

#### 匿名对象（只能使用一次 一次调用  参数  返回值）

#### 内部类（成员内部类 ）

+ 外部类使用内部类的方法格式

~~~~~~java
//外部类.内部类 变量名= new 外部类（）.new 内部类();
Outer.Inner i = new Outer().newinner();
this.i   outer.this.i
~~~~~~

##### 局部内部类（在方法中的类）

##### 匿名内部类（实际使用）

+ 继承一个类

  ~~~~~~java
  //继承
  new Father(){
      
  }.das;  创建子类对象
  ~~~~~~

+ 实现一个接口

  ~~~~~~java
  //实现接口
  同上
  ~~~~~~

#### 包的概念

#### 访问修饰符（如下图）

![1560411942327](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1560411942327.png)

+ 默认权限只在本包下有用
+ 保护权限 在保外只有继承才可以用（只能在子类的里面  很坑啊 ）

#### 代码块 （写在类中）（优先于构造方法）（先执行静态构造代码块）

##### 构造代码块 {}

##### 静态代码块 static{} （只执行一次）

#### jaava中的文档注释和生成jar包

##### 文档注释（/**回车）

+ eclipse->export->java->javadoc

##### 文档书写

##### 导出jar包

+ eclipse->export->java->jar

##### 使用jar包

+ build path

#### 修饰符总结（记住常用的）

<center><h2>第三章</h2></center>

### Api

#### object类

+ 重写equals
+ 重写toString()  syso默认调用toString

#### String 类

##### 构造函数

+ String()
+ String(char[])
+ String(char[], int offset, int count) 
+ String(byte[]) 字节数组变成字符串 也可以用方法变回来

##### 常用的方法

+ length()   返回字符串长度
+ substring(start, end) 不包含end 重载subString(start) 截取后面的字符串
+ startsWith() 以什么字符开头  
+ endsWith() 以什么结尾
+ toLowerCase()  toUpCase()   
+ contains() 判断是否包含
+ indexOf() 返回查找的字符
+ getBytes()将字符串 改为字节数组数组
+ toCharArray() 变为字节数组
+ charAt(i) 返回i位置的字符
+ 数字范围 48-57    小写 65-90  大写 90-122
+ isEmpty() 字符串是否为空
+ repalce(char oldChar, char newChar)
+ repalce(String old, String newstr)
+ trim()去掉两端的空格

#### StringBuffer类

##### 构造函数

+ Stringbuffer()十六个字节
+ Stringbuffer(String str) 初始化一个字符串缓冲区

##### 常用方法

+ append(String str) 可以链式调用  方法返回this  
+ delete(int start, int end) 移除字符串中的字符
+ insert(int offset, String str)
+ replace(int start, int end, String str)
+ reverse()
+ toString()
+ setCharAt(int i, char ch) 设置指定位置的字符

### 正则表达式

#### 一些常用正则

+ \w     [0-9a-zA-Z_]
+ \d     代表数组0-9
+ {x, }  代表最少x个
+ \D 不是数字

#### 正则举例

+ 验证邮箱    "[\\w]+@[a-z0-9]+\\.([a-z]+)"

#### 字符串中涉及正则表达式的常用方法

+ matches("  ") 
+ split("  ")  使用规则切割字符串
+ replaceAll(正则规则, 替换字符串)

### date类

#### 当前日期的毫秒值（System.currentTimeMillis()）

#### 常用构造函数

+ date()  空参构造器  创建一个date对象
+ date(long 312323l) 吧毫秒值转化为日期对象

#### 常用方法

+ getTime() 获取当前时间的毫秒值
+ setTime(long 112) 设置当前时间为传入对应毫秒值的时间

#### 日期格式化(Date-> String)

~~~~~~java
//使用抽象类 dateFomat下面的子类simpleDateFormat/下面的format犯法

//格式 yyyy年    MM月份  dd月中的天数   HH小时  mm分钟 ss秒
SimpleDateFormat df = new SimpleDateFormat(规则);


SimpleDateFormat df = new SimpleDateFormat(yyyy年MM月dd日 。。。);
String s = df.format(new Date()); //参数数date对象
~~~~~~

#### String ->Date  (dateFoamat中的parse方法)

~~~~~~~java
SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
Date d = sdf.parse("2017-12-23");
~~~~~~~

#### Calendar类（getInsttance()  //获取子类实例） 日历对象

##### get方法

~~~~~java
public static void function() {
    Calendar cd = Calendar.getInstance();
    int year = cd.get(Calendar.YEAR);
    int month = cd.get(Calendar.MONTH) + 1;
    int day = cd.get(Calendar.DAY_OF_MONTH);
    System.out.println(year+"年" + month+"月"+day+"日");
}
~~~~~

##### set方法   set(int field, int value)  set(int year, int month, int day)

~~~~~~java
....
~~~~~~

##### add方法（int field，int value）//时间段偏移    支持负数

##### getTime() 让日历类 变成Date对象

#####  计算闰年的高级算法

~~~~~~java
Calendar c = Calendar.getInstance();
c.set(year, 2， 1)；//设置到当年的3月一号
c.add(Calendar.DAY_OF_MONTH, -1)
c.get(Calendar.DAY_OF_MONTH) //判断2月份的天数是28天还是29天

~~~~~~

### 基本类型的包装类

#### 主攻的包装类 integer

+ Integer.parseInt()  静态方法

+ Interger.toString()  静态方法

+ Integer(String s) 保存字符串   获取值的话   对象.intValue()
+ 两个静态成员    MAX_VALUE   MIN_VALUE
+ 三个静态方法   转二进制 toBinaryString()   转十进制toOctalString()   转十六进制toHexString()    都是十进制  转的   返回值是字符串 

#### System类

##### 常用方法

+ System.currentTimeMillis()
+ System.exit(0)  退出虚拟机
+ System.gc()   jvm在内存中，收取对象的垃圾
+ System.getProperties()    返回系统属性
+ System.arrayCopy   复制数组   使用时自己查文档

#### Math类

##### 常用方法

+ abs() 绝对值
+ max
+ min
+ ceil()  
+ floor()
+ pow(double a, double b)
+ double random()   0.0-1.0
+ double round() 四舍五入值

#### Arrarys类

##### 常用方法

+  sort()
+ binarySearch() 返回index  不存在返回  插入点减一

+ toString()   数组转为字符串

#### 超大整数 BigInteger类

##### 常用方法

+ BigInteger（String s）
+ add() 加   以下不是静态类
+ subtract()
+  mutiply() 乘积
+ divided()  出发

#### BigDecimal类（计算机表示浮点数 不精确   提供大型的浮点数据   和高精度浮点的额运算）

##### 常用方法

+ BigDecimal(String s)

  ~~~~~~java
  BigDecimal b1 = new BigDecimal("0.111")
  BigDecimal b2 = new BigDecimal("0.232")
  ~~~~~~

+ add    subtract   mutiply       加减乘  返回对象是BigDecimal数据类型的对象

+ divide  除法  (值， 舍入几位， 舍入模式看文档)

### 集合

![1560926392700](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1560926392700.png)



#### Collenction顶级集合接口  下面都是它的子接口  或者实现类

##### 常用方法

+ add()
+ get()
+ size()
+ boolean remove(object o) 删除第一个遇到的元素
+ clear()
+ toArray()   是把集合中的元素转成数组   
+ contains()

### Iterater类（屏蔽了 集合中间的不同）

#### 迭代器的使用

~~~~~~java
Collection<String> c = new ArrayList<String>();
c.add("dasd");
Iterator<String> it = c.Iterator();//返回当前集合的迭代器
while(it.hasNext()) {
    syso(it.next())
}
~~~~~~

#### 增强for循环（Iterable实现接口 ）

~~~~~~java
for(数据类型 变量名： 数组或者集合) {sop(变量) }
~~~~~~

+ 只能查看集合元素    没有索引  不能操作容器的元素

### 伪泛型（编译前   泛型到编译后的class文件时没有的）

+ 指定类型过后   类下面的E都是你指定的类型
+ 泛型定义方法   ArrayList<? extends Employee>    <? super Employee>  传入的参数必须是Employee的子类    后面时父类

### List 接口（有序，有索引，可以重复元素）

#### ArrayList(带有索引的方法  时它的特有方法)

+ add(index, element)
+ E remove(index) 删除并返回删除的元素
+ set(index, e ) 

#### 迭代器的并发修改异常（迭代的过程中  不准许调用方法修改集合的长度）

####  数据存储方式     栈堆   队列    数组（查询快）   链表（增删快）

#### LinkedList

##### 特有功能

+ addFirst()
+ addLast()
+ getFirst()
+ getLast()
+ isEmpty()  Collection顶层方法 
+ removeFirst(); //删除返回
+ removeLast();

### Set接口

#### HashSet

![1561013059396](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1561013059396.png)

#### LinkedHashSet（有序的set集合）

#### 基于链表的哈希实现     自身特性，具有顺序，存储和取出的顺序相同

####  泛型的方法



![1561021258081](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1561021258081.png)

### Map接口

#### HashMap

+ 返回被覆盖的值     put(<k>, <v>)
+ get(key) 获取对应的val   没有建  返回null
+ remove（Object key  ） 返回被移除的值
+ size() 长度

##### map集合的遍历

+ keySet()方法   返回存储建的set

~~~~~~java
Map<Integer, String> map = new HashMap<Integer, String>();
map.put(1, "张无忌");
map.put(2, "张三忌");
map.put(3, "磊哥");
for(Integer key : map.keySet()) {
    System.out.println(key+"->"+map.get(key));
}
~~~~~~

+ entrySet() 结果时一个set集合  里面装的时Entry类型的对象 （是Set的内部类   保存着映射关系）

~~~~~~java
Map<Integer, String> map = new HashMap<Integer, String>();
map.put(1, "你好啊");
map.put(2, "小丸子");
map.put(3, "小新");
Set<Map.Entry<Integer, String>> set = map.entrySet();
Iterator<Map.Entry<Integer, String>> it = set.iterator();
while(it.hasNext()) {
    //Map.Entry<Integer, String> entry = it.next();
    System.out.println(it.next().getValue());
}

Map<Integer, String> map = new HashMap<Integer, String>();
map.put(1, "你好啊");
map.put(2, "小丸子");
map.put(3, "小新");
for(Map.Entry<Integer, String> entry: map.entrySet()) {
    entry.getVlaue();
    entry.getKey();
}
~~~~~~

#### 两中遍历都要熟练

~~~~~~java
Map<Person, String> map = new HashMap<Person, String>();
map.put(new Person("haha", 1), "天津");
map.put(new Person("hehe", 3), "南京");
map.put(new Person("heihei", 5), "北京");
//遍历
//keySet()
//entrySet //内部类  结婚证
for(Person key: map.keySet()) {
    System.out.println(key +"..."+map.get(key));
}
for(Map.Entry<Person, String> entry: map.entrySet()) {
    System.out.println(entry.getValue()+"..."+entry.getKey());
}
~~~~~~

#### LinkedHashMap（有序的hashMap）

#### HashTable(线程安全  运行慢 被HashMap取代)

![1561087869394](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1561087869394.png)

#### 静态导入  目的是较少代码量

#### 函数可变参数

![1561100313843](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1561100313843.png)

~~~~~~java
public static int sum(int... a) {
		int sum = 0;
		for(int i:a) {
			sum +=i;
		}
		return sum;
	}
~~~~~~

#### 集合工具类  collections

##### 常用方法

+ Collections.sort()  针对list集合
+ shuffle()  把list打散随机排列
+ binarySearch()

#### 集合Map的嵌套

<center><h2>第四章</h2></center>

### 异常（Throwable -> Error     Throwable-> Exception）

#### 错误和异常的区别

+ 错误是程序运行时期出现的   必须要改代码了
+ 异常时编译，运行时期出现的问题   可以手动区处理

#### 异常的处理过程   Throwable-> Exception -> RunTimeException

+ 虚拟机创建一个异常对象
+ 将异常抛给调用者，调用者不处理 ，基础扔出去  知道扔到虚拟机
+ throw 方法内部抛出异常      throws  方法声明异常

![1561342179503](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1561342179503.png)

#### try...catch处理异常（try 检查和抛出异常    catch 捕获异常   catch可以连续写 

![1561342433407](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1561342433407.png)

+ 平级异常没有顺序关系    如果有继承关系的异常     子类异常应该先被抓取  切记

#### RunTimeException  

![1561344981589](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1561344981589.png)

#### 方法重写中的异常

![1561350298994](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1561350298994.png)

#### Throwable类的方法

+ getMessage()   对异常信息的详细描述
+ toString()  对异常信息的简短描述
+ printStackTrace()  将信息追踪到标准的错误流

#### 自定义异常

<center><h2>第四章</h2></center>

### io输入输出流

#### File类（将操作系统的文件，路径，目录（文件夹），封装成File对象）

##### 两个静态成员变量          

+ pathSeparator    是一个分号，目录 Linux : 号
+ separator  目录名称分隔符

##### 构造函数

+ File(String pathname)   文件夹名称不区分大小写  把路径变成file对象  不判断路径是否存在
+ File(String parent, String child) 
+ File(File parent, String child)

##### 一些常用的方法

+ createNewFile();

![1561360793891](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1561360793891.png)

+ mkdirs()     创建多层文件夹

~~~~~~java
File f  = new File("c:\\abc\\gg");
boolean b = f.mkdir();  //在c盘创建了zbc\gg这个文件夹
~~~~~~

+ delete()  删除成功true   用法同上
+ getName()  //获取最后的文件夹或者文件名称
+ getPath()  获取整个路径
+ length()   返回文件大小字节数
+ getAbsolutePath()  获取绝对路径    ==     File  getAbsoluteFile()   前者返回String     后者File对象
+ getParent()    getParentFile()    同上    推荐使用后者     盘符的父目录时null

![1561362432852](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1561362432852.png)

+ exists()   file构造函数中的路径是否正确
+ isDirectory() 判断是否是一个路径
+ isFile()  判断是否是一个文件
+ String[]     list()遍历了一个目录
+ File[]   listFiles() 遍历一个目录  listFiles(FileFilter filter)  参数是过滤器   具体用法如下

~~~~~~java
File file = new File("d:\\demo");
FileFilter filter = new MyFilter();// 建立一个实现类MyFilter来实现接口  并当参数传递
File[] files = file.listFiles(filter);
for(File f: files) {
    System.out.println(f);
}
~~~~~~

+ File.listRoots()  计算机中的所有根目录  // c:  d: 

##### 递归遍历文件中的文件

~~~~~~java
public static void main(String[] args) throws Exception {
    File file = new File("d:\\demo");
    getAll(file);
}
public static void getAll(File file) {
    File[] files = file.listFiles();
    for(File  f: files) {
        if(f.isDirectory()) {
            getAll(f);
        }else {
            System.out.println(f);
        }
    }
}
~~~~~~

### 输入 输出流

#### OutPutStream  所有字节输出流的超类 抽象

##### 常用方法

+ write(int b) 写入1个字节     write(byte[])    write(byte[], int start, int length)
+ close()  关闭流对象   释放与次流相关的资源

#####  FileOutPutStream

+ FileOutPutStream(String s)  FileOutPutStream(File f) 绑定一个数据目的 文件内容直接覆盖FileOutputStream(File file, boolean append)   //append为true的时候   会续写文件  不会覆盖文件

+ write  写入文件  换行+ \r\n

~~~~~~java
OutputStream ops = new FileOutputStream("c:\\a.txt");	
ops.write(96);
ops.write("hello".getBytes(), 1, 2);
ops.close();
~~~~~~

~~~~~~java
// 创建对象  写文件
FileOutputStream fps = null;

try {
    fps = new FileOutputStream("c:\\a.txt");

    fps.write(49);
}catch(IOException ox) {
    System.out.println(ox.getMessage());
    throw new RuntimeException("文件写入失败");
}finally {
    try{
        if(fps != null)
            fps.close();
    }catch(IOException ex) {
        ex.printStackTrace();
    }
}
~~~~~~

#### InputStream(怎么存的 就可以怎么读)

##### 常用方法（基本同上）

+  int  read()  执行一次 自动向后挪一个字节     到达数据的结尾读不到就是-1   int  read(char[] c)

  ![1561432587272](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1561432587272.png)

~~~~~~java
FileInputStream fis = new FileInputStream("c:\\a.txt");
int len = 0;
byte[] c = new byte[1024];
while((len = fis.read(c)) != -1) {
    System.out.print(new String(c, 0, len));
}
fis.close();
~~~~~~

##### 文件的复制

~~~~~~java
// 文件的赋值   先获取  存储
File file = new File("c:\\a.txt");
FileInputStream fis = new FileInputStream(file);
FileOutputStream fos = new FileOutputStream("d:\\"+file.getName());
int len = 0;
byte[] b = new byte[1024 * 10];
while ((len = fis.read(b)) != -1) {
    //向文件中写入   东西
    fos.write(b, 0, len);
}
~~~~~~

#### 编码表

![1561443609366](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1561443609366.png)

### 字符输入输出流

#### Writer输出流

#### 子类FileWriter

  #####  常用方法

+ write(int c) 写一个字符   write(char[] c) 写一个字符数组   write(char[] c, int ,len)    write(String s) 写指定的字符串

~~~~~~java
FileWriter fw = new FileWriter("c:\\a.txt");
//写一个字符
fw.write('c');
fw.flush();
//写一个字符数组
fw.write(new char[]{'q','w'});
fw.flush();
//写一个字符串
fw.write("23");
fw.flush(); //刷新缓冲区  将字符写入硬盘
fw.close();
~~~~~~

####  读文本文件   Reader

##### 常用方法

+ int read()读一个字符   读一个自读数组   int read(char[] c, int, length)

~~~~~~java
FileReader fr = new FileReader("c:\\a.txt");
//开始读了
int len = 0;
char[] c = new char[1024];
while((len = fr.read(c)) != -1) {
    syso(new String(c, 0, len))
}
~~~~~~

##### 只能复制文本文件  不然文件会损坏

~~~~~~java
public static void main(String[] args){
		FileReader fr = null;
		FileWriter fw = null;
		try {
			fr = new FileReader("c:\\a.txt");
			fw = new FileWriter("d:\\a.txt");
			
			// 一边读  一边写
			char[] c = new char[1024];
			int len = 0;
			while((len = fr.read(c)) != -1) {
				fw.write(c, 0, len);
				fw.flush();
			}
		} catch (IOException e) {
			e.printStackTrace();
			throw new RuntimeException("字符流创建失败");
		}finally {
			try {
				fw.close();
			}catch(IOException e){
				e.printStackTrace();
				throw new RuntimeException("关闭失败");
			}finally {
				try {
					fr.close();
				} catch(IOException e) {
					e.printStackTrace();
					throw new RuntimeException("关闭失败");
				}
			}
		}
	}
~~~~~~

### 转换流

#### OutputStreamWriter   字符流向字节

#### InputSteamReader    字节流向字符

![1561450367313](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1561450367313.png)

+ OutputStreamReader(OutputStream os)     
+ InputStreamWrite(inputStream  is)    InputStreamWrite(inputStream is, charset 编码表 ) 

~~~~~~java
//读的时候是字节转成字符
		FileInputStream fis = new FileInputStream("c:\\a.txt");
		InputStreamReader isr = new InputStreamReader(fis, "UTF-8");
		int len = 0;
		char[] c = new char[1024];
		while((len = isr.read(c)) != -1) {
			System.out.println(new String(c, 0, len));
		}
~~~~~~

### 缓冲流

#### BufferedOutputStream(OutputStream out)

~~~~~~java
BufferedOutputStream bot = new 
    BufferedOutputStream(new FileOutputStream("c:\\a.txt"));
//提高写的速度
~~~~~~



#### BufferedInputStream(InputStream in)

~~~~~~java
BufferedInputStream bis = new
    BufferedInputStream(new FileInputStream("数据源"))
    //提高写入的速度
~~~~~~

~~~~~~java
BufferedInputStream bis = new
BufferedInputStream(new FileInputStream("c:\\a.txt"));
InputStreamReader isr  = new InputStreamReader(bis, "UTF-8");
int len = 0;
char[] b = new char[1024];
while((len = isr.read(b)) != -1) {
    System.out.println(new String(b, 0, len));
}
~~~~~~

###  字符流缓冲区 

#### BufferedReader

##### 特有方法

+ String  readLine(0)     读没了  返回null  

#### BufferedWriter (继承了Writer)

##### 特有方法

+ void      newLine()    换行  具有跨平台性  

### 流总结

+ OutputStream 

  + FileOuputStream   
  + bufferedOutputSream

+ InputStream

  + FileInputStream
  + BufferedInputStream

+ Writer

  + OutputStreamWriter
    + FileWriter
  + BufferedWriter

+ Reader

  + InputStreamReader	
    + FileReader

  + BufferedReader

### Properties 类    持久存储集合     然后就是键值都是String

![1561518265875](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1561518265875.png)

#### 常用方法

+ setProperty()
+ getProperty()
+ Set<String>  stringPropertyNames()

+ load(InputStream in或者Reader r)
+ store(OutputStream out或者Wrtier r)

~~~~~~java
Properties p = new Properties();
p.load(new InputStreamReader(new FileInputStream("c:\\pro.properties"), "gbk"));
System.out.println(p);
p.setProperty("hello", "world");
p.setProperty("hehe", "haha");		
p.store(new FileWriter("c:\\pro.properties", true), "");
~~~~~~

### 对象的序列化和反序列化

#### ObjectInputStream, ObjectOutputStream的使用（简单的就是保存对象和取出对象）

+ ObjectInputStream（Outputstream out）
+ writeObject()
+ readObject()

~~~~~~java
ObjectOutputStream ops = new ObjectOutputStream(new 
FileOutputStream("d:\\a.txt"));
Person p = new Person("磊哥", 20);
//序列化保存到文件中  保存的对象类需要实现serilzieable接口 里面是空的
ops.writeObject(p);
ops.close();
//反序列化   把文件中保存的对象  取出来
ObjectInputStream ois = new ObjectInputStream(
    new FileInputStream("d:\\a.txt"));
Object o = ois.readObject();
ois.close();
System.out.println(o);
~~~~~~

+ 静态成员不能被序列化
+ 关键字transient阻止成员变量序列化
+ 没有方法的接口被称为标记型接口（cloneable接口'）

#### 序列化原理

![1561532889236](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1561532889236.png)

![1561533183318](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1561533183318.png)  

#### 自定义序列号static final long serialVersionUID = 321323L;  

### 打印流

#### 特点

+ 此流不负责数据源，主负责数据目的
+ 为其他输出流，提供功能
+ 不会抛出ioexception，可能抛出其他异常

#### PrintStream

+ 构造函数是指目的        PrintStream(File f)   PrintStream(String f)//文件路径     PrintStream(OutputStream out)

#### PrintWriter（常用    方法两个完全一致）

+ 构造函数是指目的        PrintWriter(File f)   PrintWriter(String s )   PrintWriter(OutputStream out )   PrintWriter(Writer w)

+ println()

#### 打印流开启自动刷新功能

+ 输出的数据目的必须是流对象
+ 调用 println    printf（） format

~~~~~~java
// 使用打印流  向文件中 打印数据
PrintWriter pw = new PrintWriter(
    new FileWriter("d:\\a.txt"), true);
pw.println("滚滚红尘");
pw.close();
~~~~~~

+ 实现文本的复制   BufferedReader + readLine() ------PrintWriter+println()

~~~~~~java
BufferedReader bdr = new BufferedReader(
new FileReader(new File("c:\\a.txt")));
PrintWriter pw = new PrintWriter(
new FileWriter(new File("d:\\a.txt")), true);//开启自动刷新
String s = "";
while((s = bdr.readLine()) != null) {
    pw.println(s);
}
bdr.close();
pw.close();
~~~~~~

### 工具类  common-io

#### FilenameUtils  静态

+ static        getExtension(String s);   获取文件类型
+ static        getName()  获取文件名

+ isExtension(String filename , String ext)   //判断后缀名

#### FileUtil

+ static String    readFileToString(File src) 读取文本返回字符串
+ static  writeStringToFile(file src, String s) 向文件中写入字符串

+ static copyFile(File src, File dest)  //复制文件
+ static copyDirectoryToDirectory() 复制文件夹

### 进程（在内存中运行的程序）

#### 线程(每个功能对于cpu的独立执行路径 就是线程)

##### 程序运行原理

+ 分时调度（平均分配cpu'）
+ 抢占式调度（按优先级）

##### 使用方法

+ 继承Thread类    重写run方法
+ 建立子类对象运行start方法    让线程程序执行  虚拟机调用子类重写的run方法     

+ getName() 获取线程的名称
+ Thread.currentThread()  返回正在执行的线程对象

+ setName()  设置线程的名字
+ Static   sleep(休眠时间);

##### 使用方法2

+ 实现Runale接口  重写抽象方法run
+ 创建Thread类对象   构造方法中可以传入Runable接口对象

##### 常见两个静态方法

+ currentThread
+ sleep()

##### 匿名内部类去实现多线程

~~~~~~java
//匿名内部类实现多线程程序 ’‘’
new Thread(){
    public void run() {
        System.out.println("111");
    }
}.start();
//接口实现
new Thread(new Runnable(){
    public void run() {
        System.out.println("222");
    }
}).start();
~~~~~~

##### 线程的状态

##### ![1561603372340](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1561603372340.png)

##### 线程池（缓冲池 ）     线程池方式  Runnable接口

+ 使用工厂类 Executors 的newFixedThreadPool()方法 创建一个线程池对象 ，这个对象是 ExecutorSercice(接口)的实现类对象
+ 使用submit(Runnable run)

##### Callable<T>

+ 实现Callable接口     
+ 重写call方法  得到返回值
+ 返回Future接口实现对象   调用get方法获取到返回值

### 多线程

+ 同步的关键子   synchronized(任意的对象) {    }   ()对象监视器
+ 同步锁的原理

![1561620253590](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1561620253590.png)

+ 方法的声明上写   public synchronized void get(){}   同步方法     使用的是this作为锁
+ 静态方法的 锁是本类自己.class属性

#### lock接口 实现类（使用类ReentrantLoack）

+ 在成员变量中声明锁 Lock l = new ReentrantLock();
+ 方法的开头   l.lock()    最后释放锁   l.unlock();

~~~~~~333###java
lock.lock();
if(tickets > 0) {
    try{
        Thread.sleep(5);
        System.out.println(Thread.currentThread().getName()+"--->"+ --tickets);
    }catch(Exception ex){

    }finally{
        lock.unlock();
    }	
}
~~~~~~

#### 线程的死锁

![1561625168346](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1561625168346.png)

#### 等待唤醒机制(wait( ), notify( ) )

### 数据库

####  java连接数据库的步骤

+   注册驱动
+ 连接数据库
+ 获取数据库执行者
+ 执行sql
+ 处理结果
+ 关闭数据库连接

~~~~~~java
//注册驱动
//使用Java.sql.DriverManager类中的方法 registerDriver()
Class.forName("com.mysql.jdbc.Driver");
//连接数据库
//url:  jdbc:mysql://localhost:3306/数据库的名字
String url = "jdbc:mysql://localhost:3306/leige";
String user = "root";
String pass = "123";
Connection con = DriverManager.getConnection(url, user, pass);
//获得数据库执行者
Statement st = con.createStatement();
//操作mysql
//使用执行者对象 发送sql给数据库update	
//处理结果
String sql = "insert into sort values(null, '磊哥牌软件', 3000000, '人的一生有很多痛苦，多注意健康，好好的生活')";
int count = st.executeUpdate(sql); //增删改
System.out.println(count);
//关闭数据库连接
st.close();
con.close();
~~~~~~

~~~~~~java
Class.forName("com.mysql.jdbc.Driver");	
String url = "jdbc:mysql://localhost:3306/leige";
String user = "root";
String pass = "123";
Connection con = DriverManager.getConnection(url, user, pass);
Statement st = con.createStatement();
String sql = "select * from sort";
ResultSet res = st.executeQuery(sql);
while(res.next()) {
    System.out.println(res.getString("sname")+res.getString("sprice")+res.getString("sdesc"));
}
res.close();
st.close();
con.close();
~~~~~~

#### 防止sql注入式攻击

~~~~~~java
Class.forName("com.mysql.jdbc.Driver");	
String url = "jdbc:mysql://localhost:3306/leige";
String user = "root";
String pass = "123";
Connection con = DriverManager.getConnection(url, user, pass);
String sql = "select * from user where uname=? and upwd=?";
PreparedStatement pst = con.prepareStatement(sql);
pst.setString(1, "3213");
pst.setString(2, "ewqe");
ResultSet res = pst.executeQuery();	
res.close();
pst.close();	
con.close();
~~~~~~

#### 封装数据库操作



~~~~~~java
Connection con = JDBCUtils.getCon();
System.out.println(con);
String sql = "update sort set sprice=? where sname=?";
PreparedStatement st = con.prepareStatement(sql);
st.setString(1, "12");
st.setString(2, "儿童玩具");
int res = st.executeUpdate();
System.out.println(res);
JDBCUtils.close(con, st);
~~~~~~

~~~~~~java
//封装类的代码
public class JDBCUtils {
	private JDBCUtils(){};
	private static String url;
	private static String user;
	private static String pwd;
	private static Connection con;
	
	static {
		try{
			Class.forName("com.mysql.jdbc.Driver");
		}catch(ClassNotFoundException ex){ex.printStackTrace();}
		url = "jdbc:mysql://localhost:3306/leige";
		user = "root";
		pwd = "123";
		try {
			con = DriverManager.getConnection(url, user, pwd);
		} catch (SQLException e) {
			e.printStackTrace();
		}
	}
	public static Connection getCon() {
		return con;
	}
	
	public static void close(Connection con, Statement st, ResultSet res) throws Exception{
		con.close();
		st.close();
		res.close();
	}
	public static void close(Connection con, Statement st) throws Exception{
		con.close();
		st.close();
	}
}
~~~~~~

#### 封装一个对象接受数据

~~~~~~java
Connection con = JDBCUtils.getCon();
String sql = "select * from sort";
PreparedStatement st = con.prepareStatement(sql);
ResultSet res = st.executeQuery();
List<Sort> list = new ArrayList<Sort>();
while(res.next()) {
    list.add(new Sort(res.getInt("sid"), res.getString("sname"), res.getString("sdesc"), res.getDouble("sprice")));
}
for(Sort l: list) {
    System.out.println(l);
}
JDBCUtils.close(con, st);
~~~~~~

#### 建立properties配置文件

##### 获取配置资源的路径 

~~~~~~java
Properties p = new Properties();
p.load(Test.class.getClassLoader().getResourceAsStream("jdbc.properties"));
System.out.println(p.getProperty("user"));
~~~~~~

### 数据库第三方包 DBUtils

#### 数据库中的事物

![1561969613332](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1561969613332.png)

#### QueryRunner

+ update(Connection con, String sql, Object...o) 
+ query(Connection con, String sql, ResultSetHandler, Object... o)

~~~~~~java
QueryRunner qr  = new QueryRunner();
String sql = "update student set name=?,sex=? where id=1";
Object[] obj = {"扫讨", "男"}; 
qr.update(con, sql, obj);
DbUtils.closeQuietly(con);
~~~~~~

#### ResultSetHandler

![1562032086833](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1562032086833.png)

+ ArrayHandler  将结果集的第一行存储到结果数组中

~~~~~~java
QueryRunner qr = new QueryRunner();
String sql  = "select * from student";
Object[] obj = qr.query(con, sql, new ArrayHandler());
~~~~~~

+ ArrayListHandler  将结果集中的每一条数据封装到数组中然后存到集合中

~~~~~~java
QueryRunner qr = new QueryRunner();
String sql  = "select * from student";
List<Object[]> list = qr.query(con, sql, new ArrayListHandler());
for(Object[] l: list) {
    for(Object o: l) {
        System.out.print(o);
    }
    System.out.println();
}
~~~~~~

+ BeanHandler 把结果集第一行封装成JavaBean类的对象

~~~~~~java
QueryRunner qr = new QueryRunner();
String sql  = "select * from student";
Student stu = qr.query(con, sql, new BeanHandler<Student>(Student.class));
System.out.println(stu.getId()+stu.getName()+stu.getSex()+stu.getScore());
~~~~~~

+ BeanListHandler  把结果集的每一条数据疯涨成javabean对象然后存到list集合中

~~~~~~java
QueryRunner qr = new QueryRunner();
String sql  = "select * from student";
List<Student> stu = qr.query(con, sql, new BeanListHandler<Student>(Student.class));
~~~~~~

+ ColumnListHandler 封装指定一列数据到list集合中

~~~~~~java
QueryRunner qr = new QueryRunner();
String sql  = "select * from student";
List<Object> cols = qr.query(con, sql, new ColumnListHandler<Object>("name"));
for(Object col: cols) {
    System.out.println(col);
}
~~~~~~

+ ScalarHandler   查询一个数据的时候使用   一般是集合函数的结果 

~~~~~~jav
QueryRunner qr = new QueryRunner();
String sql  = "select count(*) from student";
long count = qr.query(con, sql, new ScalarHandler<Long>());
System.out.println(count);
~~~~~~

+ MapHandler 封装第一条数据 到map<String, Object>中

~~~~~~java
QueryRunner qr = new QueryRunner();
String sql  = "select * from student";
Map<String, Object> res= qr.query(con, sql, new MapHandler());
for(String obj : res.keySet()) {
    System.out.println(obj+"-->"+res.get(obj));
}
~~~~~~

+ MapListHandler 封装每一条数据到Map中存到List集合里面

~~~~~~java
QueryRunner qr = new QueryRunner();
String sql  = "select * from student";
Map<String, Object> res= qr.query(con, sql, new MapListHandler());
~~~~~~



##### JavaBean类

+ private 成员变量    
+ 提供get set方法
+ 提供无参构造方法
+ 实现序列化接口  这个可以省略 不影响程序的运行

#### DbUtils 定义了 关闭资源和事物的处理方式

### 连接池

#### DBCP（mysql连接池）

##### BasicDataSource

+ 常见配置项

![1562036684855](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1562036684855.png)

~~~~~~java
// 使用datasource数据源  连接池俩操作数据库
BasicDataSource ds = new BasicDataSource();
//设置配置项
ds.setDriverClassName("com.mysql.jdbc.Driver");
ds.setUsername("root");
ds.setPassword("123");
ds.setUrl("jdbc:mysql://127.0.0.1:3306/leige");
ds.setInitialSize(10);
ds.setMaxIdle(2);
ds.setMaxIdle(5);
ds.setMaxActive(8);
ds.getConnection();
//ds可以封装成一个方法 
QueryRunner qr = new QueryRunner(ds);
String sql = "select * from student";
List<Object[]> lists =  qr.query(sql, new ArrayListHandler());
~~~~~~

#### C3P0(就业班学习   oracle接连池)

### 管家婆项目

![1562040650642](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1562040650642.png)

#### 运行sql建立数据库

#### 创建包 利用分层思想

![1562057446690](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1562057446690.png)

+ app包    存放main方法的类
+ domain包   // 存放javabean类
+ controller包     控制view层的显示  接收view层传来的数据
+ dao包   操作数据库
+ service包   //提供数据服务，接收controller控制层的数据
+ tools包   //写的工具类在里面
+ view包   //显示试图

#### 创建好每一层的类  并且写好  成员变量（用于层与层之间的沟通）(参考管家婆项目)（结束）

<center><h2>第五章</h2></center>

### 面向网络编程

#### TCP/IP协议 

![1562141106828](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1562141106828.png)

#### 互联网中的ip地址类（InetAddress）

##### 常用的方法 

+ static  InetAddress   getLocalHost()     //获取本机的ip对象
+ static InetAddress getByName("可以写ip也可也写计算机的名字")
+ String getHostName()  获取本机的名字
+ String getHostAddress()  获取ip地址

### UDP协议（面向无连接，不安全，最大传输限制在64kb）

![1562143828465](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1562143828465.png) 

#### 代码实现 UDP协议的发送端

##### 模拟发送

![1562146029003](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1562146029003.png)



##### 代码实现发送（DatagramPacket    DatagramSocket   来实现发送 ）

+  new DatagramPacket    (byte[], length, InetAddress, port) //指定地点实现发送
+ getLength 方法获取封装的数据包的长度
+ new  DatagramSocket   () 对象     发出去send

~~~~~~java
// 数据包   套接字 
byte[] b = "hello 我是 数据传递员".getBytes();
//封装好数据 包  指定地址 和端口号
DatagramPacket dg = new DatagramPacket(b, b.length, InetAddress.getByName("127.0.0.1"), 5000);
DatagramSocket ds = new DatagramSocket();
// 发送数据
ds.send(dg);
~~~~~~

+ 接受端要指定数组去接受

~~~~~~java
//定义接收端的 数据
byte[] b = new byte[1024];
DatagramPacket dg = new DatagramPacket(b, b.length);	
DatagramSocket ds = new DatagramSocket(5000);
ds.receive(dg);
System.out.println(new String(b, 0, dg.getLength())+".....>"+dg.getAddress().getHostAddress()+":"+dg.getPort());
~~~~~~

### TCP（面向有连接）（ServerSocket    socket）

![1562203539681](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1562203539681.png)

![1562205272033](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1562205272033.png)

#### Socket  客户端

~~~~~~java
Socket s = new Socket("127.0.0.1", 8888);//设置IP和端口号
InputStream in = s.getInputStream();
OutputStream out = s.getOutputStream();
byte[] b = "你好服务器".getBytes();
out.write(b);
s.close();
~~~~~~

#### ServerSocket  服务器端

~~~~~~java
ServerSocket ser = new ServerSocket(8888);
//获取客户端连接的套接字
Socket s = ser.accept();
InputStream in = s.getInputStream();
OutputStream out  = s.getOutputStream();
byte[] b = new byte[1024];
int len = in.read(b);
System.out.println(new String(b, 0, len));
s.close();
ser.close();
~~~~~~

#### 模仿上传功能（记住客户端上传完成要加上终止符）

~~~~~~java
//创建服务器
//服务器去读客户端写入的字节
ServerSocket ser = new ServerSocket(8000);
Socket s = ser.accept();
InputStream in = s.getInputStream();
//OutputStream out = s.getOutputStream();
FileOutputStream fs = new FileOutputStream("d:\\upload\\guanlan.jpg");
byte[] b = new byte[1024];
int len = 0; 
while((len= in.read(b)) != -1) {
    fs.write(b, 0, len);
}

//回复 客户端下载完成

OutputStream out = s.getOutputStream();
out.write("下载成功".getBytes());
fs.close();
s.close();
ser.close();
~~~~~~

~~~~~~java
//创建客户端
//把读的数据变成字节数组   然后写入到服务器
Socket s = new Socket("127.0.0.1", 8000);
InputStream in = s.getInputStream();
OutputStream out = s.getOutputStream();

InputStream i = new FileInputStream("c:\\haha.jpg");
byte[] b = new byte[1024*6];
int len = 0;
while((len = i.read(b)) != -1) {
    out.write(b, 0, len);
}
//写完之后  要设置结束标志 
b = new byte[1024];
s.shutdownOutput();
len = in.read(b);
System.out.println(new String(b, 0, len));
i.close();
s.close();
~~~~~~

#### 多线程上传

+ 多线程思想是  把每个上传的功能封装到 run方法中    每次有客户端连接就开线程去执行 run中的下载方法

~~~~~~java
public class Upload implements Runnable{
	private Socket s;
	public Upload(Socket s) {
		this.s = s;
	}
	public void run() {
		try{
			//创建服务器
			//服务器去读客户端写入的字节
			InputStream in = s.getInputStream();
			//OutputStream out = s.getOutputStream();
			File f = new File("d:\\upload");
			if(!f.exists()) {
				f.mkdirs();
			}
			String filename = "leige" + System.currentTimeMillis()+new Random().nextInt(999999)+"jpg";
			FileOutputStream fs = new FileOutputStream(f + File.separator + filename);
			byte[] b = new byte[1024];
			int len = 0; 
			while((len= in.read(b)) != -1) {
				fs.write(b, 0, len);
			}
			
			//回复 客户端下载完成
			
			OutputStream out = s.getOutputStream();
			out.write("下载成功".getBytes());
			fs.close();
			s.close();
		}catch(IOException ex) {
			new RuntimeException("上传中发生未知故障");
		}
	}
}
~~~~~~



<center><h2>第六章</h2></center> 

### java中的反射机制

#### 类的加载 （加载  连接    初始化）

![1562229071829](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1562229071829.png)

![1562229021487](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1562229021487.png)

#### 类的初始化时机

![1562229634081](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1562229634081.png)

#### 类的加载机制

![1562229891875](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1562229891875.png)

#### 类的加载器组成

![1562229939341](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1562229939341.png)

### 反射

#### 获取class对象的三种方式

+ 对象获取

~~~~~~java
Person s = new person()
Class c = s.getClass()
~~~~~~

+ 类名获取

~~~~~~java
Person.class //利用属性获取
~~~~~~

+ Class静态方法获取

~~~~~~java
Class.forName("//类的完整名字");
~~~~~~

#### 解剖class文件 获取里面的构造方法   成员变量   成员方法

##### 获取空参构造器   并且运行

~~~~~~java
Class c = Class.forName("cn.leige.demo13.Student");	
Constructor cst = c.getConstructor();
Object o = cst.newInstance();
~~~~~~

##### 获取非空参构造器，new对象

~~~~~~java
Class c = Class.forName("cn.leige.demo13.Student");	
Constructor<Student> cst = c.getConstructor(String.class, int.class, String.class);
System.out.println(cst);
Student o = cst.newInstance("磊哥", 23, "清华大学实验班");		
System.out.println(o);
~~~~~~

##### 反射获取构造方法并运行的快速方式

+ 有空参构造器    权限是public（必须）

  ~~~~~~java
  Class c = Class.forName("cn.leige.demo13.Student");	
  Object 0 = c.newInstance();
  ~~~~~~

##### 暴力解剖私有构造函数 (Constructor, filed, Method 的父类AccessibleObject 可以解除权限限制)

~~~~~~java
Class c = Class.forName("cn.leige.demo13.Student");
//获取私有的构造函数
Constructor cst = c.getDeclaredConstructor(int.class, String.class);
cst.setAccessible(true);
cst.newInstance(12, "leieg");
~~~~~~

##### 获取成员变量

~~~~~~java
// 把class文件加入内存   返回class文件对象
Class c = Class.forName("cn.leige.demo13.Student");
Constructor cst = c.getConstructor(String.class, int.class, String.class);
Object o = cst.newInstance("磊哥", 28, "最牛逼班");
//获取私有的构造函数
Field f = c.getField("name");
System.out.println(f.get(o));
~~~~~~

##### 获取成员的变量并且修改值

~~~~~~java
Class c = Class.forName("cn.leige.demo13.Student");
Constructor cst = c.getConstructor(String.class, int.class, String.class);
Object o = cst.newInstance("磊哥", 28, "最牛逼班");
//获取私有的构造函数
Field f = c.getField("name");
f.set(o, "剑哥");
System.out.println(f.get(o));
~~~~~~

##### 获取空参书的成员方法

~~~~~~java
// 把class文件加入内存   返回class文件对象
Class c = Class.forName("cn.leige.demo13.Student");
Constructor cst = c.getConstructor(String.class, int.class, String.class);
Object o = cst.newInstance("磊哥", 28, "最牛逼班");
//获取私有的构造函数
Method m = c.getMethod("haha");
m.invoke(o);
~~~~~~

##### 获取有参数的成员方法运行

~~~~~~java
// 把class文件加入内存   返回class文件对象
Class c = Class.forName("cn.leige.demo13.Student");
Constructor cst = c.getConstructor(String.class, int.class, String.class);
Object o = cst.newInstance("磊哥", 28, "最牛逼班");
//获取私有的构造函数
Method m = c.getMethod("setAge", int.class);
m.invoke(o, 12);
System.out.println(o);
~~~~~~

##### 利用反射的泛型擦除

~~~~~~java
List<String> list = new ArrayList<String>();
Class c = list.getClass();
Method m = c.getMethod("add", int.class);
m.invoke(list, 12);
~~~~~~

##### 利用配置文件运行类和方法

~~~~~~java
InputStream in = Class.forName("cn.leige.demo14.Test").
getClassLoader().getResourceAsStream("mothod.properties");
Reader r = new InputStreamReader(in);
Properties p = new Properties();
p.load(r);
String classname = p.getProperty("classname");
String method = p.getProperty("method");
System.out.println(classname);
Class c = Class.forName(classname);
Method m = c.getMethod(method);
Constructor cst = c.getConstructor();
Object o = cst.newInstance();
m.invoke(o);
~~~~~~

