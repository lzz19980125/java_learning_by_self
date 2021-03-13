# java程序基础

#### 常用java术语

|          术语名          | 缩写 |                   解释                    |
| :----------------------: | :--: | :---------------------------------------: |
|   java development kit   | JDK  |      编写java程序的程序员使用的软件       |
| java runtime environment | JRE  |       运行java程序的用户使用的软件        |
|     standard edition     |  SE  |   用于桌面或简单的服务器应用的java平台    |
|    enterprise edition    |  EE  |      用于复杂的服务器应用的java平台       |
| software development kit | SDK  | 一个过时术语，用于描述1998年至2006年的JDK |

#### 典型java程序结构

1. 一个典型的java程序结构为：

   ```java
   public class Hello {
       public static void main(String[] args) {
           System.out.println("Hello,world!");
       }
   }
   ```

2. **注意：以上这段代码所对应的文件名必须定义为：`Hello.java`    即：java文件的文件名必须与文件中所包含的`public`类名相同！**

3. 一个程序的基本单位为类，即`class `。类名的定义要求：***习惯以大写字母开头***。

   `public` 为访问修饰符，表示`class` 是公开的，不写`public` ，也可以正确编译，但此类将无法从命令行执行。

   `class` 内部可以定义诸多method ，这里的method为`main` ，**`main`方法必须声明为`public`，且必须是`static`的**，返回值为`void` ,表示没有任何返回值。

   method的命名与class类似，只不过通常用小写开头。`static` 为静态方法修饰符，此方法括号内的参数必须为`String[]` ,即字符串数组

#### 注释

1. 最常用的方法是使用`//`，其注释内容从`//`开始到本行结尾。
2. 当需要长篇的注释时，既可以在每行的注释前面标记`//`，也可以使用`/*`和`*/`将一段比较长的注释括起来。
3. 第三种注释可以用来自动的生成文档。这种注释以`/**`开始，以`*/`结束。


#### java数据类型

整形（略）

<img src="https://github.com/lzz19980125/java_learning_by_self/blob/main/java%E7%A8%8B%E5%BA%8F%E5%9F%BA%E7%A1%80/figures/2021-02-20_105457.PNG?raw=true" alt="数据类型" style="zoom:67%;" />



常量：

定义变量时，如果假如`final`修饰符，则变为常量。根据习惯，常量名定义全部采用大写。

```java
final double PI =3.14;
```

#### java 运算

**整数运算**：*即使是除法也永远是精确的，因为两个数相除只能够得到整数的部分。整数运算除了整除与取余操作之外，还提供自增以及自减操作。

```java
int x =12345/67;
System.out.println("x="+x);
int y =12345%67;
System.out.println("y="+y);
x++;
y--;
```

<img src="https://github.com/lzz19980125/java_learning_by_self/blob/main/java%E7%A8%8B%E5%BA%8F%E5%9F%BA%E7%A1%80/figures/2021-02-20_110626.PNG?raw=true" alt="运算" style="zoom:67%;" />

**布尔运算：**

布尔运算符包括：

<img src="https://github.com/lzz19980125/java_learning_by_self/blob/main/java%E7%A8%8B%E5%BA%8F%E5%9F%BA%E7%A1%80/figures/2021-02-21_192629.PNG?raw=true" alt="布尔运算" style="zoom:67%;" />

**短路运算**（两个条件相与，则前一个假，后一个不判断，整个都假；两个条件相或反之一样）

```java
public class Hello {
    public static void main(String[] args) {
        boolean b = false;
        if (b && 5/0>5){
            System.out.println("真的");
        }
    }
}
```

如果没有短路运算，则上述会报错（因为除数为0了）

**三元运算符**：

```java
public class Hello {
    public static void main(String[] args) {
        int b = 5>2 ? 100:2;
        System.out.println(b);
    }
}
```

**字符与字符串的常见操作：**

常见转义字符：

<img src="https://github.com/lzz19980125/java_learning_by_self/blob/main/java%E7%A8%8B%E5%BA%8F%E5%9F%BA%E7%A1%80/figures/%E6%9C%AA%E5%91%BD%E5%90%8D%E5%9B%BE%E7%89%87.png?raw=true" alt="常见转义字符" style="zoom:67%;" />

通常用方法`equals`检测字符串是否相等，一定不能够使用`==`检测两个字符串是否相等！

```java
s.equals(t)
```

字符串拼接：

