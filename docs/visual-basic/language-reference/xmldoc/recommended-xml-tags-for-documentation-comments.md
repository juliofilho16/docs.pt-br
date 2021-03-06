---
title: marcações XML recomendadas para comentários da documentação (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.XmlDocComment
helpviewer_keywords:
- tags, XML
- XML comments, recommended tags [Visual Basic]
- comments, recommended XML tags
ms.assetid: 294e0736-ff1e-498e-af83-6db71ed41a72
ms.openlocfilehash: 8f27a892117980e89fa7143b7e49551b9e8703f6
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="recommended-xml-tags-for-documentation-comments-visual-basic"></a>marcações XML recomendadas para comentários da documentação (Visual Basic)
O compilador do Visual Basic pode processar comentários de documentação em seu código para um arquivo XML. Você pode usar ferramentas adicionais para processar o arquivo XML na documentação.  
  
 Comentários XML são permitidos em construções de código, como tipos e membros de tipos. Para tipos parciais, apenas uma parte do tipo pode ter comentários XML, embora não haja nenhuma restrição em comentar seus membros.  
  
> [!NOTE]
>  Comentários de documentação não podem ser aplicados a namespaces. O motivo é que um namespace pode abranger vários assemblies, e não todos os assemblies tem de ser carregado ao mesmo tempo.  
  
 O compilador processa qualquer marca que é um XML válido. As seguintes marcas fornecem funcionalidades comumente usadas na documentação do usuário.  
  
||||  
|---|---|---|  
|[\<c>](../../../visual-basic/language-reference/xmldoc/c.md)|[\<code>](../../../visual-basic/language-reference/xmldoc/code.md)|[\<example>](../../../visual-basic/language-reference/xmldoc/example.md)|  
|[\<exceção >](../../../visual-basic/language-reference/xmldoc/exception.md) <sup>1</sup>|[\<incluir >](../../../visual-basic/language-reference/xmldoc/include.md) <sup>1</sup>|[\<list>](../../../visual-basic/language-reference/xmldoc/list.md)|  
|[\<para>](../../../visual-basic/language-reference/xmldoc/para.md)|[\<param >](../../../visual-basic/language-reference/xmldoc/param.md) <sup>1</sup>|[\<paramref>](../../../visual-basic/language-reference/xmldoc/paramref.md)|  
|[\<permissão >](../../../visual-basic/language-reference/xmldoc/permission.md) <sup>1</sup>|[\<remarks>](../../../visual-basic/language-reference/xmldoc/remarks.md)|[\<returns>](../../../visual-basic/language-reference/xmldoc/returns.md)|  
|[\<Consulte >](../../../visual-basic/language-reference/xmldoc/see.md) <sup>1</sup>|[\<seealso >](../../../visual-basic/language-reference/xmldoc/seealso.md) <sup>1</sup>|[\<summary>](../../../visual-basic/language-reference/xmldoc/summary.md)|  
|[\<typeparam >](../../../visual-basic/language-reference/xmldoc/typeparam.md) <sup>1</sup>|[\<value>](../../../visual-basic/language-reference/xmldoc/value.md)||  
  
 (<sup>1</sup> o compilador verifica a sintaxe.)  
  
> [!NOTE]
>  Se você quiser colchetes angulares sejam exibido no texto de um comentário de documentação, use `<` e `>`. Por exemplo, a cadeia de caracteres `"<text in angle brackets>"` será exibido como `<text in angle``brackets>`.  
  
## <a name="see-also"></a>Consulte também  
 [Documentando o Código com XML](../../../visual-basic/programming-guide/program-structure/documenting-your-code-with-xml.md)  
 [/doc](../../../visual-basic/reference/command-line-compiler/doc.md)  
 [Como criar documentação XML](../../../visual-basic/programming-guide/program-structure/how-to-create-xml-documentation.md)
