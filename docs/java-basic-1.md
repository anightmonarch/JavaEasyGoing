#
# 一、运行环境

## 1.1 Java虚拟机--JVM

- JVM（Java Virtual Machine ）：Java虚拟机，简称JVM，是运行所有Java程序的假想计算机，是Java程序的 运行环境，是Java 最具吸引力的特性之一。我们编写的Java代码，都运行在 JVM 之上。

- 跨平台：任何软件的运行，都必须要运行在操作系统之上，而我们用Java编写的软件可以运行在任何的操作系 统上，这个特性称为Java语言的跨平台特性。该特性是由JVM实现的，我们编写的程序运行在JVM上，而JVM 运行在操作系统上。

  

## 1.2 JRE和JDK

- JRE (Java Runtime Environment) ：是Java程序的运行时环境，包含 JVM 和运行时所需要的 核心类库 。
- JDK (Java Development Kit)：是Java程序开发工具包，包含 JRE 和开发人员使用的工具。 我们想要运行一个已有的Java程序，那么只需安装 JRE 即可。 我们想要开发一个全新的Java程序，那么必须安装 JDK 。

$$
小贴士：

三者之间的关系：JDK > JRE > JVM
$$

# 二、编译和运行

## 2.1 编译和运行是两回事 

- 编译：是指将我们编写的Java源文件翻译成JVM认识的.class文件，在这个过程中， javac 编译器会检查我们所写的程序是否有错误，有错误就会提示出来，如果没有错误就会编译成功。 
- 运行：是指将.class文件交给虚拟机JVM去运行，此时JVM就会去执行我们编写的程序了。

## 2.2 标识符

- 标识符
  - [ ] HelloWorld案例中，出现的标识符有类名字 HelloWorld 。
- 命名规则
  - [ ] 标识符可以包含 英文字母26个(区分大小写) 、 0-9数字 、 $（美元符号） 和 _（下划线） 。 
  - [ ] 标识符不能以数字开头。 
  - [ ] 标识符不能是关键字。
- 命名规范
  - [ ] 类名规范：首字母大写，后面每个单词首字母大写（大驼峰式）,例如HelloWorld。 
  - [ ] 方法名规范： 首字母小写，后面每个单词首字母大写（小驼峰式），例如getAllByUsername。 
  - [ ] 变量名规范：全部小写，例如id、username、password。

# 三、常量和变量

## 3.1 常量

 - 常量：是指在java程序中固定不变的数据。
- 常量的分类

| 类型       | 含义                                           | 数据举例                  |
| :--------- | :--------------------------------------------- | :------------------------ |
| 整数常量   | 所有的整数                                     | 0，1， 567， -9           |
| 小数常量   | 所有的小数                                     | 0.0， -0.1， 2.55         |
| 字符常量   | **单引号引起来**,只能写一个字符,**必须有内容** | 'a' , '好'                |
| 字符串常量 | **双引号引起来**,可以写多个字符,**也可以不写** | "A" ，"abc" ，"你好" ，"" |
| 布尔常量   | 只有两个值（流程控制中讲解）                   | true ， false             |
| 空常量     | 只有一个值（引用数据类型中讲解）               | null                      |

## 3.2 变量

 - 变量：常量是固定不变的数据，那么在程序中可以变化的量称为变量。

> 数学中，可以使用字母代替数字运算,例如 x=1+5 或者 6=x+5。 
> 程序中，可以使用字母保存数字的方式进行运算，提高计算能力，可以解决更多的问题。比如x保存5，x也可 以保存6，这样x保存的数据是可以改变的，也就是我们所讲解的变量。


> 注意事项：
> 1.Java中要求一个变量每次只能保存一个数据，必须要明确保存的数据类型。
> 2.变量名称：在同一个大括号范围内，变量的名字不可以相同。
> 3.变量赋值：定义的变量，不赋值不能使用

# 四、数据类型

## 4.1 数据类型分类

*java数据类型分为两大类：引用数据类型和基本数据类型*。

- ##### 引用数据类型

  - [ ] 包括类、数组、接口。

- ##### 基本数据类型（4类8种数据类型）

  | 数据类型     | 关键字       | 内存占用 |        取值范围        |
  | :----------- | :----------- | :------: | :--------------------: |
  | 字节型       | byte         | 1个字节  |        -128~127        |
  | 短整型       | short        | 2个字节  |      -32768~32767      |
  | 整型         | int(默认)    | 4个字节  | -2147483648~2147483647 |
  | 长整型       | long         | 8个字节  |  -2的63次方~2的63次方  |
  | 单精度浮点数 | float        | 4个字节  |   1.4013E~3.4028E+38   |
  | 双精度浮点数 | double(默认) | 8个字节  |  4.9E-324~1.7977E+308  |
  | 字符型       | char         | 2个字节  |        0~65535         |
  | 布尔类型     | boolean      | 1个字节  |      true，false       |

  > 小贴士：
  > Java中的默认类型：整数类型是 int 、浮点数类型是 double 。
  >
  > long类型：建议数据后加L表示。
  >
  > float类型：建议数据后加F表示。

## 4.2、数据类型转换

 - 自动类型转换
  - [ ] 转换规则：将取值范围小的类型自动提升为取值范围大的类型 。


```java
public static void main(String[] args) {
        int a = 10;
        double b = 2.5;
        //int自动提升为double类型
        //自动类型转换时，取值范围小的类型直接转换为取值范围大的类型
        double c = a + b;
        System.out.println(c);
    }
```

> 小贴士（取值范围由小->大）：
> byte、short、char‐‐>int‐‐>long‐‐>float‐‐>double

- 强制类型转换

  - [ ] 转换规则：将取值范围大的类型强制转换成取值范围小的类型 。

    - [ ] 转换格式：数据类型 变量名  = （数据类型）被转数据值;

```java
public static void main(String[] args) {
        //short短整型变量，内存中占2个字节
        short s = 1;
        /*
        出现编译失败
        s和1做运算的时候，1是int类型，s会被提升为int类型
        s+1后的结果是int类型，将结果在赋值成short类型时会发生错误
        short内存占2个字节，int类型占4个字节
        必须将int强制转成short才能完成赋值成功
        */
        s = s + 1;//编译失败
        s = (short)(s+1);//编译成功①
        s+=1;//编译成功②，②是①通过内部强转得到的
    }
```

> 特别注意：
>
> 比较而言，自动转换是Java自动执行的，而强制转换需要我们自己手动执行；
>
> 浮点数转成整数，直接取消小数点及小数点后的数据，可能造成数据损失精度。

## 4.3 常用ASCII编码表(美国标准信息交换码)

| 字符 | 数值 |
| :--: | :--: |
|  0   |  48  |
|  9   |  57  |
|  A   |  65  |
|  Z   |  90  |
|  a   |  97  |
|  z   | 122  |

# 五、运算符

## 5.1 算数运算符（Java中，整数使用这些算数运算符，无论怎么计算，也不会得到小数）

算术运算符包括：+、-、* 、/、%、++、- -。

- ++运算/--运算：变量自增1/自减1
  - [ ] 独立运算：独立运算时，变量前++和变量后++没有区别；
  - [ ] 混合运算（i=1）
    - 变量前++（++i）：先加一再赋值。
    - 变量后++（i++）：先赋值再加一。

```java
public static void main(String[] args) {
        int a = 5;
        //先对a进行+1操作，再把a的值作为++a的值,赋值给b
        int b = ++a;//此时a=6,b=6
        //先取a的值作为a++的值，赋值给c，在对a进行+1操作
        int c = a++;//此时c=5，a=6
        System.out.println(a+","+b);//6,6
        System.out.println(a+","+c);//6,5
}
```

- +符号在字符串中的操作
  - [ ] 加法：纯数字的加法操作；
  - [ ] 连接/拼接：在遇到字符串的时候，表示连接、拼接的含义。

```java
public static void main(String[] args) {
       int a = 5;
       int b = 6;
       String c = "Hello";
       System.out.println(a+b);//11：进行纯数字加操作
       System.out.println(a+c);//5Hello：进行字符串拼接操作
}
```

## 5.2 赋值运算符

赋值运算符包括：=、+=、-=、*=、/+、%=。

- 赋值运算符，就是将符号右边的值，赋给左边的变量。

## 5.3 比较运算符

比较运算符包括：==、<、>、<=、>=、!=。

- 比较运算符，是两个数据之间进行比较的运算，运算结果都是布尔值 true 或者 false 。

## 5.4 逻辑运算符

逻辑运算符包括：&&、||、！。

- 逻辑运算符，是用来连接两个布尔类型结果的运算符，运算结果都是布尔值 true 或者 false。

## 5.5 三元运算符

- 三元运算符格式：

  数据类型 变量名 = 布尔类型表达式 ? 结果1 : 结果2

- 三元运算符运算方式：

  - [ ] 布尔类型表达式结果是true，三元运算符整体结果为结果1，赋值给变量；
  - [ ] 布尔类型表达式结果是false，三元运算符整体结果为结果2，赋值给变量。

# 六、流程控制语句

## 6.1 判断语句


 -  if语句

```java
if(关系表达式){
	语句体;
｝
```

>执行流程：
>首先判断关系表达式看其结果是true还是false
>如果是true就执行语句体
>如果是false就不执行语句体
>
>![image-20210126201647096](C:\Users\wang'bo'shi\AppData\Roaming\Typora\typora-user-images\image-20210126201647096.png)

 - if...else语句

```java
if(关系表达式){
	语句体1;
}else{
	语句体2;
}
```

