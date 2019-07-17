<center><h1>java结合web进阶</h1><center>

### 回顾数据库相关知识

#### sql语句的分类

+ ddl 定义数据库对象   结构有关系 create  table
+ dml  数据操作语言  进行更新数据表  update  delete   insert
+ dql   用来查询数据表结构
+ dcl 数据控制语言   创建用户    定义数据库访问权限

### 常用的命令

#### 对数据库的操作

+ create  database  xxx character set gbk  //创建带编码的数据库
+ show databases 查看数据库
+ show create database xxxx   查看数据库的结构编码
+ dop database xxx   删除数据裤
+ use xxx  选择选用哪个数据库
+ select  database();   //查看当前使用的数据库

#### 对表的操作

+ create table xxx  //创建数据表  
+ xxxx  类型  【约束】  对每个字段的定义
+ show  tables// 查看所有表
+ show create table   xxxx;   //详细查看   包括表的字符集
+ desc  xxxx 查看表的结构
+ drop   table xxxx  删除一个表
+ alter table   xxxx add   字段   类型  【约束】  添加一列
+ alter table xxx  modify   字段   类型（长度） 【约束】   修改一列
+ alter table xxx  change    old（列名）   new （新列名）   类型（长度） 【约束】   修改一列

+ alter table   xxxx drop 列名;   //删除一列
+ rename table   xxxx  to   newtablename;   //修改表的名字
+ alter table xxx    character  set    utf8;   //设置表的字符集

#### 字段的类型

+ int类型
+ double(m, d)
+ decimal(m, d) //用于表示钱数的时候
+ datatime
+ timestamp
+ varchar

#### 对表记录的操作

+ insert into xxxx  values()
+ update xxxx  set  xxx=xx  where...
+ delete from  xxxx  where  ....    truncate  (删除整个表   然后创建一个一样的表  和事务配合无法找回)

#### 事务（tansaction 关键字）

+ start     transaction  
+ rollback

#### 数据库操作 回顾

~~~~~~java
//注册驱动
Class.forName("com.mysql.jdbc.Driver");
//获得连接
Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/leige", "root", "123");
//写sql语句
String sql = "select * from user where uname=? and upwd=?";
//获得执行对象  预编译
PreparedStatement pst = con.prepareStatement(sql);
//设置占位符参数
pst.setString(1, username);
pst.setString(2, password);
//执行语句
ResultSet res = pst.executeQuery();
//处理结果
if(res.next()) {
    System.out.println("登陆成功");
}else {
    System.out.println("登陆失败");
}
//关闭资源
if(res != null)res.close();
if(pst != null)pst.close();
if(con != null)con.close();
~~~~~~

#### limit关键字的扩展

+ limit（2起始位置， 2每页的条数）// 其实位置=（当前页数-1）*每页的条数

#### 多表查询

##### 外键约束

+ alter table 从表  add [constraint] [外键名称] foreign key（从表的外键字段名称） references 主表(主表的主键)
+ alter table 从表 drop foreign key  外键名称（就是上面建立外键的那个名称   _fk结尾）

##### 多对多的建表图

![1562555395768](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1562555395768.png)

##### 一对一关系的建表图

![1562555707384](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1562555707384.png)

##### 一对多的关系（这个很熟悉）

##### 多表查询

+ select * from A,B where  //隐式内连接     （select * from A inner join B on 条件）inner可以省略
+ select * from A left join B  on  条件         //把左边的数据全部选出来
+ select * from A right join B  on  条件      //把右边的数据全部选出来
+ select  * from A where  A.id=(select id from B where name="xxx")  //子查询

+ where   xxx not in(a,b,c)  作为条件使用 列字段不再in的范围内
+ where   xxx is not null   查出此字段不为空的数据
+ SELECT * FROM emp ORDER BY sal DESC, hiredate ASC //先工资降序   如果工资一样的按日期升序


#### 约束

+ primary key
+ not null
+ unique
+ foreign key

#### 级联操作

+ alter  table xxx add  constaint xxx_fk  foreign key  xxx   references xxx(xxx)  on update cascade

##### 级联更新

+  on update cascade

##### 级联删除

+  on delete cascade

#### 多表的关系

#### 数据库设计的范式

