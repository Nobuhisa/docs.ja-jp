---
title: "Attached and Detached Child Tasks | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "tasks, child tasks"
ms.assetid: c95788bf-90a6-4e96-b7bc-58e36a228cc5
caps.latest.revision: 21
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 21
---
# Attached and Detached Child Tasks
*子タスク* \(または*入れ子のタスク*\) は、<xref:System.Threading.Tasks.Task?displayProperty=fullName>親タスクと呼ばれる、別のタスクのユーザー デリゲートで作成された、 *のインスタンスです。* 子タスクはデタッチまたはアタッチできます。  *デタッチされた子タスク*は、親とは独立して実行されるタスクです。   *アタッチされた子タスク* は、<xref:System.Threading.Tasks.TaskCreationOptions?displayProperty=fullName> オプションで作成される入れ子式のタスクです。その親は、明示的にも既定でも、子タスクがアタッチされることを禁止しません。  タスクでは、システム リソースが許す限り、任意の数のアタッチされた子タスクおよびデタッチされた子タスクを作成できます。  
  
 以下の表に、2 種類の子タスクの基本的な相違点を示します。  
  
|カテゴリ|デタッチされた子タスク|アタッチされた子タスク|  
|----------|-----------------|-----------------|  
|親は子タスクが完了するまで待機します。|いいえ|はい|  
|親は子タスクによってスローされた例外を反映します。|いいえ|はい|  
|親のステータスは子のステータスに依存します。|いいえ|はい|  
  
 ほとんどの場合、デタッチされた子タスクを使用することをお勧めします。他のタスクとの関係は複雑度が低いためです。  こうした理由から、既定では親タスク内に作成されたタスクはデタッチされており、アタッチされた子タスクを作成する場合は <xref:System.Threading.Tasks.TaskCreationOptions?displayProperty=fullName> オプションを明示的に指定する必要があります。  
  
