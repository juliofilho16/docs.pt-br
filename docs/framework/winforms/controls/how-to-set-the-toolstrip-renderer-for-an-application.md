---
title: Como definir o renderizador ToolStrip para um aplicativo
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Renderer property [Windows Forms]
- ToolStripProfessionalRenderer class [Windows Forms]
- ToolStrip control [Windows Forms]
- MenuStrip control [Windows Forms]
- toolbars [Windows Forms], customizing
ms.assetid: 46acef3e-9844-4ae8-9a2e-3006fe99cadf
ms.openlocfilehash: f4189b19b78ce3cda1981220caa1fce3f2ec708d
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-set-the-toolstrip-renderer-for-an-application"></a>Como definir o renderizador ToolStrip para um aplicativo
Você pode personalizar a aparência de seu <xref:System.Windows.Forms.ToolStrip> controla individualmente ou todos os <xref:System.Windows.Forms.ToolStrip> controles em seu aplicativo.  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir demonstra como aplicar seletivamente um renderizador personalizado para um <xref:System.Windows.Forms.ToolStrip> controle e um <xref:System.Windows.Forms.MenuStrip> controle.  
  
 Para usar este exemplo de código, compilar e executar o aplicativo e, em seguida, selecione o escopo de rending personalizado do <xref:System.Windows.Forms.ComboBox> controle. Clique em **Aplicar** para definir o renderizador.  
  
 Para ver o processamento do item de menu personalizados, selecione o <xref:System.Windows.Forms.MenuStrip> opção o <xref:System.Windows.Forms.ComboBox> de controle, clique em **aplicar**e, em seguida, abra o **arquivo** item de menu.  
  
 [!code-csharp[System.Windows.Forms.ToolStrip.Misc#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.Misc/CS/Program.cs#1)]
 [!code-vb[System.Windows.Forms.ToolStrip.Misc#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.Misc/VB/Program.vb#1)]  
[!code-csharp[System.Windows.Forms.ToolStrip.Misc#70](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.Misc/CS/Program.cs#70)]
[!code-vb[System.Windows.Forms.ToolStrip.Misc#70](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.Misc/VB/Program.vb#70)]  
  
 Definir o <xref:System.Windows.Forms.ToolStripManager.Renderer%2A?displayProperty=nameWithType> aplicar um renderizador personalizado para todos o <xref:System.Windows.Forms.ToolStrip> controles em seu aplicativo.  
  
 Definir o <xref:System.Windows.Forms.ToolStrip.Renderer%2A?displayProperty=nameWithType> aplicar um renderizador personalizado a um indivíduo <xref:System.Windows.Forms.ToolStrip> controle.  
  
## <a name="compiling-the-code"></a>Compilando o código  
 Este exemplo requer:  
  
-   Referências aos assemblies System.Design, System.Drawing e System.Windows.Forms.  
  
 Para obter informações sobre como criar este exemplo da linha de comando para o visual Basic ou Visual c#, consulte [Compilando a partir da linha de comando](~/docs/visual-basic/reference/command-line-compiler/building-from-the-command-line.md) ou [criação de linha de comando com csc.exe](~/docs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md). Você também pode criar este exemplo no Visual Studio colando o código em um novo projeto.  Consulte também [Como compilar e executar um exemplo completo de código do Windows Forms usando o Visual Studio](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\)).  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.Windows.Forms.ToolStripManager>  
 <xref:System.Windows.Forms.MenuStrip>  
 <xref:System.Windows.Forms.ToolStrip>  
 <xref:System.Windows.Forms.ToolStripProfessionalRenderer>  
 [Controle ToolStrip](../../../../docs/framework/winforms/controls/toolstrip-control-windows-forms.md)