+ 第一范式（1fn）  每个数据都是不可分割的原子数据
+ 第二范式（2FN） 减少部分依赖
+ 第三范式（3FN） 减少传递依赖

#### 数据库的备份和还原

+ mysqldump -u root -p xxx  数据库名称 >保存路径
+ source 执行的sql路径

#### 事务的操作

+ 开启事务  start    transaction 
+ 回滚 rollback
+ 提交事务     commit

##### mysql dml会自动提交一次事务 （orcle不是自动提交）

##### 开启事务就需要手动提交一下

##### 查看事务的默认提交方式

+ select @@autocommit   0--手动提交    1---自动提交
+ set @@autocommit = 0 手动设置提交方式

##### 事务的四大特征

+ 原子性  不可分割的最小操作单位
+ 持久性  事务一旦提交或者回滚，数据库会持久化的保存数据
+ 隔离性   多个事务之间。相互独立
+ 一致性   事务操作前后数据的总量不变

##### 事务的隔离级别

[连接 ](<https://jingyan.baidu.com/article/f25ef254891845482c1b8215.html>)

#### dcl(use mysql)

##### 管理用户

+ 添加用户     create user  '用户名'@'主机名' identified by '密码'
+ 删除用户     drop  user  '用户名'@'主机名'
+ 修改密码     set  password for '用户名'@'主机名' = password('123')

##### 忘记mysql 密码

![1562666199616](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1562666199616.png)

##### 权限管理

- 查询权限 show  grants for '用户名'@'主机名’
- 授予权限  grant  权限(select)  on 数据库名称.表名  to  '用户名'@'主机名'        //grant all on *.* to ...   设置全部的权限
- 撤销权限   revoke  权限  on 数据库.表   from   '用户名'@‘主机名

### JDBC连接池

#### 自定义连接池（自定义连接池类   实现DataSource中的getConnection()方法）

#### 增强Connection实现类中close方法 （正常情况下继承加重写）

+ 定义第三个类 实现Connection
+ 在构造函数中  把之前Connection实现类  new一个对象 存到成员变量中
+ 然后写方法

+ ~~~~~~java
  public class MyConnection implements Connection{
  	private Connection conn = null;
  	private LinkedList<Connection> pool;
  	public MyConnection(Connection conn) {
  		this.conn = conn;
  	}
  	
  	public void setCons(LinkedList<Connection> cons) {
  		this.pool = cons;
  	}
  	@Override
  	public void close() throws SQLException {
  		pool.add(conn);
  	}
  ~~~~~~

#### c3p0连接池

+ 在src目录下  创建c3p0-config.xml 文件

~~~~~~xml
<?xml version="1.0" encoding="UTF-8"?>
<c3p0-config>
  <default-config>
    <property name="driverClass">com.mysql.jdbc.Driver</property>
	<property name="jdbcUrl">jdbc:mysql:///web_07</property>
	<property name="user">root</property>
	<property name="password">123</property>
	<property name="initialPoolSize">5</property>
	<property name="maxPoolSize">20</property>
  </default-config>
  
  <named-config name="oracle"> 
    <property name="driverClass">com.mysql.jdbc.Driver</property>
	<property name="jdbcUrl">jdbc:mysql:///web_07</property>
	<property name="user">root</property>
	<property name="password">123</property>
  </named-config>
</c3p0-config>
~~~~~~

+ 默认连接是上面   下面是自定义连接

~~~~~~java
Connection conn = null;
PreparedStatement pst = null;
ComboPooledDataSource mds = null;
try{
    mds = new ComboPooledDataSource("leige");
    conn = mds.getConnection();
    String sql = "insert into user values(null,?,?)";
    pst = conn.prepareStatement(sql);
    pst.setString(1, "杨过");
    pst.setInt(2, 1122);
    int rows = pst.executeUpdate();
}catch(Exception e) {
    e.printStackTrace();
    throw new RuntimeException("ss");
}finally{
    mds.close();
}
~~~~~~

#### dpcp连接池

+ 在classpath目录写下 dbcp.properties

~~~~~~text
driverClass=com.mysql.jdbc.Driver
username=root
url=jdbc:mysql://localhost:3306/leige
password=123
~~~~~~

+ 接下来获取DataSource  即可

~~~~~java
public class DBCPUtils {
	//获取 数据源    获取连接对象Connection 为什么要是静态的呢   因为获取一个数据源就够了】
	private static  DataSource ds;
	static {
		InputStream in = DBCPUtils.class.getClassLoader().getResourceAsStream("jdbc.properties");
		
		Properties pro = new Properties();
		try {
			pro.load(in);
			ds = BasicDataSourceFactory.createDataSource(pro);
		} catch (Exception e) {
			e.printStackTrace();
		}	
	}
	public static DataSource getDs() {
		return ds;
	}
	
	public static Connection getCon() throws SQLException {
		return ds.getConnection();
	}
}
~~~~~

~~~~~~java
public void test() throws Exception{
    Connection con = DBCPUtils.getCon();
    String sql = "update user set upwd=? where uname=?";
    PreparedStatement pst = con.prepareStatement(sql);
    pst.setString(1, "112233");
    pst.setString(2, "杨过");
    pst.executeUpdate();
}
~~~~~~

#### 连接池结合dputils

~~~~~~java
DataSource ds = null;
QueryRunner qr = null;
String sql = "select * from user";
try {
    ds = DBCPUtils.getDs();
    qr = new QueryRunner(ds);
    List<User> users= qr.query(sql, new BeanListHandler<User>(User.class));
    System.out.println(users.get(1));
} catch (SQLException e) {
    // TODO Auto-generated catch block
    e.printStackTrace();
}
~~~~~~

### xml和反射

#### xml语法

+ 属性  version 1.0   encoding utf-8

~~~~~~text
<?xml version="1.0" encoding="UTF-8"?>//头部可以省略
~~~~~~

+ CDATA区可以写任意内容    <![CDATA[  ]]>

 #### DTD约束（后缀名 dtd）

![1562828492836](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1562828492836.png)



#### schema约束（xst 后缀名）

##### 命名空间

~~~~~~java
<web-app xmlns="http://www.example.org/web-app_2_5" //引入自定义命名空间
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"   //引入w3c实例
        xsi:schemaLocation="http://www.example.org/web-app_2_5 web-app_2_5.xsd"  //引用路径 加上空间的名字
            version="2.5">
~~~~~~

##### 解析xml文件（使用 dom4j）

+ 引入jar包 （dom4j-1.6.1.jar）
+ 下面是案例

~~~~~~java
//获取文档的解析器
SAXReader sr = new SAXReader();
//获取document文档对象
Document doc = sr.read("src/cn/leige/xml/web.xml");
//获取根元素
Element root = doc.getRootElement();
//然后遍历去获取各个元素
List<Element> els = root.elements();
for(Element el: els) {
    if("servlet".equals(el.getName())) {
        //el.elementText("servlet-name");
        System.out.println(el.element("servlet-name").getText());
    }
}
~~~~~~

##### xpath解析xml文件

+ selectNodes("xpath表达式")     //获取多个节点
+ selectSingleNode("xpath表达式")   //获取一个节点
+ 表达式：//root//....       //root[last || 1]  找最后一个或者第一个

~~~~~~java
SAXReader sax = new SAXReader();
Document doc = sax.read("leige01\\xml\\student.xml");
Element name = (Element) doc.selectSingleNode("//name[@id='itcast2']"); //使用属性值查找
System.out.println(name.getText());
~~~~~~

### idea的基本使用

#### 目录结构

+ project(项目) -> module (模块)-> package(包)

#### 常用的快捷键

+ alt+enter   自动导包  代码补全
+ ctrl+y  删除光标所在的行
+ ctrl+d   复制一行
+ ctrl+shift+l  格式化代码
+ ctrl+/  单行注释
+ ctrl+shift+/  多行注释
+ ctrl+shift+上线键      移动代码行
+ alt+4 关闭控制台
### http请求
#### get请求

+ 请求行（GET /http://地址?user=&password HTTP1.1）
+ 请求头（k: v）(一键多值)  指导性信息（指导服务器的）

#### post请求

+ 请求行（GET /http://地址?user=&password HTTP1.1）
+ 请求头（k: v）(一键多值)  指导性信息（指导服务器的）
+ 请求体   username=?&haha=ll

### HTTP的响应

+ 响应行  HTTP1.1 200(状态码)
+ 响应头 指导性信息   知道浏览器
+ 响应体

#### 响应状态码

+ 200 响应成功
+ 302 浏览器重定向
+ 304 查找本地缓存
+ 404 找不到资源
+ 500 服务器错误

### tomcat服务器

+ bin目录  服务器软件目录
+ conf 软件配置
+ lib 第三方的jar包
+ logs 日志文件
+ temp 临时目录
+ webapps 开发号的web项目，放在这里
+ work jsp文件的存储位置

#### idea绑定tomcat服务器

+ run -->edit configuration --> 点击加号 --> tomcat server （选择local本地）
+ 随便起个名字 --> 导入tomcat安装目录 --> vm option ：-Xms128m -Xmx256m -XX:PermSize=128m -XX:MaxPermSize=256m --> 其他默认配置  下面是vm参数解释
+ **-vmargs** **说明后面是****VM****的参数，所以后面的其实都是****JVM****的参数了**
  **-Xms128m JVM****初始分配的堆内存**
  **-Xmx512m JVM****最大允许分配的堆内存，按需分配**
  **-XX:PermSize=64M JVM****初始分配的非堆内存**
  **-XX:MaxPermSize=128M JVM****最大允许分配的非堆内存，按需分配**

#### idea创建web项目

+ file --> new --> module --> java Enterpirse 

![1563355132333](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1563355132333.png)

![1563355155759](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1563355155759.png)

#### idea web项目目录结构

![1563352063364](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1563352063364.png)

#### web项目发布到tomcat

+ 修改发布文件的路径
+ 发布这个模块
+ 修改更新

![1563355499329](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1563355499329.png)

![1563355659382](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1563355659382.png)

![1563355953920](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1563355953920.png)

![1563355986323](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1563355986323.png)

![1563356102137](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1563356102137.png)

#### 项目编译的原理

![1563357327625](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1563357327625.png)

### servlet （java13规范之一）
+ 请求行（GET /http://地址?user=&password HTTP1.1）
+ 请求头（k: v）(一键多值)  指导性信息（指导服务器的）

#### post请求

+ 请求行（GET /http://地址?user=&password HTTP1.1）
+ 请求头（k: v）(一键多值)  指导性信息（指导服务器的）
+ 请求体   username=?&haha=ll

### HTTP的响应

+ 响应行  HTTP1.1 200(状态码)
+ 响应头 指导性信息   知道浏览器
+ 响应体

#### 响应状态码

+ 200 响应成功
+ 302 浏览器重定向
+ 304 查找本地缓存
+ 404 找不到资源
+ 500 服务器错误

### tomcat服务器

+ bin目录  服务器软件目录
+ conf 软件配置
+ lib 第三方的jar包
+ logs 日志文件
+ temp 临时目录
+ webapps 开发号的web项目，放在这里
+ work jsp文件的存储位置

#### idea绑定tomcat服务器

+ run -->edit configuration --> 点击加号 --> tomcat server （选择local本地）
+ 随便起个名字 --> 导入tomcat安装目录 --> vm option ：-Xms128m -Xmx256m -XX:PermSize=128m -XX:MaxPermSize=256m --> 其他默认配置  下面是vm参数解释
+ **-vmargs** **说明后面是****VM****的参数，所以后面的其实都是****JVM****的参数了**
  **-Xms128m JVM****初始分配的堆内存**
  **-Xmx512m JVM****最大允许分配的堆内存，按需分配**
  **-XX:PermSize=64M JVM****初始分配的非堆内存**
  **-XX:MaxPermSize=128M JVM****最大允许分配的非堆内存，按需分配**

#### idea创建web项目

+ file --> new --> module --> java Enterpirse 

![1563355132333](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1563355132333.png)

![1563355155759](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1563355155759.png)

#### idea web项目目录结构

![1563352063364](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1563352063364.png)

#### web项目发布到tomcat

+ 修改发布文件的路径
+ 发布这个模块
+ 修改更新

![1563355499329](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1563355499329.png)

![1563355659382](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1563355659382.png)

![1563355953920](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1563355953920.png)

![1563355986323](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1563355986323.png)

![1563356102137](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1563356102137.png)

![1563357327625](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1563357327625.png)