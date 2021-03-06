---
title: Método ICorDebugBlockingObjectEnum::Next
ms.date: 03/30/2017
api_name:
- ICorDebugBlockingObjectEnum.Next Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugBlockingObjectEnum::Next
helpviewer_keywords:
- Next method, ICorDebugBlockingObjectEnum interface [.NET Framework debugging]
- ICorDebugBlockingObjectEnum::Next method [.NET Framework debugging]
ms.assetid: 0121753f-ebea-48d0-aeb2-ed7fda76dc60
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b4336978825fbf7844b3ceaf179954f28660f08c
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="icordebugblockingobjectenumnext-method"></a>Método ICorDebugBlockingObjectEnum::Next
Obtém o número especificado de [CorDebugBlockingObject](../../../../docs/framework/unmanaged-api/debugging/cordebugblockingobject-structure.md) objetos de enumeração, começando na posição atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT Next([in] ULONG  celt,  
             [out, size_is(celt), length_is(*pceltFetched)]  
                           CorDebugBlockingObject values[],  
             [out] ULONG *pceltFetched;  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `celt`  
 [in] O número de objetos para recuperar.  
  
 `values`  
 [out] Uma matriz de ponteiros para [CorDebugBlockingObject](../../../../docs/framework/unmanaged-api/debugging/cordebugblockingobject-structure.md) objetos.  
  
 `pceltFetched`  
 [out] Um ponteiro para o número de objetos que foram recuperados.  
  
## <a name="return-value"></a>Valor de retorno  
 Esse método retorna os HRESULTs específicos a seguir.  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|O método foi concluído com êxito.|  
|S_FALSE|`pceltFetched` não é igual a `celt`.|  
  
## <a name="remarks"></a>Comentários  
 Essas funções de método como um enumerador COM típico.  
  
 Os valores da matriz de entrada devem ser pelo menos do tamanho `celt`. A matriz será preenchida com o próximo `celt` valores na enumeração ou com todos os valores restantes se menos de `celt` permanecem. Quando este método retorna, `pceltFetched` será preenchido com o número de valores que foram recuperados. Se `values` contém ponteiros inválidos ou aponta para um buffer que é menor do que `celt`, ou se `pceltFetched` é um ponteiro inválido, o resultado é indefinido.  
  
> [!NOTE]
>  Embora o [CorDebugBlockingObject](../../../../docs/framework/unmanaged-api/debugging/cordebugblockingobject-structure.md) estrutura não precisa ser liberado, a interface "ICorDebugValue" dentro do elemento precisam ser liberados.  
  
-  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** consulte [requisitos de sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versões do .NET framework:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Interface ICorDebugDataTarget](../../../../docs/framework/unmanaged-api/debugging/icordebugdatatarget-interface.md)  
 [Depurando interfaces](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)  
 [Depuração](../../../../docs/framework/unmanaged-api/debugging/index.md)
