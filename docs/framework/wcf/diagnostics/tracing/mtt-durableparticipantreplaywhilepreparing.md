---
title: Microsoft.Transactions.TransactionBridge.DurableParticipantReplayWhilePreparing
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 10ef3876-6f8e-4d4e-8444-f47847b64795
caps.latest.revision: "5"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: 830a55a9f82c38b0a58783c49d3f58f64d5afdb4
ms.sourcegitcommit: ce279f2d7fe2220e6ea0a25a8a7a5370ddf8d9f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2017
---
# <a name="microsofttransactionstransactionbridgedurableparticipantreplaywhilepreparing"></a>Microsoft.Transactions.TransactionBridge.DurableParticipantReplayWhilePreparing
WS-AT プロトコル サービスは、準備メッセージに応答していない永続的な参加要素から、リプレイ メッセージを受信しました。 そのため、トランザクションが中止されました。  
  
## <a name="description"></a>説明  
 永続的な参加要素がまだ準備している間にリプレイ メッセージが受信された場合は、トレースされます。 これは、この状態に対して無効なメッセージであり、トランザクションは中止されます。  
  
## <a name="troubleshooting"></a>トラブルシューティング  
 このエラー メッセージは、永続的な参加要素 (下位トランザクション マネージャーを含む) がエラーから回復したが、トランザクション結果が不明であるため、状態を要求していることを示している場合があります。  
  
## <a name="see-also"></a>関連項目  
 [トレース](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)  
 [トレースを使用して、アプリケーションのトラブルシューティング](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)  
 [管理と診断](../../../../../docs/framework/wcf/diagnostics/index.md)
