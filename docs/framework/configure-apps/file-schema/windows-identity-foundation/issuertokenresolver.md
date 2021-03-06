---
title: <issuerTokenResolver>
ms.date: 03/30/2017
ms.assetid: f74392f6-3f5b-4880-bd8a-3a9130d31e65
author: BrucePerlerMS
ms.openlocfilehash: 451750a1facd9a886b53427a8d54580d1a939fa5
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/12/2019
ms.locfileid: "73968515"
---
# <a name="issuertokenresolver"></a>\<issuerTokenResolver >
註冊權杖處理常式集合中處理常式所使用的簽發者 token 解析程式。 簽發者權杖解析程式是用來解析傳入權杖和訊息上的簽署權杖。  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<microsoft.identitymodel >** ](system-identitymodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<identityConfiguration >** ](identityconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<securityTokenHandlers >** ](securitytokenhandlers.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<securityTokenHandlerConfiguration >** ](securitytokenhandlerconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<issuerTokenResolver >**  
  
## <a name="syntax"></a>語法  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <securityTokenHandlerConfiguration>  
        <issuerTokenResolver type=xs:string>  
        </issuerTokenResolver>  
      </securityTokenHandlerConfiguration>  
    </securityTokenHandlers>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  
 下列各節描述屬性、子項目和父項目。  
  
### <a name="attributes"></a>屬性  
  
|屬性|描述|  
|---------------|-----------------|  
|型別|指定簽發者 token 解析程式的類型。 必須是 <xref:System.IdentityModel.Tokens.IssuerTokenResolver> 類別，或是衍生自 <xref:System.IdentityModel.Tokens.IssuerTokenResolver> 類別的類型。 必要項。|  
  
### <a name="child-elements"></a>子項目  
 None  
  
### <a name="parent-elements"></a>父項目  
  
|項目|描述|  
|-------------|-----------------|  
|[\<securityTokenHandlerConfiguration >](securitytokenhandlerconfiguration.md)|提供安全性權杖處理常式集合的設定。|  
  
## <a name="remarks"></a>備註  
 簽發者權杖解析程式是用來解析傳入權杖和訊息上的簽署權杖。 它是用來抓取用於檢查簽章的密碼編譯內容。 您必須指定 `type` 屬性。 指定的型別可以是 <xref:System.IdentityModel.Tokens.IssuerTokenResolver> 或衍生自 <xref:System.IdentityModel.Tokens.IssuerTokenResolver> 類別的自訂型別。  
  
 某些權杖處理常式可讓您在設定中指定簽發者權杖解析程式設定。 個別權杖處理常式上的設定會覆寫安全性權杖處理常式集合上指定的設定。  
  
> [!NOTE]
> 將 `<issuerTokenResolver>` 專案指定為[\<identityConfiguration >](identityconfiguration.md)元素的子項目已被取代，但仍支援回溯相容性。 `<securityTokenHandlerConfiguration>` 專案上的設定會覆寫 `<identityConfiguration>` 元素上的值。  
  
## <a name="example"></a>範例  
 下列 XML 顯示的簽發者 token 解析程式的設定是以衍生自 <xref:System.IdentityModel.Tokens.IssuerTokenResolver>的自訂類別為基礎。 權杖解析程式會維護一組物件-金鑰組的字典，這些是從為類別定義的自訂設定元素（`<AddAudienceKeyPair>`）初始化的。 類別會覆寫 <xref:System.IdentityModel.Selectors.SecurityTokenResolver.LoadCustomConfiguration%2A> 方法來處理這個元素。 此覆寫如下列範例所示：不過，為了簡潔起見，不會顯示其所呼叫的方法。 如需完整範例，請參閱 `CustomToken` 範例。  
  
```xml  
<issuerTokenResolver type="SimpleWebToken.CustomIssuerTokenResolver, SimpleWebToken">  
  <AddAudienceKeyPair  symmetricKey="wAVkldQiFypTQ+kdNdGWCYCHRcee8XmXxOvgmak8vSY=" audience="http://localhost:19851/" />  
</issuerTokenResolver>  
```  
  
## <a name="example"></a>範例
  
```csharp
public override void LoadCustomConfiguration(System.Xml.XmlNodeList nodelist)  
{  
    foreach (XmlNode node in nodelist)  
    {  
        XmlDictionaryReader rdr = XmlDictionaryReader.CreateDictionaryReader(new XmlTextReader(new StringReader(node.OuterXml)));  
        rdr.MoveToContent();  
  
        string symmetricKey = rdr.GetAttribute("symmetricKey");  
        string audience = rdr.GetAttribute("audience");  
  
        this.AddAudienceKeyPair(audience, symmetricKey);  
    }  
}  
``` 
  
## <a name="see-also"></a>請參閱

- <xref:System.IdentityModel.Tokens.IssuerTokenResolver>
