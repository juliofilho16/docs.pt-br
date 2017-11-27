---
title: "Instruções passo a passo: associando a dados em aplicativos híbridos"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- hybrid applications [WPF interoperability]
- data binding [WPF interoperability]
ms.assetid: 18997e71-745a-4425-9c69-2cbce1d8669e
caps.latest.revision: "39"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: 957559cbc88855700471cc457f76d69ef5a296d9
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="walkthrough-binding-to-data-in-hybrid-applications"></a><span data-ttu-id="6d753-102">Instruções passo a passo: associando a dados em aplicativos híbridos</span><span class="sxs-lookup"><span data-stu-id="6d753-102">Walkthrough: Binding to Data in Hybrid Applications</span></span>
<span data-ttu-id="6d753-103">Associando uma fonte de dados a um controle é essencial para fornecer aos usuários acesso aos dados subjacentes, se você estiver usando [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] ou [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].</span><span class="sxs-lookup"><span data-stu-id="6d753-103">Binding a data source to a control is essential for providing users with access to underlying data, whether you are using [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] or [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].</span></span> <span data-ttu-id="6d753-104">Este passo a passo mostra como você pode usar a associação de dados em aplicativos híbridos que incluem ambas [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] e [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] controles.</span><span class="sxs-lookup"><span data-stu-id="6d753-104">This walkthrough shows how you can use data binding in hybrid applications that include both [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] and [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] controls.</span></span>  
  
 <span data-ttu-id="6d753-105">As tarefas ilustradas neste passo a passo incluem:</span><span class="sxs-lookup"><span data-stu-id="6d753-105">Tasks illustrated in this walkthrough include:</span></span>  
  
-   <span data-ttu-id="6d753-106">Criar o projeto.</span><span class="sxs-lookup"><span data-stu-id="6d753-106">Creating the project.</span></span>  
  
-   <span data-ttu-id="6d753-107">Definir o modelo de dados.</span><span class="sxs-lookup"><span data-stu-id="6d753-107">Defining the data template.</span></span>  
  
-   <span data-ttu-id="6d753-108">Especificar o layout do formulário.</span><span class="sxs-lookup"><span data-stu-id="6d753-108">Specifying the form layout.</span></span>  
  
-   <span data-ttu-id="6d753-109">Especificar associações de dados.</span><span class="sxs-lookup"><span data-stu-id="6d753-109">Specifying data bindings.</span></span>  
  
-   <span data-ttu-id="6d753-110">Exibir dados usando interoperação.</span><span class="sxs-lookup"><span data-stu-id="6d753-110">Displaying data by using interoperation.</span></span>  
  
-   <span data-ttu-id="6d753-111">Adicionar a fonte de dados ao projeto.</span><span class="sxs-lookup"><span data-stu-id="6d753-111">Adding the data source to the project.</span></span>  
  
