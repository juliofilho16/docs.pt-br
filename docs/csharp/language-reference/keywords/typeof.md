---
title: typeof (Referência de C#)
ms.date: 07/20/2015
f1_keywords:
- typeof
- typeof_CSharpKeyword
helpviewer_keywords:
- typeof keyword [C#]
ms.assetid: 0c08d880-515e-46bb-8cd2-48b8dd62c08d
ms.openlocfilehash: be79fa4f2cfb1119a50201bf6c18a144726f2f21
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="typeof-c-reference"></a>typeof (Referência de C#)
Usado para obter o objeto `System.Type` para um tipo. Uma expressão `typeof` usa o seguinte formato:  
  
```  
System.Type type = typeof(int);  
```  
  
## <a name="remarks"></a>Comentários  
 Para obter o tipo de tempo de execução de uma expressão, você pode usar o método do .NET Framework <xref:System.Object.GetType%2A>, assim como no exemplo a seguir:  
  
```  
int i = 0;  
System.Type type = i.GetType();  
```  
  
 O operador `typeof` não pode ser sobrecarregado.  
  
 O operador `typeof` também pode ser usado em tipos genéricos abertos. Tipos com mais de um parâmetro de tipo devem ter o número apropriado de vírgulas na especificação. O exemplo a seguir mostra como determinar se o tipo de retorno de um método é um <xref:System.Collections.Generic.IEnumerable%601> genérico. Suponha que o método seja uma instância de um tipo de MethodInfo:  
  
```  
string s = method.ReturnType.GetInterface  
    (typeof(System.Collections.Generic.IEnumerable<>).FullName);  
```  
  
## <a name="example"></a>Exemplo  
 [!code-csharp[csrefKeywordsOperator#12](../../../csharp/language-reference/keywords/codesnippet/CSharp/typeof_1.cs)]  
  
## <a name="example"></a>Exemplo  
 Este exemplo usa o método <xref:System.Object.GetType%2A> para determinar o tipo que é usado para conter o resultado de um cálculo numérico. Isso depende dos requisitos de armazenamento do número resultante.  
  
 [!code-csharp[csrefKeywordsOperator#13](../../../csharp/language-reference/keywords/codesnippet/CSharp/typeof_2.cs)]  
  
## <a name="c-language-specification"></a>Especificação da Linguagem C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.Type?displayProperty=nameWithType>  
 [Referência de C#](../../../csharp/language-reference/index.md)  
 [Guia de Programação em C#](../../../csharp/programming-guide/index.md)  
 [Palavras-chave do C#](../../../csharp/language-reference/keywords/index.md)  
 [is](../../../csharp/language-reference/keywords/is.md)  
 [Palavras-chave do operador](../../../csharp/language-reference/keywords/operator-keywords.md)
