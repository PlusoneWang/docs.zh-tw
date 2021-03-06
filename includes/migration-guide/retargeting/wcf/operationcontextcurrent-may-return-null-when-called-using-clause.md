---
ms.openlocfilehash: 62ba525a28960d96c5458aa1481e1f319d5bc875
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2019
ms.locfileid: "67859334"
---
### <a name="operationcontextcurrent-may-return-null-when-called-in-a-using-clause"></a>OperationContext.Current 在 using 子句中進行呼叫時，可能會傳回 Null

|   |   |
|---|---|
|詳細資料|如果符合下列所有條件，則 <xref:System.ServiceModel.OperationContext.Current?displayProperty=nameWithType> 可能會傳回 <code>null</code>，而且可能會導致 <xref:System.NullReferenceException>：<ul><li>擷取傳回 <xref:System.Threading.Tasks.Task> 或 <xref:System.Threading.Tasks.Task%601> 的方法中 <xref:System.ServiceModel.OperationContext.Current?displayProperty=nameWithType> 屬性的值。</li><li>具現化 <code>using</code> 子句中的 <xref:System.ServiceModel.OperationContextScope> 物件。</li><li>擷取 <code>using statement</code> 內 <xref:System.ServiceModel.OperationContext.Current?displayProperty=nameWithType> 屬性的值。 例如：</li></ul><pre><code class="lang-csharp">using (new OperationContextScope(OperationContext.Current))&#13;&#10;{&#13;&#10;OperationContext context = OperationContext.Current;      // OperationContext.Current is null.&#13;&#10;// ...&#13;&#10;}&#13;&#10;</code></pre>|
|建議|若要解決此問題，您可執行以下動作：<ul><li>如下所示修改您的程式碼，以具現化新的非 <code>null</code> <xref:System.ServiceModel.OperationContext.Current%2A> 物件：</li></ul><pre><code class="lang-csharp">OperationContext ocx = OperationContext.Current;&#13;&#10;using (new OperationContextScope(OperationContext.Current))&#13;&#10;{&#13;&#10;OperationContext.Current = new OperationContext(ocx.Channel);&#13;&#10;// ...&#13;&#10;}&#13;&#10;</code></pre><ul><li>安裝 .NET Framework 4.6.2 的最新更新，或升級至更新版本的 .NET Framework。 這會停用 <xref:System.ServiceModel.OperationContext.Current?displayProperty=nameWithType> 中的 <xref:System.Threading.ExecutionContext> 流程，並還原 WCF 應用程式在 .NET Framework 4.6.1 和舊版中的行為。 這是可設定的行為；相當於在您的組態檔中新增下列應用程式設定：</li></ul><pre><code class="lang-xml">&lt;appSettings&gt;&#13;&#10;&lt;add key=&quot;Switch.System.ServiceModel.DisableOperationContextAsyncFlow&quot; value=&quot;true&quot; /&gt;&#13;&#10;&lt;/appSettings&gt;&#13;&#10;</code></pre>如果這項變更並不適當，且您的應用程式相依於作業內容之間流動的執行內容，您可以啟用其流程，如下所示：<pre><code class="lang-xml">&lt;appSettings&gt;&#13;&#10;&lt;add key=&quot;Switch.System.ServiceModel.DisableOperationContextAsyncFlow&quot; value=&quot;false&quot; /&gt;&#13;&#10;&lt;/appSettings&gt;&#13;&#10;</code></pre>|
|範圍|Edge|
|版本|4.6.2|
|類型|正在重定目標|
|受影響的 API|<ul><li><xref:System.ServiceModel.OperationContext.Current?displayProperty=nameWithType></li></ul>|

