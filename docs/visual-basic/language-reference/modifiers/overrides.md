---
title: Overrides (Visual Basic)
ms.date: 07/20/2015
ms.prod: .net
ms.suite: 
ms.technology: devlang-visual-basic
ms.topic: article
f1_keywords:
- Overrides
- vb.Overrides
helpviewer_keywords:
- properties [Visual Basic], redefining
- procedures [Visual Basic], overriding
- procedures [Visual Basic], redefining
- overriding
- Overrides keyword [Visual Basic]
- overriding, Overrides keyword
- properties [Visual Basic], overriding
ms.assetid: 9f5e6144-ce10-465e-842b-1a8f8760af90
caps.latest.revision: "18"
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: 1bee6a6235b87a7e20f087a73bef76e0fc7bf124
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="overrides-visual-basic"></a>Overrides (Visual Basic)
プロパティまたはプロシージャが基本クラスから継承された同じ名前のプロパティまたはプロシージャをオーバーライドすることを示します。  
  
## <a name="remarks"></a>コメント  
  
## <a name="rules"></a>ルール  
  
-   **宣言コンテキスト。** `Overrides` は、プロパティまたはプロシージャの宣言ステートメントでのみ使用できます。  
  
-   **結合された修飾子。** 同じ宣言内で `Overrides` を `Shadows` または `Shared` と共に指定することはできません。 オーバーライドする要素は暗黙的にオーバーライド可能であるため、`Overridable` と `Overrides` を結合することはできません。  
  
-   **署名が一致します。** この宣言のシグネチャと一致する必要があります、*署名*のプロパティまたはプロシージャをオーバーライドします。 つまり、パラメーター リストには、同じ数のパラメーターを、同じ順序、同じデータ型で指定する必要があります。  
  
     オーバーライドする宣言は、シグネチャに加え、次の点でも完全に一致している必要があります。  
  
    -   アクセス レベル  
  
    -   戻り値の型 (戻り値がある場合)  
  
-   **ジェネリック シグネチャ。** ジェネリック プロシージャでは、シグネチャに型パラメーターの数が含まれます。 したがって、オーバーライドする宣言は、その点でも基底クラスのバージョンに一致している必要があります。  
  
-   **その他の一致。** この宣言は、基底クラスのバージョンのシグネチャに一致していることに加え、次の点でも基底クラスと一致している必要があります。  
  
    -   アクセス レベル修飾子 (など[パブリック](../../../visual-basic/language-reference/modifiers/public.md))  
  
    -   各パラメーターの渡し ([ByVal](../../../visual-basic/language-reference/modifiers/byval.md)または[ByRef](../../../visual-basic/language-reference/modifiers/byref.md))  
  
    -   ジェネリック プロシージャの型パラメーターごとの制約リスト  
  
-   **シャドウとオーバーライドされます。** シャドウとオーバーライドは、どちらも継承された要素を再定義しますが、その方法は大きく異なります。 詳細については、次を参照してください。 [Visual Basic におけるシャドウ](../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)です。  
  
 `Overrides` を使用する場合は、ライブラリ API と C# が連携しやすくなるように、コンパイラが暗黙的に `Overloads` を追加します。  
  
 `Overrides` 修飾子は、次のコンテキストで使用できます。  
  
 [Function ステートメント](../../../visual-basic/language-reference/statements/function-statement.md)  
  
 [Property ステートメント](../../../visual-basic/language-reference/statements/property-statement.md)  
  
 [Sub ステートメント](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## <a name="see-also"></a>関連項目  
 [MustOverride](../../../visual-basic/language-reference/modifiers/mustoverride.md)  
 [NotOverridable](../../../visual-basic/language-reference/modifiers/notoverridable.md)  
 [Overridable](../../../visual-basic/language-reference/modifiers/overridable.md)  
 [キーワード](../../../visual-basic/language-reference/keywords/index.md)  
 [Visual Basic におけるシャドウ](../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)  
 [Visual Basic におけるジェネリック型](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)  
 [型リスト](../../../visual-basic/language-reference/statements/type-list.md)
