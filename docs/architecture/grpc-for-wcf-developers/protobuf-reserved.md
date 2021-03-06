---
title: Protobuf 保留的欄位-WCF 開發人員的 gRPC
description: 瞭解跨版本相容性的保留字段。
ms.date: 09/09/2019
ms.openlocfilehash: 50082a1aab2e7707a1839b9d56455124a9e4a6a1
ms.sourcegitcommit: 771c554c84ba38cbd4ac0578324ec4cfc979cf2e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/21/2020
ms.locfileid: "77542972"
---
# <a name="protobuf-reserved-fields"></a>Protobuf 保留欄位

通訊協定緩衝區（Protobuf）中的回溯相容性保證會依賴欄位號碼，一律代表相同的資料項目。 如果從新的服務版本中的訊息移除欄位，則永遠不應重複使用該欄位編號。 您可以使用 `reserved` 關鍵字來強制執行此項。 

如果 [`displayName`] 和 [`marketId`] 欄位已從先前定義的 `Stock` 訊息中移除，則應保留其欄位號碼，如下列範例所示。

```protobuf
syntax "proto3";

message Stock {

    reserved 3, 4;
    int32 id = 1;
    string symbol = 2;

}
```

您也可以使用 `reserved` 關鍵字做為未來可能加入之欄位的預留位置。 您可以使用 `to` 關鍵字，將連續的域編號表達為範圍。

```protobuf
syntax "proto3";

message Info {

    reserved 2, 9 to 11, 15;
    // ...
}
```

>[!div class="step-by-step"]
>[上一頁](protobuf-repeated.md)
>[下一頁](protobuf-any-oneof.md)
