### 3.2 解决方案

GOF(Erich Gamma, Richard Helm, Ralph Johnson, John Vlissides)在《设计模式：可复用面向对象软件的基础》中对**享元模式**(Flyweight)的定义是：
> 利用共享方法更高效地支持大数量的细粒度对象。

![](/assets/flywght.png)

Flyweight的主要参与者是**Flyweight Factory**和**Client**, **享元工厂**往往负责管理、创建和存储享元对象，而**client**是对享元对象的引用。

那Dom4j中如何界定这种client和factory的任务分工呢？

我原本以为从下面的Dom4j的类图中可以看出Default Attribute维持着对享元的引用，但后来才发现自己理解错了。

>类图：继承关系
![](/assets/inherit.png)

仔细解构dom4j享元层与client可以发现, default client往往存储着所挂载的父元素节点，而剩下的例如文本的信息，属性的Qname和属性值被存储在了享元层中。

`Client示例：`
![](/assets/6.png)

`Flyweight示例:`
![](/assets/7.png)

在元素添加属性和属性值时，在Document Factory中构造属性时，所有的属性都只需要两个值qname和value, 也可以看出Dom4j设计者精巧的Adapter适配器模式思想，将一个类的接口转化为客户希望的另一个接口，这种接口的改动封装了内部的算法设计，体现了对客户的信息隐藏。

>图8

![](/assets/8.png)

我们的工厂会将父元素节点和属性名的信息过滤掉，以Qname的方式进行构造。默认属性构造方法会将Qname和value交给享元属性类进行存储。

在执行下面的代码时

 <img src="/assets/8_5.png" width = "340" height = "26"/>

我们清楚地看到
>图9

![](/assets/9.png)

享元层把一个XML元素属性的属性名和名字空间打包递交给了qname，把value交给成员变量value。
此时一个对象被构造完毕，也是真正进入了内存。
按照前面所述，如果**Flyweight Attribute**是所谓的享元，那费解的地方在于，qname和value似乎包含了一个节点的所有信息，**DefaultAttribute**中的parent成员变量也只不过在Element add attribute时指针调动一下，享元在哪里呢？

需要理解的是，java里面对象的复制只是一种**软拷贝**，维护的变量qname和value也只不过是一种赋值关系，对众多节点而言是必要的，而且并不会耗费大量内存。
真正考虑内存时应该关心的也就是硬数据的存储位置。

我们把视线转向图8中**createAttribute**紧接调用的**createQname**

>图10

![](/assets/10.png)

**QnameCache**是真正的享元工厂，完成了对Qname的存储与创建。QnameCache的get具有享元模式的明显特点:去寻找享元池（cache）中具有该外蕴状态(name)的对象，将其返回，如果不存在，则将这个name放入享元池中。

![](/assets/11.png)

QnameCache的内部实现是**Hash表**,这在Qname的成员变量中就可见端倪。

![](/assets/12.png)

另外值得一提的QnameCache的成员变量并不是**NamespaceCache**,而是一种**synchronizedMap**,有别于NamespaceCache所使用的**ConcurrentHashMap**。这两种map都支持多线程同步访问，我也暂未发现这两种数据结构对两种Cache的应用有何区分。