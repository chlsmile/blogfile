原文地址:https://blogs.oracle.com/sundararajan/entry/understanding_java_class_loading

Understanding Java class loading
理解Java类加载机制


Are you thinking of writing ClassLoaders? or are you facing "unexpected" ClassCastException or LinkageError with wierd message "loader constraint violation". Then, it is time to take a closer look at Java class loading process.
你想写类加载器?或者你遇到了ClassCastException异常,或者你遇到了奇怪的LinkageError状态约束异常.应该仔细看看java类的加载处理了.

What is a ClassLoader and how it loads?
什么是类加载器以及它是如何加载的类?

A Java class is loaded by an instance of java.lang.ClassLoader class. java.lang.ClassLoader itself is an abstract class and so a class loader can only an instance of a concrete subclass of java.lang.ClassLoader. If this is the case, which class loader loads java.lang.ClassLoader class itself? (classic "who will load the loader" bootstrap issue). It turns out that there is a bootstrap class loader built into the JVM. The bootstrap loader loads java.lang.ClassLoader and many other Java platform classes.
一个Java类是由java.lang.ClassLoader类的一个实例加载的. 由于java.lang.ClassLoader自己本身是一个抽象类所以一个类加载器只能够是java.lang.ClassLoader类的具体子类的实例.如果是这种情况,哪一个类加载器来加载java.lang.ClassLoader这个类?(经典的"谁将会加载加载"引导的问题).事实证明JVM有一个内置的引导类加载器.引导加载器加载java.lang.ClassLoader和许多其他java平台类.