>执行流程：
>首先判断关系表达式看其结果是true还是false
>如果是true就执行语句体1
>如果是false就执行语句体2
>
>![在这里插入图片描述](https://img-blog.csdnimg.cn/20210126142807939.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzUwOTk0MjM1,size_16,color_FFFFFF,t_70)

 - if...else if...else语句

```java
if(判断条件1){
	执行语句1;
}else if(判断条件2){
	执行语句2;
}
……
}else if(判断条件n){
	执行语句n;
}else{
	执行语句n+1;
}
```

>执行流程：
>首先判断关系表达式1看其结果是true还是false
>如果是true就执行语句体1
>如果是false就继续判断关系表达式2看其结果是true还是false
>如果是true就执行语句体2
>如果是false就继续判断关系表达式...看其结果是true还是false
>...
>如果没有任何关系表达式为true，就执行语句体n+1
>
>![image-20210126201822055](C:\Users\wang'bo'shi\AppData\Roaming\Typora\typora-user-images\image-20210126201822055.png)

- if语句与三元运算符的互换

```java
public static void main(String[] args) {
      int a = 20;
      int b = 10;
      //定义变量，保存a和b的最大值
      int c;
      if (a > b){
          c = a;
      }else {
          c = b;
      }
      System.out.println("1.输出最大值为："+c);
      //用三元运算符代替if...else判断语句，结果相同
      c = a > b ? a : b;
      System.out.println("2.输出最大值为："+c);
  }
```

## 6.2 选择语句

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210126150222780.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzUwOTk0MjM1,size_16,color_FFFFFF,t_70)

- 选择语句--switch

  ```java
  switch(表达式){
  	case 常量值1:
  		语句体1;
  		break;
  	case 常量值2:
  		语句体2;
  		break;
  	...
  	default:
  		语句体n+1;
  		break;
  }
  ```

  >执行流程：
  >首先计算出表达式的值
  >其次，和case依次比较，一旦有对应的值，就会执行相应的语句，在执行的过程中，遇到break就会结束。
  >最后，如果所有的case都和表达式的值不匹配，就会执行default语句体部分，然后程序结束掉。

- case的穿透性
  在switch语句中，如果case的后面不写break，将出现穿透现象，也就是不会在判断下一个case的值，直接向后运行，直到遇到break，或者整体switch结束。

  ```
  public static void main(String[] args) {
        int a = 5;
        switch (a){
            case 0:
                System.out.println("执行case0");
                break;
            case 5:
                System.out.println("执行case5");
            case 10:
                System.out.println("执行case10");
            default:
                System.out.println("执行default");
        }
        /*最后程序执行结果是
        执行case5
        执行case10
        执行default
        */
    }
  ```

  >小贴士：
  >上述程序中，执行case5后，由于没有break语句，程序会一直向后走，不会在判断case，也不会理会break，直接运行完整体switch。由于case存在穿透性，因此初学者在编写switch语句时，必须要写上break。
  >
  >switch语句中，表达式的数据类型，可以是byte，short，int，char，enum（枚举），JDK7版本后可以接收字符串。

## 6.3 循环语句

- for循环
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20210126151652426.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzUwOTk0MjM1,size_16,color_FFFFFF,t_70)

```java
for(初始化表达式①; 布尔表达式②; 步进表达式④){
	循环体③
}
```

  >执行流程：
  >执行顺序：①②③④>②③④>②③④...当②不满足时才会停止循环，执行其他语句。
  >①负责完成循环变量初始化
  >②负责判断是否满足循环条件，不满足则跳出循环
  >③具体执行的语句
  >④循环后，循环条件所涉及变量的变化情况

- while循环
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20210126151842969.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzUwOTk0MjM1,size_16,color_FFFFFF,t_70)

  ```java
  初始化表达式①
  while(布尔表达式②){
  	循环体③
  	步进表达式④
  }
  ```

  >执行流程：
  >执行顺序：①②③④>②③④>②③④...②不满足为止。
  >①负责完成循环变量初始化。
  >②负责判断是否满足循环条件，不满足则跳出循环。
  >③具体执行的语句。
  >④循环后，循环变量的变化情况。

- do...while循环
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20210126153019892.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzUwOTk0MjM1,size_16,color_FFFFFF,t_70)

  ```java
  初始化表达式①
  do{
  	循环体③
  	步进表达式④
  }while(布尔表达式②);
  ```

  >执行流程：
  >执行顺序：①③④>②③④>②③④...②不满足为止。
  >①负责完成循环变量初始化。
  >②负责判断是否满足循环条件，不满足则跳出循环。
  >③具体执行的语句
  >④循环后，循环变量的变化情况

```java
public static void main(String[] args) {
        //使用循环输出10次HelloWorld
        //1.for循环
        for (int i = 0;i < 10;i++){
            System.out.println("HelloWorld"+i);
        }
        //2.while循环
        int j = 1;
        while (j <= 10){
            System.out.println("HelloWorld"+j);
            //步进表达式
            j++;
        }
        //3.do...while循环
        int x = 1;
        do {
            System.out.println("HelloWorld"+x);
            x++;
        }while (x <= 10)
    }
```

- 嵌套循环

  所谓嵌套循环，是指一个循环的循环体是另一个循环。比如for循环里面还有一个for循环，就是嵌套循环。总共的循环次数=外循环次数*内循环次数


  ```
  for(初始化表达式①;循环条件②;步进表达式⑦){
  	for(初始化表达式③;循环条件④;步进表达式⑥){
  		执行语句⑤;
  	}
  }
  ```

  >执行流程：
  >执行顺序：①②③④⑤⑥>④⑤⑥>⑦②③④⑤⑥>④⑤⑥
  >外循环一次，内循环多次。
  >比如跳绳：一共跳5组，每组跳10个。5组就是外循环，10个就是内循环。


  ```java
  public static void main(String[] args) {
          //使用嵌套循环，打印5*8的矩形
          //5*8的矩形，打印5行*号，每行8个(5行8列)
          //外循环5次，内循环8次
          for (int i = 0;i < 5;i++){
              for (int j = 0;j < 8;j++){
                  System.out.print("*");
              }
              //内循环打印8个*后，需要一次换行
              System.out.println();
          }
      }
  ```

- 死循环

  死循环：也就是循环中的条件永远为true，死循环的是永不结束的循环。例如：while(true){}。

- 跳出语句

 - [ ] break

 	使用场景：终止switch或者循环

 - [ ] continue

	使用场景：结束本次循环，继续下一次的循环


```java
public static void main(String[] args) {
        for (int i = 1;i <= 10;i++){
            if (i == 3){
                /*
                break;
                输出 HelloWorld1 HelloWorld2
                */
                /*
                continue;
                输出 除了HelloWorld3其他全都输出
                */
            }
            System.out.println("HelloWorld"+i);
        }
    }
```

[^**for 和 while 的小区别：**]: 控制条件语句所控制的那个变量，在for循环结束后，就不能再被访问到了，而while循环结束还可以继 续使用，如果你想继续使用，就用while，否则推荐使用for。原因是for循环结束，该变量就从内存中消 失，能够提高内存的使用效率。 在已知循环次数的时候使用推荐使用for，循环次数未知的时推荐使用while。

# 七、数组

## 7.1 数组的定义和访问

- 数组的概念

  数组的概念：数组就是存储数据长度固定的容器，保证多个数据的数据类型要一致。

- 数组的定义（三种）

 - [x] #### 格式一：


~~~java
```
数组存储的数据类型[] 数组名字 = new 数组存储的数据类型[长度]；
int[] arr = new int[3];
```

>int 数组存储的数据类型：创建的数组容器可以存储什么数据类型。
[]:表示数组。
数组名字：为定义的数组起个变量名，满足标识符规范，可以使用名字操作数组。
new：关键字，创建数组使用的关键字。
>int 数组存储的数据类型：创建的数组容器可以存储什么数据类型。
[长度]：数组的长度，表示数组容器中可以存储多少个元素。
**注意：数组有定长特性，长度一旦指定，不可更改。
（和水杯道理相同，买了一个2升的水杯，总容量就是2升，不能多也不能少。）**
~~~

 - [x] #### 格式二：

   ```java
   数据类型[] 数组名 = new 数据类型[]{元素1,元素2,元素3...};
   int[] arr = new int[]{1,2,30};
   ```

 - [x] #### 格式三：


```java
数据类型[] 数组名 = {元素1,元素2,元素3...};
int[] arr = {1,2,3,4,5};
```

- 数组的访问

  - [ ] **索引**：每一个存储到数组的元素，都会自动的拥有一个编号，从0开始，这个自动编号称为数组索引(index)，可以通过数组的索引访问到数组中的元素。
  - [ ] **格式**：


  ```
  数组名[索引]
  ```

  - [x] **数组的长度属性**：每个数组都具有长度，而且是固定的，Java中赋予了数组的一个属性，可以获取到数组的长度，语句为：数组名.length，属性length的执行结果是数组的长度，int类型结果。由此可以推断出，数组的最大索引值为 数组名.length-1。


  ```java
  public static void main(String[]args){
  	int[] arr=new int[]{1,2,3,4,5};//打印数组的长度属性，输出结果是5
  	System.out.println(arr.length);
  }
  ```

  - [x] **索引访问数组中的元素**：


  ```java
  数组名[索引] = 数值; //为数组中的元素赋值
  变量 = 数组名[索引]; //获取出数组中的元素
  ```


  ```java
  public static void main(String[]args){
  	//定义存储int类型数组，赋值元素1，2，3，4，5
  	int[] arr = {1,2,3,4,5};
  	//为0索引元素赋值为6
  	arr[0]=6;
  	//获取数组0索引上的元素
  	int i  = arr[0];
  	System.out.println(i);
  	//直接输出数组0索引元素
  	System.out.println(arr[0]);
  }
  ```

## 7.2 数组原理内存图

- 内存概述

内存是计算机中的重要原件，临时存储区域，作用是运行程序。我们编写的程序是存放在硬盘中的，在硬盘中的程序是不会运行的，必须放进内存中才能运行，运行完毕后会清空内存。

```java
Java虚拟机要运行程序，必须要对内存进行空间的分配和管理。
```

- java虚拟机的内存划分

  JVM的内存划分：

| 区域名称   | 作用                                                       |
| ---------- | ---------------------------------------------------------- |
| 寄存器     | 给CPU使用，和我们开发无关。                                |
| 本地方法栈 | JVM在使用操作系统功能的时候使用，和我们开发无关。          |
| 方法区     | 存储可以运行的class文件。                                  |
| 堆内存     | 存储对象或者数组，new是用来创建的，都存储在堆内存。        |
| 方法栈     | 方法运行时使用的内存，比如main方法运行，进入方法栈中执行。 |

- 数组在内存中的存储

 - [ ] 一个数组内存图


