---
title: CreateDebuggingInterfaceFromVersion 函式
ms.date: 03/30/2017
api_name:
- CreateDebuggingInterfaceFromVersion
api_location:
- mscoree.dll
- mscoreei.dll
api_type:
- DLLExport
f1_keywords:
- CreateDebuggingInterfaceFromVersion
helpviewer_keywords:
- CreateDebuggingInterfaceFromVersion function [.NET Framework hosting]
ms.assetid: a746a849-463c-44f5-a2f0-9e812ed8bcc3
topic_type:
- apiref
ms.openlocfilehash: e23dfb86c2129a02a0ca95de8c89d8294e97ad81
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/30/2019
ms.locfileid: "73136842"
---
# <a name="createdebugginginterfacefromversion-function"></a>CreateDebuggingInterfaceFromVersion 函式
根據指定的版本資訊建立[ICorDebug](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md)物件。  
  
 此函式在 .NET Framework 4 中已過時。 相反地，若要取得 common language runtime （CLR）2.0 的介面，請使用[ICLRRuntimeInfo：： GetInterface](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-getinterface-method.md)方法，並指定類別識別碼 CLSID_CLRDebuggingLegacy 和介面識別碼 IID_ICorDebug。 若要取得 CLR 4 或更新版本的介面，請呼叫[CLRCreateInstance](../../../../docs/framework/unmanaged-api/hosting/clrcreateinstance-function.md)函數，並指定類別識別碼 CLSID_CLRDebugging 和介面識別碼 IID_ICLRDebugging。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT CreateDebuggingInterfaceFromVersion (  
    [in]  int      iDebuggerVersion,   
    [in]  LPCWSTR  szDebuggeeVersion,   
    [out] IUnknown **ppCordb  
);  
```  
  
## <a name="parameters"></a>參數  
 `iDebuggerVersion`  
 在偵錯工具所需的 `ICorDebug` 版本。 如需有效的值，請參閱[CorDebugInterfaceVersion](../../../../docs/framework/unmanaged-api/debugging/cordebuginterfaceversion-enumeration.md)列舉。  
  
 `szDebuggeeVersion`  
 在與要進行調試的應用程式或進程相關聯的 common language runtime 版本。 如需有關抓取此值的詳細資訊，請參閱[GetVersionFromProcess](../../../../docs/framework/unmanaged-api/hosting/getversionfromprocess-function.md)或[GetRequestedRuntimeVersion](../../../../docs/framework/unmanaged-api/hosting/getrequestedruntimeversion-function.md)方法。  
  
 `ppCordb`  
 脫銷接收 `ICorDebug` 物件之指標的位置。  
  
## <a name="return-value"></a>傳回值  
 除了下列值之外，這個方法會傳回 Winerror.h 檔案中定義的標準 COM 錯誤碼。  
  
|傳回碼|描述|  
|-----------------|-----------------|  
|S_OK|已成功完成命令。|  
|E_INVALIDARG|`szDebuggeeVersion` 或 `ppCordb` 為 null，或版本字串不正確。|  
  
## <a name="remarks"></a>備註  
 `szDebuggeeVersion` 參數會對應至相對應的 Mscordbi.dll 版本。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **標頭：** Mscoree.dll. h  
  
 連結**庫：** Mscoree.dll .dll  
  
 **.NET framework 版本：** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>請參閱

- [已被取代的 CLR 裝載函式](../../../../docs/framework/unmanaged-api/hosting/deprecated-clr-hosting-functions.md)
