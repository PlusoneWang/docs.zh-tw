---
title: HOW TO：轉換立體模型的比例
ms.date: 03/30/2017
helpviewer_keywords:
- scaling [WPF], 3-D objects
- 3-D objects [WPF], scaling
ms.assetid: f3fdfe33-f7dc-44b0-84a5-e43b89947f35
ms.openlocfilehash: 6d668de08201d819ce9f8752bedf6c388a6bc718
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "61769326"
---
# <a name="how-to-transform-the-scale-of-a-3-d-model"></a>HOW TO：轉換立體模型的比例
此範例示範如何調整 3d 物件。 若要調整的 3d 物件，使用<xref:System.Windows.Media.Media3D.ScaleTransform3D>。 <xref:System.Windows.Media.Media3D.ScaleTransform3D.ScaleX%2A>， <xref:System.Windows.Media.Media3D.ScaleTransform3D.ScaleY%2A>，和<xref:System.Windows.Media.Media3D.ScaleTransform3D.ScaleZ%2A>所指定的因數調整元素的屬性。 比方說，<xref:System.Windows.Media.Media3D.ScaleTransform3D.ScaleX%2A>的 1.5 倍的值會自動縮放其原始寬度的 150%的物件。 A<xref:System.Windows.Media.Media3D.ScaleTransform3D.ScaleY%2A>值為 0.5 百分之 50 壓縮物件的高度。 下列程式碼示範使用<xref:System.Windows.Media.Media3D.ScaleTransform3D>轉換為<xref:System.Windows.Media.Media3D.GeometryModel3D>。  
  
 [!code-xaml[3DGallery_snip#ScaleTransform3DExampleInline1](~/samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_snip/CS/ScaleTransform3DExample.xaml#scaletransform3dexampleinline1)]  
  
## <a name="example"></a>範例  
 下列程式碼顯示整個範例。  
  
 [!code-xaml[3DGallery_snip#ScaleTransform3DExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_snip/CS/ScaleTransform3DExample.xaml#scaletransform3dexamplewholepage)]  
  
## <a name="see-also"></a>另請參閱

- [建立立體轉譯動畫](how-to-animate-3-d-translations.md)
- [建立立體場景](how-to-create-a-3-d-scene.md)
- [立體圖形概觀](3-d-graphics-overview.md)
