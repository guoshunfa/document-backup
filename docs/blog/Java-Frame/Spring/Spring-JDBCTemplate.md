# JdbcTemplate

### JdbcTemplate( 概念和准备 )

**1** 、什么是 **JdbcTemplate**
（ 1 ）Spring框架对JDBC进行封装，使用JdbcTemplate方便实现对数据库操作

**2** 、准备工作
（ 1 ）引入相关jar包

（ 2 ）在spring配置文件配置数据库连接池
<!-- 数据库连接池 -->
<bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource"
destroy-method="close">
<property name="url" value="jdbc:mysql:///user_db" />
<property name="username" value="root" />
<property name="password" value="root" />
<property name="driverClassName" value="com.mysql.jdbc.Driver" />
</bean>

（ 3 ）配置JdbcTemplate对象，注入DataSource
<!-- JdbcTemplate对象 -->
<bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
<!--注入dataSource-->
<property name="dataSource" ref="dataSource"></property>
</bean>

（ 4 ）创建service类，创建dao类，在dao注入jdbcTemplate对象

* 配置文件
  <!-- 组件扫描 -->
  <context:component-scan base-package="com.atguigu"></context:component-scan>

⚫ Service
@Service
public class BookService {
//注入dao
@Autowired
private BookDao bookDao;
}


⚫ Dao
@Repository
public class BookDaoImpl implements BookDao {
//注入JdbcTemplate
@Autowired
private JdbcTemplate jdbcTemplate;
}

### JdbcTemplate 操作数据库（添加）

**1** 、对应数据库创建实体类

**2** 、编写 **service** 和 **dao**
（ 1 ）在dao进行数据库添加操作
（ 2 ）调用JdbcTemplate对象里面update方法实现添加操作

⚫ 有两个参数
⚫ 第一个参数：sql语句
⚫ 第二个参数：可变参数，设置sql语句值
@Repository
public class BookDaoImpl implements BookDao {
//注入JdbcTemplate
@Autowired
private JdbcTemplate jdbcTemplate;
//添加的方法
@Override
public void add(Book book) {
//1 创建sql语句
String sql = "insert into t_book values(?,?,?)";
//2 调用方法实现
Object[] args = {book.getUserId(), book.getUsername(),
book.getUstatus()};
int update = jdbcTemplate.update(sql,args);


System.out.println(update);
}
}

**3** 、测试类
@Test
public void testJdbcTemplate() {
ApplicationContext context =
new ClassPathXmlApplicationContext("bean1.xml");
BookService bookService = context.getBean("bookService",
BookService.class);
Book book = new Book();
book.setUserId("1");
book.setUsername("java");
book.setUstatus("a");
bookService.addBook(book);
}

### JdbcTemplate 操作数据库（修改和删除）

1 、修改

@Override
public void updateBook(Book book) {
String sql = "update t_book set username=?,ustatus=? where user_id=?";
Object[] args = {book.getUsername(), book.getUstatus(),book.getUserId()};
int update = jdbcTemplate.update(sql, args);
System.out.println(update);
}

2 、删除
@Override
public void delete(String id) {
String sql = "delete from t_book where user_id=?";
int update = jdbcTemplate.update(sql, id);
System.out.println(update);
}

### JdbcTemplate 操作数据库（查询返回某个值）

**1** 、查询表里面有多少条记录，返回是某个值
**2** 、使用 **JdbcTemplate** 实现查询返回某个值代码

⚫ 有两个参数
⚫ 第一个参数：sql语句
⚫ 第二个参数：返回类型Class
//查询表记录数
@Override
public int selectCount() {


String sql = "select count(*) from t_book";
Integer count = jdbcTemplate.queryForObject(sql, Integer.class);
return count;
}

### JdbcTemplate 操作数据库（查询返回对象）

**1** 、场景：查询图书详情
**2** 、 **JdbcTemplate** 实现查询返回对象

⚫ 有三个参数
⚫ 第一个参数：sql语句
⚫ 第二个参数：RowMapper 是接口，针对返回不同类型数据，使用这个接口里面实现类完成
数据封装
⚫ 第三个参数：sql语句值
//查询返回对象
@Override
public Book findBookInfo(String id) {
String sql = "select * from t_book where user_id=?";
//调用方法
Book book = jdbcTemplate.queryForObject(sql, new
BeanPropertyRowMapper<Book>(Book.class), id);
return book;
}

### JdbcTemplate 操作数据库（查询返回集合）

**1** 、场景：查询图书列表分页 **...**

**2** 、调用 **JdbcTemplate** 方法实现查询返回集合

⚫ 有三个参数
⚫ 第一个参数：sql语句
⚫ 第二个参数：RowMapper 是接口，针对返回不同类型数据，使用这个接口里面实现类完成
数据封装
⚫ 第三个参数：sql语句值
//查询返回集合
@Override
public List<Book> findAllBook() {
String sql = "select * from t_book";
//调用方法
List<Book> bookList = jdbcTemplate.query(sql, new
BeanPropertyRowMapper<Book>(Book.class));
return bookList;
}

### JdbcTemplate 操作数据库（批量操作）

**1** 、批量操作：操作表里面多条记录

**2** 、 **JdbcTemplate** 实现批量添加操作


⚫ 有两个参数
⚫ 第一个参数：sql语句
⚫ 第二个参数：List集合，添加多条记录数据
//批量添加
@Override
public void batchAddBook(List<Object[]> batchArgs) {
String sql = "insert into t_book values(?,?,?)";
int[] ints = jdbcTemplate.batchUpdate(sql, batchArgs);
System.out.println(Arrays.toString(ints));
}
//批量添加测试
List<Object[]> batchArgs = new ArrayList<>();
Object[] o1 = {"3","java","a"};
Object[] o2 = {"4","c++","b"};
Object[] o3 = {"5","MySQL","c"};
batchArgs.add(o1);
batchArgs.add(o2);
batchArgs.add(o3);
//调用批量添加
bookService.batchAdd(batchArgs);

**3** 、 **JdbcTemplate** 实现批量修改操作
//批量修改
@Override
public void batchUpdateBook(List<Object[]> batchArgs) {
String sql = "update t_book set username=?,ustatus=? where user_id=?";
int[] ints = jdbcTemplate.batchUpdate(sql, batchArgs);
System.out.println(Arrays.toString(ints));
}
//批量修改
List<Object[]> batchArgs = new ArrayList<>();
Object[] o1 = {"java0909","a3","3"};
Object[] o2 = {"c++1010","b4","4"};
Object[] o3 = {"MySQL1111","c5","5"};
batchArgs.add(o1);
batchArgs.add(o2);
batchArgs.add(o3);
//调用方法实现批量修改
bookService.batchUpdate(batchArgs);

**4** 、 **JdbcTemplate** 实现批量删除操作
//批量删除
@Override
public void batchDeleteBook(List<Object[]> batchArgs) {
String sql = "delete from t_book where user_id=?";
int[] ints = jdbcTemplate.batchUpdate(sql, batchArgs);
System.out.println(Arrays.toString(ints));
}
//批量删除
List<Object[]> batchArgs = new ArrayList<>();

Object[] o1 = {"3"};
Object[] o2 = {"4"};
batchArgs.add(o1);
batchArgs.add(o2);
//调用方法实现批量删除
bookService.batchDelete(batchArgs);