---
title: 214 - OperationCompleted
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a6287eef-023f-4816-813c-1802c82366df
caps.latest.revision: "5"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: 09a8dc1994da30c0f0c180640e3f66c8806e4528
ms.sourcegitcommit: ce279f2d7fe2220e6ea0a25a8a7a5370ddf8d9f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2017
---
# <a name="214---operationcompleted"></a>214 - OperationCompleted
## <a name="properties"></a>プロパティ  
  
|||  
|-|-|  
|ID|214|  
|キーワード|HealthMonitoring、EndToEndMonitoring、Troubleshooting、ServiceModel|  
|レベル|情報|  
|チャネル|Microsoft-Windows-Application Server-Applications/Analytic|  
  
## <a name="description"></a>説明  
 このイベントは、サービス モデルの既定の `OperationInvoker` が、メソッドから例外がスローされることなく、メソッドへの呼び出しを完了したときに生成されます。  
  
## <a name="message"></a>メッセージ  
 OperationInvoker がメソッド '%1' への呼び出しを完了しました。 メソッド呼び出し時間は '%2' ミリ秒でした。  
  
## <a name="details"></a>詳細  
  
|データ項目名|データ項目の型|説明|  
|--------------------|--------------------|-----------------|  
|メソッド名|`xs:string`|`OperationInvoker` によって呼び出されたメソッドの CLR 名。|  
|存続期間|`xs:long`|`OperationInvoker` でメソッドを呼び出すのにかかった時間 (ミリ秒単位)。|  
|HostReference|`xs:string`|Web ホスト サービスの場合は、このフィールドにより、サービスが Web 階層内で一意に識別されます。 その形式とは見なさ ' Web サイト名アプリケーション仮想パス &#124;です。サービス仮想パス &#124;です。ServiceName' です。 例: ' 既定の Web サイト/CalculatorApplication &#124;/CalculatorService.svc &#124;です。CalculatorService'。|  
|AppDomain|`xs:string`|AppDomain.CurrentDomain.FriendlyName で返される文字列。|
