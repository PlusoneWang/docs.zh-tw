---
title: schemeSettings 的 <add> 項目 (URI 設定)
ms.date: 03/30/2017
ms.assetid: 594a7b3b-af23-4cfa-b616-0b2dddb1a705
ms.openlocfilehash: ed40098e8d4c2d1298771e67a618b8d04f59c912
ms.sourcegitcommit: 7f8eeef060ddeb2cabfa52843776faf652c5a1f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/14/2019
ms.locfileid: "74087722"
---
# <a name="add-element-for-schemesettings-uri-settings"></a>\<為 Schemesettings 專案新增 > 元素（Uri 設定）
新增配置名稱的配置設定。  

[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<uri >** ](uri-element-uri-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<schemesettings 專案 >** ](schemesettings-element-uri-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\<**新增 >**

## <a name="syntax"></a>語法  
  
```xml  
<add
  name="http|https"
  genericUriParserOptions="DontUnescapePathDotsAndSlashes"
/>  
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  
 下列各節說明屬性、子元素和父元素  
  
### <a name="attributes"></a>屬性  
  
|屬性|描述|  
|---------------|-----------------|  
|NAME|套用此設定的配置名稱。 唯一支援的值為 name = "HTTP" 和 name = "HTTPs"。|  
  
## <a name="attribute-name-attribute"></a>{屬性名稱}特性  
  
|值|描述|  
|-----------|-----------------|  
|genericUriParserOptions|此配置的剖析器選項。 唯一支援的值為 genericUriParserOptions = "DontUnescapePathDotsAndSlashes"。|  
  
### <a name="child-elements"></a>子項目  
 None  
  
### <a name="parent-elements"></a>父項目  
  
|項目|描述|  
|-------------|-----------------|  
|[\<schemeSettings> 項目 (URI 設定)](schemesettings-element-uri-settings.md)|指定如何針對特定配置剖析 <xref:System.Uri>。|  
  
## <a name="remarks"></a>備註  
 根據預設，<xref:System.Uri?displayProperty=nameWithType> 類別會在執行路徑壓縮之前取消轉義百分比編碼的路徑分隔符號。 這會實作為安全性機制來對抗下列攻擊：  
  
 `http://www.contoso.com/..%2F..%2F/Windows/System32/cmd.exe?/c+dir+c:\`  
  
 如果將此 URI 向下傳遞至未正確處理百分比編碼字元的模組，可能會導致伺服器執行下列命令：  
  
 `c:\Windows\System32\cmd.exe /c dir c:\`  
  
 基於這個理由，<xref:System.Uri?displayProperty=nameWithType> 類別會先取消轉義路徑分隔符號，然後套用路徑壓縮。 將上述惡意 URL 傳遞給 <xref:System.Uri?displayProperty=nameWithType> 類別的函式，會產生下列 URI：  
  
 `http://www.microsoft.com/Windows/System32/cmd.exe?/c+dir+c:\`  
  
 您可以使用特定配置的 Schemesettings 專案設定選項，修改這個預設行為，而不要解除轉義百分比編碼的路徑分隔符號。  
  
## <a name="configuration-files"></a>組態檔  
 此項目可以用於應用程式組態檔或電腦組態檔 (Machine.config)。  
  
## <a name="example"></a>範例  
 下列範例示範 <xref:System.Uri> 類別所使用的設定，以支援不要將 HTTP 配置的百分比編碼路徑分隔符號進行轉義。  
  
```xml  
<configuration>  
  <uri>  
    <schemeSettings>  
      <add name="http" genericUriParserOptions="DontUnescapePathDotsAndSlashes"/>  
    </schemeSettings>  
  </uri>  
</configuration>  
```  
  
## <a name="see-also"></a>請參閱

- <xref:System.Configuration.SchemeSettingElement?displayProperty=nameWithType>
- <xref:System.Configuration.SchemeSettingElementCollection?displayProperty=nameWithType>
- <xref:System.Configuration.UriSection?displayProperty=nameWithType>
- <xref:System.Configuration.UriSection.SchemeSettings%2A?displayProperty=nameWithType>
- <xref:System.GenericUriParserOptions?displayProperty=nameWithType>
- <xref:System.Uri?displayProperty=nameWithType>
- [網路設定結構描述](index.md)
