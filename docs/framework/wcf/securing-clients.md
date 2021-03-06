---
title: Protegendo clientes
ms.date: 03/30/2017
helpviewer_keywords:
- clients [WCF], security considerations
ms.assetid: 44c8578c-9a5b-4acd-8168-1c30a027c4c5
author: BrucePerlerMS
manager: mbaldwin
ms.openlocfilehash: dfbe1fcce8a3b860e88dae4f5af43adfedbe9890
ms.sourcegitcommit: 15109844229ade1c6449f48f3834db1b26907824
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2018
---
# <a name="securing-clients"></a>Protegendo clientes
No Windows Communication Foundation (WCF), o serviço determina os requisitos de segurança para clientes. Ou seja, o serviço Especifica o modo de segurança para usar, e se o cliente deve fornecer uma credencial. O processo de proteção de um cliente, portanto, é simples: usar os metadados obtidos do serviço (se ela for publicada) e criar um cliente. Os metadados especificam como configurar o cliente. Se o serviço exigir que o cliente forneça uma credencial, você deve obter uma credencial que atende ao requisito. Este tópico descreve o processo em mais detalhes. Para obter mais informações sobre como criar um serviço seguro, consulte [protegendo serviços](../../../docs/framework/wcf/securing-services.md).  
  
## <a name="the-service-specifies-security"></a>O serviço Especifica a segurança  
 Por padrão, as associações do WCF têm recursos de segurança habilitados. (A exceção é o <xref:System.ServiceModel.BasicHttpBinding>.) Portanto, se o serviço foi criado usando o WCF, há uma possibilidade maior de implementar a segurança para garantir a integridade, confidencialidade e autenticação. Nesse caso, os metadados que de serviço fornece indicará requer para estabelecer um canal de comunicação seguro. Se os metadados de serviço não incluem quaisquer requisitos de segurança, não é possível impor um esquema de segurança, como o protocolo (SSL) sobre HTTP, em um serviço. Se, no entanto, o serviço exigir que o cliente forneça uma credencial, em seguida, o desenvolvedor do cliente, o implantador ou o administrador deve fornecer a credencial real que o cliente usará para se autenticar para o serviço.  
  
## <a name="obtaining-metadata"></a>Obtenção de metadados  
 Ao criar um cliente, a primeira etapa é obter os metadados para o serviço que o cliente se comunicará. Isso pode ser feito de duas maneiras. Primeiro, se o serviço publica um ponto de extremidade do exchange (MEX) de metadados ou disponibiliza seus metadados via HTTP ou HTTPS, você pode baixar os metadados usando o [Ferramenta Utilitária de metadados ServiceModel (Svcutil.exe)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md), que gera a ambos arquivos de código para um cliente, bem como um arquivo de configuração. (Para obter mais informações sobre como usar a ferramenta, consulte [Acessando serviços usando um cliente WCF](../../../docs/framework/wcf/accessing-services-using-a-wcf-client.md).) Se o serviço não publicar um ponto de extremidade MEX e também não disponibilizar seus metadados via HTTP ou HTTPS, você deve entrar em contato com o criador do serviço para obter a documentação que descreve os requisitos de segurança e os metadados.  
  
> [!IMPORTANT]
>  É recomendável que os metadados são provenientes de uma fonte confiável e se ele não ser violado. Metadados recuperados usando o protocolo HTTP é enviado em texto não criptografado e podem ser violados. Se o serviço usa o <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetEnabled%2A> e <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetUrl%2A> propriedades, use a URL que o criador do serviço fornecido para baixar os dados usando o protocolo HTTPS.  
  
## <a name="validating-security"></a>Validação de segurança  
 Fontes de metadados podem ser divididos em duas amplas categorias: confiar fontes e fontes não confiáveis. Se uma fonte confiável e ter baixado o código do cliente e outros metadados do ponto de extremidade MEX segura da fonte que, em seguida, você pode criar o cliente, fornecê-lo com as credenciais corretas e executá-lo com nenhum outras preocupações.  
  
 No entanto, se você optar por fazer o download de um cliente e os metadados de uma fonte que sabem muito sobre, certifique-se de validar as medidas de segurança que usa o código. Por exemplo, você deve não simplesmente criar um cliente que envia suas informações pessoais ou financeiras para um serviço, a menos que o serviço demandas confidencialidade e integridade (pelo menos). Você deve confiar o proprietário do serviço na medida em que você está disposto a divulgar essas informações porque essas informações estarão visíveis para ele.  
  
 Como regra, portanto, ao usar o código e os metadados de uma fonte não confiável, verifique o código e os metadados para garantir que ele atenda o nível de segurança que você precisa.  
  
## <a name="setting-a-client-credential"></a>Definir uma credencial de cliente  
 Definir uma credencial de cliente em um cliente consiste em duas etapas:  
  
