---
title: Testar uma biblioteca de classes com .NET Core no Visual Studio 2017
description: Saiba como testar uma biblioteca de classes escrita em C# usando o Visual Studio 2017
author: BillWagner
ms.author: wiwagn
ms.date: 08/07/2017
dev_langs:
- csharp
- vb
ms.openlocfilehash: 24d0f1366a8e4309bbfb5b548af7407de50eaf76
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="testing-a-class-library-with-net-core-in-visual-studio-2017"></a>Testar uma biblioteca de classes com .NET Core no Visual Studio 2017

Em [Building a class library with C# and .NET Core in Visual Studio 2017](library-with-visual-studio.md) (Compilar uma biblioteca de classes com C# e com .NET Core no Visual Studio 2017) ou em [Building a class library with Visual Basic and .NET Core in Visual Studio 2017](vb-library-with-visual-studio.md) (Compilar uma biblioteca de classes com o Visual Basic e com o .NET Core no Visual Studio 2017), você criou uma biblioteca de classes simples que adiciona um método de extensão à classe <xref:System.String>. Agora, você criará um teste de unidade para ter certeza de que ela funciona conforme o esperado. Você adicionará seu projeto de teste de unidade para a solução que criou no tópico anterior.

## <a name="creating-a-unit-test-project"></a>Criar um projeto de teste de unidade

Para criar o projeto de teste de unidade, faça o seguinte:

# <a name="ctabcsharp"></a>[C#](#tab/csharp)
1. No **Gerenciador de Soluções**, abra o menu de contexto do nó da solução **ClassLibraryProjects** e selecione **Adicionar** > **Novo Projeto**.

1. Na caixa de diálogo **Adicionar novo projeto**, selecione o nó **Visual C#**. Em seguida, selecione o nó **.NET Core** seguido pelo modelo de projeto **Projeto de Teste de Unidade (.NET Core)**. Na caixa de texto **Nome**, digite "StringLibraryTest" como o nome do projeto. Selecione **OK** para criar o projeto de teste de unidade.

   ![Caixa de diálogo Adicionar Novo Projeto](./media/testing-library-with-visual-studio/testproject.png)

   > [!NOTE]  
   > Além de um projeto de Teste de unidade, também é possível usar o Visual Studio para criar um projeto de teste do xUnit para o .NET Core.

1. O Visual Studio cria o projeto e abre o arquivo *UnitTest1.cs* na janela do código.

   ![Janela de código do Visual Studio mostrando o método TestMethod1 e a classe UnitTest1 do projeto de teste de unidade padrão](./media/testing-library-with-visual-studio/unittestwindow.png)

   O código-fonte criado pelo modelo de teste de unidade faz o seguinte:

   * Ele importa o namespace [Microsoft.VisualStudio.TestTools.UnitTesting](https://msdn.microsoft.com/library/microsoft.visualstudio.testtools.unittesting.aspx), que contém os tipos usados para testes de unidade.

   * Ele aplica o atributo [\[TestClass\]](https://msdn.microsoft.com/library/microsoft.visualstudio.testtools.unittesting.testclassattribute.aspx) à classe `UnitTest1`. Cada método de teste em uma classe de teste marcada com o atributo \[TestMethod\] é executado automaticamente quando o teste de unidade é executado.

   * Ele aplica o atributo [\[TestMethod\]](https://msdn.microsoft.com/library/microsoft.visualstudio.testtools.unittesting.testmethodattribute.aspx) para definir `TestMethod1` como um método de teste para execução automática quando o teste de unidade é executado.

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó **Dependências** do projeto **StringLibraryTest** e selecione **Adicionar Referência** no menu de contexto.

   ![Menu de contexto de Dependências de StringLibraryTest](./media/testing-library-with-visual-studio/addreference.png)

1. Na caixa de diálogo **Gerenciador de Referências**, expanda o nó **Projetos** e marque a caixa ao lado de **StringLibrary**. A adição de uma referência ao assembly `StringLibrary` permite que o compilador localize os métodos **StringLibrary**. Selecione o botão **OK**. Isso adiciona uma referência ao seu projeto de biblioteca de classes, `StringLibrary`.

   ![Gerenciador de referências](./media/testing-library-with-visual-studio/referencemanager.png)
# <a name="visual-basictabvisual-basic"></a>[Visual Basic](#tab/visual-basic) 
1. No **Gerenciador de Soluções**, abra o menu de contexto do nó da solução **ClassLibraryProjects** e selecione **Adicionar** > **Novo Projeto**.

1. Na caixa de diálogo **Adicionar novo projeto**, selecione o nó **Visual Basic**. Em seguida, selecione o nó **.NET Core** seguido pelo modelo de projeto **Projeto de Teste de Unidade (.NET Core)**. Na caixa de texto **Nome**, digite "StringLibraryTest" como o nome do projeto. Selecione **OK** para criar o projeto de teste de unidade.

   ![Caixa de diálogo Adicionar Novo Projeto](./media/testing-library-with-visual-studio/vb-testproject.png)

   > [!NOTE]  
   > Além de um projeto de Teste de unidade, também é possível usar o Visual Studio para criar um projeto de teste do xUnit para o .NET Core.

1. O Visual Studio cria o projeto e abre o arquivo *UnitTest1.vb* na janela do código.

   ![Janela de código do Visual Studio mostrando o método TestMethod1 e a classe UnitTest1 do projeto de teste de unidade padrão](./media/testing-library-with-visual-studio/vb-unittestwindow.png)

   O código-fonte criado pelo modelo de teste de unidade faz o seguinte:

   * Ele importa o namespace [Microsoft.VisualStudio.TestTools.UnitTesting](https://msdn.microsoft.com/library/microsoft.visualstudio.testtools.unittesting.aspx), que contém os tipos usados para testes de unidade.

   * Ele aplica o atributo [\[TestClass\]](https://msdn.microsoft.com/library/microsoft.visualstudio.testtools.unittesting.testclassattribute.aspx) à classe `UnitTest1`. Cada método de teste em uma classe de teste marcada com o atributo \[TestMethod\] é executado automaticamente quando o teste de unidade é executado.

   * Ele aplica o atributo [\[TestMethod\]](https://msdn.microsoft.com/library/microsoft.visualstudio.testtools.unittesting.testmethodattribute.aspx) para definir `TestMethod1` como um método de teste para execução automática quando o teste de unidade é executado.

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó **Dependências** do projeto **StringLibraryTest** e selecione **Adicionar Referência** no menu de contexto.

   ![Menu de contexto de Dependências de StringLibraryTest](./media/testing-library-with-visual-studio/addreference.png)

1. Na caixa de diálogo **Gerenciador de Referências**, expanda o nó **Projetos** e marque a caixa ao lado de **StringLibrary**. A adição de uma referência ao assembly `StringLibrary` permite que o compilador localize os métodos **StringLibrary**. Selecione o botão **OK**. Isso adiciona uma referência ao seu projeto de biblioteca de classes, `StringLibrary`.

   ![Gerenciador de referências](./media/testing-library-with-visual-studio/referencemanager.png)
---

## <a name="adding-and-running-unit-test-methods"></a>Adicionar e executar métodos de teste de unidade

Quando o Visual Studio executa um teste de unidade, ele executa cada método marcado com o atributo [\[TestMethod\]](https://msdn.microsoft.com/library/microsoft.visualstudio.testtools.unittesting.testmethodattribute.aspx) em uma classe de teste de unidade, a classe à qual o atributo [\[TestClass\]](https://msdn.microsoft.com/library/microsoft.visualstudio.testtools.unittesting.testclassattribute.aspx) é aplicado. Um método de teste termina quando a primeira falha é encontrada ou quando todos os testes contidos no método têm êxito.

Os testes mais comuns chamam membros da classe [Assert](https://msdn.microsoft.com/library/microsoft.visualstudio.testtools.unittesting.assert.aspx). Muitos métodos assert incluem pelo menos dois parâmetros, um deles é o resultado esperado do teste, e o outro é o resultado real do teste. Alguns de seus métodos chamados com mais frequência são mostrados na tabela abaixo.

Métodos assert | Função
--- | ---
`Assert.AreEqual` | Verifica se os dois valores ou objetos são iguais. A assert falha se os valores ou objetos não forem iguais.
`Assert.AreSame` | Verifica se duas variáveis de objeto se referem ao mesmo objeto. A assert falhará se as variáveis se referirem a objetos diferentes.
`Assert.IsFalse` | Verifica se uma condição é `false`. O assert falhará se a condição for `true`.
`Assert.IsNotNull` | Verifica se um objeto não é `null`. A assert falhará se o objeto for `null`.

Também é possível aplicar o atributo [\[ExpectedException\]](https://msdn.microsoft.com/library/microsoft.visualstudio.testtools.unittesting.expectedexceptionattribute.aspx) a um método de teste. Ele indica o tipo de exceção que um método de teste deve gerar. O teste falhará se a exceção especificada não for lançada.

Ao testar o método `StringLibrary.StartsWithUpper`, você quer fornecer um número de cadeias de caracteres que comecem com um caractere maiúsculo. Você espera que o método retorne `true` nesses casos, então pode chamar o método [Assert.IsTrue(Boolean, String)](https://msdn.microsoft.com/library/ms243754.aspx). Da mesma forma, você deseja fornecer um número de cadeias de caracteres que comecem com algo diferente de um caractere maiúsculo. Você espera que o método retorne `false` nesses casos, então pode chamar o método [Assert.IsFalse(Boolean, String)](https://msdn.microsoft.com/library/ms243805.aspx).

Como seu método de biblioteca lida com cadeias de caracteres, convém ter certeza de que ele manipulará com êxito uma [cadeia de caracteres vazia (`String.Empty`)](xref:System.String.Empty), uma cadeia de caracteres válida sem caracteres e cujo <xref:System.String.Length> é 0 e uma cadeia de caracteres `null` que não foi inicializada. Se `StartsWithUpper` for chamado como um método de extensão em uma instância de <xref:System.String>, ele não poderá receber uma cadeia de caracteres `null`. No entanto, você também pode chamá-lo diretamente como um método estático e passa um único argumento <xref:System.String>.

Você definirá três métodos, cada um deles chamará seu método [Assert](https://msdn.microsoft.com/library/microsoft.visualstudio.testtools.unittesting.assert.aspx) repetidamente para cada elemento em uma matriz de cadeia de caracteres. Como o método de teste falha assim que encontra a primeira falha, você chamará uma sobrecarga de método que permite passar uma cadeia de caracteres que indica o valor da cadeia de caracteres usado na chamada do método.

Para criar os métodos de teste:

# <a name="ctabcsharp"></a>[C#](#tab/csharp) 
1. Na janela de código *UnitTest1.cs*, substitua o código pelo seguinte código:

   [!CODE-csharp[Test#1](../../../samples/snippets/csharp/getting_started/with_visual_studio_2017/testlib1.cs)]

   Observe que seu teste de caracteres maiúsculos no método `TestStartsWithUpper` inclui a letra maiúscula grega alfa (U+0391) e a letra maiúscula cirílica EM (U+041C) e o teste de caracteres minúsculos no método `TestDoesNotStartWithUpper` inclui a letra minúscula grega alfa (U+03B1) e a letra minúscula cirílica Ghe (U+0433).

1. Na barra de menus, selecione **Arquivo** > **Salvar UnitTest1.cs Como**. Na caixa de diálogo **Salvar Arquivo Como**, selecione a seta ao lado do botão **Salvar** e selecione **Salvar com Codificação**.

   ![Caixa de diálogo Salvar Arquivo Como](./media/testing-library-with-visual-studio/savefileas.png)
# <a name="visual-basictabvisual-basic"></a>[Visual Basic](#tab/visual-basic) 
1. Na janela de código *UnitTest1.vb*, substitua o código pelo seguinte código:

    [!CODE-vb[Test#1](../../../samples/snippets/core/tutorials/vb-library-with-visual-studio/testlib.vb)]

   Observe que seu teste de caracteres maiúsculos no método `TestStartsWithUpper` inclui a letra maiúscula grega alfa (U+0391) e a letra maiúscula cirílica EM (U+041C) e o teste de caracteres minúsculos no método `TestDoesNotStartWithUpper` inclui a letra minúscula grega alfa (U+03B1) e a letra minúscula cirílica Ghe (U+0433).

1. Na barra de menus, selecione **Arquivo** > **Salvar UnitTest1.vb Como**. Na caixa de diálogo **Salvar Arquivo Como**, selecione a seta ao lado do botão **Salvar** e selecione **Salvar com Codificação**.

   ![Caixa de diálogo Salvar Arquivo Como](./media/testing-library-with-visual-studio/savefileas.png)
---

1. Na caixa de diálogo **Confirmar Salvar Como**, selecione o botão **Sim** para salvar o arquivo.

1. Na caixa de diálogo **Opções Avançadas de Salvamento**, selecione **Unicode (UTF-8 com assinatura) – página de código 65001** na lista suspensa **Codificação** e selecione **OK**.

   ![Caixa de diálogo Opções Avançadas de Salvamento](./media/testing-library-with-visual-studio/advancedsaveoptions.png)

   Se você não salvar seu código-fonte como um arquivo codificado em UTF8, o Visual Studio poderá salvá-lo como um arquivo ASCII. Quando isso acontecer, o tempo de execução não decodificará de forma precisa os caracteres UTF8 fora do intervalo ASCII e os resultados de teste não serão precisos.

1. Na barra de menus, selecione **Testar** > **Executar** > **Todos os Testes**. A janela **Gerenciador de Testes** é aberta e mostra que os testes foram executados com êxito. Os três testes estão listados na seção **Testes Aprovados**, e a seção **Resumo** relata o resultado da execução de teste.

   ![Janela Gerenciador de Testes](./media/testing-library-with-visual-studio/firsttest.png)

## <a name="handling-test-failures"></a>Tratamento de falhas do teste

Sua execução de teste não apresentou falhas, mas altere-a um pouco para que um dos métodos do teste falhe:

1. Modifique a matriz `words` no método `TestDoesNotStartWithUpper` para incluir a cadeia de caracteres “Error”. Não é necessário salvar o arquivo porque o Visual Studio salva automaticamente os arquivos abertos quando uma solução é criada para executar testes.

   ```csharp
   string[] words = { "alphabet", "Error", "zebra", "abc", "αυτοκινητοβιομηχανία", "государство",
                      "1234", ".", ";", " " };
   ```
   ```vb
   Dim words() As String = { "alphabet", "Error", "zebra", "abc", "αυτοκινητοβιομηχανία", "государство",
                      "1234", ".", ";", " " }

   ```
1. Execute o teste selecionando **Testar** > **Executar** > **Todos os Testes** na barra de menus. A Janela **Gerenciador de Testes** indica que dois testes tiveram êxito e um falhou.

   ![Janela Gerenciador de Testes](./media/testing-library-with-visual-studio/failedtest.png)

1. Na seção **Testes com Falha**, selecione o teste com falha, `TestDoesNotStartWith`. A janela **Gerenciador de Testes** mostra a mensagem produzida pelo assert: "Assert.IsFalse falhou. Esperado para 'Error': false, real: True". Devido à falha, todas as cadeias de caracteres na matriz após "Error" não foram testadas.

   ![Janela Gerenciador de Testes mostrando a falha de asserção Is False](./media/testing-library-with-visual-studio/failedtestdetail.png)

1. Remova o código que foi adicionado (`"Error", `) e execute o teste novamente. Os testes serão aprovados.

## <a name="testing-the-release-version-of-the-library"></a>Testar a versão de lançamento da biblioteca

Você estava executando nossos testes na versão de Depuração da biblioteca. Agora que todos os testes foram aprovados, e nós testamos adequadamente nossa biblioteca, você deve executar os testes mais uma vez no build de Lançamento da biblioteca. Vários fatores, incluindo as otimizações do compilador, podem produzir um comportamento diferente entre as compilações de Depuração e Lançamento.

Para testar a compilação de Lançamento:

1. Na barra de ferramentas do Visual Studio, altere a configuração de compilação de **Depurar** para **Lançamento**.

   ![Barra de ferramentas do Visual Studio](./media/testing-library-with-visual-studio/toolbar.png)

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto **StringLibrary** e selecione **Compilar** no menu de contexto para recompilar a biblioteca.

   ![Menu de contexto StringLibrary](./media/testing-library-with-visual-studio/buildlibrary.png)

1. Execute os testes de unidade escolhendo **Testar** > **Executar** > **Todos os Testes** na barra de menus. Os testes são aprovados.

Agora que você concluiu o teste de sua biblioteca, a próxima etapa é disponibilizá-la aos chamadores. Você pode agrupá-la com um ou mais aplicativos, ou pode distribuí-la como um pacote do NuGet. Para obter mais informações, consulte [Consumindo uma biblioteca de classes .NET Standard](./consuming-library-with-visual-studio.md).
