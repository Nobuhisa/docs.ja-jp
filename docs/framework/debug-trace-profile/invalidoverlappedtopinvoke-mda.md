---
title: "invalidOverlappedToPinvoke MDA | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "overlapped pointers"
  - "managed debugging assistants (MDAs), overlapped pointers"
  - "invalid overlapped pointer to platform invoke"
  - "InvalidOverlappedToPinvoke MDA"
  - "MDAs (managed debugging assistants), overlapped pointers"
  - "pointers, overlapped"
ms.assetid: 28876047-58bd-4fed-9452-c7da346d67c0
caps.latest.revision: 14
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 14
---
# invalidOverlappedToPinvoke MDA
`invalidOverlappedToPinvoke` マネージ デバッグ アシスタント \(MDA: Managed Debugging Assistant\) は、ガベージ コレクション ヒープで作成されていないオーバーラップ ポインターが特定の Win32 関数に渡されるとアクティブになります。  
  
> [!NOTE]
>  既定では、この MDA は、プラットフォームの起動の呼び出しがコードで定義され、デバッガーが各メソッドの JustMyCode 状態をレポートする場合にのみアクティブになります。  JustMyCode を理解しないデバッガー \(拡張機能なしの MDbg.exe など\) は、この MDA をアクティブにしません。  このようなデバッガーに対してこの MDA を有効にするには、構成ファイルを使用し、.mda.config ファイルで `justMyCode="false"` を明示的に設定します`(<invalidOverlappedToPinvoke enable="true" justMyCode="false"/>`\)。  
  
## 症状  
 クラッシュまたは説明のつかないヒープ破損。  
  
## 原因  
 ガベージ コレクション ヒープで作成されていないオーバーラップ ポインターが特定のオペレーティング システム関数に渡されています。  
  
 この MDA が追跡する関数を次の表に示します。  
  
|モジュール|関数|  
|-----------|--------|  
|HttpApi.dll|`HttpReceiveHttpRequest`|  
|IpHlpApi.dll|`NotifyAddrChange`|  
|kernel32.dll|`ReadFile`|  
|kernel32.dll|`ReadFileEx`|  
|kernel32.dll|`WriteFile`|  
|kernel32.dll|`WriteFileEx`|  
|kernel32.dll|`ReadDirectoryChangesW`|  
|kernel32.dll|`PostQueuedCompletionStatus`|  
|MSWSock.dll|`ConnectEx`|  
|WS2\_32.dll|`WSASend`|  
|WS2\_32.dll|`WSASendTo`|  
|WS2\_32.dll|`WSARecv`|  
|WS2\_32.dll|`WSARecvFrom`|  
|MQRT.dll|`MQReceiveMessage`|  
  
 呼び出しを行う <xref:System.AppDomain> がアンロードされる可能性があるため、この条件ではヒープが破損する可能性が高くなります。  <xref:System.AppDomain> がアンロードされると、アプリケーション コードがオーバーラップ ポインター用メモリを解放するため、操作終了時に破損が発生します。または、コードによってメモリ リークが発生し、後で問題となります。  
  
## 解決策  
 <xref:System.Threading.Overlapped> オブジェクトを使用して <xref:System.Threading.Overlapped.Pack%2A> メソッドを呼び出し、関数に渡すことができる <xref:System.Threading.NativeOverlapped> 構造体を取得します。  <xref:System.AppDomain> がアンロードされると、CLR は非同期操作が完了するのを待ってからポインターを解放します。  
  
## ランタイムへの影響  
 この MDA は CLR に影響しません。  
  
## 出力  
 この MDA からの出力の例を次に示します。  
  
 `An overlapped pointer (0x00ea3430) that was not allocated on the GC heap was passed via Pinvoke to the Win32 function 'WriteFile' in module 'KERNEL32.DLL'.  If the AppDomain is shut down, this can cause heap corruption when the async I/O completes.  The best solution is to pass a NativeOverlapped structure retrieved from a call to System.Threading.Overlapped.Pack().  If the AppDomain exits, the CLR will keep this structure alive and pinned until the I/O completes.`  
  
## 構成  
  
```  
<mdaConfig>  
  <assistants>  
    <invalidOverlappedToPinvoke/>  
  </assistants>  
</mdaConfig>  
```  
  
## 参照  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute>   
 [Diagnosing Errors with Managed Debugging Assistants](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)   
 [相互運用マーシャリング](../../../docs/framework/interop/interop-marshaling.md)