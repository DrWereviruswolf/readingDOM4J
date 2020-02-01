## 第三章: 高级设计意图分析

在第二章中，我们看到大量的DOM节点都采用了flyweight类继承abstract抽象类，去添加一些default类没有的关键信息。
接下来，我们会重点以享元模式为线来深入理解Dom4j为内存优化而改进的设计意图，同时还会涉及工厂模式和适配器模式。

 <img src="/assets/design_pattrn.png" width = "1000" height = "220" align=center />