```java
public static void main(String[]args){
	int[] arr = new int[3];
	System.out.println(arr);//[I@5f150435是数组在内存中的地址。
	//new出来的内容，都是在堆内存中存储的，而方法中的变量arr保存的是数组的地址。
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210126165229229.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzUwOTk0MjM1,size_16,color_FFFFFF,t_70)

 - [ ] 两个数组内存图


```java
public static void main(String[]args){
	int[] arr = new int[3];
	int[] arr2 = new int[2];
	System.out.println(arr);
	System.out.println(arr2);
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210126165358109.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzUwOTk0MjM1,size_16,color_FFFFFF,t_70)

 - [ ] 两个变量指向一个数组


```java
public static void main(String[]args){
	//定义数组，存储3个元素
	int[] arr = new int[3];
	//通过数组索引进行赋值
	arr[0] = 5;
	arr[1] = 6;
	arr[2] = 7;
	//输出3个索引上的元素值
	System.out.println(arr[0]);//5
	System.out.println(arr[1]);//6
	System.out.println(arr[2]);//7
	//定义数组变量arr2，将arr的地址赋值给arr2，此时arr和arr2操作的是同一个数组
	int[] arr2 = arr;
	arr2[1] = 9;
	System.out.println(arr[1]);//9
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210126165601670.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzUwOTk0MjM1,size_16,color_FFFFFF,t_70)


## 7.3 数组的常见操作

- 数组越界异常

  ```java
  public static void main(String[]args){
  	int[] arr = {1,2,3};
  	System.out.println(arr[3]);//数组索引只有0-2,3>2数组下标越界异常
  }
  ```

  	在开发中，数组的越界异常是不能出现的，一旦出现了，就必须要修改我们编写的代码。

- 数组空指针异常

  ```java
  public static void main(String[]args){
  	int[] arr = {1,2,3};
  	arr = null;
  	System.out.println(arr[0]);//数组置空，内存中已不存在数组arr，所以报空指针异常
  }
  ```

  空指针异常在内存图中的表现：
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20210126170726501.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzUwOTk0MjM1,size_16,color_FFFFFF,t_70)

- 数组遍历【重点】

  **数组遍历**：就是将数组中的每个元素分别获取出来，就是遍历。遍历也是数组操作中的基石。


  ```java
  public static void main(String[]args){
  	int[] arr = {1,2,3,4,5};
  	for(inti=0;i<arr.length;i++){
  		System.out.println(arr[i]);
  	}
  }
  ```

- 数组获取最大值元素

 - [ ] 最大值获取：从数组的所有元素中找出最大值。

 - [ ] 实现思路：
   定义变量，保存数组0索引上的元素
    	遍历数组，获取出数组中的每个元素
    	将遍历到的元素和保存数组0索引上值的变量进行比较
    	如果数组元素的值大于了变量的值，变量记录住新的值
    	数组循环遍历结束，变量保存的就是数组中的最大值

   ```java
   public static void main(String[]args){
   	int[] arr = {5,15,2000,10000,100,4000};
   	//定义变量，保存数组中0索引的元素
   	int max = arr[0];
   	//遍历数组，取出每个元素
   	for(int i = 0;i<arr.length;i++){
   		//遍历到的元素和变量max比较
   		//如果数组元素大于max 
   		if(arr[i] > max){
   			//max记录住大值
   			max = arr[i];
   		}
   	}
   	System.out.println("数组最大值是："+max);
   }
   ```

- 数组反转
  **数组的反转**：数组中的元素颠倒顺序，例如原始数组为1,2,3,4,5，反转后的数组为5,4,3,2,1
  **实现思想**：数组最远端的元素互换位置。
  实现反转，就需要将数组最远端元素位置交换
  定义两个变量，保存数组的最小索引和最大索引
  两个索引上的元素交换位置
  最小索引++，最大索引--，再次交换位置
  最小索引超过了最大索引，数组反转操作结束
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20210126171422458.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzUwOTk0MjM1,size_16,color_FFFFFF,t_70)

  ```java
  public static void main(String[]args){
  	int[] arr = {1,2,3,4,5};
  	/*循环中定义变量min=0最小索引
  	max=arr.length‐1最大索引
  	min++,max‐‐*/
  	for(int min = 0,max = arr.length‐1;min <= max;min++,max‐‐){
  		//利用第三方变量完成数组中的元素交换
  		int temp = arr[min];
  		arr[min] = arr[max];
  		arr[max] = temp;
  	}
  	//反转后，遍历数组
  	for(int i = 0;i < arr.length;i++){
  		System.out.println(arr[i]);
  	}
  }
  ```

## 7.4数组作为方法参数和返回值

- 数组作为方法参数

  **数组作为方法参数传递，传递的参数是数组内存的地址**。


  ```java
  public static void main(String[] args){
  	int[] arr = {1,3,5,7,9};
  	//调用方法，传递数组
  	printArray(arr);
  }
  /*创建方法，方法接收数组类型的参数进行数组的遍历*/
  public static void printArray(int[]arr){
  	for(int i = 0;i < arr.length;i++){
  		System.out.println(arr[i]);
  	}
  }
  ```

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20210126172052567.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzUwOTk0MjM1,size_16,color_FFFFFF,t_70)

- 数组作为方法返回值

  **数组作为方法的返回值，返回的是数组的内存地址。**


  ```java
  public static void main(String[]args){
  	//调用方法，接收数组的返回值
  	//接收到的是数组的内存地址
  	int[] arr = getArray();
  	for(int i = 0;i < arr.length;i++){
  		System.out.println(arr[i]);
  	}
  }
  /*创建方法，返回值是数组类型
  return返回数组的地址*/
  public static int[] getArray(){
  	int[] arr = {1,3,5,7,9};
  	//返回数组的地址，返回到调用者
  	return arr;
  }
  ```

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20210126172401370.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzUwOTk0MjM1,size_16,color_FFFFFF,t_70)

- 方法的参数类型区别

  ```java
  public static void main(String[]args){
        int a = 1;
        int b = 2;
        System.out.println(a);//1
        System.out.println(b);//2
        //基本数据类型相当于复制一个副本，副本中的值改变但是原来的不变
        change(a,b);
        System.out.println(a);//1
        System.out.println(b);//2
    }
    public static void change(int a,int b){
        a = a + b;
        b = b + a;
    }
  ```

  ```java
  public static void main(String[]args){
  	int[] arr = {1,3,5};
  	System.out.println(arr[0]);//1
  	//引用数据类型传递的是地址，都发生改变
  	change(arr);
  	System.out.println(arr[0]);//200
  }
  public static void change(int[]arr){
  	arr[0] = 200;
  }
  ```

> 总结（重难点）:
> ①方法的参数为基本数据类型时,传递的是数据值，只传数据值，相当于复制一个副本，改变数值时只可以改变现在的数据而原来的数据不变.
> ②方法的参数为引用数据类型时,传递的是地址值，改变数值时原来和现在的值都改变.
> **这与全局变量还是局部变量无关，只与数据类型相关！**
>
> 方法栈：存放方法的定义和结构，通过main方法进入方法栈。
>
> 堆内存：存储的是实际变量的地址及数据值，new的对象数据都存储在堆内存中。
>
> 引用数据类型：赋值是直接将a地址赋值给b，当修改b中数据值时，a中的数据值也会变，实际上此时a和b操作的是同一个变量。
>
> 基本数据类型：是直接将a拷贝一个副本赋值给b，修改b，a不变。

# 八、面向对象

**面向对象**：区别于面向过程思想，强调的是通过调用对象的行为来实现功能，而不是自己一步一步的去操作实现。它可以将复杂的事情简单化，并将我们从执行者变成了指挥者。

面向对象包含了**三大基本特征**，即封装、继承和多态。

>区别：
>面向过程：强调步骤；
>面向对象：强调对象。

## 8.1 类和对象

 - 什么是类？
  - [ ] 类：是一组相关**属性**和**行为**的集合。可以看成是一类事物的模板，使用事物的属性特征和行为特征来描述该类事物。

  - [ ] 现实中，描述一类事物：

 		属性：就是该事物的状态信息。
 		行为：就是该事物能够做什么。
 		

 - 什么是对象？
  - [ ] 对象：是一类事物的具体体现。对象是类的一个实例（对象并不是找个女朋友），必然具备该类事物的属性和行为。
 - 类与对象的关系
  - [ ] 类是对一类事物的描述，是抽象的。  
    - [ ] 对象是一类事物的实例，是具体的。 
  - [ ] **类是对象的模板，对象是类的实体**

## 8.2 类的定义

```java
public class ClassName{
	//成员变量：对应事物的属性
	//成员方法：对应事物的行为
}
```

 - [ ] 定义类：就是定义类的成员，包括成员变量和成员方法。
 - [ ] 成员变量：和以前定义变量几乎是一样的。只不过位置发生了改变。在类中，方法外。
 - [ ] 成员方法：和以前定义方法几乎是一样的，只不过把static去掉。

```java
public class Student {
    //定义成员变量
    String name;//姓名
    int age;//年龄
    //定义成员方法
    //1.学习的方法
    public void study(){
        System.out.println("好好学习，天天向上！");
    }
    //2.吃饭的方法
    public void eat(){
        System.out.println("学习饿了要吃饭！");
    }
}
```

## 8.3 对象的使用

```java
//创建对象
类名 对象名 = new 类名();  
//对象访问类中的成员
对象名.成员变量；
对象名.成员方法()；
```

成员变量的默认值

|          | 数据类型                       | 默认值           |
| -------- | ------------------------------ | ---------------- |
| 基本类型 | 整数（byte，short，int，long） | 0                |
|          | 浮点数（float，double）        | 0.0              |
|          | 字符（char）                   | ‘\u0000’--->空格 |
|          | 布尔（boolean）                | false            |
| 引用类型 | 类、对象、数组、枚举           | null             |

```java
public class testStudent {
    public static void main(String[] args) {
        //创建对象
        Student s = new Student();

        //直接输出成员变量值
        System.out.println("姓名："+s.name);
        System.out.println("年龄："+s.age);

        //给成员变量赋值
        s.name = "赵丽颖";
        s.age = 12;

        //再次输出成员变量的值
        System.out.println("姓名："+s.name);//赵丽颖
        System.out.println("年龄："+s.age);//12

        //调用成员方法
        s.study();
        s.eat();
    }
}
```

## 8.4 对象内存图

- 一个对象，调用一个方法内存图
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20210129162906704.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzUwOTk0MjM1,size_16,color_FFFFFF,t_70)
  **Phone p是存储在栈内存中的；
  new Phone()以及成员变量的赋值是存储在堆内存中的；
  变量p指向堆内存中的空间，寻找方法信息，去执行该方法。**
- 两个对象，调用同一方法内存图
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/2021012916485825.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzUwOTk0MjM1,size_16,color_FFFFFF,t_70)
  **Phone p（变量p是存储在栈内存中）指向堆内存中，系统作出方法标记，不做具体的操作；
  Phone p2（变量p2是存储在栈内存中）指向堆内存中，系统作出方法标记，不做具体的操作；
  方法信息在方法区中只保存一份，
  根据不同变量拿到的方法标记的地址去方法区寻找方法并执行**。
- 一个引用，作为参数传递到方法中内存图
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20210129165844586.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzUwOTk0MjM1,size_16,color_FFFFFF,t_70)
  **引用类型作为参数，传递的是地址值。**

## 8.5 成员变量和局部变量的区别

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210129165945189.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzUwOTk0MjM1,size_16,color_FFFFFF,t_70)

- 在类中的位置不同
  - [ ] 成员变量：类中，方法外
    - [ ] 局部变量：方法中或者方法声明上(形式参数)
- 作用范围不一样
  - [ ] 成员变量：类中
   - [ ] 局部变量：方法中
- 初始化值的不同
  - [ ] 成员变量：有默认值
  - [ ] 局部变量：没有默认值。必须先定义，再赋值，才能使用
- 在内存中的位置不同
  - [ ] 成员变量：堆内存
  - [ ] 局部变量：栈内存
- 生命周期不同
  - [ ] 成员变量：随着对象的创建而存在，随着对象的消失而消失
  - [ ] 局部变量：随着方法的调用而存在，随着方法的调用完毕而消失

# 九、封装

**概述**：面向对象编程语言是对客观世界的模拟，客观世界里成员变量都是隐藏在对象内部的，外界无法直接操作和修改。封装可以被认为是一个保护屏障，防止该类的代码和数据被其他类随意访问。要访问该类的数据，必须通过指定的方式。适当的封装可以让代码更容易理解与维护，也加强了代码的安全性。

**原则：** 将**属性隐藏**起来，若需要访问某个属性，**提供公共方法**对其访问。

## 9.1 封装的步骤

- 1.使用private关键字来修饰成员变量。
- 2.对需要访问的成员变量，提供对应的一对getXxx方法、setXxx方法。

## 9.2 封装的操作--private关键字

- private的含义

  - [ ] 1.private是一个权限修饰符，代表最小权限。
   - [ ] 2.可以修饰成员变量和成员方法。
    - [ ] 3.被private修饰后的成员变量和成员方法，只在本类中才能访问。

- private的使用格式

  ```java
  private 数据类型 变量名；
  ```

   - [ ] 使用private修饰成员变量，代码如下：

  ```java
  public class Student{
  	private String name;
  	private int age;
  }
  ```

   - [ ] 提供getXxx方法/setXxx方法，可以访问成员变量，代码如下：


  ```java
  public class Student{
  	private String name;
  	private int age;
  	public void setName(String n){
  		name = n;
  	}
  	public String getName(){
  		return name;
  	}
  	public void setAge(int a){
  		age = a;
  	}
  	public int getAge(){
  		returnage;
  	}
  }
  ```

## 9.3 封装优化1--this关键字

```java
public class Student{
	private String name;
	private int age;
	public void setName(String name){
		name = name;
	}
	public void setAge(int age){
		age=age;
	}
}
```

经过修改和测试，我们发现新的问题，成员变量赋值失败了。也就是说，在修改了setXxx()的形参变量名后，方法并没有给成员变量赋值！这是由于形参变量名与成员变量名重名，导致成员变量名被隐藏，方法中的变量名，无法访问到成员变量，从而赋值失败。所以，我们只能使用this关键字，来解决这个重名问题。

- this的含义

  this代表所在类的当前对象的引用（地址值），即对象自己的引用。

  >记住：方法被哪个对象调用，方法中的this就代表那个对象。即谁在调用，this就代表谁。

- this的使用格式

  ```java
  this.成员变量名；
  ```

  使用this修饰方法中的变量，解决成员变量被隐藏的问题，代码如下：


  ```java
  public class Student{
  	private String name;
  	private int age;
  	public void setName(String name){
  		//name = name;
  		this.name = name;
  	}
  	public String getName(){
  		return name;
  	}
  	public void setAge(int age){
  		//age = age;
  		this.age = age;
  	} 
  	public int getAge(){
  		return age;
  	}
  }
  ```

  >小贴士：方法中只有一个变量名时，默认也是使用this修饰，可以省略不写。

## 9.4 封装优化2--构造方法

当一个对象被创建时候，构造方法用来初始化该对象，给对象的成员变量赋初始值。

>小贴士：无论你与否自定义构造方法，所有的类都有构造方法，因为Java自动提供了一个无参数构造方法，一旦自己定义了构造方法，Java自动提供的默认无参数构造方法就会失效。

- 构造方法的定义格式

  ```java
  //构造方法的写法上，方法名与它所在的类名相同,没有返回值，不需要有返回值。
  修饰符 构造方法名(参数列表){
  	//方法体
  }
  ```

  ```java
  public class Student{
  	private String name;
  	private int age;
  	//无参数构造方法
  	public Student(){}
  	//有参数构造方法
  	public Student(String name,int age){
  		this.name = name;
  		this.age = age;
  	}
  }
  ```

- 注意事项

  - [ ] 1.如果你不提供构造方法，系统会给出无参数构造方法。
   - [ ] 2.如果你提供了构造方法，系统将不再提供无参数构造方法。
   - [ ] 3.构造方法是可以重载的，既可以定义参数，也可以不定义参数。

## 9.5 标准代码--JavaBean

JavaBean是Java语言编写类的一种标准规范。符合JavaBean的类，要求类必须是具体的和公共的，并且具有无参数的构造方法，提供用来操作成员变量的set和get方法。


```java
public class ClassName{
	//成员变量
	//构造方法
	//无参构造方法【必须】
	//有参构造方法【建议】
	//成员方法
	//getXxx()
	//setXxx()
}
```

编写符合JavaBean规范的类，以学生类为例，标准代码如下：

```java
public class Student{
	//成员变量
	private String name;
	private int age;
	//构造方法
	public Student(){}
	public Student(String name,int age){
		this.name = name;
		this.age = age;
	}
	//成员方法
	public void setName(String name){
		this.name = name;
	}
	public String getName(){
		return name;
	}
	public void setAge(int age){
		this.age = age;
	}
	public int getAge(){
		return age;
	}
}
```

测试类，代码如下：

```java
public class TestStudent{
	public static void main(String[] args){
		//无参构造使用
		Student s = new Student();
		s.setName("柳岩");
		s.setAge(18);
		System.out.println(s.getName()+"‐‐‐"+s.getAge());
		//带参构造使用
		Student s2 = new Student("赵丽颖",18);
		System.out.println(s2.getName()+"‐‐‐"+s2.getAge());
	}
}
```

# 十、引用类型和匿名对象

## 10.1 引用类型使用步骤

 - 导包
   使用import关键字导包，在类的所有代码之前导包，引入要使用的类型，java.lang包下的所有类无需导入。格式：

   ```java
   import 包名.类名
   ```

   举例：

   ```java
   java.util.Scanner;
   ```

 - 创建对象
   使用该类的构造方法，创建一个该类的对象。 格式：

   ```java
   数据类型 变量名 = new 数据类型(参数列表);
   ```

   举例：


   ```java
   Scanner sc = new Scanner(System.in);
   ```

 - 调用方法
   调用该类的成员方法，完成指定功能。格式：


   ```java
   变量名.方法名();
   ```

   举例：


   ```java
   int i = sc.nextInt();//接受一个键盘录入的整数
   ```

## 10.2  匿名对象

 - 匿名对象

   **没有变量名的对象。** 创建对象时，只有创建对象的语句，却没有把对象地址值赋值给某个变量。虽然是创建对象的简化写法，但是应用场景非常有限。

   格式：

   ```java
   new 类名(参数列表);
   ```

   举例：


   ```java
   new Scanner(System.in);
   ```

 - 应用场景

   - [ ] 创建匿名对象直接调用方法，没有变量名。

   ```java
   new Scanner(System.in).nextInt();
   ```

    - [ ] 一旦调用两次方法，就是创建两个对象，造成浪费。

   ```java
   	new Scanner(System.in).nextInt();
   	new Scanner(System.in).nextInt();
   ```

   > 小贴士：
   > 一个匿名对象，只能使用一次。

    - [ ] 匿名对象可以作为方法的参数和返回值。

      作为参数

      ```java
      public class demo1 {
          public static void main(String[] args) {
              //普通方式
              Scanner sc = new Scanner(System.in);
              input(sc);
              //匿名对象作为方法接收的参数
              input(new Scanner(System.in));
          }
          public static void input(Scanner sc){
              System.out.println(sc);
          }
      }
      ```

      作为返回值


   ~~~java
   ```
   public class demo3 {
       public static void main(String[] args) {
           //普通方式
           Scanner sc = getScanner();
       }
       public static Scanner getScanner(){
           //普通方式
           Scanner sc = new Scanner(System.in);
           return sc;
           //匿名对象作为方法返回值
           return new Scanner(System.in);
       }
   }
   ```
   ~~~

# 十一、Scanner类、Random类、ArrayList类

## 11.1 Scanner类

 - 什么是Scanner类？

   一个可以解析基本类型和字符串的简单文本扫描器。 
   例如，以下代码使用户能够从 System.in 中读取一个数：

   ```java
   public static void main(String[] args) {
           Scanner sc = new Scanner(System.in);
           int i = sc.nextInt();
       }
   ```

   >备注：System.in 系统输入指的是通过键盘录入数据。 

 - Scanner类的使用步骤
   **查看类**

   ```java
   import java.util.Scanner;//该类需要import导入后使用。
   ```

   **查看构造方法**

   ```java
   public Scanner(InputStream source) ;//构造一个新的 Scanner ，它生成的值是从指定的输入流扫描的。
   ```

   **查看成员方法**

   ```java
   public int nextInt() ;//将输入信息的下一个标记扫描为一个 int 值。 
   ```

   使用Scanner类，完成接收键盘录入数据的操作，代码如下：

   ```java
   //1.导包
   import java.util.Scanner;
   public class demo4 {
       public static void main(String[] args) {
           //2.创建键盘录入数据的对象
           Scanner sc = new Scanner(System.in);
           //3.接收数据
           System.out.println("请输入一个整数：");
           int i = sc.nextInt();
           //4.输出数据
           System.out.println(i);
       }
   }
   ```

## 11.2 Random类

 - 什么是Random类？

   此类的实例用于生成伪随机数。
   例如，以下代码使用户能够得到一个随机数：

   ```java
   Random r = new Random();
   int i = r.nextInt();
   ```

 - Random类的使用步骤
   **查看类**

   ```java
   java.util.Random ;//该类需要 import导入使后使用。 
   ```

   **查看构造方法**

   ```java
   public Random() ;//创建一个新的随机数生成器。
   
   ```

   **查看成员方法**

   ```java
   public int nextInt(int n) ;//返回一个伪随机数，范围在 0 （包括）和 指定值 n （不包括）之间的 int 值。 
   ```

   使用Random类，完成生成3个10以内的随机整数的操作，代码如下：

   ```java
   //1.导包
   import java.util.Random;
   public class demo5 {
       public static void main(String[] args) {
           //2.创建生成随机数的对象
           Random r = new Random();
           //3.随机生成一个数据
           int i = r.nextInt();
           //4.输出数据
           System.out.println(i);
       }
   }
   ```

## 11.3 ArrayList类

 - 什么是ArrayList类？

   java.util.ArrayList 是**大小可变的数组**的实现，存储在内的数据称为元素。此类提供一些方法来操作内部存储 的元素。 ArrayList 中可不断添加元素，其大小也自动增长。 

 - ArrayList类的使用步骤
   **查看类**

   ```java
   java.util.ArrayList <E> ;//该类需要 import导入使后使用。 
   ```

   <E> ，表示一种指定的数据类型，叫做泛型。 E ，取自Element（元素）的首字母。在出现 E 的地方，我们使 用一种引用数据类型将其替换即可，表示我们将存储哪种引用类型的元素。代码如下：

   ```java
   ArrayList<String>,ArrayList<Student>
   ```

   **查看构造方法**

   ```java
   public ArrayList() ;//构造一个内容为空的集合。
   ```

   基本格式：

   ```java
   ArrayList<String> list = new ArrayList<String>();
   ```

   在JDK 7后,右侧泛型的尖括号之内可以留空，但是<>仍然要写。简化格式：

   ```java
   ArrayList<String> list = new ArrayList<>();
   ```

**查看成员方法**
	

	```java
	public boolean add(E e) ;//将指定的元素添加到此集合的尾部。 
	```
	参数 E e ，在构造ArrayList对象时， <E> 指定了什么数据类型，那么 add(E e) 方法中，只能添加什么数据 类型的对象。
	
	使用ArrayList类，存储三个字符串元素，代码如下：

```java
	public static void main(String[] args) {
	        //创建数组
	        ArrayList<String> list = new ArrayList<>();
	        //创建三个对象
	        String s1 = "张三";
	        String s2 = "李四";
	        String s3 = "王五";
	        //把对象添加到集合
	        list.add(s1);
	        list.add(s2);
	        list.add(s3);
	        //输出集合list
	        System.out.println(list);
	    }
