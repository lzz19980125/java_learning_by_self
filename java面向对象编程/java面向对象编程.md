# java面向对象编程

#### 面向对象基础

```java
public class Hello {
    public static void main(String[] args) {
        Person person = new Person() ;
        person.name = "小蜜蜂";
        person.age = 18;
        System.out.println("person's name is "+person.name);
    }
    static class Person{
        public String name;
        public int age;
    }
}
```

上面定义了一个`class`，名为Person，而Person类中有两个`field`(也可以理解为属性)，分别是name以及age。`public`用来修饰字段，它代表两个字段都可以被外部访问。直接把`field`暴露给外部会破坏掉它的封装性（外部可以随意访问和修改`field`）。为平衡字段的私有性以及可访问与修改性，我们定义`private`类型的`field` ，以及定义相应`field`的访问以及修改方法。

#### 方法

```java
public class Hello {
    public static void main(String[] args) {
        Person person1= new Person();
        person1.setName("小蜜蜂");
        person1.setBorn_year(1972);
        System.out.printf("person1的个人信息：姓名：%s，出生年月：%d，年龄：%d",
                person1.getName(),person1.getBorn_year(),person1.getAge());
    }
    static class Person{
        private String name;
        private int age;
        private int born_year;

        public String getName(){
            return this.name;
        }
        public void setName(String name){
            if (name == null || name.isBlank()){
                throw new IllegalArgumentException("invalid name");
            }
            this.name = name.strip(); // 去掉首尾空格
        }
        public int getAge(){
            return caculateAge(this.born_year);
        }
        public int getBorn_year(){
            return this.born_year;
        }
        public void setBorn_year(int born_year){
            this.born_year = born_year;
        }
        private int caculateAge(int born_year){
            if (2021-born_year < 0 || 2021-born_year >100){
                throw new IllegalArgumentException ("invalid age value");
            }
            return 2021-born_year;
        }
    }
}
```

在方法内部，可以使用隐含变量`this`，它始终指向当前的实例。

`yield`以及`method`都需要用`public`以及`private`进行声明。

##### 方法参数

方法可以包含0个或任意个参数。方法参数用于接收传递给方法的变量值。调用方法时，必须严格按照参数的定义一一传递。例如：

```java
class Person {
    ...
    public void setNameAndAge(String name, int age) {
        ...
    }
}
```

调用这个`setNameAndAge()`方法时，必须有两个参数，且第一个参数必须为`String`，第二个参数必须为`int`：

```java
Person ming = new Person();
ming.setNameAndAge("Xiao Ming"); // 编译错误：参数个数不对
ming.setNameAndAge(12, "Xiao Ming"); // 编译错误：参数类型不对
```

##### 可变参数以及参数绑定

###### 可变参数

可变参数用`类型...`定义，可变参数相当于数组类型：

```java
import java.util.Arrays;

public class Hello {
    public static void main(String[] args) {
    Person person = new Person();
    person.setNames("小蜜蜂", "小蝴蝶");
    System.out.println(Arrays.toString(person.getNames()));
    }
    static class Person{
        private String [] names;
        public void setNames(String ... names ){
            this.names = names;
        }
        public String [] getNames(){
            return this.names;
        }
    }
}
```

同样可以将`setNames`方法中参数由可变参数设置为字符数组类型，则`setNames`传入参数时也需要更改，并且此种定义方法不允许传入`Null`：

```java
import java.util.Arrays;

public class Hello {
    public static void main(String[] args) {
    Person person = new Person();
    person.setNames(new String [] {"小蜜蜂","小蝴蝶","小鲸鱼"});
    System.out.println(Arrays.toString(person.getNames()));
    }
    static class Person{
        private String [] names;
        public void setNames(String [] names ){
            this.names = names;
        }
        public String [] getNames(){
            return this.names;
        }
    }
}
```

###### 参数绑定（分为基本类型的参数绑定与引用类型的参数绑定）

###### （这个地方还不是很明白）

##### 构造方法

为实现在初始化创建对象实例时就将对象全部的属性赋予给它，引入了构造方法。

