---
title: 適用于 <add> 的 <filter> 元素 <sharedListeners>
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/sharedListeners/add/filter
helpviewer_keywords:
- filter element for <add> for <sharedListeners>
- initializeData attribute
- <filter> element for <add> for <sharedListeners>
- filters, trace listeners
- trace listeners, filters
ms.assetid: 7d4e7faa-2e4e-4379-ac76-f6cd7f2f8fac
ms.openlocfilehash: e04ecd773bd6aa7791858711edbd72128dc391ea
ms.sourcegitcommit: 7f8eeef060ddeb2cabfa52843776faf652c5a1f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/14/2019
ms.locfileid: "74088873"
---
# <a name="filter-element-for-add-for-sharedlisteners"></a>針對 \<s 的 \<新增 > \<篩選 > 元素 >
將篩選新增至 `sharedListeners` 集合中的接聽項。  

[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<系統診斷 >** ](system-diagnostics-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<s >** ](sharedlisteners-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<新增 >** ](add-element-for-sharedlisteners.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<篩選 >**

## <a name="syntax"></a>語法  
  
```xml  
<filter type="System.Diagnostics.EventTypeFilter"   
  initializeData="Warning" />  
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  
 下列各節描述屬性、子項目和父項目。  
  
### <a name="attributes"></a>屬性  
  
|屬性|描述|  
|---------------|-----------------|  
|**type**|必要屬性。<br /><br /> 指定篩選準則的類型。 您只能使用類型的完整名稱（以 <xref:System.Type.FullName%2A?displayProperty=nameWithType> 屬性的格式），也可以使用包含元件資訊的完整型別名稱（以 <xref:System.Type.AssemblyQualifiedName%2A?displayProperty=nameWithType> 屬性的格式）。 如需建立完整型別名稱的相關資訊，請參閱[指定完整的型別名稱](../../../reflection-and-codedom/specifying-fully-qualified-type-names.md)。|  
|**initializeData**|選擇性屬性。<br /><br /> 傳遞至指定類別之函數的字串。|  
  
### <a name="child-elements"></a>子項目  
 無。  
  
### <a name="parent-elements"></a>父項目  
  
|項目|描述|  
|-------------|-----------------|  
|`configuration`|通用語言執行平台和 .NET Framework 應用程式所使用之每個組態檔中的根項目。|  
|`system.diagnostics`|指定用於收集、儲存及路由傳送訊息的追蹤接聽項，以及設定追蹤參數的層級。|  
|`sharedListeners`|任何來源或追蹤元素可以參考的接聽程式集合。|  
|`add`|將接聽程式加入至**s**集合。|  
  
## <a name="remarks"></a>備註  
 如果接聽程式是在 `<sharedListeners>` 專案的 `<add>` 專案中定義，則該接聽程式的篩選器應定義于屬於 `<add>` 專案子系的 `<filter>` 元素中。  
  
 此元素可用於電腦設定檔（Machine.config）和應用程式佈建檔。  
  
## <a name="example"></a>範例  
 下列範例顯示如何使用 `<filter>` 專案，將篩選加入至 `sharedListeners` 集合中的追蹤接聽項 `console`。  
  
```xml  
<configuration>  
  <system.diagnostics>  
    <sources>  
      <source name="myTraceSource" >  
        <listeners>  
          <add name="console" />  
          <remove name="Default" />  
        </listeners>  
      </source>  
    </sources>  
    <sharedListeners>  
      <add name="console"   
        type="System.Diagnostics.ConsoleTraceListener" >  
        <filter type="System.Diagnostics.EventTypeFilter"   
          initializeData="Error" />  
      </add>  
    </sharedListeners>  
  </system.diagnostics>  
</configuration>  
```  
  
## <a name="see-also"></a>請參閱

- <xref:System.Diagnostics.TraceFilter>
- <xref:System.Diagnostics.TraceListener>
- <xref:System.Diagnostics.TraceSource>
- [追蹤和偵錯設定結構描述](index.md)
