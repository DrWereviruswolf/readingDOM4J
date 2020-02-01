### 1.5 需求分析

#### 1. 解析XML文档
* 用例名称：解析（parse）
* 场景：文件或流、用户
* 用例描述：用户导入与XML相关的包，创建SAXReader, 从文件或流创建文档，通过调用document.selectNodes()获取所需的节点。提取XML文档的根元素，然后通过遍历器寻找想要的元素，通过attributeValue(属性)获取属性值，通过elementText获取元素的文本。
* 用例价值：用户得到XML文档的数据信息

#### 2. 创建或修改XML文档
* 用例名称：创建 (create)
* 场景：文件或流、用户
* 用例描述：用户先寻求dom4j的DocumentHelper在Dom4j内由文档工厂创建一个文档，然后通过文档的addElement方法在文档中添加节点，即为根节点。如果要在对某个元素内部添加新的元素，调用新元素的addElement即可。如果有附属的属性和文本需要添加，Element的返回值同样为Element的addAttribute和addText接口可以调用。OutputFormat类会构造自身的一个对象，然后根据特定的格式需要来添加空格或空行。最后根据该格式构建一个XML Writer对象，由它将规整后的文档打印到文件或输出流中。
* 用例价值：用户可以方便地创建新的XML文档。
* 约束和限制：使用相同的元素名时应注意命名空间不同。


