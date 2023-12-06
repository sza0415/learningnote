### JDK、JRE、JVM三者之间的关系

JDK：Java Development Kit 开发者工具
JRE：Java Runtime Environment 运行环境
JVM：Java Virtual Machine 虚拟机

`JDK`包括`JRE`，`JRE`包括了`JVM`

假如你在软件公司开发了一个新的软件，现在要去客户那边把项目部署起来，你需要安装`JDK`吗？

不需要，只需要安装`JRE`就行，`JRE`体积很小，安装非常便捷快速。

`JAVA_HOME`是Java的`JDK`所属的环境变量。简单的程序执行你只需要将`java.exe（执行字节码文件）`和`javac.exe（编译java源代码）`的路径添加至环境变量（`path`）就行了。例如学习到JavaWEB时候安装Tomcat服务器，就一定需要配置`JAVA_HOME`了。



-	

  

  

  







java程序员直接编写的java代码被称为java源代码，java源代码是无法被`JVM`识别的。

java代码这样的普通文本代码必须经过一个编译，将`普通文本代码`变成`字节码`,`JVM`可以识别`字节码`。

### java编译阶段和运行阶段可以在不同的操作系统上完成吗？

![image-20231129184752919](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231129184752919.png)

例如在`Windows`上编译，编译完成的`字节码`放到`Linux`上运行

可以，因为Java是跨平台的。

- 编译器：
  - 编写.java结尾的源代码
  - 使用编译器（`javac`是`JDK`自带的编译器）,若编写的源代码符合语法规则，编译便会通过，一个java源代码是可以生成多个`class`字节码文件
- 运行期（可以在不同的OS平台上）
  - 使用`JDK`自带命令`java`执行字节码，剩下的工作交给`JVM`虚拟机
    - `JVM`会将`class`字节码文件装载进去，然后`JVM`会对字节码进行解释（解释器会负责将字节码解释为二进制文件），然后`JVM`会将生成的二进制文件交给OS操作系统，OS会执行二进制文件和硬件进行交互。



### 字节码文件是二进制文件吗？

不是，字节码不是二进制文件，如果是二进制的话，就不需要`JVM`了，因为操作系统可以直接执行二进制文件。

-------

### `cmd`上命令`java Helloworld`的执行原理以及原理

这里是`java` 后跟上类名，在高版本可以`java`命令后跟上java源文件的路径，这是为了简化开发而提出的，`java + 源代码路径`会执行编译和运行两步。而低版本的`java + 类名`只是负责运行，下面为具体的过程。

- 会先启动`JVM`（Java虚拟机）
- `JVM`启动之后，`JVM`会启动`类加载器classloader`

  - `类加载器classloader`的作用：去硬盘上找类对应的`字节码文件`
  - 假设是`java Helloworld`，那么`类加载器`会去硬盘上搜索`Helloworld.class`文件
  - 若`类加载器classloader`在硬盘上找不到对应的字节码文件，会报错：`错误：找不到或无法加载主类`
  - `类加载器classloader`默认会从当前路径下找
- `类加载器classloader`在硬盘上找到了对应的字节码文件，`类加载器`会将字节码文件装载到`JVM`中，`JVM`会启动`解释器`，将字节码解释为`二进制文件`，操作系统会执行`二进制文件`和硬件进行交互。

------

### `类加载器classloader`如何去找字节码文件.class?

当我们在命令行上输入`java Helloworld`，`类加载器dataloader`会默认从当前路径下找字节码文件。

我们可以使用设置一个环境变量`classpath`让类加载器去指定的路径下加载字节码文件。

![image-20231129212755194](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231129212755194.png)

------

### java注释

```java
// 单行注释
```

```java
/*
	多行注释
*/
```

```java
/** javadoc注释
  * 
  * @param args
  */
public static void main(String[] args){
    System.out.println("hello world");
}
```

p54