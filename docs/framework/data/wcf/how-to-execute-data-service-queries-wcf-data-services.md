---
title: Como executar consultas do serviço de dados (WCF Data Services)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- querying the data service [WCF Data Services]
- WCF Data Services, querying
- WCF Data Services, accessing data
ms.assetid: 62997821-e0c6-4c4d-9fb7-1273fb5e5d18
ms.openlocfilehash: 574818c694b07775c4263dca066e0d2e462be27f
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-execute-data-service-queries-wcf-data-services"></a>Como executar consultas do serviço de dados (WCF Data Services)
O [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] permite consultar um serviço de dados de um aplicativo cliente baseado em .NET Framework usando as classes de serviço de dados do cliente geradas. Você pode executar consultas usando um desses métodos:  
  
-   Executando uma consulta LINQ no <xref:System.Data.Services.Client.DataServiceQuery%601> nomeado que você obtém de <xref:System.Data.Services.Client.DataServiceContext> que a ferramenta `Add Data Service Reference` produz.  
  
-   Implicitamente, enumerando um <xref:System.Data.Services.Client.DataServiceQuery%601> nomeado que você obtém de <xref:System.Data.Services.Client.DataServiceContext> que a ferramenta `Add Data Service Reference` produz.  
  
-   Explicitamente, chamando o método <xref:System.Data.Services.Client.DataServiceContext.Execute%2A> em <xref:System.Data.Services.Client.DataServiceQuery%601> ou <xref:System.Data.Services.Client.DataServiceQuery%601.BeginExecute%2A> para a execução assíncrona.  
  
 Para obter mais informações, consulte [consultando o Data Service](../../../../docs/framework/data/wcf/querying-the-data-service-wcf-data-services.md).  
  
 O exemplo deste tópico usa o serviço de dados de exemplo Northwind e as classes de serviço de dados do cliente geradas automaticamente. Esse serviço e as classes de dados do cliente são criadas quando você concluir o [WCF Data Services quickstart](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como definir e executar uma consulta LINQ que retorna todos os `Customers` no serviço de dados Northwind.  
  
 [!code-csharp[Astoria Northwind Client#GetAllCustomersLinq](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#getallcustomerslinq)]
 [!code-vb[Astoria Northwind Client#GetAllCustomersLinq](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#getallcustomerslinq)]  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como usar o contexto que a ferramenta `Add Data Service Reference` gera para implicitamente executar uma consulta que retorna todos os `Customers` no serviço de dados Northwind. O URI do conjunto de entidades de `Customers` é determinado automaticamente pelo contexto. A consulta é executada implicitamente quando a enumeração ocorre.  
  
 [!code-csharp[Astoria Northwind Client#GetAllCustomers](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#getallcustomers)]
 [!code-vb[Astoria Northwind Client#GetAllCustomers](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#getallcustomers)]  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como usar o <xref:System.Data.Services.Client.DataServiceContext> para explicitamente executar uma consulta que retorna todos os `Customers` no serviço de dados Northwind.  
  
 [!code-csharp[Astoria Northwind Client#GetAllCustomersExplicit](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#getallcustomersexplicit)]
 [!code-vb[Astoria Northwind Client#GetAllCustomersExplicit](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#getallcustomersexplicit)]  
  
## <a name="see-also"></a>Consulte também  
 [Como adicionar opções de consulta para uma consulta de serviço de dados](../../../../docs/framework/data/wcf/how-to-add-query-options-to-a-data-service-query-wcf-data-services.md)
