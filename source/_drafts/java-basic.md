# Java Baisc

1. @Override
   - 方法名，参数列表，返回类型都相同的情况下， 对方法体进行修改或重写
1. Overload
   - same function name only
1. `==` vs `equals`
   - `==` 内存地址
   - `equals` 内容
1. Set 如何快速找到元素
   - hashCode 算法
   - 分类存放： hashCode 相似的元素 放一齐
   - 快速定位
1. String
   - String 修改，会不断new
   - StringBuffer，线程安全，可修改
   - StringBuilder 不线程安全，会互相影响
1. Array
   - Array(数组)，int[]，获取快O(1)，删除慢，重新排列
   - List 两个实现
     - ArrayList (自动增长容量)
       - 找 快
       - 删慢，数据 前移
     - LinkedList: 
       - 中间 添加 或 删除 非常快
       - 找 慢
1. HashMap vs. HashTable
    - HashMap 继承 Asbtractmap
      - key 可以为 null
      - Map线程不安全，要安全用 ConcurrentHashMap
      - 快
    - HashTable 继承 Dictionary
      - 线程安全
1. Collection包结构，与Collections的区别
    - Collection 接口，子接口有 Set、List、LinkedList、ArrayList
    - Collections 是一个帮助类: ex. `Collections.sort()`
1. 泛型
    - “泛型”: 代码 可以被 不同类型的 对象 所重用。List<Integer> iniData = new ArrayList<>()
1. 深拷贝 和 浅拷贝
   - 深拷贝 - 两个对象完全独立。
   - 浅拷贝 - 两个对象不完全独立，共享内部对象。	
1. Java 异常的
    - try-catch-finally
      - try 块负责监控
      - catch 块负责捕获
      - finally 不管是否出现异常都会执行
1. final
   - final 类 不可以被继承
   - final 方法 不可以被重写 JVM会尝试将其内联,以提高运行效率
   - final 变量不可以被改变.如果修饰引用,那么表示引用不可变,引用指向的内容可变.
   - final 常量 在编译阶段会存入常量池中.
1. static - 属于类 (Class), 所有对象共享
    - 静态变量 (Static Variable)	
      - 存储所有对象共享的数据。
    - 静态方法 (Static Method)
1. Excption
    - RuntimeException运行时异常
      - NullPointerException (空指针异常)
      - ClassCastException (类转换异常)
      - ArithmeticException (算术异常)
      - IndexOutOfBoundsException（数组越界）
    - CheckedException被检查异常 FileNotFoundException
    - Error错误: OutOfMemoryError、ThreadDeath
1. StackOverflow
    - 因为栈一般默认为1-2m
    - 一旦出现 死循环 或者 大量 递归，超过1m而导致溢出
1. OutOfMemoryError
    - 如果是内存泄漏，可进一步通过工具查看泄漏对象到GCRoots的引用链。
      - 于是就能找到泄漏对象是通过怎样的路径与GC Roots相关联并导致垃圾收集器无法自动回收。
    - 如果不存在泄漏，那就应该检查虚拟机的参数(-Xmx与-Xms)的设置是否适当。
1. 线程 vs. 进程
    - 线程 更小，会互相影响
    - 进程 是系统level，不会互相影响
1. 反射的作用于原理
   - 反射机制是在运行时，对于任意一个类，只要给定类的名字，都能够知道这个类的所有属性和方法
    ```java
    Class.forName('com.mysql.jdbc.Driver.class');//加载MySQL的驱动类
    ```
    - 反射的实现方式：
      第一步：获取Class对象，有4中方法：
      - 1）Class.forName(“类的路径”)； 
      - 2）类名.class 
      - 3）对象名.getClass()
1. java.lang.Object
    - clone
    - finalize - when 否可以被回收
    - equal
    - hashCode
    - wait - synchronized
    - notify ，唤醒等待中某个线程
    - notifyAll，唤醒所有线程
1. Java 创建对象
    - new
    - 使用反射方式创建对象，使用 newInstance()，但是得处理两个异常 InstantiationException、
      IllegalAccessException
      - User user=User.class.newInstance();
    - clone
    - 反序列化
1. 获取 对象运行时 类型
    - user.getClass()
    - Class.forName
1. ArrayList 和 LinkedList
    - ArrayList 
      - good: 地址连续，查询操作效率会比较高（在内存里是连着放的）。
      - 缺点：要移动数据，所以插入和删除操作效率比较低。
    - LinkedList
        - good：地址是任意的，所以在开辟内存空间的时候不需要等
            - 对于新增和删除操作，LinkedList 比较占优势
        - bad：查询操作性能低。
1. ArrayList
    - clone 浅复制
    - 添加数组
    - 并发，线程不安全
1. 有数组了为什么还要搞个 ArrayList 呢？
   - 普通数组， 定死的数组
   - ArrayList 可以使用默认的大小，当元素个数到达一定程度 后，会自动扩容。动态数组
   
1. synchronized 
   - 是 Java 中用于实现 线程同步（Thread Synchronization）的关键字
   - 多个线程对共享资源的访问， 避免数据不一致性问题。

1. Java中实现多线程有几种方法
    - Thread : `extends Thread`
      - 重写其 run() 方法。run() 方法包含了线程要执行的任务。
      - thread1.start();
    - implements Runnabl
    - implements Callable<String>
        - 任务有返回值，并且可以抛出异常
1. 停止一个正在运行的线程
    - stop/suspend 唔推荐
    - 使用 interrupt() 方法

1. notify()和notifyAll()有什么区别
    - notify()
      - 唤醒一个等待此对象锁的线程 JVM 随机
      - 会 死锁
    - notifyAll()
      - 唤醒所有等待此对象锁的线程 它们会竞争锁
      - 开销较大
1. sleep()和wait() 有什么区别
   - 对于sleep()方法，我们首先要知道该方法是属于Thread类 中的。
   - wait()方法，则是属于Object类 中的。线程会放弃对象锁，进入等待此对象的等待锁定池
     - 正确的做法
    ```java
    while (condition_is_not_met) {
        obj.wait();
    }
    ```
      


























