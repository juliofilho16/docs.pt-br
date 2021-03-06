---
title: float (Referência de C#)
ms.date: 07/20/2015
f1_keywords:
- float
- float_CSharpKeyword
helpviewer_keywords:
- float keyword [C#]
- floating-point numbers [C#], float keyword
ms.assetid: 1e77db7b-dedb-48b7-8dd1-b055e96a9258
ms.openlocfilehash: edeed59da26c7007b23e1eec8c05fbd2e6d34d36
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="float-c-reference"></a>float (Referência de C#)
A palavra-chave `float` indica um tipo simples que armazena valores de ponto flutuante de 32 bits. A tabela a seguir mostra a precisão e o intervalo aproximado do tipo `float`.  
  
|Tipo|Intervalo aproximado|Precisão|Tipo do .NET Framework|  
|----------|-----------------------|---------------|-------------------------|  
|`float`|-3,4 × 10<sup>38</sup> a +3,4 × 10<sup>38</sup>|7 dígitos|<xref:System.Single?displayProperty=nameWithType>|  
  
## <a name="literals"></a>Literais  
 Por padrão, um literal numérico real no lado direito do operador de atribuição é tratado como [double](double.md). Portanto, para inicializar uma variável float, use o sufixo `f` ou `F`, como no exemplo a seguir:  
  
```csharp
float x = 3.5F;  
```
  
 Se você não usar o sufixo na declaração anterior, obterá um erro de compilação porque está tentando armazenar um valor [double](double.md) em uma variável `float`.  
  
## <a name="conversions"></a>Conversões  
 Você pode misturar tipos integrais numéricos e tipos de ponto flutuante em uma expressão. Nesse caso, os tipos integrais são convertidos em tipos de ponto flutuante. A avaliação da expressão é executada de acordo com as regras a seguir:  
  
-   Se um dos tipos de ponto flutuantes for [double](double.md), a expressão será avaliada como [double](double.md) ou [bool](bool.md) em expressões relacionais ou boolianas.  
  
-   Se não houver um tipo [double](double.md) na expressão, ela será avaliada como `float` ou [bool](bool.md) em expressões relacionais ou boolianas.  
  
 Uma expressão de ponto flutuante pode conter os seguintes conjuntos de valores:  
  
-   Zero positivo e negativo  
  
-   Infinito positivo e negativo  
  
-   Valor NaN (não é um número)  
  
-   O conjunto finito de valores diferentes de zero  
  
 Para obter mais informações sobre esses valores, consulte o padrão IEEE para Aritmética de ponto flutuante binário, disponível no site do [IEEE](http://www.ieee.org).  
  
## <a name="example"></a>Exemplo  
 No exemplo a seguir, um [int](int.md), um [short](short.md) e um `float` são incluídos em uma expressão matemática dando um resultado `float`. (Lembre-se de que `float` é um alias para o tipo <xref:System.Single?displayProperty=nameWithType>.) Observe que não há nenhum [double](double.md) na expressão.  
  
 [!code-csharp[csrefKeywordsTypes#13](../../../csharp/language-reference/keywords/codesnippet/CSharp/float_1.cs)]  
  
## <a name="c-language-specification"></a>Especificação da Linguagem C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.Single>  
 [Referência de C#](../../../csharp/language-reference/index.md)  
 [Guia de Programação em C#](../../../csharp/programming-guide/index.md)  
 [Transmissões e conversões de tipo](../../../csharp/programming-guide/types/casting-and-type-conversions.md)  
 [Palavras-chave do C#](index.md)  
 [Tabela de tipos integrais](integral-types-table.md)  
 [Tabela de tipos internos](built-in-types-table.md)  
 [Tabela de conversões numéricas implícitas](implicit-numeric-conversions-table.md)  
 [Tabela de conversões numéricas explícitas](explicit-numeric-conversions-table.md)
