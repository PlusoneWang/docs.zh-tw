---
title: dotnet 工具還原命令
description: Dotnet 工具 restore 命令會在您的電腦上安裝目前目錄範圍內的 .NET Core 本機工具。
ms.date: 02/14/2020
ms.openlocfilehash: 2900d431987661a9232ceed10d9a424093f8be45
ms.sourcegitcommit: 771c554c84ba38cbd4ac0578324ec4cfc979cf2e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/21/2020
ms.locfileid: "77543905"
---
# <a name="dotnet-tool-restore"></a>dotnet 工具還原

**本文適用于：** ✔️ .net CORE 3.0 SDK 和更新版本

## <a name="name"></a>名稱

`dotnet tool restore`-在您的電腦上安裝目前目錄範圍內的 .NET Core 本機工具。

## <a name="synopsis"></a>概要

```dotnetcli
dotnet tool restore <PACKAGE_NAME> [--configfile] [--add-source] [tool-manifest] [--disable-parallel] [--ignore-failed-sources] [--no-cache] [-interactive] [-v|--verbosity]
dotnet tool restore <-h|--help>
```

## <a name="description"></a>描述

`dotnet tool restore` 命令會尋找位於目前目錄範圍內的工具資訊清單檔，並安裝其中列出的工具。 如需資訊清單檔的相關資訊，請參閱[安裝本機工具](global-tools.md#install-a-local-tool)和叫[用本機工具](global-tools.md#invoke-a-local-tool)。

## <a name="arguments"></a>引數

- **`PACKAGE_NAME`**

包含要安裝之 .NET Core 工具的 NuGet 套件的名稱/識別碼。

## <a name="options"></a>選項。

- **`--configfile <FILE>`**

  要使用的 NuGet 組態檔 (*nuget.config*)。

- **`--add-source <SOURCE>`**

  新增其他 NuGet 套件來源以在安裝期間使用。

- **`--tool-manifest <PATH>`**

  資訊清單檔案的路徑。

- **`--disable-parallel`**

  防止平行還原多個專案。

- **`--ignore-failed-sources`**

  將套件來源失敗視為警告。

- **`--no-cache`**

  不要快取套件和 HTTP 要求。

- **`--interactive`**

  允許命令停止並等候使用者輸入或動作 (例如完成驗證)。

- **`-h|--help`**

  印出命令的簡短說明。

- **`-v|--verbosity <LEVEL>`**

  設定命令的詳細資訊層級。 允許的值為 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。

## <a name="example"></a>範例

- **`dotnet tool restore`**

  還原目前目錄的本機工具。

## <a name="see-also"></a>另請參閱

- [.NET Core 工具](global-tools.md)