-   <span data-ttu-id="6d753-112">Criar uma associação à fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="6d753-112">Binding to the data source.</span></span>  
  
 <span data-ttu-id="6d753-113">Para uma listagem de código completa das tarefas ilustradas neste passo a passo, consulte [associação de dados no exemplo de aplicativos híbridos](http://go.microsoft.com/fwlink/?LinkID=159983).</span><span class="sxs-lookup"><span data-stu-id="6d753-113">For a complete code listing of the tasks illustrated in this walkthrough, see [Data Binding in Hybrid Applications Sample](http://go.microsoft.com/fwlink/?LinkID=159983).</span></span>  
  
 <span data-ttu-id="6d753-114">Quando tiver terminado, você terá um entendimento dos recursos de associação de dados em aplicativos híbridos.</span><span class="sxs-lookup"><span data-stu-id="6d753-114">When you are finished, you will have an understanding of data binding features in hybrid applications.</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="6d753-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6d753-115">Prerequisites</span></span>  
 <span data-ttu-id="6d753-116">Você precisa dos seguintes componentes para concluir esta instrução passo a passo:</span><span class="sxs-lookup"><span data-stu-id="6d753-116">You need the following components to complete this walkthrough:</span></span>  
  
-   [!INCLUDE[vs_dev10_long](../../../../includes/vs-dev10-long-md.md)]<span data-ttu-id="6d753-117">.</span><span class="sxs-lookup"><span data-stu-id="6d753-117">.</span></span>  
  
-   <span data-ttu-id="6d753-118">Acesso ao banco de dados de exemplo e em execução no Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6d753-118">Access to the Northwind sample database running on Microsoft SQL Server.</span></span>  
  
## <a name="creating-the-project"></a><span data-ttu-id="6d753-119">Criando o Projeto</span><span class="sxs-lookup"><span data-stu-id="6d753-119">Creating the Project</span></span>  
  
#### <a name="to-create-and-set-up-the-project"></a><span data-ttu-id="6d753-120">Criar e configurar o projeto</span><span class="sxs-lookup"><span data-stu-id="6d753-120">To create and set up the project</span></span>  
  
1.  <span data-ttu-id="6d753-121">Crie um projeto de aplicativo WPF chamado `WPFWithWFAndDatabinding`.</span><span class="sxs-lookup"><span data-stu-id="6d753-121">Create a WPF Application project named `WPFWithWFAndDatabinding`.</span></span>  
  
2.  <span data-ttu-id="6d753-122">No Gerenciador de Soluções, adicione referências aos assemblies a seguir.</span><span class="sxs-lookup"><span data-stu-id="6d753-122">In Solution Explorer, add references to the following assemblies.</span></span>  
  
    -   <span data-ttu-id="6d753-123">WindowsFormsIntegration</span><span class="sxs-lookup"><span data-stu-id="6d753-123">WindowsFormsIntegration</span></span>  
  
    -   <span data-ttu-id="6d753-124">System.Windows.Forms</span><span class="sxs-lookup"><span data-stu-id="6d753-124">System.Windows.Forms</span></span>  
  
3.  <span data-ttu-id="6d753-125">Abra MainWindow.xaml no [!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)].</span><span class="sxs-lookup"><span data-stu-id="6d753-125">Open MainWindow.xaml in the [!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)].</span></span>  
  
4.  <span data-ttu-id="6d753-126">No <xref:System.Windows.Window> elemento, adicione o seguinte [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] mapeamento de namespaces.</span><span class="sxs-lookup"><span data-stu-id="6d753-126">In the <xref:System.Windows.Window> element, add the following [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] namespaces mapping.</span></span>  
  
    ```xaml  
    xmlns:wf="clr-namespace:System.Windows.Forms;assembly=System.Windows.Forms"  
    ```  
  
