---
title: ICorDebugFrame 介面
ms.date: 03/30/2017
api_name:
- ICorDebugFrame
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugFrame
helpviewer_keywords:
- ICorDebugFrame interface [.NET Framework debugging]
ms.assetid: 0c48f764-3c64-4602-b2f4-4ffc60eb2c65
topic_type:
- apiref
ms.openlocfilehash: ba138e79e0d6fb6f9c5e9c3efe3466f3c88cccae
ms.sourcegitcommit: 13e79efdbd589cad6b1de634f5d6b1262b12ab01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/28/2020
ms.locfileid: "76782613"
---
# <a name="icordebugframe-interface"></a>ICorDebugFrame 介面

表示目前堆疊上的框架。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|[CreateStepper 方法](icordebugframe-createstepper-method.md)|取得 ICorDebugStepper，以執行相對於此 `ICorDebugFrame`的逐步操作。|  
|[GetCallee 方法](icordebugframe-getcallee-method.md)|取得此框架所呼叫之目前鏈中 `ICorDebugFrame` 的指標，如果這是鏈中最內層的框架，則會傳回 null。|  
|[GetCaller 方法](icordebugframe-getcaller-method.md)|取得目前鏈中呼叫此框架之 `ICorDebugFrame` 的指標，如果這是鏈中最外層的框架，則傳回 null。|  
|[GetChain 方法](icordebugframe-getchain-method.md)|取得此 `ICorDebugFrame` 所屬之 ICorDebugChain 的指標。|  
|[GetCode 方法](icordebugframe-getcode-method.md)|取得與這個堆疊框架相關聯之 ICorDebugCode 的指標。|  
|[GetFunction 方法](icordebugframe-getfunction-method.md)|取得 ICorDebugFunction 的指標，其中包含與這個堆疊框架相關聯的程式碼。|  
|[GetFunctionToken 方法](icordebugframe-getfunctiontoken-method.md)|取得包含與此堆疊框架相關聯之程式碼的函式的元資料標記。|  
|[GetStackRange 方法](icordebugframe-getstackrange-method.md)|取得此 `ICorDebugFrame`所表示之堆疊框架的絕對位址範圍。|  
  
## <a name="remarks"></a>備註  
  
> [!NOTE]
> 這個介面不支援跨電腦或跨處理序的遠端呼叫。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **標頭：** CorDebug.idl、CorDebug.h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET framework 版本：** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>請參閱

- [偵錯介面](debugging-interfaces.md)
