---
title: "抽象クラスのデザイン"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- type design guidelines, abstract classes
- abstract classes, design guidelines
- class library design guidelines [.NET Framework], classes
- classes [.NET Framework], abstract
- classes [.NET Framework], design guidelines
- type design guidelines, classes
ms.assetid: d3646e6d-5c1f-4922-8fb0-ec5effb30d60
caps.latest.revision: "13"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: d7b680c3377cbfa40734a57f9408d9487dbf3769
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="abstract-class-design"></a>抽象クラスのデザイン
**X しないで**抽象型の public または protected のコンス トラクター内部を定義します。  
  
 コンス トラクターは、ユーザーが型のインスタンスを作成する必要がある場合にのみ、パブリックにする必要があります。 抽象型のインスタンスを作成できないため、パブリック コンス トラクターを持つ抽象型が正しくされていない仕様であり、ユーザーに誤解を招く。  
  
 **✓ しないで**抽象クラス内で、保護されているか、内部のコンス トラクターを定義します。  
  
 プロテクト コンス トラクターより一般的なサブタイプが作成されるときに、独自の初期化を実行する基本クラスでは。  
  
 アセンブリのクラスを定義する抽象クラスの具象実装を制限する、内部のコンス トラクターを使用できます。  
  
 **✓ しないで**を出荷する各の抽象クラスから継承する少なくとも 1 つの具象型を提供します。  
  
 抽象クラスの設計を検証するには、これによりを行っています。 たとえば、<xref:System.IO.FileStream?displayProperty=nameWithType>に実装されて、<xref:System.IO.Stream?displayProperty=nameWithType>抽象クラスです。  
  
 *部分 © 2005、2009 Microsoft Corporation します。All rights reserved.*  
  
 *ピアソン教育, Inc. からのアクセス許可によって検出[Framework デザイン ガイドライン: 規則、表現方法、および再利用可能な .NET ライブラリを第 2 版パターン](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619)は Cwalina と Brad Abrams、2008 年 10 月 22 日で発行されました。Microsoft Windows 開発シリーズの一部として、Addison-wesley Professional。*  
  
## <a name="see-also"></a>関連項目  
 [型のデザインのガイドライン](../../../docs/standard/design-guidelines/type.md)  
 [フレームワーク デザインのガイドライン](../../../docs/standard/design-guidelines/index.md)