5.  <span data-ttu-id="6d753-127">Nomeie o padrão <xref:System.Windows.Controls.Grid> elemento `mainGrid` atribuindo o <xref:System.Windows.FrameworkElement.Name%2A> propriedade.</span><span class="sxs-lookup"><span data-stu-id="6d753-127">Name the default <xref:System.Windows.Controls.Grid> element `mainGrid` by assigning the <xref:System.Windows.FrameworkElement.Name%2A> property.</span></span>  
  
     [!code-xaml[WPFWithWFAndDatabinding#8](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml#8)]  
  
## <a name="defining-the-data-template"></a><span data-ttu-id="6d753-128">Definindo o modelo de dados</span><span class="sxs-lookup"><span data-stu-id="6d753-128">Defining the Data Template</span></span>  
 <span data-ttu-id="6d753-129">A lista mestra de clientes é exibida em um <xref:System.Windows.Controls.ListBox> controle.</span><span class="sxs-lookup"><span data-stu-id="6d753-129">The master list of customers is displayed in a <xref:System.Windows.Controls.ListBox> control.</span></span> <span data-ttu-id="6d753-130">O exemplo de código a seguir define uma <xref:System.Windows.DataTemplate> objeto chamado `ListItemsTemplate` que controla a árvore visual do <xref:System.Windows.Controls.ListBox> controle.</span><span class="sxs-lookup"><span data-stu-id="6d753-130">The following code example defines a <xref:System.Windows.DataTemplate> object named `ListItemsTemplate` that controls the visual tree of the <xref:System.Windows.Controls.ListBox> control.</span></span> <span data-ttu-id="6d753-131">Isso <xref:System.Windows.DataTemplate> é atribuído para o <xref:System.Windows.Controls.ListBox> do controle <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A> propriedade.</span><span class="sxs-lookup"><span data-stu-id="6d753-131">This <xref:System.Windows.DataTemplate> is assigned to the <xref:System.Windows.Controls.ListBox> control's <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A> property.</span></span>  
  
#### <a name="to-define-the-data-template"></a><span data-ttu-id="6d753-132">Para definir o modelo de dados</span><span class="sxs-lookup"><span data-stu-id="6d753-132">To define the data template</span></span>  
  
-   <span data-ttu-id="6d753-133">Copie o XAML a seguir para o <xref:System.Windows.Controls.Grid> declaração do elemento.</span><span class="sxs-lookup"><span data-stu-id="6d753-133">Copy the following XAML into the <xref:System.Windows.Controls.Grid> element's declaration.</span></span>  
  
     [!code-xaml[WPFWithWFAndDatabinding#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml#3)]  
  
## <a name="specifying-the-form-layout"></a><span data-ttu-id="6d753-134">Especificando o layout do formulário</span><span class="sxs-lookup"><span data-stu-id="6d753-134">Specifying the Form Layout</span></span>  
 <span data-ttu-id="6d753-135">O layout do formulário é definido por uma grade com três linhas e três colunas.</span><span class="sxs-lookup"><span data-stu-id="6d753-135">The layout of the form is defined by a grid with three rows and three columns.</span></span> <span data-ttu-id="6d753-136"><xref:System.Windows.Controls.Label>controles são fornecidos para identificar cada coluna na tabela Customers.</span><span class="sxs-lookup"><span data-stu-id="6d753-136"><xref:System.Windows.Controls.Label> controls are provided to identify each column in the Customers table.</span></span>  
  
#### <a name="to-set-up-the-grid-layout"></a><span data-ttu-id="6d753-137">Para configurar o layout de grade</span><span class="sxs-lookup"><span data-stu-id="6d753-137">To set up the Grid layout</span></span>  
  
-   <span data-ttu-id="6d753-138">Copie o XAML a seguir para o <xref:System.Windows.Controls.Grid> declaração do elemento.</span><span class="sxs-lookup"><span data-stu-id="6d753-138">Copy the following XAML into the <xref:System.Windows.Controls.Grid> element's declaration.</span></span>  
  
     [!code-xaml[WPFWithWFAndDatabinding#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml#4)]  
  
#### <a name="to-set-up-the-label-controls"></a><span data-ttu-id="6d753-139">Para configurar os controles de Rótulo</span><span class="sxs-lookup"><span data-stu-id="6d753-139">To set up the Label controls</span></span>  
  
-   <span data-ttu-id="6d753-140">Copie o XAML a seguir para o <xref:System.Windows.Controls.Grid> declaração do elemento.</span><span class="sxs-lookup"><span data-stu-id="6d753-140">Copy the following XAML into the <xref:System.Windows.Controls.Grid> element's declaration.</span></span>  
  
     [!code-xaml[WPFWithWFAndDatabinding#5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml#5)]  
  
## <a name="specifying-data-bindings"></a><span data-ttu-id="6d753-141">Especificando associações de dados</span><span class="sxs-lookup"><span data-stu-id="6d753-141">Specifying Data Bindings</span></span>  
 <span data-ttu-id="6d753-142">A lista mestra de clientes é exibida em um <xref:System.Windows.Controls.ListBox> controle.</span><span class="sxs-lookup"><span data-stu-id="6d753-142">The master list of customers is displayed in a <xref:System.Windows.Controls.ListBox> control.</span></span> <span data-ttu-id="6d753-143">O anexo `ListItemsTemplate` associa um <xref:System.Windows.Controls.TextBlock> o controle para o `ContactName` campo do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="6d753-143">The attached `ListItemsTemplate` binds a <xref:System.Windows.Controls.TextBlock> control to the `ContactName` field from the database.</span></span>  
  
 <span data-ttu-id="6d753-144">Os detalhes de cada registro de cliente são exibidos em vários <xref:System.Windows.Controls.TextBox> controles.</span><span class="sxs-lookup"><span data-stu-id="6d753-144">The details of each customer record are displayed in several <xref:System.Windows.Controls.TextBox> controls.</span></span>  
  
#### <a name="to-specify-data-bindings"></a><span data-ttu-id="6d753-145">Para especificar associações de dados</span><span class="sxs-lookup"><span data-stu-id="6d753-145">To specify data bindings</span></span>  
  
-   <span data-ttu-id="6d753-146">Copie o XAML a seguir para o <xref:System.Windows.Controls.Grid> declaração do elemento.</span><span class="sxs-lookup"><span data-stu-id="6d753-146">Copy the following XAML into the <xref:System.Windows.Controls.Grid> element's declaration.</span></span>  
  
     <span data-ttu-id="6d753-147">O <xref:System.Windows.Data.Binding> classe associa o <xref:System.Windows.Controls.TextBox> controles para os campos apropriados no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="6d753-147">The <xref:System.Windows.Data.Binding> class binds the <xref:System.Windows.Controls.TextBox> controls to the appropriate fields in the database.</span></span>  
  
     [!code-xaml[WPFWithWFAndDatabinding#6](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml#6)]  
  
## <a name="displaying-data-by-using-interoperation"></a><span data-ttu-id="6d753-148">Exibindo dados usando interoperação</span><span class="sxs-lookup"><span data-stu-id="6d753-148">Displaying Data by Using Interoperation</span></span>  
 <span data-ttu-id="6d753-149">Os pedidos correspondentes ao cliente selecionado são exibidos em uma <xref:System.Windows.Forms.DataGridView?displayProperty=nameWithType> controle chamado `dataGridView1`.</span><span class="sxs-lookup"><span data-stu-id="6d753-149">The orders corresponding to the selected customer are displayed in a <xref:System.Windows.Forms.DataGridView?displayProperty=nameWithType> control named `dataGridView1`.</span></span> <span data-ttu-id="6d753-150">O `dataGridView1` controle está associado à fonte de dados no arquivo code-behind.</span><span class="sxs-lookup"><span data-stu-id="6d753-150">The `dataGridView1` control is bound to the data source in the code-behind file.</span></span> <span data-ttu-id="6d753-151">Um <xref:System.Windows.Forms.Integration.WindowsFormsHost> controle é o pai desta [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] controle.</span><span class="sxs-lookup"><span data-stu-id="6d753-151">A <xref:System.Windows.Forms.Integration.WindowsFormsHost> control is the parent of this [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] control.</span></span>  
  
#### <a name="to-display-data-in-the-datagridview-control"></a><span data-ttu-id="6d753-152">Para exibir dados no controle DataGridView</span><span class="sxs-lookup"><span data-stu-id="6d753-152">To display data in the DataGridView control</span></span>  
  
-   <span data-ttu-id="6d753-153">Copie o XAML a seguir para o <xref:System.Windows.Controls.Grid> declaração do elemento.</span><span class="sxs-lookup"><span data-stu-id="6d753-153">Copy the following XAML into the <xref:System.Windows.Controls.Grid> element's declaration.</span></span>  
  
     [!code-xaml[WPFWithWFAndDatabinding#7](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml#7)]  
  
## <a name="adding-the-data-source-to-the-project"></a><span data-ttu-id="6d753-154">Adicionando a fonte de dados ao projeto</span><span class="sxs-lookup"><span data-stu-id="6d753-154">Adding the Data Source to the Project</span></span>  
 <span data-ttu-id="6d753-155">Com [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)], você pode facilmente adicionar uma fonte de dados ao seu projeto.</span><span class="sxs-lookup"><span data-stu-id="6d753-155">With [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)], you can easily add a data source to your project.</span></span> <span data-ttu-id="6d753-156">Este procedimento adiciona um conjunto de dados fortemente tipado ao seu projeto.</span><span class="sxs-lookup"><span data-stu-id="6d753-156">This procedure adds a strongly typed data set to your project.</span></span> <span data-ttu-id="6d753-157">Várias outras classes de suporte, como adaptadores de tabela para cada uma das tabelas escolhidas, também são adicionadas.</span><span class="sxs-lookup"><span data-stu-id="6d753-157">Several other support classes, such as table adapters for each of the chosen tables, are also added.</span></span>  
  
#### <a name="to-add-the-data-source"></a><span data-ttu-id="6d753-158">Para adicionar a fonte de dados</span><span class="sxs-lookup"><span data-stu-id="6d753-158">To add the data source</span></span>  
  
1.  <span data-ttu-id="6d753-159">Do **dados** menu, selecione **adicionar nova fonte de dados**.</span><span class="sxs-lookup"><span data-stu-id="6d753-159">From the **Data** menu, select **Add New Data Source**.</span></span>  
  
2.  <span data-ttu-id="6d753-160">No **Assistente de configuração de fonte de dados**, crie uma conexão ao banco de dados Northwind usando um conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="6d753-160">In the **Data Source Configuration Wizard**, create a connection to the Northwind database by using a dataset.</span></span> <span data-ttu-id="6d753-161">Para obter mais informações, consulte [como: conectar a dados em um banco de dados](http://msdn.microsoft.com/library/6c56e54e-8834-4297-85aa-cc1a443ba556).</span><span class="sxs-lookup"><span data-stu-id="6d753-161">For more information, see [How to: Connect to Data in a Database](http://msdn.microsoft.com/library/6c56e54e-8834-4297-85aa-cc1a443ba556).</span></span>  
  
3.  <span data-ttu-id="6d753-162">Quando for solicitado pelo **Assistente de configuração de fonte de dados**, salvar a cadeia de conexão como `NorthwindConnectionString`.</span><span class="sxs-lookup"><span data-stu-id="6d753-162">When you are prompted by the **Data Source Configuration Wizard**, save the connection string as `NorthwindConnectionString`.</span></span>  
  
4.  <span data-ttu-id="6d753-163">Quando você for solicitado a escolher seus objetos de banco de dados, selecione o `Customers` e `Orders` tabelas e o nome do conjunto de dados gerado `NorthwindDataSet`.</span><span class="sxs-lookup"><span data-stu-id="6d753-163">When you are prompted to choose your database objects, select the `Customers` and `Orders` tables, and name the generated data set `NorthwindDataSet`.</span></span>  
  
## <a name="binding-to-the-data-source"></a><span data-ttu-id="6d753-164">Criando uma associação à fonte de dados</span><span class="sxs-lookup"><span data-stu-id="6d753-164">Binding to the Data Source</span></span>  
 <span data-ttu-id="6d753-165">O <xref:System.Windows.Forms.BindingSource?displayProperty=nameWithType> componente fornece uma interface uniforme para a fonte de dados do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6d753-165">The <xref:System.Windows.Forms.BindingSource?displayProperty=nameWithType> component provides a uniform interface for the application's data source.</span></span> <span data-ttu-id="6d753-166">Associação à fonte de dados é implementada no arquivo code-behind.</span><span class="sxs-lookup"><span data-stu-id="6d753-166">Binding to the data source is implemented in the code-behind file.</span></span>  
  
#### <a name="to-bind-to-the-data-source"></a><span data-ttu-id="6d753-167">Para associar à fonte de dados</span><span class="sxs-lookup"><span data-stu-id="6d753-167">To bind to the data source</span></span>  
  
1.  <span data-ttu-id="6d753-168">Abra o arquivo code-behind, que se chama MainWindow.xaml.vb ou MainWindow.xaml.cs.</span><span class="sxs-lookup"><span data-stu-id="6d753-168">Open the code-behind file, which is named MainWindow.xaml.vb or MainWindow.xaml.cs.</span></span>  
  
2.  <span data-ttu-id="6d753-169">Copie o seguinte código para o `MainWindow` definição da classe.</span><span class="sxs-lookup"><span data-stu-id="6d753-169">Copy the following code into the `MainWindow` class definition.</span></span>  
  
     <span data-ttu-id="6d753-170">Esse código declara o <xref:System.Windows.Forms.BindingSource> componente e classes auxiliares associadas que se conectam ao banco de dados.</span><span class="sxs-lookup"><span data-stu-id="6d753-170">This code declares the <xref:System.Windows.Forms.BindingSource> component and associated helper classes that connect to the database.</span></span>  
  
     [!code-csharp[WPFWithWFAndDatabinding#11](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml.cs#11)]
     [!code-vb[WPFWithWFAndDatabinding#11](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFWithWFAndDatabinding/VisualBasic/WPFWithWFAndDatabinding/Window1.xaml.vb#11)]  
  
3.  <span data-ttu-id="6d753-171">Copie o seguinte código para o construtor.</span><span class="sxs-lookup"><span data-stu-id="6d753-171">Copy the following code into the constructor.</span></span>  
  
     <span data-ttu-id="6d753-172">Esse código cria e inicializa o <xref:System.Windows.Forms.BindingSource> componente.</span><span class="sxs-lookup"><span data-stu-id="6d753-172">This code creates and initializes the <xref:System.Windows.Forms.BindingSource> component.</span></span>  
  
     [!code-csharp[WPFWithWFAndDatabinding#12](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml.cs#12)]
     [!code-vb[WPFWithWFAndDatabinding#12](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFWithWFAndDatabinding/VisualBasic/WPFWithWFAndDatabinding/Window1.xaml.vb#12)]  
  
4.  <span data-ttu-id="6d753-173">Abra MainWindow.xaml.</span><span class="sxs-lookup"><span data-stu-id="6d753-173">Open MainWindow.xaml.</span></span>  
  
5.  <span data-ttu-id="6d753-174">No modo de Design ou modo de exibição XAML, selecione o <xref:System.Windows.Window> elemento.</span><span class="sxs-lookup"><span data-stu-id="6d753-174">In Design view or XAML view, select the <xref:System.Windows.Window> element.</span></span>  
  
6.  <span data-ttu-id="6d753-175">Na janela Propriedades, clique na guia **Eventos**.</span><span class="sxs-lookup"><span data-stu-id="6d753-175">In the Properties window, click the **Events** tab.</span></span>  
  
7.  <span data-ttu-id="6d753-176">Clique duas vezes o <xref:System.Windows.FrameworkElement.Loaded> evento.</span><span class="sxs-lookup"><span data-stu-id="6d753-176">Double-click the <xref:System.Windows.FrameworkElement.Loaded> event.</span></span>  
  
8.  <span data-ttu-id="6d753-177">Copie o seguinte código para o <xref:System.Windows.FrameworkElement.Loaded> manipulador de eventos.</span><span class="sxs-lookup"><span data-stu-id="6d753-177">Copy the following code into the <xref:System.Windows.FrameworkElement.Loaded> event handler.</span></span>  
  
     <span data-ttu-id="6d753-178">Esse código atribui o <xref:System.Windows.Forms.BindingSource> componente como o contexto de dados e preenche o `Customers` e `Orders` objetos de adaptador.</span><span class="sxs-lookup"><span data-stu-id="6d753-178">This code assigns the <xref:System.Windows.Forms.BindingSource> component as the data context and populates the `Customers` and `Orders` adapter objects.</span></span>  
  
     [!code-csharp[WPFWithWFAndDatabinding#13](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml.cs#13)]
     [!code-vb[WPFWithWFAndDatabinding#13](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFWithWFAndDatabinding/VisualBasic/WPFWithWFAndDatabinding/Window1.xaml.vb#13)]  
  
9. <span data-ttu-id="6d753-179">Copie o seguinte código para o `MainWindow` definição da classe.</span><span class="sxs-lookup"><span data-stu-id="6d753-179">Copy the following code into the `MainWindow` class definition.</span></span>  
  
     <span data-ttu-id="6d753-180">Este método trata o <xref:System.Windows.Data.CollectionView.CurrentChanged> eventos e atualiza o item atual da associação de dados.</span><span class="sxs-lookup"><span data-stu-id="6d753-180">This method handles the <xref:System.Windows.Data.CollectionView.CurrentChanged> event and updates the current item of the data binding.</span></span>  
  
     [!code-csharp[WPFWithWFAndDatabinding#14](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml.cs#14)]
     [!code-vb[WPFWithWFAndDatabinding#14](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFWithWFAndDatabinding/VisualBasic/WPFWithWFAndDatabinding/Window1.xaml.vb#14)]  
  
10. <span data-ttu-id="6d753-181">Pressione F5 para compilar e executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6d753-181">Press F5 to build and run the application.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="6d753-182">Consulte também</span><span class="sxs-lookup"><span data-stu-id="6d753-182">See Also</span></span>  
 <xref:System.Windows.Forms.Integration.ElementHost>  
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>  
 [<span data-ttu-id="6d753-183">Designer do WPF</span><span class="sxs-lookup"><span data-stu-id="6d753-183">WPF Designer</span></span>](http://msdn.microsoft.com/en-us/c6c65214-8411-4e16-b254-163ed4099c26)  
 [<span data-ttu-id="6d753-184">Associação de dados em um exemplo de aplicativos híbridos</span><span class="sxs-lookup"><span data-stu-id="6d753-184">Data Binding in Hybrid Applications Sample</span></span>](http://go.microsoft.com/fwlink/?LinkID=159983)  
 [<span data-ttu-id="6d753-185">Passo a passo: hospedando um controle composto do Windows Forms no WPF</span><span class="sxs-lookup"><span data-stu-id="6d753-185">Walkthrough: Hosting a Windows Forms Composite Control in WPF</span></span>](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)  
 [<span data-ttu-id="6d753-186">Passo a passo: hospedando um controle composto do WPF no Windows Forms</span><span class="sxs-lookup"><span data-stu-id="6d753-186">Walkthrough: Hosting a WPF Composite Control in Windows Forms</span></span>](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)