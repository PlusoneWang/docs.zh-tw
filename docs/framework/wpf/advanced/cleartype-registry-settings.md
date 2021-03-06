---
title: ClearType 登錄設定
ms.date: 03/30/2017
helpviewer_keywords:
- ClearType [WPF], registry settings
- typography [WPF], ClearType registry settings
ms.assetid: 56f314bb-b30b-4f67-8492-8b8a9fa432ae
ms.openlocfilehash: 6143cf835cc44a6c6cc50372b2ac1a4d24d65311
ms.sourcegitcommit: 9a97c76e141333394676bc5d264c6624b6f45bcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2020
ms.locfileid: "75740391"
---
# <a name="cleartype-registry-settings"></a>ClearType 登錄設定
本主題概要說明 WPF 應用程式所使用的 Microsoft ClearType 登錄設定。  

<a name="overview"></a>   
## <a name="technology-overview"></a>技術概觀  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 將文字轉譯為顯示裝置的應用程式，請使用 ClearType 功能來提供增強的閱讀體驗。 ClearType 是由 Microsoft 開發的軟體技術，可改善現有 Lcd （液晶顯示器）的文字可讀性，例如膝上型電腦螢幕、Pocket PC 螢幕和平面監視器。 ClearType 的運作方式是存取 LCD 螢幕每個圖元內的個別垂直色彩 stripe 元素。 如需 ClearType 的詳細資訊，請參閱[Cleartype 總覽](cleartype-overview.md)。  
  
 在各種顯示裝置上觀看時，以 ClearType 轉譯的文字會明顯不同。 例如，少數監視器會以藍色、綠色、紅色順序來執行彩色 stripe 元素，而不是較常見的紅色、綠色、藍色（RGB）順序。  
  
 以 ClearType 轉譯的文字在以色彩敏感度層級不同的個人觀看時，也會明顯不同。 有些人比其他人更能感知色彩的細微差異。  
  
 在上述每一種情況下，都需要修改 ClearType 功能，才能為每個人提供最佳的閱讀體驗。  
  
<a name="registry_settings"></a>   
## <a name="registry-settings"></a>登錄設定  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 指定用來控制 ClearType 功能的四個登錄設定：  
  
|設定|描述|  
|-------------|-----------------|  
|ClearType 層級|描述 ClearType 色彩清晰度的層級。|  
|色差補正層級|說明顯示裝置的像素色彩元件層級。|  
|像素結構|說明顯示裝置的像素排列。|  
|文字對比層級|說明顯示文字的對比層級。|  
  
 這些設定可由外部設定公用程式存取，知道如何參考已識別的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]ClearType 登錄設定。 您也可以使用 Windows 登錄編輯程式直接存取這些值來建立或修改這些設定。  
  
 如果未設定 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]ClearType 登錄設定（這是預設狀態），則 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 應用程式會查詢 Windows 系統參數資訊中的字型平滑設定。  
  
> [!NOTE]
> 如需列舉顯示裝置名稱的詳細資訊，請參閱 `SystemParametersInfo`Win32 函數。  
  
<a name="ClearType_level"></a>   
## <a name="cleartype-level"></a>ClearType 層級  
 ClearType 層級可讓您根據個人的色彩敏感度和認知，調整文字的呈現。 對於某些人來說，在其最高層級使用 ClearType 的文字轉譯，並不會產生最佳的閱讀體驗。  
  
 ClearType 層級是一個整數值，範圍介於0到100之間。 預設層級為100，表示 ClearType 會使用顯示裝置的色彩 stripe 元素的最大功能。 不過，ClearType 層級0會將文字呈現為灰色尺規。 藉由將 ClearType 層級設定為0到100之間的某個位置，您可以建立適合個人色彩敏感度的中繼層級。  
  
### <a name="registry-setting"></a>登錄設定  
 ClearType 層級的登錄設定位置是對應到特定顯示裝置名稱的個別使用者設定：  
  
 `HKEY_CURRENT_USER\SOFTWARE\Microsoft\Avalon.Graphics\<displayName>`  
  
 針對使用者的每個顯示裝置名稱，會定義一個 `ClearTypeLevel` 的 DWORD 值。 下列螢幕擷取畫面顯示 ClearType 層級的登錄編輯程式設定。  
  
 ![登錄編輯程式中的 ClearType 設定。](./media/cleartype-registry-settings/cleartype-settings-registry-editor.png)  
  
