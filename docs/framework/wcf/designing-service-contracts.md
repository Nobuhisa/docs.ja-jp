---
title: "サービス コントラクトの設計"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords: service contracts [WCF]
ms.assetid: 8e89cbb9-ac84-4f0d-85ef-0eb6be0022fd
caps.latest.revision: "34"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: 3204e4c280c6c1acd50062fa44b46344926c3908
ms.sourcegitcommit: ce279f2d7fe2220e6ea0a25a8a7a5370ddf8d9f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2017
---
# <a name="designing-service-contracts"></a>サービス コントラクトの設計
ここでは、サービス コントラクトの概要、定義方法、使用できる操作 (および基になるメッセージ交換の影響)、使用するデータ型、およびシナリオの要件を満たす操作を設計する際に役立つその他の問題について説明します。  
  
## <a name="creating-a-service-contract"></a>サービス コントラクトの作成  
 サービスは複数の操作を公開します。 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] アプリケーションでは、メソッドを作成し、<xref:System.ServiceModel.OperationContractAttribute> 属性でマークすることによって操作を定義します。 次に、サービス コントラクトを作成するために、<xref:System.ServiceModel.ServiceContractAttribute> 属性でマークされたインターフェイス内で操作を宣言するか、この属性でマークされたクラス内で操作を定義することにより、操作をグループ化します  (基本的な例では、次を参照してください[する方法: サービス コントラクトを定義する](../../../docs/framework/wcf/how-to-define-a-wcf-service-contract.md)。)。  
  
 <xref:System.ServiceModel.OperationContractAttribute> 属性を持たないメソッドはサービス操作ではないため、[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] サービスによって公開されることはありません。  
  
 ここでは、サービス コントラクトの設計時に決定すべき以下のポイントについて説明します。  
  
-   クラスとインターフェイスのどちらを使用するか  
  
-   交換するデータ型の指定方法  
  
-   使用できる交換パターンの種類  
  
-   コントラクトのセキュリティ要件の部分を明示的に作成できるかどうか  
  
-   操作の入力と出力の制限  
  
## <a name="classes-or-interfaces"></a>クラスとインターフェイス  
 クラスとインターフェイスは、いずれも機能のグループ化を表します。したがって、どちらを使用しても [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] サービス コントラクトを定義できます。 ただし、インターフェイスはサービス コントラクトを直接モデル化するため、インターフェイスを使用することをお勧めします。 実装のないインターフェイスは、特定のシグネチャを持つメソッドのグループ化を定義しているにすぎません。 サービス コントラクト インターフェイスを実装してはじめて、[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] サービスを実装したことになります。  
  
 サービス コントラクト インターフェイスには、次のようにマネージ インターフェイスのあらゆる利点がもたらされます。  
  
-   サービス コントラクト インターフェイスでは、他のサービス コントラクト インターフェイスをいくつでも拡張できます。  
  
-   これらのサービス コントラクト インターフェイスを実装することにより、1 つのクラスでサービス コントラクトをいくつでも実装できます。  
  
-   インターフェイスの実装を変更することにより、同じサービス コントラクトを引き続き使用したまま、そのコントラクトの実装を変更できます。  
  
-   以前のインターフェイスと新しいインターフェイスを実装することで、サービスをバージョン管理できます。 以前のクライアントは元のバージョンに接続し、新しいクライアントは新しいバージョンに接続できます。  
  
