---
title: Método ICorDebugProcess::SetThreadContext
ms.date: 03/30/2017
api_name:
- ICorDebugProcess.SetThreadContext
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess::SetThreadContext
helpviewer_keywords:
- ICorDebugProcess::SetThreadContext method [.NET Framework debugging]
- SetThreadContext method, ICorDebugProcess interface [.NET Framework debugging]
ms.assetid: a7b50175-2bf1-40be-8f65-64aec7aa1247
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c9ed79eb799971dfcbc9fd787cd0290795f79d96
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="icordebugprocesssetthreadcontext-method"></a>Método ICorDebugProcess::SetThreadContext
Define o contexto de determinado thread neste processo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT SetThreadContext(  
    [in] DWORD threadID,  
    [in] ULONG32 contextSize,  
    [in, length_is(contextSize), size_is(contextSize)]  
    BYTE context[]);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `threadID`  
 [in] A ID do thread para o qual definir o contexto.  
  
 `contextSize`  
 [in] O tamanho do `context` matriz.  
  
 `context`  
 [in] Uma matriz de bytes que descrevem o contexto do thread.  
  
 O contexto Especifica a arquitetura do processador que o thread está em execução.  
  
## <a name="remarks"></a>Comentários  
 O depurador deve chamar esse método em vez de Win32 `SetThreadContext` funcionar, porque o thread, na verdade, pode estar em um estado "capturado", no qual seu contexto foi temporariamente alterado. Esse método deve ser usado somente quando um thread está no código nativo. Use [ICorDebugRegisterSet](../../../../docs/framework/unmanaged-api/debugging/icordebugregisterset-interface.md) para segmentos no código gerenciado. Nunca deve ser necessário modificar o contexto de thread durante um evento de depuração fora de banda (OOB).  
  
 Os dados passados devem ser uma estrutura de contexto para a plataforma atual.  
  
 Esse método pode corromper o tempo de execução se usada incorretamente.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** consulte [requisitos de sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versões do .NET framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
