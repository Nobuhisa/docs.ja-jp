---
title: "ICorDebugModule3 インターフェイス"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugModule3
api_location: CorDebug.dll
api_type: COM
f1_keywords: ICorDebugModule3
helpviewer_keywords: ICorDebugModule3 interface [.NET Framework debugging]
ms.assetid: 0b69f945-263a-4e11-8512-89d27f6ea296
topic_type: apiref
caps.latest.revision: "9"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: f6ef8314329aba60d8c23c6f00725192d83961ec
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="icordebugmodule3-interface"></a>ICorDebugModule3 インターフェイス
動的モジュールのシンボル リーダーを作成します。  
  
## <a name="syntax"></a>構文  
  
```  
interface ICorDebugModule3 : IUnknown  
{  
    HRESULT CreateReaderForInMemorySymbols  
      (  
      [in] REFIID riid,  
      [out][iid_is(riid)] void **  ppObj  
      );  
};  
```  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[Icordebugmodule 3::createreaderforinmemorysymbols メソッド](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule3-createreaderforinmemorysymbols-method.md)|シンボル リーダーの作成 (通常[ISymUnmanagedReader インターフェイス](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedreader-interface.md)) の動的モジュール。|  
  
## <a name="remarks"></a>コメント  
 このインターフェイスは、"ICorDebugModule"および"ICorDebugModule2"インターフェイスを論理的に拡張します。  
  
> [!NOTE]
>  このインターフェイスは、コンピューター間またはプロセス間でのリモート呼び出しをサポートしていません。  
  
## <a name="requirements"></a>要件  
 **プラットフォーム:**を参照してください[システム要件](../../../../docs/framework/get-started/system-requirements.md)です。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET framework のバージョン:**4.5、4、3.5 SP1  
  
## <a name="see-also"></a>関連項目  
 [ICorDebugRemoteTarget インターフェイス](../../../../docs/framework/unmanaged-api/debugging/icordebugremotetarget-interface.md)  
 [ICorDebug インターフェイス](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md)  
    
 [デバッグのインターフェイス](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