```

 - 常用方法和遍历
   对于元素的操作,基本体现在——增、删、查。常用的方法有：

    - [ ] public boolean add(E e) ：将指定的元素添加到此集合的尾部。

    - [ ] public E remove(int index) ：移除此集合中指定位置上的元素。返回被删除的元素。  

    - [ ] public E get(int index) ：返回此集合中指定位置上的元素。返回获取的元素。

    - [ ] public int size() ：返回此集合中的元素数。遍历集合时，可以控制索引范围，防止越界。 

      这些都是基本的方法，操作非常简单，代码如下:

      ```java
      public static void main(String[] args) {
              //创建集合对象
              ArrayList<String> list = new ArrayList<>();
              //添加元素
              list.add("Hello");
              list.add("Java");
              list.add("World");
              //public E get(int index) :返回指定索引的元素
              System.out.println("get:"+list.get(0));
              System.out.println("get:"+list.get(1));
              System.out.println("get:"+list.get(2));
              //public int size():返回集合中的元素的个数     
              System.out.println("size:"+list.size());
              //public E remove(int index):删除指定索引处的元素，返回被删除的元素
              System.out.println("remove:"+list.remove(0));
              // 遍历输出     
              for(int i = 0;i < list.size();i++){
                  System.out.println(list.get(i));
              }
          }
      ```

 - 如何存储基本数据类型

   ArrayList对象不能存储基本类型，只能存储引用类型的数据。类似 <int> 不能写，但是存储基本数据类型对应的 包装类型是可以的。所以，想要存储基本类型数据， <> 中的数据类型，必须转换后才能编写，转换写法如下：

   | 基本类型 | 基本类型包装类 |
   | -------- | -------------- |
   | byte     | Byte           |
   | short    | Short          |
   | int      | Integer        |
   | long     | Long           |
   | float    | Float          |
   | double   | Double         |
   | char     | Character      |
   | boolean  | Boolean        |



# 十二、String类、Arrays类、Math类

## 12.1 String类

 - String类概述

   **概述**

   java.lang.String 类代表字符串。Java程序中所有的字符串文字（例如 "abc" ）都可以被看作是实现此类的实例。
   类 String 中包括用于检查各个字符串的方法，比如用于**比较**字符串，**搜索**字符串，**提取**子字符串以及创建具有**翻译为大写或小写**的所有字符的字符串的副本。 

   **特点**

   1. 字符串不变：字符串的值在创建后不能被更改。

      ```java
      String s1 = "abc"; 
      s1 += "d"; 
      System.out.println(s1); // "abcd"  
      // 内存中有"abc"，"abcd"两个对象，s1从指向"abc"，改变指向，指向了"abcd"。
      ```

   2. 因为String对象是不可变的，所以它们可以被共享。

      ```java
      String s1 = "abc";
      String s2 = "abc";
      //内存中只有一个“abc”对象被创建，同时被s1和s2共享
      ```

   3. "abc" 等效于 char[] data={ 'a' , 'b' , 'c' } 。

      ```java
      例如：  
      String str = "abc";   
      相当于：  
      char data[] = {'a', 'b', 'c'};      
      String str = new String(data); 
      // String底层是靠字符数组实现的。
      ```

 - 使用步骤

   **查看类**

   ```java
   	java.lang.String ;//此类不需要导入。 
   ```

   **查看构造方法**


    - [ ] public String() ：初始化新创建的 String对象，以使其表示空字符序列。 
   - [ ] public String(char[] value) ：通过当前参数中的***字符数组***来构造新的String。 
   - [ ] public String(byte[] bytes) ：通过使用平台的默认字符集解码当前参数中的***字节数组***来构造新的 String。 


   ```java
   构造举例，代码如下：
   // 无参构造 
   String str = new String();
   // 通过字符数组构造 
   char chars[] = {'a', 'b', 'c'};      
   String str2 = new String(chars);  
    // 通过字节数组构造 
    byte bytes[] = { 97, 98, 99 };      
    String str3 = new String(bytes);
   ```

 - 常用方法

   **判断功能的方法**

   - [ ] public boolean equals (Object anObject) ：将此字符串与指定对象进行比较。 
   - [ ] public boolean equalsIgnoreCase (String anotherString) ：将此字符串与指定对象进行比较，忽略大小写。 

   >注：Object 是” 对象”的意思，也是一种引用类型。作为参数类型，表示任意对象都可以传递到方法中

   >小贴士：
   >“==”比较的是内存地址是否一直
   >“equals”比较的是两个字符串内容是否一致

   **获取功能的方法**

   - [ ] public int length () ：返回此字符串的长度。 
   - [ ] public String concat (String str) ：将指定的字符串连接到该字符串的末尾。 
   - [ ] public char charAt (int index) ：返回指定索引处的 char值。 
   - [ ] public int indexOf (String str) ：返回指定子字符串第一次出现在该字符串内的索引。 
   - [ ] public String substring (int beginIndex) ：返回一个子字符串，从beginIndex开始截取字符串到字符串结尾。 

- [ ] public String substring (int beginIndex, int endIndex) ：返回一个子字符串，从beginIndex到 endIndex截取字符串。含beginIndex，不含endIndex。

  **转换功能的方法**

  - [ ] public char[] toCharArray () ：将此字符串转换为新的字符数组。 

- [ ] public byte[] getBytes () ：使用平台的默认字符集将该 String编码转换为新的字节数组。

  - [ ] public String replace (CharSequence target, CharSequence replacement) ：将与target匹配的字符串使 用replacement字符串替换。

  >CharSequence 是一个接口，也是一种引用类型。作为参数类型，可以把String对象传递到方法中。

  **分割功能的方法**

  - [ ] public String[] split(String regex) ：将此字符串按照给定的regex（规则）拆分为字符串数组。

## 12.2 Arrays类

- 概述

  java.util.Arrays 此类包含用来操作数组的各种方法，比如排序和搜索等。其所有方法均为静态方法，调用起来非常简单。 

- 操作数组的方法

  - [ ] public static String toString(int[] a) ：返回指定数组内容的字符串表示形式。

  ```java
  public static void main(String[] args) {
          //定义int数组
          int arr[] = {2,34,35,4,657,8,69,9};
          //数组内容转为字符串
          String s = Arrays.toString(arr);
          // 打印字符串,输出内容   
          System.out.println(s); // [2, 34, 35, 4, 657, 8, 69, 9]
      }
  ```

  - [ ] public static void sort(int[] a) ：对指定的 int 型数组按数字升序进行排序。

  ```java
  public static void main(String[] args) {
          // 定义int 数组   
          int[] arr = {24,7,5,48,4,46,35,11,6,2};
          System.out.println("排序前:"+Arrays.toString(arr));// 排序前:[24, 7, 5, 48, 4, 46, 35, 11, 6,  2]
          // 升序排序   
          Arrays.sort(arr);
          System.out.println("排序后:"+Arrays.toString(arr));// 排序后:[2, 4, 5, 6, 7, 11, 24, 35, 46,  48]
      }
  ```

## 12.3 Math类

- 概述

  java.lang.Math 类包含用于执行基本数学运算的方法，如初等指数、对数、平方根和三角函数。类似这样的工具类，其所有方法均为静态方法，并且不会创建对象，调用起来非常简单。 

- 基本运算的方法

  public static double abs(double a) ：返回 double 值的绝对值。

  ```java
  double d1 = Math.abs(‐5); //d1的值为5 
  double d2 = Math.abs(5); //d2的值为5
  ```


~~~java
- [ ] public static double ceil(double a) ：返回大于等于参数的小的整数。
```
double d1 = Math.ceil(3.3); //d1的值为 4.0 
double d2 = Math.ceil(‐3.3); //d2的值为 ‐3.0 
double d3 = Math.ceil(5.1); //d3的值为 6.0
```

- [ ] public static double floor(double a) ：返回小于等于参数大的整数。

```
double d1 = Math.floor(3.3); //d1的值为3.0 
double d2 = Math.floor(‐3.3); //d2的值为‐4.0 
double d3 = Math.floor(5.1); //d3的值为 5.0
```
- [ ] public static long round(double a) ：返回接近参数的 long。(相当于四舍五入方法) 
```
long d1 = Math.round(5.5); //d1的值为6.0 
long d2 = Math.round(5.4); //d2的值为5.0
```
~~~

# 十三、static关键字

## 13.1 概述

关于 static 关键字的使用，它可以用来修饰的成员变量和成员方法，被修饰的成员是属于类的，而不是单单是属 于某个对象的。也就是说，既然属于类，就可以不靠创建对象来调用了。 

## 13.2 定义和使用格式

- 类变量

  当 static 修饰成员变量时，该变量称为类变量。该类的每个对象都共享同一个类变量的值。任何对象都可以更改 该类变量的值，但也可以在不创建该类的对象的情况下对类变量进行操作。

  类变量：使用 static关键字修饰的成员变量。
  定义格式：


  ```java
  static 数据类型 变量名;
  例：
  static int numberId;
  ```

- 静态方法

  当 static 修饰成员方法时，该方法称为类方法 。静态方法在声明中有 static ，建议使用类名来调用，而不需要 创建类的对象。调用方式非常简单。

  - [ ] 类方法：使用 static关键字修饰的成员方法，习惯称为静态方法。

    定义格式：

    ```java
    修饰符 static 返回值类型 方法名 (参数列表){  
    	// 执行语句       
    }
    例：
    public static void showNum() {   
    	System.out.println("num:" +  numberOfStudent); 
    }
    ```

  - [ ] 静态方法调用的注意事项： 

    1. 静态方法可以直接访问类变量和静态方法。
    2. 静态方法不能直接访问普通成员变量或成员方法。
    3. 反之，成员方法可以直接访问类变量或静态方法。 
    4. 静态方法中，不能使用this关键字。

  >小贴士：静态方法只能访问静态成员。 

- 调用格式

  被static修饰的成员可以并且建议通过类名直接访问。虽然也可以通过对象名访问静态成员，原因即多个对象均属 于一个类，共享使用同一个静态成员，但是不建议，会出现警告信息。
  格式：

  ```java
  // 访问类变量 
  类名.类变量名；  
  // 调用静态方法 
  类名.静态方法名(参数)； 
  ```

## 13.3 静态原理图解

static 修饰的内容：

- [ ] 是随着类的加载而加载的，且只加载一次。 
- [ ] 存储于一块固定的内存区域（静态区），所以，可以直接被类名调用。 
- [ ] 它优先于对象存在，所以，可以被所有对象共享。
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20210222173953837.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzUwOTk0MjM1,size_16,color_FFFFFF,t_70)

## 13.4 静态代码块

静态代码块：定义在成员位置，使用static修饰的代码块{ }。 

- [ ] 位置：类中方法外。 
- [ ] 执行：随着类的加载而执行且执行一次，优先于main方法和构造方法的执行。
  格式：

```java
public class ClassName{   
	static {     
		// 执行语句    
	}
} 
```

作用：给类变量进行初始化赋值。用法演示，代码如下：

```java
public class Game {   
	public static int number;   
	public static ArrayList<String> list;     
	static {     
		// 给类变量赋值     
		number = 2;     
		list = new ArrayList<String>();    
		// 添加元素到集合中     
		list.add("张三");     
		list.add("李四");   
	} 
}
```

>小贴士：
>static 关键字，可以修饰变量、方法和代码块。在使用的过程中，其主要目的还是想在不创建对象的情况 下，去调用方法。Arrays和Math两个工具类，就可以来体现static 方法的便利。

# 十四、继承

## 14.1 概述

- 由来：多个类可以称为**子类**，单独的那一个类称为**父类、基类或超类**。
  继承描述的是事物之间的所属关系，这种关系是： is-a 的关系。**父类更通用，子类更具体。** 我们通过继承，可以使多种事物之间形成一种关系体系。 

- 定义：继承就是子类继承父类的**属性**和**行为**，使得子类对象具有与父类相同的属性、相同的行为。子类可以直接访问父类中的**非私有**的属性和行为。 

- 好处：1. 提高代码的**复用性**。 

  2. 类与类之间产生了关系，是多态的前提。

  >小贴士:
  >多态的实现是建立在继承上的。 

## 14.2 继承的格式

通过extends关键字可以声明一个子类继承另外一个父类。

```java
class 父类 { 
	...      
}   
class 子类 extends 父类 { 
	...      
}
```

## 14.3 继承后的特点

### 14.3.1成员变量

***成员变量不重名***
如果子类父类中出现**不重名**的成员变量，这时的访问是**没有影响**的。代码如下：

```java 
/**
 * 父类
 */
