---
title: Método ICorDebugEval::NewArray
ms.date: 03/30/2017
api_name:
- ICorDebugEval.NewArray
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugEval::NewArray
helpviewer_keywords:
- NewArray method [.NET Framework debugging]
- ICorDebugEval::NewArray method [.NET Framework debugging]
ms.assetid: cc79a67d-5368-434d-a943-209db90491b9
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 38b00d903fdd7301415a8df7642e12366178fd10
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="icordebugevalnewarray-method"></a>Método ICorDebugEval::NewArray
Aloca uma nova matriz do tipo de elemento especificado e dimensões.  
  
 Este método está obsoleto no .NET Framework versão 2.0. Use [Icordebugeval2](../../../../docs/framework/unmanaged-api/debugging/icordebugeval2-newparameterizedarray-method.md) em vez disso.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT NewArray (  
    [in] CorElementType     elementType,  
    [in] ICorDebugClass     *pElementClass,  
    [in] ULONG32            rank,  
    [in, size_is(rank)] ULONG32 dims[],  
    [in, size_is(rank)] ULONG32 lowBounds[]  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `elementType`  
 [in] Um valor da enumeração CorElementType que especifica o tipo de elemento da matriz.  
  
 `pElementClass`  
 [in] Um ponteiro para um objeto de ICorDebugClass que especifica a classe do elemento. Esse valor pode ser null se o tipo de elemento é um tipo primitivo.  
  
 `rank`  
 [in] O número de dimensões da matriz. No .NET Framework 2.0, esse valor deve ser 1.  
  
 `dims`  
 [in] O tamanho, em bytes, de cada dimensão da matriz.  
  
 `lowBounds`  
 [in] Opcional. O limite inferior de cada dimensão da matriz. Se esse valor for omitido, um limite inferior de zero será assumido para cada dimensão.  
  
## <a name="remarks"></a>Comentários  
 A matriz sempre é criada no domínio do aplicativo no qual o thread está em execução no momento.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** consulte [requisitos de sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versões do .NET framework:** 1.1 e 1.0
