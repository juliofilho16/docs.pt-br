---
title: Operadores e expressões no Visual Basic
ms.date: 07/20/2015
helpviewer_keywords:
- operators [Visual Basic], operands
- operators [Visual Basic]
- operands [Visual Basic], definition
- Visual Basic code, operators
- Visual Basic code, expressions
- operands
- expressions [Visual Basic]
ms.assetid: b86f3131-94ee-448f-96cd-79611e028b26
ms.openlocfilehash: 06397cf05fc4da977cfecb8e412f12766a2a342d
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="operators-and-expressions-in-visual-basic"></a>Operadores e expressões no Visual Basic
Um *operador* é um elemento de código que executa uma operação em um ou mais elementos de código que retêm valores. Os elementos de valor incluem variáveis, constantes, literais, propriedades, valores retornados dos procedimentos `Function` e `Operator`, bem como expressões.  
  
 Uma *expressão* é uma série de elementos de valor combinada com operadores, que gera um novo valor. Os operadores agem em elementos de valor executando cálculos, comparações ou outras operações.  
  
## <a name="types-of-operators"></a>Tipos de operadores  
 Visual Basic oferece os seguintes tipos de operadores:  
  
-   Os [operadores aritméticos](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md) executam cálculos familiares em valores numéricos, incluindo a mudança dos padrões de bit.  
  
-   Os [operadores de comparação](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md) comparam duas expressões e retornam um valor `Boolean` que representa o resultado da comparação.  
  
-   Os [operadores de concatenação](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/concatenation-operators.md) unem várias cadeias de caracteres em uma única cadeia de caracteres.  
  
-   Os [operadores lógicos e bit a bit no Visual Basic](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md) combinam valores numéricos ou `Boolean` e retornam um resultado do mesmo tipo de dados que os valores.  
  
 Os elementos de valor combinados com um operador são chamados *operandos* desse operador. Os operadores combinados com elementos de valor formam expressões, exceto para o operador de atribuição, que forma uma *instrução*. Para obter mais informações, consulte [Instruções](../../../../visual-basic/programming-guide/language-features/statements.md).  
  
## <a name="evaluation-of-expressions"></a>Avaliação de expressões  
 O resultado final de uma expressão representa um valor, que normalmente é um tipo de dados familiar, como `Boolean`, `String` ou um tipo numérico.  
  
 Veja a seguir dois exemplos de expressões.  
  
 `5 + 4`  
  
 `' The preceding expression evaluates to 9.`  
  
 `15 * System.Math.Sqrt(9) + x`  
  
 `' The preceding expression evaluates to 45 plus the value of x.`  
  
 `"Concat" & "ena" & "tion"`  
  
 `' The preceding expression evaluates to "Concatenation".`  
  
 `763 < 23`  
  
 `' The preceding expression evaluates to False.`  
  
 Vários operadores podem executar ações em uma única expressão ou instrução, como mostra o exemplo a seguir.  
  
 [!code-vb[VbVbalrOperators#56](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/index_1.vb)]  
  
 No exemplo anterior, o Visual Basic que executa as operações na expressão à direita do operador de atribuição (`=`), em seguida, atribui o valor resultante para a variável `x` à esquerda. Não há nenhum limite prático para o número de operadores que podem ser combinados em uma expressão, mas é necessário entender a [Precedência do operador no Visual Basic](../../../../visual-basic/language-reference/operators/operator-precedence.md) para assegurar que você obtenha os resultados esperados.  
  
 Para obter mais informações e exemplos, consulte [Sobrecarga de operador no Visual Basic 2005](http://go.microsoft.com/fwlink/?LinkId=101703).  
  
## <a name="see-also"></a>Consulte também  
 [Operadores](../../../../visual-basic/language-reference/operators/index.md)  
 [Combinação Eficiente de Operadores](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/efficient-combination-of-operators.md)  
 [Instruções](../../../../visual-basic/language-reference/statements/index.md)
