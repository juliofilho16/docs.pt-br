---
title: '&lt;adicionar&gt; &lt;claimTypeRequirements&gt;'
ms.date: 03/30/2017
ms.assetid: c68e83c9-39e8-4264-b1ce-b6a9eb5b98aa
ms.openlocfilehash: b4f9275fdc36ea3c7ba79c6609f039c3b1f4c3ed
ms.sourcegitcommit: 11f11ca6cefe555972b3a5c99729d1a7523d8f50
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="ltaddgt-of-ltclaimtyperequirementsgt"></a>&lt;adicionar&gt; &lt;claimTypeRequirements&gt;
Especifica os tipos de declarações obrigatórias e opcionais esperados para aparecer na credencial federada. Por exemplo, serviços de estado os requisitos de credenciais de entrada, que devem ter um determinado conjunto de tipos de declaração.  
  
 \<system.serviceModel>  
\<associações >  
\<customBinding>  
\<associação >  
\<segurança >  
\<issuedTokenParameters >  
\<claimTypeRequirements >  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<claimTypeRequirements>  
      <add claimType="URI"  
           isOptional="Boolean" />  
</claimTypeRequirements>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|claimType|Um URI que define o tipo de declaração. Por exemplo, para adquirir um produto de um site, o usuário deve apresentar um cartão de crédito válido com limite de crédito suficiente. O tipo de declaração seria o URI do cartão de crédito.|  
|é opcional|Um valor booleano que especifica se esta é uma declaração opcional. Defina este atributo como `false` quando se trata de uma declaração necessária.<br /><br /> Você pode usar esse atributo quando o serviço solicita informações, mas não a exige. Por exemplo, se você precisar que o usuário insira seu nome, sobrenome e endereço, mas decidir que o número de telefone é opcional.|  
  
### <a name="child-elements"></a>Elementos filho  
 nenhuma.  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<claimTypeRequirements>](../../../../../docs/framework/configure-apps/file-schema/wcf/claimtyperequirements-element.md)|Especifica uma coleção de tipos de declaração necessária.<br /><br /> Em um cenário federado, serviços de estado os requisitos de credenciais de entrada. Por exemplo, as credenciais de entrada devem ter um determinado conjunto de tipos de declaração. Cada elemento na coleção Especifica os tipos de declarações obrigatórias e opcionais que deve aparecer em uma credencial federada.|  
  
## <a name="remarks"></a>Comentários  
 Em um cenário federado, serviços de estado os requisitos de credenciais de entrada. Por exemplo, as credenciais de entrada devem ter um determinado conjunto de tipos de declaração. Esse requisito é manifestado em uma política de segurança. Quando um credenciais de solicitações de cliente de um serviço federado (por exemplo, o CardSpace), ele coloca os requisitos em uma solicitação de token (RequestSecurityToken) para que o serviço federado pode emitir as credenciais que satisfaça os requisitos de acordo.  
  
## <a name="example"></a>Exemplo  
 A configuração a seguir adiciona dois requisitos de tipo de declaração para uma associação de segurança.  
  
```xml  
<bindings>  
    <wsFederationHttpBinding>  
      <binding name="myFederatedBinding">  
        <security mode="Message">  
          <message issuedTokenType="urn:oasis:names:tc:SAML:1.0:assertion">  
            <claimTypeRequirements>  
              <add claimType=  
"http://schemas.microsoft.com/ws/2005/05/identity/claims/EmailAddress"/>  
              <add claimType=  
"http://schemas.microsoft.com/ws/2005/05/identity/claims/UserName"    
optional="true" />  
            </claims>  
          </message>  
        </security>  
      </binding>  
    </wsFederationHttpBinding>  
</bindings>  
```  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.ServiceModel.Security.Tokens.ClaimTypeRequirement>  
 <xref:System.ServiceModel.Security.Tokens.IssuedSecurityTokenParameters.ClaimTypeRequirements%2A>  
 <xref:System.ServiceModel.Configuration.IssuedTokenParametersElement.ClaimTypeRequirements%2A>  
 <xref:System.ServiceModel.Configuration.ClaimTypeElementCollection>  
 <xref:System.ServiceModel.Configuration.ClaimTypeElement>  
 <xref:System.ServiceModel.Channels.CustomBinding>  
 [\<claimTypeRequirements>](../../../../../docs/framework/configure-apps/file-schema/wcf/claimtyperequirements-element.md)  
 [Associações](../../../../../docs/framework/wcf/bindings.md)  
 [Estendendo associações](../../../../../docs/framework/wcf/extending/extending-bindings.md)  
 [Associações personalizadas](../../../../../docs/framework/wcf/extending/custom-bindings.md)  
 [\<customBinding>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)  
 [Como criar uma associação personalizada utilizando o SecurityBindingElement](../../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)  
 [Segurança de associação personalizada](../../../../../docs/framework/wcf/samples/custom-binding-security.md)
