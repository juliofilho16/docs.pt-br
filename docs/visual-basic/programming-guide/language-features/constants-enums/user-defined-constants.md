---
title: Constantes definidas pelo usuário (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- constants [Visual Basic], circular references
- Const statement [Visual Basic], user-defined constants
- user-defined constants [Visual Basic]
- scope [Visual Basic], constants
- constants [Visual Basic], user-defined
- circular references between constants [Visual Basic]
ms.assetid: a1206d5c-c45e-4ac2-970a-4a0be6a05fdd
ms.openlocfilehash: b4a7e2b63b930b98ee082c0104c24f6857b5b35b
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="user-defined-constants-visual-basic"></a>Constantes definidas pelo usuário (Visual Basic)
Uma constante é um nome significativo que toma o lugar de um número ou uma cadeia de caracteres que não é alterado. Constantes armazenam valores que, como o nome implica, permanecem constantes durante a execução de um aplicativo. Você pode usar constantes definidas por controles ou componentes que você trabalha com, ou você pode criar seus próprios. Constantes que você mesmo cria são descritas como *definida pelo usuário*.  
  
 Declarar uma constante com o `Const` instrução, usando as mesmas diretrizes que você faria para criar um nome de variável. Se `Option Strict` é `On`, você deve declarar explicitamente o tipo de constante.  
  
## <a name="const-statement-usage"></a>Uso da instrução Const  
 Um `Const` instrução pode representar um matemática ou quantidade de data/hora:  
  
 [!code-vb[VbEnumsTask#10](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/user-defined-constants_1.vb)]  
  
 Ele também pode definir `String` constantes:  
  
 [!code-vb[VbEnumsTask#13](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/user-defined-constants_2.vb)]  
  
 A expressão à direita do sinal de igual ( `=` ) geralmente é um número ou cadeia de caracteres literal, mas também pode ser uma expressão que resulta em um número ou uma cadeia de caracteres (embora essa expressão não pode conter chamadas a funções). Você pode até mesmo definir constantes em termos de constantes definidas anteriormente:  
  
 [!code-vb[VbEnumsTask#15](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/user-defined-constants_3.vb)]  
  
## <a name="scope-of-user-defined-constants"></a>Escopo de constantes definidas pelo usuário  
 Um `Const` escopo da instrução é o mesmo que uma variável declarada no mesmo local. Você pode especificar o escopo em qualquer uma das seguintes maneiras:  
  
-   Para criar uma constante que existe somente dentro de um procedimento, declare-o dentro desse procedimento.  
  
-   Para criar uma constante disponível para todos os procedimentos dentro de uma classe, mas não para qualquer código fora desse módulo, declare-o na seção de declarações da classe.  
  
-   Para criar uma constante que está disponível para todos os membros de um assembly, mas não para clientes fora do assembly, declare-o usando o `Friend` palavra-chave na seção de declarações da classe.  
  
-   Para criar uma constante disponível em todo o aplicativo, declare-o usando o `Public` seção de palavra-chave nas declarações de classe.  
  
 Para obter mais informações, consulte [como: declarar uma constante](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-a-constant.md).  
  
### <a name="avoiding-circular-references"></a>Evitar referências circulares  
 Como constantes podem ser definidas em termos de outras constantes, é possível criar inadvertidamente um *ciclo*, ou uma referência circular, entre duas ou mais constantes. Um ciclo ocorre quando você tiver duas ou mais constantes públicas, cada uma delas é definida em termos de outros, como no exemplo a seguir:  
  
 [!code-vb[VbEnumsTask#16](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/user-defined-constants_4.vb)]  
[!code-vb[VbEnumsTask#17](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/user-defined-constants_5.vb)]  
  
 Se ocorrer um ciclo, Visual Basic gera um erro do compilador.  
  
## <a name="see-also"></a>Consulte também  
 [Instrução Const](../../../../visual-basic/language-reference/statements/const-statement.md)  
 [Tipos de Dados Constante e Literal](../../../../visual-basic/programming-guide/language-features/constants-enums/constant-and-literal-data-types.md)  
 [Constantes e Enumerações](../../../../visual-basic/programming-guide/language-features/constants-enums/index.md)  
 [Constantes e Enumerações](../../../../visual-basic/language-reference/constants-and-enumerations.md)  
 [Visão geral de Enumerações](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-overview.md)  
 [Visão Geral de Constantes](../../../../visual-basic/programming-guide/language-features/constants-enums/constants-overview.md)  
 [Como: declarar uma enumeração](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-enumerations.md)  
 [Enumerações e Qualificação de Nome](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)  
 [Instrução Option Strict](../../../../visual-basic/language-reference/statements/option-strict-statement.md)
