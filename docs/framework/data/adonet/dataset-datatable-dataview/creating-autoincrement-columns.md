---
title: 建立自動遞增資料行
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: cf09732a-ab54-4d98-89e2-4d0a1f28fbce
ms.openlocfilehash: 5e4a36829107480a44980c7210b39c21231c67f4
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/07/2019
ms.locfileid: "70786449"
---
# <a name="creating-autoincrement-columns"></a>建立自動遞增資料行
若要確保資料行的值是唯一的，您可以在將新資料列加入至資料表時，將資料行值設為自動累加。 若要建立自動遞增<xref:System.Data.DataColumn>，請<xref:System.Data.DataColumn.AutoIncrement%2A>將資料行的屬性設定為**true**。 接著會以<xref:System.Data.DataColumn.AutoIncrementSeed%2A>屬性中定義的值為開頭，而且每個資料列加上**自動遞增**資料行的值，都會隨著資料行<xref:System.Data.DataColumn.AutoIncrementStep%2A>的屬性中所定義的值而增加。 <xref:System.Data.DataColumn>  
  
 針對**自動遞增**資料行，我們建議<xref:System.Data.DataColumn.ReadOnly%2A>將**DataColumn**的屬性設定為**true**。  
  
 下列範例示範如何建立以 200 值做為開頭的資料行，並以增量 3 累加。  
  
```vb  
Dim workColumn As DataColumn = workTable.Columns.Add( _  
    "CustomerID", typeof(Int32))  
workColumn.AutoIncrement = true  
workColumn.AutoIncrementSeed = 200  
workColumn.AutoIncrementStep = 3  
```  
  
```csharp  
DataColumn workColumn = workTable.Columns.Add(  
    "CustomerID", typeof(Int32));  
workColumn.AutoIncrement = true;  
workColumn.AutoIncrementSeed = 200;  
workColumn.AutoIncrementStep = 3;  
```  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Data.DataColumn>
- [DataTable 結構描述定義](datatable-schema-definition.md)
- [DataTable](datatables.md)
- [ADO.NET 概觀](../ado-net-overview.md)