> [!NOTE]
> [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 應用程式會以兩種模式的其中一種來轉譯文字，而不論是否使用 ClearType。 轉譯不含 ClearType 的文字時，就稱為「灰階呈現」。  
  
<a name="gamma_level"></a>   
## <a name="gamma-level"></a>Gamma 層級  
 Gamma 層級是指像素值和明亮度之間的非線性關聯性。 Gamma 層級設定應該對應至顯示裝置的實體特性，否則轉譯的輸出可能會失真。 例如，文字可能會顯示太寬或太窄，或色彩 fringes 可能會出現在圖像的垂直詞幹邊緣。  
  
 Gamma 層級是範圍從 1000 到 2200 的整數值。 預設層級為 1900。  
  
### <a name="registry-setting"></a>登錄設定  
 Gamma 層級的登錄設定位置是對應到特定顯示裝置名稱的本機電腦設定：  
  
 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Avalon.Graphics\<displayName>`  
  
 針對使用者的每個顯示裝置名稱，會定義一個 `GammaLevel` 的 DWORD 值。 以下的螢幕擷取畫面顯示 Gamma 層級的登錄編輯程式設定。  
  
 ![登錄編輯程式中的 ClearType gamma 層級設定](./media/cleartype-registry-settings/cleartype-gamma-level-settings-registry-editor.png)  
  
<a name="pixel_structure"></a>   
## <a name="pixel-structure"></a>像素結構  
 像素結構說明構成顯示裝置的像素類型。 像素結構定義有三種類型︰  
  
|類型|{2&gt;值&lt;2}|描述|  
|----------|-----------|-----------------|  
|一般|0|顯示裝置沒有像素結構。 這表示每種色彩光源都平均分布在像素區域，此即為灰階轉譯。 這是標準顯示裝置運作的方式。 ClearType 永遠不會套用至呈現的文字。|  
|RGB|1|顯示裝置的像素色帶組成順序如下︰紅色、綠色和藍色。 ClearType 會套用至呈現的文字。|  
|BGR|2|顯示裝置的像素色帶組成順序如下︰藍色、綠色和紅色。 ClearType 會套用至呈現的文字。 請注意順序由 RGB 類型反轉的方式。|  
  
 像素結構對應至範圍從 0 到 2 的整數值。 預設層級為 0 表示一般的像素結構。  
  
> [!NOTE]
> 如需列舉顯示裝置名稱的詳細資訊，請參閱 `EnumDisplayDevices`Win32 函數。  
  
### <a name="registry-setting"></a>登錄設定  
 像素結構的登錄設定位置是對應到特定顯示裝置名稱的本機電腦設定：  
  
 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Avalon.Graphics\<displayName>`  
  
 針對使用者的每個顯示裝置名稱，會定義一個 `PixelStructure` 的 DWORD 值。 以下的螢幕擷取畫面顯示像素結構的登錄編輯程式設定。  
  
 ![登錄編輯程式中的 ClearType gamma 層級設定](./media/cleartype-registry-settings/cleartype-gamma-level-settings-registry-editor.png)  
  
<a name="text_contrast_level"></a>   
## <a name="text-contrast-level"></a>文字對比層級  
 文字對比層級可讓您根據字符的主體寬度調整文字的轉譯。 文字對比層級是一個範圍從 0 到 6 的整數值，整數值愈大，主體愈寬。 預設層級為 1。  
  
### <a name="registry-setting"></a>登錄設定  
 文字對比層級的登錄設定位置是對應到特定顯示裝置名稱的個別使用者設定：  
  
 `HKEY_CURRENT_USER\Software\Microsoft\Avalon.Graphics\<displayName>`  
  
 針對使用者的每個顯示裝置名稱，會定義一個 `TextContrastLevel` 的 DWORD 值。 下列螢幕擷取畫面顯示文字對比層級的登錄編輯程式設定。  
  
 ![登錄編輯程式中的 ClearType 設定。](./media/cleartype-registry-settings/cleartype-settings-registry-editor.png)  
  
## <a name="see-also"></a>請參閱

- [ClearType 概觀](cleartype-overview.md)
- [ClearType 消除鋸齒功能](/windows/desktop/gdi/cleartype-antialiasing)