1.  Determinar a *tipo de credencial de cliente* requer que o serviço. Isso é feito por um dos dois métodos. Primeiro, se você tiver a documentação do criador do serviço, ela deve especificar a credencial do cliente requer que o serviço do tipo (se houver). Em segundo lugar, se você tiver apenas um arquivo de configuração gerado pela ferramenta Svcutil.exe, você pode examinar as associações individuais para determinar que tipo de credencial é necessária.  
  
2.  Especifique uma credencial de cliente real. A credencial de cliente real é chamada um *valor de credencial de cliente* para distingui-lo do tipo. Por exemplo, se o tipo de credencial de cliente especifica um certificado, você deve fornecer um certificado x. 509 que é emitido por uma autoridade de certificação, o serviço de relações de confiança.  
  
### <a name="determining-the-client-credential-type"></a>Determinando o tipo de credencial de cliente  
 Se você tiver a configuração do arquivo a ferramenta Svcutil.exe gerada, examine o [ \<associações >](../../../docs/framework/configure-apps/file-schema/wcf/bindings.md) seção para determinar que tipo de credencial de cliente é necessário. Na seção são elementos de associação que especifica os requisitos de segurança. Especificamente, examine o \<segurança > elemento de cada associação. Esse elemento inclui o `mode` atributo, que pode ser definido como um dos três valores possíveis (`Message`, `Transport`, ou `TransportWithMessageCredential`). O valor do atributo determina o modo e o modo determina qual dos elementos filho é significativa.  
  
 O `<security>` elemento poderá conter um `<transport>` ou `<message>` elemento, ou ambos. O elemento significativo é aquela que corresponda ao modo de segurança. Por exemplo, o código a seguir especifica que o modo de segurança é `"Message"`e o cliente de credencial de tipo para o `<message>` elemento é `"Certificate"`. Nesse caso, o `<transport>` elemento pode ser ignorado. No entanto, o `<message>` elemento Especifica que um certificado x. 509 deve ser fornecido.  
  
```xml  
<wsHttpBinding>  
    <binding name="WSHttpBinding_ICalculator">  
       <security mode="Message">  
           <transport clientCredentialType="Windows"   
                      realm="" />  
           <message clientCredentialType="Certificate"   
                    negotiateServiceCredential="true"  
                    algorithmSuite="Default"   
                    establishSecurityContext="true" />  
       </security>  
    </binding>  
</wsHttpBinding>  
```  
  
 Observe que, se o `clientCredentialType` atributo é definido como `"Windows"`, conforme mostrado no exemplo a seguir, você não precisa fornecer um valor de credencial real. Isso ocorre porque a segurança integrada do Windows fornece a credencial real (um token Kerberos) da pessoa que está executando o cliente.  
  
```xml  
<security mode="Message">  
    <transport clientCredentialType="Windows "   
        realm="" />  
</security>  
```  
  
### <a name="setting-the-client-credential-value"></a>Definir o valor de credencial de cliente  
 Se for determinado que o cliente deve fornecer uma credencial, use o método apropriado para configurar o cliente. Por exemplo, para definir um certificado de cliente, use o <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential.SetCertificate%2A> método.  
  
 Uma forma comum de credencial é o certificado x. 509. Você pode fornecer a credencial de duas maneiras:  
  
-   Por programação-la no código do cliente (usando o `SetCertificate` método).  
  
 Adicionando um [ \<comportamentos >](../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md) seção do arquivo de configuração para o cliente e usar o `clientCredentials` elemento (mostrado abaixo).  
  
#### <a name="setting-a-clientcredentials-value-in-code"></a>Definindo um \<clientCredentials > valor no código  
 Para definir um [ \<clientCredentials >](../../../docs/framework/configure-apps/file-schema/wcf/clientcredentials.md) valor no código, você deve acessar o <xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A> propriedade o <xref:System.ServiceModel.ClientBase%601> classe. A propriedade retorna um <xref:System.ServiceModel.Description.ClientCredentials> objeto que permite o acesso a vários tipos de credencial, conforme mostrado na tabela a seguir.  
  
|Propriedade ClientCredential|Descrição|Observações|  
|-------------------------------|-----------------|-----------|  
|<xref:System.ServiceModel.Description.ClientCredentials.ClientCertificate%2A>|Retorna um <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential>|Representa um certificado x. 509 fornecido pelo cliente para se autenticar para o serviço.|  
|<xref:System.ServiceModel.Description.ClientCredentials.HttpDigest%2A>|Retorna um <xref:System.ServiceModel.Security.HttpDigestClientCredential>|Representa uma credencial de digest HTTP. A credencial é um hash do nome de usuário e senha.|  
|<xref:System.ServiceModel.Description.ClientCredentials.IssuedToken%2A>|Retorna um <xref:System.ServiceModel.Security.IssuedTokenClientCredential>|Representa um token de segurança personalizada emitido por um serviço de Token de segurança, geralmente usados em cenários de Federação.|  
|<xref:System.ServiceModel.Description.ClientCredentials.Peer%2A>|Retorna um <xref:System.ServiceModel.Security.PeerCredential>|Representa uma credencial de ponto a ponto para participação em uma malha de pontos em um domínio do Windows.|  
|<xref:System.ServiceModel.Description.ClientCredentials.ServiceCertificate%2A>|Retorna um <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential>|Representa um certificado x. 509 fornecido pelo serviço em uma negociação de fora da banda.|  
|<xref:System.ServiceModel.Description.ClientCredentials.UserName%2A>|Retorna um <xref:System.ServiceModel.Security.UserNamePasswordClientCredential>|Representa um par de nome e a senha do usuário.|  
|<xref:System.ServiceModel.Description.ClientCredentials.Windows%2A>|Retorna um <xref:System.ServiceModel.Security.WindowsClientCredential>|Representa uma credencial de cliente do Windows (uma credencial Kerberos). As propriedades da classe são somente leitura.|  
  
