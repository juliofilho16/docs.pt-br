---
title: "Método ICorProfilerCallback::RuntimeThreadResumed"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorProfilerCallback.RuntimeThreadResumed
api_location: mscorwks.dll
api_type: COM
f1_keywords: ICorProfilerCallback::RuntimeThreadResumed
helpviewer_keywords:
- ICorProfilerCallback::RuntimeThreadResumed method [.NET Framework profiling]
- RuntimeThreadResumed method [.NET Framework profiling]
ms.assetid: da984f89-4f53-4ab0-ae6f-3e2ee6085994
topic_type: apiref
caps.latest.revision: "11"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: b460f87ead93c5f375c758a5547c0ae0be2b5691
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="icorprofilercallbackruntimethreadresumed-method"></a><span data-ttu-id="7bff8-102">Método ICorProfilerCallback::RuntimeThreadResumed</span><span class="sxs-lookup"><span data-stu-id="7bff8-102">ICorProfilerCallback::RuntimeThreadResumed Method</span></span>
<span data-ttu-id="7bff8-103">Notifica o criador de perfil que o thread especificado foi retomado após ter sido suspenso.</span><span class="sxs-lookup"><span data-stu-id="7bff8-103">Notifies the profiler that the specified thread has resumed after being suspended.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="7bff8-104">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="7bff8-104">Syntax</span></span>  
  
```  
HRESULT RuntimeThreadResumed(  
    [in] ThreadID threadId);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="7bff8-105">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="7bff8-105">Parameters</span></span>  
 `threadId`  
 <span data-ttu-id="7bff8-106">[in] A ID do thread que foi retomado.</span><span class="sxs-lookup"><span data-stu-id="7bff8-106">[in] The ID of the thread that has been resumed.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="7bff8-107">Requisitos</span><span class="sxs-lookup"><span data-stu-id="7bff8-107">Requirements</span></span>  
 <span data-ttu-id="7bff8-108">**Plataformas:** consulte [requisitos de sistema](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="7bff8-108">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="7bff8-109">**Cabeçalho:** Corprof. idl, CorProf.h</span><span class="sxs-lookup"><span data-stu-id="7bff8-109">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="7bff8-110">**Biblioteca:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="7bff8-110">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="7bff8-111">**Versões do .NET framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="7bff8-111">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="7bff8-112">Consulte também</span><span class="sxs-lookup"><span data-stu-id="7bff8-112">See Also</span></span>  
 [<span data-ttu-id="7bff8-113">Interface ICorProfilerCallback</span><span class="sxs-lookup"><span data-stu-id="7bff8-113">ICorProfilerCallback Interface</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)  
 [<span data-ttu-id="7bff8-114">Método RuntimeThreadSuspended</span><span class="sxs-lookup"><span data-stu-id="7bff8-114">RuntimeThreadSuspended Method</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-runtimethreadsuspended-method.md)