---
title: "方法 : 結合したジオメトリを作成する"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- combining geometries [WPF]
- graphics [WPF], combining geometries
- geometries [WPF], combining
ms.assetid: 54c3277c-6b6e-4b25-91be-fda0bbc706b4
caps.latest.revision: "8"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: 2be0471f27d26b145cc29847a08bf3bc3b1d51ff
ms.sourcegitcommit: c2e216692ef7576a213ae16af2377cd98d1a67fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2017
---
# <a name="how-to-create-a-combined-geometry"></a>方法 : 結合したジオメトリを作成する
この例では、ジオメトリを結合する方法を示します。 2 つのジオメトリを組み合わせるを使用して、<xref:System.Windows.Media.CombinedGeometry>オブジェクト。 設定の<xref:System.Windows.Media.CombinedGeometry.Geometry1%2A>と<xref:System.Windows.Media.CombinedGeometry.Geometry2%2A>結合、および設定を 2 つのジオメトリを持つプロパティ、<xref:System.Windows.Media.CombinedGeometry.GeometryCombineMode%2A>ジオメトリを一緒に結合される方法を決定するプロパティを`Union`、 `Intersect`、 `Exclude`、または`Xor`.  
  
 2 つ以上のジオメトリから複合ジオメトリを作成するには、使用、<xref:System.Windows.Media.GeometryGroup>です。  
  
## <a name="example"></a>例  
 次の例で、<xref:System.Windows.Media.CombinedGeometry>の geometry 組み合わせモードで定義された`Exclude`です。  両方<xref:System.Windows.Media.CombinedGeometry.Geometry1%2A>と<xref:System.Windows.Media.CombinedGeometry.Geometry2%2A>50 センター オフセットを含むが、同じの半径の円として定義されます。  
  
 [!code-xaml[GeometrySample#21](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/combininggeometriesexample.xaml#21)]  
  
 ![組み合わせモードの結果、除外の](../../../../docs/framework/wpf/graphics-multimedia/media/mil-task-combined-geometry-exclude.PNG "mil_task_combined_geometry_exclude")  
結合したジオメトリの除外  
  
 次のマークアップで、<xref:System.Windows.Media.CombinedGeometry>の組み合わせモードで定義された`Intersect`です。  両方<xref:System.Windows.Media.CombinedGeometry.Geometry1%2A>と<xref:System.Windows.Media.CombinedGeometry.Geometry2%2A>50 センター オフセットを含むが、同じの半径の円として定義されます。  
  
 [!code-xaml[GeometrySample#22](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/combininggeometriesexample.xaml#22)]  
  
 ![組み合わせモードの交差部分の結果](../../../../docs/framework/wpf/graphics-multimedia/media/mil-task-combined-geometry-intersect.PNG "mil_task_combined_geometry_intersect")  
結合された Geometry を交差します。  
  
 次のマークアップで、<xref:System.Windows.Media.CombinedGeometry>の組み合わせモードで定義された`Union`です。  両方<xref:System.Windows.Media.CombinedGeometry.Geometry1%2A>と<xref:System.Windows.Media.CombinedGeometry.Geometry2%2A>50 センター オフセットを含むが、同じの半径の円として定義されます。  
  
 [!code-xaml[GeometrySample#23](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/combininggeometriesexample.xaml#23)]  
  
 ![和集合結合モードの結果](../../../../docs/framework/wpf/graphics-multimedia/media/mil-task-combined-geometry-union.PNG "mil_task_combined_geometry_union")  
結合された Geometry の和集合  
  
 次のマークアップで、<xref:System.Windows.Media.CombinedGeometry>の組み合わせモードで定義された`Xor`です。  両方<xref:System.Windows.Media.CombinedGeometry.Geometry1%2A>と<xref:System.Windows.Media.CombinedGeometry.Geometry2%2A>50 センター オフセットを含むが、同じの半径の円として定義されます。  
  
 [!code-xaml[GeometrySample#24](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/combininggeometriesexample.xaml#24)]  
  
 ![Xor 結合モードの結果](../../../../docs/framework/wpf/graphics-multimedia/media/mil-task-combined-geometry-xor.PNG "mil_task_combined_geometry_xor")  
結合したジオメトリ Xor
