---
title: "使用して &#39;FileGetObject &#39;代わりに &#39;です。FileGet &#39;型 &#39; オブジェクト &#39; の引数を使用する場合"
ms.date: 07/20/2015
ms.prod: .net
ms.technology: devlang-visual-basic
ms.topic: article
ms.assetid: 090b8088-895a-482a-9362-606596bac304
caps.latest.revision: "9"
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: 996e8a50f90c738bbc64c200125a785c0e9bcd58
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="use-39filegetobject39-instead-of-39fileget39-when-using-argument-of-type-39object39"></a>使用して &#39;FileGetObject &#39;代わりに &#39;です。FileGet &#39;型 &#39; オブジェクト &#39; の引数を使用する場合
`FileGet` メソッドには、型 `Object`の引数が含まれています。 あいまいさを避けるため、`FileGetObject` の代わりに `FileGet` を使用する必要があります。  
  
 `My.Computer.Filesystem` によって提供される機能は、 `FileGet` または `FileGetObject`よりも使いやすく、パフォーマンスが優れています。  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
1.  `FileGet` を `FileGetObject`に置き換えます。  
  
2.  `Object` 引数をより具体的な種類にキャストします。  
  
## <a name="see-also"></a>関連項目  
 [ビルド内にありません: FileGetObject 関数](http://msdn.microsoft.com/en-us/3eda786b-d1ee-4b44-9dd7-0ea6bff072c0)  
 [My.Computer.FileSystem オブジェクト](../../visual-basic/language-reference/objects/my-computer-filesystem-object.md)