```java
public class Hello {
    public static void main(String[] args) {
        String a ="hello";
        String b ="world";
        String c =a+" "+b+"!";
        System.out.println(c);
        int d =25;
        System.out.println(c+" "+d);
    }
}
```

多行字符串：

```java
public class Hello {
    public static void main(String[] args) {
        String a = """
                大家好，我是小蜜蜂！
                大家好，我是小蝴蝶！
                大家好，我是小狐狸！
                """;
        System.out.println(a);
    }
}
```

字符串空值：

```java
public class Hello {
    public static void main(String[] args) {
        String a =null;
        String b ="";
        String c =a;
    }
}
```

#### 数组

##### 一维数组

**一维数组的定义方式**

<img src="https://github.com/lzz19980125/java_learning_by_self/blob/main/java%E7%A8%8B%E5%BA%8F%E5%9F%BA%E7%A1%80/figures/%E6%9C%AA%E5%91%BD%E5%90%8D%E5%9B%BE%E7%89%87123.png?raw=true" alt="一维数组的定义方式" style="zoom:67%;" />

定义整数以及字符串数组的几种方式：

```java
public class Hello {
    public static void main(String[] args) {
        int [] a =new int [5];
        a[0] =1;
        a[1] =2;
        a[2] =3;
        a[3] =4;
        a[4] =5;
        int [] b =new int [] {1,2,3,4,5};
        int [] c ={1,2,3,4,5};
        String [] p =new String [5];
    }
}
```

可以通过`数组变量.length`来获取数组的长度

**一维数组的基本操作**

* 专门针对数组的遍历循环

```java
public class Hello {
    public static void main(String[] args) {
        int [] a = new int [5];
        for (int i:a){
            System.out.printf("%d\n",i);
        }
    }
}
```

* 遍历一维数组并且打印所有值

```java
import java.util.Arrays;
public class Hello {
    public static void main(String[] args) {
        int [] a ={1,2,3,4,5};
        System.out.printf("遍历一维数组值并打印为："+Arrays.toString(a)+"\n");
    }
}
```

* 冒泡排序

```java
import java.util.Arrays;

public class Hello {
    public static void main(String[] args) {
        int [] a ={3,6,4,2,11,10,5};
        for (int i=0;i<a.length-1;i++){
            //一共要冒n-1个泡
            for (int j=0;j<a.length-1-i;j++){
                //每有一个泡浮出水面，就少遍历一次
                if (a[j]<a[j+1]){
                    int temp =a[j];
                    a[j]=a[j+1];
                    a[j+1]=temp;
                }
            }
        }
        System.out.printf("经过排序后的数组："+Arrays.toString(a)+"\n");
    }
}
```

冒泡排序的特点是，每一轮循环后，最大的一个数被交换到末尾，因此，下一轮循环就可以“刨除”最后的数，每一轮循环都比上一轮循环的结束位置靠前一位。

* 以上的排序功能可通过JDK中内置的排序函数实现，直接调用即可

```java
import java.util.Arrays;

public class Hello {
    public static void main(String[] args) {
        int [] a ={3,6,4,2,11,10,5};
        System.out.printf("未经排序的数组为："+Arrays.toString(a)+"\n");
        Arrays.sort(a);
        System.out.printf("经过排序的数组为："+Arrays.toString(a)+"\n");
    }
}
```

##### 二维数组

**二维数组的定义**

```java
public class Hello {
    public static void main(String[] args) {
        int [][] a ={
                {3,6,4,2,11,10,5},
                {1,2,3,4,5,6,7},
                {7,6,5,4,3,2,1}
        };
    }
}
```

**二维数组的遍历**

```java
public class Hello {
    public static void main(String[] args) {
        int [][] a = {
                {1,2,3,4,5},
                {6,7,8,9,10},
                {11,12,13,14,15}
        };
        for (int [] s :a){
            for (int b:s){
                System.out.printf(b+" ");
            }
            System.out.println();
        }
    }
}
```

**二维数组的遍历以及打印**

```java
import java.util.Arrays;

public class Hello {
    public static void main(String[] args) {
        int [][] a = {
                {1,2,3,4,5},
                {6,7,8,9,10},
                {11,12,13,14,15}
        };
        System.out.println(Arrays.deepToString(a));
    }
}
```

例子：涉及到二维数组的逐行打印，以及二维数组的行和列如何索引：





#### IO流

* 输入（即`print()`,`printf()`,`println)()`等函数的使用，略）
* 输出：

java的输出比较复杂：

