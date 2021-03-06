---
title: '&lt;autenticação&gt; de elemento &lt;clientCertificate&gt;'
ms.date: 03/30/2017
ms.assetid: 4a55eea2-1826-4026-b911-b7cc9e9c8bfe
ms.openlocfilehash: ccc184f63428fd4a12b9047c0bcf4416e87f24d2
ms.sourcegitcommit: 11f11ca6cefe555972b3a5c99729d1a7523d8f50
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="ltauthenticationgt-of-ltclientcertificategt-element"></a>&lt;autenticação&gt; de elemento &lt;clientCertificate&gt;
Especifica os comportamentos de autenticação para certificados de cliente usados por um serviço.  
  
 \<system.ServiceModel>  
\<comportamentos >  
\<serviceBehaviors >  
\<comportamento >  
\<serviceCredentials>  
\<clientCertificate >  
\<autenticação >  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<authentication  
customCertificateValidatorType="namespace.typeName, [,AssemblyName] [,Version=version number] [,Culture=culture] [,PublicKeyToken=token]"  
certificateValidationMode="ChainTrust/None/PeerTrust/PeerOrChainTrust/Custom"  
includeWindowsGroups="Boolean"  
mapClientCertificateToWindowsAccount="Boolean"  
revocationMode="NoCheck/Online/Offline"  
trustedStoreLocation="CurrentUser/LocalMachine"   
/>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem os elementos pai de atributos e elementos filho  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|customCertificateValidatorType|Cadeia de caracteres opcional. Um tipo e assembly usados para validar um tipo personalizado. Esse atributo deve ser definido quando `certificateValidationMode` é definido como `Custom`.|  
|certificateValidationMode|Enumeração opcional. Especifica um dos modos usados para validar credenciais. Esse atributo é do <xref:System.ServiceModel.Security.X509CertificateValidationMode> tipo. Se definido como <xref:System.ServiceModel.Security.X509CertificateValidationMode.Custom?displayProperty=nameWithType>, em seguida, um `customCertificateValidator` também deve ser fornecido. O padrão é <xref:System.ServiceModel.Security.X509CertificateValidationMode.ChainTrust?displayProperty=nameWithType>.|  
|includeWindowsGroups|Booleano opcional. Especifica se os grupos do Windows são incluídos no contexto de segurança. A configuração desse atributo `true` tem um impacto no desempenho, já que resulta em uma expansão de grupo completo. Defina este atributo como `false` se você não precisa estabelecer a lista de grupos de um usuário pertence.|  
|mapClientCertificateToWindowsAcccount|Booliano. Especifica se o cliente pode ser mapeado para uma identidade do Windows usando o certificado. Active Directory deve ser habilitado para fazer isso.|  
|revocationMode|Enumeração opcional. Um dos modos usados para verificar por listas de certificados revogados (RCL). O padrão é `Online`. Esse valor é ignorado ao usar a segurança de transporte HTTP.|  
|trustedStoreLocation|Enumeração opcional. Um dos locais de armazenamento de sistema de dois: `LocalMachine` ou `CurrentUser`. Esse valor é usado quando um certificado de serviço é negociado ao cliente. A validação é executada em relação a **pessoas confiáveis** armazenar no local de armazenamento especificado. O padrão é `CurrentUser`.|  
  
## <a name="customcertificatevalidatortype-attribute"></a>customCertificateValidatorType atributo  
  
|Valor|Descrição|  
|-----------|-----------------|  
|Cadeia de Caracteres|Especifica o nome do tipo e assembly e outros dados usados para localizar o tipo.|  
  
## <a name="certificatevalidationmode-attribute"></a>certificateValidationMode atributo  
  
|Valor|Descrição|  
|-----------|-----------------|  
|Enumeração|Um dos seguintes valores: None, PeerTrust, ChainTrust, PeerOrChainTrust, personalizado.<br /><br /> Para obter mais informações, consulte [trabalhar com certificados](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md).|  
  
## <a name="revocationmode-attribute"></a>revocationMode atributo  
  
