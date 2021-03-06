---
title: <remarks> - C#程式設計指南
ms.date: 07/20/2015
f1_keywords:
- remarks
- <remarks>
helpviewer_keywords:
- remarks C# XML tag
- <remarks> C# XML tag
ms.assetid: f8641391-31f3-4735-af7a-c502a5b6a251
ms.openlocfilehash: e37dac9cb9fed1df6ca027f09f2c95dbbc8ea66d
ms.sourcegitcommit: 13e79efdbd589cad6b1de634f5d6b1262b12ab01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/28/2020
ms.locfileid: "76793378"
---
# <a name="remarks-c-programming-guide"></a>\<備註 > （C#程式設計手冊）

## <a name="syntax"></a>語法

```xml
<remarks>description</remarks>
```

## <a name="parameters"></a>參數

- `Description`

  成員的描述。

## <a name="remarks"></a>備註

\<remarks> 標記是用來新增類型的資訊，以補充使用 [\<summary>](./summary.md) 所指定的資訊。 這項資訊會顯示在 [物件瀏覽器] 視窗中。

使用 [-doc](../../language-reference/compiler-options/doc-compiler-option.md) 編譯可處理檔案的文件註解。

## <a name="example"></a>範例

[!code-csharp[csProgGuideDocComments#9](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDocComments/CS/DocComments.cs#9)]

## <a name="see-also"></a>請參閱

- [C# 程式設計指南](../index.md)
- [建議使用的檔註解標記](./recommended-tags-for-documentation-comments.md)
