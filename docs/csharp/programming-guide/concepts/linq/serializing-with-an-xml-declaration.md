---
title: "带 XML 声明的序列化 (C#) | Microsoft Docs"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: c237fa4a-a042-40fd-886f-17b54c66bb75
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 5c0389630c7fc4b8aa394974b7e42cce2a5101a4
ms.lasthandoff: 03/13/2017

---
# <a name="serializing-with-an-xml-declaration-c"></a>带 XML 声明的序列化 (C#)
本主题说明如何控制序列化是否生成 XML 声明。  
  
## <a name="xml-declaration-generation"></a>XML 声明的生成  
 使用 <xref:System.Xml.Linq.XElement.Save%2A?displayProperty=fullName> 方法或 <xref:System.Xml.Linq.XDocument.Save%2A?displayProperty=fullName> 方法序列化为 <xref:System.IO.File> 或 <xref:System.IO.TextWriter> 会生成 XML 声明。 在序列化为 <xref:System.Xml.XmlWriter> 时，编写器设置（在 <xref:System.Xml.XmlWriterSettings> 对象中指定）确定是否生成 XML 声明。  
  
 如果要使用 `ToString` 方法序列化为字符串，则生成的 XML 不会包括 XML 声明。  
  
### <a name="serializing-with-an-xml-declaration"></a>使用 XML 声明进行序列化  
 下面的示例创建一个 <xref:System.Xml.Linq.XElement>，将文档保存到文件，然后将文件打印到控制台：  
  
```csharp  
XElement root = new XElement("Root",  
    new XElement("Child", "child content")  
);  
root.Save("Root.xml");  
string str = File.ReadAllText("Root.xml");  
Console.WriteLine(str);  
```  
  
 该示例产生下面的输出：  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<Root>  
  <Child>child content</Child>  
</Root>  
```  
  
### <a name="serializing-without-an-xml-declaration"></a>不带 XML 声明的序列化  
 下面的示例演示如何将 <xref:System.Xml.Linq.XElement> 保存到 <xref:System.Xml.XmlWriter>。  
  
```csharp  
StringBuilder sb = new StringBuilder();  
XmlWriterSettings xws = new XmlWriterSettings();  
xws.OmitXmlDeclaration = true;  
  
using (XmlWriter xw = XmlWriter.Create(sb, xws)) {  
    XElement root = new XElement("Root",  
        new XElement("Child", "child content")  
    );  
    root.Save(xw);  
}  
Console.WriteLine(sb.ToString());  
```  
  
 该示例产生下面的输出：  
  
```xml  
<Root><Child>child content</Child></Root>  
```  
  
## <a name="see-also"></a>请参阅  
 [序列化 XML 树 (C#)](../../../../csharp/programming-guide/concepts/linq/serializing-xml-trees.md)
