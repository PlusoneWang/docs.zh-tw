---
title: ICorDebugModule2::ApplyChanges 方法
ms.date: 03/30/2017
api_name:
- ICorDebugModule2.ApplyChanges
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugModule2::ApplyChanges
helpviewer_keywords:
- ApplyChanges method [.NET Framework debugging]
- ICorDebugModule2::ApplyChanges method [.NET Framework debugging]
ms.assetid: 96fa3406-6a6f-41a1-88c6-d9bc5d1a16d1
topic_type:
- apiref
ms.openlocfilehash: c324019e1e62701f4f2aaba1c00948b292ba6847
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/30/2019
ms.locfileid: "73127904"
---
# <a name="icordebugmodule2applychanges-method"></a>ICorDebugModule2::ApplyChanges 方法
將中繼資料中的變更和 Microsoft 中繼語言（MSIL）程式碼中的變更套用至執行中的進程。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT ApplyChanges (  
    [in] ULONG                       cbMetadata,  
    [in, size_is(cbMetadata)] BYTE   pbMetadata[],  
    [in] ULONG                       cbIL,  
    [in, size_is(cbIL)] BYTE         pbIL[]  
);  
```  
  
## <a name="parameters"></a>參數  
 `cbMetadata`  
 在差異中繼資料的大小（以位元組為單位）。  
  
 `pbMetadata`  
 在包含差異中繼資料的緩衝區。 緩衝區的位址會從[IMetaDataEmit2：： SaveDeltaToMemory](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-savedeltatomemory-method.md)方法傳回。  
  
 中繼資料中的相對虛擬位址（Rva）應該相對於 MSIL 程式碼的開頭。  
  
 `cbIL`  
 在差異 MSIL 程式碼的大小（以位元組為單位）。  
  
 `pbIL`  
 在包含更新的 MSIL 程式碼的緩衝區。  
  
## <a name="remarks"></a>備註  
 `pbMetadata` 參數是特殊的差異元資料格式（如[IMetaDataEmit2：： SaveDeltaToMemory](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-savedeltatomemory-method.md)所輸出）。 `pbMetadata` 會將先前的中繼資料當做基底，並描述要套用至該基底的個別變更。  
  
 相反地，`pbIL[`] 參數包含新的 MSIL 做為已更新的方法，其目的是要完全取代該方法先前的 MSIL  
  
 在偵錯工具的記憶體中建立 delta MSIL 和中繼資料時，偵錯工具會呼叫 `ApplyChanges` 將變更傳送至 common language runtime （CLR）。 執行時間會更新其中繼資料資料表，將新的 MSIL 放在進程中，並設定新 MSIL 的即時（JIT）編譯。 套用變更之後，偵錯工具應該呼叫[IMetaDataEmit2：： ResetENCLog](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-resetenclog-method.md)來準備下一個編輯會話。 偵錯工具可能會繼續處理。  
  
 每當偵錯工具在具有 delta 中繼資料的模組上呼叫 `ApplyChanges` 時，它也應該在該模組中繼資料的所有複本上，使用相同的差異中繼資料來呼叫[IMetaDataEmit：： ApplyEditAndContinue](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-applyeditandcontinue-method.md) ，但用來發出變更的複本除外。 如果中繼資料的複本與實際的中繼資料有某種的同步，則偵錯工具一律會擲回該複本並取得新的複本。  
  
 如果 `ApplyChanges` 方法失敗，則 debug 會話會處於無效狀態，而且必須重新開機。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **標頭：** CorDebug.idl、CorDebug.h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET framework 版本：** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
