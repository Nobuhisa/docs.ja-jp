---
title: "カスタム コントロールのアプリケーション設定"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-winforms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- custom controls [Windows Forms], application settings
- application settings [Windows Forms], custom controls
ms.assetid: f44afb74-76cc-44f2-890a-44b7cdc211a1
caps.latest.revision: "13"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: 3f8292ac459a2943376229ef62466b0a772430dc
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="application-settings-for-custom-controls"></a>カスタム コントロールのアプリケーション設定
カスタム コントロールのコントロールがサード パーティ製のアプリケーションでホストされているときに、アプリケーションの設定を保存する機能を提供する特定のタスクを完了する必要があります。  
  
 アプリケーション設定機能についてのドキュメントのほとんどは、スタンドアロンのアプリケーションを作成していることを前提として書き込まれます。 ただし場合は、アプリケーションで他の開発者がホストするコントロールを作成する必要があります、コントロールがその設定を保持するためのいくつかの追加手順を実行する適切です。  
  
## <a name="application-settings-and-custom-controls"></a>アプリケーションの設定とカスタム コントロール  
 その設定を正しく維持する目的のコントロールの必要がありますをカプセル化プロセスから派生した、設定のラッパー クラスの独自の専用のアプリケーションを作成することで<xref:System.Configuration.ApplicationSettingsBase>です。 また、メイン コントロール クラスを実装する必要があります、<xref:System.Configuration.IPersistComponentSettings>です。 インターフェイスには、いくつかのプロパティだけでなく 2 つのメソッドが含まれています。<xref:System.Configuration.IPersistComponentSettings.LoadComponentSettings%2A>と<xref:System.Configuration.IPersistComponentSettings.SaveComponentSettings%2A>です。 使用して、フォームにコントロールを追加する場合、 **Windows フォーム デザイナー** Visual Studio で、Windows フォームが呼び出す<xref:System.Configuration.IPersistComponentSettings.LoadComponentSettings%2A>以外のコントロールが初期化される場合に自動的に呼び出す必要があります<xref:System.Configuration.IPersistComponentSettings.SaveComponentSettings%2A>で自分自身、 `Dispose`コントロールのメソッドです。  
  
 さらに、Visual Studio などのデザイン時環境で正しく動作するカスタム コントロールのアプリケーション設定の順序で、次を実装する必要があります。  
  
1.  受け取るコンス トラクターを持つカスタム アプリケーション設定クラス、<xref:System.ComponentModel.IComponent>として 1 つのパラメーターです。 保存し、すべてのアプリケーションの設定を読み込むには、このクラスを使用します。 このクラスの新しいインスタンスを作成するときは、コンス トラクターを使用して、カスタム コントロールを渡します。  
  
2.  コントロールを作成し、フォームのように、フォームに配置した後、このカスタム設定クラスを作成する<xref:System.Windows.Forms.Form.Load>イベント ハンドラー。  
  
 カスタム設定クラスを作成する方法の詳細については、次を参照してください。[する方法: アプリケーション設定の作成](../../../../docs/framework/winforms/advanced/how-to-create-application-settings.md)です。  
  
## <a name="settings-keys-and-shared-settings"></a>設定キーと共有設定  
 一部のコントロールを同じフォーム内で複数回使用できます。 ほとんどの場合、これらのコントロールを各自の設定を保持します。 <xref:System.Configuration.IPersistComponentSettings.SettingsKey%2A>プロパティ<xref:System.Configuration.IPersistComponentSettings>フォーム上のコントロールの複数のバージョンを区別するために機能する一意の文字列を指定することができます。  
  
 実装する最も簡単な方法<xref:System.Configuration.IPersistComponentSettings.SettingsKey%2A>を使用して、<xref:System.Windows.Forms.Control.Name%2A>のコントロールのプロパティ、<xref:System.Configuration.IPersistComponentSettings.SettingsKey%2A>です。 値を渡すロードまたはコントロールの設定を保存するときに<xref:System.Configuration.IPersistComponentSettings.SettingsKey%2A>に、<xref:System.Configuration.ApplicationSettingsBase.SettingsKey%2A>のプロパティ、<xref:System.Configuration.ApplicationSettingsBase>クラスです。 アプリケーションの設定は、XML へのユーザーの設定が引き続き発生するときに、この一意のキーを使用します。 次のコード例に示す方法、`<userSettings>`セクションという名前のカスタム コントロールのインスタンスを検索`CustomControl1`の設定を保存するその`Text`プロパティです。  
  
```xml  
<userSettings>  
    <CustomControl1>  
        <setting name="Text" serializedAs="string">  
            <value>Hello, World</value>  
        </setting>  
    </CustomControl1>  
</userSettings>  
```  
  
 値を指定しない、コントロールのすべてのインスタンス<xref:System.Configuration.ApplicationSettingsBase.SettingsKey%2A>同じ設定で共有されます。  
  
## <a name="see-also"></a>関連項目  
 <xref:System.Configuration.ApplicationSettingsBase>  
 <xref:System.Configuration.IPersistComponentSettings>  
 [アプリケーション設定アーキテクチャ](../../../../docs/framework/winforms/advanced/application-settings-architecture.md)