public class Fu {
    //父类中的成员变量
    int num1 = 5;
}
/**
 * 子类
 */
public class Zi extends Fu{
    //子类中的成员变量
    int num2 = 6;
    //子类中的成员方法
    public void show(){
        //访问父类中的num1
        System.out.println("Fu num1="+num1);//继承自父类，可以直接访问
        //访问子类中的num2
        System.out.println("Zi num2="+num2);
    }
}
/**
 * 测试类
 */
public class test1 {
    public static void main(String[] args) {
        //创建子类对象
        Zi zi = new Zi();
        //调用子类中的show方法
        zi.show();
    }
}
```

***成员变量重名***
如果子类父类中出现**重名**的成员变量，这时的访问是**有影响**的。代码如下：

```java
		/**
		 * 父类
		 */
		public class Fu {
		    //父类中的成员变量
		    int num = 5;
		}
		/**
		 * 子类
		 */
		public class Zi extends Fu{
		    //子类中的成员变量
		    int num = 6;
		    //子类中的成员方法
		    public void show(){
		        //访问父类中的num
		        System.out.println("Fu num1="+super.num);
		        //访问子类中的num
		        System.out.println("Zi num2="+this.num);
		    }
		}
		/**
		 * 测试类
		 */
		public class test1 {
		    public static void main(String[] args) {
		        //创建子类对象
		        Zi zi = new Zi();
		        //调用子类中的show方法
		        zi.show();
		    }
		}
