---
title: "Como permitir solicitações de metadados durante a autorização"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords: allowing metadata requests while authorizing [WCF]
ms.assetid: 90cec34f-b619-452b-a056-8b1c0de49d05
caps.latest.revision: "9"
author: Erikre
ms.author: erikre
manager: erikre
ms.openlocfilehash: 103aba5118810064c1cafb7c82634ef000ced667
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="how-to-allow-metadata-requests-while-authorizing"></a><span data-ttu-id="53918-102">Como permitir solicitações de metadados durante a autorização</span><span class="sxs-lookup"><span data-stu-id="53918-102">How To: Allow Metadata Requests While Authorizing</span></span>
<span data-ttu-id="53918-103">Durante a autorização personalizada, é necessário para permitir que uma solicitação de metadados a serem processadas.</span><span class="sxs-lookup"><span data-stu-id="53918-103">During custom authorization, it may be necessary to allow a request for metadata to be processed.</span></span> <span data-ttu-id="53918-104">O tópico a seguir apresenta as etapas para validar essa solicitação.</span><span class="sxs-lookup"><span data-stu-id="53918-104">The following topic walks through the steps to validate such a request.</span></span>  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]<span data-ttu-id="53918-105">[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] autorização, consulte [autorização](../../../../docs/framework/wcf/feature-details/authorization-in-wcf.md).</span><span class="sxs-lookup"><span data-stu-id="53918-105"> [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] authorization, see [Authorization](../../../../docs/framework/wcf/feature-details/authorization-in-wcf.md).</span></span>  
  
### <a name="to-allow-metadata-requests-during-authorization"></a><span data-ttu-id="53918-106">Para permitir solicitações de metadados durante a autorização</span><span class="sxs-lookup"><span data-stu-id="53918-106">To allow metadata requests during authorization</span></span>  
  
1.  <span data-ttu-id="53918-107">Criar uma extensão de <xref:System.ServiceModel.ServiceAuthorizationManager> classe.</span><span class="sxs-lookup"><span data-stu-id="53918-107">Create an extension of the <xref:System.ServiceModel.ServiceAuthorizationManager> class.</span></span>  
  
2.  <span data-ttu-id="53918-108">Substituir o método <xref:System.ServiceModel.ServiceAuthorizationManager.CheckAccessCore%2A>.</span><span class="sxs-lookup"><span data-stu-id="53918-108">Override the <xref:System.ServiceModel.ServiceAuthorizationManager.CheckAccessCore%2A> method.</span></span> <span data-ttu-id="53918-109">O método retorna `true` ou `false` dependendo se a autorização é permitida.</span><span class="sxs-lookup"><span data-stu-id="53918-109">The method returns `true` or `false` depending on whether authorization is allowed.</span></span> <span data-ttu-id="53918-110">Obter informações sobre o procedimento atual o <xref:System.ServiceModel.OperationContext> passado como um parâmetro para o método.</span><span class="sxs-lookup"><span data-stu-id="53918-110">Information about the current procedure is found in the <xref:System.ServiceModel.OperationContext> passed as a parameter to the method.</span></span>  
  
3.  <span data-ttu-id="53918-111">Em uma substituição, verifique o nome do contrato, namespace e a ação, conforme mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="53918-111">In the override, check the contract name, namespace, and the action as shown in the following example.</span></span> <span data-ttu-id="53918-112">Se as condições forem válidas, em seguida, retornar`true.`</span><span class="sxs-lookup"><span data-stu-id="53918-112">If the conditions are valid, then return `true.`</span></span>  
  
4.  <span data-ttu-id="53918-113">Use o ponto de extensibilidade para empregar a classe.</span><span class="sxs-lookup"><span data-stu-id="53918-113">Use the extensibility point to employ the class.</span></span> [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)]<span data-ttu-id="53918-114">[Como: criar um Gerenciador de autorização personalizada para um serviço](../../../../docs/framework/wcf/extending/how-to-create-a-custom-authorization-manager-for-a-service.md).</span><span class="sxs-lookup"><span data-stu-id="53918-114"> [How to: Create a Custom Authorization Manager for a Service](../../../../docs/framework/wcf/extending/how-to-create-a-custom-authorization-manager-for-a-service.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="53918-115">Exemplo</span><span class="sxs-lookup"><span data-stu-id="53918-115">Example</span></span>  
 <span data-ttu-id="53918-116">O exemplo a seguir mostra uma substituição do <xref:System.ServiceModel.ServiceAuthorizationManager.CheckAccessCore%2A> método.</span><span class="sxs-lookup"><span data-stu-id="53918-116">The following example shows an override of the <xref:System.ServiceModel.ServiceAuthorizationManager.CheckAccessCore%2A> method.</span></span>  
  
 [!code-csharp[C_HowtoCheckForMexRequestsInAuthorization#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtocheckformexrequestsinauthorization/cs/source.cs#1)]
 [!code-vb[C_HowtoCheckForMexRequestsInAuthorization#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtocheckformexrequestsinauthorization/vb/source.vb#1)]  
  
## <a name="see-also"></a><span data-ttu-id="53918-117">Consulte também</span><span class="sxs-lookup"><span data-stu-id="53918-117">See Also</span></span>  
 <xref:System.ServiceModel.ServiceAuthorizationManager>  
 [<span data-ttu-id="53918-118">Autorização</span><span class="sxs-lookup"><span data-stu-id="53918-118">Authorization</span></span>](../../../../docs/framework/wcf/feature-details/authorization-in-wcf.md)  
 [<span data-ttu-id="53918-119">Gerenciando reivindicações e autorização com o modelo de identidade</span><span class="sxs-lookup"><span data-stu-id="53918-119">Managing Claims and Authorization with the Identity Model</span></span>](../../../../docs/framework/wcf/feature-details/managing-claims-and-authorization-with-the-identity-model.md)