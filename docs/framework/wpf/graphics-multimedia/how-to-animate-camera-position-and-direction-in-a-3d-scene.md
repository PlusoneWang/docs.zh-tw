---
title: HOW TO：在立體場景中建立鏡頭位置和方向的動畫
ms.date: 03/30/2017
helpviewer_keywords:
- animation [WPF], camera position in 3-D scenes
- camera direction [WPF], animating in 3-D scenes
- 3-D scenes [WPF], animating camera position
- 3-D scenes [WPF], animating camera direction
- camera position [WPF], animating in 3-D scenes
- animation [WPF], camera direction in 3-D scenes
ms.assetid: 480224b7-a5e5-4165-ba7f-ef760ddff94a
ms.openlocfilehash: b64263a495ffe845a76317aad8f5b4a14e11b31e
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "61651372"
---
# <a name="how-to-animate-camera-position-and-direction-in-a-3d-scene"></a>HOW TO：在立體場景中建立鏡頭位置和方向的動畫
下列範例示範如何以動畫顯示觀景窗的位置，並以動畫顯示其為 3D 場景中所指的方向。 這是藉由使用<xref:System.Windows.Media.Animation.Point3DAnimation>並<xref:System.Windows.Media.Animation.Vector3DAnimation>來以動畫顯示<xref:System.Windows.Media.Media3D.ProjectionCamera.Position%2A>並<xref:System.Windows.Media.Media3D.ProjectionCamera.LookDirection%2A>屬性，分別是<xref:System.Windows.Media.Media3D.PerspectiveCamera>。 若要變更旁觀者的檢視，以回應事件場景的您可以使用這類動畫。  
  
## <a name="example"></a>範例  
 [!code-xaml[Animation3DGallery_snip#PointVector3DAnimationExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/PointVector3DAnimationExample.xaml#pointvector3danimationexamplewholepage)]  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Windows.Media.Animation.Vector3DAnimation>
- <xref:System.Windows.Media.Animation.Point3DAnimation>
- [使用主要畫面格建立鏡頭位置和方向的動畫](how-to-animate-camera-position-and-direction-using-key-frames.md)
- [立體圖形概觀](3-d-graphics-overview.md)
