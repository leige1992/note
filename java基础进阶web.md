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

### servlet 快速入门

#### 实现步骤

+ 创建实现类去实现tomcat提供的Servlet接口

~~~~~~java
public class QuikStartServlet implements Servlet {
    @Override
    public void service(ServletRequest req, ServletResponse res) throws 					ServletException, IOException {
        res.getWriter().print("dassada");
    }
~~~~~~



+ 配置xml文件（通知tomcat去执行这个实现类）

~~~~~~xml
<servlet>
    <servlet-name>haha</servlet-name>
    <servlet-class>com.leige.lianxi.QuikStartServlet</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>haha</servlet-name>
    <url-pattern>/first</url-pattern>
</servlet-mapping>
~~~~~~

#### 自动代码补全设置

![1563411883252](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1563411883252.png)

#### 什么是servlet

运行在服务器端的java小程序，是sun公司提供给的一套规范，处理客户端请求，响应数据

#### 执行原理

![1563418008028](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1563418008028.png)

+ 启动tomcat，扫描webapps目录， 读取项目中的web.xml文件
+ 接受客户端请求
+ 创建 request， response对象
+ 去xml文件中匹配虚拟路径 去找执行的类
+ 调用servlset实现类类 使用反射技术去创建对象  调对象中的service方法传入参数 request和response 
+ 数据写在response的缓冲区中
+ service结束response取出缓冲区数据，组装http的响应信息，回传浏览器

#### servlet生命周期（init service  destroy）

+ tomcat文件夹下conf --> context  下面可以修改tomcat监视器  可以自动监视web.xml的修改  

+ init() 创建servlet对象时候调用 只调用一次

~~~~~~java
//配置tomcat启动时创建servlet对象
<servlet>
    <servlet-name>quik</servlet-name>
    <servlet-class>com.leige.lianxi.QuikStartServlet</servlet-class>
    <load-on-startup>2（写任意的整数，代表优先级，数字越小优先级越高）</load-on-startup>
</servlet>
~~~~~~

+ service()  客户端访问一次  执行一次
+ destory()  停止tomcat服务器      移除项目

#### web.xml配置的详解

+ url-pattern匹配方式
  + 完全匹配 /ab
  + 目录匹配 /ad/da/*
  + 完全匹配  *.abc

#### 全局的web.xml  conf --> web.xml

+ 一些常用的配置

~~~~~~~xml
//设置session的超时时间 单位是分钟
<session-config>
	<session-timeout>30</session-timeout>
</session-config>
~~~~~~~

#### 继承HtttServlet的原理

+ 继承可HttpServlet, 这个类的父类 实现了servlet接口
+ Tomcat服务器的调用这个类的service方法因为本类没有所以调用的是父类HttpServlet中service方法
+ 然后父类里面使用this，这时候的this指的是继承的子类对象调用doPost，doGet（屏蔽了程序员来判断get还是post）

~~~~~~java
public class RunSerlet extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.getWriter().print(2312123);
    }

    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doGet(request, response);
    }
}
~~~~~~

#### 修改servlet模板

+ file --> settings --> editor --> file and code template 
+ 右边的菜单栏有  file  includes code other   选择other
+ web --> java code template --> servlet class.java  修改保存即可

#### ServletConfig对象

##### 获取这个对象（有几个servlet就有几个这个对象）

+ 父类的父类中有个方法  getServletConfig() 子类直接使用即可

##### 如何使用

+ 获取servlet的名字   config.getServletName()
+ 获取初始化参数值     config.getInitParameter("键值")

~~~~~~xml
//在servlet里面配置
<init-param>
  <param-name>leige</param-name>  //键
  <param-value>111</param-value>  //值
</init-param>
~~~~~~

+ 获取servlet上下文对象   getServletContext()

~~~~~~java
public class ConfigServlet extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //获取servlet配置对象
        ServletConfig config = getServletConfig();
        //获取servlet名称
        String name = config.getServletName();
        //获取上下文
        config.getServletContext();
        //获取初始化参数
        String leige = config.getInitParameter("leige");
        response.getWriter().print(name+leige);
    }

    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doGet(request, response);
    }
}

~~~~~~

#### servlet 通信总结

+ 新建servlet
+ 在web.xml里面配置 信息（一个是servlet一个是servlet-mapping）

~~~~~~java
public class UerLogin extends HttpServlet {

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        String username = request.getParameter("username");
        String pwd = request.getParameter("pwd");
        if(username ==null || pwd == null) {
            response.getWriter().print("error");
        }else {
            QueryRunner qr = new QueryRunner(C3P0Utils.getDs());
            String sql = "select * from user where username=? and pwd=?";
            try {
                User u = qr.query(sql, new BeanHandler<User>(User.class), new Object[]{username, pwd});
                if(u != null) {
                    response.getWriter().print("succ");
                }else {
                    response.getWriter().print("error");
                }
            }catch (Exception e){e.printStackTrace();}finally {

            }
        }
    }

    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doGet(request, response);
    }
}
~~~~~~

### response

#### ServletContext对象（对应一个web应用程序 一个应用只有一个）一个接口 tomcat实现

##### 是什么

+ 是一个web模块应用程序的上下文对象

##### 怎么获取

+ 上节提到的先获取   getServletConfig().getServletContext()  
+ 父类中已经封装好了一个方法直接获取     getServletContext();

##### 有什么用

+ 获取模块的初始化参数

~~~~~~xml
<context-param>
    <param-name>leige</param-name>
    <param-value>23</param-value>
</context-param>
~~~~~~

~~~~~~java
//获取这个对象   获取初始化参数
ServletContext sc = getServletContext();
System.out.println(sc.getInitParameter("leige"));
~~~~~~

+ 获取绝对路径   getRealPath("里面写资源相对路径")

~~~~~~java
ServletContext sc = getServletContext();
String apath = sc.getRealPath("WEN-INF/web.xml");
System.out.println(apath);
~~~~~~

##### 域对象（所谓的域对象，说明这个对象是个容器，作用域是整个web应用程序）

+ setAttribute(String s, Object o)
+ getAttribute(String s);
+ removeAttribute(String s)

~~~~~~java
//在其他servlet都可以用  作用域是整个项目
ServletContext sc = getServletContext();
sc.setAttribute("haha", 111);
~~~~~~

##### 统计访问次数

+ ServletContext存储次数    每次访问++

##### ServletContext空指针异常

+ 父类中写的init（ServletConfig config）对ServletContext赋值 并调用了this.init()空参方法
+ 如果子类继承使用 init（ServletConfig config）会覆盖父类的方法   造成赋值失败   造成空指针
+ 如果想写  init方法  请写空参构造

##### servlet注解开发

~~~~~~java
@WebServlet(urlPatterns = "/count")
public class CountServlet extends HttpServlet {

~~~~~~

#### response对象详解

+ 负责历览器的响应   ServletResponse接口   ， 由HttpServletResponse继承
+ 此接口对象是tomcat引擎来实现   调用由引擎传参

##### 响应行

+ 设置状态码     setStatus(int 状态码)

##### 响应头

+ addHeader(String key, String val)
+ addIntHeader(String key, intval)
+ addDateHeader(String key, longval)
+ ***setHeader*()   这个比较重要**     //response.addHeader("leige", "23");
+ setIntHeader()
+ setDateHeader()

##### 响应体

+ getWriter()    //打印流   PrintWriter  只能做文本数据响应

+ getOutputStream()    //获取字节输出流

+ 解决中文乱码问题

  + 问题原因是编码和解码不一样     默认是拉丁文编码     gbk解码

  + 响应的数据没有直接回到客户端    写在response对象的缓冲区使用拉丁文编码    

  + 设置缓冲区编码  response.setCharacterEncoding();

  + ```
    response.setContentType("text/html;charset=utf-8"); //一句话就可以告诉浏览器怎么解码
    ```

+ 字节流响应非文本数据给浏览器

~~~~~~java
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    //web根目录由一个a.jpg图片
    String apath = getServletContext().getRealPath("a.jpg");
    FileInputStream in = new FileInputStream(apath);
    OutputStream out = response.getOutputStream();
    byte[] bt = new byte[1024 * 2];
    int len = 0;
    while((len = in.read(bt)) != -1) {
        out.write(bt, 0, len);
    }
    in.close();
}
~~~~~~

##### 重定向

![1563504828661](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1563504828661.png)

+ 可以设置状态码    重定向地址（response.setStatus(302)   response.setHeader("location", "地址")）
+ sun公司很人性化   提供了重定向的方法     

~~~~~~java
response.sendRedirect("/WEB03/redirect");  //设置重定向到。。。。
~~~~~~

##### 注意事项

+ 重定向过后不要再写代码
+ 写两个重定向
+ 两个流  有冲突   只能定义一个  因为缓冲区不能又是字节又是字符

##### 文件的下载

~~~~~~java
response.setHeader("Content-Disposition", "attachment;fileName="+"a.pdf");   //通知浏览器下载文件，而不是打开这个文件
~~~~~~

+ 控制下载文件的文件名称

~~~~~~java
String agent = request.getHeader("User-Agent");
String filename="美女.jpg";
if (agent.contains("MSIE")) {
    // IE浏览器
    filename = URLEncoder.encode(filename, "utf-8");
    filename = filename.replace("+", " ");
} else if (agent.contains("Firefox")) {
    // 火狐浏览器
    BASE64Encoder base64Encoder = new BASE64Encoder();
    filename = "=?utf-8?B?" + base64Encoder.encode(filename.getBytes("utf-8")) + "?=";
} else {
    // 其它浏览器
    filename = URLEncoder.encode(filename, "utf-8");
}
response.setHeader("Content-Disposition", "attachment;fileName="+filename+".pdf");
//下面是使用流读取 写到浏览器
~~~~~~

##### 实现验证码

~~~~~~java
 //  前端你懂的
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
     //  创建画布
     int width = 120;
     int height = 40;
     BufferedImage bufferedImage = new BufferedImage(width, height, BufferedImage.TYPE_INT_RGB);
     //  获得画笔
     Graphics g = bufferedImage.getGraphics();
     //  填充背景颜色
     g.setColor(Color.white);
     g.fillRect(0, 0, width, height);
     //  绘制边框
     g.setColor(Color.red);
     g.drawRect(0, 0, width - 1, height - 1);
     //  生成随机字符
     //  准备数据
     String data = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz1234567890";
     //  准备随机对象
     Random r = new Random();
     //  声明一个变量 保存验证码
     String code = "";
     //  书写4个随机字符
     for (int i = 0; i < 4; i++) {
         //  设置字体
         g.setFont(new Font("宋体", Font.BOLD, 28));
         //  设置随机颜色
         g.setColor(new Color(r.nextInt(255), r.nextInt(255), r.nextInt(255)));

         String str = data.charAt(r.nextInt(data.length())) + "";
         g.drawString(str, 10 + i * 28, 30);

         //  将新的字符 保存到验证码中
         code = code + str;
     }
     //  绘制干扰线
     for (int i = 0; i < 6; i++) {
         //  设置随机颜色
         g.setColor(new Color(r.nextInt(255), r.nextInt(255), r.nextInt(255)));

         g.drawLine(r.nextInt(width), r.nextInt(height), r.nextInt(width), r.nextInt(height));
     }

     //  将验证码 打印到控制台
     System.out.println(code);

     //  将验证码放到session中
     //request.getSession().setAttribute("code_session", code);

     //  将画布显示在浏览器中
     ImageIO.write(bufferedImage, "jpg", response.getOutputStream());
 }
~~~~~~

### request对象（获得请求）

  #### ServletRequest 的子接口 HttpServletRequest

+ 实现类是tomcat引擎创建好的

#### 获取请求行

+ **获取请求的方式**

~~~~~~java
//返回值GET  POST
String method = request.getMethod();
System.out.println(method);
~~~~~~

+ 获取请求的参数，请求的服务器路径 String getRequestURI()

+ 获取请求的参数，请求服务器路径  StringBuffer  getRequestURL()

~~~~~~java
//url统一资源定位符    uri统一资源标识符
StringBuffer url = request.getRequestURL();
String uri = request.getRequestURI();
System.out.println(url); //     http://localhost:8080/WEB04/line
System.out.println(uri); //     /WEB04/line
~~~~~~

+ **获取应用服务器文件名称  request.getContextPath()  //      /WEB04**

+ String     getQueryString()   //获取问号后面的所有参数

#### 获取请求头（k: v  指导服务器的）

+ String getHeader(String key)    //返回一个键对应的值  referer//返回的是上一个页面的来源 用这个判断可以防盗链
+ Enumeration   getHeaderNames()    //这个是迭代器的前身    两个方法     hasMoreElements()   nextElment()

~~~~~~java
Enumeration<String> enu = request.getHeaderNames();
while(enu.hasMoreElements()) {
    System.out.println(enu.nextElement());
    //再用getHeader获取值
}
~~~~~~

#### 获取请求参数

+ String  getParameter("传递的name值") //获取指定的请求参数
+ String[] getParameterValues("传递name的值")  //一键多值的情况   例如cehckbox
+ Map<String, String[]> getParameterMap()    //获取所有的键值

~~~~~~java
 //获取请求参数的三个方法
String val = request.getParameter("username");

String[] s = request.getParameterValues("haha");

Map<String, String[]> map = request.getParameterMap();
for(Map.Entry<String, String[]> m: map.entrySet()) {
    System.out.println(m.getKey()+"-->"+m.getValue());  //注意value是数组
}
~~~~~~

#### request域对象

+ 作用域是一次请求
+ setAttribute(String s, Object o)
+ getAttribute(String key)
+ removeAttribute(String key)

#### request处理中文乱码问题

##### 出现的原因

+ 浏览器是utf8 编码的   但是服务器解码默认使用iso8859-1

##### 处理方法

+ tomcat 8.5以上版本 使用  request.setCharacterEncoding()   //高版本设置这一个就可以了
+ 8.5版本以下   get参数不适用 

~~~~~~java
String username = request.getParameter("username");
// 首先用拉丁编码把乱码转成字节   然后用utf-8转成字符串
new String(username.getBytes("iso8859-1"), "utf-8");
~~~~~~

#### 转发

+ RequestDidpacher        getRequestDidpacher()    //获得转发器
+  forword(request, response)   //转发

~~~~~~java
//将servlet1请求转发给servlet2
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    //设置转发
    request.setAttribute("leige", "java");
    RequestDispatcher rd = request.getRequestDispatcher("/servlet2");
    rd.forward(request, response);
}
~~~~~~

#### 转发和重定向的区别

##### 重定向

+ 浏览器两次请求
+ 浏览器地址栏发生变化
+ 重定向可以区外网
+ 重定向写web应用名称  /web04/servlet2
+ 浏览器看到的结果是servlet2

##### 转发（wait()  //释放锁      sleep()  //不释放锁）

+ 浏览器一次请求
+ 浏览器地址不变
+ 转发是服务器内部行为，浏览器不知道，不能到外网
+ 转发不能写web应用名称
+ 浏览器看到结果servlet2

#### javaEE三层架构 （高内聚，低耦合）

##### 用户注册案例

+ 创建数据库
+ 创建新的module
+ 创建包
  + 添加jar
  + 配置文件
+ 功能编写服务器程序

#### BeanUtils静态方法  

+ BeanUtils.populate(对象， 取到的map)

#### 登陆注册案例的实现

+ 创建数据库
+ 创建项目 （web , service, dao, domain, utils）

### 会话技术

#### 什么叫会话

+ 打开一次浏览器   访问某个页面  只要不关闭浏览器   就算一次会话   再次访问还是算一次会话
+ 服务器的session存储   由客户端用cookie存储     就像超市密码柜    纸条相当于cookie   柜子是服务器

#### 像浏览器发送cookie 本质是当文件来存储的

~~~~~~java
//设置cookie
Cookie cookie = new Cookie("leige", "java");
//发送到客户端
response.addCookie(cookie);
~~~~~~

#### 获取浏览器请求的cookie

+ request 有一个方法叫   getCookies()    //返回保存多个cookie数组
+ Cookie    有方法叫    getName()  //获取键     getValue()   //返回值

~~~~~~java
Cookie[] cs = request.getCookies();
for(Cookie c: cs) {
    System.out.println(c.getValue());
}
~~~~~~

#### cookie中使用中文（不建议使用中文）

+ 只有8版本才支持cookie设置中文
+ 如果想在低版本 

~~~~~~java
URLEncoder.encode(String s, String charsetname)
URLDecoder.decode(String s, String charsetname)

~~~~~~

#### cookie的携带路径

+ 并不是每次请求都会携带cookie，浏览器携带cookie，在cookie产生的路径下，例如abc/下面产生的cookie只会在该路径下面访问  会携带cookie
+ 所以要设置cookie的携带路径

~~~~~~java
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    Cookie co = new Cookie("leige", "java");
    // 返回设置的cookie
    //设置cookie的携带路径 为整个模块下面
    co.setPath(request.getContextPath());
    response.addCookie(co);
}
~~~~~~

#### cookie的生存时间

+ 生存时间默认是当前的会话
+ 设置生存时间，cookie对象的方法 setMaxAge(单位是秒)

#### 记录上一次的访问时间案例

~~~~~~java
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    //获取cookie  看是否存取值
    Cookie[] cos = request.getCookies();
    if(cos == null) {
        //设置编码
        response.setContentType("text/html;charset=utf-8");
        response.getWriter().print("欢迎第一次访问");

        //获取当前时间  保存为用户可以看懂的格式
        SimpleDateFormat sf = new SimpleDateFormat("yyyy-MM-dd-hh-mm-ss");
        String s = sf.format(new Date());
        //设置cookie保存这次的访问时间
        Cookie co = new Cookie("lastDate", s);
        //设置失效时间 单位是秒
        co.setMaxAge(10*60);
        //设置携带路径
        co.setPath(request.getContextPath());
        response.addCookie(co);
    }else {
        for(Cookie co: cos) {
            if (co.getName().equals("lastDate")) {
                //设置编码 
                response.setContentType("text/html;charset=utf-8");
                response.getWriter().print("你的上一次访问时间是" + co.getValue());
            }
        }
        //获取当前时间  保存为用户可以看懂的格式
        SimpleDateFormat sf = new SimpleDateFormat("yyyy-MM-dd-hh-mm-ss");
        String s = sf.format(new Date());
        //设置cookie保存这次的访问时间
        Cookie co = new Cookie("lastDate", s);
        //设置携带路径
        co.setPath(request.getContextPath());
        response.addCookie(co);
    }

}
~~~~~~

#### session

+ HttpSession接口实现类对象是session      
+ request.getSession();   //作用域是一次会话有效  （只要浏览器不关闭就有效）
+ setAttribute()   getAttribue()      removeAttribute()

#### 持久化session存储

+ 实际上session的持久化 是客户端cookie的持久化  把服务器的sessionid存到浏览器cookie中  下次访问就可以访问的到
+ getSession方法干了很多事
  + 获得浏览器携带的cookie
  + 找一个键sessionid（对应一个session域对象）   找到或者找不到
  + 找不到就新创建一个session域对象
  + 找到sessionid 然后区session中找id对应的session
  + 如果匹配到了  不会新创建而是直接找到拿来用   
  + 找不到就新创建session域对象

~~~~~~java
//存储session的值  并返回session的id保存到cookie中   键名叫JSESSIONID
HttpSession session = request.getSession();
session.setAttribute("leige", "磊哥");
//session域的唯一编号  存到cookie 下次访问直接使用这个 session相当于小票
String id  = session.getId();
Cookie co = new Cookie("JSESSIONID", id);
co.setPath(request.getContextPath());
co.setMaxAge(60 * 10);
response.addCookie(co);
~~~~~~

~~~~~~java
//取出值  这就是session的持久化
HttpSession session = request.getSession();
System.out.println(session.getAttribute("leige"));
~~~~~~

#### session对象的生命周期

+ 什么时候创建
  + request.getSession()  Cookie中的id和服务器大的id匹配不上就创建

+ session什么时候销毁
  + 默认30分钟销毁 ，tomcat全局配置为你按web.xml
  + 调用方法session.invalidate()
  + 关闭服务器（非正常关闭服务器）

#### 清除cookie

+  覆盖的方法
  + 保证同名键
  + 保证相同的携带路径
  + setMaxAge(0)   //覆盖cookie法

#### 验证码案例分析

~~~~~~java
//取出服务器中session保存的验证码的值和客户端提交的值进行对比
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    HttpSession session = request.getSession();
    String code = (String)session.getAttribute("code_session");
    if(code.equalsIgnoreCase(request.getParameter("yanzheng"))) {
        response.getWriter().print("succ");
    }else {
        response.getWriter().print("err");
    }
}
~~~~~~

#### session和cookie的比较

![1563761212083](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1563761212083.png)



### jsp(java的动态服务器端网页技术)java server page

#### 在html中潜入java代码

+ <%%>
+ <%=%>
+ <%!%>  声明的变量  变成成员变量   基本不使用

#### jsp运行的原理

+ 本质就是servlet

![1563762734599](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1563762734599.png)

#### jsp注释

+ <!-- -->jsp中存在，翻译后.java存在，浏览器中也存在
+ <%  //   /* */%>  浏览器中不存在
+ <%-- --%>  旨在jsp源码中存在

#### jsp的九大内置对象

+ **request**
+ **response**
+ ServletContext对象，在jsp中写只能写application
+ ServletConfig -->config(jsp service里面声明的)
+ **session**
+ out 继承Writer
+ this 当前jsp类对象（page）
+ **PageContext 最小域对象       作用域是当前页面**
+ Exception 异常

### el表达式

#### 从域中取数据表达式  （${表达式}）

+ application.setAttribute(String key, Object value)   //原本就是ServletContext
  + ${applicationScope.key}
+ session
  + ${sessionScope.key}
+ request
  + ${requestScope.key}
+ pageContext
  + el表达式 ${pageScope.key}
+ 简化写法${key}   : el自动从最小的域开始找，找不到就不找了

~~~~~~jsp
<%
application.setAttribute("haha", "这是最大域");
session.setAttribute("haha","session域");
request.setAttribute("haha","request域");
pageContext.setAttribute("haha", "page域");
%>
<%-- 取不到是空字符串  友好度提升--%>
${applicationScope.haha}
${sessionScope.haha}
${requestScope.haha}
${pageScope.haha}
${haha}//默认从最小的域开始找
~~~~~~

#### 存储user用户到域对象（list集合中）并且取出 （对比el标签的好处）

~~~~~~jsp
<body>
    <%
        Addr addr1 = new Addr();
        addr1.setLocation("北京5环");
        addr1.setName("北京");

