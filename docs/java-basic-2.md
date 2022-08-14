## 一、Object类

## 1.1 概述

java.lang.Object 类是Java语言中的根类，即**所有类的父类**。它中描述的所有方法子类都可以使用。在对象实例化的时候，终找的父类就是Object。
**如果一个类没有特别指定父类， 那么默认则继承自Object类**，并可以使用Object类中所有的方法。例如：

```java
public class MyClass /*extends Object*/ {    
	// ...    
}
```

>小贴士：
>根据JDK源代码及Object类的API文档，Object类当中包含的方法有11个。

## 1.2 toString方法

- 方法摘要

  public String toString() ：返回该对象的字符串表示。

  toString方法返回该对象的字符串表示，其实该字符串内容就是**对象的类型+@+内存地址值**。 

  由于toString方法返回的结果是内存地址，而在开发中，经常需要按照对象的属性得到相应的字符串表现形式，因此也需要重写它。 

  

  ```java
  public static void main(String[] args) {
          String name = "狮子";
          //下面两个变量输出相同的值
          System.out.println(name);
          System.out.println(name.toString());
  }
  ```

  ```java
  public class People {
      private String name;
      private int age;
      public String getName() {
          return name;
      }
      public void setName(String name) {
          this.name = name;
      }
      public int getAge() {
          return age;
      }
      public void setAge(int age) {
          this.age = age;
      }
  
      public static void main(String[] args) {
          People people = new People();
          people.setName("张晓");
          //下面两个对象输出相同的地址
          System.out.println(people);
          System.out.println(people.toString());
      }
  }
  ```

>小贴士：
>单独输出一个String类型的变量或者一个对象名时都默认调用了Object的toString方法（String类默认继承自Object类，并对其Object类中的toString方法进行了重写）。

- 覆盖重写

  如果不希望使用toString方法的默认行为，则可以对它进行覆盖重写。例如自定义的Person类：

  ```java
  public class People {
      private String name;
      private int age;
      public String getName() {
          return name;
      }
      public void setName(String name) {
          this.name = name;
      }
      public int getAge() {
          return age;
      }
      public void setAge(int age) {
          this.age = age;
      }
      //对toString方法进行重写
      @Override
      public String toString() {
          return "People{" + "name='" + name + '\'' +", age=" + age +'}';
      }
  }
  ```

## 1.3 equals方法

- 方法摘要

  public boolean equals(Object obj) ：指示其他某个对象是否与此对象“相等”。

  调用成员方法equals并指定参数为另一个对象，则可以判断这两个对象是否是相同的。这里的“相同”有默认和自定义两种方式。 

  >小贴士：
  >String中的equals是对Object类中equals的重写。

- 默认地址（值）比较

  - [ ] 1.String类型的变量调用equals是调用String类中的equals方法，只比较内容是否相同；
  - [ ] 2.Object类型的变量调用equals是调用Object类中的equals方法，比较的是对象的地址。

- 自定义比较

  如果希望进行对象的内容比较，即所有或指定的部分成员变量相同就判定两个对象相同，则可以覆盖重写equals方 法。例如：

  ```java
  //重写equals方法
  public boolean equals(Object anObject){
      if (this == anObject){
          return true;
      }
      if (anObject instanceof Dog){
          Dog d = (Dog)anObject;
          if (d.getName().equals(this.name) && d.getAge() == this.age){
              return true;
          }
      }
      return false;
  }
  ```

## 1.4 Objects类

在JDK7添加了一个Objects工具类，它提供了一些方法来操作对象，它由一些静态的实用方法组成，这些方法是 null-save（空指针安全的）或null-tolerant（容忍空指针的），用于计算对象的hashcode、返回对象的字符串表 示形式、比较两个对象。

在比较两个对象的时候，Object的equals方法容易抛出空指针异常，而Objects类中的equals方法就优化了这个问 题。方法如下：
public static boolean equals(Object a, Object b) :判断两个对象是否相等。

```java
public static boolean equals(Object a, Object b) {       
	return (a == b) || (a != null && a.equals(b));   
}
```

## 二、日期时间类

## 2.1 Date类

- 概述
  java.util.Date 类表示特定的瞬间，精确到毫秒。 

  Date类的常用构造函数：

  ```java
  public Date() ：分配Date对象并初始化此对象，以表示分配它的时间（精确到毫秒）。 
  public Date(long date) ：分配Date对象并初始化此对象，以表示自从标准基准时间（称为“历元 （epoch）”，即1970年1月1日00:00:00 GMT）以来的指定毫秒数。 
  ```

  >tips: 由于我们处于东八区，所以我们的基准时间为1970年1月1日8时0分0秒。

  ```java
  import java.util.Date;   
  public class Demo01Date {     
  	public static void main(String[] args) {         
  		// 创建日期对象，把当前的时间输出   
  		System.out.println(new Date()); // Tue Jan 16 14:37:35 CST 2018         
  		// 创建日期对象，把当前的毫秒值转成日期对象         
  		System.out.println(new Date(0L)); // Thu Jan 01 08:00:00 CST 1970 
  	} 
  }
  ```

  >tips:在使用println方法时，会自动调用Date类中的toString方法。Date类对Object类中的toString方法进行了覆盖重写，所以结果为指定格式的字符串。 

- 常用方法

  Date类中的多数方法已经过时，常用的方法有： 

  ```java
  public long getTime();//把日期对象转换成对应的时间毫秒值
  ```

## 2.2 DateFormat类

- 概述
  java.text.DateFormat 是日期/时间格式化子类的抽象类，我们通过这个类可以帮我们完成日期和文本之间的转 换,也就是可以在Date对象与String对象之间进行来回转换。

  - [ ] 格式化：按照指定的格式，从Date对象转换为String对象。 
  - [ ] 解析：按照指定的格式，从String对象转换为Date对象。 

- 构造方法

  由于DateFormat为抽象类，不能直接使用，所以需要常用它的子类 java.text.SimpleDateFormat 。这个类需要一个模式（格式）来指定格式化或解析的标准。

  构造方法为：

  ```java
  public SimpleDateFormat(String pattern) 
  //用给定的模式和默认语言环境的日期格式符号构造 SimpleDateFormat。 
  ```

参数pattern是一个字符串，代表日期时间的自定义格式。 

- 格式规则

  | 标识字母（区分大小写） | 含义 |
  | :--------------------: | ---- |
  |           y            | 年   |
  |           M            | 月   |
  |           d            | 日   |
  |           H            | 时   |
  |           m            | 分   |
  |           s            | 秒   |

  ```java
  public static void main(String[] args) {         
  	// 对应的日期格式如：2018‐01‐16 15:06:38         
  	DateFormat format = new SimpleDateFormat("yyyy‐MM‐dd HH:mm:ss");     
  }  
  ```

- 常用方法

  DateFormat类的常用方法有：
  	public String format(Date date) ：将Date对象格式化为字符串。 
  	public Date parse(String source) ：将字符串解析为Date对象。

  - [ ] format方法 

  ```java
  public class testDate {
      public static void main(String[] args) throws ParseException {
          Date date = new Date();
          SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd hh:mm:ss");
          //将一个日期对象格式化为字符串日期
          String nowDate = sdf.format(date);
          System.out.println(nowDate);
      }
  }
  ```

  - [ ] parse方法 

  ```java
  public class testDate {
      public static void main(String[] args) throws ParseException {
          Date date = new Date();
          SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd hh:mm:ss");
          //将一个字符串转换成日期
          String myDate = "2021-02-26 10:51:56";
          Date date1 = sdf.parse(myDate);
          System.out.println(date1);
      }
  }
  ```

## 2.3 Calendar类

- 概述

  java.util.Calendar 是日历类，在Date后出现，替换掉了许多Date的方法。该类将所有可能用到的时间信息封装为静态成员变量，方便获取。日历类就是方便获取各个时间属性的。 

- 获取方式

  Calendar为抽象类，由于语言敏感性，Calendar类在创建对象时并非直接创建，而是通过静态方法创建，返回子 类对象，如下：

  ```java
  Calendar静态方法
  public static Calendar getInstance() ：使用默认时区和语言环境获得一个日历
  
  例如：
  import java.util.Calendar;   
  public class Demo06CalendarInit {     
  	public static void main(String[] args) {         
  		Calendar cal = Calendar.getInstance();     
  	}     
  }
  ```

- 常用方法

  常用方法有：

  1. public int get(int field) ：返回给定日历字段的值。 
  2. public void set(int field, int value) ：将给定的日历字段设置为给定值。 
  3. public abstract void add(int field, int amount) ：根据日历的规则，为给定的日历字段添加或减去指 定的时间量。 
  4. public Date getTime() ：返回一个表示此Calendar时间值（从历元到现在的毫秒偏移量）的Date对象。

Calendar类中提供很多成员常量，代表给定的日历字段：
	

| 字段值       | 含义                                  |
| ------------ | ------------------------------------- |
| YEAR         | 年                                    |
| MONTH        | 月（从0开始，可以+1使用 )             |
| DAY_OF_MONTH | 月中的天（几号）                      |
| HOUR         | 时（12小时制）                        |
| HOUR_OF_DAY  | 时（24小时制）                        |
| MINUTE       | 分                                    |
| SECOND       | 秒                                    |
| DAY_OF_WEEK  | 周中的天（周几，周日为1，可以-1使用） |

- [ ] get/set方法 

  get方法用来获取指定字段的值，set方法用来设置指定字段的值，代码使用演示：

  ```java
   import java.util.Calendar;   
   public class CalendarUtil {     
   	public static void main(String[] args) {         
   		// 创建Calendar对象         
   		Calendar cal = Calendar.getInstance();         
   		// 设置年          
   		int year = cal.get(Calendar.YEAR);        
   		// 设置月         
   		int month = cal.get(Calendar.MONTH) + 1;         
   		// 设置日         
   		int dayOfMonth = cal.get(Calendar.DAY_OF_MONTH);         
   		System.out.print(year + "年" + month + "月" + dayOfMonth + "日");     
   	}     
  }
  
  import java.util.Calendar;   
  public class Demo07CalendarMethod {     
  	public static void main(String[] args) {         
  		Calendar cal = Calendar.getInstance();         
  		cal.set(Calendar.YEAR, 2020);         
  		System.out.print(year + "年" + month + "月" + dayOfMonth + "日"); // 2020年1月17日     
  	} 
  }
  ```

- [ ] add方法 

  add方法可以对指定日历字段的值进行加减操作，如果第二个参数为正数则加上偏移量，如果为负数则减去偏移 量。代码如：

  ```java
  import java.util.Calendar;   
  public class Demo08CalendarMethod {     
  	public static void main(String[] args) {        
  		 Calendar cal = Calendar.getInstance();         
  		 System.out.print(year + "年" + month + "月" + dayOfMonth + "日"); // 2018年1月17日         
  		 // 使用add方法         
  		 cal.add(Calendar.DAY_OF_MONTH, 2); // 加2天         
  		 cal.add(Calendar.YEAR, ‐3); // 减3年         
  		 System.out.print(year + "年" + month + "月" + dayOfMonth + "日"); // 2015年1月18日;      
  	} 
  }
  ```

- [ ] getTime方法 

  Calendar中的getTime方法并不是获取毫秒时刻，而是拿到对应的Date对象。

  ```java
  import java.util.Calendar; import java.util.Date;   
  public class Demo09CalendarMethod {     
  	public static void main(String[] args) {         
  		Calendar cal = Calendar.getInstance();         
  		Date date = cal.getTime();         
  		System.out.println(date); // Tue Jan 16 16:03:09 CST 2018     
  	} 
  }
  ```

>小贴士：
>西方星期的开始为周日，中国为周一。
>在Calendar类中，月份的表示是以0-11代表1-12月。
>日期是有大小关系的，时间靠后，时间越大。 

## 三、常用API（System类、StringBuilder类、包装类）

## 3.1 System类

java.lang.System 类中提供了大量的静态方法，可以获取与系统相关的信息或系统级操作，在System类的API文档中，常用的方法有：

1. public static long currentTimeMillis() ：返回以毫秒为单位的当前时间。 
2. public static void arraycopy(Object src, int srcPos, Object dest, int destPos, int length) ：将数组中指定的数据拷贝到另一个数组中。 

- currentTimeMillis方法

  currentTimeMillis方法就是 获取当前系统时间与1970年01月01日00:00点之间的毫秒差值。


  ```java
  public static void main(String[] args) {         
  	//获取当前时间毫秒值           
  	System.out.println(System.currentTimeMillis()); // 1516090531144    
  } 
  ```

- arraycopy方法

  public static void arraycopy(Object src, int srcPos, Object dest, int destPos, int length) ：将数组中指定的数据拷贝到另一个数组中。

  数组的拷贝动作是系统级的，性能很高。System.arraycopy方法具有5个参数，含义分别为：

  | 参数序号 | 参数名称 | 参数类型 | 参数含义             |
  | -------- | -------- | -------- | -------------------- |
  | 1        | src      | Object   | 源数组               |
  | 2        | srcPos   | int      | 源数组索引起始位置   |
  | 3        | dest     | Object   | 目标数组             |
  | 4        | destPos  | int      | 目标数组索引起始位置 |
  | 5        | length   | int      | 复制元素个数         |

  例如：将src数组中前3个元素，复制到dest数组的前3个位置上。
  复制元素前：src数组元素[1,2,3,4,5]，dest数组元素 [6,7,8,9,10]
  复制元素后：src数组元素[1,2,3,4,5]，dest数组元素[1,2,3,9,10]

  ```java
  import java.util.Arrays;   
  public class systemArrayCopy {     
  	public static void main(String[] args) {         
  		int[] src = new int[]{1,2,3,4,5};         
  		int[] dest = new int[]{6,7,8,9,10};         
  		System.arraycopy( src, 0, dest, 0, 3);         
  		/*代码运行后：两个数组中的元素发生了变化          
  		src数组元素[1,2,3,4,5]          
  		dest数组元素[1,2,3,9,10]         
  		*/     
  	} 
  }
  ```

## 3.2 StringBuilder类

![StringBuilder数据结构](https://img-blog.csdnimg.cn/20210228151636289.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzUwOTk0MjM1,size_16,color_FFFFFF,t_70)

- StringBuilder类的由来（字符串拼接问题）

  由于String类的对象内容不可改变，所以每当进行字符串拼接时，总是会在内存中创建一个新的对象。例如：


  ```java
  public class StringDemo {     
  	public static void main(String[] args) {         
  		String s = "Hello";         
  		s += "World";         
  		System.out.println(s);     
  	} 
  }
  ```

  在API中对String类有这样的描述：字符串是常量，它们的值在创建后不能被更改。

  根据这句话分析我们的代码，其实总共产生了三个字符串，即 "Hello" 、 "World" 和 "HelloWorld" 。引用变量s 首先指向 Hello 对象，终指向拼接出来的新字符串对象，即 HelloWord 。
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20210228152214175.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzUwOTk0MjM1,size_16,color_FFFFFF,t_70)
  由此可知，如果对字符串进行拼接操作，每次拼接，都会构建一个新的String对象，既耗时，又浪费空间。为了解 决这一问题，可以使用 java.lang.StringBuilder 类。

