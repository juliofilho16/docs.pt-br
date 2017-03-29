---
title: "Árvores de expressão (C#) | Microsoft Docs"
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
ms.assetid: 7d0ac21a-6d90-4e2e-8903-528cb78615b7
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
ms.openlocfilehash: e7ffa63a7002b63de871f0458d2f02d543a17f5c
ms.lasthandoff: 03/13/2017

---
# <a name="expression-trees-c"></a>Árvores de expressão (C#)
Árvores de expressão representam código em uma estrutura de dados de árvore, onde cada nó é, por exemplo, uma expressão, uma chamada de método ou uma operação binária como `x < y`.  
  
 Você pode compilar e executar código representado por árvores de expressão. Isso permite a modificação dinâmica de código executável, a execução de consultas LINQ em vários bancos de dados e a criação de consultas dinâmicas. Para obter mais informações sobre árvores de expressão no LINQ, consulte [Como usar árvores de expressão para compilar consultas dinâmicas (C#)](../../../../csharp/programming-guide/concepts/expression-trees/how-to-use-expression-trees-to-build-dynamic-queries.md).  
  
 Árvores de expressão também são usadas no tempo de execução de linguagem dinâmica (DLR) para fornecer interoperabilidade entre linguagens dinâmicas e o .NET Framework e permitir que gravadores compiladores emitam árvores de expressão em vez de Microsoft intermediate language (MSIL). Para obter mais informações sobre o DLR, consulte [Visão geral do Dynamic Language Runtime](https://msdn.microsoft.com/library/dd233052).  
  
 Você pode fazer o compilador do C# ou do Visual Basic criar uma árvore de expressões para você com base em uma expressão lambda anônima ou criar árvores de expressão manualmente usando o namespace <xref:System.Linq.Expressions>.  
  
## <a name="creating-expression-trees-from-lambda-expressions"></a>Criando árvores de expressão de expressões Lambda  
 Quando uma expressão lambda é atribuída a uma variável do tipo <xref:System.Linq.Expressions.Expression%601>, o compilador emite código para criar uma árvore de expressão que representa a expressão lambda.  
  
 Os compiladores do C# podem gerar árvores de expressão apenas por meio de expressões lambda (ou lambdas de linha única). Ele não é possível analisar instruções lambdas (ou lambdas de várias linhas). Para obter mais informações sobre expressões lambda no C#, consulte [Expressões lambda](../../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md).  
  
 Os exemplos de código a seguir demonstram como fazer os compiladores do C# criarem uma árvore de expressão que representa a expressão lambda `num => num < 5`.  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
## <a name="creating-expression-trees-by-using-the-api"></a>Criando árvores de expressão usando a API  
 Para criar árvores de expressão usando a API, use a classe <xref:System.Linq.Expressions.Expression>. Essa classe contém métodos de fábrica estáticos que criam nós de árvore de expressão de tipos específicos, por exemplo, <xref:System.Linq.Expressions.ParameterExpression>, que representa uma variável ou parâmetro, ou <xref:System.Linq.Expressions.MethodCallExpression>, que representa uma chamada de método. <xref:System.Linq.Expressions.ParameterExpression>, <xref:System.Linq.Expressions.MethodCallExpression>, e outros tipos específicos de expressão também são definidos no namespace <xref:System.Linq.Expressions>. Esses tipos derivam do tipo abstrato <xref:System.Linq.Expressions.Expression>.  
  
 O exemplo de código a seguir demonstra como criar uma árvore de expressão que representa a expressão lambda `num => num < 5` usando a API.  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
 No .NET Framework 4 ou posterior, a API de árvores de expressão também dá suporte a atribuições e expressões de fluxo de controle, como loops, blocos condicionais e blocos `try-catch`. Usando a API, você pode criar árvores de expressão mais complexas do que aquelas que podem ser criadas por meio de expressões lambda pelos compiladores do C#. O exemplo a seguir demonstra como criar uma árvore de expressão que calcula o fatorial de um número.  
  
<CodeContentPlaceHolder>2</CodeContentPlaceHolder>  
 Para obter mais informações, consulte [Gerar métodos dinâmicos com árvores de expressão no Visual Studio 2010 (ou posterior)](http://go.microsoft.com/fwlink/?LinkId=169513).  
  
## <a name="parsing-expression-trees"></a>Analisando árvores de expressão  
 O exemplo de código a seguir demonstra como a árvore de expressão que representa a expressão lambda `num => num < 5` pode ser decomposta em suas partes.  
  
<CodeContentPlaceHolder>3</CodeContentPlaceHolder>  
## <a name="immutability-of-expression-trees"></a>Imutabilidade das árvores de expressão  
 Árvores de expressão devem ser imutáveis. Isso significa que se você deseja modificar uma árvore de expressão, deverá criar uma nova árvore de expressão, copiando a existente e substituindo seus nós. Você pode usar um visitantes de árvore expressão para percorrer a árvore de expressão existente. Para obter mais informações, consulte [Como modificar árvores de expressão (C#)](../../../../csharp/programming-guide/concepts/expression-trees/how-to-modify-expression-trees.md).  
  
## <a name="compiling-expression-trees"></a>Compilando árvores de expressão  
 O tipo <xref:System.Linq.Expressions.Expression%601> fornece o método <xref:System.Linq.Expressions.Expression%601.Compile%2A> que compila o código representado por uma árvore de expressão em um representante executável.  
  
 O exemplo de código a seguir demonstra como compilar uma árvore de expressão e executar o código resultante.  
  
```cs  
// Creating an expression tree.  
Expression<Func<int, bool>> expr = num => num < 5;  
  
// Compiling the expression tree into a delegate.  
Func<int, bool> result = expr.Compile();  
  
// Invoking the delegate and writing the result to the console.  
Console.WriteLine(result(4));  
  
// Prints True.  
  
// You can also use simplified syntax  
// to compile and run an expression tree.  
// The following line can replace two previous statements.  
Console.WriteLine(expr.Compile()(4));  
  
// Also prints True.  
```  
  
 Para obter mais informações, consulte [Como executar árvores de expressão (C#)](../../../../csharp/programming-guide/concepts/expression-trees/how-to-execute-expression-trees.md).  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.Linq.Expressions>   
 [Como executar árvores de expressão (C#)](../../../../csharp/programming-guide/concepts/expression-trees/how-to-execute-expression-trees.md)   
 [Como modificar árvores de expressão (C#)](../../../../csharp/programming-guide/concepts/expression-trees/how-to-modify-expression-trees.md)   
 [Expressões lambda](../../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)   
 [Visão geral do Dynamic Language Runtime](https://msdn.microsoft.com/library/dd233052)   
 [Conceitos de programação (C#)](../../../../csharp/programming-guide/concepts/index.md)