```



子父类中出现了同名的成员变量时，在子类中需要访问父类中非私有成员变量时，需要使用 super 关键字，修饰父类成员变量，类似于之前学过的 this 。
使用格式：

```java
super.父类成员变量名
```

>小贴士：
>① Fu 类中的成员变量是非私有的，子类中可以直接访问。
>② 若Fu 类中的成员变量私有了，子类是不能直接访问的。通常编码时，我们遵循封装的原则，使用private修饰成员变量，那么如何访问父类的私有成员变量呢？对！可以在父类中提供公共的getXxx方法和setXxx方法。
>注：super.getXxx();      	this.getXxx();    	getXxx();这三种方式都可以访问私有成员变量，但在访问父类的成员变量时一般选择第一种方式。

### 14.3.2成员方法

***成员方法不重名***
如果子类父类中出现**不重名**的成员方法，这时的调用是**没有影响**的。对象调用方法时，会先在子类中查找有没有对应的方法，若子类中存在就会执行子类中的方法，若子类中不存在就会执行父类中相应的方法。代码如下：

```java
class Fu{
	public void show(){
		System.out.println("父类中的show方法执行！");
	}
}
class Zi extends Fu{
	public void show2(){
		System.out.println("子类中的show2方法执行！");
	}
}
public static void main(String[] args) {
        //创建子类对象
        Zi zi = new Zi();
        //调用子类中的show方法
        //子类中虽然没有show方法，但是可以去父类中调用
        zi.show();
        zi.show2();
}
```


```java
- [ ] 成员方法重名--方法重写（Override）
```

如果子类父类中出现**重名**的成员方法，这时的访问是一种特殊情况，叫做**方法重写 (Override)**。
**方法重写** ：子类中出现与父类一模一样的方法时（返回值类型，方法名和参数列表都相同），会出现覆盖效果，也称为重写或者复写。声明不变，重新实现。

~~~java
```
	class Fu{
		public void show(){
			System.out.println("父类中的show方法执行！");
		}
	}
	class Zi extends Fu{
		public void show(){
			System.out.println("子类中的show方法执行！");
		}
	}
	public static void main(String[] args) {
	        //创建子类对象
	        Zi zi = new Zi();
	        //调用子类中的show方法
	        //子类中有show方法，只执行重写后的show方法 
	        zi.show();//子类中的show方法执行！
	}
