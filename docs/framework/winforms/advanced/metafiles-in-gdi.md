---
title: Metarquivos no GDI+
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- images [Windows Forms], metafiles
- GDI+, metafiles
- metafiles
ms.assetid: 51da872c-c783-440f-8bf6-1e580a966c31
ms.openlocfilehash: 73cacb7f701768b42121c31cfbc4f26905961231
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="metafiles-in-gdi"></a>Metarquivos no GDI+
[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] fornece o <xref:System.Drawing.Imaging.Metafile> de classe para que você possa registrar e exibir metarquivos. Um metarquivo, também chamado de uma imagem de vetor, é uma imagem que é armazenada como uma sequência de comandos e configurações de desenho. Os comandos e configurações são registradas em um <xref:System.Drawing.Imaging.Metafile> objeto pode ser armazenado na memória ou salvo em um arquivo ou fluxo.  
  
## <a name="metafile-formats"></a>Formatos de metarquivos  
 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] pode exibir metarquivos que foram armazenados nos seguintes formatos:  
  
-   Metarquivo do Windows (WMF)  
  
-   EMF (Metarquivo Avançado)  
  
-   EMF+  
  
 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] pode registrar metarquivos nos formatos EMF e EMF+, mas não no formato WMF.  
  
 EMF+ é uma extensão de EMF que permite que registros [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] sejam armazenados. Há duas variações no formato EMF+: Apenas EMF+ e EMF+ Duplo. Metarquivos Apenas EMF+ contêm apenas registros [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)]. Esses metarquivos podem ser exibidos por [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)], mas não por [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)]. Metarquivos EMF+ Duplos contêm registros [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] e [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)]. Cada registro [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] em um metarquivo EMF+ Duplo é associado a um registro [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)] alternativo. Esses metarquivos podem ser exibidos por [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] ou por [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)].  
  
 O exemplo a seguir exibe um metarquivo que foi salvo anteriormente como um arquivo. O metarquivo é exibido com seu canto superior esquerdo em (100, 100).  
  
 [!code-csharp[System.Drawing.ImagesBitmapsMetafiles#21](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ImagesBitmapsMetafiles/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.ImagesBitmapsMetafiles#21](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ImagesBitmapsMetafiles/VB/Class1.vb#21)]  
  
## <a name="see-also"></a>Consulte também  
 [Imagens, bitmaps e metarquivos](../../../../docs/framework/winforms/advanced/images-bitmaps-and-metafiles.md)
