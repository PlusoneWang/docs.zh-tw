---
title: Visual Studio 中的偵錯運算式樹狀架構 (C#)
ms.date: 07/20/2015
ms.assetid: 1369fa25-0fbd-4b92-98d0-8df79c49c27a
ms.openlocfilehash: 30f538712881e41b4fd0e62d06f74373d755ea40
ms.sourcegitcommit: 5a28f8eb071fcc09b045b0c4ae4b96898673192e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/31/2019
ms.locfileid: "73195679"
---
# <a name="debugging-expression-trees-in-visual-studio-c"></a>Visual Studio 中的偵錯運算式樹狀架構 (C#)
當您針對應用程式進行偵錯時，可以分析運算式樹狀架構的結構與內容。 若要取得運算式樹狀架構的快速概觀，您可以使用 `DebugView` 屬性，其代表[使用特殊語法](debugview-syntax.md)的運算式樹狀架構。 (請注意，`DebugView` 僅適用於偵錯模式。)  

![VS 偵錯工具中運算式樹狀架構 DebugView 的螢幕擷取畫面。](media/debugging-expression-trees-in-visual-studio/debugview-expression-tree.png)

由於 `DebugView` 是字串，所以您可以使用[內建的文字視覺化檢視](https://docs.microsoft.com/visualstudio/debugger/view-strings-visualizer#open-a-string-visualizer)跨多行檢視它，請從 `DebugView` 標籤旁的放大鏡圖示選取 [文字視覺化檢視]。

 ![套用至 DebugView 結果的文字視覺化檢視螢幕擷取畫面。](media/debugging-expression-trees-in-visual-studio/string-visualizer-debugview.png)

或者，您可以安裝並使用適用於運算式樹狀架構的[自訂視覺化檢視](https://docs.microsoft.com/visualstudio/debugger/create-custom-visualizers-of-data)，例如：

- [可讀取的運算式](https://github.com/agileobjects/ReadableExpressions) ([MIT 授權](https://github.com/agileobjects/ReadableExpressions/blob/master/LICENSE.md)，位於 [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=vs-publisher-1232914.ReadableExpressionsVisualizers))，將運算式樹狀架構轉譯為 C# 程式碼：

  ![可讀取的運算式視覺化檢視的螢幕擷取畫面。](media/debugging-expression-trees-in-visual-studio/readable-expressions-visualizer.png)

- [運算式樹狀架構視覺化檢視](https://github.com/zspitz/ExpressionToString#visual-studio-debugger-visualizer-for-expression-trees) ([MIT 授權](https://github.com/zspitz/ExpressionToString/blob/master/LICENSE))，提供運算式樹狀架構的圖形檢視、其屬性和相關物件：

  ![運算式樹狀架構視覺化檢視的螢幕擷取畫面。](media/debugging-expression-trees-in-visual-studio/expression-to-string-visualizer.png)

### <a name="to-open-a-visualizer-for-an-expression-tree"></a>開啟運算式樹狀架構的視覺化檢視  
  
1. 在 [DataTips]、[監看式] 視窗、[自動變數] 視窗或 [區域變數] 視窗中，按一下出現在運算式樹狀架構旁邊的放大鏡圖示。  

    可用的視覺化檢視清單隨即顯示： 

    ![螢幕擷取畫面，顯示從 Visual Studio 開啟視覺化檢視。](media/debugging-expression-trees-in-visual-studio/expression-tree-visualizers.png)

2. 按一下要使用的視覺化檢視。  
  
## <a name="see-also"></a>請參閱

- [運算式樹狀結構 (C#)](./index.md)
- [Visual Studio 偵錯](/visualstudio/debugger/debugger-feature-tour)
- [建立自訂視覺化檢視](/visualstudio/debugger/create-custom-visualizers-of-data)
- [`DebugView` 語法](debugview-syntax.md)
