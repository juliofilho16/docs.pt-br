---
title: Método IMetaDataImport::FindMemberRef
ms.date: 03/30/2017
api_name:
- IMetaDataImport.FindMemberRef
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::FindMemberRef
helpviewer_keywords:
- IMetaDataImport::FindMemberRef method [.NET Framework metadata]
- FindMemberRef method [.NET Framework metadata]
ms.assetid: 1ccda329-d752-4d89-abe8-511af3c3f4c9
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: c3736d604b7e77028a2b99d462d88ae207df926c
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="imetadataimportfindmemberref-method"></a>Método IMetaDataImport::FindMemberRef
Obtém um ponteiro para o token de MemberRef para o membro de referência que é delimitada por especificado <xref:System.Type> e que tem a assinatura de nome e os metadados especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT FindMemberRef (  
   [in]  mdTypeRef          td,  
   [in]  LPCWSTR            szName,   
   [in]  PCCOR_SIGNATURE    pvSigBlob,   
   [in]  ULONG              cbSigBlob,   
   [out] mdMemberRef        *pmr  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `td`  
 [in] O token TypeRef para a classe ou interface que inclui a referência do membro a ser pesquisado. Se esse valor for `mdTokenNil`, a pesquisa é feita para uma variável global ou uma referência de função global.  
  
 `szName`  
 [in] O nome da referência de membro para pesquisar.  
  
 `pvSigBlob`  
 [in] Um ponteiro para a assinatura de binários de metadados da referência do membro.  
  
 `cbSigBlob`  
 [in] O tamanho em bytes do `pvSigBlob`.  
  
 `pmr`  
 [out] Um ponteiro para o token de MemberRef correspondente.  
  
## <a name="remarks"></a>Comentários  
 Especifique o membro usando sua classe ou interface de delimitador (`td`), seu nome (`szName`) e, opcionalmente, sua assinatura (`pvSigBlob`).  
  
 A assinatura é passado para `FindMemberRef` deve foram gerados no escopo atual, porque as assinaturas associadas a um determinado escopo. Uma assinatura pode inserir um token que identifica o tipo de valor ou classe delimitador. O token é um índice na tabela de TypeDef local. Você não pode criar uma assinatura de tempo de execução fora do contexto do escopo atual e usar essa assinatura como entrada para `FindMemberRef`.  
  
 `FindMemberRef` localiza apenas as referências de membro que foram definidas diretamente na classe ou interface. referências de membro herdado não for encontrada.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** consulte [requisitos de sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor.h  
  
 **Biblioteca:** incluído como um recurso no MSCOREE  
  
 **Versões do .NET framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Interface IMetaDataImport](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)  
 [Interface IMetaDataImport2](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)
