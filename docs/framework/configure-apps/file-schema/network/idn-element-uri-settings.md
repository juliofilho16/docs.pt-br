---
title: '&lt;IDN&gt; elemento (configurações de Uri)'
ms.date: 03/30/2017
ms.assetid: 16c8e869-1791-4cf5-9244-3d3c738f60ec
author: mcleblanc
ms.author: markl
manager: markl
ms.openlocfilehash: 17f68fbb92797928be911e530232e8638793687f
ms.sourcegitcommit: 11f11ca6cefe555972b3a5c99729d1a7523d8f50
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="ltidngt-element-uri-settings"></a>&lt;IDN&gt; elemento (configurações de Uri)
Especifica se a análise de nome de domínio internacionalizado (IDN) é aplicada a um nome de domínio.  
  
## <a name="schema-hierarchy"></a>Hierarquia de esquema  
 [Elemento \<configuration>](../../../../../docs/framework/configure-apps/file-schema/configuration-element.md)  
  
 [\<URI > elemento (configurações de Uri)](../../../../../docs/framework/configure-apps/file-schema/network/uri-element-uri-settings.md)  
  
 [\<IDN >](../../../../../docs/framework/configure-apps/file-schema/network/idn-element-uri-settings.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<idn  
  enabled="All|AllExceptIntranet|None"  
/>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|**Elemento**|**Descrição**|  
|-----------------|---------------------|  
|`enabled`|Especifica que se a análise de nome de domínio internacionalizado (IDN) é aplicado a um nome de domínio o valor padrão é none.|  
  
### <a name="child-elements"></a>Elementos filho  
 Nenhum  
  
### <a name="parent-elements"></a>Elementos pai  
  
|**Elemento**|**Descrição**|  
|-----------------|---------------------|  
|[URI](../../../../../docs/framework/configure-apps/file-schema/network/uri-element-uri-settings.md)|Contém configurações que especificam como o .NET Framework controla endereços da web expressados usando identificadores de recurso uniformes (URIs).|  
  
## <a name="remarks"></a>Comentários  
 Existente <xref:System.Uri> classe foi estendida no .NET Framework 3.5. 3.0 SP1 e 2.0 SP1 com suporte para identificadores de recursos internacionais (IRI) e nomes de domínio internacionalizados (IDNS). Os usuários atuais não verão qualquer alteração no comportamento do .NET Framework 2.0, a menos que eles permitem especificamente IRI e IDN suporte. Isso garante a compatibilidade do aplicativo com versões anteriores do .NET Framework.  
  
 Para habilitar o suporte para IRI, as alterações a seguir são necessárias:  
  
1.  Adicione a seguinte linha no arquivo Machine. config no diretório do .NET Framework 2.0  
  
    ```xml  
    <section name="uri" type="System.Configuration.UriSection, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
    ```  
  
2.  Especifique se deseja que a análise de nome de domínio internacionalizado (IDN) aplicado ao nome de domínio e se as regras de análise de IRI deve ser aplicada. Isso pode ser feito no arquivo machine.config ou em app.config.  
  
 Há três valores possíveis para IDN dependendo os servidores DNS que são usados:  
  
-   IDN habilitado = All  
  
     Esse valor converterá todos os nomes de domínio Unicode em seus equivalentes do Punycode (nomes IDN).  
  
-   IDN habilitado = AllExceptIntranet  
  
     Esse valor serão convertidos em todos os nomes de domínio de Unicode não na Intranet local para usar os equivalentes de Punycode (nomes IDN). Nesse caso para lidar com nomes internacionais da intranet local, os servidores DNS que são usados para a Intranet devem dar suporte a resolução de nomes de Unicode.  
  
-   IDN habilitado = nenhum  
  
     Esse valor não converterá nenhum nome de domínio Unicode para usar o Punycode. Este é o valor padrão que é consistente com o comportamento do .NET Framework 2.0.  
  
 Habilitar o IDN converterá todos os rótulos Unicode de um nome de domínio para seus equivalentes em Punycode. Os nomes Punycode contêm apenas caracteres ASCII e sempre começam com o prefixo xn--. A razão para isso é dar suporte a servidores DNS existentes na Internet, pois a maioria dos servidores DNS dá suporte somente a caracteres ASCII (consulte RFC 3940).  
  
### <a name="configuration-files"></a>Arquivos de Configuração  
 Esse elemento pode ser usado no arquivo de configuração do aplicativo ou o arquivo de configuração de máquina (Machine. config).  
  
## <a name="example"></a>Exemplo  
  
### <a name="description"></a>Descrição  
 O exemplo a seguir mostra uma configuração usada pela <xref:System.Uri> classe para dar suporte a análise de IRI e nomes IDN.  
  
### <a name="code"></a>Código  
  
```xml  
<configuration>  
  <uri>  
    <idn enabled="All" />  
    <iriParsing enabled="true" />  
  </uri>  
</configuration>  
```  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.Configuration.IdnElement?displayProperty=nameWithType>  
 <xref:System.Configuration.UriSection?displayProperty=nameWithType>  
 [Esquema de configurações de rede](../../../../../docs/framework/configure-apps/file-schema/network/index.md)