由于构造方法是如此特殊，所以构造方法的名称就是类名。构造方法的参数没有限制，在方法内部，也可以编写任意语句。但是，和普通方法相比，构造方法没有返回值（也没有`void`），调用构造方法，必须用`new`操作符。

是不是任何`class`都有构造方法？是的。

要特别注意的是，如果我们自定义了一个构造方法，那么，编译器就*不再*自动创建默认构造方法。

如果既要能使用带参数的构造方法，又想保留不带参数的构造方法，那么只能把两个构造方法都定义出来。

可以定义多个构造方法，在通过`new`操作符调用的时候，编译器通过构造方法的参数数量、位置和类型自动区分。

一个构造方法可以调用其他构造方法，这样做的目的是便于代码复用。调用其他构造方法的语法是`this(…)`。

```java
public class Hello {
    public static void main(String[] args) {
    Person person1 = new Person("小蜜蜂",24);
    Person person2 = new Person();
    System.out.printf("person1的名字是：%s, person1的年龄是：%d\n",person1.getName(),person1.getAge());
    System.out.printf("person2的名字是：%s, person2的年龄是：%d\n",person2.getName(),person2.getAge());
    }
    static class Person{
        private String name = "unnamed";
        private int age = 18;
        public Person(String name , int age){
            this.name = name;
            this.age = age;
        }
        public Person(String name){
            this(name,18);
        }
        public Person(){
            this("unnamed");
        }
        public String getName(){
            return this.name;
        }
        public int getAge(){
            return this.age;
        }
        public void setName(String name){
            this.name = name;
        }
        public void setAge(int age){
            this.age = age;
        }
    }
}
```

##### 方法重载

```java
public class Hello {
    public static void main(String[] args) {
    Person person1 = new Person("小蜜蜂",24);
    person1.hello();
    person1.hello(person1.age);
    person1.hello("女",person1.age);
    }
    static class Person{
        private String name = "unnamed";
        private int age = 18;
        public Person(String name , int age){
            this.name = name;
            this.age = age;
        }
        public Person(String name){
            this(name,18);
        }
        public Person(){
            this("unnamed");
        }
        public String getName(){
            return this.name;
        }
        public int getAge(){
            return this.age;
        }
        public void setName(String name){
            this.name = name;
        }
        public void setAge(int age){
            this.age = age;
        }
        public void hello(){
            System.out.println("大家好，我是小蜜蜂！");
        }
        public void hello(int age){
            System.out.printf("大家好，我是小蜜蜂！ 蜜蜂的年龄是%d\n",age);
        }
        public void hello(String sex , int age){
            System.out.printf("大家好，我是小蜜蜂，我的性别是%s,我的年龄是%d\n",sex,age);
        }
    }
}
```

在一个类中，我们可以定义多个方法。如果有一系列方法，它们的功能都是类似的，只有参数有所不同，那么，可以把这一组方法名做成*同名*方法。例如，在`Hello`类中，定义多个`hello()`方法。

这种方法名相同，但各自的参数不同，称为方法重载（`Overload`）。

注意：方法重载的返回值类型通常都是相同的。

方法重载的目的是，功能类似的方法使用同一名字，更容易记住，因此，调用起来更简单。

#### 继承

Java使用`extends`关键字来实现继承。

***注意：子类自动获得了父类的所有字段，严禁定义与父类重名的字段！***

在OOP的术语中，我们把`Person`称为超类（super class），父类（parent class），基类（base class），把`Student`称为子类（subclass），扩展类（extended class）。

Java只允许一个class继承自一个类，因此，一个类有且仅有一个父类。只有`Object`特殊，它没有父类。

继承有个特点，就是子类无法访问父类的`private`字段或者`private`方法。例如，`Student`类就无法访问`Person`类的`name`和`age`字段。这使得继承的作用被削弱了。为了让子类可以访问父类的字段，我们需要把`private`改为`protected`。用`protected`修饰的字段可以被子类访问。因此，`protected`关键字可以把字段和方法的访问权限控制在继承树内部。