> [!NOTE]
>  他のサービス コントラクト インターフェイスから継承した場合、操作のプロパティ (名前や名前空間など) をオーバーライドすることはできません。 これを行う場合は、現在のサービス コントラクトに新しい操作を作成します。  
  
 [!INCLUDE[crexample](../../../includes/crexample-md.md)]インターフェイスを使用して、サービス コントラクトを作成するを参照してください[する方法: コントラクト インターフェイスでサービスを作成](../../../docs/framework/wcf/feature-details/how-to-create-a-service-with-a-contract-interface.md)です。  
  
 クラスを使用すると、サービス コントラクトの定義と実装を一度に行うことができます。 <xref:System.ServiceModel.ServiceContractAttribute> と <xref:System.ServiceModel.OperationContractAttribute> をそれぞれクラスとクラスのメソッドに直接適用してサービスを作成する方法には、サービスを迅速かつ簡単に作成できるという利点があります。 欠点は、マネージ クラスでは複数の継承をサポートしていないため、サービス コントラクトを一度に 1 つしか実装できないことです。 また、クラスまたはメソッド シグネチャに変更を加えると、そのサービスのパブリック コントラクトが変更されるため、変更されていないクライアントがサービスを使用できなくなることがあります。 [!INCLUDE[crdefault](../../../includes/crdefault-md.md)][サービス コントラクトを実装する](../../../docs/framework/wcf/implementing-service-contracts.md)です。  
  
 例については、クラスを使用して、サービス コントラクトを作成し、同時に実装する、次を参照してください。[する方法: コントラクト クラスでサービスを作成](../../../docs/framework/wcf/feature-details/how-to-create-a-wcf-contract-with-a-class.md)です。  
  
 これで、サービス コントラクトを定義する際に、インターフェイスを使用した場合とクラスを使用した場合の違いがわかりました。 次に、サービスとクライアント間で受け渡しできるデータを決定します。  
  
## <a name="parameters-and-return-values"></a>パラメーターと戻り値  
 各操作は戻り値とパラメーターを持ちます (戻り値とパラメーターが `void` の場合も含まれます)。 ただし、オブジェクトへの参照をオブジェクト間で渡すことができるローカル メソッドとは異なり、サービス操作ではオブジェクトへの参照を渡しません。 代わりに、オブジェクトのコピーを渡します。  
  
 これが重要なのは、パラメーターまたは戻り値で使用される各型がシリアル化可能でなければならないためです。つまり、その型のオブジェクトをバイト ストリームに変換でき、バイト ストリームからオブジェクトに変換できる必要があります。  
  
 プリミティブ型は既定でシリアル化可能であり、.NET Framework の多くの型も同様です。  
  
> [!NOTE]
>  操作シグネチャのパラメーター名の値はコントラクトに含まれ、大文字と小文字が区別されます。 ローカルでは同じパラメーター名を使用するが、公開されるメタデータでは名前を変更する場合は、<xref:System.ServiceModel.MessageParameterAttribute?displayProperty=nameWithType> を参照してください。  
  
#### <a name="data-contracts"></a>データ コントラクト  
 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] アプリケーションのようなサービス指向アプリケーションは、マイクロソフトとマイクロソフト以外の両方のプラットフォームで、できる限り多くのクライアント アプリケーションと相互運用できるように設計されています。 最大限の相互運用性を実現するために、使用する型を <xref:System.Runtime.Serialization.DataContractAttribute> 属性と <xref:System.Runtime.Serialization.DataMemberAttribute> 属性でマークして、データ コントラクトを作成することをお勧めします。データ コントラクトは、サービス コントラクトの一部であり、サービス操作で交換するデータを記述したものです。  
  
 データ コントラクトは opt-in 方式のコントラクトです。つまり、データ コントラクト属性を明示的に適用しない限り、型またはデータ メンバーはシリアル化されません。 データ コントラクトはマネージ コードのアクセス スコープとして関連付けられていません。プライベートのデータ メンバーはシリアル化され、パブリックにアクセスされる他の場所に送信されます  (データ コントラクトの基本的な例を参照してください[する方法: クラスまたは構造体に基本的なデータ コントラクトを作成する](../../../docs/framework/wcf/feature-details/how-to-create-a-basic-data-contract-for-a-class-or-structure.md)。)。[!INCLUDE[indigo2](../../../includes/indigo2-md.md)]操作の機能を有効にする基になる SOAP メッセージの定義だけでなく、シリアル化データの種類に出入りするメッセージの本文を処理します。 使用するデータ型がシリアル化可能であれば、操作の設計時に、基盤となるメッセージ交換インフラストラクチャについて考える必要はありません。  
  
 通常の [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] アプリケーションは <xref:System.Runtime.Serialization.DataContractAttribute> 属性および <xref:System.Runtime.Serialization.DataMemberAttribute> 属性を使用して操作のデータ コントラクトを作成しますが、他のシリアル化機構を使用することもできます。 <xref:System.Runtime.Serialization.ISerializable>、<xref:System.SerializableAttribute>、および <xref:System.Xml.Serialization.IXmlSerializable> の各標準機構はすべて、基になる SOAP メッセージへのデータ型のシリアル化を処理します。このメッセージはアプリケーション間でデータ型を伝達します。 使用するデータ型で特別なサポートが必要な場合は、さらに多くのシリアル化方法を使用できます。 [!INCLUDE[crabout](../../../includes/crabout-md.md)]内のデータ型のシリアル化の選択肢[!INCLUDE[indigo2](../../../includes/indigo2-md.md)]アプリケーションを参照してください[サービス コントラクトのデータ転送を指定する](../../../docs/framework/wcf/feature-details/specifying-data-transfer-in-service-contracts.md)です。  
  
