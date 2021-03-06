---
title: 作法：旋轉、反射和傾斜影像
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- images [Windows Forms], reflecting
- images [Windows Forms], rotating
- images [Windows Forms], skewing
ms.assetid: a3bf97eb-63ed-425a-ba07-dcc65efb567c
ms.openlocfilehash: 80ac92d545d9be7a4a611038eaaadbbdbe2e8ecf
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/14/2019
ms.locfileid: "65590334"
---
# <a name="how-to-rotate-reflect-and-skew-images"></a>作法：旋轉、反射和傾斜影像
您可以旋轉、 反射和傾斜影像藉由指定之左上角、 右上方和左下角邊角原始映像的目的點。 這三個目的點決定仿射轉換，原始的矩形映像會對應至平行四邊形。  
  
## <a name="example"></a>範例  
 例如，假設原始的映像會在左上角的矩形 （0，0），在右上角 （100，0），並在左下角 （0，50）。 現在假設您將這些對應三個點至目的地點，如下所示。  
  
|原始的點|目的地點|  
|--------------------|-----------------------|  
|左上角 （0，0）|(200, 20)|  
|右上方 （100，0）|(110, 100)|  
|左下角 （0，50）|(250, 30)|  
  
 下圖顯示原始的映像和對應的平行四邊形的映像。 原始的映像具有已扭曲、 反映、 旋轉和轉譯。 原始的映像的上邊緣的 x 軸會對應到執行的那一行 （200，20） 和 （110，100）。 原始的映像的左邊緣沿著 y 軸會對應到執行的那一行 （200，20） 和 250 (30）。  
  
 ![原始的映像和映像對應的平行四邊形。](./media/how-to-rotate-reflect-and-skew-images/reflected-skewed-rotated-illustration.gif)  
  
 下圖顯示類似的轉換套用至相片的映像：  
  
 ![就和對應的平行四邊形的圖片的圖片。](./media/how-to-rotate-reflect-and-skew-images/reflected-skewed-rotated-photo.png)  
  
 下圖顯示類似的轉換套用至中繼檔：  
  
 ![說明圖形和文字，以及對應之平行四邊形。](./media/how-to-rotate-reflect-and-skew-images/reflected-skewed-rotated-metafile.png)  
  
 下列範例會產生的第一個圖例中顯示的映像。  
  
 [!code-csharp[System.Drawing.WorkingWithImages#61](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/CS/Class1.cs#61)]
 [!code-vb[System.Drawing.WorkingWithImages#61](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/VB/Class1.vb#61)]  
  
## <a name="compiling-the-code"></a>編譯程式碼  
 上述範例中專為搭配 Windows Form 使用，而且需要<xref:System.Windows.Forms.PaintEventArgs> `e`，這是參數的<xref:System.Windows.Forms.Control.Paint>事件處理常式。 請務必取代`Stripes.bmp`適用於您的系統映像的路徑。  
  
## <a name="see-also"></a>另請參閱

- [使用影像、點陣圖、圖示和中繼檔](working-with-images-bitmaps-icons-and-metafiles.md)