- 概述
  查阅 java.lang.StringBuilder 的API，StringBuilder又称为可变字符序列，它是一个类似于 String 的字符串缓冲区，通过某些方法调用可以改变该序列的长度和内容。

  原来StringBuilder是个字符串的缓冲区，即它是一个容器，容器中可以装很多字符串。并且能够对其中的字符串进行各种操作。

  它的内部拥有一个数组用来存放字符串内容，进行字符串拼接时，直接在数组中加入新内容。StringBuilder会自动维护数组的扩容。原理如下图所示：(默认16字符空间，超过自动扩充)
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20210228152431574.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzUwOTk0MjM1,size_16,color_FFFFFF,t_70)

- 构造方法

  根据StringBuilder的API文档，常用构造方法有2个：

  1. public StringBuilder() ：构造一个空的StringBuilder容器。 
  2. public StringBuilder(String str) ：构造一个StringBuilder容器，并将字符串添加进去。

  ```java
  public class StringBuilderDemo {     
  	public static void main(String[] args) {         
  		StringBuilder sb1 = new StringBuilder();         
  		System.out.println(sb1); // (空白)         
  		// 使用带参构造         
  		StringBuilder sb2 = new StringBuilder("itcast");         
  		System.out.println(sb2); // itcast     
  	} 
  }
  ```

- 常用方法

  StringBuilder常用的方法有2个：

  1. public StringBuilder append(...) ：添加任意类型数据的字符串形式，并返回当前对象自身。   	
  2. public String toString() ：将当前StringBuilder对象转换为String对象。

  - [ ] append方法
    append方法具有多种重载形式，可以接收任意类型的参数。任何数据作为参数都会将对应的字符串内容添加到 StringBuilder中。例如：

  ```java
  public class Demo02StringBuilder { 
  	public static void main(String[] args) {      
  		//创建对象          
  		StringBuilder builder = new StringBuilder();          
  		//public StringBuilder append(任意类型)          
  		StringBuilder builder2 = builder.append("hello");          
  		//对比一下          
  		System.out.println("builder:"+builder);          
  		System.out.println("builder2:"+builder2);          
  		System.out.println(builder == builder2); //true              
  		// 可以添加 任何类型      
  		builder.append("hello");          
  		builder.append("world");          
  		builder.append(true);          
  		builder.append(100);          
  		// 在我们开发中，会遇到调用一个方法后，返回一个对象的情况。
  		//然后使用返回的对象继续调用方法。                  			    
  		// 这种时候，我们就可以把代码现在一起，如append方法一样，代码如下: 
  		//链式编程          
  		builder.append("hello").append("world").append(true).append(100);
  		System.out.println("builder:"+builder);          
  		}      
  }
  ```

  - [ ] toString方法 
    StringBuilder已经覆盖重写了Object当中的toString方法。 
    通过toString方法，StringBuilder对象将会转换为不可变的String对象。如：

  ```java
  public class Demo16StringBuilder {     
  	public static void main(String[] args) {         
  		// 链式创建         
  		StringBuilder sb = new StringBuilder("Hello").append("World").append("Java"); 
  		// 调用方法         
  		String str = sb.toString();         
  		System.out.println(str); // HelloWorldJava     
  	} 
  }
  ```

## 3.3 包装类

- 概述
  Java提供了两个类型系统，基本类型与引用类型，使用基本类型在于效率，然而很多情况，会创建对象使用，因为对象可以做更多的功能，如果想要我们的基本类型像对象一样操作，就可以使用基本类型对应的包装类，如下：

  | 基本类型 | 对应的包装类（位于java.lang包中） |
  | -------- | --------------------------------- |
  | byte     | Byte                              |
  | short    | Short                             |
  | int      | **Integer**                       |
  | long     | Long                              |
  | float    | Float                             |
  | double   | Double                            |
  | char     | **Character**                     |
  | boolean  | Boolean                           |

- 装箱与拆箱

  基本类型与对应的包装类对象之间，来回转换的过程称为”装箱“与”拆箱“：

  1. 装箱：从基本类型转换为对应的包装类对象。 
  2. 拆箱：从包装类对象转换为对应的基本类型。

  ```java
  //基本数值---->包装对象
  Integer i = new Integer(4);//使用构造函数
  Integer ii = Integer.valueOf(4);//使用包装类中的valueOf方法 
  //包装对象---->基本数值
  int num = i.intValue();
  ```

- 自动装箱与自动拆箱

  由于我们经常要做基本类型与包装类之间的转换，从Java 5（JDK 1.5）开始，基本类型与包装类的装箱、拆箱动作可以自动完成。例如：

  ```java
  //自动装箱。相当于Integer i = Integer.valueOf(4); 
  Integer i = 4;
  
  //等号右边：将i对象转成基本数值(自动拆箱) i.intValue() + 5; 
  //加法运算完成后，再次装箱，把基本数值转成对象。
  i = i + 5;
  ```

- 基本类型与字符串之间的转换 

  - [ ] 基本类型转换为String

    基本类型转换String总共有三种方式，查看课后资料可以得知，这里只讲简单的一种方式：


  ```java
  基本类型直接与””相连接即可；如：34+""
  ```

  - [ ] String转换成对应的基本类型
    除了Character类之外，其他所有包装类都具有parseXxx静态方法可以将字符串参数转换为对应的基本类型： 

    1. public static byte parseByte(String s) ：将字符串参数转换为对应的byte基本类型。 
    2. public static short parseShort(String s) ：将字符串参数转换为对应的short基本类型。 
    3. public static int parseInt(String s) ：将字符串参数转换为对应的int基本类型。 
    4. public static long parseLong(String s) ：将字符串参数转换为对应的long基本类型。 
    5. public static float parseFloat(String s) ：将字符串参数转换为对应的ﬂoat基本类型。 
    6. public static double parseDouble(String s) ：将字符串参数转换为对应的double基本类型。 
    7. public static boolean parseBoolean(String s) ：将字符串参数转换为对应的boolean基本类型。

  ```java
  public class Demo18WrapperParse {     
  	public static void main(String[] args) {         
  		int num = Integer.parseInt("100");     
  	} 
  }
  ```

  >注：如果字符串参数的内容无法正确转换为对应的基本类型，则会抛出 java.lang.NumberFormatException 异常。

# 第四章 Collection集合、Iterator接口

## 4.1 集合概述

在前面基础班我们已经学习过并使用过集合ArrayList ,那么集合到底是什么呢?

- **集合**：集合是java中提供的一种容器，可以用来存储多个数据。集合和数组既然都是容器，它们有啥区别呢？

- 数组的长度是固定的。集合的长度是可变的。
- 数组中存储的是同一类型的元素，可以存储基本数据类型值。集合存储的都是对象。而且对象的类型可以不
  一致。在开发中一般当对象多的时候，使用集合进行存储。

## 4.2 集合框架

JAVASE提供了满足各种需求的API，在使用这些API前，先了解其继承与接口操作架构，才能了解何时采用哪个类，以及类之间如何彼此合作，从而达到灵活应用。

集合按照其存储结构可以分为两大类，分别是单列集合 java.util.Collection 和双列集合 java.util.Map ，今天我们主要学习 Collection 集合，在day04时讲解 Map 集合。

- **Collection**：**单列集合类的根接口**，用于存储一系列符合某种规则的元素，它有两个重要的子接口，分别是
  java.util.List 和 java.util.Set 。其中， List 的特点是元素有序、元素可重复。 Set 的特点是元素无序，而且不可重复。 List 接口的主要实现类有 java.util.ArrayList 和 java.util.LinkedList ， Set 接口的主要实现类有 java.util.HashSet 和 java.util.TreeSet 。

从上面的描述可以看出JDK中提供了丰富的集合类库，为了便于初学者进行系统地学习，接下来通过一张图来描述整个集合类的继承体系。


