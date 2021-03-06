---
title: Enumeração EClrUnhandledException
ms.date: 03/30/2017
api_name:
- EClrUnhandledException
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- EClrUnhandledException
helpviewer_keywords:
- EClrUnhandledException enumeration [.NET Framework hosting]
ms.assetid: d231044e-2b53-4836-93f9-8117ff0e5c3a
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: eeff8aa0336c0c497e306825c6c77f4f8745ca7c
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="eclrunhandledexception-enumeration"></a>Enumeração EClrUnhandledException
Descreve as opções disponíveis para o gerenciamento de exceções que são sem tratamento no código do usuário.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
typedef enum {  
    eRuntimeDeterminedPolicy,  
    eHostDeterminedPolicy  
} EClrUnhandledException;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|Descrição|  
|------------|-----------------|  
|`eRuntimeDeterminedPolicy`|Especifica que o comportamento padrão ocorre. O processo é interrompido.|  
|`eHostDeterminedPolicy`|Especifica que o common language runtime (CLR) ignora exceções sem tratamento e permite que o host determine nenhuma outra ação.|  
  
## <a name="remarks"></a>Comentários  
 Para especificar que o CLR se comportam como nas versões anteriores, use o `eHostDeterminedPolicy` membro.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** consulte [requisitos de sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE.h  
  
 **Biblioteca:** MSCorEE.dll  
  
 **Versões do .NET framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Enumeração EClrFailure](../../../../docs/framework/unmanaged-api/hosting/eclrfailure-enumeration.md)  
 [Enumeração EClrOperation](../../../../docs/framework/unmanaged-api/hosting/eclroperation-enumeration.md)  
 [Interface ICLRPolicyManager](../../../../docs/framework/unmanaged-api/hosting/iclrpolicymanager-interface.md)  
 [Método SetUnhandledExceptionPolicy](../../../../docs/framework/unmanaged-api/hosting/iclrpolicymanager-setunhandledexceptionpolicy-method.md)  
 [Interface IHostPolicyManager](../../../../docs/framework/unmanaged-api/hosting/ihostpolicymanager-interface.md)  
 [Enumerações de hospedagem](../../../../docs/framework/unmanaged-api/hosting/hosting-enumerations.md)
