---
title: ReliableSessionBindingElement
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: effda125-b8d3-4de6-8c0e-f59f5ea8f6eb
caps.latest.revision: "11"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: 35a8a92ca93525c9f04ab984073ca64188f03284
ms.sourcegitcommit: ce279f2d7fe2220e6ea0a25a8a7a5370ddf8d9f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2017
---
# <a name="reliablesessionbindingelement"></a>ReliableSessionBindingElement
ReliableSessionBindingElement  
  
## <a name="syntax"></a>構文  
  
```  
class ReliableSessionBindingElement : BindingElement  
{  
  datetime AcknowledgementInterval;  
  boolean FlowControlEnabled;  
  datetime InactivityTimeout;  
  sint32 MaxPendingChannels;  
  sint32 MaxRetryCount;  
  sint32 MaxTransferWindowSize;  
  boolean Ordered;  
  integer ReliableMessagingVersion;  
};  
```  
  
## <a name="methods"></a>メソッド  
 ReliableSessionBindingElement クラスは、メソッドを一切定義しません。  
  
## <a name="properties"></a>プロパティ  
 ReliableSessionBindingElement クラスには、次のプロパティがあります。  
  
### <a name="acknowledgementinterval"></a>AcknowledgementInterval  
 データ型 : datetime  
  
 アクセスの種類 : 読み取り専用  
  
 ファクトリによって作成された信頼できるチャネルで、メッセージの送信元に受信確認を送信するまで送信先が待機する時間  
  
### <a name="flowcontrolenabled"></a>FlowControlEnabled  
 データ型 : boolean  
  
 アクセスの種類 : 読み取り専用  
  
 フロー制御を有効にするかどうかを示すブール値  
  
### <a name="inactivitytimeout"></a>InactivityTimeout  
 データ型 : datetime  
  
 アクセスの種類 : 読み取り専用  
  
 他の通信相手がチャネルにメッセージを送信せずにいられる最長期間を指定します。他の通信相手がメッセージを送信しない期間がこの値を超えると、チャネルでエラーが発生します。  
  
### <a name="maxpendingchannels"></a>MaxPendingChannels  
 データ型 : sint32  
  
 アクセスの種類 : 読み取り専用  
  
 リスナーで受け入れを待機できるチャネルの最大数。  
  
### <a name="maxretrycount"></a>MaxRetryCount  
 データ型 : sint32  
  
 アクセスの種類 : 読み取り専用  
  
 基になるチャネルで `Send` を呼び出すことで、信頼できるチャネルが受信確認を受信していないメッセージの再転送を試みる最大回数  
  
### <a name="maxtransferwindowsize"></a>MaxTransferWindowSize  
 データ型 : sint32  
  
 アクセスの種類 : 読み取り専用  
  
 信頼できるセッションの転送ウィンドウの最大サイズ  
  
### <a name="ordered"></a>順序あり  
 データ型 : boolean  
  
 アクセスの種類 : 読み取り専用  
  
 メッセージが送信された順序で到着されることを保証するかどうかを指定するブール値です。  
  
### <a name="reliablemessagingversion"></a>ReliableMessagingVersion  
 データ型 : integer  
  
 アクセスの種類 : 読み取り専用  
  
 信頼できるセッションで使用される WS-ReliableMessaging プロトコルのバージョンを指定する整数。  
  
## <a name="requirements"></a>要件  
  
|MOF|Servicemodel.mof にて宣言済み。|  
|---------|-----------------------------------|  
|Namespace|root\ServiceModel で定義|  
  
## <a name="see-also"></a>関連項目  
 <xref:System.ServiceModel.Channels.ReliableSessionBindingElement>