```java
public class Hello {
    public static void main(String[] args) {
        Person person1 = new Person("小蜜蜂",18);
        System.out.printf("person1的名字为：%s， person1的年龄为：%d\n",person1.getName(),person1.getAge());
        Student student1 = new Student(person1.name,person1.age,100);
        System.out.printf("student1的名字为：%s，student1的年龄为：%d，student1的分数为：%d\n",student1.getName(),student1.getAge(),student1.getScore());
    }
    static  class Person {
        protected String name;
        protected int age;
        public  Person(String name, int age){
            this.age = age;
            this.name = name;
        }
        public void setName(String name){
            this.name = name;
        }
        public String getName(){
            return this.name;
        }
        public void setAge(int age){
            this.age = age;
        }
        public int getAge(){
            return this.age ;
        }
    }
    static  class Student extends Person{
        protected int score;
        public Student(String name,int age,int score){
            super(name,age); 
            this.score = score;
        }
        public void setScore(int score){
            this.score = score;
        }
        public int getScore(){
            return this.score;
        }
    }
}
```

`super`关键字表示父类（超类）。子类引用父类的字段时，可以用`super.fieldName`。

一般情况下，使用`super.name`，或者`this.name`，或者`name`，效果都是一样的。编译器会自动定位到父类的`name`字段。但在某些情况下，必须使用`super`关键字。在Java中，任何`class`的构造方法，第一行语句必须是调用父类的构造方法。如果没有明确地调用父类的构造方法，编译器会帮我们自动加一句`super();`但是，`Person`类并没有无参数的构造方法，因此有此结构才能够正常编译：

```java
 public Student(String name,int age,int score){
        super(name,age); 
 }
```

因此我们得出结论：如果父类没有默认的构造方法，子类就必须显式调用`super()`并给出参数以便让编译器定位到父类的一个合适的构造方法。

这里还顺带引出了另一个问题：即子类*不会继承*任何父类的构造方法。子类默认的构造方法是编译器自动生成的，不是继承的。

##### 向上转型与向下转型

* 向上转型（你是学生，就一定是人（有名字，有年龄））：

```java
Student student1 = new Student(person1.name,person1.age,100);
System.out.printf("student1的名字为：%s，student1的年龄为：%d，student1的分数为：		    
                  %d\n",student1.getName(),student1.getAge(),student1.getScore());
Person student2 = student1;
System.out.printf("student2的名字为：%s，student2的年龄为：%d\n",student2.getName(),student2.getAge());
```

* 向下转型（你是人，但不一定是学生（有名字，有年龄，但不一定有分数））：

```java
public class Hello {
    public static void main(String[] args) {
        Person person1 = new Person("小蜜蜂",18);
        System.out.printf("person1的名字为：%s， person1的年龄为：%d\n",person1.getName(),person1.getAge());
        Student student1 = new Student(person1.name,person1.age,100);
        System.out.printf("student1的名字为：%s，student1的年龄为：%d，student1的分数为：%d\n",student1.getName(),student1.getAge(),student1.getScore());
        Student student2 = new Student();
        if(student2 instanceof Person person2){
            System.out.printf("person2的名字为：%s，person2的年龄为：%d\n",person2.getName(),person2.getAge());
        }
    }
    static class Person {
        protected String name;
        protected int age;
        public Person(){
            this.age = 99;
            this.name = "Alex";
        }
        public  Person(String name, int age){
            this.age = age;
            this.name = name;
        }
        public void setName(String name){
            this.name = name;
        }
        public String getName(){
            return this.name;
        }
        public void setAge(int age){
            this.age = age;
        }
        public int getAge(){
            return this.age ;
        }
    }
    static  class Student extends Person{
        protected int score;
        public Student(){
            this.score = 60;
        }
        public Student(String name,int age,int score){
            super(name,age);
            this.score = score;
        }
        public void setScore(int score){
            this.score = score;
        }
        public int getScore(){
            return this.score;
        }
    }
}
```

为了避免向下转型出错，Java提供了`instanceof`操作符，可以先判断一个实例究竟是不是某种类型：

