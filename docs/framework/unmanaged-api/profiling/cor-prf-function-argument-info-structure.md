---
title: Estrutura COR_PRF_FUNCTION_ARGUMENT_INFO
ms.date: 03/30/2017
api_name:
- COR_PRF_FUNCTION_ARGUMENT_INFO
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- COR_PRF_FUNCTION_ARGUMENT_INFO
helpviewer_keywords:
- COR_PRF_FUNCTION_ARGUMENT_INFO structure [.NET Framework profiling]
ms.assetid: 07cf3bab-e193-4991-8205-3f41cf2d67b3
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 1fbc41ca1366b412c37d6af09e90e3f1b042ba21
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="corprffunctionargumentinfo-structure"></a>Estrutura COR_PRF_FUNCTION_ARGUMENT_INFO
Representa os argumentos de uma função, em ordem da esquerda para a direita.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
typedef struct _COR_PRF_FUNCTION_ARGUMENT_INFO {  
    ULONG numRanges;  
    ULONG totalArgumentSize;  
    COR_PRF_FUNCTION_ARGUMENT_RANGE ranges[1];  
} COR_PRF_FUNCTION_ARGUMENT_INFO;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|Descrição|  
|------------|-----------------|  
|`numRanges`|O número de blocos de argumentos. Ou seja, esse valor é o número de [COR_PRF_FUNCTION_ARGUMENT_RANGE](../../../../docs/framework/unmanaged-api/profiling/cor-prf-function-argument-range-structure.md) estruturas de `ranges` matriz.|  
|`totalArgumentSize`|O tamanho total de todos os argumentos. Em outras palavras, esse valor é a soma dos comprimentos de argumento.|  
|`ranges`|Uma matriz de `COR_PRF_FUNCTION_ARGUMENT_RANGE` estruturas, cada um deles representa um bloco de argumentos da função.|  
  
## <a name="remarks"></a>Comentários  
 Uma função pode ter muitos argumentos. Esses argumentos não podem ser armazenados contiguamente na memória. Você pode ter um bloco de três argumentos em um só lugar, um bloco de dois argumentos em outro lugar e um bloco final de um argumento em um local diferente. Esses argumentos são todos para a mesma função; eles apenas são armazenados em diferentes locais.  
  
 O `COR_PRF_FUNCTION_ARGUMENT_INFO` estrutura representa todos os argumentos de uma única função. Ele usa uma matriz para fazer referência a todos os blocos de argumentos de função. Portanto, para uma única função, você tem um único `COR_PRF_FUNCTION_ARGUMENT_INFO` estrutura, o que faz referência a vários `COR_PRF_FUNCTION_ARGUMENT_RANGE` estruturas, cada qual apontando para um ou mais argumentos de função.  
  
 Argumentos que são armazenados nos registros serem distribuídos na memória para criar as estruturas.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** consulte [requisitos de sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Cabeçalho:** Corprof. idl  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versões do .NET framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Estruturas de criação de perfil](../../../../docs/framework/unmanaged-api/profiling/profiling-structures.md)
