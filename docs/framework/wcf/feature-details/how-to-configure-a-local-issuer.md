---
title: HOW TO：設定本機簽發者
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF, federation
- federation
ms.assetid: 15263371-514e-4ea6-90fb-14b4939154cd
ms.openlocfilehash: 0028a0522447588ee0fb183b5b2f93d334a7b2b2
ms.sourcegitcommit: a97ecb94437362b21fffc5eb3c38b6c0b4368999
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/13/2019
ms.locfileid: "68972074"
---
# <a name="how-to-configure-a-local-issuer"></a>作法：設定本機簽發者

本主題會說明如何將用戶端設定成使用已發行權杖的本機簽發者。

通常，當用戶端與聯合服務進行通訊時，服務都會指定特定安全性權杖服務的位址，該服務預期會發出用戶端要用來向聯合服務驗證自己的權杖。 在某些情況下, 可能會將用戶端設定為使用*本機簽發者*。

Windows Communication Foundation (WCF) 的聯合繫結的簽發者位址的情況下使用本機簽發者 `http://schemas.microsoft.com/2005/12/ServiceModel/Addressing/Anonymous` 或`null`。 在這種情況下，您必須設定包含本機簽發者位址的 <xref:System.ServiceModel.Description.ClientCredentials>，以及用來與該簽發者進行通訊的繫結。

> [!NOTE]
> 如果`ClientCredentials`類別<xref:System.ServiceModel.Description.ClientCredentials.SupportInteractive%2A>的屬性設定為`true`, 則未指定本機簽發者位址[ \<, 而且 wsFederationHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/wsfederationhttpbinding.md)或其他同盟系結所指定的簽發者位址為`http://schemas.xmlsoap.org/ws/2005/05/identity/issuer/self` 、`http://schemas.microsoft.com/2005/12/ServiceModel/Addressing/Anonymous`或為`null`, 則會使用 Windows CardSpace 簽發者。

## <a name="to-configure-the-local-issuer-in-code"></a>透過程式碼來設定本機簽發者

1. 建立型別為 <xref:System.ServiceModel.Security.IssuedTokenClientCredential> 的變數

2. 將此變數設為從 <xref:System.ServiceModel.Description.ClientCredentials.IssuedToken%2A> 類別的 `ClientCredentials` 屬性傳回的執行個體 (Instance)。 該執行個體會由用戶端 (繼承自 <xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A>) 的 <xref:System.ServiceModel.ClientBase%601> 屬性，或是 <xref:System.ServiceModel.ChannelFactory.Credentials%2A> 的 <xref:System.ServiceModel.ChannelFactory> 屬性傳回：

     [!code-csharp[c_CreateSTS#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#9)]
     [!code-vb[c_CreateSTS#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#9)]

3. 將 <xref:System.ServiceModel.Security.IssuedTokenClientCredential.LocalIssuerAddress%2A> 屬性設定為 <xref:System.ServiceModel.EndpointAddress> 的新執行個體，其本機簽發者位址會當做建構函式 (Constructor) 的引數。

     [!code-csharp[c_CreateSTS#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#10)]
     [!code-vb[c_CreateSTS#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#10)]

     或者，建立新的 <xref:System.Uri> 執行個體做為該建構函式的引數。

     [!code-csharp[c_CreateSTS#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#11)]
     [!code-vb[c_CreateSTS#11](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#11)]

     參數是實例的<xref:System.ServiceModel.Channels.AddressHeader>陣列, 如下所示。 `addressHeaders`

     [!code-csharp[c_CreateSTS#12](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#12)]
     [!code-vb[c_CreateSTS#12](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#12)]

4. 使用<xref:System.ServiceModel.Security.IssuedTokenClientCredential.LocalIssuerBinding%2A>屬性來設定本機簽發者的系結。

     [!code-csharp[c_CreateSTS#13](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#13)]
     [!code-vb[c_CreateSTS#13](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#13)]

5. 選擇性。 將本機簽發者的已設定端點行為新增到 <xref:System.ServiceModel.Security.IssuedTokenClientCredential.LocalIssuerChannelBehaviors%2A> 屬性所傳回的集合，即可新增該行為。

     [!code-csharp[c_CreateSTS#14](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#14)]
     [!code-vb[c_CreateSTS#14](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#14)]

## <a name="to-configure-the-local-issuer-in-configuration"></a>透過組態來設定本機簽發者

1. 建立 localIssuer > 元素做為[ \<issuedToken >](../../../../docs/framework/configure-apps/file-schema/wcf/issuedtoken.md)元素的子系, 本身就是端點行為中[ \<clientCredentials >](../../../../docs/framework/configure-apps/file-schema/wcf/clientcredentials.md)專案的子系。 [ \< ](../../../../docs/framework/configure-apps/file-schema/wcf/localissuer.md)

2. 將 `address` 屬性設定為將接受權杖要求之本機簽發者的位址。

3. 將 `binding` 和 `bindingConfiguration` 屬性設定為會參考當與本機簽發者端點進行通訊時所使用之適當繫結的值。

4. 選擇性。 `localIssuer` [將identity>專案設定為<>元素的子系,並指定本機簽發者\<](../../../../docs/framework/configure-apps/file-schema/wcf/identity.md)的身分識別資訊。

5. 選擇性。 `localIssuer` [將標頭>專案設定為<>元素的子系,並指定必要的其他標頭,以便正確地\<](../../../../docs/framework/configure-apps/file-schema/wcf/headers.md)處理本機簽發者。

## <a name="net-framework-security"></a>.NET Framework 安全性

請注意，如果已指定特定繫結的簽發者位址和繫結，這時使用該繫結的端點就不會使用該本機簽發者。 預期一定要使用該本機簽發者的用戶端應該要確定自己沒有使用這類繫結，否則它們就會修改繫結，進而使得簽發者位址成為 `null`。

## <a name="see-also"></a>另請參閱

- [如何：在同盟服務上設定認證](../../../../docs/framework/wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md)
- [如何：建立同盟用戶端](../../../../docs/framework/wcf/feature-details/how-to-create-a-federated-client.md)
- [如何：建立 WSFederationHttpBinding](../../../../docs/framework/wcf/feature-details/how-to-create-a-wsfederationhttpbinding.md)
