---
title: 4212 - LockRetryTimeout
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d4ad415a-9871-49fc-85b8-8ee2ea149b1d
caps.latest.revision: "2"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: abe1f560cc984551f069a75873a7e5545aec03cf
ms.sourcegitcommit: ce279f2d7fe2220e6ea0a25a8a7a5370ddf8d9f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2017
---
# <a name="4212---lockretrytimeout"></a>4212 - LockRetryTimeout
## <a name="properties"></a>プロパティ  
  
|||  
|-|-|  
|ID|4212|  
|キーワード|WFInstanceStore|  
|レベル|警告|  
|チャネル|Microsoft-Windows-Application Server-Applications/Debug|  
  
## <a name="description"></a>説明  
 SQL プロバイダーはインスタンス ロックを取得しようとしてタイムアウトを検出しました。  
  
## <a name="message"></a>メッセージ  
 インスタンス ロックを取得しようとしてタイムアウトになりました。  割り当てられたタイムアウト時間 %1 内に操作が完了しませんでした。 この操作に割り当てられた時間は、より長いタイムアウト時間の一部であった可能性があります。  
  
## <a name="details"></a>詳細  
  
|データ項目名|データ項目の型|説明|  
|--------------------|--------------------|-----------------|  
|Delay|xs:string|再試行の遅延。|  
|AppDomain|xs:string|AppDomain.CurrentDomain.FriendlyName で返される文字列。|
