---
title: "Configurando a serialização em um serviço de fluxo de trabalho"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: aa70b290-a2ee-4c3c-90ea-d0a7665096ae
caps.latest.revision: "4"
author: Erikre
ms.author: erikre
manager: erikre
ms.openlocfilehash: 9aa50b8e9f29e5dd14f0ff18d253943a73ef3a0b
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/18/2017
---
# <a name="configuring-serialization-in-a-workflow-service"></a>Configurando a serialização em um serviço de fluxo de trabalho
Serviços de fluxo de trabalho são [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] serviços e, portanto, ter a opção de usar qualquer um de <xref:System.Runtime.Serialization.DataContractSerializer> (o padrão) ou o <xref:System.Xml.Serialization.XmlSerializer>. Quando o tipo de serializador a ser usado de serviços gravar o fluxo de trabalho não é especificado no contrato de serviço ou operação. Ao criar [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] serviços de fluxo de trabalho, você não especificar esses contratos em código, mas em vez disso, eles são gerados em tempo de execução por inferência de contrato. [!INCLUDE[crabout](../../../../includes/crabout-md.md)]inferência de tipos de contrato, consulte [usando contratos no fluxo de trabalho](../../../../docs/framework/wcf/feature-details/using-contracts-in-workflow.md).  O serializador é especificado usando o <xref:System.ServiceModel.Activities.Receive.SerializerOption%2A> propriedade. Isso pode ser definido no designer como mostrado na ilustração a seguir.  
  
 ![Definindo o serializador](../../../../docs/framework/wcf/feature-details/media/settingserialzier.png "SettingSerialzier")  
  
 O serializador também pode ser definido no código conforme mostrado no exemplo a seguir,  
  
```  
Receive approveExpense = new Receive  
            {  
                OperationName = "ApproveExpense",  
                CanCreateInstance = true,  
                ServiceContractName = "FinanceService",  
                SerializerOption = SerializerOption.DataContractSerializer,  
                Content = ReceiveContent.Create(new OutArgument<Expense>(expense))  
            };  
```  
  
 Tipos conhecidos podem ser especificados em serviços de fluxo de trabalho. [!INCLUDE[crabout](../../../../includes/crabout-md.md)]Conhecido Consulte tipos [tipos conhecidos de contrato de dados](../../../../docs/framework/wcf/feature-details/data-contract-known-types.md). Tipos conhecidos podem ser especificados no designer ou no código. Para especificar os tipos conhecidos no designer, clique no botão de reticências ao lado da propriedade KnownTypes na janela Propriedades para um <xref:System.ServiceModel.Activities.Receive> atividade conforme mostrado na ilustração a seguir.  
  
 ![Propriedade KnownTypes](../../../../docs/framework/wcf/feature-details/media/knowntypes.png "KnownTypes")  
  
 Isso exibirá o Editor de coleções de tipo que permite pesquisar e especifique tipos conhecidos.  
  
 ![Adicionando tipos conhecidos](../../../../docs/framework/wcf/feature-details/media/typecollectionseditor.gif "TypeCollectionsEditor")  
  
 Clique o **adicionar novo tipo** link e use a lista suspensa para selecionar ou pesquisar um tipo para adicionar à coleção de tipos conhecidos. Para especificar os tipos conhecidos em uso do código de <xref:System.ServiceModel.Activities.Receive.KnownTypes%2A> propriedade conforme mostrado no exemplo a seguir.  
  
```  
Receive approveExpense = new Receive  
            {  
                OperationName = "ApproveExpense",  
                CanCreateInstance = true,  
                ServiceContractName = "FinanceService",  
                SerializerOption = SerializerOption.DataContractSerializer,  
                Content = ReceiveContent.Create(new OutArgument<Expense>(expense))  
            };  
            approveExpense.KnownTypes.Add(typeof(Travel));  
            approveExpense.KnownTypes.Add(typeof(Meal));  
```  
  
 Para ver um exemplo de código completo que mostra como configurar a serialização de um serviço de fluxo de trabalho consulte [mensagens de formatação em serviços de fluxo de trabalho](../../../../docs/framework/windows-workflow-foundation/samples/formatting-messages-in-workflow-services.md).