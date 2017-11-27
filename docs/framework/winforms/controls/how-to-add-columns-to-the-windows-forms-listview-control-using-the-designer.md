---
title: Como adicionar colunas ao controle ListView dos Windows Forms usando o designer
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-winforms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ListView control [Windows Forms], adding column headers
- columns [Windows Forms], adding to ListView controls
ms.assetid: 5b1a8b4d-587e-479a-95c1-f9b90884f13a
caps.latest.revision: "6"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: 7223fc47c885b7e659b9bab00c276759410d2567
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="how-to-add-columns-to-the-windows-forms-listview-control-using-the-designer"></a><span data-ttu-id="e04f8-102">Como adicionar colunas ao controle ListView dos Windows Forms usando o designer</span><span class="sxs-lookup"><span data-stu-id="e04f8-102">How to: Add Columns to the Windows Forms ListView Control Using the Designer</span></span>
<span data-ttu-id="e04f8-103">Windows Forms <xref:System.Windows.Forms.ListView> controle pode exibir várias colunas para cada lista de item quando o **detalhes** exibição.</span><span class="sxs-lookup"><span data-stu-id="e04f8-103">The Windows Forms <xref:System.Windows.Forms.ListView> control can display multiple columns for each list item when in the **Details** view.</span></span> <span data-ttu-id="e04f8-104">Você pode usar as colunas para exibir vários tipos de informações sobre cada item de lista.</span><span class="sxs-lookup"><span data-stu-id="e04f8-104">You can use the columns to display several types of information about each list item.</span></span> <span data-ttu-id="e04f8-105">Por exemplo, uma lista de arquivos pode exibir o nome do arquivo, tipo de arquivo, tamanho e data da última modificação do arquivo.</span><span class="sxs-lookup"><span data-stu-id="e04f8-105">For example, a list of files could display the file name, file type, size, and date the file was last modified.</span></span> <span data-ttu-id="e04f8-106">Para obter informações sobre como preencher as colunas depois que elas forem criadas, consulte [Como exibir subitens em colunas com o controle ListView dos Windows Forms](../../../../docs/framework/winforms/controls/how-to-display-subitems-in-columns-with-the-windows-forms-listview-control.md).</span><span class="sxs-lookup"><span data-stu-id="e04f8-106">For information on populating the columns once they are created, see [How to: Display Subitems in Columns with the Windows Forms ListView Control](../../../../docs/framework/winforms/controls/how-to-display-subitems-in-columns-with-the-windows-forms-listview-control.md).</span></span>  
  
 <span data-ttu-id="e04f8-107">O procedimento a seguir requer um **aplicativo do Windows** projeto com um formulário que contém um <xref:System.Windows.Forms.ListView> controle.</span><span class="sxs-lookup"><span data-stu-id="e04f8-107">The following procedure requires a **Windows Application** project with a form containing a <xref:System.Windows.Forms.ListView> control.</span></span> <span data-ttu-id="e04f8-108">Para obter informações sobre como configurar um projeto desse tipo, consulte [Como Criar um Projeto de Aplicativo do Windows](http://msdn.microsoft.com/en-us/b2f93fed-c635-4705-8d0e-cf079a264efa) e [Como Adicionar Controles ao Windows Forms](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md).</span><span class="sxs-lookup"><span data-stu-id="e04f8-108">For information about setting up such a project, see [How to: Create a Windows Application Project](http://msdn.microsoft.com/en-us/b2f93fed-c635-4705-8d0e-cf079a264efa) and [How to: Add Controls to Windows Forms](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md).</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="e04f8-109">As caixas de diálogo e os comandos de menu que você vê podem ser diferentes dos descritos na Ajuda, dependendo da sua edição ou das configurações ativas.</span><span class="sxs-lookup"><span data-stu-id="e04f8-109">The dialog boxes and menu commands you see might differ from those described in Help depending on your active settings or edition.</span></span> <span data-ttu-id="e04f8-110">Para alterar as configurações, escolha **Importar e Exportar Configurações** no menu **Ferramentas**.</span><span class="sxs-lookup"><span data-stu-id="e04f8-110">To change your settings, choose **Import and Export Settings** on the **Tools** menu.</span></span> <span data-ttu-id="e04f8-111">Para obter mais informações, consulte [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3).</span><span class="sxs-lookup"><span data-stu-id="e04f8-111">For more information, see [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3).</span></span>  
  
### <a name="to-add-columns-in-the-designer"></a><span data-ttu-id="e04f8-112">Para adicionar colunas no designer</span><span class="sxs-lookup"><span data-stu-id="e04f8-112">To add columns in the designer</span></span>  
  
1.  <span data-ttu-id="e04f8-113">No **propriedades** janela, defina o controle <xref:System.Windows.Forms.ListView.View%2A> propriedade <xref:System.Windows.Forms.View.Details>.</span><span class="sxs-lookup"><span data-stu-id="e04f8-113">In the **Properties** window, set the control's <xref:System.Windows.Forms.ListView.View%2A> property to <xref:System.Windows.Forms.View.Details>.</span></span>  
  
2.  <span data-ttu-id="e04f8-114">No **propriedades** janela, clique no **reticências** botão (![de tela de VisualStudioEllipsesButton](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")) ao lado de o <xref:System.Windows.Forms.ListView.Columns%2A> propriedade.</span><span class="sxs-lookup"><span data-stu-id="e04f8-114">In the **Properties** window, click the **Ellipsis** button (![VisualStudioEllipsesButton screenshot](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")) next to the <xref:System.Windows.Forms.ListView.Columns%2A> property.</span></span>  
  
     <span data-ttu-id="e04f8-115">O **Editor de coleção ColumnHeader** é exibido.</span><span class="sxs-lookup"><span data-stu-id="e04f8-115">The **ColumnHeader Collection Editor** appears.</span></span>  
  
3.  <span data-ttu-id="e04f8-116">Use o botão **Adicionar** para adicionar novas colunas.</span><span class="sxs-lookup"><span data-stu-id="e04f8-116">Use the **Add** button to add new columns.</span></span> <span data-ttu-id="e04f8-117">Em seguida, você pode selecionar o cabeçalho da coluna e definir seu texto (a legenda da coluna), o alinhamento do texto e a largura.</span><span class="sxs-lookup"><span data-stu-id="e04f8-117">You can then select the column header and set its text (the caption of the column), text alignment, and width.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="e04f8-118">Consulte também</span><span class="sxs-lookup"><span data-stu-id="e04f8-118">See Also</span></span>  
 [<span data-ttu-id="e04f8-119">Visão geral do controle ListView</span><span class="sxs-lookup"><span data-stu-id="e04f8-119">ListView Control Overview</span></span>](../../../../docs/framework/winforms/controls/listview-control-overview-windows-forms.md)  
 [<span data-ttu-id="e04f8-120">Como Adicionar e Remover Itens com o Controle ListView dos Windows Forms</span><span class="sxs-lookup"><span data-stu-id="e04f8-120">How to: Add and Remove Items with the Windows Forms ListView Control</span></span>](../../../../docs/framework/winforms/controls/how-to-add-and-remove-items-with-the-windows-forms-listview-control.md)  
 [<span data-ttu-id="e04f8-121">Como Exibir Subitens em Colunas com o Controle ListView dos Windows Forms</span><span class="sxs-lookup"><span data-stu-id="e04f8-121">How to: Display Subitems in Columns with the Windows Forms ListView Control</span></span>](../../../../docs/framework/winforms/controls/how-to-display-subitems-in-columns-with-the-windows-forms-listview-control.md)  
 [<span data-ttu-id="e04f8-122">Como Exibir Ícones do Controle ListView dos Windows Forms</span><span class="sxs-lookup"><span data-stu-id="e04f8-122">How to: Display Icons for the Windows Forms ListView Control</span></span>](../../../../docs/framework/winforms/controls/how-to-display-icons-for-the-windows-forms-listview-control.md)  
 [<span data-ttu-id="e04f8-123">Como adicionar informações personalizadas a um controle TreeView ou ListView (Windows Forms)</span><span class="sxs-lookup"><span data-stu-id="e04f8-123">How to: Add Custom Information to a TreeView or ListView Control (Windows Forms)</span></span>](../../../../docs/framework/winforms/controls/add-custom-information-to-a-treeview-or-listview-control-wf.md)