```
~~~

>小贴士：
>① 父类的方法会先被创建（初始化），父类的构造方法会优先输出。
>② 父类和子类可以有相同的属性名。
>③ 因在父类中无法确定方法是哪个子类的方法，所以就定义一个方法体。
>④ ↑ 表示重写父类的方法，↓ 表示方法被子类重写。
>⑤ 重写方法时可以提升访问修饰符，但是不能降低访问修饰符。
>⑥ 子类方法覆盖父类方法，返回值类型、函数名和参数列表都要一模一样。 
>⑦ 调用父类的成员方法时，用super.父类成员方法。

>java内注解：
>1.Override：检查当前方法在类中是否存在；
>2.Deprecated：标记当前方法已过时；
>3.SuppressWarnings：去除方法或类中的警告信息。

## 构造方法

- [ ] 构造方法的名字是与类名一致的。所以子类是无法继承父类构造方法的。 
- [ ] 构造方法的作用是初始化成员变量的。所以子类的初始化过程中，必须先执行父类的初始化动作。子类的构造方法中默认有一个 super() ，表示调用父类的构造方法，父类成员变量初始化后，才可以给子类使用。代 码如下：

```java
class Fu {   
	private int n;   
	Fu(){     
		System.out.println("Fu()");   
	}
}
class Zi extends Fu {   
	Zi(){     
		// super（），调用父类构造方法     
		super();     
		System.out.println("Zi（）");   
	}   
} 
public class test{   
	public static void main (String args[]){     
		Zi zi = new Zi();   
	} 
} 
输出结果： 
Fu（） 
Zi（） 
```

## 14.4 super和this

- 父类空间优于子类对象产生
  在每次创建子类对象时，先初始化父类空间，再创建其子类对象本身。目的在于子类对象中包含了其对应的父类空 间，便可以包含其父类的成员，如果父类成员非private修饰，则子类可以随意使用父类成员。代码体现在子类的构 造方法调用时，一定先调用父类的构造方法。理解图解如下：
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20210223165630225.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzUwOTk0MjM1,size_16,color_FFFFFF,t_70)

- super和this的含义

  - [ ] super ：代表父类的**存储空间标识**(可以理解为父亲的引用)。 
  - [ ] this ：代表**当前对象的引用**(谁调用就代表谁)。 

- super和this的用法

  - [ ] 访问成员

  ```java
  this.成员变量     ‐‐    本类的     
  super.成员变量     ‐‐    父类的      
  
  this.成员方法名()   ‐‐    本类的        
  super.成员方法名()   ‐‐    父类
  ```

  - [ ] 访问构造方法

  ```java
  this(...)     ‐‐    本类的构造方法     
  super(...)    ‐‐    父类的构造方法
  ```

>小贴士：
>子类的每个构造方法中均有默认的super()，调用父类的空参构造。
>手动调用父类构造会覆盖默认的super()。 
>super() 和 this() 都必须是在构造方法的第一行，所以不能同时出现。 

## 14.5 继承的特点

- java只支持单继承，不支持多继承

  ```java
  //一个类只能有一个父类，不可以有多个父类。 
  class C extends A{}  //ok      
  class C extends A，B... //error
  ```

- java支持多层继承（继承体系）

  ```java
  class A{} 
  class B extends A{} 
  class C extends B{}
  ```

  >顶层父类是Object类。所有的类默认继承Object，作为父类。 

- 子类和父类是一种相对的概念

# 十五、抽象类

## 15.1 概述

- 由来
  父类中的方法，被它的子类们重写，子类各自的实现都不尽相同。那么父类的方法声明和方法主体，只有声明还有意义，而方法主体则没有存在的意义了。我们把没有方法主体的方法称为抽象方法。Java语法规定，**包含抽象方法的类就是抽象类** 。
- 定义
  抽象方法 ： 没有方法体的方法。
  抽象类：包含抽象方法的类。

## 15.2 abstract使用格式

- 抽象方法

  使用 abstract 关键字修饰方法，该方法就成了抽象方法，抽象方法只包含一个方法名，而没有方法体。

  定义格式：

  ```java
  修饰符 abstract 返回值类型 方法名 (参数列表);
  例：
  public abstract void run();
  ```

- 抽象类

  **如果一个类包含抽象方法，那么该类必须是抽象类。(反之不成立)**

  定义格式：

  ```java
  abstract class 类名字 {     
  }
  例：
  public abstract class Animal {     
  	public abstract void run()； 
  }
  ```

- 抽象的使用

  继承抽象类的子类必须重写父类所有的抽象方法。否则，该子类也必须声明为抽象类时也可以。最终，必须有子类实现该父类的抽象方法，否则，从最初的父类到最终的子类都不能创建对象，失去意义。

## 15.3 注意事项

1. 抽象类不能创建对象，如果创建，编译无法通过而报错。只能创建其非抽象子类的对象。

   > 理解：假设创建了抽象类的对象，调用抽象的方法，而抽象方法没有具体的方法体，没有意义。
   > Person p = new Student();
   > Person是父类抽象类，Student是子类非抽象类

2. 抽象类中，可以有构造方法，是供子类创建对象时，初始化父类成员使用的。

   > 理解：子类的构造方法中，有默认的super()，需要访问父类构造方法。

3. 抽象类中，不一定包含抽象方法，但是有抽象方法的类必定是抽象类。

   > 理解：未包含抽象方法的抽象类，目的就是不想让调用者创建该类对象，通常用于某些特殊的类结构设 计。

4. 抽象类的子类，必须重写抽象父类中所有的抽象方法，否则，编译无法通过而报错。除非该子类也是抽象 类。

   > 理解：假设不重写所有抽象方法，则类中可能包含抽象方法。那么创建对象后，调用抽象的方法，没有 意义。

# 十六、接口

## 16.1 概述

- **接口**，是Java语言中一种引用类型，是方法的集合，如果说类的内部封装了成员变量、构造方法和成员方法，那么**接口的内部主要就是封装了方法**，包含抽象方法（JDK 7及以前），默认方法和静态方法（JDK 8），私有方法 （JDK 9）。 

- **接口的定义**，它与定义类方式相似，但是使用 interface 关键字。它也会被编译成.class文件，但一定要明确它并不是类，而是另外一种引用数据类型。

  >小贴士：

>引用数据类型：数组、类、接口

- **接口的使用**，它不能创建对象（不能被实例化，但是使用匿名接口时可以），但是可以被实现（ implements ，类似于被继承）。一个实现接口的类（可以看做是接口的子类），需要实现接口中所有的抽象方法，创建该类对象，就可以调用方法了，否则它必须是一个抽象 类。 

  >小贴士：
  >接口中的方法都是抽象方法，不允许有普通方法！

## 16.2 定义格式

```java
 public interface 接口名称 {     
 	/**
     * 抽象方法
     */
    public void service1();
    /**
     * 默认方法
     */
    public default void service2(){
        System.out.println("默认方法输出service2");
    }
    /**
     * 静态方法
     */
    public static void service3(){
        System.out.println("静态方法输出service3");
    }
    /**
     * 私有方法
     */
    private void service4(){
        System.out.println("私有方法输出service4");
    }
    /**
     * 私有静态方法
     */
    private static void service5(){
        System.out.println("私有静态方法输出service5");
    }
 }
