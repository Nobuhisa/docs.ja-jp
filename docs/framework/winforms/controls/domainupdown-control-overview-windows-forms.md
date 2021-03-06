---
title: "DomainUpDown コントロールの概要 (Windows フォーム)"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-winforms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: DomainUpDown
helpviewer_keywords:
- spin button control [Windows Forms], about spin button
- DomainUpDown control [Windows Forms], about DomainUpDown control
ms.assetid: 3f40f9c1-20ad-4331-b9b5-b0127eb36eb3
caps.latest.revision: "11"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: a0692677b8ef596bb31b1869480603573a9ec98d
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="domainupdown-control-overview-windows-forms"></a>DomainUpDown コントロールの概要 (Windows フォーム)
Windows フォーム<xref:System.Windows.Forms.DomainUpDown>コントロールは基本的にテキスト ボックスの組み合わせや組の一覧を上または下に移動するためのボタンです。 コントロールは、表示し、選択肢の一覧から、テキスト文字列を設定します。 上下一覧内を移動するボタンをクリックして、上下の矢印キーを押すことによって、または、リスト内の項目に一致する文字列を入力して、ユーザーは、文字列を選択できます。 このコントロールの用途の 1 つでは、名前のアルファベット順に並べ替えられたリストから項目を選択するためです。  
  
> [!NOTE]
>  一覧を並べ替えるには設定、<xref:System.Windows.Forms.DomainUpDown.Sorted%2A>プロパティを`true`です。  
  
 このコントロールの機能は、リスト ボックスまたはコンボ ボックスによく似ていますが、非常に小さい領域を占有します。  
  
## <a name="key-properties"></a>主要プロパティ  
 コントロールのプロパティは<xref:System.Windows.Forms.DomainUpDown.Items%2A>、 <xref:System.Windows.Forms.UpDownBase.ReadOnly%2A>、および<xref:System.Windows.Forms.DomainUpDown.Wrap%2A>です。 <xref:System.Windows.Forms.DomainUpDown.Items%2A>プロパティには、文字列値を持つが、コントロールに表示されるオブジェクトの一覧が含まれています。 場合<xref:System.Windows.Forms.UpDownBase.ReadOnly%2A>に設定されている`false`コントロールは、ユーザーが型し、リスト内の値を内容と一致するテキストを自動的に完了します。 場合<xref:System.Windows.Forms.DomainUpDown.Wrap%2A>に設定されている`true`、スクロールの過去の最後の項目をクリックすると、一覧で、その逆の最初の項目。 コントロールの主要なメソッドは<xref:System.Windows.Forms.DomainUpDown.UpButton%2A>と<xref:System.Windows.Forms.DomainUpDown.DownButton%2A>です。  
  
 このコントロールには、テキスト文字列のみが表示されます。 数値を表示するコントロールを実行する場合に、使用、<xref:System.Windows.Forms.NumericUpDown>コントロール。 詳細については、次を参照してください。 [NumericUpDown コントロールの概要](../../../../docs/framework/winforms/controls/numericupdown-control-overview-windows-forms.md)です。  
  
## <a name="see-also"></a>関連項目  
 <xref:System.Windows.Forms.DomainUpDown>  
 [DomainUpDown コントロール](../../../../docs/framework/winforms/controls/domainupdown-control-windows-forms.md)
