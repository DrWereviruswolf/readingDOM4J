### 1.4 XML命名空间

在XML中，如果两个不同的文档使用相同的元素名，在合并时就会发生冲突。
为了避免冲突，可以通过使用名称前缀避免。
在XML使用前缀时，一个在元素的开始标签的xmlns属性中定义的命名空间(Namespace)必须被定义。
命名空间的声明按照如下语法：
*<center> xmlns:前缀=“URI” </center>*

###### 例2
```xml
<root>

<h:table xmlns:h="http://www.w3.org/TR/html4/">
<h:tr>
<h:td>Apples</h:td>
<h:td>Bananas</h:td>
</h:tr>
</h:table>

<f:table xmlns:f="http://www.w3cschool.cc/furniture">
<f:name>African Coffee Table</f:name>
<f:width>80</f:width>
<f:length>120</f:length>
</f:table>

</root>
```
在上面的实例中，<table>标签的xmlns属性定义了h:和f:前缀的合格命名空间。所有带有相同前缀的子元素都会和同一个命名空间相关联。另外W3C规定了Qname是带前缀或不带前缀的名字。