`instanceof`实际上判断一个变量所指向的实例是否是指定类型，或者这个类型的子类。如果一个引用变量为`null`，那么对任何`instanceof`的判断都为`false`。从Java 14开始，判断`instanceof`后，可以直接转型为指定变量，避免再次强制转型。

#### 多态

多态的特性是：运行期才能动态决定调用的子类方法。对某个类型调用某个方法，执行的实际方法可能是某个子类的覆写方法。

```java
public class Hello {
    public static void main(String[] args) {
        Person person = new Student();
        person.run();
        }
    }
      class Person {
        public Person(){}
        public void run(){
            System.out.println("Person.run");
        }
    }
      class Student extends Person{
        public Student(){}
        @Override
        public void run(){
            System.out.println("Student.run");
        }
    }
```

以下为计算一个人的三种收入的代码实例（此人共有三种收入：1.普通收入，所有普通收入征收百分之二十的税务；2.工资收入，工资收入大于5000的按百分之二十征税；3.国务院特殊津贴：此部分不征收税务）

```java
public class Hello {
    public static void main(String[] args) {
        Income [] totalincome = new Income [] {
                new Income(3000),
                new Salary(7500),
                new StateCouncilSpecialAllowance(15000)
        };
        System.out.printf("此人的总征税额为：%.2f\n",caculateTax(totalincome));
    }
    public static double caculateTax(Income ... totalTax){
        double total = 0;
        for (Income incomes : totalTax){
            total += incomes.getTax();
        }
        return total;
    }
}
    class Income{  //普通收入，全部普通收入征收百分之十的税务
        protected double income;
        public Income(double income){
            this.income = income;
        }
        public double getTax(){
            return income*0.1;
        }
    }
    class Salary extends Income { //工资收入，大于五千的工资收入征收百分之二十的税务
        public Salary(double income){
            super(income);
        }
        @Override
        public double getTax() {
            if (super.income < 5000) {
                return 0;
            } else {
                return (super.income - 5000) * 0.2;
            }
        }
    }
    class StateCouncilSpecialAllowance extends Income{ //享受国务院特殊津贴的收入不征收税务
        public StateCouncilSpecialAllowance(double income){
            super(income);
        }
        @Override
        public double getTax(){
            return 0;
        }
    }
```

观察`totalTax()`方法：利用多态，`totalTax()`方法只需要和`Income`打交道，它完全不需要知道`Salary`和`StateCouncilSpecialAllowance`的存在，就可以正确计算出总的税。如果我们要新增一种稿费收入，只需要从`Income`派生，然后正确覆写`getTax()`方法就可以。把新的类型传入`totalTax()`，不需要修改任何代码。

可见，多态具有一个非常强大的功能，就是允许添加更多类型的子类实现功能扩展，却不需要修改基于父类的代码。

##### 覆写Object方法

因为所有的`class`最终都继承自`Object`，而`Object`定义了几个重要的方法：

- `toString()`：把instance输出为`String`；
- `equals()`：判断两个instance是否逻辑相等；
- `hashCode()`：计算一个instance的哈希值。

在必要的情况下，我们可以覆写`Object`的这几个方法。例如：

```java
public class Hello {
    public static void main(String[] args) {
        Person person = new Person("小蜜蜂",18);
        System.out.printf("向person打招呼：%s, 判断person的名字和person1相等吗: %b , 将person的名字转化为hash: %d\n",person.toString(),
                person.equals(new Person("小蜜蜂",18)),person.hashCode());
    }
}
class Person{
    protected String name;
    protected int age;
    public  Person(String name,int age){
        this.name = name;
        this.age = age;
    }
    @Override
    public String toString() {
        return "Hello, "+this.name;
    }
    @Override
    public boolean equals(Object o){
        if (o instanceof Person p){
            return this.name.equals(p.name);
        }
        return false;
    }
    @Override
    public int hashCode() {
        return this.name.hashCode();
    }
}
```

##### 调用`super`

在子类的覆写方法中，如果要调用父类的被覆写的方法，可以通过`super`来调用。例如：

