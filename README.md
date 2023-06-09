## 一、阿里简历评估(阿里集团-淘宝天猫商业集团-超市业务发展中心-物流技术)4.10

### 1. 本科和硕士期间的GPA

### 2. Java的内存模型和内存空间的分布

Java内存模型（Java Memory Model，JMM）是一种规范，定义了Java虚拟机(JVM)中的线程之间如何进行通信，以及如何访问共享内存。Java内存模型的主要目的是保证多线程环境下，共享变量的可见性、原子性和有序性。JMM定义了以下两种内存：

1. 线程私有内存：每个线程都有自己的线程栈，用于存储局部变量、方法参数、返回值等。线程私有内存之间互不干扰，不需要进行同步操作。
2. 共享内存：多个线程共享的内存区域，包括Java堆和方法区等。由于多个线程可以同时访问共享内存，因此需要进行同步操作，以保证共享变量的可见性和原子性。

Java内存模型通过使用同步机制（如synchronized关键字、volatile关键字、Lock和Atomic等工具类）来保证多个线程之间对共享内存的正确访问。具体来说，JMM定义了以下规则：

1. 原子性规则：对基本数据类型（如int、long等）的读写操作具有原子性。
2. 可见性规则：在一个线程中修改了共享变量的值，另一个线程能够立即看到这个修改。
3. 有序性规则：在多线程环境下，指令可能会被重排序，JMM通过禁止一些重排序来保证有序性

---

Java的内存模型指的是Java程序中的内存结构，包括了线程私有部分（如**线程栈**、**程序计数器**等）和线程共享部分（如**堆**、**方法区**等）。Java虚拟机的内存空间分布如下：

1. 程序计数器(Program Counter Register)：是线程私有的内存空间，用于存放当前线程所执行的字节码的行号指示器。每个线程都有一个独立的程序计数器，线程之间的计数器互不影响。
2. 虚拟机栈(Java Virtual Machine Stacks)：也是线程私有的内存空间，用于存储方法执行的栈帧。每个方法被执行的时候，JVM都会为它创建一个栈帧并压入虚拟机栈中。栈帧中存储着局部变量表、操作数栈、动态链接、方法出口等信息。栈帧随着方法的执行结束而出栈。
3. 本地方法栈(Native Method Stacks)：也是线程私有的内存空间，与虚拟机栈类似，用于存储Native方法的栈帧。
4. Java堆(Java Heap)：是Java虚拟机所管理的内存中最大的一块，也是线程共享的内存空间。用于存放对象实例以及数组等。Java堆可以分为新生代和老年代，新生代又可以分为Eden空间、From Survivor空间和To Survivor空间。
5. 方法区(Method Area)：也是线程共享的内存空间，用于存储已被虚拟机加载的类信息、常量、静态变量、即时编译器编译后的代码等数据。
6. 运行时常量池(Runtime Constant Pool)：也是方法区的一部分，用于存储编译期生成的各种字面量和符号引用。在类加载后，将常量池中的数据放入方法区中，随着JVM的运行常量池也会动态地进行扩充。
7. 直接内存(Direct Memory)：不是JVM虚拟机运行时数据区的一部分，但是也会被频繁地使用到。直接内存不是通过new关键字分配的，而是通过调用本地方法（如NIO）分配的，它直接使用操作系统的内存空间，而不会占用JVM虚拟机内存空间。

### 3. 一个对象中的临时变量i，list分别在内存中的哪里？

一个对象实例中包含的所有成员变量，无论是基本数据类型还是引用类型，都存储在堆内存中。所以，临时变量 `i` 和引用类型变量 `list` 也都存储在堆内存中。

### 4. 为什么会产生并发问题？

产生并发问题的主要原因是多个线程共享同一个资源，且对该资源进行读写操作时没有进行正确的同步处理。==由于CPU时间片轮转、线程调度等原因，多个线程执行的顺序和时间都是不确定的==，当多个线程同时对一个资源进行写操作时，就会出现竞态条件（Race Condition）的问题，导致程序的运行结果不符合预期。

### 5. 在项目中用到的一些常用的集合类有哪些？

ArrayList，HashMap

### 6. ArrayList 和 LinkedList的区别

- ArrayList采用动态数组实现，支持随机访问和快速遍历

- LinkedList采用双向链表实现，因为只需修改指针，支持高效地增删

  链表在内存中是不连续的，随机访问效率低，每次都须遍历

  需要存储前后前后节点的地址，占用更大的存储空间

### 7. ArrayList 和 LinkedList为什么都是线程不安全的？

因为它们的内部实现并没有考虑到多线程并发访问的情况，如果多个线程同时对同一个集合进行增删改查等操作，可能会导致集合数据的不一致和线程安全问题。

- `ArrayList`的内部实现是一个数组，当数组大小不足时会进行扩容操作，如果多个线程同时对其进行扩容操作，可能会导致数据的覆盖和丢失，因此需要加锁来保证线程安全；
- `LinkedList`的内部实现是一个双向链表，如果多个线程同时对其进行增删操作，可能会导致链表节点的丢失和环路问题，因此需要加锁来保证线程安全。

### 8. 为什么要用Redis，它的优势是什么？

1. 高性能：Redis使用内存作为数据存储介质，因此具有非常高的读写性能，适用于对响应速度和吞吐量要求较高的应用场景。
2. 数据结构丰富：Redis支持丰富的数据结构，包括字符串、哈希、列表、集合、有序集合等，可以满足不同的数据处理需求。
3. 数据持久化：Redis支持数据持久化，可以将内存中的数据定时或手动写入磁盘，保证数据不会因进程退出或机器宕机而丢失。

### 9.Redis除了它是以内存方式存储带来的性能提升，还有其他因素吗？