        Addr addr2 = new Addr();
        addr2.setLocation("南京6环");
        addr2.setName("南京");

        User user1 = new User();
        user1.setAddr(addr1);
        User user2 = new User();
        user2.setAddr(addr2);
        ArrayList<User> list = new ArrayList<User>();
        list.add(user1);
        list.add(user2);
        pageContext.setAttribute("list", list);
    %>
    <%=list.get(0).getAddr().getName()%>
    ${list[1].addr.name}
</body>
~~~~~~

#### 存储user用户到域对象（map集合中）并且取出 （对比el标签的好处）

~~~~~~jsp
<body>
<%
    Addr addr1 = new Addr();
    addr1.setLocation("北京5环");
    addr1.setName("北京");

    Addr addr2 = new Addr();
    addr2.setLocation("南京6环");
    addr2.setName("南京");

    User user1 = new User();
    user1.setAddr(addr1);
    User user2 = new User();
    user2.setAddr(addr2);
    Map<String, User> map = new HashMap<String, User>();
    map.put("u1", user1);
    map.put("u2", user2);
    pageContext.setAttribute("map", map);
%>
    ${map.u1.addr.name}
    ${pageScope.map.u1.addr.name}
    ${pageScope.map['u1'].addr.name}
</body>
~~~~~~

#### el取出内置对象的数据

+ pageContext
  + 获取jsp内置对象request    
  + pageContext.request.contextPath  //获取文本应用名称

+ cookie.键名.value  //获取cookie的值

#### el运算符

+ 三元运算符   ${num>4? "haha": "hehe"}
+ 判空  ${empty str}   
  + 对象是否为null
  + 字符串""
  + 数据集合长度是否>0

#### 记录上次的用户名

~~~~~~java
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    //利用cookie存储
    String username = request.getParameter("username");
    String password = request.getParameter("password");
    String rem = request.getParameter("rem");
    if(rem == null) {
        Cookie co = new Cookie("uname", username);
        co.setMaxAge(0);
        response.addCookie(co);
    }
    if(rem!=null && rem.equals("rem")) {
        Cookie co = new Cookie("uname", username);
        response.addCookie(co);
    }
    //判断
    if(username.equals("tom") && password.equals("123")) {
        response.sendRedirect(request.getContextPath());
    }else {
        response.sendRedirect(request.getContextPath()+"/login.jsp");
    }
}
~~~~~~

