---
title: Entradas para a classe de XslCompiledTransform
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
ms.assetid: 834049f1-ab41-449e-9f10-4a1d0701bc48
caps.latest.revision: 
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 7aac1e85bdc27c9c8394eadcae841069115b369d
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/23/2017
---
# <a name="inputs-to-the-xslcompiledtransform-class"></a>Entradas para a classe de XslCompiledTransform
O método de <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> aceita três tipos de entrada para o documento de origem: um objeto que implementa a interface de <xref:System.Xml.XPath.IXPathNavigable> , um objeto de <xref:System.Xml.XmlReader> que lê o documento de origem, ou URI de uma cadeia de caracteres.  
  
> [!NOTE]
>  A classe de <xref:System.Xml.Xsl.XslCompiledTransform> preserva o espaço em branco por padrão. Isso é de acordo com a seção 3,4 de recomendação W3C XSLT seção 1,0 (3,4, http://www.w3.org/TR/xslt.html#strip).  
  
## <a name="ixpathnavigable-interface"></a>Interface de IXPathNavigable  
 A interface de <xref:System.Xml.XPath.IXPathNavigable> é implementada nas classes de <xref:System.Xml.XmlNode> e de <xref:System.Xml.XPath.XPathDocument> . Essas classes representam um cache de memória de dados XML.  
  
-   A classe de <xref:System.Xml.XmlNode> é baseado no W3C Document Object Model (DOM) e inclui recursos de edição.  
  
-   A classe de <xref:System.Xml.XPath.XPathDocument> é um repositório de dados somente leitura com base no modelo de dados XPath. <xref:System.Xml.XPath.XPathDocument> é a classe recomendada para processar XSLT. Fornece um desempenho mais rápido quando comparada a <xref:System.Xml.XmlNode> a classe.  
  
> [!NOTE]
>  As transformações são aplicadas ao documento no dataset. Ou seja se você passar em um nó que não seja o nó de diretório base, isso não impede que o processo de transformação acessar todos os nós do documento carregado. Para transformar um fragmento de nó, você deve criar um objeto que contém apenas o fragmento de nó, e passa esse objeto para o método de <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> . Para saber mais, confira [Como transformar um fragmento de nó](../../../../docs/standard/data/xml/how-to-transform-a-node-fragment.md).  
  
 O exemplo a seguir usa o método de <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A?displayProperty=nameWithType> para transformar o arquivo de books.xml para o arquivo de books.html usando a folha de estilos de transform.xsl. Os arquivos books.xml e transform.xsl podem ser encontrados neste tópico: [Como executar uma transformação XSLT usando um assembly](../../../../docs/standard/data/xml/how-to-perform-an-xslt-transformation-by-using-an-assembly.md).  
  
 [!code-csharp[XslCompiledTransform.Transform2#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XslCompiledTransform.Transform2/CS/Program.cs#1)]
 [!code-vb[XslCompiledTransform.Transform2#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XslCompiledTransform.Transform2/VB/Module1.vb#1)]  
  
## <a name="xmlreader-object"></a>Objeto de XmlReader  
 As tanto o método de <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> do nó atual de <xref:System.Xml.XmlReader> através de todos seus filhos. Isso permite que você use uma parte de um documento como o documento de contexto. Depois que o método de <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> retorna, <xref:System.Xml.XmlReader> está localizado no nó seguir após ao final do documento de contexto. Se o final do documento é alcançada, <xref:System.Xml.XmlReader> está localizado no final do arquivo (EOF).  
  
 O exemplo a seguir usa o método de <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A?displayProperty=nameWithType> para transformar o arquivo de books.xml para o arquivo de books.html usando a folha de estilos de transform.xsl. Os arquivos books.xml e transform.xsl podem ser encontrados neste tópico: [Como executar uma transformação XSLT usando um assembly](../../../../docs/standard/data/xml/how-to-perform-an-xslt-transformation-by-using-an-assembly.md).  
  
 [!code-csharp[XslCompiledTransform.Transform2#2](../../../../samples/snippets/csharp/VS_Snippets_Data/XslCompiledTransform.Transform2/CS/Program.cs#2)]
 [!code-vb[XslCompiledTransform.Transform2#2](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XslCompiledTransform.Transform2/VB/Module1.vb#2)]  
  
## <a name="string-uri"></a>URI de cadeia de caracteres  
 Você também pode especificar o URI de documento de origem como sua entrada XSLT. <xref:System.Xml.XmlResolver> é usado para resolver URI. Você pode especificar <xref:System.Xml.XmlResolver> para usar passando para o método de <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> . Se <xref:System.Xml.XmlResolver> não for especificado, o método de <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> usa <xref:System.Xml.XmlUrlResolver> padrão sem credenciais.  
  
 O exemplo a seguir usa o método de <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A?displayProperty=nameWithType> para transformar o arquivo de books.xml para o arquivo de books.html usando a folha de estilos de transform.xsl. Os arquivos books.xml e transform.xsl podem ser encontrados neste tópico: [Como executar uma transformação XSLT usando um assembly](../../../../docs/standard/data/xml/how-to-perform-an-xslt-transformation-by-using-an-assembly.md).  
  
 [!code-csharp[XslCompiledTransform.Transform2#3](../../../../samples/snippets/csharp/VS_Snippets_Data/XslCompiledTransform.Transform2/CS/Program.cs#3)]
 [!code-vb[XslCompiledTransform.Transform2#3](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XslCompiledTransform.Transform2/VB/Module1.vb#3)]  
  
 Para saber mais, confira [Resolvendo recursos externos durante o processamento de XSLT](../../../../docs/standard/data/xml/resolving-external-resources-during-xslt-processing.md).  
  
## <a name="see-also"></a>Consulte também  
 [Transformações XSLT](../../../../docs/standard/data/xml/xslt-transformations.md)