- Redis使用的是非阻塞IO，IO多路复用，使用了单线程来轮询描述符，将数据库的开、关、读、写都转换成了事件，减少了线程切换时上下文的切换和竞争。
- Redis采用了单线程的模型，保证了每个操作的原子性，也减少了线程的上下文切换和竞争。
- Redis全程使用hash结构，读取速度快，还有一些特殊的数据结构，对数据存储进行了优化，如压缩表，对短数据进行压缩存储，再如，跳表，使用有序的数据结构加快读取的速度。

[参考资料](https://blog.csdn.net/XingXing_Java/article/details/92626174#:~:text=Redis%E7%9A%84%E9%AB%98%E5%B9%B6%E5%8F%91%E5%92%8C%E5%BF%AB%E9%80%9F%E5%8E%9F%E5%9B%A0%201.redis%E6%98%AF%E5%9F%BA%E4%BA%8E%E5%86%85%E5%AD%98%E7%9A%84%EF%BC%8C%E5%86%85%E5%AD%98%E7%9A%84%E8%AF%BB%E5%86%99%E9%80%9F%E5%BA%A6%E9%9D%9E%E5%B8%B8%E5%BF%AB%EF%BC%9B,2.redis%E6%98%AF%E5%8D%95%E7%BA%BF%E7%A8%8B%E7%9A%84%EF%BC%8C%E7%9C%81%E5%8E%BB%E4%BA%86%E5%BE%88%E5%A4%9A%E4%B8%8A%E4%B8%8B%E6%96%87%E5%88%87%E6%8D%A2%E7%BA%BF%E7%A8%8B%E7%9A%84%E6%97%B6%E9%97%B4%EF%BC%9B%203.redis%E4%BD%BF%E7%94%A8%E5%A4%9A%E8%B7%AF%E5%A4%8D%E7%94%A8%E6%8A%80%E6%9C%AF%EF%BC%8C%E5%8F%AF%E4%BB%A5%E5%A4%84%E7%90%86%E5%B9%B6%E5%8F%91%E7%9A%84%E8%BF%9E%E6%8E%A5%E3%80%82)

### 10. SpringBoot大概的一个启动流程

1. 加载Spring Boot核心配置类：Spring Boot会加载一个或多个核心配置类，这些配置类通常使用注解`@SpringBootApplication`或其组合注解`@EnableAutoConfiguration`、`@ComponentScan`来标记。其中`@EnableAutoConfiguration`是Spring Boot自动配置的核心注解，它会根据classpath下的jar包、类路径、及其它配置来自动配置Spring应用程序所需要的组件。
2. 创建Spring IoC容器：Spring Boot会创建Spring IoC容器，也就是ApplicationContext。在容器初始化的过程中，会扫描所有的配置类和类路径，将其转化为BeanDefinition并加载到容器中。
3. 运行ApplicationContext：Spring Boot会调用ApplicationContext的`refresh()`方法来启动IoC容器。在此过程中，Spring会创建并初始化所有的Bean，以及完成Bean之间的注入等操作。
4. 启动内嵌的Web服务器：Spring Boot内嵌了多种Web服务器，如Tomcat、Jetty、Undertow等。在ApplicationContext初始化完成后，Spring Boot会自动选择一个合适的Web服务器，并启动该服务器。
5. 注册ShutdownHook：Spring Boot会注册ShutdownHook，用于在JVM关闭时优雅地关闭ApplicationContext及内嵌的Web服务器等资源。

### 11. 浏览器访问一个网站，它背后发生了什么事情

1. 浏览器向 DNS 服务器发出请求，获取该网站的 IP 地址。
2. 浏览器通过 TCP 协议与服务器建立连接，发送 HTTP 请求。
3. 服务器接收到请求后，根据请求的 URL 路径等信息，找到对应的处理程序或静态资源，生成 HTTP 响应，并通过 TCP 协议将响应发送给浏览器。
4. 浏览器接收到响应后，根据响应头中的 Content-Type 等信息，决定如何显示响应内容。例如，如果是 HTML 文档，则将其解析成 DOM 树，并通过 CSS 解析器、JavaScript 解析器等工具渲染出页面。
5. 当用户与页面进行交互时，例如点击按钮、输入表单等，浏览器会向服务器发送新的请求，重复上述过程。

### 12. 内核态和用户态

- 内核态和用户态是操作系统中的两种执行模式，通常用来区分运行在不同特权级别下的程序或者代码。

- 用户态是指程序在非特权模式下执行，它只能访问有限的资源，比如进程的私有内存和系统调用等。在用户态下，==程序无法直接访问系统硬件，必须通过操作系统提供的系统调用来间接访问。==

- 内核态是指程序在特权模式下执行，==它可以访问操作系统的所有资源==，比如硬件设备和系统内存等。在内核态下，程序可以直接访问硬件，而不需要通过系统调用来间接访问。

- 在操作系统中，内核是运行在内核态下的，而应用程序是运行在用户态下的。当应用程序需要执行一些需要特权级别的操作时，比如读写系统文件或者打开网络连接等，它就需要向操作系统发起系统调用，将自己的权限提升到内核态下，让内核代表它完成这些操作。

### 13. 线程和进程的区别

1. ==进程是程序的一次执行过程，是操作系统进行资源分配和调度的基本单位==，包含程序代码、数据和进程控制块等信息，具有独立的内存空间；==线程是进程中的一条执行路径，是操作系统进行CPU调度的基本单位==，包含线程控制块和线程栈等信息，与同一进程的其他线程共享内存空间。
2. 进程之间相互独立，通信需要借助操作系统提供的IPC（进程间通信）机制；线程之间共享同一进程的内存空间，可以通过共享变量来进行通信。
3. 进程的创建和销毁比较复杂，开销较大；线程的创建和销毁比较简单，开销较小。
4. 进程之间的切换开销较大；线程之间的切换开销较小，因为线程共享进程的内存空间，切换时只需要切换线程的上下文。

### 14. 向面试官问一些自己的问题

## 二、腾讯初面(腾讯大数据)4.12

### 1. 介绍部门地点和实习时间，询问是否符合

### 2.自我介绍

### 3. 研究方向大数据体现在哪里？

### 4. 数据从哪里获取的？

### 5. 怎么验证模型的正确性

### 6.用到的模型，具体怎么实现的

### 7. 项目中有用到DB，可以具体介绍一下吗？

### 8. mysql怎么保证并发修改时数据的一致性？

在 MySQL 中，为了保证并发修改时数据的一致性，采用了以下两种机制：

1. 锁机制：通过给数据加锁来实现并发控制。MySQL 支持多种锁机制，例如表锁、行锁、共享锁、排它锁等。
2. MVCC（Multi-Version Concurrency Control）机制：通过版本号的方式实现并发控制，不同的版本号对应不同的数据快照。当读取数据时，读取的是符合版本号的最新的数据快照。当更新数据时，会将新数据写入新的数据块，同时生成新的版本号，更新数据时不会影响已经存在的旧版本数据块，从而实现并发修改时数据的一致性。

### 9. DB怎么保证数据不丢失呢，有什么机制

1. 事务：事务是一组原子性的操作，要么全部执行成功，要么全部执行失败回滚，保证了数据的一致性。在 MySQL 中，事务是通过 InnoDB 存储引擎来实现的。
2. 锁机制：数据库通过加锁来保证数据在并发修改时的一致性，包括行级锁、表级锁等。
3. 写 Ahead Logging（WAL）：WAL 技术是一种常见的保证数据不丢失的机制。WAL 通过将所有修改操作先记录到一个日志文件中，然后再将这些修改操作同步到磁盘上的数据文件中，保证了数据的一致性。
4. 数据备份与恢复：数据库还会定期备份数据，以便在发生数据丢失等情况时可以快速恢复数据。
5. 数据复制与主从备份：数据库会通过数据复制和主从备份等技术，在多个服务器之间同步数据，以保证数据的可用性和备份。

### 10. 主从复制是基于什么原理做的？

主从复制是基于二进制日志 (binlog) 实现的。

在主从复制的过程中，主服务器会把自己的数据更改操作 (INSERT/UPDATE/DELETE) 记录到二进制日志中，并将二进制日志传输到从服务器，从服务器则通过解析这些二进制日志，执行相同的数据更改操作，从而保持主从服务器的数据一致性。

### 11.binlog和redolog有了解他们的区别吗？

binlog是二进制日志，记录了所有对数据的更新操作，包括insert、update、delete等，以二进制的形式记录在磁盘上。它的作用是用于数据恢复、主从复制和高可用等场景。

redolog是重做日志，记录了对InnoDB存储引擎中数据的修改操作，以及对表空间的变更等，是MySQL中的事务日志。它的作用是保证事务的原子性和持久性，当MySQL发生异常重启时，通过重做日志可以将未提交的事务重新执行。

它们的主要区别在于：

1. 记录内容不同：binlog记录了所有的数据更新操作，而redolog只记录了InnoDB存储引擎中的数据修改操作；
2. 记录方式不同：binlog以二进制的形式记录在磁盘上，而redolog以顺序写的方式记录在内存中的redo缓冲区或磁盘上的重做日志文件中；
3. 作用不同：binlog用于数据恢复、主从复制和高可用等场景，而redolog用于保证事务的原子性和持久性。

### 12. 主从复制可以提高系统的高并发能力，它体现在哪里？

1. 负载均衡：主从复制可以将读请求分摊到多个从库上，从而分担主库的负载，提高系统的并发能力。
2. 数据备份：从库可以作为主库的备份，当主库出现故障时，从库可以快速接替主库的工作，从而保证系统的可用性。
3. 数据分析：从库可以用于数据分析、数据挖掘等应用，从而减少对主库的影响，提高主库的并发能力。
4. 数据隔离：从库可以用于数据隔离，将不同的业务数据分配到不同的从库上，从而降低数据之间的耦合度，提高系统的并发能力。

### 13. 查询时主库修改了，从库还未更新造成的幻读怎么解决

主从复制时，主库和从库之间可能会存在数据不一致的情况，这是由于网络延迟或者从库的应用速度慢于主库的写入速度造成的。为了解决这个问题，有几种方法可以尝试：

- [使用MySQL 5.6或更高版本，开启基于GTID（全局事务标识符）的复制](https://zhuanlan.zhihu.com/p/335142300)[1](https://zhuanlan.zhihu.com/p/335142300)[。这样，从库可以自动找到主库的binlog位置，并且可以使用多线程复制（基于库）来提高应用速度](https://zhuanlan.zhihu.com/p/335142300)[1](https://zhuanlan.zhihu.com/p/335142300)。
- 在查询从库之前，使用`SELECT MASTER_POS_WAIT()`函数来等待从库同步到指定的binlog位置。这个函数会阻塞查询，直到从库达到指定的位置或者超时为止。
- 在查询从库之前，使用`SHOW SLAVE STATUS`命令来查看从库的复制状态。如果`Seconds_Behind_Master`列显示为0或者一个很小的值，说明从库已经基本同步了主库的数据。如果显示为NULL或者一个很大的值，说明从库有复制延迟或者出现了错误。

幻读问题通常指在一次事务中，前后读取同一范围的数据时，发现后读取的数据结果发生了变化。在主从复制中，由于从库的数据同步有一定的延迟，因此可能出现主库修改了数据，但是从库还未更新的情况，进而导致在从库上执行查询时出现幻读问题。解决幻读问题的方式主要有以下几种：

1. 提高隔离级别：在事务的隔离级别上升至可重复读或以上级别，从而避免了读取过程中出现的其他事务修改。
2. 使用悲观锁：在执行查询语句时对查询的数据行或范围加锁，确保其他事务无法修改，从而避免幻读问题。
3. 使用乐观锁：在查询数据时获取数据的版本号，当需要修改数据时，检查数据的版本号是否与当前一致，如果不一致则说明其他事务修改了该数据，需要重新执行操作。
4. 增加等待时间：当发生幻读时，可以通过增加等待时间等待从库同步完成，从而避免出现幻读问题。

### 14. 写Java程序会配置一些JVM启动参数，选用那个垃圾回收器，垃圾回收器有哪些参数

常见的垃圾回收器包括Serial、Parallel、CMS、G1等。

选用垃圾回收器需要考虑以下几个方面：

1. 应用场景：不同的垃圾回收器适用于不同的应用场景。比如，对于需要快速响应时间的应用，可以使用低暂停时间的CMS垃圾回收器，而对于需要最大吞吐量的应用，则可以使用并行GC。
2. 垃圾回收的时间：不同的垃圾回收器有不同的垃圾回收时间，需要根据应用的需求来选择。比如，对于需要最小化暂停时间的应用，可以使用低暂停时间的CMS垃圾回收器，而对于需要最大吞吐量的应用，则可以使用并行GC。
3. 堆大小：不同的垃圾回收器对堆大小的要求不同。比如，对于堆比较小的应用，可以使用串行垃圾回收器或并行垃圾回收器，而对于堆比较大的应用，则需要使用CMS或G1垃圾回收器。
4. 硬件配置：不同的垃圾回收器对硬件配置的要求不同。比如，并行垃圾回收器需要多核CPU的支持，而CMS垃圾回收器需要大量的物理内存。
5. GC日志分析：通过分析GC日志，可以了解垃圾回收器的性能表现，从而选择合适的垃圾回收器。

常见的垃圾回收器参数包括：

1. -Xmx：设置堆的最大值；
2. -Xms：设置堆的初始大小；
3. -XX:+UseSerialGC：使用Serial垃圾回收器；
4. -XX:+UseParallelGC：使用Parallel垃圾回收器；
5. -XX:+UseConcMarkSweepGC：使用CMS垃圾回收器；
6. -XX:+UseG1GC：使用G1垃圾回收器；
7. -XX:NewRatio：设置新生代与老年代的比例；
8. -XX:SurvivorRatio：设置新生代中Eden区和Survivor区的比例；
9. -XX:MaxTenuringThreshold：设置晋升到老年代的对象年龄阈值；
10. -XX:PermSize：设置永久代大小；
11. -XX:MaxPermSize：设置最大永久代大小。

### 15. 有一个队列，遍历的每个元素扔到线程池里去处理，每个线程对符合条件的元素进行删除，该怎么实现，选用那个队列，怎么来处理？

1. 选用线程安全的队列，如`ConcurrentLinkedQueue`。
2. 遍历队列中的每个元素，将符合条件的元素扔到线程池中进行处理。
3. 由于多个线程同时进行操作可能会导致并发问题，因此可以在遍历队列时将其锁定，确保同一时间只有一个线程进行队列的遍历和元素的删除操作。
4. 在处理完队列中的所有元素后，需要手动关闭线程池，确保程序的安全退出。

以下是一个示例代码：

```java
import java.util.concurrent.ConcurrentLinkedQueue;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class QueueExample {

    public static void main(String[] args) {

        // 创建线程池
        ExecutorService executorService = Executors.newFixedThreadPool(10);

        // 创建并初始化队列
        ConcurrentLinkedQueue<Integer> queue = new ConcurrentLinkedQueue<>();
        for (int i = 0; i < 1000; i++) {
            queue.add(i);
        }

        // 遍历队列，将符合条件的元素扔到线程池中进行处理
        synchronized (queue) {
            while (!queue.isEmpty()) {
                Integer element = queue.peek();
                if (element != null && element % 2 == 0) {
                    executorService.execute(() -> {
                        // 执行处理逻辑
                        System.out.println("Process element: " + element);
                        // 删除队列中的元素
                        synchronized (queue) {
                            queue.remove(element);
                        }
                    });
                } else {
                    queue.poll();
                }
            }
        }

        // 关闭线程池
        executorService.shutdown();
    }
}

```

### 16. ArrayList 和 LinkedList的区别

- ArrayList采用动态数组实现，支持随机访问和快速遍历

- LinkedList采用双向链表实现，因为只需修改指针，支持高效地增删

  链表在内存中是不连续的，随机访问效率低，每次都须遍历

  需要存储前后前后节点的地址，占用更大的存储空间

### 17.数组连续的内存空间是在物理内存还是在虚拟内存？

在物理内存中，数组是连续的。但在虚拟内存中，可能会因为分页机制而导致数组在虚拟内存中不是完全连续的。

虚拟内存是一种计算机系统内存管理的技术，在这种技术下，程序所使用的内存并不需要全部存放在物理内存中，而是在需要时根据一定的算法将虚拟地址转换为物理地址，从而实现内存的动态分配和扩充。虚拟内存通常会将物理内存分成若干个大小相等的页面，程序所使用的内存空间则由一系列连续的页面组成。当程序访问某个页面时，虚拟内存会将该页面从磁盘上读取到物理内存中，并将该页面映射到程序所使用的虚拟地址空间中，程序就可以正常地访问该页面了。因此，在虚拟内存中，数组可能会被分成多个页面，这些页面可能不是连续的，但对于程序来说，它们仍然是作为一个连续的内存空间来使用的。

### 18. 乐观锁和悲观锁怎么使用，用哪个关键字？

悲观锁假设并发访问会发生冲突，因此在访问数据之前先获取锁，确保自己是独占数据的。Java中常用的悲观锁有`synchronized`和`ReentrantLock`等。

乐观锁则假设并发访问不会发生冲突，在进行数据操作之前先不加锁，而是先读取数据，得到版本号等标识信息，然后在写回数据时检查这些标识信息是否被修改，如果没有被修改，则执行写操作，否则表示数据已经被其他线程修改，需要进行重试或回滚操作。Java中常用的乐观锁有`CAS`（比如`AtomicInteger`、`AtomicReference`等）、`StampedLock`等。

### 19.什么场景下该选用那个锁？

1. 乐观锁：
   - 适用于多读少写的场景，例如缓存、统计信息等；
   - 适用于数据冲突概率较低的场景；
   - 适用于并发性较高，锁竞争较激烈的场景。
2. 悲观锁：
   - 适用于多写少读的场景，例如订单系统、库存管理等；
   - 适用于数据冲突概率较高的场景；
   - 适用于并发性较低，锁竞争较少的场景。

### 20. 一个场景，在通信中，有10个线程，但是我要等这十个线程全部结束再做后面的操作，应该怎么实现？

可以使用==CountDownLatch==来实现这个场景。

具体实现可以分为以下几个步骤：

1. 在主线程中创建一个CountDownLatch对象，并将计数器初始化为10。
2. 创建10个线程，每个线程执行完任务后，将CountDownLatch的计数器减1。
3. 主线程调用CountDownLatch的await方法，等待计数器变为0，表示所有线程都已经执行完毕。
4. 主线程执行后续操作。

```java
import java.util.concurrent.CountDownLatch;

public class MultiThreadDemo {

    public static void main(String[] args) throws InterruptedException {
        // 创建一个CountDownLatch对象，计数器初始化为10
        CountDownLatch latch = new CountDownLatch(10);

        // 创建10个线程，每个线程执行完任务后将计数器减1
        for (int i = 0; i < 10; i++) {
            Thread thread = new Thread(() -> {
                // 执行任务
                System.out.println("Thread " + Thread.currentThread().getId() + " is running.");
                // 将计数器减1
                latch.countDown();
            });
            thread.start();
        }

        // 主线程调用await方法，等待计数器变为0
        latch.await();
        // 所有线程都已经执行完毕，执行后续操作
        System.out.println("All threads have finished their tasks.");
    }
}
```

### 21. 向面试官提问

## 三、美团一面(到店事业群-平台技术部)4.24

### 1. 自我介绍

### 2. 项目现在有人在用吗？还是练手的项目？

### 3. 简单讲一下这个项目的一个架构？

### 4. 用户登录功能怎么实现的？

### 5. 登录完之后怎么留存用户的登录信息？

### 6. 我第一次登陆成功了，访问其他页面怎么判断我的页面需不需要重新登录？

### 7. 拦截器是怎么实现的？

### 8. ArrayList和LinkedList的区别

| ArrayList                                    | LinkedList                                               |
| -------------------------------------------- | -------------------------------------------------------- |
| ① 基于数组，在内存中是连续分布的             | ① 基于双向链表，在内存中一般是不连续的                   |
| ② 随机访问速度快(可以基于下标快速定位)       | ② 随机访问速度慢(需沿着链表进行遍历)                     |
| ③ 在尾部增删的性能可以，其他位置需要移动数据 | ③ 在头尾增删的性能高，中间位置需遍历找到待处理的节点指针 |
| ④ 由于数组的扩容，可能存在尾部空间的浪费     | ④ 占用内存多(一个节点还需存前后节点的位置)               |

### 9. 讲一下HashMap的结构

数组+(链表 或 红黑树)

当链表长度过长时，会导致性能的下降；举一个例子：假设我添加了一些元素，在得到hash值后计算的桶下标均相同，那么在进行查询时，还是要全表扫描，最坏的情况下需要比较n次，树化之后最坏情况只需比较logn次。

这主要是为了避免DoS攻击，正常情况下链表长度超过8的概率是非常小的

### 10. HashMap线程不安全怎么理解？

① 数据丢失的问题，假设两个线程添加元素时索引是相同的，而且该位置时未占用的，那么在进行put操作时会先判断该位置是否为空，如果它们同时都执行到这里，那么都会进入条件语句，那么后执行的线程创建的节点就会覆盖掉先运行线程的元素，导致元素丢失。
② 在1.7版本中由于头插法，在扩容进行链表迁移的时候可能会导致死链

### 11. 哈希冲突的常规解法有哪些？

四种方法：

1. 开放定址法：我们在遇到哈希冲突时，去寻找一个新的空闲的哈希地址
   - 线性探测法：往后一直+1并%数组长度，直到找到一个空闲空间
     公式：`h(x)=(Hash(x)+i)mod (Hashtable.length);`（i会逐渐递增加1）
   - 平方探测法（二次探测），会前后寻找而不是单独方向的寻找
     公式：`h(x)=(Hash(x) +i)mod (Hashtable.length);`（i依次为+(i^2^)和-(i^2^)，i会逐渐递增加1）
   - 二次哈希
2. 再哈希法：时构造多个不同的哈希函数，等发生哈希冲突时就使用第二个、第三个……等其他的哈希函数计算地址，直到不发生冲突为止。
3. 链地址法：使用数组和链表结合的方式。当多个元素哈希到同一个位置时，将它们存储在同一个位置的链表中。
4. 建立公共溢出区：将哈希表分为基本表和溢出表，将发生冲突的都存放在溢出表中

[参考资料](https://blog.csdn.net/qq_48241564/article/details/118613312)

### 12. 知道布隆过滤器吗？

布隆过滤器（Bloom Filter）是一种概率型数据结构，用于快速判断一个元素是否属于一个集合中。

基本思想是利用多个哈希函数将要存储的元素映射到位数组的不同位置上，并将这些位置的值置为1。当查询一个元素时，同样使用多个哈希函数计算其哈希值，并检查对应的位数组位置上的值。如果所有的位置上的值都为1，则说明该元素可能存在于集合中；如果任何一个位置上的值为0，则说明该元素一定不存在于集合中。

布隆过滤器常用于需要快速判断元素是否存在的场景，如缓存、大型数据集合的过滤、URL去重等。

### 13. java中线程池是怎么创建的？

可以使用`java.util.concurrent.Executors`提供的静态方法来创建线程池

- 创建线程池对象`ExecutorService executor = Executors.newFixedThreadPool(10);`
- 提交任务`executor.submit(new MyTask());`
- 关闭线程池`executor.shutdown();`

### 14. lock和synchronized的区别？

|      | lock                                                         | synchronized                                                 |
| ---- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 语法 | Lock是一个接口，使用java实现，使用Lock时，需手动调用unlock方法释放锁 | synchronized关键字底层使用c++实现，在退出同步代码块的时候会自动释放锁 |
| 功能 | ①属于悲观锁，都支持互斥、同步、锁重入<br />②Lock支持获取等待状态、可选择公平锁、可打断、可超市、多条件变量<br />③Lock有适合不同场景的实现，比如ReentrantLock、ReentrantReadWriteLock | 属于悲观锁，都支持互斥、同步、锁重入                         |
| 性能 | 在竞争激烈时，Lock的性能一般更好                             | 在没有竞争时，synchronized有许多优化，比如偏向锁、轻量级锁   |

### 15. synchronized加锁有几种方式？

有两种方式，分别是同步代码块和同步方法

同步方法：将 `synchronized` 关键字应用于方法上，表示对整个方法进行加锁。但是它锁的是整个对象，可能导致性能问题。

同步代码块：将 `synchronized` 关键字应用于代码块上，使用代码块级的同步可以灵活控制加锁的范围。

### 16. volatile的作用？

volatile能保证操作的有序性和可见性，

- 首先是可见性，它能保证变量的值是最新的；
- 其次是有序性，在对volatile关键字修饰的变量的读写操作不会受到指令重排的影响，*它使用的是内存屏障，在对变量进行写操作时，可以防止之前的代码跑到下面来，在对变量进行读操作时，可以防止之后的代码跑到上面去。*

### 17. mysql查询-假设有两张表，其中一张学生表student，包含学生id，学生姓名，其中一张成绩表achievement，包含学生id，课程id，课程成绩，进行查询select * from achievement where student_id = ? and course_id = ?，假设学生非常多，课程也非常多，要建索引怎么实现？

```mysql
CREATE INDEX achievement_studentid _courseid ON achievement (student_id , course_id);
```

### 18. 查询出所有课程成绩>80的学生姓名、课程id和成绩

```mysql
SELECT student.name, achievement.course_id, achievement.achievement
	FROM student
	JOIN achievement ON student.id = achievement.student_id
	WHERE achievement.achievement > 80;
```

### 19. 有序链表中重复元素的删除

给定一个已排序的链表的头 head ， 删除原始链表中所有重复数字的节点，只留下不同的数字 。返回 已排序的链表 。[力扣](https://leetcode.cn/problems/remove-duplicates-from-sorted-list/)

示例 ：

![](https://assets.leetcode.com/uploads/2021/01/04/linkedlist1.jpg)

输入：head = [1,2,3,3,4,4,5]
输出：[1,2,3,4,5]

思路：左指针left和右指针right，右指针为左指针的下一个节点，如果指针指向的值相等代表有重复元素，右指针循环右移，直至遇到不同的值为止。
```java
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        ListNode left = head;
        ListNode right = head != null ? head.next : null;
        while(right != null){
            if(left.val == right.val){//有重复元素
                while(right.next != null && right.next.val == right.val){
                    right = right.next;
                }
                //删除元素
                right = right.next;//到节点4上
                left.next = right; 
            }
            left = right;
            if(right != null) right = right.next;
        }
        return head;
    }
}
```

### 20. 提问环节

## 四、阿里简历评估(阿里集团-淘宝天猫商业集团-技术线-营销与平台策略技术)4.24



## 五、江西移动5.5

### 1. 非常欢迎你来参加我们江西移动的本次招聘面试现在的话先用一分钟时间做一个自我介绍

### 2. 你毕业之后是打算在家乡发展吗？

### 3. 主要想从事那个方向的岗位？

### 4. 自我介绍里的项目是落地了吗？有没有校企合作的项目？

### 5. 是否接受调剂？调剂地点有哪些意向？

### 6. 具体实习时间的话是从几月份开始大概到什么是时候？

### 7. SpringBoot的注入是怎么实现的？

Spring框架提供了IoC（Inversion of Control）容器，当Spring Boot应用程序启动时，它会自动扫描项目中的注解，并根据注解的配置信息创建相应的Bean实例。

常用的注解有`@Autowired`、`@Component`、`@Service、@Repository、@Controller`、`@Configuration`

比如我要实现用户登录的功能，在service层，在UserService的实现类加上`@Service`注解，我在控制层想要使用UserService，加个`@Autowired`就能自动注入。

### 8. 用到的数据库是啥？

### 9. redis有了解吗？

### 10. 为什么Redis的速度快？

1. 高性能：Redis使用内存作为数据存储介质，因此具有非常高的读写性能，适用于对响应速度和吞吐量要求较高的应用场景。
2. 数据结构丰富：Redis支持丰富的数据结构，包括字符串、哈希、列表、集合、有序集合等，可以满足不同的数据处理需求。
3. 数据持久化：Redis支持数据持久化，可以将内存中的数据定时或手动写入磁盘，保证数据不会因进程退出或机器宕机而丢失。

### 11. End

## 六、5.8

### 1. 详细介绍一下你这个java项目

### 2. 怎么看待MyBatis？

MyBatis 是一个开源的持久层框架，它在 Java 开发中广泛应用于数据库访问操作。

- 它能简化数据库的访问，MyBatis 提供大量API方便地执行数据库的增删改查操作
- 可扩展性强，可以和其他框架（如Spring）非常方便地整合

### 3.MyBatis是一个ORM的框架，什么是ORM框架？

ORM（Object-Relational Mapping，对象关系映射）

将关系数据库与面向对象模型进行映射，从而实现对象与数据库之间的数据转换和交互。

### 4. 在内存中是如何分配一个对象的呢？

1. 在堆中申请内存空间
2. 分配内存
3. 对象初始化，设置默认值
4. 执行构造函数
5. 返回对象引用

### 5. 除了在堆中分配内存给对象，会不会在其他存储介质上分配呢？比如栈中呢？

在Java中，典型的对象不在堆上分配的情况有两种：TLAB（Thread Local Allocation Buffer，线程私有的分配缓冲区）和栈上分配（严格来说TLAB也是属于堆，只是在TLAB比较特殊）。

![](https://img-blog.csdnimg.cn/20190420173121975.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3poYW9ob25nX2Jv,size_16,color_FFFFFF,t_70)

为什么不直接在堆上分配呢？

堆是所有线程共享的，对于竞争资源，必须采取必要的同步，需要对整个堆加锁，会影响效率。对于某些特殊情况，可以采取避免在堆上分配对象的办法，以提高对象创建和销毁的效率。

[详细资料](https://blog.csdn.net/zhaohong_bo/article/details/89419480)

### 6. 堆和栈有什么区别？

- 堆是用于存储Java对象的一块内存区域，所有通过new关键字创建的对象都被存储在堆中。堆是线程共享的。

- 栈是一种用于存储局部变量和方法调用的内存区域，每个线程都有自己的栈空间，不同线程之间的栈空间是独立的。

### 7. 在JVM中是如何加载一个对象的呢？

主要分为加载、连接、初始化三个阶段

1. 加载
   查找并读取类的字节码文件，将其转换为JVM内部的数据结构，并在内存中创建一个对应的Class对象

2. 连接

   - 验证：验证字节码的正确性，包括文件格式、语义等方面的检查，以确保字节码的安全性和合法性。

   - 准备：为类的静态变量分配内存，并设置默认初始值。
   - 解析：将类的符号引用转换为直接引用，这是为了支持动态绑定和多态性。

3. 初始化
   执行类的初始化代码，包括静态变量的赋值和静态代码块的执行。

### 8. mysql介绍一些他的查询语句是如何进行查询的呢？

1. 客户端（运行程序）先通过连接器连接到MySQL服务器
2. 连接器通过数据库权限身份验证后，先查询数据库缓存是否存在（之前执行过相同条件的SQL查询），如果有会直接返回缓存中的数据。如果没有则会进入分析器
3. 进入分析器后会对查询语句进行语法的分析，判断该查询语句SQL是否存在语法错误，如果存在查询语法错误，会直接返回给客户端错误，如果正确会进入优化器
4. 优化器会对查询语句进行优化处理：如：如果一条语句用到了多个索引会判断哪个索引性能更好
5. 最终会进入执行器，开始执行查询语句直到查询出满足条件的所有数据，然后进行返回



![](https://img-blog.csdnimg.cn/img_convert/d979b153cf4c4b52b542c1b6fcc119b6.png)

[参考资料](https://blog.csdn.net/kaituozhe_sh/article/details/110038689)

### 9. mysql中什么叫做回表？

可以举一个简单的例子，我有一张用于用户登录的user表：

| 字段名   | 类型        | 说明   |
| -------- | ----------- | ------ |
| id       | bigint(20)  | 主键ID |
| username | varchar(20) | 用户名 |
| password | varchar(20) | 密码   |


假如现在有一个用户名为admin，密码为123的用户要登录，那我会先找出username为admin的那条用户数据

```mysql
SELECT * FROM user WHERE username = 'admin'
```

再根据查出来的user信息去对比密码是否正确
这时你发现username字段是唯一的又经常作为where条件所以可以给username字段建一个索引，于是就给username建了一个普通的B+Tree索引。这时候就出问题的，因为MySQL的InnoDB使用聚簇索引，具体的数据只和主键索引放在一起，其他的索引只存储了数据的地址（主键id）。比如上面的例子中，我根据username索引找到的只是一个username为admin这条数据的id而不是这条数据信息，所以要找到整条数据信息要根据得到的id再去找。看完上面的流程，你应该已经发现问题了，==我要通过username找到id，再根据id找整条数据，这里有两个查找过程，这是影响效率的。就像上面的两个查找过程就是回表了。==

**解决办法**
使用覆盖索引可以解决上面所说的回表的问题。还是拿上面上面登录的例子来说，其实登录只需要判断用户名和密码，如果user表中有其他用户信息也是不需要的那我们能不能只查询一次就找到这个用户名对应的密码呢。这个是可以的，上面所说的分两步查找，第一步根据username查找是肯定不能少的，那我们只要把password和索引username放到一起就可以了。我们可以建立一个（username、password）的组合索引，这里username一定要放在前面，然后我们把sql语句改一下

```mysql
SELECT username, password FROM user WHERE username = 'admin'
```

或

```mysql
SELECT password FROM user WHERE username = 'admin'
```

这样建立组合索引后根据username查找password，只要一步查找就可以查找到，因为password已经是username索引的一部分了，直接可以查出来，不再需要通过id找对应的整条数据。覆盖索引就是覆盖了多个列（字段）的索引。
[参考资料](https://blog.csdn.net/dong_ly/article/details/106627876)

### 10. 创建一个表时支持几种存储引擎？

InnoDB、MyISAM、BDB等(InnoDB、BDB提供事务安全表)

### 11. InnoDB有什么特点呢？

1. 支持事务，允许对数据进行原子性操作，支持提交和回滚
2. 行锁，多个事务可以同时对不同行的数据进行读写操作，提高性能
3. 外键约束，在表之间建立关联，保证数据的一致性
4. 数据的一致性和持久性，通过事务日志(redo log)可以在系统崩溃或者异常的状态下进行恢复

### 12.InnoDB如何实现事务机制的呢？

利用==回滚日志（undo log）==和==重做日志（redo log）==两种表实现事务，并实现 MVCC (多版本并发控制)；

**在执行事务的每条SQL时，会先将数据原值写入undo log 中， 然后执行SQL对数据进行修改，最后将修改后的值写入redo log中。**

redo log 重做日志包括两部分：1 是内存中的重做日志缓冲 ；2 是重做日志文件。在事务提交时，必须先将该事务的所有日志写入到重做日志文件进行持久化，待事务commit操作完成才算完成。

**当一个事务中的所有SQL都执行成功后，会将redo log 缓存中的数据刷入磁盘，然后提交。如果发生回滚，会根据undo log 恢复数据。**

[参考资料](https://blog.csdn.net/argleary/article/details/104189850)

### 13. 事务的隔离级别有几个？

四个

| 隔离级别        | 脏读[^ 脏读] | 不可重复读[^ 不可重复读] | 幻读[^ 幻读] |
| --------------- | :----------: | :----------------------: | :----------: |
| Read uncommited |      ⭕       |            ⭕             |      ⭕       |
| Read commited   |      ❌       |            ⭕             |      ⭕       |
| Repeatable read |      ❌       |            ❌             |      ⭕       |
| Serializable    |      ❌       |            ❌             |      ❌       |

[参考资料](https://blog.csdn.net/justlpf/article/details/106835122)

[^ 脏读]: 某个事务已更新一份数据，另一个事务在此时读取了同一份数据，由于某些原因，前一个RollBack了操作，则后一个事务所读取的数据就会是不正确的。
[^ 不可重复读]: 在一个事务的两次查询之中数据不一致，这可能是两次查询过程中间插入了一个事务更新的原有的数据。
[^ 幻读]: 在一个事务的两次查询中数据笔数不一致，例如有一个事务查询了几列(Row)数据，而另一个事务却在此时插入了新的几列数据，先前的事务在接下来的查询中，就有几列数据是未查询出来的，如果此时插入和另外一个事务插入的数据，就会报错。

### 14. 用多线程的方式写一段生产者和消费者的代码

```java
package product_consumer;

import lombok.extern.slf4j.Slf4j;

import java.util.LinkedList;

/**
 * @author Chen Y.J
 * @date 2023/4/20 11:15
 */
@Slf4j
public class MessageQueue {
    //消息队列的集合
    private final LinkedList<Message> list = new LinkedList<>();
    //消息容量
    private final int capacity;

    public MessageQueue(int capacity) {
        this.capacity = capacity;
    }

    public synchronized Message getMessage() throws InterruptedException {
        while (list.isEmpty()){
            log.debug("队列为空，等待...");
            this.wait();
        }
        Message message = list.removeFirst();
        log.debug("取出消息{}", message);
        this.notifyAll();
        return message;
    }
    public synchronized void setMessage(Message message) throws InterruptedException {
        while (list.size() == capacity){
            log.debug("队列已满，等待...");
            this.wait();
        }
        list.add(message);
        log.debug("生产消息{}", message);
        this.notifyAll();
    }
}
```

测试：

```java
package product_consumer;

/**
 * @author Chen Y.J
 * @date 2023/4/20 14:41
 */
public class Test {
    public static void main(String[] args) {
        MessageQueue queue = new MessageQueue(2);
        //生产者线程
        for (int i = 0; i < 3; i++) {
            int id = i;
            new Thread(() -> {
                try {
                    queue.setMessage(new Message(id, "mess" + id));
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }, "product" + i).start();
        }
        new Thread(() -> {
            while (true){
                try {
                    Thread.sleep(1000);
                    queue.getMessage();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }, "consumer").start();
    }
}
```

```
2023-04-20 14:54:03 [DEBUG] [product0] product_consumer.MessageQueue:38 - 生产消息Message{id=0, message=mess0}
2023-04-20 14:54:03 [DEBUG] [product1] product_consumer.MessageQueue:38 - 生产消息Message{id=1, message=mess1}
2023-04-20 14:54:03 [DEBUG] [product2] product_consumer.MessageQueue:34 - 队列已满，等待...
2023-04-20 14:54:04 [DEBUG] [consumer] product_consumer.MessageQueue:28 - 取出消息Message{id=0, message=mess0}
2023-04-20 14:54:04 [DEBUG] [product2] product_consumer.MessageQueue:38 - 生产消息Message{id=2, message=mess2}
2023-04-20 14:54:05 [DEBUG] [consumer] product_consumer.MessageQueue:28 - 取出消息Message{id=1, message=mess1}
2023-04-20 14:54:06 [DEBUG] [consumer] product_consumer.MessageQueue:28 - 取出消息Message{id=2, message=mess2}
2023-04-20 14:54:07 [DEBUG] [consumer] product_consumer.MessageQueue:24 - 队列为空，等待...
```

### 15. wait函数有什么特点

1. wait()是Object类的一个方法，任意对象都可以使用，但是必须持有锁才能调用
2. 调用了wait()之后，线程会进入等待状态，等待其他线程调用notify()或notifyAll()将其唤醒
3. 调用了wait()之后，当前线程会释放锁
4. wait()应该放在while循环中，防止虚假唤醒

### 16. sleep函数和yield函数有什么区别呢

|        | sleep                        | yield                                           |
| ------ | ---------------------------- | ----------------------------------------------- |
| 功能   | 使当前线程暂停执行指定的时间 | 放弃当前的 CPU 执行时间片，让其他线程有机会执行 |
| 锁释放 | 不会释放持有的锁             | 不会释放持有的锁                                |

### 17. 如果要你自己设计一个MVC框架，你要怎么实现呢？

1. 模型（Model）层
   - 定义数据模型和业务逻辑，封装数据访问和处理的操作。
   - 提供数据的增删改查方法，与数据库或其他数据源进行交互。
2. 视图（View）层：
   - 负责展示数据和用户界面，接收用户的输入。
   - 提供用户交互的界面，与用户进行信息交流。
3. 控制器（Controller）层
   - 接收用户的请求，并根据请求选择相应的处理逻辑。
   - 调用模型层处理数据，将结果传递给视图层展示。

### 18. 提问环节











































