#### <a name="setting-a-clientcredentials-value-in-configuration"></a>Definindo um \<clientCredentials > valor na configuração  
 Valores de credenciais são especificados por meio de um comportamento de ponto de extremidade como elementos filho de [ \<clientCredentials >](../../../docs/framework/configure-apps/file-schema/wcf/clientcredentials.md) elemento. O elemento usado depende do tipo de credencial de cliente. Por exemplo, o exemplo a seguir mostra a configuração para definir um certificado x. 509 usando o <[\<clientCertificate >](../../../docs/framework/configure-apps/file-schema/wcf/clientcertificate-of-clientcredentials-element.md).  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <endpointBehaviors>  
        <behavior name="myEndpointBehavior">  
          <clientCredentials>  
            <clientCertificate findvalue="myMachineName"   
            storeLocation="Current" X509FindType="FindBySubjectName" />  
          </clientCredentials>  
        </behavior>              
    </behaviors>  
  </system.serviceModel>  
</configuration>  
```  
  
 Para definir a credencial do cliente em configuração, adicione uma [ \<endpointBehaviors >](../../../docs/framework/configure-apps/file-schema/wcf/endpointbehaviors.md) elemento ao arquivo de configuração. Além disso, o elemento de comportamento adicional deve ser vinculado ao ponto de extremidade do serviço usando o `behaviorConfiguration` atributo o [ \<ponto de extremidade >](http://msdn.microsoft.com/library/13aa23b7-2f08-4add-8dbf-a99f8127c017) elemento conforme mostrado no exemplo a seguir. O valor de `behaviorConfiguration` atributo deve corresponder ao valor do comportamento `name` atributo.  
  
 `<configuration>`  
  
 `<system.serviceModel>`  
  
 `<client>`  
  
 `<endpoint address="http://localhost/servicemodelsamples/service.svc"`  
  
 `binding="wsHttpBinding"`  
  
 `bindingConfiguration="Binding1"`  
  
 `behaviorConfiguration="myEndpointBehavior"`  
  
 `contract="Microsoft.ServiceModel.Samples.ICalculator" />`  
  
 `</client>`  
  
 `</system.serviceModel>`  
  
 `</configuration>`  
  
> [!NOTE]
>  Alguns dos valores de credencial de cliente não podem ser definido usando arquivos de configuração do aplicativo, por exemplo, nome de usuário e senha, ou usuário do Windows e valores de senha. Esses valores de credencial podem ser especificados somente no código.  
  
 Para obter mais informações sobre como configurar a credencial do cliente, consulte [como: especificar valores de credencial de cliente](../../../docs/framework/wcf/how-to-specify-client-credential-values.md).  
  
> [!NOTE]
>  `ClientCredentialType` é ignorado quando `SecurityMode` é definido como `"TransportWithMessageCredential",` conforme mostrado no exemplo de configuração.  
  
```xml  
<wsHttpBinding>  
    <binding name="PingBinding">  
        <security mode="TransportWithMessageCredential"  >  
           <message  clientCredentialType="UserName"   
               establishSecurityContext="false"    
               negotiateServiceCredential="false" />  
           <transport clientCredentialType="Certificate"  />  
         </security>  
    </binding>  
</wsHttpBinding>  
```  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A>  
 <xref:System.ServiceModel.ClientBase%601>  
 <xref:System.ServiceModel.Description.ClientCredentials>  
 <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetEnabled%2A>  
 <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetUrl%2A>  
 [\<associações >](../../../docs/framework/configure-apps/file-schema/wcf/bindings.md)  
 [Ferramenta Editor de configuração (SvcConfigEditor.exe)](../../../docs/framework/wcf/configuration-editor-tool-svcconfigeditor-exe.md)  
 [Protegendo serviços](../../../docs/framework/wcf/securing-services.md)  
 [Usando um cliente do WCF para acessar serviços](../../../docs/framework/wcf/accessing-services-using-a-wcf-client.md)  
 [Como especificar valores de credenciais do cliente](../../../docs/framework/wcf/how-to-specify-client-credential-values.md)  
 [Ferramenta de utilitário de metadados ServiceModel (Svcutil.exe)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)  
 [Como especificar o tipo de credencial do cliente](../../../docs/framework/wcf/how-to-specify-the-client-credential-type.md)
