---
title: Como acessar um elemento de matriz com um ponteiro (Guia de Programação em C#)
ms.date: 07/20/2015
helpviewer_keywords:
- pointers [C#], array access
ms.assetid: 6c46f2af-a730-4855-8638-f136d9abaa12
ms.openlocfilehash: 92eb7a79c0e7522d1474537aeefbfdb083a11dc2
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-access-an-array-element-with-a-pointer-c-programming-guide"></a>Como acessar um elemento de matriz com um ponteiro (Guia de Programação em C#)
Em um contexto não seguro, é possível acessar um elemento na memória por meio do acesso de elemento de ponteiro, conforme mostrado no exemplo a seguir:  
  
```  
 char* charPointer = stackalloc char[123];  
for (int i = 65; i < 123; i++)  
{  
    charPointer[i] = (char)i; //access array elements  
}  
```  
  
 A expressão entre colchetes deve ser implicitamente conversível para `int`, `uint`, `long` ou `ulong`. A operação p[e] é equivalente a *(p+e). Assim como no C e no C++, o acesso de elemento de ponteiro não verifica erros fora dos limites.  
  
## <a name="example"></a>Exemplo  
 Neste exemplo, os locais de memória 123 são alocados para uma matriz de caracteres, `charPointer`. A matriz é usada para exibir as letras minúsculas e maiúsculas em dois loops [for](../../../csharp/language-reference/keywords/for.md).  
  
 Observe que a expressão `charPointer[i]` é equivalente à expressão `*(charPointer + i)` e é possível obter o mesmo resultado usando qualquer uma das duas expressões.  
  
 [!code-csharp[csProgGuidePointers#11](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/CSharp/how-to-access-an-array-element-with-a-pointer_1.cs)]  
  
 [!code-csharp[csProgGuidePointers#12](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/CSharp/how-to-access-an-array-element-with-a-pointer_2.cs)]  
  
 **Letras maiúsculas:**  
**ABCDEFGHIJKLMNOPQRSTUVWXYZ**  
**Letras minúsculas:**  
**abcdefghijklmnopqrstuvwxyz**   
## <a name="see-also"></a>Consulte também  
 [Guia de Programação em C#](../../../csharp/programming-guide/index.md)  
 [Expressões de ponteiro](../../../csharp/programming-guide/unsafe-code-pointers/pointer-expressions.md)  
 [Tipos de ponteiro](../../../csharp/programming-guide/unsafe-code-pointers/pointer-types.md)  
 [Tipos](../../../csharp/language-reference/keywords/types.md)  
 [unsafe](../../../csharp/language-reference/keywords/unsafe.md)  
 [Instrução fixed](../../../csharp/language-reference/keywords/fixed-statement.md)  
 [stackalloc](../../../csharp/language-reference/keywords/stackalloc.md)
