---
title: Clonagem contra. Anexando (Visual Basic)
ms.date: 07/20/2015
ms.assetid: 3c3bd105-c9d3-49bd-875b-27ab4e8bc7a3
ms.openlocfilehash: 35a265d2aaef40977a9a6b89d174e9a585c525c8
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="cloning-vs-attaching-visual-basic"></a>Clonagem contra. Anexando (Visual Basic)
Ao adicionar <xref:System.Xml.Linq.XNode> (incluindo <xref:System.Xml.Linq.XElement>) ou objetos de <xref:System.Xml.Linq.XAttribute> para uma nova árvore, se o novo conteúdo não tem nenhum pai, os objetos estão conectados somente à árvore XML. Se o novo conteúdo já parented, e é parte de outra árvore XML, o novo conteúdo são clonados. O conteúdo recentemente clonado é anexado a árvore XML.  
  
## <a name="example"></a>Exemplo  
 O código a seguir demonstra o comportamento quando você adiciona um elemento parented a uma árvore, e quando você adiciona um elemento sem o pai a uma árvore.  
  
```vb  
' Create a tree with a child element.  
Dim xmlTree1 As XElement = _  
    <Root>  
        <Child1>1</Child1>  
    </Root>  
  
' Create an element that is not parented.  
Dim child2 As XElement = <Child2>2</Child2>  
  
' Create a tree and add Child1 and Child2 to it.  
Dim xmlTree2 As XElement = _  
    <Root>  
        <%= xmlTree1.<Child1>(0) %>  
        <%= child2 %>  
    </Root>  
  
' Compare Child1 identity.  
Console.WriteLine("Child1 was {0}", _  
    IIf(xmlTree1.Element("Child1") Is xmlTree2.Element("Child1"), _  
    "attached", "cloned"))  
  
' Compare Child2 identity.  
Console.WriteLine("Child2 was {0}", _  
    IIf(child2 Is xmlTree2.Element("Child2"), _  
    "attached", "cloned"))  
```  
  
 Este exemplo gera a seguinte saída:  
  
```  
Child1 was cloned  
Child2 was attached  
```  
  
## <a name="see-also"></a>Consulte também  
 [Criando árvores XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/creating-xml-trees.md)
