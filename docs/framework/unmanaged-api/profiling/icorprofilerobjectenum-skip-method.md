---
title: "ICorProfilerObjectEnum::Skip メソッド"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorProfilerObjectEnum.Skip
api_location: mscorwks.dll
api_type: COM
f1_keywords: ICorProfilerObjectEnum::Skip
helpviewer_keywords:
- ICorProfilerObjectEnum::Skip method [.NET Framework profiling]
- Skip method, ICorProfilerObjectEnum interface [.NET Framework profiling]
ms.assetid: f8e498f8-f93a-4b82-bd22-55bdbf5e8d45
topic_type: apiref
caps.latest.revision: "11"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 84960af6e128f3a6aa9e3b45187e282ac7228e0f
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2017
---
# <a name="icorprofilerobjectenumskip-method"></a>ICorProfilerObjectEnum::Skip メソッド
指定した要素数がスキップされるように、現在の位置からこの列挙子のカーソルを進めます。  
  
## <a name="syntax"></a>構文  
  
```  
HRESULT Skip (  
    [in] ULONG   celt  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `celt`  
 [in]スキップする要素の数。  
  
## <a name="remarks"></a>コメント  
 この列挙子のカーソルの新しい位置は: (現在の位置) +`celt`です。  
  
## <a name="requirements"></a>要件  
 **プラットフォーム:**を参照してください[システム要件](../../../../docs/framework/get-started/system-requirements.md)です。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目  
 [ICorProfilerObjectEnum インターフェイス](../../../../docs/framework/unmanaged-api/profiling/icorprofilerobjectenum-interface.md)