## デタッチされた子タスク  
 子タスクは親タスクによって作成されますが、既定では親タスクに依存しません。  次の例では、親タスクが単に 1 つの子タスクを作成します。  このコード例を複数回実行すると、出力がここに示したものとは異なり、またコードを実行するたびに出力が変わる場合があることに気付くことがあります。  これは親タスクと子タスクが、それぞれ独立して実行されるために生じます。子タスクはデタッチされたタスクです。  この例は親タスクの完了のみを待機します。コンソール アプリが終了する前には、子タスクは実行または完了しないことがあります。  
  
 [!code-csharp[TPL_ChildTasks#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_childtasks/cs/nested1.cs#1)]
 [!code-vb[TPL_ChildTasks#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_childtasks/vb/nested1.vb#1)]  
  
 子タスクが <xref:System.Threading.Tasks.Task%601> オブジェクトではなく <xref:System.Threading.Tasks.Task> オブジェクトによって表される場合、デタッチされた子タスクであっても、子の <xref:System.Threading.Tasks.Task%601.Result%2A?displayProperty=fullName> プロパティにアクセスして、親タスクが子タスクの完了を待機することを確認できます。  次の例に示すように、<xref:System.Threading.Tasks.Task%601.Result%2A> プロパティはタスクが完了するまでブロックします。  
  
 [!code-csharp[TPL_ChildTasks#4](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_childtasks/cs/childtasks.cs#4)]
 [!code-vb[TPL_ChildTasks#4](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_childtasks/vb/tpl_childtasks.vb#4)]  
  
## アタッチされた子タスク  
 デタッチされた子タスクとは異なり、アタッチされた子タスクは親と緊密に同期します。  次の例に示すように、タスクの作成ステートメントで <xref:System.Threading.Tasks.TaskCreationOptions?displayProperty=fullName> オプションを使用すると、前の例のデタッチされた子タスクを、アタッチされた子タスクに変更できます。  このコードでは、アタッチされた子タスクは親の前に完了します。  その結果、この例の出力結果は、コードを実行するたびに同じになります。  
  
 [!code-csharp[TPL_ChildTasks#2](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_childtasks/cs/child1.cs#2)]
 [!code-vb[TPL_ChildTasks#2](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_childtasks/vb/child1.vb#2)]  
  
 アタッチされた子タスクを使用すると、非同期操作の厳密に同期されたグラフを作成できます。  
  
 ただし、その親タスクが子タスクのアタッチを禁止していない場合にのみ、子タスクは親タスクにアタッチできます。  親タスクは、親タスクのクラスのコンストラクターの <xref:System.Threading.Tasks.TaskCreationOptions?displayProperty=fullName> オプションまたは <xref:System.Threading.Tasks.TaskFactory.StartNew%2A?displayProperty=fullName> メソッドで指定することで、明示的に子タスクが親タスクにアタッチできないようにすることができます。  親タスクが <xref:System.Threading.Tasks.Task.Run%2A?displayProperty=fullName> メソッドを呼び出して作成された場合、親タスクは暗黙的に子タスクをアタッチできないようにします。  次に例を示します。  親タスクが <xref:System.Threading.Tasks.TaskFactory.StartNew%28System.Action%29?displayProperty=fullName> メソッドではなく <xref:System.Threading.Tasks.Task.Run%28System.Action%29?displayProperty=fullName> メソッドを呼び出して作成される点を除き、これは前の例と同一です。  子タスクはその親にアタッチすることができないため、例からの出力は予測できません。  <xref:System.Threading.Tasks.Task.Run%2A?displayProperty=fullName> のオーバーロードにおける既定のタスクの作成オプションには <xref:System.Threading.Tasks.TaskCreationOptions?displayProperty=fullName> が含まれるため、この例は、「デタッチされた子タスク」セクションの最初の例と機能的に同等です。  
  
 [!code-csharp[TPL_ChildTasks#3](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_childtasks/cs/child1a.cs#3)]
 [!code-vb[TPL_ChildTasks#3](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_childtasks/vb/child1a.vb#3)]  
  
## 子タスクでの例外  
 デタッチされた子タスクが例外をスローする場合、その例外は入れ子でないタスクの場合と同様に監視するか、または親タスク内で直接処理する必要があります。  アタッチされた子タスクが例外をスローした場合、例外は自動的に親タスクに反映され、タスクの <xref:System.Threading.Tasks.Task%601.Result%2A?displayProperty=fullName> プロパティへのアクセスを待機するか、アクセスを試みるスレッドに戻されます。  したがって、アタッチされた子タスクを使用することで、呼び出し元のスレッドの <xref:System.Threading.Tasks.Task.Wait%2A?displayProperty=fullName> の呼び出しの 1 つの場所ですべての例外を処理できます。  詳細については、「[例外処理](../../../docs/standard/parallel-programming/exception-handling-task-parallel-library.md)」を参照してください。  
  
## キャンセルと子タスク  
 タスクの取り消し処理は他の処理と連携して行われます。  つまり、キャンセル可能であるためには、すべてのアタッチされた子タスク、またはデタッチされた子タスクが、キャンセル トークンの状態を監視する必要があります。  1 つのキャンセル要求を使用して親とその子をすべて取り消す場合は、同じトークンをすべてのタスクに引数として渡し、各タスクの要求に応答するためのロジックを各タスクに提供します。  詳細については、「[Task Cancellation](../../../docs/standard/parallel-programming/task-cancellation.md)」および「[How to: Cancel a Task and Its Children](../../../docs/standard/parallel-programming/how-to-cancel-a-task-and-its-children.md)」を参照してください。  
  
### 親が取り消された場合  
 子タスクが開始される前に親が取り消された場合、子は開始されません。  子タスクが既に開始された後に親が取り消された場合、子はそれ自体にキャンセル ロジックが適用されていない限り、完了まで実行されます。  詳細については、「[Task Cancellation](../../../docs/standard/parallel-programming/task-cancellation.md)」を参照してください。  
  
### デタッチされた子タスクが取り消された場合  
 デタッチされた子タスクが、そのタ親に渡されたのと同じトークンを使用して取り消された場合、親は子タスクを待機せず、例外も反映されません。例外は、他の処理と連携したキャセル処理として扱われるためです。  この動作は最上位のタスクと同じです。  
  
### アタッチされた子タスクが取り消された場合  
 アタッチされた子タスクが、その親タスクに渡されたのと同じトークンを使用して取り消された場合、<xref:System.Threading.Tasks.TaskCanceledException> が <xref:System.AggregateException> 内の連結されたスレッドに反映されます。  アタッチされた子タスクのグラフにまで反映されるすべてのエラーが発生している例外に加え、問題のないすべての例外も処理できるようにするため、親タスクを待機する必要があります。  
  
 詳細については、「[例外処理](../../../docs/standard/parallel-programming/exception-handling-task-parallel-library.md)」を参照してください。  
  
## 子タスクがその親にアタッチされないようにする  
 子タスクがスローした未処理の例外は親タスクに反映されます。  この動作を使うと、タスク ツリーを走査することなく、1 つのルート タスクのすべての子タスクの例外を確認することができます。  ただし、親タスクは他のコードからのアタッチを想定していない場合には、例外の反映は問題となる場合があります。  たとえば、<xref:System.Threading.Tasks.Task> オブジェクトのサードパーティ ライブラリのコンポーネントを呼び出すアプリケーションを考えてみます。  サードパーティのライブラリのコンポーネントが <xref:System.Threading.Tasks.Task> オブジェクトを作成し、親タスクにアタッチするように <xref:System.Threading.Tasks.TaskCreationOptions?displayProperty=fullName> を指定する場合は、子タスクで発生するハンドルされない例外はすべて親に反映されます。  これによりメイン アプリケーションで予期しない動作が発生することがあります。  
  
 子タスクが親タスクにアタッチされないようにするには、親の <xref:System.Threading.Tasks.TaskCreationOptions?displayProperty=fullName> または <xref:System.Threading.Tasks.Task> オブジェクトを作成するときに、<xref:System.Threading.Tasks.Task%601> オプションを指定します。  タスクがその親にアタッチしようとし、親が <xref:System.Threading.Tasks.TaskCreationOptions?displayProperty=fullName> オプションを指定する場合、子タスクは親にアタッチされず、<xref:System.Threading.Tasks.TaskCreationOptions?displayProperty=fullName> オプションが指定されなかったかのように実行されます。  
  
 子タスクが適時に完了しない場合には、子タスクがその親にアタッチしないようにすることをお勧めします。  親タスクは、すべての子タスクが終了するまで完了しないため、長時間実行される子タスクによって、アプリケーション全体のパフォーマンスの低下を生じる場合があります。  タスクがその親タスクにアタッチしないようにすることにより、アプリケーションのパフォーマンスを向上させる方法の例については、「[How to: Prevent a Child Task from Attaching to its Parent](../../../docs/standard/parallel-programming/how-to-prevent-a-child-task-from-attaching-to-its-parent.md)」を参照してください。  
  
## 参照  
 [Parallel Programming](../../../docs/standard/parallel-programming/index.md)   
 [Data Parallelism](../../../docs/standard/parallel-programming/data-parallelism-task-parallel-library.md)