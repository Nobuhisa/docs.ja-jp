---
title: "ICLRDataTarget::GetCurrentThreadID メソッド"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICLRDataTarget.GetCurrentThreadID
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICLRDataTarget::GetCurrentThreadID
helpviewer_keywords:
- GetCurrentThreadID method, ICLRDataTarget interface [.NET Framework debugging]
- ICLRDataTarget::GetCurrentThreadID method [.NET Framework debugging]
ms.assetid: dc9a0a6c-d592-4fb7-86ed-62684da3b0e1
topic_type: apiref
caps.latest.revision: "10"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 3820a3f32834f02b60fb33448bcaf8febdc15ce6
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2017
---
# <a name="iclrdatatargetgetcurrentthreadid-method"></a>ICLRDataTarget::GetCurrentThreadID メソッド
現在のスレッドのオペレーティング システムの識別子を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
HRESULT GetCurrentThreadID (  
    [out] ULONG32    *threadID  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `threadID`  
 [out]ターゲット プロセスの現在のスレッドのオペレーティング システム識別子へのポインター。  
  
## <a name="remarks"></a>コメント  
 ターゲット プロセスでは、現在のスレッドが存在しない場合、`GetCurrentThreadID`メソッドが失敗する可能性があります。  
  
## <a name="requirements"></a>要件  
 **プラットフォーム:**を参照してください[システム要件](../../../../docs/framework/get-started/system-requirements.md)です。  
  
 **ヘッダー:** ClrData.idl、ClrData.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目  
 [ICLRDataTarget インターフェイス](../../../../docs/framework/unmanaged-api/debugging/iclrdatatarget-interface.md)
