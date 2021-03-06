---
title: "IMetaDataAssemblyImport::GetAssemblyProps メソッド"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IMetaDataAssemblyImport.GetAssemblyProps
api_location: mscoree.dll
api_type: COM
f1_keywords: IMetaDataAssemblyImport::GetAssemblyProps
helpviewer_keywords:
- GetAssemblyProps method [.NET Framework metadata]
- IMetaDataAssemblyImport::GetAssemblyProps method [.NET Framework metadata]
ms.assetid: 0eaa4aa9-9441-444a-920c-e4b2a2db899e
topic_type: apiref
caps.latest.revision: "12"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: f3ff9c66d483392823a1cc95163e4d5e7e81a364
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2017
---
# <a name="imetadataassemblyimportgetassemblyprops-method"></a>IMetaDataAssemblyImport::GetAssemblyProps メソッド
指定したメタデータ シグネチャを持つアセンブリのプロパティのセットを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
HRESULT GetAssemblyProps (  
    [in]  mdAssembly          mda,  
    [out] const void          **ppbPublicKey,   
    [out] ULONG               *pcbPublicKey,  
    [out] ULONG               *pulHashAlgId,  
    [out] LPWSTR              szName,  
    [in] ULONG                cchName,  
    [out] ULONG               *pchName,  
    [out] ASSEMBLYMETADATA    *pMetaData,  
    [out] DWORD               *pdwAssemblyFlags  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `mda`  
 [in] です。 `mdAssembly`プロパティを取得する対象のアセンブリを表すメタデータ トークン。  
  
 `ppbPublicKey`  
 [out]公開キーまたはメタデータ トークンへのポインター。  
  
 `pcbPublicKey`  
 [out]返されたパブリック キー内のバイト数。  
  
 `pulHashAlgId`  
 [out]アセンブリ内のファイルのハッシュに使用されるアルゴリズムへのポインター。  
  
 `szName`  
 [out]アセンブリの簡易名。  
  
 `cchName`  
 [in]ワイド文字単位のサイズの`szName`します。  
  
 `pchName`  
 [out]実際に返されるワイド文字数`szName`です。  
  
 `pMetaData`  
 [out]アセンブリのメタデータを含む ASSEMBLYMETADATA 構造体へのポインター。  
  
 `pdwAssemblyFlags`  
 [out]アセンブリに適用されるメタデータを記述するフラグ。 この値は 1 つまたは複数の組み合わせ[CorAssemblyFlags](../../../../docs/framework/unmanaged-api/metadata/corassemblyflags-enumeration.md)値。  
  
## <a name="requirements"></a>要件  
 **プラットフォーム:**を参照してください[システム要件](../../../../docs/framework/get-started/system-requirements.md)です。  
  
 **ヘッダー:** Cor.h  
  
 **ライブラリ:** MsCorEE.dll にリソースとして使用  
  
 **.NET framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目  
 [IMetaDataAssemblyImport インターフェイス](../../../../docs/framework/unmanaged-api/metadata/imetadataassemblyimport-interface.md)
