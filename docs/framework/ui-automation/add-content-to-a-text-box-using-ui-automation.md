---
title: "UI オートメーションを使用した、テキスト ボックスへのコンテンツの追加"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-bcl
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- adding content to text boxes
- text boxes, adding content
- UI Automation, adding content to text boxes
ms.assetid: 8bdd1a73-1ecb-4a05-a891-a7827ebb767f
caps.latest.revision: "13"
author: Xansky
ms.author: mhopkins
manager: markl
ms.openlocfilehash: 0acd6510e6349917b38e33e487123a118c2e653c
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2017
---
# <a name="add-content-to-a-text-box-using-ui-automation"></a>UI オートメーションを使用した、テキスト ボックスへのコンテンツの追加
> [!NOTE]
>  このドキュメントは、[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 名前空間で定義されているマネージ <xref:System.Windows.Automation> クラスを使用する .NET Framework 開発者を対象としています。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]の最新情報については、「 [Windows Automation API: UI Automation (Windows のオートメーション API: UI オートメーション)](http://go.microsoft.com/fwlink/?LinkID=156746)」を参照してください。  
  
 このトピックを使用する方法を示すコード例が含まれています。[!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)]単一行のテキスト ボックスにテキストを挿入します。 複数行およびリッチ テキスト コントロールを別の方法が提供される、[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]は適用されません。 例は、比較のための Win32 メソッドを使用して、同じ結果を達成する方法も示します。  
  
## <a name="example"></a>例  
 ターゲット アプリケーション内のテキスト コントロールのシーケンスで次の例の手順です。 各テキスト コントロールがかどうかをテストする<xref:System.Windows.Automation.ValuePattern>オブジェクトを取得するにを使用して、<xref:System.Windows.Automation.AutomationElement.TryGetCurrentPattern%2A>メソッドです。 場合は、テキスト コントロールはサポート<xref:System.Windows.Automation.ValuePattern>、<xref:System.Windows.Automation.ValuePattern.SetValue%2A>テキスト コントロールにユーザー定義の文字列を挿入するメソッドを使用します。 それ以外の場合、<xref:System.Windows.Forms.SendKeys.SendWait%2A?displayProperty=nameWithType>メソッドを使用します。  
  
 [!code-csharp[InsertText#InsertText](../../../samples/snippets/csharp/VS_Snippets_Wpf/InsertText/CSharp/Window1.xaml.cs#inserttext)]
 [!code-vb[InsertText#InsertText](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/InsertText/VisualBasic/Window1.xaml.vb#inserttext)]  
  
## <a name="see-also"></a>関連項目  
 [TextPattern の挿入テキスト サンプル](http://msdn.microsoft.com/en-us/67353f93-7ee2-42f2-ab76-5c078cf6ca16)
