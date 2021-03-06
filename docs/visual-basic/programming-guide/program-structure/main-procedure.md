---
title: Procedimento principal no Visual Basic
ms.date: 07/20/2015
f1_keywords:
- vb.Main
helpviewer_keywords:
- Main procedure
- Main method [Visual Basic]
- main function
ms.assetid: f0db283e-f283-4464-b521-b90858cc1b44
ms.openlocfilehash: 109bf94eb91292cfca700a9e456c8ab53e83d68f
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="main-procedure-in-visual-basic"></a>Procedimento principal no Visual Basic
Cada aplicativo do Visual Basic deve conter um procedimento chamado `Main`. Esse procedimento serve como a partir do ponto e controle geral para seu aplicativo. O .NET Framework chama o `Main` procedimento quando ele carregar seu aplicativo e está pronto para passá-lo para controle. A menos que você estiver criando um aplicativo Windows Forms, você deve escrever o `Main` procedimento para aplicativos que são executados em seus próprios.  
  
 `Main` contém o código que é executado primeiro. Em `Main`, determinar qual formulário é carregado pela primeira vez, quando o programa for iniciado, descubra se uma cópia do seu aplicativo já está em execução no sistema, estabelecer um conjunto de variáveis para o seu aplicativo ou abrir um banco de dados que o aplicativo requer.  
  
## <a name="requirements-for-the-main-procedure"></a>Requisitos para o procedimento principal  
 Um arquivo que é executado em seu próprio (normalmente com extensão .exe) deve conter um `Main` procedimento. Uma biblioteca (por exemplo, com extensão. dll) não é executado em seu próprio e não requer uma `Main` procedimento. Os requisitos para os diferentes tipos de projetos que você pode criar são da seguinte maneira:  
  
-   Aplicativos de console executam em seus próprios, e você deve fornecer pelo menos um `Main` procedimento. .  
  
-   Executar seus próprios aplicativos do Windows Forms. No entanto, o compilador do Visual Basic gera automaticamente um `Main` procedimento como um aplicativo e você não precisa gravar um.  
  
-   Bibliotecas de classes não exigem uma `Main` procedimento. Esses incluem bibliotecas de controle do Windows e bibliotecas de controles da Web. Aplicativos Web são implantados como bibliotecas de classe.  
  
## <a name="declaring-the-main-procedure"></a>Declarando o procedimento principal  
 Há quatro maneiras para declarar o `Main` procedimento. Pode levar argumentos ou não, e pode retornar um valor ou não.  
  
> [!NOTE]
>  Se você declarar `Main` em uma classe, você deve usar o `Shared` palavra-chave. Em um módulo, `Main` não precisa ser `Shared`.  
  
-   É a maneira mais simples para declarar um `Sub` procedimento que não usam argumentos ou retornar um valor.  
  
    ```  
    Module mainModule  
        Sub Main()  
            MsgBox("The Main procedure is starting the application.")  
            ' Insert call to appropriate starting place in your code.  
            MsgBox("The application is terminating.")  
        End Sub  
    End Module  
    ```  
  
-   `Main` também pode retornar um `Integer` valor, que o sistema operacional usa como o código de saída para o seu programa. Outros programas podem testar esse código, examinando o valor de ERRORLEVEL do Windows. Para retornar um código de saída, você deve declarar `Main` como um `Function` procedimento em vez de uma `Sub` procedimento.  
  
    ```  
    Module mainModule  
        Function Main() As Integer  
            MsgBox("The Main procedure is starting the application.")  
            Dim returnValue As Integer = 0  
            ' Insert call to appropriate starting place in your code.  
            ' On return, assign appropriate value to returnValue.  
            ' 0 usually means successful completion.  
            MsgBox("The application is terminating with error level " &  
                 CStr(returnValue) & ".")  
            Return returnValue  
        End Function  
    End Module  
    ```  
  
-   `Main` também pode usar um `String` matriz como um argumento. Cada cadeia de caracteres na matriz contém um dos argumentos de linha de comando usados para invocar o programa. Você pode executar ações diferentes dependendo de seus valores.  
  
    ```  
    Module mainModule  
        Function Main(ByVal cmdArgs() As String) As Integer  
            MsgBox("The Main procedure is starting the application.")  
            Dim returnValue As Integer = 0  
            ' See if there are any arguments.  
            If cmdArgs.Length > 0 Then  
                For argNum As Integer = 0 To UBound(cmdArgs, 1)  
                    ' Insert code to examine cmdArgs(argNum) and take  
                    ' appropriate action based on its value.  
                Next argNum  
            End If  
            ' Insert call to appropriate starting place in your code.  
            ' On return, assign appropriate value to returnValue.  
            ' 0 usually means successful completion.  
            MsgBox("The application is terminating with error level " &  
                 CStr(returnValue) & ".")  
            Return returnValue  
        End Function  
    End Module  
    ```  
  
-   Você pode declarar `Main` para examinar os argumentos de linha de comando, mas não retornar um código de saída, da seguinte maneira.  
  
    ```  
    Module mainModule  
        Sub Main(ByVal cmdArgs() As String)  
            MsgBox("The Main procedure is starting the application.")  
            Dim returnValue As Integer = 0  
            ' See if there are any arguments.  
            If cmdArgs.Length > 0 Then  
                For argNum As Integer = 0 To UBound(cmdArgs, 1)  
                    ' Insert code to examine cmdArgs(argNum) and take  
                    ' appropriate action based on its value.  
                Next argNum  
            End If  
            ' Insert call to appropriate starting place in your code.  
            MsgBox("The application is terminating.")  
        End Sub  
    End Module  
    ```  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualBasic.Interaction.MsgBox%2A>  
 <xref:System.Array.Length%2A>  
 <xref:Microsoft.VisualBasic.Information.UBound%2A>  
 [Estrutura de um programa do Visual Basic](../../../visual-basic/programming-guide/program-structure/structure-of-a-visual-basic-program.md)  
 [/main](../../../visual-basic/reference/command-line-compiler/main.md)  
 [Compartilhado](../../../visual-basic/language-reference/modifiers/shared.md)  
 [Instrução Sub](../../../visual-basic/language-reference/statements/sub-statement.md)  
 [Instrução Function](../../../visual-basic/language-reference/statements/function-statement.md)  
 [Tipo de Dados Integer](../../../visual-basic/language-reference/data-types/integer-data-type.md)  
 [Tipo de Dados String](../../../visual-basic/language-reference/data-types/string-data-type.md)