```

- 含有抽象方法

  抽象方法：使用 abstract 关键字修饰，可以省略，没有方法体。该方法供子类实现使用。

- 含有默认方法

  默认方法：使用 default 修饰，不可省略，供子类调用或者子类重写。 

- 含有静态方法

  静态方法：使用 static 修饰，供接口直接调用。

- 含有私有方法

  私有方法：使用 private 修饰，只供接口中的默认方法调用。

- 含有私有静态方法
  私有静态方法：使用private和static修饰，供接口中的默认方法和静态方法调用。

## 16.3 基本的实现

- 实现：类与接口的关系为实现关系，即**类实现接口**，该类可以称为接口的实现类，也可以称为接口的子类。实现的动作类 似继承，格式相仿，只是关键字不同，实现使用 implements 关键字。

  非抽象子类实现接口：

  1. 必须重写接口中所有抽象方法。 
  2. 继承了接口的默认方法，即可以直接调用，也可以重写。

  实现格式：

  ```java
  class 类名 implements 接口名 {     
  	// 重写接口中抽象方法【必须】    
  	// 重写接口中默认方法【可选】   
  } 
  ```

- 抽象方法的使用

  所有抽象方法必须全部实现。

- 默认方法的使用

  可以继承，可以重写，二选一，但是只能通过实现类的对象来调用。

  - [ ] 继承默认方法

  ```java
  //定义接口
  public interface IUSB {
      /**
       * 默认方法
       */
      public default void service2(){
          System.out.println("默认方法输出service2");
      }
  }
  //定义实现类
  public class UDISK implements IUSB{
     @Override
      public void service2() {
      	//继承，什么都不用写，直接调用
      }
  }
  //测试类
  public class test {
      public static void main(String[] args) {
        	IUSB iusb = new UDISK();
          iusb.service2();
      }
  }
  输出结果：
  默认方法输出service2
  ```

  - [ ] 重写默认方法

  ```java
  //定义接口
  public interface IUSB {
      /**
       * 默认方法
       */
      public default void service2(){
          System.out.println("默认方法输出service2");
      }
  }
  //定义实现类
  public class UDISK implements IUSB{
     @Override
      public void service2() {
      	//方法重写
      	System.out.println("重写默认方法输出service2");
      }
  }
  //测试类
  public class test {
      public static void main(String[] args) {
        	IUSB iusb = new UDISK();
        	//调用重写的默认方法
          iusb.service2();
      }
  }
  输出结果：
  重写默认方法输出service2
  ```

- 静态方法的使用

  静态与.class 文件相关，只能使用接口名调用，不可以通过实现类的类名或者实现类的对象调用。


  ```java
  //定义接口
  public interface IUSB {
      /**
       * 静态方法
       */
      public static void service3(){
          System.out.println("静态方法输出service3");
      }
  }
  //定义实现类
  public class UDISK implements IUSB{
    //无法重写静态方法
  }
  //测试类
  public class test {
      public static void main(String[] args) {
        	//UDISK.service3();错误，无法继承方法，也无法调用。
          IUSB.service3();
      }
  }
  输出结果：
  静态方法输出service3
  ```

- 私有方法的使用

  - [ ] 私有方法：只有默认方法可以调用。 
  - [ ] 私有静态方法：默认方法和静态方法可以调用。

  ```java
  //定义接口
  public interface IUSB {
   	/**
      * 默认方法
       */
      public default void service2(){
          System.out.println("默认方法输出service2");
          service4();
          service5();
      }
      /**
       * 静态方法
       */
      public static void service3(){
          System.out.println("静态方法输出service3");
          service5();
      }
      /**
       * 私有方法
       */
      private void service4(){
          System.out.println("私有方法输出service4");
      }
      /**
       * 私有静态方法
       */
      private static void service5(){
          System.out.println("私有静态方法输出service5");
      }
  }
  ```

## 16.4 接口的多实现

- 多实现：在继承体系中，一个类只能继承一个父类。而对于接口而言，**一个类是可以实现多个接口**的，这叫做接口的多实现。并且，**一个类能继承一个父类，同时实现多个接口**。

  实现格式:

  ```java
  class 类名 [extends 父类名] implements 接口名1,接口名2,接口名3... {     
  	// 重写接口中抽象方法【必须】    
  	// 重写接口中默认方法【不重名时可选】    
  }
  ```

  >[ ]： 表示可选操作。

- 抽象方法 

  接口中，有多个抽象方法时，实现类必须重写所有抽象方法。**如果抽象方法有重名的，只需要重写一次。**


  ```java
  //定义多个接口
  interface A {     
  	public abstract void showA();     
  	public abstract void show(); 
  }   
  interface B {     
  	public abstract void showB();     
  	public abstract void show(); 
  }
  //定义实现类
  public void C implements A,B{
   	@Override     
   	public void showA() {         
   		System.out.println("showA");     
   	}       
   	@Override     
   	public void showB() {         
   		System.out.println("showB");     
   	}       
   	@Override     
   	public void show() {         
   		System.out.println("show");     //重名抽象方法只用重写一次
   	} 
  }
  ```

- 默认方法

  接口中，有多个默认方法时，实现类都可继承使用。**如果默认方法有重名的，必须重写一次。**

  ```java
  //定义多个接口
  interface A {     
  	public default void showA();     
  	public default void show(); 
  }   
  interface B {     
  	public default void showB();     
  	public default void show(); 
  }
  //定义实现类
  public void C implements A,B{
   	@Override     
   	public void showA() {         
   		System.out.println("showA");     
   	}       
   	@Override     
   	public void showB() {         
   		System.out.println("showB");     
   	}       
   	@Override     
   	public void show() {         
   		System.out.println("show");   //重名默认方法必须重写  
   	} 
  }
  ```

- 静态方法

  接口中，存在同名的静态方法并不会冲突，原因是只能通过各自接口名访问静态方法。 

- 优先级问题

  当一个类，既继承一个父类，又实现若干个接口时，父类中的成员方法与接口中的默认方法重名，子类就近选择执行父类的成员方法。


  ```java
  //定义接口
  interface A {    
  	 public default void methodA(){         
  	 	System.out.println("AAAAAAAAAAAA");     
  	 } 
  }
  //定义父类
  class D {     
  	public void methodA(){         
  		System.out.println("DDDDDDDDDDDD");     
  	} 
  }
  //定义子类
  class C extends D implements A {   
  	 // 未重写methodA方法   
  }
  //定义测试类
  public class Test {     
  	public static void main(String[] args) {         
  		C c = new C();         
  		c.methodA();      
  	} 
  } 
  输出结果: 
  DDDDDDDDDDDD
  ```

## 16.5 接口的多继承

一个接口能继承另一个或者多个接口，这和类之间的继承比较相似。接口的继承使用 extends 关键字，子接口继承父接口的方法。**如果父接口中的默认方法有重名的，那么子接口需要重写一次**。

```java
//定义父接口
interface A {     
	public default void method(){         
		System.out.println("AAAAAAAAAAAAAAAAAAA");     
	}
}   
interface B {     
	public default void method(){         
		System.out.println("BBBBBBBBBBBBBBBBBBB");     
	} 
}
//定义子接口
interface D extends A,B{     
	@Override     
	public default void method() {         
		System.out.println("DDDDDDDDDDDDDD");     
	} 
}
```

>小贴士：
>子接口重写默认方法时，default关键字可以保留。 
>子类重写默认方法时，default关键字不可以保留。 

## 16.6 其他成员特点

- 接口中，无法定义成员变量，但是可以定义常量，其值不可以改变，默认使用public static ﬁnal修饰。 

  ```java
  //默认是一个静态常量，不可以被修改
  (static final) int age = 20;
  ```

- 接口中，没有构造方法，不能创建对象。

  ```java
  //① 通过new其实现类来创建
  IUSB iusb = new UDISK();
  //② 用匿名接口重写抽象方法实现
  IUSB iusb = new IUSB() {
          @Override
           public void service1() {
               System.out.println("USB正在工作");
           }
       };
       iusb.service1();
  ```


- 接口中，没有静态代码块。 

# 十七、多态

## 17.1 概述

- 定义
  多态： 是指同一行为，具有多个不同表现形式。
- 前提

1. 继承或者实现【二选一】 
2. 方法的重写【意义体现：不重写，无意义】 
3. 父类引用指向子类对象【格式体现】 

## 17.2 多态的体现

多态体现的格式：

```java
父类类型 变量名 = new 子类对象； 
变量名.方法名();
例：
Fu f = new Zi(); 
f.method()
```

>父类类型：指子类对象继承的父类类型，或者实现的父接口类型。
>当使用多态方式调用方法时，首先检查父类中是否有该方法，如果没有，则编译错误；如果有，执行的是子类重写后的方法。

```java
//定义父类
public abstract class Animal {       
	public abstract void eat();   
}
//定义子类
class Cat extends Animal {       
	public void eat() {           
		System.out.println("吃鱼");       
	}   
}     
class Dog extends Animal {       
	public void eat() {           
		System.out.println("吃骨头");       
	}  
}
//测试类
public class Test {     
	public static void main(String[] args) {         
		// 多态形式，创建对象         
		Animal a1 = new Cat();           
		// 调用的是 Cat 的 eat         
		a1.eat();                     
		
		// 多态形式，创建对象         
		Animal a2 = new Dog();          
		// 调用的是 Dog 的 eat         a2.eat();                    
	}   
}

```

## 17.3 多态的好处

实际开发的过程中，父类类型作为方法形式参数，传递子类对象给方法，进行方法的调用，更能体现出多态的扩展 性与便利。

```java
//定义父类
public abstract class Animal {       
	public abstract void eat();   
}
//定义子类
class Cat extends Animal {       
	public void eat() {           
		System.out.println("吃鱼");       
	}   
}     
class Dog extends Animal {       
	public void eat() {           
		System.out.println("吃骨头");       
	}  
}
//定义测试类
public class Test {     
	public static void main(String[] args) {         
		// 多态形式，创建对象         
		Cat c = new Cat();           
		Dog d = new Dog();            
		// 调用showCatEat         
		showCatEat(c);        
		 // 调用showDogEat 
		 showDogEat(d);            
		 /*         
		 以上两个方法, 均可以被showAnimalEat(Animal a)方法所替代,而执行效果一致         
		 */         		
		 showAnimalEat(c);         
		 showAnimalEat(d);      
	 }      
	  public static void showCatEat (Cat c){         
	  	c.eat();      
	  }      
	  public static void showDogEat (Dog d){         
	  	d.eat();     
	  }       
	  public static void showAnimalEat (Animal a){         
	  	a.eat();     
	  } 
}
```

## 17.4 引用类型转换

- 多态的转型分为向上转型与向下转型两种。

  - [ ] 向上转型

    向上转型：多态本身是子类类型向父类类型向上转换的过程，这个过程是默认的。
    **当父类引用指向一个子类对象时，便是向上转型。**

    使用格式：

    ```java
    父类类型  变量名 = new 子类类型(); 
    如：Animal a = new Cat();
    ```

  - [ ] 向下转型

    向下转型：父类类型向子类类型向下转换的过程，这个过程是强制的。
    一个已经向上转型的子类对象，**将父类引用转为子类引用**，可以使用强制类型转换的格式，**便是向下转型**。

    使用格式：

    ```java
    子类类型 变量名 = (子类类型) 父类变量名; 
    如:Cat c =(Cat) a;
    ```

- 为什么要转型？

  当使用多态方式调用方法时，首先检查父类中是否有该方法，如果没有，则编译错误。也就是说，不能调用子类拥 有，而父类没有的方法。编译都错误，更别说运行了。这也是多态给我们带来的一点"小麻烦"。所以，想要调用子 类特有的方法，必须做向下转型。

  ```java
  //定义类
  abstract class Animal {       
  	abstract void eat();   
  }     
  class Cat extends Animal {       
  	public void eat() {           
  		System.out.println("吃鱼");       
  	}       
  	public void catchMouse() {           
  		System.out.println("抓老鼠");       
  	}   
  }     
  class Dog extends Animal {       
  	public void eat() {           
  		System.out.println("吃骨头");       
  	}      
  	public void watchHouse() {           
  		System.out.println("看家");       
  	}   
  }
  //定义测试类
  public class Test {     
  	public static void main(String[] args) {         
  		// 向上转型           
  		Animal a = new Cat();           
  		a.eat();  // 调用的是 Cat 的 eat                           
  		// 向下转型           
  		Cat c = (Cat)a;               
  		c.catchMouse();  // 调用的是 Cat 的 catchMouse              }  
  }
  ```

- 转型的异常

  ```java
  public class Test {     
  	public static void main(String[] args) {         
  		// 向上转型           
  		Animal a = new Cat();           
  		a.eat();               // 调用的是 Cat 的 eat           
  		// 向下转型           
  		Dog d = (Dog)a;                
  		d.watchHouse();        // 调用的是 Dog 的 watchHouse 【运行报错】     
  	}   
  }
  ```

  这段代码可以通过编译，但是运行时，却报出了 ClassCastException ，类型转换异常！这是因为，明明创建了 Cat类型对象，运行时，当然不能转换成Dog对象的。这两个类型并没有任何继承关系，不符合类型转换的定义。 为了避免ClassCastException的发生，Java提供了 instanceof 关键字，给引用变量做类型的校验，格式如下：

  ```java
  变量名 instanceof 数据类型  
  如果变量属于该数据类型，返回true。 
  如果变量不属于该数据类型，返回false
  ```

  所以，转换前，我们好先做一个判断。

