---
title: "Notas de implementação de suporte do tipo XML"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 26b071f3-1261-47ef-8690-0717f5cd93c1
caps.latest.revision: 
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 8c2706782ed1242ecdb5af1fdfab7a3f24e19236
ms.sourcegitcommit: 15316053918995cc1380163a7d7e7edd5c44e6d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/19/2018
---
# <a name="xml-type-support-implementation-notes"></a>Notas de implementação de suporte do tipo XML
Este tópico descreve alguns detalhes de implementação de que você deseja estar ciente.  
  
## <a name="list-mappings"></a>Mapeamentos de lista  
 Os tipos <xref:System.Collections.IList>, <xref:System.Collections.ICollection>, <xref:System.Collections.IEnumerable>, **Type[]** e <xref:System.String> são usados para representar tipos de lista de XSD (linguagem de definição de esquema XML).  
  
## <a name="union-mappings"></a>Mapeamentos de união  
 Os tipos de união são representados usando o tipo de <xref:System.Xml.Schema.XmlAtomicValue> ou de <xref:System.String> . O tipo de origem ou o tipo de destino portanto deve ser sempre <xref:System.String> ou <xref:System.Xml.Schema.XmlAtomicValue>.  
  
 Se o objeto de <xref:System.Xml.Schema.XmlSchemaDatatype> representa um tipo de lista o objeto converte o valor da cadeia de caracteres de entrada em uma lista de um ou mais objetos. Se <xref:System.Xml.Schema.XmlSchemaDatatype> representa um tipo de união então é feita uma tentativa de analisar o valor de entrada como um tipo de membro de união. Se a tentativa de análise falhar na conversão será tentada com o membro a seguir de união e assim por diante até que a conversão foi bem-sucedida, ou não há nenhum outro tipo do membro a tentar nesse caso, uma exceção é lançada.  
  
## <a name="differences-between-clr-and-xml-data-types"></a>Diferenças entre tipos de dados de CLR e XML  
 O exemplo a seguir descreve determinadas incompatíveis que podem ocorrer entre tipos de CLR e tipos de dados XML e como elas são tratadas.  
  
> [!NOTE]
>  O `xs` prefixo é mapeado para o http://www.w3.org/2001/XMLSchema e URI de namespace.  
  
### <a name="systemtimespan-and-xsduration"></a>System.TimeSpan e xs:duration  
 O tipo de `xs:duration` é ordenada parcialmente em que há determinados valores de duração que são diferentes mas equivalente. Isso significa que para o valor do tipo de `xs:duration` como 1 mês (P1M) está menos de 32 dias (P32D), maior que 27 dias (P27D) e equivalente a 28, 29 ou 30 dias.  
  
 A classe de <xref:System.TimeSpan> não suporta este pedido parcial. Em vez disso, escolher um número específico de dias para 1 e 1 ano mês; 365 dias e 30 dias respectivamente.  
  
 Para obter mais informações sobre o `xs:duration` de tipo, consulte W3C XML Schema Part 2: recomendação de tipos de dados em http://www.w3.org/TR/xmlschema-2/.  
  
### <a name="xstime-gregorian-date-types-and-systemdatetime"></a>xs:time, tipos gregorianos de data, e System.DateTime  
 Quando um valor de `xs:time` é mapeado para um objeto de <xref:System.DateTime> , o campo de <xref:System.DateTime.MinValue> é usado para inicializar propriedades de data do objeto de <xref:System.DateTime> (como <xref:System.DateTime.Year%2A>, <xref:System.DateTime.Month%2A>, e <xref:System.DateTime.Day%2A>) para o valor possível com o menor de <xref:System.DateTime> .  
  
 Da mesma forma, as instâncias de `xs:gMonth`, `xs:gDay`, `xs:gYear`, `xs:gYearMonth` e `xs:gMonthDay` também são mapeados para um objeto de <xref:System.DateTime> . As propriedades não usado no objeto de <xref:System.DateTime> são inicializadas àquelas de <xref:System.DateTime.MinValue>.  
  
> [!NOTE]
>  Você não pode depender no valor de <xref:System.DateTime.Year%2A?displayProperty=nameWithType> quando o conteúdo está digitado como `xs:gMonthDay`. O valor de <xref:System.DateTime.Year%2A?displayProperty=nameWithType> é sempre definido como 1904 nesse caso.  
  
### <a name="xsanyuri-and-systemuri"></a>xs:anyURI e System.Uri  
 Quando uma instância de `xs:anyURI` que representa o URL relativa é mapeada a <xref:System.Uri>, o objeto de <xref:System.Uri> não tem URI base.  
  
## <a name="see-also"></a>Consulte também  
 [Type Support in the System.Xml Classes](../../../../docs/standard/data/xml/type-support-in-the-system-xml-classes.md) (Suporte a tipo nas classes System.XML)
