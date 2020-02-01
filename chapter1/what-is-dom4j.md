### 1.2 什么是Dom4j

**Dom4j** 意为 DOM for java, 是一款 java 开源库，主要用于解析 XML,此外还协同处理 XPATH 和 XSLT。

> **Dom4j 官方释义** :Dom4j is an easy to use, open source library for working with XML, XPath and XSLT on the Java platform using the Java Collections Framework and with full support for DOM, SAX and JAXP.

它相比于其他 XML 解析库如 DOM, SAX, JDOM 具有以下两个特点：
* 高度灵活
* 内存使用高效

**DOM** 接口通过一种**分层对象模型**来访问 XML 文档信息，即用一棵**节点树**的形式来描述 XML 的文档结构。
但 DOM解析库 由于需要一次性把整个文档转化成树结构，所以对内存的需求就比较高，遍历操作带来的开销较大。
这就可能会导致内存溢出等极端情况发生。

