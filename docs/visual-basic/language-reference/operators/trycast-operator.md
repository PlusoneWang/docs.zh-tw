---
title: TryCast 運算子
ms.date: 07/20/2015
f1_keywords:
- vb.trycast
- trycast
helpviewer_keywords:
- TryCast keyword [Visual Basic]
ms.assetid: d1ef5d47-fef4-491e-b014-1d910628f65c
ms.openlocfilehash: 53306575cfc385039be3939fd87cf993b4509af4
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/22/2019
ms.locfileid: "74348205"
---
# <a name="trycast-operator-visual-basic"></a>TryCast 運算子 (Visual Basic)
引進不會擲回例外狀況的類型轉換作業。  
  
## <a name="remarks"></a>備註  
 如果嘗試的轉換失敗，`CType` 和 `DirectCast` 都會擲回 <xref:System.InvalidCastException> 錯誤。 這可能會對應用程式的效能造成不良影響。 `TryCast` 不會傳回[任何內容](../../../visual-basic/language-reference/nothing.md)，因此您只需要針對 `Nothing`測試傳回的結果，而不需處理可能的例外狀況。  
  
 使用 `TryCast` 關鍵字的方式與使用[CType 函數](../../../visual-basic/language-reference/functions/ctype-function.md)和[DirectCast Operator](../../../visual-basic/language-reference/operators/directcast-operator.md)關鍵字相同。 您會提供運算式做為第一個引數，以及要將它轉換成做為第二個引數的類型。 `TryCast` 只會在參考型別上運作，例如類別和介面。 它需要兩個類型之間的繼承或實現關聯性。 這表示一種類型必須繼承或執行另一個。  
  
## <a name="errors-and-failures"></a>錯誤和失敗  
 如果 `TryCast` 偵測到沒有繼承或實現關聯性存在，則會產生編譯器錯誤。 但是缺少編譯器錯誤並不保證轉換成功。 如果想要的轉換縮小，可能會在執行時間失敗。 如果發生這種情況，`TryCast` 不會傳回[任何內容](../../../visual-basic/language-reference/nothing.md)。  
  
## <a name="conversion-keywords"></a>轉換關鍵字  
 類型轉換關鍵字的比較如下所示。  
  
|關鍵字|資料類型|引數關聯性|運行時失敗|  
|---|---|---|---|  
|[CType 函式](../../../visual-basic/language-reference/functions/ctype-function.md)|任何資料類型|必須在兩個資料類型之間定義擴展或縮小轉換|擲回 <xref:System.InvalidCastException>|  
|[DirectCast 運算子](../../../visual-basic/language-reference/operators/directcast-operator.md)|任何資料類型|一種類型必須繼承自或執行另一個類型|擲回 <xref:System.InvalidCastException>|  
|`TryCast`|僅限參考型別|一種類型必須繼承自或執行另一個類型|不傳回[任何內容](../../../visual-basic/language-reference/nothing.md)|  
  
## <a name="example"></a>範例  
 下列範例示範如何使用 `TryCast`。  
  
 [!code-vb[VbVbalrKeywords#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrKeywords/VB/Class1.vb#6)]  
  
## <a name="see-also"></a>請參閱

- [擴展和縮小轉換](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)
- [隱含和明確轉換](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)
