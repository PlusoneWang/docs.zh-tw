---
title: HOW TO：使用主要畫面格建立布林值的動畫
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Booleans [WPF], animating with key frames
- animation [WPF], Booleans with key frames
- key frames [WPF], animating Booleans with
ms.assetid: 4b0fac96-6231-4fcf-9775-4dd673ddc785
ms.openlocfilehash: 59a72916721cccbe66f704253f148828fa8cd418
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62020201"
---
# <a name="how-to-animate-a-boolean-by-using-key-frames"></a>HOW TO：使用主要畫面格建立布林值的動畫
此範例示範如何建立動畫的布林屬性值<xref:System.Windows.Controls.Button>使用主要畫面格的控制項。  
  
## <a name="example"></a>範例  
 下列範例會使用<xref:System.Windows.Media.Animation.BooleanAnimationUsingKeyFrames>類別以動畫顯示<xref:System.Windows.UIElement.IsEnabled%2A>屬性<xref:System.Windows.Controls.Button>控制項。 在此範例中的所有主要畫面格使用的執行個體<xref:System.Windows.Media.Animation.DiscreteBooleanKeyFrame>類別。 特定主要畫面格喜歡<xref:System.Windows.Media.Animation.DiscreteBooleanKeyFrame>建立突然跳躍點之間的值，也就是為動畫的移動不穩定。  
  
 [!code-csharp[keyframes_snip#BooleanAnimationUsingKeyFramesWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_snip/CSharp/BooleanAnimationUsingKeyFramesExample.cs#booleananimationusingkeyframeswholepage)]
 [!code-vb[keyframes_snip#BooleanAnimationUsingKeyFramesWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/keyframes_snip/visualbasic/booleananimationusingkeyframesexample.vb#booleananimationusingkeyframeswholepage)]
 [!code-xaml[keyframes_snip#BooleanAnimationUsingKeyFramesWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/BooleanAnimationUsingKeyFramesExample.xaml#booleananimationusingkeyframeswholepage)]  
  
 如需完整的範例，請參閱[主要畫面格動畫範例](https://go.microsoft.com/fwlink/?LinkID=160012)。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Windows.Media.Animation.BooleanAnimationUsingKeyFrames>
- <xref:System.Windows.UIElement.IsEnabled%2A>
- <xref:System.Windows.Controls.Button>
- [主要畫面格動畫概觀](key-frame-animations-overview.md)
- [主要畫面格操作說明主題](key-frame-animation-how-to-topics.md)