![Collection体系](https://files.mdnice.com/user/34144/80612d36-8707-43c2-aee8-9784c2a04fe5.png)


其中，橙色框里填写的都是接口类型，而蓝色框里填写的都是具体的实现类。这几天将针对图中所列举的集合类进行逐一地讲解。

集合本身是一个工具，它存放在java.util包中。在 Collection 接口定义着单列集合框架中最最共性的内容。

## 4.3 Collection 常用功能

Collection是所有单列集合的父接口，因此在Collection中定义了单列集合(List和Set)通用的一些方法，这些方法可用于操作所有的单列集合。

方法如下：

- public boolean add(E e) ： 把给定的对象添加到当前集合中 。
- public void clear() :清空集合中所有的元素。
- public boolean remove(E e) : 把给定的对象在当前集合中删除。
- public boolean contains(E e) : 判断当前集合中是否包含给定的对象。
- public boolean isEmpty() : 判断当前集合是否为空。
- public int size() : 返回集合中元素的个数。
- public Object[] toArray() : 把集合中的元素，存储到数组中。

方法演示：

```java
import java.util.ArrayList;
import java.util.Collection;
public class Demo1Collection {
    public static void main(String[] args) {
      // 创建集合对象         
     // 使用多态形式    
     Collection<String> coll = new ArrayList<String>();    
     // 使用方法    
     // 添加功能  boolean  add(String s)    
     coll.add("小李广");    
     coll.add("扫地僧");    
     coll.add("石破天");    
     System.out.println(coll);    
     // boolean contains(E e) 判断o是否在集合中存在    
     System.out.println("判断  扫地僧 是否在集合中"+coll.contains("扫地僧"));    
     //boolean remove(E e) 删除在集合中的o元素    
     System.out.println("删除石破天："+coll.remove("石破天"));    
     System.out.println("操作之后集合中元素:"+coll);    
       
     // size() 集合中有几个元素    
    System.out.println("集合中有"+coll.size()+"个元素");        
    // Object[] toArray()转换成一个Object数组        
    Object[] objects = coll.toArray();    
    // 遍历数组    
    for (int i = 0; i < objects.length; i++) {    
    		System.out.println(objects[i]);            
    }        
    // void  clear() 清空集合        
    coll.clear();        
    System.out.println("集合中内容为："+coll);        
    // boolean  isEmpty()  判断是否为空        
    System.out.println(coll.isEmpty());              
    }    
}
```

`tips: 有关Collection中的方法可不止上面这些，其他方法可以自行查看API学习。`



## 4.4 Iterator接口

在程序开发中，经常需要遍历集合中的所有元素。针对这种需求，JDK专门提供了一个接口java.util.Iterator 。 Iterator 接口也是Java集合中的一员，但它与 Collection 、 Map 接口有所不同，Collection 接口与 Map 接口主要用于存储元素，而 Iterator 主要用于迭代访问（即遍历） Collection 中的元素，因此 Iterator 对象也被称为迭代器。

想要遍历Collection集合，那么就要获取该集合迭代器完成迭代操作，下面介绍一下获取迭代器的方法：

- public Iterator iterator() : 获取集合对应的迭代器，用来遍历集合中的元素的。

下面介绍一下迭代的概念：

- **迭代**：即Collection集合元素的通用获取方式。在取元素之前先要判断集合中有没有元素，如果有，就把这个元素取出来，继续在判断，如果还有就再取出出来。一直把集合中的所有元素全部取出。这种取出方式专业术语称为迭代。

Iterator接口的常用方法如下：

- public E next() :返回迭代的下一个元素。
- public boolean hasNext() :如果仍有元素可以迭代，则返回 true。

接下来我们通过案例学习如何使用Iterator迭代集合中元素：

```java
public class IteratorDemo {
   public static void main(String[] args) {  
        // 使用多态方式 创建对象
        Collection<String> coll = new ArrayList<String>();
        // 添加元素到集合
        coll.add("串串星人");
        coll.add("吐槽星人");
        coll.add("汪星人");
        //遍历
        //使用迭代器 遍历   每个集合对象都有自己的迭代器
        Iterator<String> it = coll.iterator();
        //  泛型指的是 迭代出 元素的数据类型
        while(it.hasNext()){ //判断是否有迭代元素
            String s = it.next();//获取迭代出的元素
            System.out.println(s);
        }
   }  
}
```

- tips:：在进行集合元素取出时，如果集合中已经没有元素了，还继续使用迭代器的next方法，将会发生
  java.util.NoSuchElementException没有集合元素的错误。

## 4.5 迭代器的实现原理

我们在之前案例已经完成了Iterator遍历集合的整个过程。当遍历集合时，首先通过调用t集合的iterator()方法获得迭代器对象，然后使用hashNext()方法判断集合中是否存在下一个元素，如果存在，则调用next()方法将元素取出，否则说明已到达了集合末尾，停止遍历元素。

Iterator迭代器对象在遍历集合时，内部采用指针的方式来跟踪集合中的元素，为了让初学者能更好地理解迭代器的工作原理，接下来通过一个图例来演示Iterator对象迭代元素的过程：


![迭代器实现原理](https://files.mdnice.com/user/34144/1ffaedaf-76eb-41b3-b1ce-2f4990535091.png)


在调用Iterator的next方法之前，迭代器的索引位于第一个元素之前，不指向任何元素，当第一次调用迭代器的next方法后，迭代器的索引会向后移动一位，指向第一个元素并将该元素返回，当再次调用next方法时，迭代器的索引会指向第二个元素并将该元素返回，依此类推，直到hasNext方法返回false，表示到达了集合的末尾，终止对元素的遍历。

## 4.6 增强for循环

增强for循环(也称for each循环)是JDK1.5以后出来的一个高级for循环，专门用来遍历数组和集合的。它的内部原理其实是个Iterator迭代器，所以在遍历的过程中，不能对集合中的元素进行增删操作。

格式：

```java
for(元素的数据类型  变量 : Collection集合or数组){
   //写操作代码  
}
```

它用于遍历Collection和数组。通常只进行遍历元素，不要在遍历的过程中对集合元素进行增删操作。

## 4.7 遍历数组

```java
public class NBForDemo1 {
    public static void main(String[] args) {
      int[] arr = {3,5,6,87};        
      //使用增强for遍历数组 
      for(int a : arr){
        //a代表数组中的每个元素        
      	System.out.println(a);            
      }        
		}    
}
```

## 4.8 遍历集合

```java
public class NBFor {
    public static void main(String[] args) {       
     Collection<String> coll = new ArrayList<String>();    
     coll.add("小河神");    
     coll.add("老河神");    
     coll.add("神婆");    
     //使用增强for遍历    
     for(String s :coll){//接收变量s代表 代表被遍历到的集合元素    
     System.out.println(s);        
     }    
}    
}
```

- `tips: 新for循环必须有被遍历的目标。目标只能是Collection或者是数组。新式for仅仅作为遍历操作出现。`



# 第五章 泛型

## 5.1 泛型概述

在前面学习集合时，我们都知道集合中是可以存放任意对象的，只要把对象存储集合后，那么这时他们都会被提升成Object类型。当我们在取出每一个对象，并且进行相应的操作，这时必须采用类型转换。
大家观察下面代码：

```java
public class GenericDemo {
  public static void main(String[] args) {    
    Collection coll = new ArrayList();        
    coll.add("abc");        
    coll.add("itcast");        
    coll.add(5);//由于集合没有做任何限定，任何类型都可以给其中存放        
    Iterator it = coll.iterator();        
    while(it.hasNext()){        
      //需要打印每个字符串的长度,就要把迭代出来的对象转成String类型            
      String str = (String) it.next();            
      System.out.println(str.length());            
    }        
  }    
}
```

程序在运行时发生了问题java.lang.ClassCastException。 为什么会发生类型转换异常呢？ 我们来分析下：由于集合中什么类型的元素都可以存储。导致取出时强转引发运行时 ClassCastException。 
怎么来解决这个问题呢？
Collection虽然可以存储各种对象，但实际上通常Collection只存储同一类型对象。例如都是存储字符串对象。因此在JDK5之后，新增了泛型(Generic)语法，让你在设计API时可以指定类或方法支持泛型，这样我们使用API的时候也变得更为简洁，并得到了编译时期的语法检查。

`泛型：可以在类或方法中预支地使用未知的类型。`

`tips:一般在创建对象时，将未知的类型确定具体的类型。当没有指定泛型时，默认类型为Object类型。`

## 5.2 使用泛型的好处

上一节只是讲解了泛型的引入，那么泛型带来了哪些好处呢？

- 将运行时期的ClassCastException，转移到了编译时期变成了编译失败。
- 避免了类型强转的麻烦。

通过我们如下代码体验一下：

```java
public class GenericDemo2 {
  public static void main(String[] args) {    
          Collection<String> list = new ArrayList<String>();
          list.add("abc");
          list.add("itcast");
          // list.add(5);//当集合明确类型后，存放类型不一致就会编译报错
          // 集合已经明确具体存放的元素类型，那么在使用迭代器的时候，迭代器也同样会知道具体遍历元素类型
          Iterator<String> it = list.iterator();
          while(it.hasNext()){
              String str = it.next();
              //当使用Iterator<String>控制元素类型后，就不需要强转了。获取到的元素直接就是String类型
              System.out.println(str.length());
          }
  }    
}
```

`tips:泛型是数据类型的一部分，我们将类名与泛型合并一起看做数据类型。`

## 5.3 泛型的定义与使用

我们在集合中会大量使用到泛型，这里来完整地学习泛型知识。
泛型，用来灵活地将数据类型应用到不同的类、方法、接口当中。将数据类型作为参数进行传递。

### 5.3.1定义和使用含有泛型的类

定义格式：

```java
修饰符 class 类名<代表泛型的变量> {  }
```

例如，API中的ArrayList集合：

```java
class ArrayList<E>{
    public boolean add(E e){ }
    public E get(int index){ }
   .... 
}
```

使用泛型： 即什么时候确定泛型。

### 5.3.2在创建对象的时候确定泛型

例如， 

```java
ArrayList<String> list = new ArrayList<String>();
```

此时，变量E的值就是String类型,那么我们的类型就可以理解为：

```java
class ArrayList<String>{
     public boolean add(String e){ }
     public String get(int index){  }
     ...
}
```

再例如， 

```java
ArrayList<Integer> list = new ArrayList<Integer>();
```

此时，变量E的值就是Integer类型,那么我们的类型就可以理解为：

```java
class ArrayList<Integer> {
     public boolean add(Integer e) { }
     public Integer get(int index) {  }
     ...
}
```

举例自定义泛型类

```java
public class MyGenericClass<MVP> {
    //没有MVP类型，在这里代表 未知的一种数据类型 未来传递什么就是什么类型    
    private MVP mvp;    
    
    public void setMVP(MVP mvp) {
        this.mvp = mvp;
    }
    
    public MVP getMVP() {
        return mvp;
    }
}
```

使用：

```java
public class GenericClassDemo {
   public static void main(String[] args) {             
         // 创建一个泛型为String的类
         MyGenericClass<String> my = new MyGenericClass<String>();     
         // 调用setMVP
         my.setMVP("大胡子登登");
         // 调用getMVP
         String mvp = my.getMVP();
         System.out.println(mvp);
         //创建一个泛型为Integer的类
         MyGenericClass<Integer> my2 = new MyGenericClass<Integer>();
         my2.setMVP(123);          
         Integer mvp2 = my2.getMVP();
    }
}
```

含有泛型的方法
定义格式：

```java
修饰符 <代表泛型的变量> 返回值类型 方法名(参数){  }
```

例如，

```java
public class MyGenericMethod {     
    public <MVP> void show(MVP mvp) {
     System.out.println(mvp.getClass());    
    }
   
    public <MVP> MVP show2(MVP mvp) {  
     return mvp;    
    }
}
```

此时，泛型E的值就是String类型。

### 5.3.3始终不确定泛型的类型，直到创建对象时，确定泛型的类型

例如：

```java
public class MyImp2<E> implements MyGenericInterface<E> {
  @Override    
  public void add(E e) {    
          // 省略... 
  }    
  @Override    
  public E getE() {    
  	return null;        
  }    
}
```

确定泛型：

```java
/*
 * 使用
 */
public class GenericInterface {
    public static void main(String[] args) {
        MyImp2<String>  my = new MyImp2<String>(); 
        my.add("aa");
    }
}
```

## 5.4 泛型通配符

当使用泛型类或者接口时，传递的数据中，泛型类型不确定，可以通过通配符<?>表示。但是一旦使用泛型的通配符后，只能使用Object类中的共性方法，集合中元素自身方法无法使用。

**通配符基本使用**

泛型的通配符:**不知道使用什么类型来接收的时候,此时可以使用?,?表示未知通配符。**
此时只能接受数据,不能往该集合中存储数据。

举个例子大家理解使用即可：

```java
public static void main(String[] args) {
    Collection<Intger> list1 = new ArrayList<Integer>();
    getElement(list1);
    Collection<String> list2 = new ArrayList<String>();
    getElement(list2);
}
public static void getElement(Collection<?> coll){}
//？代表可以接收任意类型
```

`tips:泛型不存在继承关系 Collection list = new ArrayList();这种是错误的。`

**通配符高级使用----受限泛型**

之前设置泛型的时候，实际上是可以任意设置的，只要是类就可以设置。但是在JAVA的泛型中可以指定一个泛型的**上限**和**下限**。

**泛型的上限：**

- 格式： 类型名称 <? extends 类 > 对象名称
- 意义： 只能接收该类型及其子类

**泛型的下限：**

- 格式： 类型名称 <? super 类 > 对象名称
- 意义： 只能接收该类型及其父类型

比如：现已知Object类，String 类，Number类，Integer类，其中Number是Integer的父类

```java
public static void main(String[] args) {
    Collection<Integer> list1 = new ArrayList<Integer>();
    Collection<String> list2 = new ArrayList<String>();
    Collection<Number> list3 = new ArrayList<Number>();
    Collection<Object> list4 = new ArrayList<Object>();
   
    getElement(list1);
    getElement(list2);//报错
    getElement(list3);
    getElement(list4);//报错
 
    getElement2(list1);//报错
    getElement2(list2);//报错
    getElement2(list3);
    getElement2(list4);
 
}
// 泛型的上限：此时的泛型?，必须是Number类型或者Number类型的子类
public static void getElement1(Collection<? extends Number> coll){}
// 泛型的下限：此时的泛型?，必须是Number类型或者Number类型的父类
public static void getElement2(Collection<? super Number> coll){}
```



## 5.5 案例介绍

按照斗地主的规则，完成洗牌发牌的动作。 具体规则：
使用54张牌打乱顺序,三个玩家参与游戏，三人交替摸牌，每人17张牌，最后三张留作底牌。

## 5.5.1 案例分析

- **准备牌**：
  牌可以设计为一个ArrayList,每个字符串为一张牌。 每张牌由花色数字两部分组成，我们可以使用花色集合与数字集合嵌套迭代完成每张牌的组装。 牌由Collections类的shuffle方法进行随机排序。
- **发牌**
  将每个人以及底牌设计为ArrayList,将最后3张牌直接存放于底牌，剩余牌通过对3取模依次发牌。
- **看牌**
  直接打印每个集合。

## 5.5.2 代码实现

```java
import java.util.ArrayList;
import java.util.Collections;
public class Poker {
    public static void main(String[] args) {
        /*
        * 1: 准备牌操作
        */
        //1.1 创建牌盒 将来存储牌面的
        ArrayList<String> pokerBox = new ArrayList<String>();
        //1.2 创建花色集合
        ArrayList<String> colors = new ArrayList<String>();
        //1.3 创建数字集合
        ArrayList<String> numbers = new ArrayList<String>();
        //1.4 分别给花色 以及 数字集合添加元素
        colors.add("♥");
        colors.add("♦");
        colors.add("♠");
        colors.add("♣");
        for(int i = 2;i<=10;i++){
            numbers.add(i+"");
        }
        numbers.add("J");
        numbers.add("Q");
        numbers.add("K");
        numbers.add("A");
        //1.5 创造牌  拼接牌操作
      	// 拿出每一个花色  然后跟每一个数字 进行结合  存储到牌盒中
        for (String color : colors) {
            //color每一个花色
            //遍历数字集合
            for(String number : numbers){
                //结合
                String card = color+number;
                //存储到牌盒中
                pokerBox.add(card);
            }
        }
        //1.6大王小王
        pokerBox.add("小☺");
        pokerBox.add("大☠");    
        // System.out.println(pokerBox);
        //洗牌 是不是就是将  牌盒中 牌的索引打乱
        // Collections类  工具类  都是 静态方法
        // shuffer方法  
        /*
         * static void shuffle(List<?> list)
         *     使用默认随机源对指定列表进行置换。
         */
        //2:洗牌
        Collections.shuffle(pokerBox);
        //3 发牌
        //3.1 创建 三个 玩家集合  创建一个底牌集合
        ArrayList<String> player1 = new ArrayList<String>();
        ArrayList<String> player2 = new ArrayList<String>();
        ArrayList<String> player3 = new ArrayList<String>();
        ArrayList<String> dipai = new ArrayList<String>();     
        //遍历 牌盒  必须知道索引  
        for(int i = 0;i<pokerBox.size();i++){
            //获取 牌面
            String card = pokerBox.get(i);
            //留出三张底牌 存到 底牌集合中
            if(i>=51){//存到底牌集合中
                dipai.add(card);
            } else {
                //玩家1   %3  ==0
                if(i%3==0){
                   player1.add(card);  
                }else if(i%3==1){//玩家2
                   player2.add(card);  
                }else{//玩家3
                   player3.add(card);  
                }
            }
        }
        //看看
        System.out.println("令狐冲："+player1);
        System.out.println("田伯光："+player2);
        System.out.println("绿竹翁："+player3);
        System.out.println("底牌："+dipai); 
}    
}
```



# 第六章 数据结构

## 6.1 数据结构有什么用？

当你用着java里面的容器类很爽的时候，你有没有想过，怎么ArrayList就像一个无限扩充的数组，也好像链表之类 的。好用吗？好用，这就是数据结构的用处，只不过你在不知不觉中使用了。 

现实世界的存储，我们使用的工具和建模。每种数据结构有自己的优点和缺点，想想如果Google的数据用的是数 组的存储，我们还能方便地查询到所需要的数据吗？而算法，在这么多的数据中如何做到最快的插入，查找，删 除，也是在追求更快。 

我们java是面向对象的语言，就好似自动档轿车，C语言好似手动档吉普。数据结构呢？是变速箱的工作原理。你 完全可以不知道变速箱怎样工作，就把自动档的车子从 A点 开到 B点，而且未必就比懂得的人慢。写程序这件事， 和开车一样，经验可以起到很大作用，但如果你不知道底层是怎么工作的，就永远只能开车，既不会修车，也不能 造车。当然了，数据结构内容比较多，细细的学起来也是相对费功夫的，不可能达到一蹴而就。

**我们将常见的数据结构**：堆栈、队列、数组、链表和红黑树 这几种给大家介绍一下，作为数据结构的入门，了解一下它们的特点即 可。

![数据结构](https://img-blog.csdnimg.cn/2021030408311699.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzUyNTk2MjU4,size_16,color_FFFFFF,t_70#pic_center)


## 6.2 常见的数据结构

数据存储的常用结构有：**栈、队列、数组、链表和红黑树**。我们分别来了解一下： 

### 6.2.1 栈

- **栈**：**stack**,又称堆栈，它是运算受限的线性表，其限制是仅允许在标的一端进行插入和删除操作，不允许在其 他任何位置进行添加、查找、删除等操作。 

简单的说：采用该结构的集合，对元素的存取有如下的特点 

- 先进后出（即，存进去的元素，要在后它后面的元素依次取出后，才能取出该元素）。例如，子弹压进弹 夹，先压进去的子弹在下面，后压进去的子弹在上面，当开枪时，先弹出上面的子弹，然后才能弹出下面的 子弹。 

- 栈的入口、出口的都是栈的顶端位置。 

  ![栈](https://img-blog.csdnimg.cn/20210304083128393.png#pic_center)


这里两个名词需要注意： 

- **压栈**：就是存元素。即，把元素存储到栈的顶端位置，栈中已有元素依次向栈底方向移动一个位置。 

- **弹栈**：就是取元素。即，把栈的顶端位置元素取出，栈中已有元素依次向栈顶方向移动一个位置。 

### 6.2.2队列

- **队列**：**queue**,简称队，它同堆栈一样，也是一种运算受限的线性表，其限制是仅允许在表的一端进行插入， 而在表的另一端进行删除。

 简单的说，采用该结构的集合，对元素的存取有如下的特点： 

- 先进先出（即，存进去的元素，要在后它前面的元素依次取出后，才能取出该元素）。例如，小火车过山 洞，车头先进去，车尾后进去；车头先出来，车尾后出来。
- 队列的入口、出口各占一侧。例如，下图中的左侧为入口，右侧为出口。 

![队列](https://img-blog.csdnimg.cn/2021030408320232.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzUyNTk2MjU4,size_16,color_FFFFFF,t_70#pic_center)


### 6.2.3 数组

- **数组**:**Array**,是有序的元素序列，数组是在内存中开辟一段连续的空间，并在此空间存放元素。就像是一排出 租屋，有100个房间，从001到100每个房间都有固定编号，通过编号就可以快速找到租房子的人。 简单的说,采用该结构的集合，对元素的存取有如下的特点： 

- 查找元素快：通过索引，可以快速访问指定位置的元素 

![通过索引查找元素](https://img-blog.csdnimg.cn/20210304083219350.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzUyNTk2MjU4,size_16,color_FFFFFF,t_70#pic_center)


- 增删元素慢 
  - `**指定索引位置增加元素**：需要创建一个新数组，将指定新元素存储在指定索引位置，再把原数组元素根` 

  - `据索引，复制到新数组对应索引的位置。如下图`

![增删元素](https://img-blog.csdnimg.cn/2021030408323164.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzUyNTk2MjU4,size_16,color_FFFFFF,t_70#pic_center)


  - `指定索引位置删除元素：需要创建一个新数组，把原数组元素根据索引，复制到新数组对应索引的位置，原数组中指定索引位置元素不复制到新数组中。如下图` 

   ![指定索引位置删除元素](https://img-blog.csdnimg.cn/20210304083242265.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzUyNTk2MjU4,size_16,color_FFFFFF,t_70#pic_center)


### 6.2.4 链表

- **链表**:**linked list**,由一系列结点node（链表中每一个元素称为结点）组成，结点可以在运行时i动态生成。每 个结点包括两个部分：一个是存储数据元素的数据域，另一个是存储下一个结点地址的指针域。我们常说的 链表结构有单向链表与双向链表，那么这里给大家介绍的是**单向链表**。 

![单链表](https://img-blog.csdnimg.cn/202103040832528.png#pic_center)


简单的说，采用该结构的集合，对元素的存取有如下的特点： 

- 多个结点之间，通过地址进行连接。例如，多个人手拉手，每个人使用自己的右手拉住下个人的左手，依次 类推，这样多个人就连在一起了。

![首尾相连](https://img-blog.csdnimg.cn/20210304083300780.png#pic_center)


- 查找元素慢：想查找某个元素，需要通过连接的节点，依次向后查找指定元素 

- 增删元素快： 

  `增加元素：只需要修改连接下个元素的地址即可。` 

![增加元素](https://img-blog.csdnimg.cn/20210304083312963.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzUyNTk2MjU4,size_16,color_FFFFFF,t_70#pic_center)


  `删除元素：只需要修改连接下个元素的地址即可。` 

![删除元素](https://img-blog.csdnimg.cn/20210304083326129.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzUyNTk2MjU4,size_16,color_FFFFFF,t_70#pic_center)


### 6.2.5 红黑树

**二叉树**：**binary tree** ,是每个结点不超过2的有序**树（****tree****）** 。 

简单的理解，就是一种类似于我们生活中树的结构，只不过每个结点上都最多只能有两个子结点。二叉树是每个节点最多有两个子树的树结构。顶上的叫根结点，两边被称作“左子树”和“右子树”。 

如图： 

![二叉树](https://img-blog.csdnimg.cn/20210304083336536.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzUyNTk2MjU4,size_16,color_FFFFFF,t_70#pic_center)


我们要说的是二叉树的一种比较有意思的叫做**红黑树**，红黑树本身就是一颗二叉查找树，将节点插入后，该树仍然 是一颗二叉查找树。也就意味着，树的键值仍然是有序的。 

**红黑树的约束:** 

1. 节点可以是红色的或者黑色的 

2. 根节点是黑色的 

3. 叶子节点(特指空节点)是黑色的 

4. 每个红色节点的子节点都是黑色的 

5. 任何一个节点到其每一个叶子节点的所有路径上黑色节点数相同 

**红黑树的特点:** 

速度特别快,趋近平衡树,查找叶子元素最少和最多次数不多于二倍



# 第七章 List集合

我们掌握了Collection接口的使用后，再来看看Collection接口中的子类，他们都具备那些特性呢？接下来，我们一起学习Collection中的常用几个子类（ java.util.List 集合、 java.util.Set 集合）。

## 7.1 List接口介绍

List接口特点：

1. 它是一个元素存取有序的集合。例如，存元素的顺序是11、22、33。那么集合中，元素的存储就是按照11、22、33的顺序完成的）。
2. 它是一个带有索引的集合，通过索引就可以精确的操作集合中的元素（与数组的索引是一个道理）。
3. 集合中可以有重复的元素，通过元素的equals方法，来比较是否为重复的元素。

`tips:我们在基础班的时候已经学习过List接口的子类java.util.ArrayList类，该类中的方法都是来自List中定`
`义。`

## 7.2 List接口中常用方法

List作为Collection集合的子接口，不但继承了Collection接口中的全部方法，而且还增加了一些根据元素索引来操作集合的特有方法，

如下：

- public void add(int index, E element) : 将指定的元素，添加到该集合中的指定位置上。
- public E get(int index) :返回集合中指定位置的元素。
- public E remove(int index) : 移除列表中指定位置的元素, 返回的是被移除的元素。
- public E set(int index, E element) :用指定元素替换集合中指定位置的元素,返回值的更新前的元素。

List集合特有的方法都是跟索引相关，我们在基础班都学习过，那么我们再来复习一遍吧：  

```java
public class ListDemo {
  public static void main(String[] args) {
      // 创建List集合对象
      List<String> list = new ArrayList<String>();
      // 往 尾部添加 指定元素
      list.add("图图");
      list.add("小美");
      list.add("不高兴");
      System.out.println(list);
      // add(int index,String s) 往指定位置添加
      list.add(1,"没头脑");
      System.out.println(list);
      // String remove(int index) 删除指定位置元素 返回被删除元素
      // 删除索引位置为2的元素
      System.out.println("删除索引位置为2的元素");
      System.out.println(list.remove(2));
      System.out.println(list);
      // String set(int index,String s)
      // 在指定位置 进行 元素替代（改）
      // 修改指定位置元素
      list.set(0, "三毛");
      System.out.println(list);
      // String get(int index) 获取指定位置元素
      // 跟size() 方法一起用 来 遍历的
      for(int i = 0;i<list.size();i++){
      System.out.println(list.get(i));
      } 
      //还可以使用增强for
      for (String string : list) {
          System.out.println(string);
      }
  }
}
```

# 

## 7.3 ArrayList集合

java.util.ArrayList 集合数据存储的结构是数组结构。元素增删慢，查找快，由于日常开发中使用最多的功能为查询数据、遍历数据，所以 ArrayList 是最常用的集合。

许多程序员开发时非常随意地使用ArrayList完成任何需求，并不严谨，这种用法是不提倡的。

## 7.4 LinkedList集合

java.util.LinkedList 集合数据存储的结构是链表结构。方便元素添加、删除的集合。
LinkedList是一个双向链表，那么双向链表是什么样子的呢，我们用个图了解下  

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210304083729857.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzUyNTk2MjU4,size_16,color_FFFFFF,t_70#pic_center)


实际开发中对一个集合元素的添加与删除经常涉及到首尾操作，而LinkedList提供了大量首尾操作的方法。这些方法我们作为了解即可：

- public void addFirst(E e) :将指定元素插入此列表的开头。
- public void addLast(E e) :将指定元素添加到此列表的结尾。
- public E getFirst() :返回此列表的第一个元素。
- public E getLast() :返回此列表的最后一个元素。
- public E removeFirst() :移除并返回此列表的第一个元素。
- public E removeLast() :移除并返回此列表的最后一个元素。
- public E pop() :从此列表所表示的堆栈处弹出一个元素。
- public void push(E e) :将元素推入此列表所表示的堆栈。
- public boolean isEmpty() ：如果列表不包含元素，则返回true。  

LinkedList是List的子类，List中的方法LinkedList都是可以使用，这里就不做详细介绍，我们只需要了解LinkedList的特有方法即可。在开发时，LinkedList集合也可以作为堆栈，队列的结构使用。（了解即可）
方法演示：  

```java
public class LinkedListDemo {
    public static void main(String[] args) {
        LinkedList<String> link = new LinkedList<String>();
        //添加元素
        link.addFirst("abc1");
        link.addFirst("abc2");
        link.addFirst("abc3");
        System.out.println(link);
        // 获取元素
        System.out.println(link.getFirst());
        System.out.println(link.getLast());
        // 删除元素
        System.out.println(link.removeFirst());
        System.out.println(link.removeLast());
        while (!link.isEmpty()) { //判断集合是否为空
        		System.out.println(link.pop()); //弹出集合中的栈顶元素
        } 
        System.out.println(link);
    }
}
```



# 第八章 Set接口

java.util.Set 接口和 java.util.List 接口一样，同样继承自 Collection 接口，它与 Collection 接口中的方法基本一致，并没有对 Collection 接口进行功能上的扩充，只是比 Collection 接口更加严格了。与 List 接口不同的是， Set 接口中元素无序，并且都会以某种规则保证存入的元素不出现重复。

Set 集合有多个子类，这里我们介绍其中的 java.util.HashSet 、 java.util.LinkedHashSet 这两个集合。
`tips:Set集合取出元素的方式可以采用：迭代器、增强for。`

## 8.1 HashSet集合介绍

java.util.HashSet 是 Set 接口的一个实现类，它所存储的元素是不可重复的，并且元素都是无序的(即存取顺序
不一致)。 java.util.HashSet 底层的实现其实是一个 java.util.HashMap 支持，由于我们暂时还未学习，先做了
解。

HashSet 是根据对象的哈希值来确定元素在集合中的存储位置，因此具有良好的存取和查找性能。保证元素唯一性
的方式依赖于： hashCode 与 equals 方法。

我们先来使用一下Set集合存储，看下现象，再进行原理的讲解:  

```java
public class HashSetDemo {
    public static void main(String[] args) {
        //创建 Set集合
        HashSet<String> set = new HashSet<String>();
        //添加元素
        set.add(new String("cba"));
        set.add("abc");
        set.add("bac");
        set.add("cba");
        //遍历
        for (String name : set) {
        		System.out.println(name);
        }
    }
}
```

输出结果如下，说明集合中不能存储重复元素：  

```java
cba
abc
bac
```

`tips:根据结果我们发现字符串"cba"只存储了一个，也就是说重复的元素set集合不存储。`

## 8.2 HashSet集合存储数据的结构（哈希表）

**什么是哈希表呢？**
在**JDK1.8**之前，哈希表底层采用数组+链表实现，即使用链表处理冲突，同一hash值的链表都存储在一个链表里。
但是当位于一个桶中的元素较多，即hash值相等的元素较多时，通过key值依次查找的效率较低。而JDK1.8中，哈
希表存储采用数组+链表+红黑树实现，当链表长度超过阈值（8）时，将链表转换为红黑树，这样大大减少了查找
时间。

简单的来说，哈希表是由数组+链表+红黑树（JDK1.8增加了红黑树部分）实现的，如下图所示。  


![](https://files.mdnice.com/user/34144/1481a520-e0f5-4494-80f0-15991286a55d.png)


看到这张图就有人要问了，这个是怎么存储的呢？
为了方便大家的理解我们结合一个存储流程图来说明一下：  


![](https://files.mdnice.com/user/34144/c43292a9-c249-47f0-a61c-4a905a6e461b.png)


总而言之，JDK1.8引入红黑树大程度优化了HashMap的性能，那么对于我们来讲保证HashSet集合元素的唯一，
其实就是根据对象的hashCode和equals方法来决定的。如果我们往集合中存放自定义的对象，那么保证其唯一，
就必须复写hashCode和equals方法建立属于当前对象的比较方式。

## 8.3 HashSet存储自定义类型元素

**给HashSet中存放自定义类型元素时，需要重写对象中的hashCode和equals方法，建立自己的比较方式，才能保
证HashSet集合中的对象唯一

创建自定义Student类  

```java
public class Student {
    private String name;
    private int age;
  
    public Student() {
    } 
  	public Student(String name, int age) {
      this.name = name;
      this.age = age;
    } 
    public String getName() {
      return name;
      } 
    public void setName(String name) {
      this.name = name;
      } 
    public int getAge() {
      return age;
      } 
    public void setAge(int age) {
      this.age = age;
      } 
  
    @Override
    public boolean equals(Object o) {
        if (this == o)
        		return true;
        if (o == null || getClass() != o.getClass())
        		return false;
        Student student = (Student) o;
        
      	return age == student.age && Objects.equals(name, student.name);
    } 
  
  	@Override
    public int hashCode() {
    		return Objects.hash(name, age);
    }
}  
```

```java
public class HashSetDemo2 {
        public static void main(String[] args) {
            //创建集合对象 该集合中存储 Student类型对象
            HashSet<Student> stuSet = new HashSet<Student>();
            //存储
            Student stu = new Student("于谦", 43);
            stuSet.add(stu);
            stuSet.add(new Student("郭德纲", 44));
            stuSet.add(new Student("于谦", 43));
            stuSet.add(new Student("郭麒麟", 23));
            stuSet.add(stu);
            for (Student stu2 : stuSet) {
              System.out.println(stu2);
            }
        }
} 
```

执行结果：

```java
Student [name=郭德纲, age=44]
Student [name=于谦, age=43]
Student [name=郭麒麟, age=23]
```

## 8.4 linkedHashSet

我们知道HashSet保证元素唯一，可是元素存放进去是没有顺序的，那么我们要保证有序，怎么办呢？
在HashSet下面有一个子类 java.util.LinkedHashSet ，它是链表和哈希表组合的一个数据存储结构。
演示代码如下:  

```java
public class LinkedHashSetDemo {
    public static void main(String[] args) {
        Set<String> set = new LinkedHashSet<String>();
        set.add("bbb");
        set.add("aaa");
        set.add("abc");
        set.add("bbc");
        Iterator<String> it = set.iterator();
        while (it.hasNext()) {
        		System.out.println(it.next());
        }
    }
} 

结果：
  bbb
  aaa
  abc
  bbc
```

## 8.5 可变参数

在JDK1.5之后，如果我们定义一个方法需要接受多个参数，并且多个参数类型一致，我们可以对其简化成如下格
式：

```java
修饰符 返回值类型 方法名(参数类型... 形参名){ }
```

其实这个书写完全等价与

```java
修饰符 返回值类型 方法名(参数类型[] 形参名){ }
```

只是后面这种定义，在调用时必须传递数组，而前者可以直接传递数据即可。
JDK1.5以后。出现了简化操作。... 用在参数上，称之为可变参数。  

同样是代表数组，但是在调用这个带有可变参数的方法时，不用创建数组(这就是简单之处)，直接将数组中的元素作为实际参数进行传递，其实编译成的class文件，将这些元素先封装到一个数组中，在进行传递。这些动作都在编译.class文件时，自动完成了。
代码演示：  

```java
public class ChangeArgs {
    public static void main(String[] args) {
        int[] arr = { 1, 4, 62, 431, 2 };
        int sum = getSum(arr);
        System.out.println(sum);
        // 6 7 2 12 2121
        // 求 这几个元素和 6 7 2 12 2121
        int sum2 = getSum(6, 7, 2, 12, 2121);
        		System.out.println(sum2);
     } 
  			/**
        完成数组 所有元素的求和 原始写法
        public static int getSum(int[] arr){
        int sum = 0;
        for(int a : arr){
        sum += a;
        } r
        eturn sum;
        }
        */
        //可变参数写法
        public static int getSum(int... arr) {
          int sum = 0;
          for (int a : arr) {
          sum += a;
       		} 
          return sum;
    		}
}
```

``tips: 上述add方法在同一个类中，只能存在一个。因为会发生调用的不确定性`
`注意：如果在方法书写时，这个方法拥有多参数，参数中包含可变参数，可变参数一定要写在参数列表的末`
`尾位置`。`



## 8.6 常用功能

- java.utils.Collections 是集合工具类，用来对集合进行操作。部分方法如下：  

- public static <T> boolean addAll(Collection<T> c, T... elements) :往集合中添加一些元素。

- public static void shuffle(List<?> list) 打乱顺序 :打乱集合顺序。

- public static <T> void sort(List<T> list) :将集合中元素按照默认规则排序。

- public static <T> void sort(List<T> list，Comparator<? super T> ) :将集合中元素按照指定规则排

  序。

  **代码演示：**  

```java
public class CollectionsDemo {
    public static void main(String[] args) {
      ArrayList<Integer> list = new ArrayList<Integer>();
      //原来写法
      //list.add(12);
      //list.add(14);
      //list.add(15);
      //list.add(1000);
      //采用工具类 完成 往集合中添加元素
      Collections.addAll(list, 5, 222, 1，2);
      System.out.println(list);
      //排序方法
      Collections.sort(list);
      System.out.println(list);
    }
} 
结果：
[5, 222, 1, 2]
[1, 2, 5, 222]
```

代码演示之后 ，发现我们的集合按照顺序进行了排列，可是这样的顺序是采用默认的顺序，如果想要指定顺序那该
怎么办呢？

我们发现还有个方法没有讲， public static <T> void sort(List<T> list，Comparator<? super T> ) :将集合中
元素按照指定规则排序。接下来讲解一下指定规则的排列。

## 8.7 Comparator比较器

我们还是先研究这个方法
public static <T> void sort(List<T> list) :将集合中元素按照默认规则排序。
不过这次存储的是字符串类型。  

```java
public class CollectionsDemo2 {
    public static void main(String[] args) {
      ArrayList<String> list = new ArrayList<String>();
      list.add("cba");
      list.add("aba");
      list.add("sba");
      list.add("nba");
      //排序方法
      Collections.sort(list);
      System.out.println(list);
    }
}
```

结果：

```java
[aba, cba, nba, sba]
```

我们使用的是默认的规则完成字符串的排序，那么默认规则是怎么定义出来的呢？

说到排序了，简单的说就是两个对象之间比较大小，那么在JAVA中提供了两种比较实现的方式，一种是比较死板的
采用 java.lang.Comparable 接口去实现，一种是灵活的当我需要做排序的时候在去选择的java.util.Comparator 接口完成。

那么我们采用的 public static <T> void sort(List<T> list) 这个方法完成的排序，实际上要求了被排序的类型
需要实现Comparable接口完成比较的功能，在String类型上如下：  

```java
public final class String implements java.io.Serializable,Comparable<String>,CharSequence {
```

String类实现了这个接口，并完成了比较规则的定义，但是这样就把这种规则写死了，那比如我想要字符串按照第一个字符降序排列，那么这样就要修改String的源代码，这是不可能的了，那么这个时候我们可以使用public static <T> void sort(List<T> list，Comparator<? super T> ) 方法灵活的完成，这个里面就涉及到了Comparator这个接口，位于位java.util包下，排序是comparator能实现的功能之一,该接口代表一个比较器，比较器具有可比性！顾名思义就是做排序的，通俗地讲需要比较两个对象谁排在前谁排在后，那么比较的方法就是：

- public int compare(String o1, String o2) ：比较其两个参数的顺序。

`两个对象比较的结果有三种：大于，等于，小于。`
`如果要按照升序排序， 则o1 小于o2，返回（负数），相等返回0，01大于02返回（正数） 如果要按照`
`降序排序 则o1 小于o2，返回（正数），相等返回0，01大于02返回（负数）`

操作如下:  

```java
public class CollectionsDemo3 {
  public static void main(String[] args) {
    ArrayList<String> list = new ArrayList<String>();
    list.add("cba");
    list.add("aba");
    list.add("sba");
    list.add("nba");
    //排序方法 按照第一个单词的降序
    Collections.sort(list, new Comparator<String>() {
        @Override
        public int compare(String o1, String o2) {
            return o2.charAt(0) ‐ o1.charAt(0);
        }
    });
    System.out.println(list);
  }
}
```

结果如下：

```java
[sba, nba, cba, aba]
```

## 8.8 简述Comparable和Comparator两个接口的区别。

**Comparable**：强行对实现它的每个类的对象进行整体排序。这种排序被称为类的自然排序，类的compareTo方法
被称为它的自然比较方法。只能在类中实现compareTo()一次，不能经常修改类的代码实现自己想要的排序。实现
此接口的对象列表（和数组）可以通过Collections.sort（和Arrays.sort）进行自动排序，对象可以用作有序映射中
的键或有序集合中的元素，无需指定比较器。

**Comparator**：强行对某个对象进行整体排序。可以将Comparator 传递给sort方法（如Collections.sort或
Arrays.sort），从而允许在排序顺序上实现精确控制。还可以使用Comparator来控制某些数据结构（如有序set或
有序映射）的顺序，或者为那些没有自然顺序的对象collection提供排序。

## 8.9 练习

创建一个学生类，存储到ArrayList集合中完成指定排序操作。
Student 初始类  

```java
public class Student{
    private String name;
    private int age;
    public Student() {
    } 
    public Student(String name, int age) {
      this.name = name;
      this.age = age;
      } 
    public String getName() {
      return name;
      } 
    public void setName(String name) {
      this.name = name;
      } 
    public int getAge() {
      return age;
      } 
    public void setAge(int age) {
      this.age = age;
      } 
    @Override
    public String toString() {
      return "Student{" +
      "name='" + name + '\'' +
      ", age=" + age +
      '}';
    }
}
```

测试类：

```java
public class Demo {
  public static void main(String[] args) {
    // 创建四个学生对象 存储到集合中
    ArrayList<Student> list = new ArrayList<Student>();
    list.add(new Student("rose",18));
    list.add(new Student("jack",16));
    list.add(new Student("abc",16));
    list.add(new Student("ace",17));
    list.add(new Student("mark",16));
    /*
    让学生 按照年龄排序 升序
    */
    // Collections.sort(list);//要求 该list中元素类型 必须实现比较器Comparable接口
    for (Student student : list) {
    	System.out.println(student);
    }
  }
}
```

发现，当我们调用Collections.sort()方法的时候 程序报错了。
原因：如果想要集合中的元素完成排序，那么必须要实现比较器Comparable接口。
于是我们就完成了Student类的一个实现，如下： 

```java
public class Student implements Comparable<Student>{
  ....
  @Override
  public int compareTo(Student o) {
  	return this.age‐o.age;//升序
  }
}
```

 再次测试，代码就ok了：

```java
Student{name='jack', age=16}
Student{name='abc', age=16}
Student{name='mark', age=16}
Student{name='ace', age=17}
Student{name='rose', age=18}
```

## 8.10 扩展

如果在使用的时候，想要独立的定义规则去使用 可以采用Collections.sort(List list,Comparetor c)方式，自己定义
规则：  

```java
Collections.sort(list, new Comparator<Student>() {
  @Override
  public int compare(Student o1, Student o2) {
 		 return o2.getAge()‐o1.getAge();//以学生的年龄降序
  }
});
```

效果：

```java
Student{name='rose', age=18}
Student{name='ace', age=17}
Student{name='jack', age=16}
Student{name='abc', age=16}
Student{name='mark', age=16}
```

如果想要规则更多一些，可以参考下面代码：  

```java
Collections.sort(list, new Comparator<Student>() {
  @Override
  public int compare(Student o1, Student o2) {
    // 年龄降序
    int result = o2.getAge()‐o1.getAge();//年龄降序
    if(result==0){
      //第一个规则判断完了 下一个规则 姓名的首字母 升序
    result = o1.getName().charAt(0)‐o2.getName().charAt(0);
    } 
    return result;
  }
});
```

效果如下：

```java
Student{name='rose', age=18}
Student{name='ace', age=17}
Student{name='abc', age=16}
Student{name='jack', age=16}
Student{name='mark', age=16}
```

# 第九章 Map集合

## 9.1 概述

现实生活中，我们常会看到这样的一种集合：IP地址与主机名，身份证号与个人，系统用户名与系统用户对象等，这种一一对应的关系，就叫做映射。Java提供了专门的集合类用来存放这种对象关系的对象，即 java.util.Map 接口。

我们通过查看 Map 接口描述，发现 Map 接口下的集合与 Collection 接口下的集合，它们存储数据的形式不同，如下图。
![Map接口和Collection接口存储形式对比](https://img-blog.csdnimg.cn/20210304202051981.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzUyNTk2MjU4,size_16,color_FFFFFF,t_70#pic_center)

 - Collection 中的集合(单列集合)，元素是孤立存在的（理解为单身），向集合中存储元素采用一个个元素的方式存储。
 - Map 中的集合(双列集合)，元素是成对存在的(理解为夫妻)。每个元素由键与值两部分组成，通过键可以找对所对应的值。
 - Collection 中的集合称为单列集合， Map 中的集合称为双列集合。
 - 需要注意的是， Map 中的集合不能包含重复的键，值可以重复；每个键只能对应一个值。

## 9.2 Map 常用子类

通过查看Map接口描述，看到Map有多个子类，这里我们主要讲解常用的HashMap集合、LinkedHashMap集合。

 - **HashMap**：存储数据采用的哈希表结构，元素的存取顺序不能保证一致。由于要保证键的唯一、不重复，需要重写键的hashCode()方法、equals()方法。
 - **LinkedHashMap**：HashMap下有个子类LinkedHashMap，存储数据采用的哈希表结构+链表结构。通过链表结构可以保证元素的存取顺序一致；通过哈希表结构可以保证的键的唯一、不重复，需要重写键的hashCode()方法、equals()方法。

> tips：Map接口中的集合都有两个泛型变量,在使用时，要为两个泛型变量赋予数据类型。两个泛型变量的数

据类型可以相同，也可以不同。

## 9.3 Map 接口中的常用方法

Map接口中定义了很多方法，常用的如下：

 - public V put(K key, V value) : 把指定的键与指定的值添加到Map集合中。 
 - public V remove(Object key) : 把指定的键 所对应的键值对元素 在Map集合中删除，返回被删除元素的值。 
 - public V get(Object key) 根据指定的键，在Map集合中获取对应的值。 
 - public Set<K> keySet() :获取Map集合中所有的键，存储到Set集合中。 
 - public Set<Map.Entry<K,V>> entrySet() :获取到Map集合中所有的键值对对象的集合(Set集合)。

Map 接口的方法演示：

```java
public class MapDemo {
    public static void main(String[] args) {
        //创建 map对象
        HashMap<String, String>  map = new HashMap<String, String>();
        //添加元素到集合
        map.put("黄晓明", "杨颖");
        map.put("文章", "马伊琍");
        map.put("邓超", "孙俪");
        System.out.println(map);
        //String remove(String key)
        System.out.println(map.remove("邓超"));
        System.out.println(map);
        // 想要查看 黄晓明的媳妇 是谁
        System.out.println(map.get("黄晓明"));
        System.out.println(map.get("邓超"));   
    }
}
```

运行结果：

```java
{邓超=孙俪, 文章=马伊琍, 黄晓明=杨颖}
孙俪
{文章=马伊琍, 黄晓明=杨颖}
杨颖
null
```

> tips:
> 使用put方法时，若指定的键(key)在集合中没有，则没有这个键对应的值，返回null，并把指定的键值添加到集合中；
> 若指定的键(key)在集合中存在，则返回值为集合中键对应的值（该值为替换前的值），并把指定键所对应的值，替换成指定的新值。

## 9.4 Map 集合遍历键找值方式

键找值方式：即通过元素中的键，获取键所对应的值
分析步骤：

1. 获取Map中所有的键，由于键是唯一的，所以返回一个Set集合存储所有的键。方法提示: keyset()
2. 遍历键的Set集合，得到每一个键。
3. 根据键，获取键所对应的值。方法提示: get(K key)

代码演示：

```java
public class MapDemo01 {
    public static void main(String[] args) {
        //创建Map集合对象
        HashMap<String, String> map = new HashMap<String,String>();
        //添加元素到集合
        map.put("胡歌", "霍建华");
        map.put("郭德纲", "于谦");
        map.put("薛之谦", "大张伟");
        //获取所有的键  获取键集
        Set<String> keys = map.keySet();
        // 遍历键集 得到 每一个键
        for (String key : keys) {
           //key  就是键  
            //获取对应值
            String value = map.get(key);
            System.out.println(key+"的CP是："+value);
        } 
    }
}
```

运行结果：

```java
郭德纲的CP是：于谦
薛之谦的CP是：大张伟
胡歌的CP是：霍建华
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210304204225192.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzUyNTk2MjU4,size_16,color_FFFFFF,t_70#pic_center)

## 9.5 Entry 键值对对象

我们已经知道， Map 中存放的是两种对象，一种称为**key**(键)，一种称为**value**(值)，它们在 Map 中是一一对应关系，这一对对象又称做 Map 中的一个 Entry( 项) 。 Entry 将键值对的对应关系封装成了对象。即键值对对象，这样我们在遍历 Map 集合时，就可以从每一个键值对（ Entry ）对象中获取对应的键与对应的值。

既然Entry表示了一对键和值，那么也同样提供了获取对应键和对应值得方法：

 - public K getKey() ：获取Entry对象中的键。 
 - public V getValue() ：获取Entry对象中的值。

在Map集合中也提供了获取所有Entry对象的方法：

 - public Set<Map.Entry<K,V>> entrySet() : 获取到Map集合中所有的键值对对象的集合(Set集合)。

## 9.6 Map 集合遍历键值对方式

键值对方式：即通过集合中每个键值对(Entry)对象，获取键值对(Entry)对象中的键与值。
操作步骤与图解：

1. 获取Map集合中，所有的键值对(Entry)对象，以Set集合形式返回。方法提示: entrySet() 。
2. 遍历包含键值对(Entry)对象的Set集合，得到每一个键值对(Entry)对象。
3. 通过键值对(Entry)对象，获取Entry对象中的键与值。 方法提示: getkey() getValue()。

```java
public class MapDemo02 {
    public static void main(String[] args) {
        // 创建Map集合对象
        HashMap<String, String> map = new HashMap<String,String>();
        // 添加元素到集合
        map.put("胡歌", "霍建华");
        map.put("郭德纲", "于谦");
        map.put("薛之谦", "大张伟");
        // 获取 所有的 entry对象  entrySet
        Set<Map.Entry<String,String>> entrySet = map.entrySet();
        // 遍历得到每一个entry对象
        for (Map.Entry<String, String> entry : entrySet) {
           // 解析  
            String key = entry.getKey();
            String value = entry.getValue(); 
            System.out.println(key+"的CP是:"+value);
        }
    }
}
```

运行结果：

```java
郭德纲的CP是：于谦
薛之谦的CP是：赵英俊
胡歌的CP是：霍建华
```

遍历图解：
![Map过程](https://img-blog.csdnimg.cn/20210304204956888.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzUyNTk2MjU4,size_16,color_FFFFFF,t_70#pic_center)

> tips：Map集合不能直接使用迭代器或者foreach进行遍历。但是转成Set之后就可以使用了。

## 9.7 HashMap 存储自定义类型键值

练习：每位学生（姓名，年龄）都有自己的家庭住址。那么，既然有对应关系，则将学生对象和家庭住址存储到map集合中。学生作为键, 家庭住址作为值。

> 注意，学生姓名相同并且年龄相同视为同一名学生。

编写学生类：

```java
public class Student {
		private String name;
	    private int age;
	    public Student() {
	    }
	    public Student(String name, int age) {
	        this.name = name;
	        this.age = age;
	    }
	    public String getName() {
	        return name;
	    }
	    public void setName(String name) {
	        this.name = name;
	    }
	    public int getAge() {
	        return age;
	    }
	    public void setAge(int age) {
	        this.age = age;
	    }
	    @Override
	    public boolean equals(Object o) {
	        if (this == o)
	            return true;
	        if (o == null || getClass() != o.getClass())
	            return false;
	        Student student = (Student) o;
	        return age == student.age && Objects.equals(name, student.name);
	    }
	    @Override
	    public int hashCode() {
	        return Objects.hash(name, age);
	    }
}
```

编写测试类：

```java
public class HashMapTest {
    public static void main(String[] args) {
        //1,创建Hashmap集合对象。
        Map<Student,String>map = new HashMap<Student,String>();
        //2,添加元素。
        map.put(new Student("lisi",28), "上海");
        map.put(new Student("wangwu",22), "北京");
        map.put(new Student("zhaoliu",24), "成都");
        map.put(new Student("zhouqi",25), "广州");
        map.put(new Student("wangwu",22), "南京");
       
        //3,取出元素。键找值方式
        Set<Student>keySet = map.keySet();
        for(Student key: keySet){
            String value = map.get(key);
            System.out.println(key.toString()+"....."+value);
        }
    }
}
```

运行结果：

```java
Student{name='lisi', age=28}.....上海
Student{name='wangwu', age=22}.....北京
Student{name='zhouqi', age=25}.....广州
Student{name='wangwu', age=22}.....南京
Student{name='zhaoliu', age=24}.....成都
```

 - 当给HashMap中存放自定义对象时，如果自定义对象作为key存在，这时要保证对象唯一，必须复写对象的hashCode和equals方法(如果忘记，请回顾HashSet存放自定义对象)。
 - 如果要保证 map中存放的key和取出的顺序一致，可以使用 java.util.LinkedHashMap 集合来存放。

## 9.8 LinkedHashMap

我们知道HashMap保证成对元素唯一，并且查询速度很快，可是成对元素存放进去是没有顺序的，那么我们要保证有序，还要速度快怎么办呢？

在HashMap下面有一个子类LinkedHashMap，它是链表和哈希表组合的一个数据存储结构。

```java
public class LinkedHashMapDemo {
    public static void main(String[] args) {
        LinkedHashMap<String, String> map = new LinkedHashMap<String, String>();
        map.put("邓超", "孙俪");
        map.put("李晨", "范冰冰");
        map.put("刘德华", "朱丽倩");
        Set<Map.Entry<String, String>> entrySet = map.entrySet();
        for (Map.Entry<String, String> entry : entrySet) {
            System.out.println(entry.getKey() + "  " + entry.getValue());
        }
    }
}
```

运行结果：

```java
邓超  孙俪
李晨  范冰冰
刘德华  朱丽倩
```

## 9.9 Map 集合练习

#### 需求：

计算一个字符串中每个字符出现次数。

#### 分析：

1. 获取一个字符串对象
2. 创建一个Map集合，键代表字符，值代表次数。
3. 遍历字符串得到每个字符。
4. 判断Map中是否有该键。
5. 如果没有，第一次出现，存储次数为1；如果有，则说明已经出现过，获取到对应的值进行++，再次存储。
6. 打印最终结果

代码：

```java
public class MapTest {
	public static void main(String[] args) {
        //友情提示
        System.out.println("请录入一个字符串:");
        Scanner sc = new Scanner(System.in);
        String line = sc.nextLine();
        // 定义 每个字符出现次数的方法
        findChar(line);
    }
    private static void findChar(String line) {
        //1:创建一个集合 存储  字符 以及其出现的次数
        HashMap<Character, Integer> map = new HashMap<Character, Integer>();
        //2:遍历字符串
        for (int i = 0; i < line.length(); i++) {
            char c = line.charAt(i);
            //判断 该字符 是否在键集中
            if (!map.containsKey(c)) {//说明这个字符没有出现过
                //那就是第一次
                map.put(c, 1);
            } else {
                //先获取之前的次数
                Integer count = map.get(c);
                //count++;
                //再次存入  更新
                map.put(c, ++count);
            }
        }
        System.out.println(map);
    }
}
```

测试结果：

```java
请录入一个字符串:
zhangsan
{z=1, h=1, a=2, n=2, g=1, s=1}
```

# 第十章、异常

## 10.1 异常概念

- 异常 ：指的是程序在执行过程中，出现的非正常的情况，最终会导致JVM的非正常停止。 

在Java等面向对象的编程语言中，异常本身是一个类，产生异常就是创建异常对象并抛出了一个异常对象。Java处理异常的方式是中断处理。

>注：异常指的并不是语法错误,语法错了,编译不通过,不会产生字节码文件,根本不能运行。

## 10.2 异常体系

- 异常机制：其实是帮助我们找到程序中的问题，异常的根类是 java.lang.Throwable ，其下有两个子类： java.lang.Error 与 java.lang.Exception ，平常所说的异常指 java.lang.Exception 。
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20210305151037157.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzUwOTk0MjM1,size_16,color_FFFFFF,t_70)
- Throwable体系：

1. Error:严重错误Error，无法通过处理的错误，只能事先避免。好比绝症。 
2. Exception:表示异常，异常产生后程序员可以通过代码的方式纠正，使程序继续运行，是必须要处理的。好比感冒、阑尾炎。

- Throwable中的常用方法：

1. public void printStackTrace() :打印异常的详细信息。包含了异常的类型,异常的原因,还包括异常出现的位置,在开发和调试阶段,都得使用printStackTrace。 

2. public String getMessage() :获取发生异常的原因。提示给用户的时候,就提示错误原因。 

3. public String toString() :获取异常的类型和异常描述信息(不用)。

   ```java
   public class exception {
       public static void main(String[] args) {
           int[] arr = {1,2,3};
           try {
               System.out.println(arr[3]);
           }catch (Exception ex){
               /**
                * （数组下标越界实例）
                * java.lang.ArrayIndexOutOfBoundsException: 3
                * at com.wbs.advance05.ThrowableDemo1.main(ThrowableDemo1.java:7)
                */
               ex.printStackTrace();
               System.out.println(ex.getMessage());//3
           }
       }
   }
   ```

## 10.3 异常分类

- **编译时期异常:checked异常**。在编译时期,就会检查,如果没有处理异常,则编译失败。(如日期格式化异常) 。
- **运行时期异常:runtime异常**。在运行时期,检查异常；在编译时期,运行异常不会被编译器检测到(不报错)。(如数学异常)。
  ![Throwable体系](https://img-blog.csdnimg.cn/20210305152941863.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzUwOTk0MjM1,size_16,color_FFFFFF,t_70)

## 10.4 异常的产生过程解析

```java
public class ThrowableDemo2 {
    public static void main(String[] args) {
        int[] arr = {11,2,3};
        ThrowableDemo2 t = new ThrowableDemo2();
      	/**
      	*Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: 3
				*at com.wbs.advance05.ThrowableDemo2.getElement(ThrowableDemo2.java:13)
				*at com.wbs.advance05.ThrowableDemo2.main(ThrowableDemo2.java:7)
      	*/
        int intNum = t.getElement(arr,3);
        System.out.println("num:" + intNum);
        System.out.println("over");
    }

    public int getElement(int[] arr,int index){
        int elment = arr[index];
        return elment;
    }
}
```

![异常产生流程](https://img-blog.csdnimg.cn/20210305153212204.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzUwOTk0MjM1,size_16,color_FFFFFF,t_70)

## 10.5 异常的处理

**Java异常处理的五个关键字：try、catch、ﬁnally、throw、throws** 

- 抛出异常throw

  在编写程序时，我们必须要考虑程序出现问题的情况。比如，在定义方法时，方法需要接收参数。那么，当调用方 法使用接收到的参数时，首先需要先对参数数据进行合法的判断，数据若不合法，就应该告诉调用者，传递合法的 数据进来。这时需要使用抛出异常的方式来告诉调用者。

  在java中，提供了一个throw关键字，它用来抛出一个指定的异常对象。那么，抛出一个异常具体如何操作呢？

1. 创建一个异常对象。封装一些提示信息(信息可以自己编写)。 

2. 需要将这个异常对象告知给调用者。（怎么告知呢？怎么将这个异常对象传递到调用者处呢？通过关键字throw 就可以完成。throw 异常对象。） 

   **throw用在方法内，用来抛出一个异常对象，将这个异常对象传递到调用者处，并结束当前方法的执行。**

   抛出异常使用格式：


   ```java
   throw new 异常类名(参数);
   例如：
   throw new NullPointerException("要访问的arr数组不存在（空指针异常）");   
   throw new ArrayIndexOutOfBoundsException("该索引在数组中不存在，已超出范围（数组下标越界异常）");
   ```

   ```java
   public class throwDemo {
       public static void main(String[] args) {
           int[] arr = {11,22,330};
           int index = 4;
           int element = getElement(arr,index);
           /**
            *  Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: 数组下标越界！
            * 	at com.wbs.Throwable.throwDemo.getElement(throwDemo.java:20)
            * 	at com.wbs.Throwable.throwDemo.main(throwDemo.java:7)
            */
           System.out.println(element);
           System.out.println("over!");
       }
       /**
        * 根据索引找到数组中对应的元素
        */
       public static int getElement(int[] arr,int index){
           //判断索引是否越界
           if (index < 0 || index > arr.length - 1){
               /**
                *  判断条件如果满足，当执行完throw抛出异常对象后，方法已经无法继续运算。       
                *  这时就会结束当前方法的执行，并将异常告知给调用者。这时就需要通过异常来解决。 
                */
               throw new ArrayIndexOutOfBoundsException("数组下标越界！");
           }
           int element = arr[index];
           return element;
       }
   }
   ```

   >注意：如果产生了问题，我们就会通过throw将问题描述类即异常进行抛出，也就是将问题返回给该方法的调用者。

- Object非空判断

  类Objects，由一些静态的实用方法组成，这些方法是null-save（空指针安 全的）或null-tolerant（容忍空指针的），那么在它的源码中，对对象为null的值进行了抛出异常操作。 


  ```java
  public static <T> T requireNonNull(T obj) :查看指定引用对象不是null。
  ```

  ```java
  public static <T> T requireNonNull(T obj) {
          if (obj == null)
              throw new NullPointerException();
          return obj;
  }
  ```

- 声明异常throws

  声明异常：将问题标识出来，报告给调用者。如果方法内通过throw抛出了编译时异常，而没有捕获处理，那么必须通过throws进行声明，让调用者去处理。 

  关键字throws运用于方法声明之上,用于表示当前方法不处理异常,而是提醒该方法的调用者来处理异常(抛出异常).

  声明异常使用格式：


  ```java
  修饰符 返回值类型 方法名(参数) throws 异常类名1,异常类名2…{   }  
  ```

  ```java
  package com.wbs.advance05;
  
  public class ThrowableDemo2 {
      public static void main(String[] args) {
          int[] arr = {11,2,3};
          ThrowableDemo2 t = new ThrowableDemo2();
       /**
         *  Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: 数组下标越界！！！
         * 	at com.wbs.advance05.ThrowableDemo2.getElement(ThrowableDemo2.java:14)
         * 	at com.wbs.advance05.ThrowableDemo2.main(ThrowableDemo2.java:7)
         */
          int intNum = t.getElement(arr,3);
          System.out.println("num:" + intNum);
          System.out.println("over");
      }
  
   /**
     * 根据索引找到数组位置
     * 如果定义功能时有问题发生，需要报告给调用者，可以通过在方法上使用throws方法进行声明
     * @param arr
     * @param index
     * @return
     * @throws ArrayIndexOutOfBoundsException
     */
    public int getElement(int[] arr,int index) throws ArrayIndexOutOfBoundsException{
        //判断传递的索引是否越界
        if(index<0 || index>arr.length-1){
            /**
             * 如果索引越界，则会执行throw语句将异常抛出并返回给调用者，且方法终止，不再执行
             * 这时就需要通过来解决
             */
            throw new ArrayIndexOutOfBoundsException("数组下标越界！！！");
        }
        int elment = arr[index];
        return elment;
    }
}

>   
>   小贴士：
>   throws用于进行异常类的声明，若该方法可能有多种异常情况产生，那么在throws后面可以写多个异常类，用逗 号隔开。

- 捕获异常try…catch 

  如果异常出现的话,会立刻终止程序,所以我们得处理异常: 
  1. (throws声明语句)该方法不处理,而是将异常声明抛出,由该方法的调用者来处理。
  2. 在方法中使用try-catch的语句块来处理异常。

  try-catch的方式就是捕获异常。
捕获异常：Java中对异常有针对性的语句进行捕获，可以对出现的异常进行指定方式的处理。

 捕获异常的语法：

```java
  try{      
  	编写可能会出现异常的代码 
  }catch(异常类型  e){      
  	处理异常的代码      
  	/**
      *记录日志
      *打印异常信息
      *继续抛出异常 
      */
  }
```



```java
  public class tryCatchDemo {
      public static void main(String[] args) {
          /**
           * 当有异常产生时，必须处理，要么捕获要么声明
           */
          try {
              read("b.txt");
          } catch (FileNotFoundException e) {
              //try中抛出的是什么异常，在括号中就定义什么异常类型
              e.printStackTrace();
          }
          System.out.println("over!");
      }
  
      /**
       * 此方法中有编译时异常
       * @param path
       * @throws FileNotFoundException
       */
      public static void read(String path) throws FileNotFoundException {
          if (!path.equals("a.txt")){
              throw new FileNotFoundException("文件不存在！");
          }
      }
  }
```

  >注意：
  >try和catch都不能单独使用,必须连用。

- ﬁnally代码块

  ﬁnally：有一些特定的代码无论异常是否发生，都需要执行。另外，因为异常会引发程序跳转，导致有些语句执行不到。而ﬁnally就是解决这个问题的，在ﬁnally代码块中存放的代码都是一定会被执行的。

  什么时候的代码必须终执行？

  当我们在try语句块中打开了一些物理资源(磁盘文件/网络连接/数据库连接等),我们都得在使用完之后,最终关闭打开的资源。

  ﬁnally的语法: 


  ```java
  try{      
  	编写可能会出现异常的代码 
  }catch(异常类型  e){      
  	处理异常的代码      
  	//记录日志/打印异常信息/继续抛出异常 
  }finally{
    //finally语句
  }
  ```

  ```java
  public class trycatchFinallyDemo {
      public static void main(String[] args) {
          /**
           * 当有异常产生时，必须处理，要么捕获要么声明
           */
          try {
              read("b.txt");
          } catch (FileNotFoundException e) {
              //抓取到的是编译期异常  抛出去的是运行期  
              e.printStackTrace();
          }finally {
              System.out.println("无论程序啥样，这里的代码都会执行！");
          }
          System.out.println("over!");
      }
  
      /**
       * 此方法中有编译时异常
       * @param path
       * @throws FileNotFoundException
       */
      public static void read(String path) throws FileNotFoundException {
          if (!path.equals("a.txt")){
              throw new FileNotFoundException("文件不存在！");
          }
      }
  }
  ```

  >注意：
  >
  >1. try...catch....ﬁnally:自身需要处理异常,终还得关闭资源。
  >2. 当只有在try或者catch中调用退出JVM的相关方法,此时ﬁnally才不会执行,否则ﬁnally永远会执行。
  >3. finally不能单独使用。

## 10.6 异常的注意事项

- 多个异常使用捕获又该如何处理呢？ 

1. 多个异常分别处理。 
2. 多个异常一次捕获，多次处理。 
3. 多个异常一次捕获一次处理。 
   一般我们是使用一次捕获多次处理方式，格式如下：


```java
try{      
	编写可能会出现异常的代码 
}catch(异常类型A  e){ 
  //当try中出现A类型异常,就用该catch来捕获.      
	//处理异常的代码      
	//记录日志/打印异常信息/继续抛出异常 
}catch(异常类型B  e){  
  //当try中出现B类型异常,就用该catch来捕获.      
	//处理异常的代码      
	//记录日志/打印异常信息/继续抛出异常 
}
```

>注意:这种异常处理方式，要求多个catch中的异常不能相同，并且若catch中的多个异常之间有子父类异常的关系，那么子类异常要求在上面的catch处理，父类异常在下面的catch处理。

- 运行时异常被抛出可以不处理。即不捕获也不声明抛出。 
- 如果ﬁnally有return语句,永远返回ﬁnally中的结果,避免该情况。
- 如果父类抛出了多个异常,子类重写父类方法时,抛出和父类相同的异常或者是父类异常的子类或者不抛出异常。 
- 父类方法没有抛出异常，子类重写父类该方法时也不可抛出异常。此时子类产生该异常，只能捕获处理，不能声明抛出 

>小贴士：
>throws声明异常--父类，throw抛出异常--子类，两个应该配套使用。
>抛出异常类型<声明异常类型

## 10.7 自定义异常

- 概述

  在开发中根据自己业务的异常情况来定义异常类. 
  自定义一个业务逻辑异常: RegisterException。一个注册异常类。 

  异常类的定义:

  1. 自定义一个编译期异常: 自定义类并继承于 java.lang.Exception 。 
  2. 自定义一个运行时期的异常类:自定义类并继承于 java.lang.RuntimeException 。 

- 自定义异常的例子

```java
// 业务逻辑异常 
public class RegisterException extends Exception {     
	/**      
	* 空参构造      
	*/    
	public RegisterException() {     }       
	/**      
	*      
	* @param message 表示异常提示      
	*/     
	public RegisterException(String message) {         
		super(message);     
	} 
}
```

```java
package com.wbs.advance05;
import javax.security.auth.login.LoginException;
public class Demo01 {
    //模拟数据库中已存在账号
    public static String[] names = {"tom","jack","rose"};
    public static void main(String[] args) {
        try{
            checkUsername("花儿");
            System.out.println("恭喜你，注册成功！");//如果没有异常就是注册成功
        }catch (RegisterException re){
            re.printStackTrace();
        }finally {
            System.out.println("我是final");
        }
        System.out.println("成不成功，都不要紧！");

    }

    /**
     *  判断当前注册账号是否存在
     *  因为是编译期异常，又想调用者去处理 所以声明该异常
     * @param uname
     * @return
     * @throws RegisterException
     */
    public static Boolean checkUsername(String uname) throws RegisterException {
        for(String name:names){
            if(name.equals(uname)){
                throw new RegisterException("亲，您所用的用户名" + name + "已经注册过了！");
            }
        }
        return true;
    }
}
```





## 第十一章、多线程

## 11.1 并发与并行

- 并发：指两个或多个事件在**同一个时间段内**发生；
- 并行：指两个或多个事件在**同一时刻**发生（同时发生）。
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20210317152928974.png)

>注意：单核处理器的计算机肯定是不能**并行**的处理多个任务的，只能是多个任务在单个CPU上并发运行。同理,线程也是一样的，从宏观角度上理解线程是并行运行的，但是从微观角度上分析却是串行运行的，即一个线程，一个线程的去运行，当系统只有一个CPU时，线程会以某种顺序执行多个线程，我们把这种情况称之为**线程调度**。 

## 11.2 线程与进程

- 进程：是指一个内存中运行的应用程序，每个进程都有一个独立的内存空间，一个应用程序可以同时运行多个进程；进程也是程序的一次执行过程，是系统运行程序的基本单位；系统运行一个程序即是一个进程从创建、运行到消亡的过程。 
- 线程：线程是进程中的一个执行单元，负责当前进程中程序的执行，一个进程中至少有一个线程。一个进程中是可以有多个线程的，这个应用程序也可以称之为多线程程序。 

>简而言之：一个程序运行后至少有一个进程，一个进程中可以包含多个线程。
>所有线程都可以共享进程的资源。

## 11.3 创建线程类

Java使用 java.lang.Thread 类代表线程，所有的线程对象都必须是Thread类或其子类的实例。每个线程的作用是完成一定的任务，实际上就是执行一段程序流即一段顺序执行的代码。Java使用线程执行体来代表这段程序流。 

- Java中通过继承Thread类来创建并启动多线程的步骤如下： 

  1. 定义Thread类的子类，并重写该类的run()方法，该run()方法的方法体就代表了线程需要完成的任务,因此把 run()方法称为线程执行体；
  2. 创建Thread子类的实例，即创建了线程对象 ；
  3. 调用线程对象的start()方法来启动该线程。

  ```java
  /**
  *教师类
  **/
  public class Teacher1 extends Thread {
     @Override
     public void run() {
         while(true)
         {
             System.out.println("教师：大家好我是" + tname);
         }
     }
     private String tname;
     private int age;
     public String getTname() {
         return tname;
     }
     public void setTname(String tname) {
         this.tname = tname;
     }
     public int getAge() {
         return age;
     }
     public void setAge(int age) {
         this.age = age;
     }
     public Teacher(String name, int age) {
         this.tname = name;
         this.age = age;
     }
     public Teacher() {
     }
  }
  
  /**
  *学生类
  **/
  public class Student1 extends Thread {
      /**
       * 多线程执行代码方法
       */
      @Override
      public void run()
      {
         while(true)
         {
             System.out.println("学生：大家好我是" + stuname);
         }
      }
      private String stuname;
      private int age;
      public String getStuname() {
          return stuname;
      }
      public void setStuname(String stuname) {
          this.stuname = stuname;
      }
      public int getAge() {
          return age;
      }
      public void setAge(int age) {
          this.age = age;
      }
      public Student() {
      }
      public Student(String name, int age) {
          this.stuname = name;
          this.age = age;
      }
  }
  
  /**
  *测试类
  **/
  public class Test {
      public static void main(String[] args) {
          Student1 stu1=new Student1("张三",21);
          Teacher1 t=new Teacher1("老庞",32);
          // stu1.run();
          //启动一次线程
          stu1.start();
          //t.run();
          //启动一次线程
          t.start();
          /**
           * stu1.run() t.run()
           * 上述方法不可行
           * 因为run方法只是一个继承父类的线程方法执行体，直接调用该方法，跟调用普通方法没有区别，是不能启动线程的
           */
      }
  }
  ```

- 实现Runnable接口(常用)
  创建一个类实现Runnable接口，然后重写run方法
  创建实现类对象、代理类对象，然后通过代理类对象调用start()方法启动线程

  ```java
  /**
  *教师类
  **/
  public class Teacher2 implements Runnable {
     /**
       * 多线程执行代码方法（重写run方法）
       */
      @Override
      public void run() {
          while(true)
          {
              System.out.println("教师：大家好我是" + tname);
          }
      }
      private String tname;
      private int age;
      public String getTname() {
          return tname;
      }
      public void setTname(String tname) {
          this.tname = tname;
      }
      public int getAge() {
          return age;
      }
      public void setAge(int age) {
          this.age = age;
      }
      public Teacher(String name, int age) {
          this.tname = name;
          this.age = age;
      }
      public Teacher() {
      }
  }
  
  /**
  *学生类
  **/
  public class Student2 implements Runnable {
      /**
       * 多线程执行代码方法（重写run方法）
       */
      @Override
      public void run() {
          while (true) {
              System.out.println("学生：大家好我是" + stuname);
          }
      }
      private String stuname;
      private int age;
      public String getStuname() {
          return stuname;
      }
      public void setStuname(String stuname) {
          this.stuname = stuname;
      }
      public int getAge() {
          return age;
      }
      public void setAge(int age) {
          this.age = age;
      }
      public Student() {
      }
      public Student(String name, int age) {
          this.stuname = name;
          this.age = age;
      }
  }
  
  /**
  *测试类
  **/
  public class Test {
      public static void main(String[] args) {
          Student2 stu1 = new Student2("张三", 21);
          Teacher2 tea1 = new Teacher2("老庞", 32);
  
        	/**
        	  *将实现类对象放入代理对象中
        	  */
          Thread t1 = new Thread(stu1);
          Thread t2 = new Thread(tea1);
  
          t1.start();
          t2.start();
    }
  }
  ```

- 实现java.util.concurrent并发包下的Callable接口(一般不用)

  创建一个类实现Callable接口，然后重写call方法并声明异常

  创建一个实现类对象，执行Callable方式，需要FutureTask实现类的支持，用于接收计算结果，并创建一个线程代理类对象，启动线程。

  ```java
   /**
     * 学生类
     */
  public class Student3 implements Callable {
  
      @Override
      public Integer call() throws Exception {
          for(int i=0;i<=10;i++){
              System.out.println(sname + "是一名学生！");
          }
          return null;
      }
  
  
      private String sname;
      private int age;
  
      public String getSname() {
          return sname;
      }
  
      public void setSname(String sname) {
          this.sname = sname;
      }
  
      public int getAge() {
          return age;
      }
  
      public void setAge(int age) {
          this.age = age;
      }
  
      public Student3(String sname, int age) {
          this.sname = sname;
          this.age = age;
      }
  
      @Override
      public String toString() {
          return "Student{" +
                  "sname='" + sname + '\'' +
                  ", age=" + age +
                  '}';
      }
  }
  
  /**
    * 教师类
    */
  public class Teacher3 implements Callable {
  
      @Override
      public Integer call() throws Exception {
          for(int i=0;i<=10;i++){
              System.out.println(tname + "是一名老师！");
          }
          return null;
      }
  
      private String tname;
      private int age;
  
      public String getTname() {
          return tname;
      }
  
      public void setTname(String tname) {
          this.tname = tname;
      }
  
      public int getAge() {
          return age;
      }
  
      public void setAge(int age) {
          this.age = age;
      }
  
      public Teacher3(String tname, int age) {
          this.tname = tname;
          this.age = age;
      }
  
      @Override
      public String toString() {
          return "Teacher{" +
                  "tname='" + tname + '\'' +
                  ", age=" + age +
                  '}';
      }
  }
  
   /**
     * 测试类
     */
  public class ThreadDemo1 {
      public static void main(String[] args) {
          /**
           * 实现Callable接口，实现多线程
           */
          Student3 stu3 = new Student3("李四",21);
          Teacher3 tea3 = new Teacher3("老葛",30);
  
          //需要FutureTask实现类的支持,用于接收计算结果
          FutureTask stuFt = new FutureTask(stu3);
          FutureTask teaFt = new FutureTask(tea3);
  
          //创建线程代理类
          Thread t1 = new Thread(stuFt);
          Thread t2 = new Thread(teaFt);
  
          //启动线程
          t1.start();
          t2.start();
      }
  }
  ```

  

## 第十二章、反射

## 12.1 反射的概述

![反射的方式](https://img-blog.csdnimg.cn/2021032018565534.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzUwOTk0MjM1,size_16,color_FFFFFF,t_70)

- 反射的应用场合
  在编译时根本无法知道该对象或者类可能属于哪些类，程序只依靠运行时的信息来发现该对象和类的真实信息。

- 反射的作用
  通过反射可以使程序代码访问装载到JVM中的类的内部信息：

  1. 获取已装载类的属性信息；
  2. 获取已装载类的方法；
  3. 获取已装载累类的构造方法的信息。

- 反射的机制
  在JDK中，主要由这些类来实现java反射机制，这些类都位于java.lang.reflect包中：

  1. Class类：代表一个类；
  2. Field类：代表类的成员变量（属性）；
  3. Method类：代表类的成员方法；
  4. Constructor类：代表类的构造方法；
  5. Array类：提供了动态创建数组，以及访问数组的元素的静态方法。

- Class类

  - [ ] Class类是java反射机制的起源和入口

  1. 用于获取与类相关的各种信息；
  2. 提供了获取类信息的相关方法；
  3. Class类继承自Object类。

  - [ ] Class类是所有类的共同的图纸

  1. 每个类都有自己的对象，好比图纸和实物的关系；
  2. 每个类也可以看做是一个对象，有共同的图纸Class，存放类的结构信息，能够通过相应方法取出相应信息(类的名字、属性、方法、构造方法、父类和接口)。

## 12.2 反射的优缺点

- 优点

1. 反射提高了java程序的灵活性和扩展性，降低耦合性，提高自适应能力。它允许程创建和控制人格类的对象，无需提前硬编码目标类；
2. 反射是其他一些常用语言。如C、C++、Fortran或者Pascal等都不具备的；
3. java反射技术应用领域很广，如软件测试、EJB、JavaBean等；
4. 许多流行的开源框架例如Struts、Hibernate、Spring在实现过程中都采用了该技术。

- 缺点
- [ ] 性能问题
  使用反射基本上是一种解释操作，用于字段和方法接入时要远慢于直接代码。因此java反射机制主要应用在对灵活性和扩展性要求很高的系统框架上，普通程序不建议使用。
- [ ] 使用反射会模糊程序内部逻辑
  程序人员希望在源代码中看到程序的逻辑，反射的等绕过了源代码的技术，因而会带来维护问题。反射代码比相应的直接代码更复杂。

## 12.3 反射的方法和使用

Class类的常用方法：

| 方法名                              | 功能说明                               |
| ----------------------------------- | -------------------------------------- |
| getFields()                         | 获得类的public类型的属性               |
| getDeclaredFieldds()                | 获得类的所有属性                       |
| getField(Strign name)               | 获得类的指定属性                       |
| getMethods()                        | 获得类的public类型的方法               |
| getMethod(String name,Class[] args) | 获得类的指定方法                       |
| getConstrutors()                    | 获得类的public类型的构造方法           |
| getConstrutor(Class[] args)         | 获得类的特定构造方法                   |
| newInstance()                       | 通过类的无参构造方法创建该类的一个对象 |
| getName()                           | 获得类的完整名字                       |
| getPackage()                        | 获取此类所属的包                       |
| getSuperclass()                     | 获得此类的父类对应的Class对象          |

使用反射来实例化对象：

```java
public class demo1 {
    public static void main(String[] args) {
        try {
            //1.加载类（加载到JVM中）
            Class clz = Class.forName("com.qhj.fanshe.Administrator");
            //2.1 实例化对象1
            Object objInstance1 = clz.newInstance();//相当于执行Administrator administrator = new Administrator();
            System.out.println(objInstance1);
            //2.2 实例化对象2（使用构造函数）
            Constructor ct = clz.getDeclaredConstructor(null);
            Object objInstance2 = ct.newInstance(null);
            System.out.println(objInstance2);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

Administrator类：

```java
public class Administrator {
    public String sex;
    String pox;
    protected double money;
    /**
     * 管理员编号
     */
    private String adminNumber;
    /**
     * 管理员密码
     */
    private String adminPwd;
    /**
     * 管理员名字
     */
    private String adminName;

    public String getAdminNumber() {
        return adminNumber;
    }

    public void setAdminNumber(String adminNumber) {
        this.adminNumber = adminNumber;
    }

    public String getAdminPwd() {
        return adminPwd;
    }

    public void setAdminPwd(String adminPwd) {
        this.adminPwd = adminPwd;
    }

    public String getAdminName() {
        return adminName;
    }

    public void setAdminName(String adminName) {
        this.adminName = adminName;
    }

    public Administrator() {
    }

    public Administrator(String adminNumber, String adminPwd, String adminName) {
        this.adminNumber = adminNumber;
        this.adminPwd = adminPwd;
        this.adminName = adminName;
    }
    public void Hello1(){
//        System.out.println("Hello1");
    }
    public String Hello2(){
        return "success";
    }
    private int Hello3(){
        return 1;
    }
    public void Hello4(String name,int age){
        System.out.println("大家好！我是："+name+"今年："+age+"岁了！");
    }
    public String Hello5(String name,int age){
        return "success5";
    }
}
```

- **属性（Field）**

  ```java
  /**
  * 通过反射得到类里面的属性（字段）
  */
  public void c1(){
     try {
         //1.加载类（加载到jvm中）
         Class cls = Class.forName("com.qhj.fanshe.Administrator");
         //2.得到类中所有的public属性
         Field[] f = cls.getFields();
         //3.得到类中的所有属性
         Field[] f = cls.getDeclaredFields();
         //4.获得类中指定的public类型属性
         Field ff = cls.getField("sex");
         System.out.println(ff.getName()+"\t访问类型："+ff.getType()+"\t访问修饰符："+ff.getModifiers());
  
         for (Field field:f){
             System.out.println(field.getName()+"\t访问类型："+field.getType().getSimpleName()+"\t访问修饰符："+ Modifier.toString(field.getModifiers()));
         }
     } catch (Exception e) {
         e.printStackTrace();
     }
  }
  ```

- [ ] 访问类型

  ```java
  field.getType();//表示完整的输出（含包名）
  field.getType().getSimpleName();//表示只输出类型（不含包名）
  ```

- [ ] 属性名

  ```java
  field.getName();
  ```

- [ ] 访问修饰符

  ```java
  /**
  *default 0
  *public  1
  *private 2
  */
  field.getModifiers();//输出数字
  Modifier.toString(field.getModifiers());//输出名字
  ```

- [ ] 给属性赋值和获取属性值

  ```java
  /**
  * 通过反射给类中的属性赋值
  */
  public void c2(){
     try {
         //1.加载类（加载到jvm中）
         Class cls = Class.forName("com.qhj.fanshe.Administrator");
         /**
          * 2.获得类中指定的属性
          * 实例化对象，相当于
          * Administrator administrator = new Administrator();
          * administrator.setSex("男");
          */
         Field f1 = cls.getField("sex");
         //实例化对象
         Object objInstance = cls.newInstance();
         //给sex属性赋值
         f1.set(objInstance,"男");
         //得到sex的属性值
         System.out.println(f1.get(objInstance));
     } catch (Exception e) {
         e.printStackTrace();
     }
  }
  ```

- **方法（类中的方法）**

  ```java
  /**
  * 通过反射访问类中的方法
  */
  public void c3() {
     try {
         //1.加载类（加载到jvm中）
         Class cls = Class.forName("com.qhj.fanshe.Administrator");
         /**
          * 2.获取的是类的所有共有方法，这就包括自身的所有public方法，和从基类继承的、从接口实现的所有public方法
          */
         Method[] ms = cls.getMethods();
         /**
          * 3.获取的是类自身声明的所有方法，包含public、protected和private方法
          */
         Method[] ms = cls.getDeclaredMethods();
         /**
          * 4.获得类中指定的方法（只有public类型的方法可以指定）
          */
         Method mm1 = cls.getMethod("Hello2");//无参
         Method mmm1 = cls.getMethod("Hello5",String.class,int.class);//有参
  
         Method mm2 = cls.getDeclaredMethod("Hello2");//无参
         Method mmm2 = cls.getDeclaredMethod("Hello5", String.class, int.class);//有参
         Object objInstance = cls.newInstance();
  
         mm1.invoke(objInstance);//invoke()表示调用当前方法并返回执行当前方法的结果
         System.out.println("方法名："+mm1);
         mmm1.invoke(objInstance,"张三",23);
         mmm1.invoke(objInstance,new Object[]{"李四",12});
  
         mm2.invoke(objInstance);
         System.out.println("方法名："+mm2.getName());
         System.out.println("返回值："+mmm2.invoke(objInstance,"王五",52));//获得返回值
         /**
          * 5.构造方法
          */
         //5.1获得类的public类型的无参构造方法
         Constructor cz1 = cls.getConstructor();
         System.out.println("方法名："+cz1.getName()+"\t访问修饰符："+Modifier.toString(cz1.getModifiers()));
         //5.2获得类的public类型的有参构造方法
         Constructor cz2 = cls.getDeclaredConstructor(new Class[]{String.class,String.class,String.class});
         Object objInstance2 = cz2.newInstance(new Object[]{"1001","103651","赵六"});
         for (Method m:ms){
             System.out.println("方法名："+m.getName()+"\t访问修饰符："+Modifier.toString(m.getModifiers())+"\t返回值类型："+m.getReturnType().getSimpleName());
         }
     } catch (Exception e) {
         e.printStackTrace();
     }
  }
  ```

- [ ] 访问方法名

  ```java
  m.getName();
  ```

- [ ] 访问修饰符

  ```java
  m.getModifiers();//数字
  Modifier.toString(m.getModifiers());//名字
  ```

- [ ] 返回值类型

  ```java
  m.getReturnType();//完整类型
  m.getReturnType().getSimpleName();//只有返回值类型
  ```

- **类**

  ```java
  /**
  * 通过反射访问类
  */
  public void c4(){
     try {
         //1.加载类（加载到jvm中）
         Class cls = Class.forName("com.qhj.fanshe.Administrator");
         //2.类的完整名字
         System.out.println(cls.getName());
         //3.类所在的包
         System.out.println(cls.getPackage().getName());
         //4.此类的父类
         System.out.println(cls.getSuperclass());
     } catch (Exception e) {
         e.printStackTrace();
     }
  }
  ```

- [ ] 类完整名字

  ```java
  cls.getName();
  ```

- [ ] 类所在包

  ```java
  cls.getPackage();
  ```

- [ ] 此类的父类

  ```java
  cls.getSuperclass();
  ```

- **数组**

- [ ] 一维数组

  ```java
  /**
   * 通过反射动态创建数组并存取元素
   */
  public void c5(){
      try {
          //1.加载类（加载到jvm）
          Class cls = Class.forName("java.lang.Integer");
          //2.创建数组对象
          Object arr = Array.newInstance(cls,10);
          //3.给数组赋值
          Array.set(arr,5,20);
          //4.取出元素
          Object elem = Array.get(arr,5);
          System.out.println(elem);
          /**
           * 相当于
           * int arr[]=new int[10];
           * arr[5]=20;
           * System.out.println(arr[5]);
           */
      } catch (Exception e) {
          e.printStackTrace();
      }
  }
  ```

- [ ] 多维数组

  ```java
  /**
  * 通过反射动态创建数组并存取元素（多维）
  */
  public void c6(){
     // 创建一个含有10*15*18个元素的整型数组
     int dims[] = { 10, 15, 18 };
     Object arr = Array.newInstance(int.class, dims);
     // 给arr[5][8][10]赋值
     Object arr5 = Array.get(arr, 5);
     Object arr58 = Array.get(arr5, 8);
     Array.set(arr58, 10, 30);
     // 取出arr[5][8][10]值并输出
     Object elem = Array.get(arr58, 10);
     System.out.println(elem);
     /**
      * 相当于执行语句：
      * int arr[ ][ ][ ]=new int[10][15][18];
      * arr[5][8][10]=20; System.out.println(arr[5][8][10]);
      */
  }
  ```

## 第十三章、代理模式

## 13.1 代理的概述

- 代理模式的作用

  为其他对象提供一种代理以控制对目标对象的访问。某些情况下客户**不想或不能直接**引用另一个对象，而代理对象可在**客户端**和**目标对象**间起到**中介作用**。

- 代理模式一般涉及到的**角色**

- [ ] **抽象角色**：真实对象和代理对象的共同接口;

- [ ] **真实角色**：真实对象，最终要引用的对象;

- [ ] **代理角色**:

  1. 内部含有对真实对象的引用，从而可以操作真实对象;
  2. 提供与真实对象相同的接口以便在任何时刻代替真实对象;
  3. 可在执行真实对象操作前后附加其他操作，相当于对真实对象进行封装。

  ![动态代理](https://files.mdnice.com/user/34144/d82281e8-3972-4b1d-819a-e0d3d3d33351.png)


  > 小贴士：
  >
  > 必须明确一个动态代理类可适用多个抽象角色和真实角色！

  ## 13.2 代理模式的分类

  静态代理

  优点：不需要修改目标对象就实现了功能的增加。

  缺点：真实角色必须是事先已经存在的，并将其作为代理对象的内部属性。如果事先并不知道真实角色则无法使用；

  一个真实角色必须对应一个代理角色，如果大量使用会导致类的急剧膨胀。

## 13.2.1 静态代理的是演示：

1. 抽象角色

   ```java
   /**
    * 抽象角色（USB接口）
    */
   public interface USB {
       /**
        * 启动功能
        */
       void start();
   
       /**
        * 工作
        */
       void service();
   
       /**
        * 测试电脑CPU当前温度
        */
       int hotSize();
   
   }
   ```

2. 真实角色

   ```java
   /**
    * 真实角色（键盘实现类）
    */
   public class KeyBord implements USB {
   
       @Override
       public void start() {
           System.out.println("键盘正在插入电脑中……");
       }
   
       @Override
       public void service() {
           System.out.println("键盘正在工作中……");
       }
   
       @Override
       public int hotSize() {
           return 50;
       }
   }
   ```

3. 代理角色

   ```java
   /**
    * 静态代理角色（同真实角色实现类要实现USB接口）
    */
   public class UsbProxy implements USB {
       /**
        * 真实角色
        */
       KeyBord keyBord = new KeyBord();
   
       @Override
       public void start() {
           System.out.println("日志：调用start函数前置通知！");
           keyBord.start();
           System.out.println("日志：调用start函数后置通知！");
       }
   
       @Override
       public void service() {
           System.out.println("日志：调用service函数前置通知！");
           keyBord.service();
           System.out.println("日志：调用service函数前置通知！");
       }
   
       @Override
       public int hotSize() {
           System.out.println("日志：正在检测电脑温度中……");
           int i = keyBord.hotSize();
           if(i>=70){
               System.out.println("电脑温度过高！");
               return 0;
           }
           System.out.println("电脑温度正常！");
           return 1;
       }
   }
   ```

4. 测试类

   ```java
   public class Test {
       public static void main(String[] args) {
   
           UsbProxy usbProxy = new UsbProxy();
           usbProxy.start();
           System.out.println("-------------------");
           usbProxy.service();
           System.out.println("-------------------");
           System.out.println("CPU当前温度：" + usbProxy.hotSize() + "摄氏度！");
   
       }
   }
   
   运行结果：
   /**
        * 日志：调用start函数前置通知！
        * 键盘正在插入电脑中……
        * 日志：调用start函数后置通知！
        * -------------------
        * 日志：调用service函数前置通知！
        * 键盘正在工作中……
        * 日志：调用service函数前置通知！
        * -------------------
        * 日志：正在检测电脑温度中……
        * 电脑温度正常！
        * CPU当前温度：50摄氏度！
        */
   ```

## 13.3 动态代理

1. Java动态代理类位于java.lang.reflect包下，主要涉及到两个类：InvocationHandler接口和

   Proxy类；

2. InvocationHandler接口仅定义了一个方法：

```java
public object invoke(Object obj,Method method, Object[] args){
  //obj一般是指代理类
  //method是被代理的方法
  //args为该方法的参数数组	
  //这个抽象方法在代理类中动态实现
}
```

3. Proxy类即为动态代理类，主要方法包括:

```java
protected Proxy(InvocationHandler h){
  //构造函数，用于给内部的h赋值
} 

static Object newProxyInstance(ClassLoader loader, Class[ ] interfaces, InvocationHandler h) {
  //返回代理类的一个实例
  //loader是类装载器
  //interfaces是真实类所拥有的全部接口的数组
}

static Class getProxyClass (ClassLoader loader, Class[] interfaces) {
  //获得一个代理类
}
```

## 13.2.1 动态代理的演示：

1. 创建一个实现接口InvocationHandler的类；
2. 在invoke方法内通过反射调用真实对象的方法，并添加附加操作；
3. 创建被代理的类以及接口；
4. 通过Proxy类的newProxyInstance() 创建一个代理；
5. 必须传入一个InvocationHandler对象；
6. 通过代理调用方法。

-----------

1. 抽象角色

   ```java
   /**
    * 抽象角色
    */
   public interface USB {
       /**
        * 启动功能
        */
       void start();
       /**
        * 工作
        */
       void service();
       /**
        * 测试电脑CPU当前温度
        */
       int hotSize();
   
       int lenth(int num);
   }
   ```

2. 真实角色

   ```java
   /**
    * 真实角色
    */
   public class Mouse implements USB {
       @Override
       public void start() {
           System.out.println("鼠标正在插入电脑中……");
       }
       @Override
       public void service() {
           System.out.println("鼠标正在工作中……");
       }
       @Override
       public int hotSize() {
           System.out.println("鼠标温度");
           return 50;
       }
       @Override
       public int lenth(int num) {
           return num;
       }
   }
   ```

3. 动态代理角色---`注意！！！（此类不是动态代理类）`

   ```java
   import java.lang.reflect.InvocationHandler;
   import java.lang.reflect.Method;
   import java.lang.reflect.Proxy;
   import java.util.Arrays;
   
   /**
    * 动态代理角色(此类不是动态代理类，getProxy()方法返回中的newProxyInstance()才是动态代理对象，运行期间动态生成)
    */
   public class LogHandler implements InvocationHandler {
   
       /**
        * 要代理的真实角色(未知)
        */
       Object target;
   
       public LogHandler(){
       }
   
       /**
        * 要传入的真实角色
        * @param target
        */
       public LogHandler(Object target) {
           this.target = target;
       }
   
       @Override
       public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
           System.out.println("目标对象：" + target.getClass());
           System.out.println("目标对象-方法：" + method.getName());
           System.out.println("目标对象-参数：" + Arrays.toString(args));
           Object result = method.invoke(target,args);
           System.out.println("目标对象返回结果：" + result);
           return result;
       }
   
       /**
        * 获取动态代理的方法（JDK内部帮我们获取目标对象的各种信息，并负责自动调用……）
        *  getClass().getClassLoader()---类加载器
        *  getClassLoader(),getClass().getInterfaces()---类实现的接口
        *  this---指的是执行该getProxy()方法时，加载本代理类中的invoke()方法
        * @return
        */
       public Object getProxy(){
           return Proxy.newProxyInstance(target.getClass().getClassLoader(),target.getClass().getInterfaces(),this);
       }
   }
   ```

4. 测试类

   ```java
   public class Test {
       public static void main(String[] args) {
       Mouse mouse = new Mouse();
          LogHandler logHandler = new LogHandler(mouse);
          USB usb = (USB)logHandler.getProxy();
          usb.start();
          usb.lenth(11111);
       }
   
     运行结果：
       /**
        * 目标对象：class com.wbs.proxy2.Mouse
        * 目标对象-方法：start
        * 目标对象-参数：null
        * 鼠标正在插入电脑中……
        * 目标对象返回结果：null
        * 目标对象：class com.wbs.proxy2.Mouse
        * 目标对象-方法：lenth
        * 目标对象-参数：[11111]
        * 目标对象返回结果：11111
        */
   }
   
   ```

> 小贴士：
>
> LogHandler类不是动态代理类！！
>
> newProxyInstance()方法返回的才是动态代理对象，是在运行时动态创建的!

## 13.3 两种代理模式的区别

- 静态代理类确实存在，动态代理类在运行期动态生成

- 一个真实角色必须对应一个静态代理角色，而动态代理大大减少了代理类的数量（一个动态代理对象多个真是角色）
- 动态代理类不会作实质性的工作，在生成它的实例时必须提供一个handler，由它接管实际的工作（会自动执行handler的invoke方法）