```java
public class Hello {
    public static void main(String[] args) {
        Person person = new Person("小蜜蜂",18);
        System.out.println(person.run());
        Person person1 = new Student("小蜜蜂",18);
        System.out.println(person1.run());
    }
}
class Person{
    protected String name;
    protected int age;
    public  Person(String name,int age){
        this.name = name;
        this.age = age;
    }
    public String run(){
        return "person is running";
    }
}
class Student extends Person{
    public Student(String name,int age) {
        super(name,age);
    }
    @Override
    public String run(){
        return super.run()+"!";
    }
}
```

##### final

继承可以允许子类覆写父类的方法。如果一个父类不允许子类对它的某个方法进行覆写，可以把该方法标记为`final`。用`final`修饰的方法不能被`Override`.

如果一个类不希望任何其他类继承自它，那么可以把这个类本身标记为`final`。用`final`修饰的类不能被继承.

对于一个类的实例字段，同样可以用`final`修饰。用`final`修饰的字段在初始化后不能被修改.

#### 抽象类

如果父类的方法本身不需要实现任何功能，仅仅是为了定义方法签名，目的是让子类去覆写它，那么，可以把父类的方法声明为抽象方法。

把一个方法声明为`abstract`，表示它是一个抽象方法，本身没有实现任何方法语句。因为这个抽象方法本身是无法执行的，所以，`Person`类也无法被实例化。编译器会告诉我们，无法编译`Person`类，因为它包含抽象方法。

必须把`Person`类本身也声明为`abstract`，才能正确编译它。

如果一个`class`定义了方法，但没有具体执行代码，这个方法就是抽象方法，抽象方法用`abstract`修饰。

因为无法执行抽象方法，因此这个类也必须申明为抽象类（abstract class）。

使用`abstract`修饰的类就是抽象类。我们无法实例化一个抽象类。

无法实例化的抽象类有什么用？

因为抽象类本身被设计成只能用于被继承，因此，抽象类可以强迫子类实现其定义的抽象方法，否则编译会报错。因此，抽象方法实际上相当于定义了“规范”。

在编程实践中，尽量引用高层类型，避免引用实际子类型的方式，称之为面向抽象编程。

面向抽象编程的本质就是：

- 上层代码只定义规范（例如：`abstract class Person`）；
- 不需要子类就可以实现业务逻辑（正常编译）；
- 具体的业务逻辑由不同的子类实现，调用者并不关心。

用`abstract`类覆写上述收税的例子如下：

```java
public class Hello {
    public static void main(String[] args) {
        Income [] income = new Income [] {
                new normalIncome(3000),
                new Salary(7500),
                new StateCouncilSpecialAllowance(15000)
        };
        System.out.printf("此人的总征税额度为：%.2f\n",caculateTax(income));
    }
    public static double caculateTax(Income ... incomes){
        double total =0;
        for (Income s:incomes){
            total +=s.getTax();
        }
        return total;
    }
}
abstract class Income{
    public Income(){};
    public abstract double getTax();
}
class normalIncome extends Income{
    protected double income;
    public normalIncome(double income){
        this.income = income;
    }
    @Override
    public double getTax() {
        return income*0.1;
    }
}
class Salary extends Income{
    protected double salary;
    public Salary(double salary){
        this.salary = salary;
    }
    @Override
    public double getTax() {
        if (this.salary>5000){
            return (this.salary-5000)*0.2;
        }
        return 0;
    }
}
class StateCouncilSpecialAllowance extends Income{
    protected double allowance;
    public StateCouncilSpecialAllowance(double allowance){
        this.allowance = allowance;
    }
    @Override
    public double getTax() {
        return 0;
    }
}
```

#### 接口

继承（抽象类）是“是不是”的关系，而接口则是“有没有”的关系。

|            |    abstract class    |          interface          |
| :--------: | :------------------: | :-------------------------: |
|    继承    | 只能extends一个class | 可以implements多个interface |
|    字段    |   可以定义实例字段   |      不能定义实例字段       |
|  抽象方法  |   可以定义抽象方法   |      可以定义抽象方法       |
| 非抽象方法 |  可以定义非抽象方法  |     可以定义default方法     |

