---
title: "基本フォームの外観を変更した場合の影響"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-winforms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- parent forms [Windows Forms]
- inherited forms [Windows Forms], modifications to base form
- Windows Forms, base form appearance
- base forms
- inheritance [Windows Forms], forms
ms.assetid: 1c3f2b29-a05c-4c6f-aa1a-4e66b94f343a
caps.latest.revision: "9"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: c1e0eb19946ef2231b5a58df4b8d0b2e40e8e99f
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="effects-of-modifying-a-base-form39s-appearance"></a>基本フォームの外観を変更した場合の影響
アプリケーションの開発中に、同じプロジェクト (または他のプロジェクト) 内の他のフォームの継承元となる、基本フォームの外観の変更が必要になることがよくあります。  
  
 デザイン時にプロパティの設定の変更やコントロールの追加または削除によって基本フォームの外観を変更した場合、基本フォームを含むプロジェクトをビルドしたときに、継承されたフォームに変更が反映されます。 基本フォームの変更を保存するだけでは、変更は反映されません。 プロジェクトをビルドするには、**[ビルド]** メニューの **[ビルド]** を選択します。  
  
> [!NOTE]
>  実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「[Visual Studio での開発設定のカスタマイズ](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。  
  
 実行時に基本フォームに変更を加えても、既にインスタンス化されている継承されたフォームには反映されません。  
  
## <a name="see-also"></a>関連項目  
 [base](~/docs/csharp/language-reference/keywords/base.md)  
 [方法: Windows フォームを継承する](../../../../docs/framework/winforms/advanced/how-to-inherit-windows-forms.md)  
 [Windows フォームのビジュアルの継承](../../../../docs/framework/winforms/advanced/windows-forms-visual-inheritance.md)
