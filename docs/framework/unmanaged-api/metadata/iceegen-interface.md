---
title: ICeeGen 介面
ms.date: 03/30/2017
api_name:
- ICeeGen
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICeeGen
helpviewer_keywords:
- ICeeGen interface [.NET Framework metadata]
ms.assetid: 383d20b0-efe9-4e71-8fb8-1186b2e7d0c0
topic_type:
- apiref
ms.openlocfilehash: ae3c372951de00b097d0a8437039a3a85bf3aabf
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/23/2019
ms.locfileid: "74426159"
---
# <a name="iceegen-interface"></a>ICeeGen 介面
提供動態程式碼編譯的方法。  
  
 這個介面已過時，不應使用。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|[AddSectionReloc 方法](../../../../docs/framework/unmanaged-api/metadata/iceegen-addsectionreloc-method.md)|已過時。 將 reloc 指令新增至程式碼基底。|  
|[AllocateMethodBuffer 方法](../../../../docs/framework/unmanaged-api/metadata/iceegen-allocatemethodbuffer-method.md)|已過時。 為方法建立指定大小的緩衝區，並取得方法的相對虛擬位址。|  
|[ComputePointer 方法](../../../../docs/framework/unmanaged-api/metadata/iceegen-computepointer-method.md)|已過時。 判斷指定之程式碼區段的緩衝區。|  
|[EmitString 方法](../../../../docs/framework/unmanaged-api/metadata/iceegen-emitstring-method.md)|已過時。 將指定的字串發出至程式碼基底。|  
|[GenerateCeeFile 方法](../../../../docs/framework/unmanaged-api/metadata/iceegen-generateceefile-method.md)|已過時。 產生程式碼基底檔案，其中包含目前載入此 `ICeeGen`的程式碼基底。|  
|[GenerateCeeMemoryImage 方法](../../../../docs/framework/unmanaged-api/metadata/iceegen-generateceememoryimage-method.md)|已過時。 在記憶體中產生程式碼基底的影像。|  
|[GetIlSection 方法](../../../../docs/framework/unmanaged-api/metadata/iceegen-getilsection-method.md)|已過時。 取得指定控制碼所參考之中繼語言程式碼基底的區段。|  
|[GetIMapTokenIface 方法](../../../../docs/framework/unmanaged-api/metadata/iceegen-getimaptokeniface-method.md)|已過時。 取得指定之標記所參考的介面。|  
|[GetMethodBuffer 方法](../../../../docs/framework/unmanaged-api/metadata/iceegen-getmethodbuffer-method.md)|已過時。 取得在指定的相對虛擬位址上，方法之適當大小的緩衝區。|  
|[GetSectionBlock 方法](../../../../docs/framework/unmanaged-api/metadata/iceegen-getsectionblock-method.md)|已過時。 取得程式碼基底的區段區塊。|  
|[GetSectionCreate 方法](../../../../docs/framework/unmanaged-api/metadata/iceegen-getsectioncreate-method.md)|已過時。 使用指定的名稱和旗標值，產生並取得程式碼區段。|  
|[GetSectionDataLen 方法](../../../../docs/framework/unmanaged-api/metadata/iceegen-getsectiondatalen-method.md)|已過時。 取得指定區段的長度。|  
|[GetString 方法](../../../../docs/framework/unmanaged-api/metadata/iceegen-getstring-method.md)|已過時。 取得儲存在指定之相對虛擬位址的字串。|  
|[GetStringSection 方法](../../../../docs/framework/unmanaged-api/metadata/iceegen-getstringsection-method.md)|已過時。 取得指定控制碼所參考之程式碼區段的字串表示。|  
|[TruncateSection 方法](../../../../docs/framework/unmanaged-api/metadata/iceegen-truncatesection-method.md)|已過時。 依指定的長度截斷指定的程式碼區段。|  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **標頭：** Cor。h  
  
 連結**庫：** 做為 Mscoree.dll 中的資源使用  
  
 **.NET framework 版本：** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>請參閱

- [中繼資料介面](../../../../docs/framework/unmanaged-api/metadata/metadata-interfaces.md)
