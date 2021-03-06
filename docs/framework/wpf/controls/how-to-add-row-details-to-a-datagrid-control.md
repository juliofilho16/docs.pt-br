---
title: Como adicionar detalhes de linha a um controle DataGrid
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DataTemplate [WPF], DataGrid
- row details [WPF], DataGrid
- DataGrid [WPF], row details
ms.assetid: 0bdc6f50-9b4c-483f-9df6-a47a1fde998b
ms.openlocfilehash: b6b0cc99c9833e514d2d52ecf139ab8e110f73e3
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-add-row-details-to-a-datagrid-control"></a>Como adicionar detalhes de linha a um controle DataGrid
Ao usar o <xref:System.Windows.Controls.DataGrid> controle, você pode personalizar a apresentação de dados com a adição de uma seção de detalhes da linha. Adicionar uma seção de detalhes de linha permite agrupar alguns dados em um modelo que fica opcionalmente visível ou recolhido. Por exemplo, você pode adicionar detalhes da linha para um <xref:System.Windows.Controls.DataGrid> que apresenta apenas um resumo dos dados para cada linha a <xref:System.Windows.Controls.DataGrid>, mas apresenta mais campos de dados quando o usuário seleciona uma linha. Definir o modelo para a seção detalhes da linha de <xref:System.Windows.Controls.DataGrid.RowDetailsTemplate%2A> propriedade. A ilustração a seguir mostra um exemplo de uma seção de detalhes da linha.  
  
 ![DataGrid mostrada com detalhes de linha](../../../../docs/framework/wpf/controls/media/ndp-rowdetails.png "NDP_RowDetails")  
  
 Defina o modelo de detalhes de linha como XAML embutido ou como um recurso. Ambas as abordagens são mostradas nos procedimentos a seguir. Um modelo de dados adicionado como um recurso pode ser usado em todo o projeto sem recriar o modelo. Um modelo de dados que é adicionado como XAML embutido só é acessível pelo controle no qual ele está definido.  
  
### <a name="to-display-row-details-by-using-inline-xaml"></a>Para exibir detalhes de linha usando XAML embutido  
  
1.  Criar um <xref:System.Windows.Controls.DataGrid> que exibe dados de uma fonte de dados.  
  
2.  No elemento <xref:System.Windows.Controls.DataGrid>, adicione um elemento <xref:System.Windows.Controls.DataGrid.RowDetailsTemplate%2A>.  
  
3.  Criar um <xref:System.Windows.DataTemplate> que define a aparência da seção de detalhes da linha.  
  
     O XAML a seguir mostra o <xref:System.Windows.Controls.DataGrid> e como definir o <xref:System.Windows.Controls.DataGrid.RowDetailsTemplate%2A> embutido. O <xref:System.Windows.Controls.DataGrid> exibe três valores em cada linha e três valores mais quando a linha está selecionada.  
  
     [!code-xaml[DataGrid_RowDetails#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/datagrid_rowdetails/cs/mainwindow.xaml#1)]  
  
     O código a seguir mostra a consulta que é usada para selecionar os dados que são exibidos no <xref:System.Windows.Controls.DataGrid>. Neste exemplo, a consulta seleciona dados de uma entidade que contém informações de clientes.  
  
     [!code-csharp[DataGrid_RowDetails#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/datagrid_rowdetails/cs/mainwindow.xaml.cs#2)]
     [!code-vb[DataGrid_RowDetails#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/datagrid_rowdetails/vb/mainwindow.xaml.vb#2)]  
  
### <a name="to-display-row-details-by-using-a-resource"></a>Para exibir detalhes de linha usando um recurso  
  
1.  Criar um <xref:System.Windows.Controls.DataGrid> que exibe dados de uma fonte de dados.  
  
2.  Adicionar um <xref:System.Windows.FrameworkElement.Resources%2A> elemento ao elemento raiz, como um <xref:System.Windows.Window> controle ou um <xref:System.Windows.Controls.Page> controlar ou adicionar um <xref:System.Windows.Application.Resources%2A> elemento para o <xref:System.Windows.Application> classe no arquivo App. XAML (ou Application).  
  
3.  O elemento de recursos, criar um <xref:System.Windows.DataTemplate> que define a aparência da seção de detalhes da linha.  
  
     O XAML a seguir mostra o <xref:System.Windows.Controls.DataGrid.RowDetailsTemplate%2A> definido no <xref:System.Windows.Application> classe.  
  
     [!code-xaml[DataGrid_RowDetails#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/datagrid_rowdetails/cs/app.xaml#3)]  
  
4.  Sobre o <xref:System.Windows.DataTemplate>, defina o [diretiva X:Key](../../../../docs/framework/xaml-services/x-key-directive.md) para um valor que identifica exclusivamente o modelo de dados.  
  
5.  No <xref:System.Windows.Controls.DataGrid> elemento, defina o <xref:System.Windows.Controls.DataGrid.RowDetailsTemplate%2A> propriedade para o recurso definida nas etapas anteriores. Atribua o recurso como um recurso estático.  
  
     O XAML a seguir mostra o <xref:System.Windows.Controls.DataGrid.RowDetailsTemplate%2A> propriedade definida para o recurso do exemplo anterior.  
  
     [!code-xaml[DataGrid_RowDetails#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/datagrid_rowdetails/cs/window2.xaml#4)]  
  
### <a name="to-set-visibility-and-prevent-horizontal-scrolling-for-row-details"></a>Para definir a visibilidade e evitar a rolagem horizontal para detalhes de linha  
  
1.  Se necessário, defina o <xref:System.Windows.Controls.DataGrid.RowDetailsVisibilityMode%2A> propriedade para um <xref:System.Windows.Controls.DataGridRowDetailsVisibilityMode> valor.  
  
     Por padrão, o valor é definido como <xref:System.Windows.Controls.DataGridRowDetailsVisibilityMode.VisibleWhenSelected>. Você pode configurá-lo <xref:System.Windows.Controls.DataGridRowDetailsVisibilityMode.Visible> para mostrar os detalhes de todas as linhas ou <xref:System.Windows.Controls.DataGridRowDetailsVisibilityMode.Collapsed> para ocultar os detalhes de todas as linhas.  
  
2.  Se necessário, defina o <xref:System.Windows.Controls.DataGrid.AreRowDetailsFrozen%2A> propriedade `true` para impedir que a linha de detalhes de seção de rolagem horizontal.
