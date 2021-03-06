---
title: 如何：呼叫事件處理常式
ms.date: 07/20/2015
helpviewer_keywords:
- Visual Basic code, procedures
- event handlers [Visual Basic], calling
- event handlers
- procedures [Visual Basic], event handlers
- procedures [Visual Basic], calling
ms.assetid: 72e18ef8-144e-40df-a1f4-066a57271e28
ms.openlocfilehash: 0c626a9ad92fe2cd0ea117a9abdd2965a09df2ea
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/22/2019
ms.locfileid: "74340419"
---
# <a name="how-to-call-an-event-handler-in-visual-basic"></a>如何：在 Visual Basic 中呼叫事件處理常式

*事件*是某些程式元件所能辨識的動作或發生的情況，例如滑鼠點擊或已超過點數限制，而您可以撰寫程式碼來回應。 *事件處理常式*是您為了回應事件而撰寫的程式碼。

 Visual Basic 中的事件處理常式是 `Sub` 程式。 不過，您通常不會以其他 `Sub` 程式的相同方式來呼叫它。 相反地，您會將程式識別為事件的處理常式。 您可以使用[Handles](../../../language-reference/statements/handles-clause.md)子句和[WithEvents](../../../language-reference/modifiers/withevents.md)變數，或使用[AddHandler 語句](../../../language-reference/statements/addhandler-statement.md)來執行這項操作。 使用 `Handles` 子句是在 Visual Basic 中宣告事件處理常式的預設方式。 當您在整合式開發環境（IDE）中進行程式設計時，這就是設計師撰寫事件處理常式的方式。 `AddHandler` 語句適用于在執行時間動態引發事件。

 當事件發生時，Visual Basic 會自動呼叫事件處理常式。 任何可存取事件的程式碼，都可以藉由執行[RaiseEvent 語句](../../../language-reference/statements/raiseevent-statement.md)來使其發生。

 您可以將一個以上的事件處理常式與同一個事件產生關聯。 在某些情況下，您可以將處理常式與事件中斷關聯。 如需詳細資訊，請參閱 [事件](../events/index.md)中定義的介面的私用 C++ 專屬實作。

### <a name="to-call-an-event-handler-using-handles-and-withevents"></a>使用控制碼和 WithEvents 呼叫事件處理常式

1. 請確定事件是以[事件語句](../../../language-reference/statements/event-statement.md)宣告。

2. 使用[WithEvents](../../../language-reference/modifiers/withevents.md)關鍵字，在模組或類別層級宣告物件變數。 這個變數的 `As` 子句必須指定引發事件的類別。

3. 在事件處理 `Sub` 程式的宣告中，加入指定 `WithEvents` 變數和事件名稱的[控制碼](../../../language-reference/statements/handles-clause.md)子句。

4. 當事件發生時，Visual Basic 會自動呼叫 `Sub` 程式。 您的程式碼可以使用 `RaiseEvent` 語句來進行事件。

     下列範例會定義事件，以及參考引發事件之類別的 `WithEvents` 變數。 事件處理 `Sub` 程式會使用 `Handles` 子句來指定它所處理的類別和事件。

     [!code-vb[VbVbcnProcedures#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#4)]

### <a name="to-call-an-event-handler-using-addhandler"></a>使用 AddHandler 呼叫事件處理常式

1. 請確定事件是使用 `Event` 語句來宣告。

2. 執行[AddHandler 語句](../../../language-reference/statements/addhandler-statement.md)，以動態方式將事件處理 `Sub` 程式與事件連接。

3. 當事件發生時，Visual Basic 會自動呼叫 `Sub` 程式。 您的程式碼可以使用 `RaiseEvent` 語句來進行事件。

     下列範例會定義 `Sub` 程式，以處理表單的 <xref:System.Windows.Forms.Form.Closing> 事件。 然後，它會使用[AddHandler 語句](../../../language-reference/statements/addhandler-statement.md)，將 `catchClose` 程式與 <xref:System.Windows.Forms.Form.Closing>的事件處理常式產生關聯。

     [!code-vb[VbVbcnProcedures#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#5)]

     您可以藉由執行[RemoveHandler 語句](../../../language-reference/statements/removehandler-statement.md)，將事件處理常式與事件中斷關聯。

## <a name="see-also"></a>請參閱

- [程序](index.md)
- [Sub 程序](sub-procedures.md)
- [Sub 陳述式](../../../language-reference/statements/sub-statement.md)
- [AddressOf 運算子](../../../language-reference/operators/addressof-operator.md)
- [如何：建立程序](how-to-create-a-procedure.md)
- [如何：呼叫不傳回值的程序](how-to-call-a-procedure-that-does-not-return-a-value.md)
