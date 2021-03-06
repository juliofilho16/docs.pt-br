---
title: 'Instruções passo a passo: habilitando arrastar e soltar em um controle de usuário'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- walkthrough [WPF], drag-and-drop
- drag-and-drop [WPF], walkthrough
ms.assetid: cc844419-1a77-4906-95d9-060d79107fc7
ms.openlocfilehash: e4dba856b973f1210f2d088de3ed8ae5df2c6988
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="walkthrough-enabling-drag-and-drop-on-a-user-control"></a>Instruções passo a passo: habilitando arrastar e soltar em um controle de usuário
Este passo a passo demonstra como criar um controle de usuário personalizado que pode participar na transferência de dados por arrastar e soltar no [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)].  
  
 Neste passo a passo, você criará um personalizado WPF <xref:System.Windows.Controls.UserControl> que representa uma forma de círculo. Você implementará a funcionalidade no controle para permitir a transferência de dados por meio de arrastar e soltar. Por exemplo, se você arrastar de um controle do círculo para outro, os dados de cor de preenchimento serão copiados do círculo de origem para o destino. Se você arrastar um controle do círculo para um <xref:System.Windows.Controls.TextBox>, a representação de cadeia de caracteres da cor de preenchimento é copiada para o <xref:System.Windows.Controls.TextBox>. Você também criará um pequeno aplicativo que contém dois controles de painel e um <xref:System.Windows.Controls.TextBox> para testar a funcionalidade de arrastar e soltar. Será gravado um código que permite que os painéis processem os dados do círculo que foram soltos, o que permitirá mover ou copiar círculos da coleção de filhos de um painel para o outro.  
  
 Esta explicação passo a passo ilustra as seguintes tarefas:  
  
-   Crie um controle de usuário personalizado.  
  
-   Habilite o controle de usuário como uma fonte de arrastar.  
  
-   Habilite o controle de usuário como um destino de soltar.  
  
-   Habilite um painel para receber dados que foram soltos pelo controle de usuário.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
-   Visual Studio 2010  
  
## <a name="creating-the-application-project"></a>Criando o projeto de aplicativo  
 Nesta seção, você criará a infraestrutura de aplicativo, que inclui uma página principal com dois painéis e um <xref:System.Windows.Controls.TextBox>.  
  
### <a name="to-create-the-project"></a>Para criar o projeto  
  
1.  Crie um novo projeto de aplicativo do WPF no Visual Basic ou no Visual C#, chamado `DragDropExample`. Para obter mais informações, consulte [Como criar um novo projeto de aplicativo do WPF](http://msdn.microsoft.com/library/1f6aea7a-33e1-4d3f-8555-1daa42e95d82).  
  
2.  Abra MainWindow.xaml.  
  
