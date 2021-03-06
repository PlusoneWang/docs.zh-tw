---
title: 概觀
ms.date: 12/13/2019
description: Microsoft 資料 Sqlite 的總覽
ms.openlocfilehash: e84c68f0615f187e8dea7ab87ac917c0ad796a1c
ms.sourcegitcommit: 771c554c84ba38cbd4ac0578324ec4cfc979cf2e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/21/2020
ms.locfileid: "77543595"
---
# <a name="microsoftdatasqlite-overview"></a>Microsoft. Data Sqlite 總覽

Sqlite 是適用于 SQLite 的輕量[ADO.NET](../../../framework/data/adonet/index.md)提供者。 SQLite 的[Entity Framework Core](/ef/core/)提供者是以這個程式庫為基礎。 不過，它也可以單獨使用，或與其他資料存取程式庫搭配使用。

## <a name="installation"></a>安裝

最新的穩定版本可在[NuGet](https://www.nuget.org/packages/Microsoft.Data.Sqlite)上取得。

### <a name="net-core-cli"></a>[.NET Core CLI](#tab/netcore-cli)

```dotnetcli
dotnet add package Microsoft.Data.Sqlite
```

### <a name="visual-studio"></a>[Visual Studio](#tab/visual-studio)

``` PowerShell
Install-Package Microsoft.Data.Sqlite
```

---

## <a name="usage"></a>使用量

此程式庫會針對連接、命令、資料讀取器等，執行常見的 ADO.NET 抽象概念。

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/HelloWorldSample/Program.cs?name=snippet_HelloWorld)]

## <a name="see-also"></a>另請參閱

* [連接字串](connection-strings.md)
* [API 參考](/dotnet/api/?view=msdata-sqlite-3.0)
* [SQL 語法](https://www.sqlite.org/lang.html)