在抽象类中，抽象方法本质上是定义接口规范：即规定高层类的接口，从而保证所有子类都有相同的接口实现，这样，多态就能发挥出威力。

如果一个抽象类没有字段，所有方法全部都是抽象方法。

就可以把该抽象类改写为接口：`interface`。

在Java中，使用`interface`可以声明一个接口。

所谓`interface`，就是比抽象类还要抽象的纯抽象接口，因为它连字段都不能有。因为接口定义的所有方法默认都是`public abstract`的，所以这两个修饰符不需要写出来（写不写效果都一样）。

当一个具体的`class`去实现一个`interface`时，需要使用`implements`关键字。

在Java中，一个类只能继承自另一个类，不能从多个类继承。但是，一个类可以实现多个`interface`

一个`interface`可以继承自另一个`interface`。`interface`继承自`interface`使用`extends`，它相当于扩展了接口的方法。

```java
public class Hello {
    public static void main(String[] args) {
    Person person = new Student("小蜜蜂");
    System.out.println(person.getName());
    person.run();
    }
}
interface  Person{
    String getName();
    default void run(){
        System.out.println("奔跑！");
    };
}
class Student implements Person{
    protected String name;
    public Student(String name){
        this.name = name;
    }
    @Override
    public String getName(){
        return this.name;
    }
}
```

实现类可以不必覆写`default`方法。`default`方法的目的是，当我们需要给接口新增一个方法时，会涉及到修改全部子类。如果新增的是`default`方法，那么子类就不必全部修改，只需要在需要覆写的地方去覆写新增方法。

`default`方法和抽象类的普通方法是有所不同的。因为`interface`没有字段，`default`方法无法访问字段，而抽象类的普通方法可以访问实例字段。

#### 静态字段与静态方法

在一个`class`中定义的字段，我们称之为实例字段。实例字段的特点是，每个实例都有独立的字段，各个实例的同名字段互不影响。

还有一种字段，是用`static`修饰的字段，称为静态字段：`static field`。

实例字段在每个实例中都有自己的一个独立“空间”，但是静态字段只有一个共享“空间”，所有实例都会共享该字段。

对于静态字段，无论修改哪个实例的静态字段，效果都是一样的：所有实例的静态字段都被修改了，原因是静态字段并不属于实例。

虽然实例可以访问静态字段，但是它们指向的其实都是`Person class`的静态字段。所以，所有实例共享一个静态字段。

因此，不推荐用`实例变量.静态字段`去访问静态字段，因为在Java程序中，实例对象并没有静态字段。在代码中，实例对象能访问静态字段只是因为编译器可以根据实例类型自动转换为`类名.静态字段`来访问静态对象。

推荐用类名来访问静态字段。可以把静态字段理解为描述`class`本身的字段（非实例字段）。

有静态字段，就有静态方法。用`static`修饰的方法称为静态方法。

因为静态方法属于`class`而不属于实例，因此，静态方法内部，无法访问`this`变量，也无法访问实例字段，它只能访问静态字段。

通过实例变量也可以调用静态方法，但这只是编译器自动帮我们把实例改写成类名而已。

通常情况下，通过实例变量访问静态字段和静态方法，会得到一个编译警告。

```java
public class Hello {
    public static void main(String[] args) {
        Person person1 = new Person();
        Person.setNumber(Person.getNumber()+1);
        System.out.printf("此时number的值为：%d\n",Person.getNumber());
        Person person2 = new Person();
        Person.setNumber(Person.getNumber()+1);
        System.out.printf("此时number的值为：%d\n",Person.getNumber());
    }
}
class Person{
    protected static int number=0;
    public Person(){}
    public static int getNumber(){
        return number;
    }
    public static void setNumber(int number1){
        number = number1;
    }
}
```

##### 接口的静态字段

因为`interface`是一个纯抽象类，所以它不能定义实例字段。但是，`interface`是可以有静态字段的，并且静态字段必须为`final`类型。

实际上，因为`interface`的字段只能是`public static final`类型，所以我们可以把这些修饰符都去掉，编译器会自动把该字段变为`public static final`类型。

