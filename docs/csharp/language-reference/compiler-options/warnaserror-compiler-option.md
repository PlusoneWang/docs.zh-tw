---
title: -warnaserror (C# 編譯器選項)
ms.date: 07/20/2015
f1_keywords:
- /warnaserror
helpviewer_keywords:
- /warnaserror compiler option [C#]
- -warnaserror compiler option [C#]
- warnaserror compiler option [C#]
ms.assetid: 04680ec3-08d6-4e2e-a274-38310e10e33c
ms.openlocfilehash: 7d43941629e933ac5a9e9c9d6a1388b6194f8d99
ms.sourcegitcommit: f38e527623883b92010cf4760246203073e12898
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/20/2020
ms.locfileid: "77503485"
---
# <a name="-warnaserror-c-compiler-options"></a>-warnaserror (C# 編譯器選項)
**-warnaserror+** 選項會將所有警告都視為錯誤  
  
## <a name="syntax"></a>語法  
  
```console  
-warnaserror[+ | -][:warning-list]  
```  
  
## <a name="remarks"></a>備註  
 任何原本報告為警告的訊息都會改成報告為錯誤，並中止建置程序 (不會建置輸出檔)。  
  
 根據預設， **-warnaserror-** 會生效，這會導致無法產生輸出檔案的警告。 **-warnaserror** 與 **-warnaserror+** 相同，都會將警告視為錯誤。  
  
 選擇性，如果您只想要將少數特定警告視為錯誤，則可以指定將以逗號分隔的警告編號清單視為錯誤。 可以使用**可為 null**的速記來指定所有的可為 null 的警告集合。
  
 使用 [-warn](./warn-compiler-option.md) 指定您想要編譯器顯示的警告層級。 使用 [-nowarn](./nowarn-compiler-option.md) 停用特定警告。  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 開發環境中設定這個編譯器選項  
  
1. 開啟專案的 [屬性] 頁面。  
  
2. 按一下 [建置] 屬性頁面。  
  
3. 修改 [警告視為錯誤] 屬性。  
  
 若要以程式設計方式設定這個編譯器選項，請參閱 <xref:VSLangProj80.CSharpProjectConfigurationProperties3.TreatWarningsAsErrors>。  
  
## <a name="example"></a>範例  
 編譯 `in.cs`，並讓編譯器不要顯示任何警告：  
  
```console  
csc -warnaserror in.cs  
csc -warnaserror:642,649,652,nullable in.cs  
```  
  
## <a name="see-also"></a>另請參閱

- [C# 編譯器選項](./index.md)
- [管理專案和方案屬性](/visualstudio/ide/managing-project-and-solution-properties)