<img src="https://github.com/lzz19980125/java_learning_by_self/blob/main/java%E7%A8%8B%E5%BA%8F%E5%9F%BA%E7%A1%80/figures/%E6%9C%AA%E5%91%BD%E5%90%8D%E5%9B%BE%E7%89%87456.png?raw=true" alt="java输出" style="zoom:67%;" />

```java
import java.util.Scanner;

public class Hello {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.printf("please input your name");
        String name =scanner.nextLine();
        System.out.printf("please input your age");
        int age = scanner.nextInt();
        System.out.printf("your name is %s and your age is %d ",name,age);
    }
}
```

#### 命令行参数

<img src="https://github.com/lzz19980125/java_learning_by_self/blob/main/java%E7%A8%8B%E5%BA%8F%E5%9F%BA%E7%A1%80/figures/2021-02-22_125433.PNG?raw=true" alt="命令行参数" style="zoom:67%;" />

```java
public class Hello {
    public static void main(String[] args) {
        for (String arg :args){
            if("-version".equals(arg)){
                System.out.println("v 1.0");
            }
        }
    }
}
```

程序在terminal操纵运行结果为：

<img src="https://github.com/lzz19980125/java_learning_by_self/blob/main/java%E7%A8%8B%E5%BA%8F%E5%9F%BA%E7%A1%80/figures/%E6%9C%AA%E5%91%BD%E5%90%8D%E5%9B%BE%E7%89%87344.png?raw=true" alt="terminal" style="zoom:67%;" />

#### 流程控制

##### if结构

```java
public class Hello {
    public static void main(String[] args) {
        int score = 90;
        if (score>90){
            System.out.println("优秀！");
        } else if(score>60){
            System.out.println("及格！");
        } else {
            System.out.println("不及格！");
        }
        System.out.println("结束判断！");
    }
}
```

* 浮点数比较

```java
public class Hello {
    public static void main(String[] args) {
        double a=0.1;
        double b =1-9.0/10;
        if (Math.abs(a-b)<0.00001){
            System.out.printf("%f与%f相等",a,b);
        } else{
            System.out.printf("两数不相等！");
        }
    }
}
```

* 判断引用类型是否相等

```java
public class Hello {
    public static void main(String[] args) {
        String a ="hello";
        String b ="HELLO".toLowerCase();
        System.out.printf("a的值为%s\n",a);
        System.out.printf("b的值为%s\n",b);
        if (b!= null && b.equals(a)){
            System.out.printf("引用类型a与b相等\n");
        }
    }
}
```

##### switch选择结构

```java
public class Hello {
    public static void main(String[] args) {
        String a ="banana";
        int b = switch(a){
            case "banana" -> 2;
            case "1" -> 3;
            default -> 0;
        };
        System.out.printf("b的值为：%d",b);
    }
}
```

* switch中`yield`的用法

```java
public class Hello {
    public static void main(String[] args) {
        String a ="banana";
        int b = switch(a){
            case "1" -> 2;
            case "banana" -> {
                System.out.println("大家好，我是小蜜蜂！");
                System.out.println("大家好，他是小蝴蝶！");
                yield 1;
            }
            default -> 0;
        };
        System.out.printf("b的值为：%d",b);
    }
}
```

##### while循环

```java
import java.util.Scanner;

public class Hello {
    public static void main(String[] args) {
        Scanner scanner =new Scanner(System.in);
        System.out.println("please input the value of m  ");
        int m = scanner.nextInt();
        System.out.println("please input the value of n  ");
        int n =scanner.nextInt();
        int sum =0;
        while(m<=n){
            sum += m;
            m++;
        }
        System.out.printf("the sum of m~n is %d",sum);
    }
}
```

##### do while 循环

```java
import java.util.Scanner;

public class Hello {
    public static void main(String[] args) {
        Scanner scanner =new Scanner(System.in);
        System.out.println("please input the value of m  ");
        int m = scanner.nextInt();
        System.out.println("please input the value of n  ");
        int n =scanner.nextInt();
        int sum =0;
        do {
            sum += m;
            m++;
        } while(m<=n);
        System.out.printf("the sum of m~n is %d",sum);
    }
}
```

##### for循环

```java
import java.util.Scanner;

public class Hello {
    public static void main(String[] args) {
        Scanner scanner =new Scanner(System.in);
        System.out.println("please input the value of m  ");
        int m = scanner.nextInt();
        System.out.println("please input the value of n  ");
        int n =scanner.nextInt();
        int sum =0;
        for (;m<=n;m++){
            sum +=m;
        }
        System.out.printf("the sum of m~n is %d",sum);
    }
}
```

