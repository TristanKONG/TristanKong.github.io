# JDBC

## 1、加载数据库驱动程序

```
Class.forname("com.mysql.jdbc.Driver");
```

## 2、获取连接

### 方法一：先分后总

```
String url="  ";

String user="  ";

String password="  ";

Connection conn=DriverManager.getConnection(url,user,password);
```

### 方法二：直接总

```
Connection conn=DriverManager.getConnection("url","user","password");
```

**e.g.**

``Connection conn = DriverManager.getConnection( "jdbc:mysql://localhost:3306/mydatabase", "username", "password"); ``

其中，localhost代表主机，3306是MySQL默认的端口号，后面的mydatabase代指数据库所在文件夹

## 3、获取数据库操作对象

```
Statement st=conn.createStatement();
```

（在Java中使用JDBC连接到数据库通常需要执行SQL语句。为了执行SQL语句，我们需要创建一个Statement对象。这个对象用于发送SQL语句到数据库并接收结果。

在创建Statement对象时，需要传递Connection对象。这是因为Statement对象依赖于Connection对象来与数据库建立连接，从而向数据库发送SQL代码并获取结果。）

## 4、执行SQL语句

Stmt对象有三种执行SQL语句的方法：

* executeQuery()
  
* executeUpdate()
  
* execute()
  

**executeQuery()**

用于执行查询操作，并返回ResultSet（结果集）对象。

例如：

`ResultSet rs = stmt.executeQuery("SELECT * FROM emp");`

**executeUpdate()**

用于执行INSERT、UPDATE或DELETE操作，并返回受影响的行数。

例如：

`int result = stmt.executeUpdate("INSERT INTO emp(name, age) VALUES('张三', 25)");`

**execute()**

用于执行任意SQL语句，返回一个boolean类型的值。如果执行的是SELECT语句，则返回true，并且可以通过getResultSet()方法获得ResultSet对象。如果执行的是INSERT、UPDATE或DELETE语句，则返回false，并且可以通过getUpdateCount()方法获得受影响的行数。

例如：

```java
boolean hasResult = stmt.execute("SELECT * FROM emp");
if(hasResult) {
ResultSet rs = stmt.getResultSet();
}
else {
int result = stmt.getUpdateCount();
}
```

## 5、处理查询结果集

当使用executeQuery()方法执行SELECT语句时，会返回一个ResultSet对象。我们可以使用ResultSet的next()方法来遍历结果集中的数据。

例如：

```
ResultSet rs = stmt.executeQuery("SELECT * FROM emp"); 

while(rs.next()) {

 int id = rs.getInt("id");

  String name = rs.getString("name"); 

int age = rs.getInt("age"); //处理结果 

}
```

## 6、释放资源

使用close()方法关闭数据库连接，Stmt和Resultset对象

* conn.close();
  
* stmt.close();
  
* rs.close();
