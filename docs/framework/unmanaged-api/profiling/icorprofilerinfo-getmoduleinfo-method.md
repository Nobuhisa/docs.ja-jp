---
title: "ICorProfilerInfo::GetModuleInfo メソッド"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorProfilerInfo.GetModuleInfo
api_location: mscorwks.dll
api_type: COM
f1_keywords: ICorProfilerInfo::GetModuleInfo
helpviewer_keywords:
- GetModuleInfo method [.NET Framework profiling]
- ICorProfilerInfo::GetModuleInfo method [.NET Framework profiling]
ms.assetid: 5a90d16f-7929-4987-8f83-a631becf564d
topic_type: apiref
caps.latest.revision: "20"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 23dc0208b4537530f18c2c282fbe8c3495ba301f
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="icorprofilerinfogetmoduleinfo-method"></a>ICorProfilerInfo::GetModuleInfo メソッド
モジュール ID を指定して、モジュールのファイル名とモジュールの親アセンブリの ID を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
HRESULT GetModuleInfo(  
    [in]  ModuleID   moduleId,  
    [out] LPCBYTE    *ppBaseLoadAddress,  
    [in]  ULONG      cchName,  
    [out] ULONG      *pcchName,  
    [out, size_is(cchName), length_is(*pcchName)]  
          WCHAR      szName[] ,  
    [out] AssemblyID *pAssemblyId);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `moduleId`  
 [in] 情報が取得されるモジュールの ID。  
  
 `ppBaseLoadAddress`  
 [out] モジュールが読み込まれるベース アドレス。  
  
 `cchName`  
 [in] `szName` 戻りバッファーの長さ (文字単位)。  
  
 `pcchName`  
 [out] 返されるモジュールのファイル名の文字列長の合計へのポインター。  
  
 `szName`  
 [out] 呼び出し元が提供したワイド文字バッファー。 メソッドから制御が戻るとき、このバッファーにモジュールのファイル名が格納されます。  
  
 `pAssemblyId`  
 [out] モジュールの親アセンブリ ID へのポインター。  
  
## <a name="remarks"></a>コメント  
 動的モジュールの場合、`szName` パラメーターは空の文字列、ベース アドレスは 0 (ゼロ) になります。  
  
 ただし、`GetModuleInfo`モジュールの ID が存在するとすぐに、メソッドを呼び出すことができます、プロファイラーを受け取るまで、親アセンブリの ID は使用できません、 [icorprofilercallback::moduleattachedtoassembly](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-moduleattachedtoassembly-method.md)コールバック。  
  
 `GetModuleInfo` から制御が戻ったら、`szName` バッファーのサイズが十分で、モジュールのファイル名全体を格納できたかどうかを確認する必要があります。 これを行うには、`pcchName` が指している値を `cchName` パラメーターの値と比較します。 `pcchName` が指している値が `cchName` の値より大きい場合は、`szName` バッファーの割り当てを増やし、`cchName` を新しい大きいサイズに更新して、`GetModuleInfo` を再度呼び出します。  
  
 別の方法として、最初に長さ 0 の `szName` バッファーで `GetModuleInfo` を呼び出すことで、適切なバッファーのサイズを取得することもできます。 その後、バッファーのサイズを `pcchName` で返された値に設定し、`GetModuleInfo` を再度呼び出します。  
  
## <a name="requirements"></a>要件  
 **プラットフォーム:**を参照してください[システム要件](../../../../docs/framework/get-started/system-requirements.md)です。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目  
 [ICorProfilerInfo インターフェイス](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)  
 [プロファイリングのインターフェイス](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)  
 [プロファイル](../../../../docs/framework/unmanaged-api/profiling/index.md)  
 [GetModuleInfo2 メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getmoduleinfo2-method.md)
