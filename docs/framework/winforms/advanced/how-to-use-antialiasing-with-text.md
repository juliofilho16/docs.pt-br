---
title: Como usar suavização com texto
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- strings [Windows Forms], smoothing drawn
- antialiasing [Windows Forms], using with text
- text [Windows Forms], smoothing
- text [Windows Forms], antialiasing
- strings [Windows Forms], antialiasing when drawing
ms.assetid: 48fc34f3-f236-4b01-a0cb-f0752e6d22ae
ms.openlocfilehash: 842c1fb0b73533fd2e87474b9e8cfa282eba2a70
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-use-antialiasing-with-text"></a>Como usar suavização com texto
*Suavização* refere-se a suavização de bordas irregulares de texto para melhorar sua aparência ou legibilidade e gráficos desenhados. Com o gerenciado [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] classes, você pode renderizar texto de antialiasing de alta qualidade, bem como texto de qualidade inferior. Normalmente, renderização de qualidade superior leva mais tempo de processamento de renderização de qualidade inferior. Para definir o nível de qualidade do texto, defina o <xref:System.Drawing.Graphics.TextRenderingHint%2A> propriedade de um <xref:System.Drawing.Graphics> para um dos elementos do <xref:System.Drawing.Text.TextRenderingHint> enumeração  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir desenha texto com duas configurações diferentes de qualidade.  
  
 A ilustração a seguir mostra a saída de cod código de exemplo.  
  
 ![Texto de fontes](../../../../docs/framework/winforms/advanced/media/fontstext10.png "FontsText10")  
  
 [!code-csharp[System.Drawing.FontsAndText#21](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.FontsAndText/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.FontsAndText#21](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.FontsAndText/VB/Class1.vb#21)]  
  
## <a name="compiling-the-code"></a>Compilando o código  
 O exemplo de código anterior foi projetado para uso com o Windows Forms e requer <xref:System.Windows.Forms.PaintEventArgs> `e`, que é um parâmetro de <xref:System.Windows.Forms.PaintEventHandler>.  
  
## <a name="see-also"></a>Consulte também  
 [Usando fontes e texto](../../../../docs/framework/winforms/advanced/using-fonts-and-text.md)
