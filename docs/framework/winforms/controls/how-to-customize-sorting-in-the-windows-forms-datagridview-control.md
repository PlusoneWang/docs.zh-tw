---
title: 自訂 DataGridView 控制項中的排序
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- sorting [Windows Forms], DataGridView control
- DataGridView control [Windows Forms], sorting
- data grids [Windows Forms], customizing sorting
ms.assetid: 92fb5c14-afab-4cf5-a97e-924fd9cb99f5
ms.openlocfilehash: 20f581b2df6fd172a0a1998aed60c56b0306f2eb
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/24/2020
ms.locfileid: "76743174"
---
# <a name="how-to-customize-sorting-in-the-windows-forms-datagridview-control"></a>如何：自訂 Windows Forms DataGridView 控制項的排序
<xref:System.Windows.Forms.DataGridView> 控制項提供自動排序，但是根據您的需求，您可能需要自訂排序作業。 例如，您可以使用程式設計排序建立替代的使用者介面 (UI)。 或者為了在排序時獲得更大的彈性，您可以處理 <xref:System.Windows.Forms.DataGridView.SortCompare> 事件或呼叫 `Sort(IComparer)` 方法的 <xref:System.Windows.Forms.DataGridView.Sort%2A> 多載，例如排序多個資料行。  
  
 下列程式碼範例示範自訂排序的三種方法。 如需詳細資訊，請參閱 [Windows Forms DataGridView 控制項中的資料行排序模式](column-sort-modes-in-the-windows-forms-datagridview-control.md)。  
  
## <a name="programmatic-sorting"></a>程式設計排序  
 下列程式碼範例示範使用 <xref:System.Windows.Forms.DataGridView.SortOrder%2A> 和 <xref:System.Windows.Forms.DataGridView.SortedColumn%2A> 屬性的程式設計排序，以決定排序的方向和 <xref:System.Windows.Forms.DataGridViewColumnHeaderCell.SortGlyphDirection%2A> 屬性來手動設定排序圖像。 `Sort(DataGridViewColumn,ListSortDirection)` 方法的 <xref:System.Windows.Forms.DataGridView.Sort%2A> 多載只用於在單一資料行排序資料。  
  
 [!code-csharp[System.Windows.Forms.DataGridViewProgrammaticSort#00](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewProgrammaticSort/CS/form1.cs#00)]
 [!code-vb[System.Windows.Forms.DataGridViewProgrammaticSort#00](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewProgrammaticSort/VB/form1.vb#00)]  
  
## <a name="custom-sorting-using-the-sortcompare-event"></a>使用 SortCompare 事件的自訂排序  
 下列程式碼範例示範使用 <xref:System.Windows.Forms.DataGridView.SortCompare> 事件處理常式自訂排序 。 所選 <xref:System.Windows.Forms.DataGridViewColumn> 已排序，若資料行中有重複的值，則 ID 資料行會用於決定最終的順序。  
  
 [!code-csharp[System.Windows.Forms.DataGridView.SortCompare#00](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.SortCompare/CS/form1.cs#00)]
 [!code-vb[System.Windows.Forms.DataGridView.SortCompare#00](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.SortCompare/VB/form1.vb#00)]  
  
## <a name="custom-sorting-using-the-icomparer-interface"></a>使用 IComparer 介面的自訂排序  
 下列程式碼範例示範使用 `Sort(IComparer)` 方法的 <xref:System.Windows.Forms.DataGridView.Sort%2A> 多載自訂排序，這會採用 <xref:System.Collections.IComparer> 介面的實作來執行多個資料行排序。  
  
 [!code-csharp[System.Windows.Forms.DataGridViewIComparerSort#00](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewIComparerSort/CS/form1.cs#00)]
 [!code-vb[System.Windows.Forms.DataGridViewIComparerSort#00](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewIComparerSort/VB/form1.vb#00)]  
  
## <a name="compiling-the-code"></a>編譯程式碼  
 這些範例需要：  
  
- System、System.Drawing 和 System.Windows.Forms 組件的參考。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Windows.Forms.DataGridView>
- [在 Windows Forms DataGridView 控制項中排序資料](sorting-data-in-the-windows-forms-datagridview-control.md)
- [Windows Forms DataGridView 控制項中的資料行排序模式](column-sort-modes-in-the-windows-forms-datagridview-control.md)
- [操作說明：設定 Windows Forms DataGridView 控制項中的資料行排序模式](set-the-sort-modes-for-columns-wf-datagridview-control.md)
