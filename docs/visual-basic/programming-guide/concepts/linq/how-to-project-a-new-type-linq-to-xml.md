---
title: "How to: Project a New Type (LINQ to XML)"
ms.date: 07/20/2015
ms.assetid: 8cfb24f5-89b2-4cfb-b85d-e7963f8f1845
---
# How to: Project a New Type (LINQ to XML) (Visual Basic)
Other examples in this section have shown queries that return results as <xref:System.Collections.Generic.IEnumerable%601> of <xref:System.Xml.Linq.XElement>, <xref:System.Collections.Generic.IEnumerable%601> of `string`, and <xref:System.Collections.Generic.IEnumerable%601> of `int`. These are common result types, but they are not appropriate for every scenario. In many cases you will want your queries to return an <xref:System.Collections.Generic.IEnumerable%601> of some other type.  
  
## Example  
 This example shows how to instantiate objects in the `Select` clause. The code first defines a new class with a constructor, and then modifies the `Select` statement so that the expression is a new instance of the new class.  
  
 This example uses the following XML document: [Sample XML File: Typical Purchase Order (LINQ to XML)](sample-xml-file-typical-purchase-order-linq-to-xml.md).  
  
```vb  
Public Class NameQty  
    Public name As String  
    Public qty As Integer  
    Public Sub New(ByVal n As String, ByVal q As Integer)  
        name = n  
        qty = q  
    End Sub  
End Class  
  
Public Class Program  
    Shared Sub Main()  
        Dim po As XElement = XElement.Load("PurchaseOrder.xml")  
  
        Dim nqList As IEnumerable(Of NameQty) = _  
            From n In po...<Item> _  
            Select New NameQty( _  
                n.<ProductName>.Value, CInt(n.<Quantity>.Value))  
  
        For Each n As NameQty In nqList  
            Console.WriteLine(n.name & ":" & n.qty)  
        Next  
    End Sub  
End Class  
```  
  
 This example uses the `M:System.Xml.Linq.XElement.Element` method that was introduced in the topic [How to: Retrieve a Single Child Element (LINQ to XML) (Visual Basic)](how-to-retrieve-a-single-child-element-linq-to-xml.md). It also uses casts to retrieve the values of the elements that are returned by the `M:System.Xml.Linq.XElement.Element` method.  
  
 This example produces the following output:  
  
```console  
Lawnmower:1  
Baby Monitor:2  
```  
  
## See also

- [Projections and Transformations (LINQ to XML) (Visual Basic)](projections-and-transformations-linq-to-xml.md)
