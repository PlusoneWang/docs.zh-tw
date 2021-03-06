---
title: IHostSecurityManager::SetSecurityContext 方法
ms.date: 03/30/2017
api_name:
- IHostSecurityManager.SetSecurityContext
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostSecurityManager::SetSecurityContext
helpviewer_keywords:
- SetSecurityContext method [.NET Framework hosting]
- IHostSecurityManager::SetSecurityContext method [.NET Framework hosting]
ms.assetid: e4372384-ee69-48d7-97e0-8fab7866597a
topic_type:
- apiref
ms.openlocfilehash: 676a1d50202333203c13fcf916dbb14a6d91fb8f
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/30/2019
ms.locfileid: "73121437"
---
# <a name="ihostsecuritymanagersetsecuritycontext-method"></a>IHostSecurityManager::SetSecurityContext 方法
設定目前執行中線程的安全性內容。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT SetSecurityContext (  
    [in]  EContextType eContextType,  
    [out] IHostSecurityContext** ppSecurityContext  
);  
```  
  
## <a name="parameters"></a>參數  
 `eContextType`  
 在其中一個[ECoNtextType](../../../../docs/framework/unmanaged-api/hosting/econtexttype-enumeration.md)值，表示 common language RUNTIME （CLR）放置在主機上的內容類型。  
  
 `ppSecurityContext`  
 脫銷新[IHostSecurityCoNtext](../../../../docs/framework/unmanaged-api/hosting/ihostsecuritycontext-interface.md)物件的位址指標。  
  
## <a name="return-value"></a>傳回值  
  
|HRESULT|描述|  
|-------------|-----------------|  
|S_OK|已成功傳回 `SetSecurityContext`。|  
|HOST_E_CLRNOTAVAILABLE|CLR 尚未載入進程中，或 CLR 處於無法執行 managed 程式碼或成功處理呼叫的狀態。|  
|HOST_E_TIMEOUT|呼叫超時。|  
|HOST_E_NOT_OWNER|呼叫端沒有擁有鎖定。|  
|HOST_E_ABANDONED|已封鎖的執行緒或光纖在等候時取消了事件。|  
|E_FAIL|發生不明的嚴重失敗。 當方法傳回 E_FAIL 時，CLR 就無法在進程內使用。 對裝載方法的後續呼叫會傳回 HOST_E_CLRNOTAVAILABLE。|  
  
## <a name="remarks"></a>備註  
 CLR 會在數個案例中呼叫 `SetSecurityContext`。 在執行類別和模組的函式和完成項之前，CLR 會呼叫 `SetSecurityContext`，以保護主機不受執行失敗的影響。 接著，它會使用 `SetSecurityContext`的另一個呼叫，在執行函式或完成項之後，將安全性內容重設為其原始狀態。 I/o 完成時，會發生類似的模式。 如果主機執行[IHostIoCompletionManager](../../../../docs/framework/unmanaged-api/hosting/ihostiocompletionmanager-interface.md)，則 CLR 會在主機呼叫[ICLRIoCompletionManager：： OnComplete](../../../../docs/framework/unmanaged-api/hosting/iclriocompletionmanager-oncomplete-method.md)之後呼叫 `SetSecurityContext`。  
  
 在背景工作執行緒的非同步點上，CLR 會在 <xref:System.Threading.ThreadPool.QueueUserWorkItem%2A?displayProperty=nameWithType> 或[IHostThreadPoolManager：： QueueUserWorkItem](../../../../docs/framework/unmanaged-api/hosting/ihostthreadpoolmanager-queueuserworkitem-method.md)內呼叫 `SetSecurityContext`，視主機或 CLR 是否正在執行執行緒集區而定。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **標頭：** Mscoree.dll. h  
  
 連結**庫：** 包含為 Mscoree.dll 中的資源  
  
 **.NET framework 版本：** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>請參閱

- <xref:System.Threading.ThreadPool?displayProperty=nameWithType>
- [EContextType 列舉](../../../../docs/framework/unmanaged-api/hosting/econtexttype-enumeration.md)
- [ICLRIoCompletionManager 介面](../../../../docs/framework/unmanaged-api/hosting/iclriocompletionmanager-interface.md)
- [IHostIoCompletionManager 介面](../../../../docs/framework/unmanaged-api/hosting/ihostiocompletionmanager-interface.md)
- [IHostSecurityContext 介面](../../../../docs/framework/unmanaged-api/hosting/ihostsecuritycontext-interface.md)
- [IHostSecurityManager 介面](../../../../docs/framework/unmanaged-api/hosting/ihostsecuritymanager-interface.md)
- [IHostThreadPoolManager 介面](../../../../docs/framework/unmanaged-api/hosting/ihostthreadpoolmanager-interface.md)
