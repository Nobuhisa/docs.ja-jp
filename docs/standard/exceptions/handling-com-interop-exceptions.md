---
title: "COM 相互運用の例外の処理"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: error-reference
helpviewer_keywords:
- unmanaged code, exceptions
- exceptions, unmanaged code
- HRESULTs
- exceptions, COM interop
- COM interop, exceptions
ms.assetid: e6104aa8-8e5f-4069-b864-def85579c96c
caps.latest.revision: "11"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: bc3e01bc8ca463460ede9544d1d5c095c39a59d0
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2017
---
# <a name="handling-com-interop-exceptions"></a>COM 相互運用の例外の処理
マネージ コードとアンマネージ コードは、例外を処理するために一緒に操作できます。 マネージ コードでメソッドが例外をスローすると、共通言語ランタイムは、HRESULT を COM オブジェクトに渡すことができます。 アンマネージ コードでメソッドが失敗して、失敗を示す HRESULT を返した場合、ランタイムはマネージ コードでキャッチできる例外をスローします。  
  
 ランタイムは、HRESULT を COM 相互運用からの自動的にマップして、より詳細な例外を取得します。 たとえば、E_ACCESSDENIED は <xref:System.UnauthorizedAccessException> になり、E_OUTOFMEMORY は <xref:System.OutOfMemoryException> になるなどです。  
  
 HRESULT がカスタムの結果であるか、またはランタイムで不明な場合は、ランタイムがジェネリック <xref:System.Runtime.InteropServices.COMException> をクライアントに渡します。 **ErrorCode**のプロパティ、 **COMException** HRESULT 値が含まれています。  
  
## <a name="working-with-ierrorinfo"></a>IErrorInfo の処理  
 エラーが COM からマネージ コードに渡された場合、ランタイムは例外オブジェクトにエラー情報を入れます。 IErrorInfo をサポートして HRESULT を返す COM オブジェクトは、この情報をマネージ コードの例外に提供します。 たとえば、ランタイムは、COM エラーからの説明を例外の <xref:System.Exception.Message%2A> プロパティにマップします。 HRESULT が追加のエラー情報を提供しない場合、ランタイムは例外のプロパティの多くに既定値を指定します。  
  
 アンマネージ コードでメソッドが失敗した場合、例外をマネージ コードのセグメントに渡すことができます。 トピック[の HRESULT と例外](../../../docs/framework/interop/how-to-map-hresults-and-exceptions.md)HRESULT がランタイム例外オブジェクトにマップする方法を示す表が含まれています。  

## <a name="see-also"></a>関連項目
[例外](index.md) 