|Valor|Descrição|  
|-----------|-----------------|  
|Enumeração|Um dos seguintes valores: NoCheck, Online, Offline. Para obter mais informações, consulte [trabalhar com certificados](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md).|  
  
## <a name="trustedstorelocation-attribute"></a>trustedStoreLocation atributo  
  
|Valor|Descrição|  
|-----------|-----------------|  
|Enumeração|Um dos seguintes valores: `LocalMachine` ou `CurrentUser`. O padrão é `CurrentUser`. Se o aplicativo cliente é executado sob uma conta de sistema, o certificado é geralmente em `LocalMachine`. Se o aplicativo cliente é executado sob uma conta de usuário, o certificado é geralmente em `CurrentUser`.|  
  
### <a name="child-elements"></a>Elementos filho  
 nenhuma.  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<clientCertificate >](../../../../../docs/framework/configure-apps/file-schema/wcf/clientcertificate-of-servicecredentials.md)|Define um certificado x. 509 usado para autenticar um cliente para um serviço.|  
  
## <a name="remarks"></a>Comentários  
 O `<authentication>` elemento corresponde à <xref:System.ServiceModel.Security.X509ClientCertificateAuthentication> classe. Ele permite que você personalize como os clientes são autenticados. Você pode definir o `certificateValidationMode` atributo `None`, `ChainTrust`, `PeerOrChainTrust`, `PeerTrust`, ou `Custom`. Por padrão, o nível é definido como `ChainTrust`, que especifica que cada certificado deve ser encontrado em uma hierarquia de certificados terminam em um *autoridade raiz* na parte superior da cadeia. Este é o modo mais seguro. Você também pode definir o valor `PeerOrChainTrust`, que especifica que os certificados emitidos por conta própria (confiança ponto a ponto) são aceitos, bem como certificados que estão em uma cadeia confiável. Esse valor é usado durante o desenvolvimento e depuração clientes e serviços, pois os certificados emitidos por conta própria não precisam ser adquiridos de uma autoridade confiável. Ao implantar um cliente, use o `ChainTrust` valor em vez disso.  
  
 Você também pode definir o valor `Custom`. Quando definido como o `Custom` valor, você também deve definir o `customCertificateValidatorType` de atributo para um assembly e o tipo usado para validar o certificado. Para criar seu próprios validador personalizado, você deve herdar de abstrata <xref:System.IdentityModel.Selectors.X509CertificateValidator> classe. Para obter mais informações, consulte [como: criar um serviço que utiliza um validador de certificado personalizado](../../../../../docs/framework/wcf/extending/how-to-create-a-service-that-employs-a-custom-certificate-validator.md).  
  
## <a name="example"></a>Exemplo  
 O código a seguir especifica um certificado x. 509 e um tipo de validação personalizada no `<authentication>` elemento.  
  
```xml  
<serviceBehaviors>  
 <behavior name="myServiceBehavior">  
  <clientCertificate>  
   <certificate   
         findValue="www.cohowinery.com"   
         storeLocation="CurrentUser"   
         storeName="TrustedPeople"  
         x509FindType="FindByIssuerName" />  
   <authentication customCertificateValidatorType="MyTypes.Coho"  
    certificateValidationMode="Custom"   
    revocationMode="Offline"  
    includeWindowsGroups="false"   
    mapClientCertificateToWindowsAccount="true" />  
  </clientCertificate>  
 </behavior>  
</serviceBehaviors>  
```  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.ServiceModel.Security.X509ClientCertificateAuthentication>  
 <xref:System.ServiceModel.Security.X509CertificateValidationMode>  
 <xref:System.ServiceModel.Security.X509CertificateInitiatorServiceCredential.Authentication%2A>  
 <xref:System.ServiceModel.Configuration.X509InitiatorCertificateServiceElement.Authentication%2A>  
 <xref:System.ServiceModel.Configuration.X509ClientCertificateAuthenticationElement>  
 [Comportamentos de segurança](../../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md)  
 [Como criar um serviço que utiliza um validador de certificado personalizado](../../../../../docs/framework/wcf/extending/how-to-create-a-service-that-employs-a-custom-certificate-validator.md)  
 [Trabalhando com certificados](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md)
