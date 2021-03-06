---
title: Como obter ou definir propriedades de posicionamento da tela
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Canvas control [WPF], setting positioning properties
ms.assetid: 1636b950-2b5a-4507-8a10-c5034cc58b1c
ms.openlocfilehash: 294b49d427a67da849ce930cf29a48f1735bf135
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-get-or-set-canvas-positioning-properties"></a>Como obter ou definir propriedades de posicionamento da tela
Este exemplo mostra como usar os métodos de posicionamento de <xref:System.Windows.Controls.Canvas> elemento para posicionar conteúdo filho. Este exemplo usa conteúdo em um <xref:System.Windows.Controls.ListBoxItem> para representar valores de posicionamento e converte os valores em instâncias de <xref:System.Double>, que é um argumento requerido para posicionamento. Os valores são então convertidos de volta em cadeias de caracteres e exibidos como texto em uma <xref:System.Windows.Controls.TextBlock> elemento usando o <xref:System.Windows.Controls.Canvas.GetLeft%2A> método.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir cria um <xref:System.Windows.Controls.ListBox> elemento que tem onze selecionável <xref:System.Windows.Controls.ListBoxItem> elementos. O <xref:System.Windows.Controls.Primitives.Selector.SelectionChanged> os disparadores de evento de `ChangeLeft` método personalizado, que define o bloco de código subsequentes.  
  
 Cada <xref:System.Windows.Controls.ListBoxItem> representa um <xref:System.Double> valor, que é um dos argumentos que o <xref:System.Windows.Controls.Canvas.SetLeft%2A> método <xref:System.Windows.Controls.Canvas> aceita. Para usar um <xref:System.Windows.Controls.ListBoxItem> para representar uma instância de <xref:System.Double>, você deve primeiro converter o <xref:System.Windows.Controls.ListBoxItem> para o tipo de dados correto.  
  
 [!code-xaml[CanvasPositioningProperties#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CanvasPositioningProperties/CSharp/Window1.xaml#1)]  
  
 Quando um usuário altera a <xref:System.Windows.Controls.ListBox> seleção, ele chama o `ChangeLeft` método personalizado. Esse método passa o <xref:System.Windows.Controls.ListBoxItem> para um <xref:System.Windows.LengthConverter> objeto, que converte o <xref:System.Windows.Controls.ContentControl.Content%2A> de um <xref:System.Windows.Controls.ListBoxItem> para uma instância de <xref:System.Double> (Observe que esse valor já foi convertido em um <xref:System.String> usando o <xref:System.Windows.Controls.Control.ToString%2A> método). Este valor é então passado para o <xref:System.Windows.Controls.Canvas.SetLeft%2A> e <xref:System.Windows.Controls.Canvas.GetLeft%2A> métodos de <xref:System.Windows.Controls.Canvas> para alterar a posição do `text1` objeto.  
  
 [!code-csharp[CanvasPositioningProperties#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CanvasPositioningProperties/CSharp/Window1.xaml.cs#2)]
 [!code-vb[CanvasPositioningProperties#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CanvasPositioningProperties/VisualBasic/Window1.xaml.vb#2)]  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.Windows.Controls.Canvas>  
 <xref:System.Windows.Controls.ListBoxItem>  
 <xref:System.Windows.LengthConverter>  
 [Visão geral de painéis](../../../../docs/framework/wpf/controls/panels-overview.md)