#### <a name="mapping-parameters-and-return-values-to-message-exchanges"></a>メッセージ交換へのパラメーターと戻り値のマッピング  
 サービス操作は、特定の標準セキュリティ、トランザクション、およびセッション関連の機能をサポートするためにアプリケーションが必要とするデータに加え、アプリケーション データをやり取りする SOAP メッセージの基になる交換によってサポートされます。 これは大文字と小文字であるため、サービス操作のシグネチャは、基になるによって決まります*メッセージ交換パターン*(MEP)、データ転送と操作に必要な機能をサポートすることができます。 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] プログラミング モデルでは、要求/応答、一方向、および双方向の 3 つのメッセージ パターンを指定できます。  
  
##### <a name="requestreply"></a>要求/応答  
 要求/応答パターンでは、要求の送信側 (クライアント アプリケーション) は、その要求に関連付けられた応答を受信します。 このパターンでは、1 つの操作において、1 つ以上のパラメーターを操作に渡し、戻り値を呼び出し元に返すことができるため、このパターンが既定の MEP となります。 たとえば、次の C# コード例は、文字列を 1 つ受け取り、文字列を返す基本的なサービス操作を示しています。  
  
```csharp  
[OperationContractAttribute]  
string Hello(string greeting);  
```  
  
 次のコードは同等の Visual Basic コードです。  
  
```vb  
<OperationContractAttribute()>  
Function Hello (ByVal greeting As String) As String  
```  
  
 この操作シグネチャは、基になるメッセージ交換の形式を指定しています。 相関関係がない場合、[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] は戻り値の対象となる操作を特定できません。  
  
 別の基になるメッセージ パターンを指定しない限り、`void` (`Nothing` では [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]) を返すサービス操作も要求/応答メッセージ交換です。 クライアントが操作を非同期で呼び出していない場合、通常、メッセージが空の場合でも、戻りメッセージを受信するまでクライアントは処理を中止します。 クライアントが応答で空のメッセージを受信するまで制御が戻らない操作の C# コード例を次に示します。  
  
```csharp  
[OperationContractAttribute]  
void Hello(string greeting);  
```  
  
 次のコードは同等の Visual Basic コードです。  
  
```vb  
<OperationContractAttribute()>  
Sub Hello (ByVal greeting As String)  
```  
  
 上記の例では、実行に時間のかかる操作の場合に、クライアントのパフォーマンスと応答性が低下するおそれがありますが、要求/応答操作で `void` を返す場合でも、この操作には利点があります。 最も明らかな利点は、応答メッセージで SOAP エラーを返すことが可能であるということです。これにより、通信と処理のどちらで発生したかに関係なく、サービス関連の何らかのエラー状態が発生したことがわかります。 サービス コントラクトに指定された SOAP エラーは、<xref:System.ServiceModel.FaultException%601> オブジェクトとしてクライアント アプリケーションに渡されます。このオブジェクトの型パラメーターは、サービス コントラクトで指定された型です。 これにより、[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] サービスのエラー状態をクライアントに通知しやすくなります。 [!INCLUDE[crabout](../../../includes/crabout-md.md)]例外、SOAP エラー、およびエラー処理を参照してください。[を指定すると処理のエラー コントラクトおよびサービスの](../../../docs/framework/wcf/specifying-and-handling-faults-in-contracts-and-services.md)します。 要求/応答サービスとクライアントの例を参照してください[する方法: 要求/応答コントラクトを作成する](../../../docs/framework/wcf/feature-details/how-to-create-a-request-reply-contract.md)です。 [!INCLUDE[crabout](../../../includes/crabout-md.md)]要求/応答パターンで問題を参照してください[要求/応答サービス](../../../docs/framework/wcf/feature-details/request-reply-services.md)です。  
  