### jstl标签库

#### 使用标签库

+ 在开头引入标签库
+ 指令 <%@ taglib  prefix="c" uri='....'%>

#### if标签

~~~~~~java
<body>
    <%
        pageContext.setAttribute("leige", 5);
    %>
    <c:if test="${leige>2}">
        <div>nihao</div>
    </c:if>
</body>
~~~~~~

#### foreach标签

~~~~~~~jsp
 <c:forEach begin="1" end="5" var="i" //i 自动存储到pageContext域中   step="2">
     ${i}//取出存取的值
</c:forEach>
~~~~~~~

#### 增强for循环

~~~~~~jsp
 <c:forEach items="${arr} var="i" varStatus="vs">
     ${i}, ${vs.count}//取出存取的值  后面是循环的次数
</c:forEach>
~~~~~~

#### 开发模式发展历史

##### jsp model1 第一代（全是jsp）

##### jsp model1 第二代 （把业务的逻辑内容放到javaBean中）

##### jsp model2 (mvc)

![1563788457433](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1563788457433.png)

#### 商品展示案例 ......

##### 展示后来商品  （这个之前做过）

##### 删除商品信息 （根据传入的主键进行修改）

##### 查询商品

##### 分页（主要是封装pagebean对象，以后的分页就需要这五个数据）

