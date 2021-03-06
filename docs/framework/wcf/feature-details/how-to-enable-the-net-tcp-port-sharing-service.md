---
title: Como habilitar o serviço de compartilhamento de porta Net.TCP
ms.date: 03/30/2017
helpviewer_keywords:
- port sharing [WCF]
- activation services [WCF]
ms.assetid: c9175af4-c27c-4765-bf45-b8f7528a7282
ms.openlocfilehash: 4b5a18e11d9fc15f23b5353883a63d838face58a
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-enable-the-nettcp-port-sharing-service"></a>Como habilitar o serviço de compartilhamento de porta Net.TCP
Windows Communication Foundation (WCF) usa um serviço do Windows chamado o serviço de compartilhamento de porta NET. TCP para facilitar o compartilhamento de portas TCP entre vários processos. Esse serviço é instalado como parte do WCF, mas o serviço não está habilitado por padrão como uma precaução de segurança e portanto deve ser habilitado manualmente antes da primeira utilização. Este tópico descreve como configurar o serviço de compartilhamento de porta de TCP Net usando o snap-In do Console de gerenciamento Microsoft (MMC).  
  
 Depois de habilitar o serviço de compartilhamento de porta NET. TCP e iniciá-lo manualmente, consulte [como: configurar um serviço WCF para usar o compartilhamento de porta](../../../../docs/framework/wcf/feature-details/how-to-configure-a-wcf-service-to-use-port-sharing.md) para obter informações sobre como configurar seu serviço para usar este serviço.  
  
 Para obter um exemplo que usa o compartilhamento de porta net.tcp://, consulte o [exemplo de compartilhamento de porta NET. TCP](../../../../docs/framework/wcf/samples/net-tcp-port-sharing-sample.md).  
  
### <a name="to-enable-the-nettcp-port-sharing-service-using-mmc"></a>Para habilitar o usando o MMC Serviço de compartilhamento de porta de NET. TCP  
  
1.  No menu Iniciar, abra o Console de gerenciamento de serviços, abrindo uma janela de Prompt de comando e digitando `services.msc` ou abrindo executar e digitando `services.msc` na caixa Abrir.  
  
2.  No **nome** coluna da lista de serviços, clique com botão direito do **serviço de compartilhamento de porta NET. TCP**e selecione **propriedades** no menu.  
  
3.  Para habilitar a inicialização manual do serviço, no **propriedades** janela Selecionar o **geral** guia e no **tipo de inicialização** caixa de seleção Manual e, em seguida, clique em **Aplicar**.  
  
4.  Para iniciar o serviço, na área de status do serviço, clique o **iniciar** botão. O status do serviço agora deve exibir "Iniciado".  
  
5.  Para retornar à lista de serviços, clique o **Okey**e saia do Console do MMC.  
  
## <a name="example"></a>Exemplo  
  
## <a name="see-also"></a>Consulte também  
 [Compartilhamento de porta do NET.TCP](../../../../docs/framework/wcf/feature-details/net-tcp-port-sharing.md)  
 [Configurando o serviço de compartilhamento de porta NET.TCP](../../../../docs/framework/wcf/feature-details/configuring-the-net-tcp-port-sharing-service.md)