##### <a name="one-way"></a>一方向  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] サービス アプリケーションのクライアントが操作の完了まで待機する必要がなく、SOAP エラーも処理しない場合は、操作で一方向メッセージ パターンを指定できます。 一方向操作では、クライアントが操作を呼び出し、[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] がメッセージをネットワークに書き込んだら、クライアントは処理を続行できます。 通常、これは、送信メッセージで送信するデータが膨大な量でない限り、(データ送信時にエラーが発生しなければ) クライアントはほぼすぐに実行を続けることを意味します。 この種のメッセージ交換パターンでは、クライアントからサービス アプリケーションへのイベントのような動作をサポートします。  
  
 1 つのメッセージを送信し、何も受信しないメッセージ交換では、`void` 以外の戻り値を指定したサービス操作をサポートすることはできません。この場合、<xref:System.InvalidOperationException> 例外がスローされます。  
  
 戻りメッセージがないということは、処理または通信時のエラーを示すために SOAP エラーを返すこともできないということです  (操作が一方向操作の場合にエラー情報を伝達するには、双方向メッセージ交換パターンが必要です)。  
  
 `void` を返す操作で一方向メッセージ交換を指定するには、次の C# コード例に示すように、<xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> プロパティを `true` に設定します。  
  
```csharp  
[OperationContractAttribute(IsOneWay=true)]  
void Hello(string greeting);  
```  
  
 次のコードは同等の Visual Basic コードです。  
  
```vb  
<OperationContractAttribute(IsOneWay := True)>  
Sub Hello (ByVal greeting As String)  
```  
  
 このメソッドは、前述の要求/応答の例と同じです。ただし、<xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> プロパティを `true` に設定するということは、メソッドは同じでも、サービス操作は戻りメッセージを送信せず、送信メッセージがチャネル レイヤーに渡されると、すぐにクライアントに制御が戻ることを意味します。 例については、次を参照してください。[する方法: 一方向コントラクトを作成する](../../../docs/framework/wcf/feature-details/how-to-create-a-one-way-contract.md)です。 [!INCLUDE[crabout](../../../includes/crabout-md.md)]一方向のパターンを参照してください[一方向サービス](../../../docs/framework/wcf/feature-details/one-way-services.md)です。  
  
##### <a name="duplex"></a>二重  
 双方向パターンの特徴は、一方向メッセージングと要求/応答メッセージングのどちらを使用しているかに関係なく、サービスとクライアントが共に独立して、相互にメッセージを送信できるという点です。 二方向通信のこの形式は、サービスがクライアントと直接通信する必要がある場合や、イベントのような動作など、メッセージを交換するどちらの側も非同期で動作できるようにする場合に役立ちます。  
  
 双方向パターンでは、クライアントと通信するための機構が別途必要になるため、要求/応答パターンや一方向パターンに比べると若干複雑になります。  
  
 双方向コントラクトを設計する場合、コールバック コントラクトも設計し、そのコールバック コントラクトの型を、サービス コントラクトをマークする <xref:System.ServiceModel.ServiceContractAttribute.CallbackContract%2A> 属性の <xref:System.ServiceModel.ServiceContractAttribute> プロパティに割り当てる必要があります。  
  
 双方向パターンを実装するには、クライアントで呼び出されるメソッド宣言を含む 2 つ目のインターフェイスを作成する必要があります。  
  
 [!INCLUDE[crexample](../../../includes/crexample-md.md)]サービス、およびそのサービスにアクセスするクライアントを作成するを参照してください[する方法: 双方向コントラクトを作成する](../../../docs/framework/wcf/feature-details/how-to-create-a-duplex-contract.md)と[する方法: 双方向コントラクトでサービスをアクセス](../../../docs/framework/wcf/feature-details/how-to-access-services-with-a-duplex-contract.md)です。 作業用サンプルについては、次を参照してください。[双方向](../../../docs/framework/wcf/samples/duplex.md)です。 [!INCLUDE[crabout](../../../includes/crabout-md.md)]二重のコントラクトを使用して、問題を参照してください[双方向サービス](../../../docs/framework/wcf/feature-details/duplex-services.md)です。  
  
> [!CAUTION]
>  サービスは、双方向メッセージを受信すると、その受信メッセージの `ReplyTo` 要素を参照して応答の送信先を決定します。 メッセージの受信に使用するチャネルがセキュリティで保護されていない場合、信頼関係のないクライアントが対象コンピューターの `ReplyTo` を使用して悪意のあるメッセージを送信し、その対象コンピューターのサービス拒否 (DOS: Denial Of Service) を引き起こすおそれがあります。  
  
