---
title: Enumeração CorDebugDecodeEventFlagsWindows
ms.date: 03/30/2017
api_name:
- CorDebugDecodeEventFlagsWindows
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: aa6cf962-30ae-4cfd-8895-826deeb46a54
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: fa8bbcf4d8e5aadee6a4250d23842187d6c2af09
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="cordebugdecodeeventflagswindows-enumeration"></a>Enumeração CorDebugDecodeEventFlagsWindows
Fornece informações adicionais sobre eventos de depuração na plataforma Windows.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
typedef enum CorDebugDecodeEventFlagsWindows {  
    IS_FIRST_CHANCE = 1,  
} CorDebugDecodeEventFlagsWindows;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|Descrição|  
|------------|-----------------|  
|`IS_FIRST_CHANCE`|Indica que o evento de depuração é uma exceção de primeira chance.|  
  
## <a name="remarks"></a>Comentários  
 O [Icordebugprocess6](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess6-decodeevent-method.md) método inclui um `dwFlags` parâmetro que fornece informações adicionais sobre um evento de depuração e cujo valor é dependente da arquitetura de destino. A enumeração `CorDebugDecodeEventFlagsWindows` pode ser usada com eventos de depuração na plataforma Windows.  
  
> [!NOTE]
>  Essa enumeração é destinada ao uso no .NET Native somente para cenários de depuração.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** consulte [requisitos de sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versões do .NET framework:** [!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Declarando enumerações](../../../../docs/framework/unmanaged-api/debugging/debugging-enumerations.md)
