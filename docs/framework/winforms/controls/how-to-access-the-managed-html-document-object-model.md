---
title: Como acessar o Document Object Model HTML gerenciado
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- HTML DOM [Windows Forms], accessing
- managed HTML DOM [Windows Forms], accessing
ms.assetid: 40fa5cd5-1ed8-42f6-a93f-9ac01608bbeb
ms.openlocfilehash: 175a29322fe2af13992e267b3fc3308b70212272
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-access-the-managed-html-document-object-model"></a>Como acessar o Document Object Model HTML gerenciado
É possível acessar o Document Object Model (DOM) do HTML gerenciado a partir de dois tipos de aplicativos:  
  
-   Um aplicativo do Windows Forms (.exe) que hospedou o controle <xref:System.Windows.Forms.WebBrowser> gerenciado. Essas duas tecnologias se complementam entre si, com o controle <xref:System.Windows.Forms.WebBrowser> exibindo a página para o usuário e o DOM do HTML representando a estrutura lógica do documento.  
  
-   Um <xref:System.Windows.Forms.UserControl> do Windows Forms hospedado dentro do Internet Explorer. É possível acessar o DOM do HTML que representa a página na qual o <xref:System.Windows.Forms.UserControl> está hospedado para alterar a estrutura do documento ou abrir caixas de diálogo restritas, entre muitas outras possibilidades.  
  
### <a name="to-access-dom-from-a-windows-forms-application"></a>Para acessar o DOM a partir de um aplicativo do Windows Forms  
  
1.  Hospede um controle <xref:System.Windows.Forms.WebBrowser> dentro do aplicativo do Windows Forms e monitore pelo evento <xref:System.Windows.Forms.WebBrowser.DocumentCompleted>. Para obter detalhes sobre controles de host e monitoramento de eventos, consulte [Eventos](../../../../docs/standard/events/index.md).  
  
2.  Recupere o <xref:System.Windows.Forms.HtmlDocument> da página atual acessando a propriedade <xref:System.Windows.Forms.WebBrowser.Document%2A> do controle <xref:System.Windows.Forms.WebBrowser>.  

### <a name="to-access-dom-from-a-usercontrol-hosted-in-internet-explorer"></a>Para acessar o DOM a partir de um UserControl hospedado no Internet Explorer  
  
1.  Crie sua própria classe derivada personalizada da classe <xref:System.Windows.Forms.UserControl>. Para mais informações, consulte [Como criar controles compostos](../../../../docs/framework/winforms/controls/how-to-author-composite-controls.md).  
  
2.  Coloque o seguinte código dentro do manipulador de eventos Carregar do <xref:System.Windows.Forms.UserControl>:  
  
 [!code-csharp[AccessHTMLDOMControl#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/AccessHTMLDOMControl/cs/UserControl1.cs#1)]
 [!code-vb[AccessHTMLDOMControl#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/AccessHTMLDOMControl/vb/UserControl1.vb#1)]  
  
## <a name="robust-programming"></a>Programação robusta  
  
1.  Ao usar o DOM através do controle <xref:System.Windows.Forms.WebBrowser>, é sempre necessário esperar até o evento <xref:System.Windows.Forms.WebBrowser.DocumentCompleted> ocorrer antes de tentar acessar a propriedade <xref:System.Windows.Forms.WebBrowser.Document%2A> do controle <xref:System.Windows.Forms.WebBrowser>. O evento <xref:System.Windows.Forms.WebBrowser.DocumentCompleted> é elevado após o documento inteiro ser carregado, se o DOM for usado antes disso, haverá o risco de causar uma exceção de tempo de execução no aplicativo.  
  
## <a name="net-framework-security"></a>Segurança do .NET Framework  
  
1.  O aplicativo ou o <xref:System.Windows.Forms.UserControl> exigirá confiança total para acessar o DOM do HTML gerenciado. Ao implantar um aplicativo do Windows Forms usando [!INCLUDE[ndptecclick](../../../../includes/ndptecclick-md.md)], é possível solicitar confiança total usando Implantação de Aplicativo Confiável ou Elevação de Permissões; consulte [Protegendo Aplicativos ClickOnce](/visualstudio/deployment/securing-clickonce-applications) para obter mais detalhes.  
  
## <a name="see-also"></a>Consulte também  
 [Usando o Modelo de Objeto do Documento HTML gerenciado](../../../../docs/framework/winforms/controls/using-the-managed-html-document-object-model.md)