##### <a name="out-and-ref-parameters"></a>Out パラメーターと Ref パラメーター  
 ほとんどの場合、`in` パラメーター (`ByVal` では [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]) および `out` パラメーターと `ref` パラメーター (`ByRef` では [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]) を使用できます。 `out` パラメーターと `ref` パラメーターは、操作からデータが返されることを示すため、操作シグネチャが `void` を返す場合でも、次のような操作シグネチャによって要求/応答操作が必要であることを指定します。  
  
```csharp  
[ServiceContractAttribute]  
public interface IMyContract  
{  
  [OperationContractAttribute]  
  public void PopulateData(ref CustomDataType data);  
}  
```  
  
 次のコードは同等の Visual Basic コードです。  
  
```vb  
<ServiceContractAttribute()> _  
Public Interface IMyContract  
  <OperationContractAttribute()> _  
  Public Sub PopulateData(ByRef data As CustomDataType)  
End Interface  
```  
  
 唯一の例外は、シグネチャに特定の構造体が含まれている場合です。 たとえば、<xref:System.ServiceModel.NetMsmqBinding> バインディングを使用してクライアントと通信できるのは、操作の宣言に使用されたメソッドが `void` を返す場合だけです。戻り値、`ref` パラメーター、または `out` パラメーターのいずれであるかに関係なく、出力値を指定することはできません。  
  
 また、`out` パラメーターまたは `ref` パラメーターを使用する場合、操作には基になる応答メッセージが必要です。このメッセージが変更されたオブジェクトを返します。 操作が一方向操作の場合、実行時に <xref:System.InvalidOperationException> 例外がスローされます。  
  
### <a name="specify-message-protection-level-on-the-contract"></a>コントラクトでのメッセージ保護レベルの指定  
 コントラクトの設計時に、コントラクトを実装するサービスのメッセージ保護レベルも決定する必要があります。 これは、メッセージ セキュリティをコントラクトのエンドポイントのバインディングに適用する場合にのみ必要です。 バインディングのセキュリティが無効になっている場合 (つまり、システム指定のバインディングで <xref:System.ServiceModel.SecurityMode?displayProperty=nameWithType> の値が <xref:System.ServiceModel.SecurityMode.None?displayProperty=nameWithType> に設定されている場合)、コントラクトのメッセージ保護レベルを決定する必要はありません。 ほとんどの場合、メッセージ レベルのセキュリティが適用されたシステム指定のバインディングは、十分な保護レベルを備えているため、操作ごとまたはメッセージごとに保護レベルを検討する必要はありません。  
  
 保護レベルは、サービスをサポートするメッセージ (またはメッセージ部分) が署名されるのか、署名および暗号化されるのか、または署名と暗号化なしで送信されるのかを指定する値です。 保護レベルは、さまざまなスコープ (サービス レベル、特定の操作、その操作内のメッセージ、またはメッセージ部分) で設定できます。 あるスコープで設定された値は、明示的にオーバーライドしない限り、そのスコープよりも小さなスコープの既定値になります。 コントラクトに必要とされる最小限の保護レベルをバインディング構成で提供できない場合は、例外がスローされます。 保護レベルの値がコントラクトで明示的に設定されていない場合、バインディングのメッセージ セキュリティが有効であれば、バインディング構成によってすべてのメッセージの保護レベルが制御されます。 これが既定の動作です。  
  
> [!IMPORTANT]
>  一般に、コントラクトのさまざまなスコープを完全な保護レベルである <xref:System.Net.Security.ProtectionLevel.EncryptAndSign?displayProperty=nameWithType> よりも下のレベルに明示的に設定するかどうかは、パフォーマンスの向上と引き換えに、ある程度のセキュリティで妥協できるかどうかという判断によって決まります。 このような場合、操作および操作で交換するデータの価値に焦点を絞って判断を下す必要があります。 [!INCLUDE[crdefault](../../../includes/crdefault-md.md)][Services のセキュリティ保護](../../../docs/framework/wcf/securing-services.md)です。  
  
 たとえば、次のコード例では、<xref:System.ServiceModel.ServiceContractAttribute.ProtectionLevel%2A> も、コントラクトの <xref:System.ServiceModel.OperationContractAttribute.ProtectionLevel%2A> プロパティも設定していません。  
  
