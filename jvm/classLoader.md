#类加载一般分为三个阶段: 
- 加载阶段: 主要是负责查找并且加载类的二进制文件,其实就是class文件
    - 将类的.class文件中的二进制数据读入到内存中,将其放在运行时数据区的方法区内,然后在内存中创建一个java.lang.Class对象(规范并未说明Class对象位于哪里,HotSpot虚拟机将其放在了方法区中)用来封装类在方法区内的数据结构
    - 加载方式
        - 本地系统直接加载
        - 网络下载
        - zip,jar归档文件加载
        - 专有数据库提取
        - java源文件动态编译(jap编译为servlet)
    - 追踪类的加载信息并打印出来: -XX:+TraceClassLoading 
    - jvm规范允许类加载器在预料到某个类将要被使用时就预先加载它,如果在预先加载的过程中遇到了.class文件缺失或存在错误,类加载器必须在**程序首次主动**使用该类时才报告错误(LinkAgeError错误)
    - 如果这个类一直没有被程序使用,那么**类加载器就不会报告错误**
- 连接阶段: 连接阶段负责的工作比较多.细分的话还可以分为如下三个阶段
    - 验证: 主要是确保类文件的正确性,比如class的版本,class文件的魔术因子是否正确
    - 准备: 为类的静态变量分配内存,并将为其初始化默认值
    - 解析: 把类中的符号引用转换为直接引用
- 初始化阶段: 为类的静态变量赋予正确的初始值(代码编写阶段给定的值)

JVM对类的初始化是一个延时的机制,即使用的是LAZY的方式,当一个类在首次使用时才会被初始化,在同一个运行包下,一个Class只会被初始化一次

#类的主动使用和被动使用:  
JVM虚拟机规定了,每个类或者每个接口再被java程序**首次主动使用**时才会对其初始化,当然随着JIT技术的成熟,JVM运行期间的编译也越来越智能,不排除JVM在运行期间提前预判并且初始化某个类  
JVM同时规范了以下六种主动使用类的场景:  

1. 通过使用new关键字进行初始化,会导致类的加载并且最终初始化
2. 访问类的静态变量,包括读取和更新会导致类的初始化 对静态字段来说,只有直接定义了该字段的类才会被初始化(使用子类访问父类静态变量,子类不会初始化)(引用类的**简单静态常量**不会导致类的初始化,如果访问final static 修饰的**random构造的常量**会导致类的初始化)
>常量在编译阶段会存入调用这个常量的方法所在的类的常量池中
本质上,调用类并没有直接引用到定义常量的类,因此并不会触发
定义常量的类的初始化
注意:将简单常量存放到使用该常量的类中之后两者就毫无关系,甚至可以将定义常量类的class文件删除

- 助记符
    - 访问静态变量:getstatic
    - 静态变量赋值:putstatic
    - 访问静态方法:invokestatic
    
3. 访问类的静态变量,会导致类的初始化
4. 对某个类进行反射操作
5. 初始化子类会导致父类初始化(子类引用调用父类静态变量只会导致父类初始化)
6. 启动类(带有main函数的类 java Test)  
7. 1.7之后动态语言支持:java.long.invoke.MethodHandle实例的解析结果REF_getStatic,REF_putStatic,REF_invokeStatic句柄对应的类没有初始化,则初始化

**除了以上七种情况,其余均为被动使用,不会导致类的初始化**  

接口与类的区别:没有直接使用到父接口,不会导致父接口**初始化**,但是会**加载**
- 在初始化一个类时,并不会先初始化它所实现的接口
- 在初始化一个接口时,并不会先初始化他的父接口
因此一个父接口并不会因为他的子接口或者实现类的初始化而初始化,只有当程序首次使用特定接口的静态变量时,才会导致该接口的初始化
```
// 可以用于接口初始化的依据
new Class{{System.out.print("hello word")}}
```

**扩展类加载器**
扩展类加载器不会直接加载.class,只会加载jar包中的class文件,与跟类加载器和系统类加载器不一样