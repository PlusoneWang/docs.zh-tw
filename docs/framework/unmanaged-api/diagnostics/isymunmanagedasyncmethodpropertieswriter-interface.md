---
title: ISymUnmanagedAsyncMethodPropertiesWriter 介面
ms.date: 03/30/2017
ms.assetid: caa71820-8058-4b6a-93a2-25ee757d92d3
ms.openlocfilehash: db065357e22ac576600a3ca61dda0882b9206a86
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/30/2019
ms.locfileid: "73129156"
---
# <a name="isymunmanagedasyncmethodpropertieswriter-interface"></a>ISymUnmanagedAsyncMethodPropertiesWriter 介面
可讓您定義每個方法符號的選擇性非同步方法資訊。 一律搭配已開啟的方法使用;也就是呼叫[OpenMethod 方法](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-openmethod-method.md)和[CloseMethod 方法](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-closemethod-method.md)之間的。  
  
## <a name="syntax"></a>語法  
  
```idl  
[object,uuid(FC073774-1739-4232-BD56-A027294BEC15),pointer_default(unique)]interface ISymUnmanagedAsyncMethodPropertiesWriter : IUnknown  
```  
  
## <a name="methods"></a>方法  
 這個介面包含下列方法：  
  
|方法|描述|  
|------------|-----------------|  
|[DefineAsyncStepInfo 方法](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedasyncmethodpropertieswriter-defineasyncstepinfo-method.md)|在目前方法中定義非同步 await 作業的群組。<br /><br /> 每個產生位移都會符合 await 的傳回指示，以識別潛在的收益。 每個 `breakpointMethod`/`breakpointOffset` 組都會識別非同步作業的繼續位置;它可能是在不同的方法中。|  
|[DefineCatchHandlerILOffset 方法](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedasyncmethodpropertieswriter-definecatchhandleriloffset-method.md)|設定編譯器所產生的 catch 處理常式（包裝非同步方法）的 IL 位移。<br /><br /> 產生之 catch 的 IL 位移會由偵錯工具用來處理 catch，就好像它是非使用者程式碼一樣，即使它可能發生在使用者程式碼方法中也一樣。 特別是，它是用來回應**CatchHandlerFound**例外狀況事件。|  
|[DefineKickoffMethod 方法](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedasyncmethodpropertieswriter-definekickoffmethod-method.md)|設定啟動非同步作業的起始方法。|  
  
## <a name="requirements"></a>需求  
 **標頭：** CorSym .idl，CorSym。h  
  
## <a name="see-also"></a>請參閱

- [診斷符號存放區介面](../../../../docs/framework/unmanaged-api/diagnostics/diagnostics-symbol-store-interfaces.md)