```csharp  
[ServiceContract]  
public interface ISampleService  
{  
  [OperationContractAttribute]  
  public string GetString();  
  
  [OperationContractAttribute]  
  public int GetInt();    
}  
```  
  
 次のコードは同等の Visual Basic コードです。  
  
```vb  
<ServiceContractAttribute()> _  
Public Interface ISampleService  
  
  <OperationContractAttribute()> _  
  Public Function GetString()As String  
  
  <OperationContractAttribute()> _  
  Public Function GetData() As Integer  
  
End Interface  
```  
  
 既定の `ISampleService` (既定の <xref:System.ServiceModel.WSHttpBinding> は <xref:System.ServiceModel.SecurityMode?displayProperty=nameWithType>) を使用するエンドポイントの <xref:System.ServiceModel.SecurityMode.Message> 実装とやり取りする場合は、暗号化と署名が既定の保護レベルであるため、すべてのメッセージが暗号化および署名されます。 ただし、既定の `ISampleService` (既定の <xref:System.ServiceModel.BasicHttpBinding> は <xref:System.ServiceModel.SecurityMode>) を使用して <xref:System.ServiceModel.SecurityMode.None> サービスを使用すると、すべてのメッセージがテキストとして送信されます。これは、このバインディングにはセキュリティがないため、保護レベルが無視されるためです (つまり、メッセージの暗号化も署名も行われません)。 <xref:System.ServiceModel.SecurityMode> を <xref:System.ServiceModel.SecurityMode.Message> に変更すると、これがこのバインディングの既定の保護レベルになるため、これらのメッセージは暗号化および署名されるようになります。  
  
 コントラクトの保護要件を明示的に指定または調整する場合は、<xref:System.ServiceModel.ServiceContractAttribute.ProtectionLevel%2A> プロパティ (またはより小さなスコープの `ProtectionLevel` プロパティのいずれか) をサービス コントラクトに必要なレベルに設定します。 この場合、明示的な設定を使用するには、使用するスコープに少なくともその設定をサポートするバインディングが必要です。 たとえば、次のコード例では、<xref:System.ServiceModel.OperationContractAttribute.ProtectionLevel%2A> 操作の `GetGuid` の値を明示的に指定しています。  
  
```csharp  
[ServiceContract]  
public interface IExplicitProtectionLevelSampleService  
{  
  [OperationContractAttribute]  
  public string GetString();  
  
  [OperationContractAttribute(ProtectionLevel=ProtectionLevel.None)]  
  public int GetInt();    
  [OperationContractAttribute(ProtectionLevel=ProtectionLevel.EncryptAndSign)]  
  public int GetGuid();    
}  
```  
  
 次のコードは同等の Visual Basic コードです。  
  
```vb  
<ServiceContract()> _   
Public Interface IExplicitProtectionLevelSampleService   
    <OperationContract()> _   
    Public Function GetString() As String   
    End Function   
  
    <OperationContract(ProtectionLevel := ProtectionLevel.None)> _   
    Public Function GetInt() As Integer   
    End Function   
  
    <OperationContractAttribute(ProtectionLevel := ProtectionLevel.EncryptAndSign)> _   
    Public Function GetGuid() As Integer   
    End Function   
  
End Interface  
```  
  
 この `IExplicitProtectionLevelSampleService` コントラクトを実装し、既定の <xref:System.ServiceModel.WSHttpBinding> (既定の <xref:System.ServiceModel.SecurityMode?displayProperty=nameWithType> は <xref:System.ServiceModel.SecurityMode.Message>) を使用するエンドポイントを持つサービスの動作は次のようになります。  
  
-   `GetString` 操作のメッセージは、暗号化および署名されます。  
  
-   `GetInt` 操作のメッセージは、暗号化も署名もされない (プレーン) テキストとして送信されます。  
  
-   `GetGuid` 操作の <xref:System.Guid?displayProperty=nameWithType> は、暗号化および署名されたメッセージで返されます。  
  
 [!INCLUDE[crabout](../../../includes/crabout-md.md)]保護レベルと、その使用方法を参照してください。[について保護レベル](../../../docs/framework/wcf/understanding-protection-level.md)です。 [!INCLUDE[crabout](../../../includes/crabout-md.md)]セキュリティを参照してください[Services のセキュリティ保護](../../../docs/framework/wcf/securing-services.md)です。  
  