+ 当前页  currentPage
+ 总条数  totalCount
+ 总页数  totalPage
+ 每页显示的个数  everyCount
+ 每页显示的数据  list 

### 监听器和过滤器（像安检一样）

#### 客户端和资源之间

#### 实现步骤

+ 配置xml

~~~~~~xml
<filter>
    <filter-name>my</filter-name>
    <filter-class>com.leige.Filter.MyFilter</filter-class>
</filter>
<filter-mapping>
    <filter-name>my</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>
~~~~~~

+ 实现接口的方法

~~~~~~~java
System.out.println("filter1");
//放行
filterChain.doFilter(servletRequest, servletResponse);
~~~~~~~

#### 过滤器的生命周期

+ init  过滤器对象创建       tomcat服务器启动时创建
+ doFilter（）   //过滤被访问的资源的时候
+ destory    // 停掉服务器之前被调用

####  过滤器的配置

+ 绝对匹配   /abc  
+ 目录匹配   /abc/*
+ 后缀名匹配

#### 直接配置过滤器

```java
@WebFilter(urlPatterns = "/filter1")
```

#### 过滤器的执行顺序

+ 配置文件看 mapping位置
+ 注解开发看 类名的自然顺序

#### 过滤器解决中文乱码问题

~~~~~~java
request.setCharacterEncoding(); //写在全局额过滤器中
~~~~~~

### 监听器

#### 监听某个组件的变化 主要是 request，session, servletContext

#### 监听器的接口

![1564112094241](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1564112094241.png)



##### 唯一比较实用的是servletContextListener

+ 注解开发  @WebListener
+ 配置开发  

