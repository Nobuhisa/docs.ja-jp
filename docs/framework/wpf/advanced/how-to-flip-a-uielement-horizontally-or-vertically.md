---
title: "方法 : UIElement を左右または上下に反転させる"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- flipping UIElements [WPF]
- UIElements [WPF], flipping
ms.assetid: 02c6730f-65c0-40d5-a553-4cb663721882
caps.latest.revision: "4"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: 84d1360246141cfa565d669fff108e3e4db3ce33
ms.sourcegitcommit: c2e216692ef7576a213ae16af2377cd98d1a67fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2017
---
# <a name="how-to-flip-a-uielement-horizontally-or-vertically"></a>方法 : UIElement を左右または上下に反転させる
この例を使用する方法を示しています、<xref:System.Windows.Media.ScaleTransform>反転するのには、<xref:System.Windows.UIElement>水平方向または垂直方向にします。 この例では、<xref:System.Windows.Controls.Button>コントロール (の型<xref:System.Windows.UIElement>) を適用して反転、<xref:System.Windows.Media.ScaleTransform>にその<xref:System.Windows.UIElement.RenderTransform%2A>プロパティです。  
  
## <a name="example"></a>例  
 次の図は、反転するボタンを示しています。  
  
 ![変換のないボタン](../../../../docs/framework/wpf/advanced/media/graphicsmm-buttonflipbeforeflip.gif "graphicsmm_buttonflipbeforeflip")  
反転する ui 要素  
  
 ボタンを作成するコードを次に示します。  
  
 [!code-xaml[Transforms_snip#GraphicsMMButtonWithoutFlip](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/FlipExample.xaml#graphicsmmbuttonwithoutflip)]  
  
## <a name="example"></a>例  
 ボタンを水平方向に反転 を作成、<xref:System.Windows.Media.ScaleTransform>設定とその<xref:System.Windows.Media.ScaleTransform.ScaleX%2A>プロパティを-1 にします。 適用、 <xref:System.Windows.Media.ScaleTransform>  ボタンの<xref:System.Windows.UIElement.RenderTransform%2A>プロパティです。  
  
 [!code-xaml[Transforms_snip#GraphicsMMFlipButtonExample1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/FlipExample.xaml#graphicsmmflipbuttonexample1)]  
  
 ![周りで水平方向に反転されるボタン &#40;0, 0&#41;] (../../../../docs/framework/wpf/advanced/media/graphicsmm-buttonfliphorizontalflip-displaced.gif "graphicsmm_buttonfliphorizontalflip_displaced")  
ScaleTransform を適用した後、ボタン  
  
## <a name="example"></a>例  
 前の図からわかるように、ボタンは反転したもに移動されました。 ボタンは、左上隅から反転したためです。 適用する場所で、ボタンを反転するのには、<xref:System.Windows.Media.ScaleTransform>できません、上隅にある、中央にします。 適用する簡単な方法、<xref:System.Windows.Media.ScaleTransform>ボタン センターでボタンの設定には<xref:System.Windows.UIElement.RenderTransformOrigin%2A>プロパティを 0.5 0.5 です。  
  
 [!code-xaml[Transforms_snip#GraphicsMMFlipButtonExample2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/FlipExample.xaml#graphicsmmflipbuttonexample2)]  
  
 ![中心の周り水平方向に反転されるボタン](../../../../docs/framework/wpf/advanced/media/graphicsmm-buttonfliphorizontalflip-inplace.gif "graphicsmm_buttonfliphorizontalflip_inplace")  
0.5 の RenderTransformOrigin ボタン 0.5  
  
## <a name="example"></a>例  
 ボタンを垂直方向に反転するには設定、<xref:System.Windows.Media.ScaleTransform>オブジェクトの<xref:System.Windows.Media.ScaleTransform.ScaleY%2A>プロパティの代わりにその<xref:System.Windows.Media.ScaleTransform.ScaleX%2A>プロパティです。  
  
 [!code-xaml[Transforms_snip#GraphicsMMVerticalFlipButtonExample2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/FlipExample.xaml#graphicsmmverticalflipbuttonexample2)]  
  
 ![中心の周り垂直方向に反転されるボタン](../../../../docs/framework/wpf/advanced/media/graphicsmm-buttonflipverticalflip-inplace.gif "graphicsmm_buttonflipverticalflip_inplace")  
垂直方向に反転されたボタン  
  
## <a name="see-also"></a>関連項目  
 [変換の概要](../../../../docs/framework/wpf/graphics-multimedia/transforms-overview.md)
