---
title: '&lt;bufferReceive&gt;'
ms.date: 03/30/2017
ms.topic: reference
ms.assetid: b23c3a54-10d4-4f13-ab6d-98b26b76f22a
ms.openlocfilehash: 07d5b66b14d9495808f972734cdce4476efaefde
ms.sourcegitcommit: 11f11ca6cefe555972b3a5c99729d1a7523d8f50
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="ltbufferreceivegt"></a>&lt;bufferReceive&gt;
Um comportamento de serviço que permite que um serviço a ser usado em buffer recebe o processamento, que permite que um serviço de fluxo de trabalho processar mensagens de fora de ordem.  
  
\<system.ServiceModel>  
\<comportamentos >  
\<serviceBehaviors >  
\<comportamento >  
\<bufferReceive >  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<behaviors>
  <serviceBehaviors>
    <behavior name="String">
      <bufferReceive maxPendingMessagesPerChannel="Integer" />
    </behavior>
  </serviceBehaviors>
</behaviors>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|maxPendingMessagesPerChannel|Um inteiro que especifica o número máximo de mensagens permitido para cada canal pendentes. O valor padrão é 512. Essa propriedade limita o número de mensagens de fora de ordem que pode ser recebido por um serviço de fluxo de trabalho.|  
  
### <a name="child-elements"></a>Elementos filho  
 nenhuma.  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<comportamento > de \<serviceBehaviors >](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/behavior-of-servicebehaviors-of-workflow.md)|Especifica um elemento de comportamento.|  
  
## <a name="see-also"></a>Consulte também  
<!-- <xref:System.ServiceModel.Activities.Description.BufferReceiveServiceBehavior>  -->
 <xref:System.ServiceModel.Activities.Configuration.BufferedReceiveElement>
