---
title: "Using Objects That Implement IDisposable | Microsoft Docs"
ms.custom: ""
ms.date: "04/07/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Dispose method"
  - "try/finally block"
  - "garbage collection, encapsulating resources"
ms.assetid: 81b2cdb5-c91a-4a31-9c83-eadc52da5cf0
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 15
---
# Using Objects That Implement IDisposable
共通言語ランタイムのガベージ コレクターは、アンマネージ オブジェクトによって使用されているメモリを解放しますが、アンマネージ リソースを使用する型は、このアンマネージ メモリが解放されるように <xref:System.IDisposable> インターフェイスを実装します。  <xref:System.IDisposable> を実装するオブジェクトを使い終わったら、オブジェクトの <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> の実装を呼び出す必要があります。  2 つの方法のいずれかでこれを行うことができます。  
  
-   C\# の **using** ステートメントまたは Visual Basic の `Using` ステートメントを使用します。  
  
-   `try`\/`finally` ブロックを実装します。  
  
## using ステートメント  
 C\# の **using** ステートメントおよび Visual Basic の `Using` ステートメントを使うと、オブジェクトの作成時やクリーンアップ時に記述する必要のあるコードが簡略化されます。  **using** ステートメントは、1 つ以上のリソースを取得し、指定されたステートメントを実行し、オブジェクトを自動的に破棄します。  ただし、**using** ステートメントは、オブジェクトが構築されるメソッドのスコープ内で使用されるオブジェクトに対してのみ有効です。  
  
 次の例では、`using` ステートメントを使用して <xref:System.IO.StreamReader?displayProperty=fullName> オブジェクトを作成し解放します。  
  
 [!code-csharp[Conceptual.Disposable#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/using1.cs#1)]
 [!code-vb[Conceptual.Disposable#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/using1.vb#1)]  
  
 <xref:System.IO.StreamReader> クラスは <xref:System.IDisposable> インターフェイスを実装し、これはアンマネージ リソースを使用することを示していますが、例では <xref:System.IO.StreamReader.Dispose%2A?displayProperty=fullName> メソッドを明示的に呼び出していないことに注意してください。  C\# または Visual Basic コンパイラが `using` ステートメントを見つけると、明示的に `try`\/`finally` ブロックを含む次のコードと同等の中間言語 \(IL\) を生成します。  
  
 [!code-csharp[Conceptual.Disposable#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/using3.cs#3)]
 [!code-vb[Conceptual.Disposable#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/using3.vb#3)]  
  
 また、C\# の **using** ステートメントでは、単一のステートメントで複数のリソースを取得できます。そのようなステートメントは、内部的には複数の **using** ステートメントを入れ子にした場合と同等です。  次の例では、2 つの異なるファイルの内容を読み取るために、<xref:System.IO.StreamReader> の 2 つのオブジェクトをインスタンス化します。  
  
 [!code-csharp[Conceptual.Disposable#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/using4.cs#4)]  
  
## Try\/Finally ブロック  
 `using` ステートメントで `try`\/`finally` ブロックをラップする代わりに、`try`\/`finally` ブロックを直接実装することもできます。  これは、個人のコーディング スタイルであることも、次のいずれかの理由からそうすることもあります。  
  
-   `try` ブロックでスローされた例外をすべて処理する `catch` ブロックを含めるため。  そうしないと、`try`\/`catch` ブロックがない場合に `using` ブロック内でスローされた例外と同様に、`using` ステートメントによってスローされた例外は処理されません。  
  
-   宣言されたブロックに対してスコープがローカルでない <xref:System.IDisposable> を実装するオブジェクトをインスタンス化するため。  
  
 次の例は前の例に似ていますが、`try`\/`catch`\/`finally` ブロックを使用して、<xref:System.IO.StreamReader> オブジェクトのインスタンス化、使用、破棄を実行し、<xref:System.IO.StreamReader> コンストラクターと <xref:System.IO.StreamReader.ReadToEnd%2A> メソッドによってスローされた例外を処理しています。  <xref:System.IDisposable.Dispose%2A> メソッドを呼び出す前に <xref:System.IDisposable> を実装するオブジェクトが `null` でないことを `finally` ブロックのコードがチェックしていることに注意してください。  これを行わない場合、実行時に <xref:System.NullReferenceException> 例外が発生する可能性があります。  
  
 [!code-csharp[Conceptual.Disposable#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/using5.cs#6)]
 [!code-vb[Conceptual.Disposable#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/using5.vb#6)]  
  
 この基本パターンを利用できるのは、プログラミング言語で `using` ステートメントがサポートされていないが、<xref:System.IDisposable.Dispose%2A> メソッドを直接呼び出すことはできるため、`try`\/`finally` ブロックの実装を選択した場合、または実装する必要がある場合です。  
  
 使用言語が <xref:System.IDisposable.Dispose%2A> メソッドの直接の呼び出しをサポートしていない場合は \(C\+\+ など\)、一般にその言語のデストラクター構文を使用できます。  
  
## 参照  
 [Cleaning Up Unmanaged Resources](../../../docs/standard/garbage-collection/unmanaged.md)   
 [using ステートメント](../Topic/using%20Statement%20\(C%23%20Reference\).md)   
 [Using Statement](../Topic/Using%20Statement%20\(Visual%20Basic\).md)