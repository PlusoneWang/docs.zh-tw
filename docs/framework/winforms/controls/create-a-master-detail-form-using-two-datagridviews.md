---
title: 使用兩個 DataGridView 控制項建立主版詳細資料表單
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DataGridView control [Windows Forms], master/detail form
- parent-child tables [Windows Forms], displaying on Windows Forms
- master-details lists [Windows Forms], creating
ms.assetid: 99f6e876-3f7f-4139-9063-e36587c95b02
ms.openlocfilehash: d317f4e592790c9b48b539b1601814569e14529f
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/24/2020
ms.locfileid: "76737328"
---
# <a name="how-to-create-a-masterdetail-form-using-two-windows-forms-datagridview-controls"></a>如何：使用兩個 Windows Form DataGridView 控制項建立主從式表單
下列程式碼範例會使用兩個 <xref:System.Windows.Forms.DataGridView> 控制項繫結至兩個 <xref:System.Windows.Forms.BindingSource> 元件來建立主從式表單。 資料來源是 <xref:System.Data.DataSet>，包含來自 Northwind SQL Server 範例資料庫的 `Customers` 和 `Orders` 資料表，以及透過 <xref:System.Data.DataRelation> 資料行和這兩者產生關聯的 `CustomerID`。  
  
 一個 <xref:System.Windows.Forms.BindingSource> 會繫結至資料集中的父代 `Customers` 資料表。 此資料會顯示在 <xref:System.Windows.Forms.DataGridView> 主控制項。 其他 <xref:System.Windows.Forms.BindingSource> 會繫結程序至第一個資料連接器。 第二個 <xref:System.Windows.Forms.BindingSource.DataMember%2A> 的 <xref:System.Windows.Forms.BindingSource> 屬性會設為 <xref:System.Data.DataRelation> 的名稱。 這會導致相關的 <xref:System.Windows.Forms.DataGridView> 詳細資料控制項顯示 `Orders` 子資料表的資料列，對應到 <xref:System.Windows.Forms.DataGridView> 主控制項中的目前資料列。  
  
 如需此程式碼範例的完整說明，請參閱[逐步解說：使用兩個 Windows Forms DataGridView 控制項建立主要/詳細表單](creating-a-master-detail-form-using-two-datagridviews.md)。  
  
## <a name="example"></a>範例  
 [!code-csharp[System.Windows.Forms.DataGridViewMasterDetails#00](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMasterDetails/CS/masterdetails.cs#00)]
 [!code-vb[System.Windows.Forms.DataGridViewMasterDetails#00](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMasterDetails/VB/masterdetails.vb#00)]  
  
## <a name="compiling-the-code"></a>編譯程式碼  
 這個範例需要：  
  
 System、System.Data、System.Windows.Forms 和 System.XML 組件的參考。  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 在連接字串內儲存機密資訊 (例如密碼) 會影響應用程式的安全性。 使用 Windows 驗證 (也稱為整合式安全性) 是控制資料庫存取的更安全方式。 如需詳細資訊，請參閱[保護連線資訊](../../data/adonet/protecting-connection-information.md)。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.BindingSource>
- [逐步解說：使用兩個 Windows Forms DataGridView 控制項建立主從式表單](creating-a-master-detail-form-using-two-datagridviews.md)
- [在 Windows Forms DataGridView 控制項中顯示資料](displaying-data-in-the-windows-forms-datagridview-control.md)
- [保護連線資訊](../../data/adonet/protecting-connection-information.md)
