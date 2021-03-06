---
title: Exemplo de anúncios
ms.date: 03/30/2017
ms.assetid: 954a75e4-9a97-41d6-94fc-43765d4205a9
ms.openlocfilehash: ee58a2fef970fa3e7936e2fc26a9e7fd31633347
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="announcements-sample"></a>Exemplo de anúncios
Este exemplo mostra como usar a funcionalidade de lançamento do recurso de descoberta. Anúncios de permitir que os serviços enviar mensagens de aviso que contém metadados sobre o serviço. Por padrão, um anúncio de saudação é enviado quando o serviço é iniciado e um anúncio bye é enviado quando o serviço foi desligado. Esses anúncios podem ser multicast ou eles podem ser enviados ponto a ponto. Este exemplo consiste de cliente e o serviço de dois projetos.  
  
## <a name="service"></a>Serviço  
 Este projeto contém um serviço auto-hospedado Calculadora. No `Main` método, um host de serviço é criado e um ponto de extremidade de serviço é adicionado a ele. Em seguida, um <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior> é criado. Para habilitar os avisos, um ponto de extremidade de anúncio deve ser adicionado para o <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior>. Nesse caso, um ponto de extremidade padrão, usando UDP multicast é adicionado como o ponto de extremidade de anúncio. Isso transmite os anúncios sobre um endereço conhecido do UDP.  
  
```  
Uri baseAddress = new Uri("http://localhost:8000/" + Guid.NewGuid().ToString());  
  
// Create a ServiceHost for the CalculatorService type.  
using (ServiceHost serviceHost = new ServiceHost(typeof(CalculatorService), baseAddress))  
{  
     serviceHost.AddServiceEndpoint(typeof(ICalculatorService), new WSHttpBinding(), String.Empty);  
  
     ServiceDiscoveryBehavior serviceDiscoveryBehavior = new ServiceDiscoveryBehavior();  
  
     // Announce the availability of the service over UDP multicast  
    serviceDiscoveryBehavior.AnnouncementEndpoints.Add(new UdpAnnouncementEndpoint());  
  
    // Make the service discoverable over UDP multicast.  
    serviceHost.Description.Behaviors.Add(serviceDiscoveryBehavior);                  
    serviceHost.AddServiceEndpoint(new UdpDiscoveryEndpoint());  
    serviceHost.Open();  
    // ...  
}  
```  
  
## <a name="client"></a>Cliente  
 Neste projeto, observe que os hosts de cliente um <xref:System.ServiceModel.Discovery.AnnouncementService>. Além disso, os dois delegados são registrados com eventos. Esses eventos determinam o que o cliente faz quando anúncios online e offline são recebidos.  
  
```  
// Create an AnnouncementService instance  
AnnouncementService announcementService = new AnnouncementService();  
  
// Subscribe the announcement events  
announcementService.OnlineAnnouncementReceived += OnOnlineEvent;  
announcementService.OfflineAnnouncementReceived += OnOfflineEvent;  
```  
  
 O `OnOnlineEvent` e `OnOfflineEvent` métodos controlam as mensagens de aviso hello e bye respectivamente.  
  
```  
static void OnOnlineEvent(object sender, AnnouncementEventArgs e)  
{  
    Console.WriteLine();              
    Console.WriteLine("Received an online announcement from {0}:", e.AnnouncementMessage.EndpointDiscoveryMetadata.Address);  
PrintEndpointDiscoveryMetadata(e.AnnouncementMessage.EndpointDiscoveryMetadata);  
}  
  
static void OnOfflineEvent(object sender, AnnouncementEventArgs e)  
{  
    Console.WriteLine();  
    Console.WriteLine("Received an offline announcement from {0}:", e.AnnouncementMessage.EndpointDiscoveryMetadata.Address);  
            PrintEndpointDiscoveryMetadata(e.AnnouncementMessage.EndpointDiscoveryMetadata);  
}  
```  
  
#### <a name="to-use-this-sample"></a>Para usar este exemplo  
  
1.  Este exemplo usa pontos de extremidade HTTP e executar este exemplo, adequado ACLs de URL deve ser adicionados consulte [Configurando HTTP e HTTPS](http://go.microsoft.com/fwlink/?LinkId=70353) para obter detalhes. Executando o seguinte comando em um privilégio elevado deve adicionar as ACLs corretas. Convém substituir seu domínio e nome de usuário para os argumentos a seguir se o comando não funcionar como está. `netsh http add urlacl url=http://+:8000/ user=%DOMAIN%\%UserName%`  
  
2.  Compile a solução.  
  
3.  Execute o aplicativo client.exe.  
  
4.  Execute o aplicativo service.exe. Observe que o cliente recebe um anúncio online.  
  
5.  Feche o aplicativo service.exe. Observe que o cliente recebe um aviso offline.  
  
> [!IMPORTANT]
>  Os exemplos podem já estar instalados no seu computador. Verifique o seguinte diretório (padrão) antes de continuar.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Se este diretório não existir, vá para [Windows Communication Foundation (WCF) e exemplos do Windows Workflow Foundation (WF) para o .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) para baixar todos os Windows Communication Foundation (WCF) e [!INCLUDE[wf1](../../../../includes/wf1-md.md)] exemplos. Este exemplo está localizado no seguinte diretório.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Discovery\Announcements`  
  
## <a name="see-also"></a>Consulte também