3.  Adicione a seguinte marcação entre a abertura e fechamento <xref:System.Windows.Controls.Grid> marcas.  
  
     Essa marcação cria a interface do usuário para o aplicativo de teste.  
  
     [!code-xaml[DragDropWalkthrough#PanelsStep1XAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/SnippetWindow.xaml#panelsstep1xaml)]  
  
## <a name="adding-a-new-user-control-to-the-project"></a>Adicionando um novo controle de usuário ao projeto  
 Nesta seção, você adicionará um novo controle de usuário ao projeto.  
  
### <a name="to-add-a-new-user-control"></a>Para adicionar um novo controle de usuário  
  
1.  No menu Projeto, selecione **Adicionar controle de usuário**.  
  
2.  Na caixa de diálogo Adicionar novo item, altere o nome para `Circle.xaml` e clique em **Adicionar**.  
  
     O Circle.xaml e seu code-behind são adicionados ao projeto.  
  
3.  Abra o Circle.xaml.  
  
     Esse arquivo conterá os elementos de interface do usuário do controle de usuário.  
  
4.  Adicione a seguinte marcação para a raiz <xref:System.Windows.Controls.Grid> para criar um controle de usuário simples que tem um círculo azul como sua interface do usuário.  
  
     [!code-xaml[DragDropWalkthrough#EllipseXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml#ellipsexaml)]  
  
5.  Abra Circle.xaml.cs ou Circle.xaml.vb.  
  
6.  No C#, adicione o código a seguir após o construtor padrão para criar um construtor de cópia. No Visual Basic, adicione o código a seguir para criar um construtor padrão e um construtor de cópia.  
  
     Para permitir que o controle de usuário seja copiado, você pode adicionar um método de construtor de cópia no arquivo code-behind. No controle de usuário simplificado do círculo, será copiado apenas o preenchimento e o tamanho do controle de usuário.  
  
     [!code-csharp[DragDropWalkthrough#CopyCtor](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#copyctor)]
     [!code-vb[DragDropWalkthrough#CopyCtor](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#copyctor)]  
  
### <a name="to-add-the-user-control-to-the-main-window"></a>Para adicionar o controle de usuário à janela principal  
  
1.  Abra MainWindow.xaml.  
  
2.  Adicionar o XAML a seguir para a abertura <xref:System.Windows.Window> marca para criar uma referência de namespace XML para o aplicativo atual.  
  
    ```  
    xmlns:local="clr-namespace:DragDropExample"  
    ```  
  
3.  Na primeira <xref:System.Windows.Controls.StackPanel>, adicionar o XAML a seguir para criar duas instâncias do controle de usuário círculo no primeiro painel.  
  
     [!code-xaml[DragDropWalkthrough#CirclesXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/SnippetWindow.xaml#circlesxaml)]  
  
     O XAML completo para o painel tem a aparência a seguir.  
  
     [!code-xaml[DragDropWalkthrough#PanelsStep2XAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/SnippetWindow.xaml#panelsstep2xaml)]  
  
## <a name="implementing-drag-source-events-in-the-user-control"></a>Implementando eventos de origem do arrasto no controle de usuário  
 Nesta seção, você substituirá o <xref:System.Windows.UIElement.OnMouseMove%2A> método e iniciar a operação de arrastar e soltar.  
  
 Se um arraste for iniciado (um botão do mouse é pressionado e o mouse é movido), você incluirá os dados a serem transferidos para um <xref:System.Windows.DataObject>. Nesse caso, o controle do círculo empacotará três itens de dados; uma representação de cadeia de caracteres da cor de preenchimento, uma representação dupla da altura e uma cópia de si mesmo.  
  
### <a name="to-initiate-a-drag-and-drop-operation"></a>Para iniciar uma operação do tipo “arrastar e soltar”  
  
1.  Abra Circle.xaml.cs ou Circle.xaml.vb.  
  
2.  Adicione o seguinte <xref:System.Windows.UIElement.OnMouseMove%2A> substituição para fornecer manipulação de classe para o <xref:System.Windows.UIElement.MouseMove> evento.  
  
     [!code-csharp[DragDropWalkthrough#OnMouseMove](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#onmousemove)]
     [!code-vb[DragDropWalkthrough#OnMouseMove](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#onmousemove)]  
  
     Isso <xref:System.Windows.UIElement.OnMouseMove%2A> substituição executa as seguintes tarefas:  
  
    -   Verifica se o botão esquerdo do mouse é pressionado enquanto o mouse se move.  
  
    -   Empacota os dados de círculo em uma <xref:System.Windows.DataObject>. Nesse caso, o controle do círculo empacota três itens de dados; uma representação de cadeia de caracteres da cor de preenchimento, uma representação dupla da altura e uma cópia de si mesmo.  
  
    -   Chama estático <xref:System.Windows.DragDrop.DoDragDrop%2A?displayProperty=nameWithType> método para iniciar a operação de arrastar e soltar. Passe os seguintes três parâmetros para o <xref:System.Windows.DragDrop.DoDragDrop%2A> método:  
  
        -   `dragSource` – Uma referência para esse controle.  
  
        -   `data` – A <xref:System.Windows.DataObject> criado no código anterior.  
  
        -   `allowedEffects` – As operações de arrastar e soltar permitidas, que são <xref:System.Windows.DragDropEffects.Copy> ou <xref:System.Windows.DragDropEffects.Move>.  
  
3.  Pressione F5 para compilar e executar o aplicativo.  
  
4.  Clique em um dos controles do círculo e arraste-o sobre painéis, o círculo e o <xref:System.Windows.Controls.TextBox>. Ao arrastar sobre o <xref:System.Windows.Controls.TextBox>, o cursor muda para indicar uma movimentação.  
  
5.  Ao arrastar um círculo sobre o <xref:System.Windows.Controls.TextBox>, pressione a tecla CTRL. Observe como o cursor muda para indicar uma cópia.  
  
6.  Arraste e solte um círculo para o <xref:System.Windows.Controls.TextBox>. A representação de cadeia de caracteres da cor de preenchimento do círculo é acrescentada ao <xref:System.Windows.Controls.TextBox>.  
  
     ![Representação de cadeia de caracteres da cor de preenchimento do círculo](../../../../docs/framework/wpf/advanced/media/dragdrop-colorstring.png "DragDrop_ColorString")  
  
 Por padrão, o cursor será alterado durante uma operação do tipo “arrastar e soltar” para indicar qual será o efeito de soltar os dados. Você pode personalizar os comentários especificados para o usuário manipulando o <xref:System.Windows.UIElement.GiveFeedback> evento e definindo um cursor diferente.  
  
### <a name="to-give-feedback-to-the-user"></a>Para fornecer comentários ao usuário  
  
1.  Abra Circle.xaml.cs ou Circle.xaml.vb.  
  
2.  Adicione o seguinte <xref:System.Windows.UIElement.OnGiveFeedback%2A> substituição para fornecer manipulação de classe para o <xref:System.Windows.UIElement.GiveFeedback> evento.  
  
     [!code-csharp[DragDropWalkthrough#OnGiveFeedback](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#ongivefeedback)]
     [!code-vb[DragDropWalkthrough#OnGiveFeedback](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#ongivefeedback)]  
  
     Isso <xref:System.Windows.UIElement.OnGiveFeedback%2A> substituição executa as seguintes tarefas:  
  
    -   Verifica o <xref:System.Windows.GiveFeedbackEventArgs.Effects%2A> valores que são definidos no destino de soltar <xref:System.Windows.UIElement.DragOver> manipulador de eventos.  
  
    -   Define um cursor personalizado com base no <xref:System.Windows.GiveFeedbackEventArgs.Effects%2A> valor. O cursor deve fornecer comentários visuais ao usuário a respeito de qual será o efeito de soltar os dados.  
  
3.  Pressione F5 para compilar e executar o aplicativo.  
  
4.  Arraste um círculo controle sobre os painéis, o círculo, e o <xref:System.Windows.Controls.TextBox>. Observe que os cursores agora são os cursores personalizados que você especificou no <xref:System.Windows.UIElement.OnGiveFeedback%2A> substituir.  
  
     ![Arraste e solte com os cursores personalizados](../../../../docs/framework/wpf/advanced/media/dragdrop-customcursor.png "DragDrop_CustomCursor")  
  
5.  Selecione o texto `green` do <xref:System.Windows.Controls.TextBox>.  
  
6.  Arraste o texto `green` para um controle do círculo. Observe que os cursores padrão são mostrados para indicar os efeitos da operação do tipo “arrastar e soltar”. O cursor de comentários sempre é definido pela fonte de arrastar.  
  
## <a name="implementing-drop-target-events-in-the-user-control"></a>Implementando eventos de destino de soltar no controle de usuário  
 Nesta seção, você especificará que o controle de usuário é um destino de soltar, substituirá os métodos que permitem que o controle de usuário seja um destino de soltar e processará os dados soltos nele.  
  
### <a name="to-enable-the-user-control-to-be-a-drop-target"></a>Para permitir que o controle de usuário seja um destino de soltar  
  
1.  Abra o Circle.xaml.  
  
2.  Na abertura <xref:System.Windows.Controls.UserControl> marca, adicione o <xref:System.Windows.UIElement.AllowDrop%2A> propriedade e defina-a como `true`.  
  
     [!code-xaml[DragDropWalkthrough#UCTagXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml#uctagxaml)]  
  
 O <xref:System.Windows.UIElement.OnDrop%2A> método é chamado quando o <xref:System.Windows.UIElement.AllowDrop%2A> está definida como `true` e dados de origem do arrasto são arrastados para o controle de usuário do círculo. Nesse método, você processará os dados que foram soltos e aplicará os dados ao círculo.  
  
### <a name="to-process-the-dropped-data"></a>Para processar os dados soltos  
  
1.  Abra Circle.xaml.cs ou Circle.xaml.vb.  
  
2.  Adicione o seguinte <xref:System.Windows.UIElement.OnDrop%2A> substituição para fornecer manipulação de classe para o <xref:System.Windows.UIElement.Drop> evento.  
  
     [!code-csharp[DragDropWalkthrough#OnDrop](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#ondrop)]
     [!code-vb[DragDropWalkthrough#OnDrop](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#ondrop)]  
  
     Isso <xref:System.Windows.UIElement.OnDrop%2A> substituição executa as seguintes tarefas:  
  
    -   Usa o <xref:System.Windows.DataObject.GetDataPresent%2A> método para verificar se os dados arrastados contém um objeto de cadeia de caracteres.  
  
    -   Usa o <xref:System.Windows.DataObject.GetData%2A> método para extrair os dados de cadeia de caracteres se ele estiver presente.  
  
    -   Usa um <xref:System.Windows.Media.BrushConverter> ao tentar converter a cadeia de caracteres para um <xref:System.Windows.Media.Brush>.  
  
    -   Se a conversão for bem-sucedida, o pincel aplica-se a <xref:System.Windows.Shapes.Shape.Fill%2A> do <xref:System.Windows.Shapes.Ellipse> que fornece a interface do usuário do controle do círculo.  
  
    -   Marcas de <xref:System.Windows.UIElement.Drop> eventos tratados. O evento de soltar deve ser marcado como manipulado para que os outros elementos que o recebem saibam que foi manipulado pelo controle de usuário do círculo.  
  
3.  Pressione F5 para compilar e executar o aplicativo.  
  
4.  Selecione o texto `green` no <xref:System.Windows.Controls.TextBox>.  
  
5.  Arraste o texto para um controle do círculo e solte-o. O círculo muda de azul para verde.  
  
     ![Converta uma cadeia de caracteres em um pincel](../../../../docs/framework/wpf/advanced/media/dragdrop-dropgreentext.png "DragDrop_DropGreenText")  
  
6.  Digite o texto `green` no <xref:System.Windows.Controls.TextBox>.  
  
7.  Selecione o texto `gre` no <xref:System.Windows.Controls.TextBox>.  
  
8.  Arraste-o para um controle do círculo e solte-o. Observe que o cursor muda para indicar que é permitido soltar; porém, a cor do círculo não muda, porque `gre` não é uma cor válida.  
  
9. Arraste do controle do círculo verde e solte no controle do círculo azul. O círculo muda de azul para verde. Observe que o cursor é mostrado depende se o <xref:System.Windows.Controls.TextBox> ou o círculo é a origem do arrasto.  
  
 Definindo o <xref:System.Windows.UIElement.AllowDrop%2A> propriedade `true` e processamento de dados descartados é tudo o que é necessário para habilitar um elemento seja um destino de soltar. No entanto, para fornecer uma melhor experiência de usuário, você deve também tratar o <xref:System.Windows.UIElement.DragEnter>, <xref:System.Windows.UIElement.DragLeave>, e <xref:System.Windows.UIElement.DragOver> eventos. Nesses eventos, é possível executar verificações e fornecer comentários adicionais ao usuário antes de soltar os dados.  
  
 Quando dados são arrastados sobre o controle de usuário do círculo, o controle deve notificar a fonte de arrasto se os dados arrastados podem ser processados. Se o controle não souber como processar os dados, deverá recusá-los quando forem soltos. Para fazer isso, você irá manipular o <xref:System.Windows.UIElement.DragOver> evento e defina o <xref:System.Windows.DragEventArgs.Effects%2A> propriedade.  
  
### <a name="to-verify-that-the-data-drop-is-allowed"></a>Para verificar se é permitido soltar os dados  
  
1.  Abra Circle.xaml.cs ou Circle.xaml.vb.  
  
2.  Adicione o seguinte <xref:System.Windows.UIElement.OnDragOver%2A> substituição para fornecer manipulação de classe para o <xref:System.Windows.UIElement.DragOver> evento.  
  
     [!code-csharp[DragDropWalkthrough#OnDragOver](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#ondragover)]
     [!code-vb[DragDropWalkthrough#OnDragOver](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#ondragover)]  
  
     Isso <xref:System.Windows.UIElement.OnDragOver%2A> substituição executa as seguintes tarefas:  
  
    -   Define a propriedade <xref:System.Windows.DragEventArgs.Effects%2A> como <xref:System.Windows.DragDropEffects.None>.  
  
    -   Executa as mesmas verificações são executadas no <xref:System.Windows.UIElement.OnDrop%2A> método para determinar se o controle de usuário do círculo pode processar os dados arrastados.  
  
    -   Se o controle de usuário pode processar os dados, define o <xref:System.Windows.DragEventArgs.Effects%2A> propriedade <xref:System.Windows.DragDropEffects.Copy> ou <xref:System.Windows.DragDropEffects.Move>.  
  
3.  Pressione F5 para compilar e executar o aplicativo.  
  
4.  Selecione o texto `gre` no <xref:System.Windows.Controls.TextBox>.  
  
5.  Arraste o texto para um controle do círculo. Observe que, agora, o cursor muda para indicar que não é permitido soltar, porque `gre` não é uma cor válida.  
  
 É possível aprimorar ainda mais a experiência do usuário por meio da aplicação de uma visualização da operação do tipo “soltar”. Para o controle de usuário do círculo, você substituirá o <xref:System.Windows.UIElement.OnDragEnter%2A> e <xref:System.Windows.UIElement.OnDragLeave%2A> métodos. Quando os dados são arrastados sobre o controle, o plano de fundo atual <xref:System.Windows.Shapes.Shape.Fill%2A> é salvo em uma variável de espaço reservado. A cadeia de caracteres é convertida em um pincel e aplicada para o <xref:System.Windows.Shapes.Ellipse> que fornece o círculo interface do usuário. Se os dados são arrastados para fora do círculo sem queda original <xref:System.Windows.Shapes.Shape.Fill%2A> valor novamente é aplicado ao círculo.  
  
### <a name="to-preview-the-effects-of-the-drag-and-drop-operation"></a>Para visualizar os efeitos da operação do tipo “arrastar e soltar”  
  
1.  Abra Circle.xaml.cs ou Circle.xaml.vb.  
  
2.  Na classe do círculo, declarar uma particular <xref:System.Windows.Media.Brush> variável chamada `_previousFill` e inicializá-lo para `null`.  
  
     [!code-csharp[DragDropWalkthrough#Brush](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#brush)]
     [!code-vb[DragDropWalkthrough#Brush](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#brush)]  
  
3.  Adicione o seguinte <xref:System.Windows.UIElement.OnDragEnter%2A> substituição para fornecer manipulação de classe para o <xref:System.Windows.UIElement.DragEnter> evento.  
  
     [!code-csharp[DragDropWalkthrough#OnDragEnter](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#ondragenter)]
     [!code-vb[DragDropWalkthrough#OnDragEnter](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#ondragenter)]  
  
     Isso <xref:System.Windows.UIElement.OnDragEnter%2A> substituição executa as seguintes tarefas:  
  
    -   Salva o <xref:System.Windows.Shapes.Shape.Fill%2A> propriedade o <xref:System.Windows.Shapes.Ellipse> no `_previousFill` variável.  
  
    -   Executa as mesmas verificações são executadas no <xref:System.Windows.UIElement.OnDrop%2A> método para determinar se os dados podem ser convertidos em um <xref:System.Windows.Media.Brush>.  
  
    -   Se os dados são convertidos para um válida <xref:System.Windows.Media.Brush>, aplica-se para o <xref:System.Windows.Shapes.Shape.Fill%2A> do <xref:System.Windows.Shapes.Ellipse>.  
  
4.  Adicione o seguinte <xref:System.Windows.UIElement.OnDragLeave%2A> substituição para fornecer manipulação de classe para o <xref:System.Windows.UIElement.DragLeave> evento.  
  
     [!code-csharp[DragDropWalkthrough#OnDragLeave](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#ondragleave)]
     [!code-vb[DragDropWalkthrough#OnDragLeave](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#ondragleave)]  
  
     Isso <xref:System.Windows.UIElement.OnDragLeave%2A> substituição executa as seguintes tarefas:  
  
    -   Aplica-se a <xref:System.Windows.Media.Brush> salvo no `_previousFill` variável para o <xref:System.Windows.Shapes.Shape.Fill%2A> do <xref:System.Windows.Shapes.Ellipse> que fornece a interface do usuário do controle de usuário do círculo.  
  
5.  Pressione F5 para compilar e executar o aplicativo.  
  
6.  Selecione o texto `green` no <xref:System.Windows.Controls.TextBox>.  
  
7.  Arraste o texto sobre um controle do círculo sem soltá-lo. O círculo muda de azul para verde.  
  
     ![Visualize os efeitos de uma operação do tipo “arrastar&#45;e&#45;soltar”](../../../../docs/framework/wpf/advanced/media/dragdrop-previeweffects.png "DragDrop_PreviewEffects")  
  
8.  Arraste o texto para fora do controle do círculo. O círculo volta de verde para azul.  
  
## <a name="enabling-a-panel-to-receive-dropped-data"></a>Permitindo que um painel receba dados que foram soltos  
 Nesta seção, você permitirá que os painéis que hospedam os controles de usuário do círculo funcionem como destinos de soltar para os dados arrastados do círculo. Você implementará o código que permite mover um círculo de um painel para outro ou fazer uma cópia de um controle do círculo, mantendo a tecla CTRL pressionada enquanto arrasta e solta em um círculo.  
  
### <a name="to-enable-the-panel-to-be-a-drop-target"></a>Para permitir que o painel seja um destino de soltar  
  
1.  Abra MainWindow.xaml.  
  
2.  Como mostra o XAML a seguir, em cada uma da <xref:System.Windows.Controls.StackPanel> controles, adicionar manipuladores para o <xref:System.Windows.UIElement.DragOver> e <xref:System.Windows.UIElement.Drop> eventos. Nome do <xref:System.Windows.UIElement.DragOver> manipulador de eventos, `panel_DragOver`e nomeie o <xref:System.Windows.UIElement.Drop> manipulador de eventos, `panel_Drop`.  
  
     [!code-xaml[DragDropWalkthrough#PanelsXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/MainWindow.xaml#panelsxaml)]  
  
3.  Abra MainWindows.xaml.cs ou MainWindow.xaml.vb.  
  
4.  Adicione o seguinte código para o <xref:System.Windows.UIElement.DragOver> manipulador de eventos.  
  
     [!code-csharp[DragDropWalkthrough#PanelDragOver](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/MainWindow.xaml.cs#paneldragover)]
     [!code-vb[DragDropWalkthrough#PanelDragOver](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/MainWindow.xaml.vb#paneldragover)]  
  
     Isso <xref:System.Windows.UIElement.DragOver> manipulador de eventos executa as seguintes tarefas:  
  
    -   Verifica se os dados arrastados contém os dados de "Objeto" que foi empacotados no <xref:System.Windows.DataObject> pelo controle de usuário círculo e passado na chamada para <xref:System.Windows.DragDrop.DoDragDrop%2A>.  
  
    -   Se os dados do “objeto” estiverem presentes, verifica se a tecla CTRL está pressionada.  
  
    -   Se for pressionada a tecla CTRL, define o <xref:System.Windows.DragEventArgs.Effects%2A> propriedade <xref:System.Windows.DragDropEffects.Copy>. Caso contrário, defina o <xref:System.Windows.DragEventArgs.Effects%2A> propriedade <xref:System.Windows.DragDropEffects.Move>.  
  
5.  Adicione o seguinte código para o <xref:System.Windows.UIElement.Drop> manipulador de eventos.  
  
     [!code-csharp[DragDropWalkthrough#PanelDrop](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/MainWindow.xaml.cs#paneldrop)]
     [!code-vb[DragDropWalkthrough#PanelDrop](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/MainWindow.xaml.vb#paneldrop)]  
  
     Isso <xref:System.Windows.UIElement.Drop> manipulador de eventos executa as seguintes tarefas:  
  
    -   Verifica se o <xref:System.Windows.UIElement.Drop> evento já foi tratado. Por exemplo, se um círculo é solto em outro círculo que identificadores o <xref:System.Windows.UIElement.Drop> evento, você não quiser que o painel que contém o círculo para manipulá-lo também.  
  
    -   Se o <xref:System.Windows.UIElement.Drop> evento não é tratado, verifica se a tecla CTRL pressionada.  
  
    -   Se a tecla CTRL foi pressionada quando o <xref:System.Windows.UIElement.Drop> acontece, faz uma cópia do círculo controla e adicioná-lo para o <xref:System.Windows.Controls.Panel.Children%2A> coleção do <xref:System.Windows.Controls.StackPanel>.  
  
    -   Se não for pressionada a tecla CTRL, move o círculo do <xref:System.Windows.Controls.Panel.Children%2A> coleção de seu painel pai para o <xref:System.Windows.Controls.Panel.Children%2A> coleção do painel que ele foi removido.  
  
    -   Conjuntos de <xref:System.Windows.DragEventArgs.Effects%2A> propriedade para notificar o <xref:System.Windows.DragDrop.DoDragDrop%2A> método se uma operação de mover ou copiar foi executada.  
  
6.  Pressione F5 para compilar e executar o aplicativo.  
  
7.  Selecione o texto `green` do <xref:System.Windows.Controls.TextBox>.  
  
8.  Arraste o texto sobre um controle do círculo e solte-o.  
  
9. Arraste um controle do círculo do painel esquerdo para o painel direito e solte-o. O círculo é removido do <xref:System.Windows.Controls.Panel.Children%2A> coleção do painel esquerdo e adicionado à coleção de filhos do painel à direita.  
  
10. Arraste um controle do círculo do painel em que está para o outro painel e solte-o enquanto pressiona a tecla CTRL. Círculo é copiado e a cópia é adicionada para o <xref:System.Windows.Controls.Panel.Children%2A> conjunto do painel de recebimento.  
  
     ![Arrastando um círculo enquanto pressiona a tecla CTRL](../../../../docs/framework/wpf/advanced/media/dragdrop-paneldrop.png "DragDrop_PanelDrop")  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral de arrastar e soltar](../../../../docs/framework/wpf/advanced/drag-and-drop-overview.md)