##### <a name="other-operation-signature-requirements"></a>操作シグネチャのその他の要件  
 アプリケーションの一部の機能では、特定の種類の操作シグネチャを必要とします。 たとえば、<xref:System.ServiceModel.NetMsmqBinding> バインディングは、永続的なサービスとクライアントをサポートします。永続的なサービスとクライアントでは、通信の途中でアプリケーションを再起動し、メッセージを失うことなく、アプリケーションが中止された場所を検出できます  ([!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [WCF のキュー](../../../docs/framework/wcf/feature-details/queues-in-wcf.md))。ただし、永続的操作では、`in` パラメーターを 1 つしか受け取ることができず、戻り値を持つこともできません。  
  
 もう 1 つの例として、操作における <xref:System.IO.Stream> 型の使用が挙げられます。 <xref:System.IO.Stream> パラメーターにはメッセージの本文全体が含まれるため、入力または出力 (つまり、`ref` パラメーター、`out` パラメーター、または戻り値) が <xref:System.IO.Stream> 型である場合、操作で指定された入力または出力に限定する必要があります。 また、パラメーターまたは戻り値の型は <xref:System.IO.Stream>、<xref:System.ServiceModel.Channels.Message?displayProperty=nameWithType>、<xref:System.Xml.Serialization.IXmlSerializable?displayProperty=nameWithType> のいずれかである必要があります。 [!INCLUDE[crabout](../../../includes/crabout-md.md)]ストリームを参照してください[大量のデータとストリーミング](../../../docs/framework/wcf/feature-details/large-data-and-streaming.md)です。  
  
##### <a name="names-namespaces-and-obfuscation"></a>名前、名前空間、および難読化  
 コントラクトおよび操作の定義内の .NET 型の名前や名前空間は、コントラクトが WSDL に変換されるとき、およびコントラクト メッセージが作成および送信されるときに重要になります。 したがって、サービス コントラクトの名前と名前空間は、`Name`、`Namespace`、<xref:System.ServiceModel.ServiceContractAttribute>、<xref:System.ServiceModel.OperationContractAttribute> などの、すべてのサポート対象コントラクト属性や、他のコントラクト属性の <xref:System.Runtime.Serialization.DataContractAttribute> プロパティと <xref:System.Runtime.Serialization.DataMemberAttribute> プロパティを使用して明示的に設定することを強くお勧めします。  
  
 この 1 つの結果として、名前と名前空間が明示的に設定されていない場合、アセンブリで IL 隠ぺいを使用すると、コントラクトの型名と名前空間が変更され、その結果、WSDL が変更され、通常はネットワークでのメッセージ交換に失敗します。 コントラクトの名前と名前空間を明示的に設定せずに隠ぺいを使用する場合は、<xref:System.Reflection.ObfuscationAttribute> 属性と <xref:System.Reflection.ObfuscateAssemblyAttribute> 属性を使用して、コントラクトの型名と名前空間が変更されないようにします。  
  
## <a name="see-also"></a>関連項目  
 [方法: 要求/応答コントラクトを作成します。](../../../docs/framework/wcf/feature-details/how-to-create-a-request-reply-contract.md)  
 [方法: 一方向コントラクトを作成します。](../../../docs/framework/wcf/feature-details/how-to-create-a-one-way-contract.md)  
 [方法: 双方向コントラクトを作成します。](../../../docs/framework/wcf/feature-details/how-to-create-a-duplex-contract.md)  
 [サービス コントラクトで指定するデータを転送します。](../../../docs/framework/wcf/feature-details/specifying-data-transfer-in-service-contracts.md)  
 [コントラクトおよびサービスのエラーの指定と処理](../../../docs/framework/wcf/specifying-and-handling-faults-in-contracts-and-services.md)  
 [セッションの使用](../../../docs/framework/wcf/using-sessions.md)  
 [同期操作と非同期操作](../../../docs/framework/wcf/synchronous-and-asynchronous-operations.md)  
 [信頼できるサービス](../../../docs/framework/wcf/reliable-services.md)  
 [サービスとトランザクション](../../../docs/framework/wcf/services-and-transactions.md)
