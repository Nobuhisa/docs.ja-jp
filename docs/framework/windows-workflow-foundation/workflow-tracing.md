---
title: "ワークフロー トレース"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 18737989-0502-4367-b5f6-617ebfb77c96
caps.latest.revision: "12"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: 7cc400c2925d1a4a1810780528bad6da3ad492eb
ms.sourcegitcommit: ce279f2d7fe2220e6ea0a25a8a7a5370ddf8d9f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2017
---
# <a name="workflow-tracing"></a>ワークフロー トレース
ワークフロー トレースでは、.NET Framework のトレース リスナーを使用して診断情報を取得できます。 トレースは、アプリケーションで問題が検出された場合に有効にし、その問題が解決されたら、再度無効にすることが可能です。 ワークフローのデバッグ トレースを有効にする方法は 2 つあります。 また、イベント トレース ビューアーを使用してトレースを構成したり、<xref:System.Diagnostics> を使用してトレース イベントをファイルに送信したりすることができます。  
  
## <a name="enabling-debug-tracing-in-etw"></a>ETW でのデバッグ トレースの有効化  
 ETW を使用してトレースを有効化するには、次の手順に従ってイベント ビューアーでデバッグ チャネルを有効化します。  
  
1.  イベント ビューアーで分析ログおよびデバッグ ログのノードに移動します。  
  
2.  イベント ビューアーのツリー ビューに移動**イベント ビューアー] の [アプリケーションとサービス ログ] の [Microsoft]-> [Windows アプリケーション サーバー-アプリケーション]-> [**です。 右クリック**アプリケーション サーバー-アプリケーション**選択**ビューでは、分析およびデバッグ ログ->** です。 右クリック**デバッグ**選択**ログの有効化**です。  
  
3.  ワークフローがデバッグを実行し、トレースが ETW デバッグ チャネルに出力されると、トレースをイベント ビューアーで参照できます。 移動**イベント ビューアー] の [アプリケーションとサービス ログ] の [Microsoft]-> [Windows アプリケーション サーバー-アプリケーション]-> [**です。 右クリック**デバッグ**選択**更新**です。  
  
4.  既定の分析トレースのバッファー サイズは 4 KB ですが、このサイズを 32 KB に増やすことをお勧めします。 これを行うには、次の手順を実行します。  
  
    1.  現在のフレームワークのディレクトリ (C:\Windows\Microsoft.NET\Framework\v4.0.21203 など) で、次のコマンドを実行します。`wevtutil um Microsoft.Windows.ApplicationServer.Applications.man`  
  
    2.  変更、 \<bufferSize > 32 Windows.ApplicationServer.Applications.man ファイル内の値。  
  
        ```xml  
        <channel name="Microsoft-Windows-Application Server-Applications/Analytic" chid="ANALYTIC_CHANNEL" symbol="ANALYTIC_CHANNEL" type="Analytic" enabled="false" isolation="Application" message="$(string.MICROSOFT_WINDOWS_APPLICATIONSERVER_APPLICATIONS.channel.ANALYTIC_CHANNEL.message)" >  
                    <publishing>  
                      <bufferSize>32</bufferSize>  
                    </publishing>  
                  </channel>  
        ```  
  
    3.  現在のフレームワークのディレクトリ (C:\Windows\Microsoft.NET\Framework\v4.0.21203 など) で、次のコマンドを実行します。`wevtutil im Microsoft.Windows.ApplicationServer.Applications.man`  
  
> [!NOTE]
>  .NET Framework 4 Client Profile を使用している場合は、.NET Framework 4 ディレクトリから次のコマンドを実行して ETW マニフェストを登録する必要がありますまず。`ServiceModelReg.exe –i –c:etw`  
  
## <a name="enabling-debug-tracing-using-systemdiagnostics"></a>System.Diagnostics によるデバッグ トレースの有効化  
 これらのリスナーは、ワークフロー アプリケーションの App.config ファイルまたはワークフロー サービスの Web.config ファイルで構成します。 この例では、 [TextWriterTraceListener](http://go.microsoft.com/fwlink/?LinkId=165424)現在のディレクトリで MyTraceLog.txt ファイルにトレース情報を保存するように構成します。  
  
```xml  
<configuration>  
  <system.diagnostics>  
    <sources>  
      <source name="System.Activities" switchValue="Information">  
        <listeners>  
          <add name="textListener" />  
          <remove name="Default" />  
        </listeners>  
      </source>  
    </sources>  
    <sharedListeners>  
      <add name="textListener"  
           type="System.Diagnostics.TextWriterTraceListener"  
           initializeData="MyTraceLog.txt"  
           traceOutputOptions="ProcessId, DateTime" />  
    </sharedListeners>  
    <trace autoflush="true" indentsize="4">  
      <listeners>  
        <add name="textListener" />  
      </listeners>  
    </trace>  
  </system.diagnostics>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目  
 [Windows Server App Fabric の監視](http://go.microsoft.com/fwlink/?LinkId=201273)  
 [アプリケーション App Fabric の監視](http://go.microsoft.com/fwlink/?LinkId=201275)