To load a specific Java class, say for example com.acme.Foo, JVM invokes loadClass method of a java.lang.ClassLoader (actually, JVM looks for loadClassInternal method - if found it uses that method, or else JVM uses loadClass. And loadClassInternal method calls loadClass). loadClass receives name of the class to load and returns java.lang.Class instance that represent the loaded class. Actually, loadClass method finds the actual bytes of .class file (or URL) and calls defineClass method to construct java.lang.Class out of the byte array. Loader on which loadClass is called is referred as initiating loader (i.e., JVM initiates loading using that loader).
But, the initiating loader need not directly find the byte[] for class - instead it may delegate the class loading to another class loader (for example, to it's parent loader) - which itself may delegate to another loader and so on.
Eventually some class loader object in delegation chain ends up calling defineClass method to actually load the concerned class (com.acme.Foo).
That particular loader is called defining loader of com.acme.Foo. At runtime, a Java class is uniquely identified by the pair - the fully qualified name of the class and the defining loader that loaded it.
If the same named (i.e., same fully qualified name) class is defined by two different loaders, these classes are different - even if the .class bytes are same and loaded from the same location (URL).
要加载一个具体的java类,例如com.acme.Foo,JVM调用java.lang.ClassLoader类的loadClass方法(事实上,JVM查找loadClassInternal方法-如果发现它用该方法,否则JVM使用loadClass方法.而loadClassInternal方法会调用loadClass方法).loadClass方法接收类名来加载类返回表示加载的类的java.lang.Class实例.事实上loadClass方法找到.class文件(或者URL)的实际字节,并调用defineClass方法来构造出java.lang.Class类的字节数组.加载器上调用loadClass方法的加载器称之为启动加载器(即,JVM启动加载使用这个加载器).
但是,启动加载器不是直接加载类的-而是可能委托给另外一个类加载器(例如,它的父加载器)-它自己也可能委派给另外一个加载器去加载等等.
最终在委托链中的某些类加载器对象调用defineClass方法加载有关的类(com.acme.Foo).
这个特殊的类加载器叫做com.acme.Foo的确切加载器.在运行时,一个java类是由类的完全限定类名和和类加载器确定其唯一性的.
如果指定相同的类名(即,相同的完全限定类名)的类是由两个不同的类加载器加载的,那么这些类是不同的-即使这些.class的字节码是相同的并且都是从相同的位置进行加载的(相同的URL).

How many classloaders and where they do load from?
有多少种类加载器并且它们是从哪里加载类的?

Even with a good old simple "hello world" Java program, there are atleast 3 class loaders.
即便是一个简单的"hell world"java程序,也有至少3种类加载器.

bootstrap loader
启动类加载器
loads platform classes (such as java.lang.Object, java.lang.Thread etc)
加载java平台基础类(例如java.lang.Object,java.lang.Thread等)
loads classes from rt.jar ($JRE_HOME/lib/rt.jar)
加载rt.jar包种的类($JRE_HOME/lib/rt.jar)
-Xbootclasspath may be used to alter the boot class path -Xbootclasspath/p: and -Xbootclasspath/a: may be used to prepend/append additional bootstrap directories - have extreme caution doing so. In most scenarios, you want to avoid playing with boot class path.
-Xbootclasspath参数可以更改启动类路径-Xbootclasspath/p: 和 -Xbootclasspath/a:参数可以前置/追加额外的引导目录-一定要格外小心这样做.在大多数情况下,要避免随意启动类路径.


In Sun's implementation, the read-only System property sun.boot.class.path is set to point to the boot class path.Note that you can not change this property at runtime - if you change the value that won't be effective.
在Sun的实现中,只读系统属性sun.boot.class.path设置为指向启动类路径.注意你不能在运行时修改这个属性-如果你修改了修改也不会生效.

This loader is represented by Java null. i.e., For example, java.lang.Object.class.getClassLoader() would return null (and so for other bootstrap classes such as java.lang.Integer, java.awt.Frame, java.sql.DriverManager etc.)
这个加载器由java的null表示.例如,java.lang.Object.class.getClassLoader()方法将会返回null(还有其他的类例如java.lang.Integer, java.awt.Frame, java.sql.DriverManager 等)

extension class loader
扩展类加载器

loads classes from installed optional packages
从已安装的可选包中加载类

loads classes from jar files under $JRE_HOME/lib/ext directory
从$JRE_HOME/lib/ext目录下加载jar文件

System property java.ext.dirs may be set to change the extension directories using -Djava.ext.dirs command line option.
可以使用-Djava.ext.dirs命令修改系统属性java.ext.dirs来修改扩展目录


In Sun's implementation, this is an instance of sun.misc.Launcher$ExtClassLoader (actually it is an inner class of sun.misc.Launcher class).
在Sun的实现中,它是sun.misc.Launcher$ExtClassLoader的实例(事实上它是sun.misc.Launcher类的一个内部类)

Programmatically, you can read (only-read!) System property java.ext.dirs to find which directories are used as extension directories. Note that you can not change this property at runtime - if you change the value that won't be effective.
在编写代码中,你可能读取(只能够读取!)系统通属性java.ext.dirs来寻找哪个目录是扩展目录.你不能在在运行期间修改这个属性-即使你改变了也不会生效.

application class loader
应用类加载器

Loads classes from application classpath
从应用的classpath中加载类

Application classpath is set using Environment variable CLASSPATH (or)-cp or -classpath option with Java launcher If both CLASSPATH and -cp are missing, "." (current directory) is used.
使用环境变量CLASSPATH(或者)-cp或者-classpath选项设置应用的classpath,如果CLASSPATH和-cp都找不到,则使用"."(当前目录).

The read-only System property java.class.path has the value of application class path. Note that you can not change this property at runtime - if you change the value that won't be effective.
只读系统属性java.class.path是应用类路径.你不能在运行期间修改这个属性-即使你改变了也不会生效.


java.lang.ClassLoader.getSystemClassLoader() returns this loader This loader is also (confusingly) called as "system class loader" - not to be confused with bootstrap loader which loads Java "system" classes.
java.lang.ClassLoader.getSystemClassLoader()方法的返回值是这个加载器,这个加载器也叫做"系统加载器"-不过不要将加载java"系统"类的启动加载器混淆.


This is the loader that loads your Java application's "main" class (class with main method in it). In Sun's implementation, this is an instance of sun.misc.Launcher$AppClassLoader (actually it is an inner class of sun.misc.Launcher class).
这个加载器加载你应用的"main"(由main方法的类).在Sun的实现中,它是sun.misc.Launcher$AppClassLoader的一个实例(事实上它是sun.misc.Launcher类的一个内部类).

the default application loader uses extension loader as it's parent loader.
默认的应用加载器用扩展加载器做为它的父加载器.


You can change the application class loader by command line option -Djava.system.class.loader. This value specifies name of a subclass of java.lang.ClassLoader class. First the default application loader loads the named class (and so this class has to be in CLASSPATH or -cp) and creates an instance of it. The newly created loader is used to load application main class.
Typical class loading flow
你可以使用-Djava.system.class.loader命令更改应用的类加载器.这个值指定java.lang.ClassLoader的子类的名字.首先默认应用加载器加载已命名的类(这个类在CLASSPATH或者-cp)和创建一个它的实例.新创建的这个类的实例用于加载应用的main类.

Let us assume you are running a "hello world" java program. We will how class loading proceeds. JVM loads main class using the "application class loader". If you run the following program
让我们假设你正在运行一个"hello world" java程序.我们来看一些类的加载过程.JVM用应用类加载器加载主方法(main)所在的类.如果你运行下面的程序
class Main {
	public static void main(String[] args) {
            System.out.println(Main.class.getClassLoader());
            javax.swing.JFrame f = new javax.swing.JFrame();
            f.setVisible(true);
            SomeAppClass s = new SomeAppClass();
	}
}

it prints something like
它会打印如下内容
sun.misc.Launcher$AppClassLoader@17943a4
Whenever a reference to some other class has to be resolved from Main class, then JVM uses the defining loader of Main class - the application class loader - as initiating loader. In the above example, to load the class javax.swing.JFrame, JVM will use the application class loader as initiating loader. i.e., JVM will call loadClass() (loadClassInternal) on the application class loader. The application class loader delegates that to extension class loader.
And the extension class loader checks whether it is a bootstrap class (using a private method - ClassLoader.findBootstrapClass) and the bootstrap loader defines the class by loading it from rt.jar.
When reference to SomeAppClass has to be resolved, JVM follows the same process - it uses application class loader as initiating loader for it.
The application loader delegates it to extension loader. Extension loader checks with bootstrap loader. Bootstrap loader won't find "SomeAppClass". Then extension loader checks whether "SomeAppClass" is in any of the extension jars and it won't find any.
Then application class loader check the .class bytes in application CLASSPATH. If it finds, it defines the same. If not, NoClassDefFoundError will be thrown.
每当一些其它的类引用在Main类中被解析时,JVM用Main所在类的明确的加载器-应用类加载器-做为初始化加载器.在上面的列子中,为了加载javax.swing.JFrame类JVM将使用应用类加载器做为一个初始化加载器.即,JVM将用应用类应用做为初始化加载器.即,JVM将调用loadClass()方法(loadClassInternal方法)在应用类加载器中.应用类加载器委托给扩展类加载器.
扩展加载器检查这是否是一个启动类(用私有方法 - ClassLoader.findBootstrapClass),启动类加载器是否从rt.jar加载过它.
当SomeAppClass的引用类被解析时,JVM有着相同的过程-用应用类加载器做为初始化加载器.
应用加载器委托给扩展加载器.扩展加载器检查启动加载器.启动加载器找不到"SomeAppClass"类.
于是扩展加载器检查"SomeAppClass"类是否在扩展jars里,结果发现不在.
于是应用类加载器检查在应用的CLASSPATH下的.class字节.如果找到了则进行加载.如果没有找到,将会抛出NoClassDefFoundError异常.

Summary

Class is uniquely identified by defining loader and fully qualified name.
Classes are different even if loaded from identical .class bytes from the same location in file system, if the defining loaders are different.
Class loaders delegate loading to parent loaders.
To load class "Foo" referrred from "Bar" class, JVM uses Bar's defining loader as initiating loader. JVM will call loadClass("Foo") on the defining loader of Bar.
JVM caches -> runtime class record for each time it initiates a load. JVM will use cache for subsequent resolution. i.e, loadClass won't be called for every reference. This ensures time invariance - i.e., a ClassLoader that loads different .class bytes for the same class name won't be allowed. It is taken care by cache. Well written class loaders have to check cache by ClassLoader.findLoadedClass() call.
Stay tuned for more discussion on loader constraints and LinkageErrors..