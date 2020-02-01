### 1.3 XML文档树结构

下面我们简要介绍一下 XML 的文档树结构，理解这种树的构成对理解 DOM4j 的处理流程有重要帮助。下面是一个典型的 XML 文档。

###### 例1
```xml
<?xml version="1.0" encoding="UTF-8"?>
<bookstore>
<book category="cooking">
<title lang="en">Everyday Italian</title>
<author>Giada De Laurentiis</author>
<year>2005</year>
<price>30.00</price>
</book>
<book category="children">
<title lang="en">Harry Potter</title>
<author>J K. Rowling</author>
<year>2005</year>
<price>29.99</price>
</book>
</bookstore>
```
XML 使用简单的具有**自我描述性**的语法。
第一行是 XML **声明**，它定义了 XML 的版本号(1.0)和所使用的编码方式(UTF-8)。

第二行便是 XML 的**根元素**，每个 XML 都需要一个根元素。
它类似于描述了本文档的主题:bookstore。
接下来的若干行可以从形如<>和</>的打开与关闭标签中分别看出包含关系与并列关系，我们称包括打开标签、关闭标签和它们之间的内容成为**元素**，元素之间的关系可以抽象成树结构中的 parent, children, sibling。

我们还可以发现打开标签中包含着一个等式，等式左右分别规定了**属性**与**属性值**，用于为元素提供额外信息。
包含在元素内且没有打开关闭标签的称为**文本**，文本主要负责存储元素信息。
我们将例 1 中的每个上述的元素、属性、文本写成如下的树结构，每个信息都成了一个**节点**。

![](/assets/xml_tree.png)

总结XML文档树的结构如下

```xml
<root>
  <child>
    <subchild>.....</subchild>
  </child>
</root>
```

