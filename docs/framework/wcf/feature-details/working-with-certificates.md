---
title: "証明書の使用"
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
helpviewer_keywords: certificates [WCF]
ms.assetid: 6ffb8682-8f07-4a45-afbb-8d2487e9dbc3
caps.latest.revision: "26"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: 63f9d22c571a007653fc794dc7638c8221a676aa
ms.sourcegitcommit: ce279f2d7fe2220e6ea0a25a8a7a5370ddf8d9f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2017
---
# <a name="working-with-certificates"></a>証明書の使用
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] のセキュリティをプログラミングする場合、一般に X.509 デジタル証明書を使用して、クライアントとサーバーの認証、暗号化、およびメッセージのデジタル署名を行います。 ここでは、X.509 デジタル証明書の機能および [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] でのそれらの機能の使用方法について簡単に説明します。また、これらの概念の詳細を説明するトピックや、[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] と証明書を使用した一般的なタスクの実行方法が記載されたトピックへのリンクも示します。  
  
 デジタル証明書の一部である、簡単に言えば、*公開キー基盤*(PKI)、これは、デジタル証明書、証明書機関、およびその他の検証し、認証の有効性を登録機関のシステム公開キーの暗号化を使用して、電子取引に関与する各当事者です。 証明機関が証明書を発行し、各証明書など、データを含んでいるフィールドのセットがあります*サブジェクト*(証明書の発行先であるエンティティ) 有効期間 (ときに、証明書が有効)、(、発行者エンティティ証明書を発行する) と公開キー。 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] では、これらの各プロパティは <xref:System.IdentityModel.Claims.Claim> (クレーム) として処理されます。各クレームは、さらに ID と権限の 2 種類に分けられます。 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]X.509 証明書を参照してください[X.509 公開キー証明書](http://go.microsoft.com/fwlink/?LinkId=209952)[!INCLUDE[crabout](../../../../includes/crabout-md.md)]クレームと WCF での承認を参照してください。[管理クレームと Id モデル承認](../../../../docs/framework/wcf/feature-details/managing-claims-and-authorization-with-the-identity-model.md)です。 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]参照してください、PKI を実装する[Windows Server 2008 R2 の証明書サービス](http://go.microsoft.com/fwlink/?LinkId=209949)です。  
  
 証明書の第一の機能は、他者に対して証明書の所有者の ID を認証することです。 証明書が含まれています、*公開キー*の所有者、所有者、秘密キーを保持するときにします。 公開キーを使用して、証明書の所有者に送信されるメッセージを暗号化できます。 秘密キーにアクセスできるのは所有者だけであるため、所有者だけが暗号化されたメッセージを復号化できます。  
  
 証明書は、証明機関によって発行される必要があります。多くの場合、証明機関はサードパーティの証明書発行者です。 Windows ドメインでは、そのドメインのコンピューターに対して証明書を発行する際に使用できる証明機関が含まれています。  
  
## <a name="viewing-certificates"></a>証明書の表示  
 証明書を使用するには、多くの場合、証明書を表示し、プロパティを確認する必要があります。 Microsoft 管理コンソール (MMC: Microsoft Management Console) スナップイン ツールを使用すると、これを簡単に行うことができます。 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][する方法: MMC スナップインで証明書を表示](../../../../docs/framework/wcf/feature-details/how-to-view-certificates-with-the-mmc-snap-in.md)です。  
  
## <a name="certificate-stores"></a>証明書ストア  
 証明書はストアに格納されています。 2 つの主要なストアがあり、さらにサブストアに分かれています。 コンピューターの管理者は、MMC スナップイン ツールを使用して、両方の主要なストアを表示できます。 管理者以外のユーザーは、現在のユーザー ストアだけを表示できます。  
  
-   **ローカル コンピューター ストア**です。 このストアには、コンピューター プロセス ([!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] など) がアクセスする証明書が格納されます。 クライアントに対してサーバーを認証するための証明書は、ここに格納します。  
  
-   **現在のユーザー ストア**です。 コンピューターの現在のユーザーの証明書は、通常、対話型アプリケーションによってここに配置されます。 クライアント アプリケーションを作成する場合、サービスに対してユーザーを認証するための証明書は、通常、ここに配置します。  
  
 上記の 2 つのストアは、さらにサブストアに分かれています。 サブストアの中で、[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] でプログラミングするときに最も重要なものは次のとおりです。  
  
-   **信頼されたルート証明機関**です。 このストア内の証明書を使用して、証明書チェーンを作成できます。証明書チェーンをさかのぼることで、このストア内の任意の証明機関証明書に到達できます。  
  
    > [!IMPORTANT]
    >  証明書が信頼されたサードパーティ証明機関から発行されたものではない場合でも、ローカル コンピューターは、このストアに配置された証明書を暗黙で信頼します。 したがって、発行者を完全に信頼し、かつ信頼することの結果を理解していない限り、このストアに証明書を配置しないでください。  
  
-   **個人用**です。 このストアは、コンピューターのユーザーに関連付けられた証明書に使用されます。 通常、このストアは、信頼されたルート証明機関ストアにある証明機関証明書のいずれかによって発行された証明書に使用されます。 また、自己発行され、アプリケーションから信頼された証明書が格納されている場合もあります。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]証明書のストアは、「[証明書ストア](http://go.microsoft.com/fwlink/?LinkId=88912)です。  
  
### <a name="selecting-a-store"></a>ストアの選択  
 証明書を格納する場所の選択は、サービスまたはクライアントの実行方法や実行する状況によって異なります。 次の一般規則が適用されます。  
  
-   Windows サービスの使用中で、WCF サービスがホストされている場合、**ローカル マシン**を格納します。 ローカル コンピューター ストアに証明書をインストールするには、管理特権が必要です。  
  
-   サービスまたはクライアントがアプリケーション ユーザー アカウントで実行される場合を使用して、**現在のユーザー**を格納します。  
  
### <a name="accessing-stores"></a>ストアへのアクセス  
 ストアは、コンピューター上の一種のフォルダーであり、アクセス制御リスト (ACL: Access Control List) によって保護されています。 インターネット インフォメーション サービス (IIS: Internet Information Services) によってホストされたサービスを作成すると、[!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] アカウントで [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] プロセスが実行されます。 このアカウントは、サービスが使用する証明書を格納するストアにアクセス可能である必要があります。 各主要ストアは既定のアクセス リストで保護されていますが、これらのリストは変更できます。 ストアにアクセスする別のロールを作成した場合、そのロールにアクセス許可を付与する必要があります。 WinHttpCertConfig.exe ツールを使用してアクセス リストを変更する方法については、次を参照してください。[する方法: 開発中に使用する一時的な証明書を作成](../../../../docs/framework/wcf/feature-details/how-to-create-temporary-certificates-for-use-during-development.md)です。 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]IIS クライアント証明書を使用して、参照してください[を ASP.NET Web アプリケーションでは認証にクライアント証明書を使用して、Web サービスを呼び出す方法](http://go.microsoft.com/fwlink/?LinkId=88914)です。  
  
## <a name="chain-trust-and-certificate-authorities"></a>信頼チェーンと証明機関  
 証明書は、各証明書がその発行元の CA にリンクされる階層構造で作成されます。 このリンクは CA の証明書へのリンクになります。 次に、CA の証明書は元の CA の証明書を発行した CA にリンクします。 ルート CA の証明書に到達するまでこのプロセスが繰り返されます。 ルート CA の証明書は本質的に信頼されています。  
  
 デジタル証明書が証明書利用者のとも呼ばれる、この階層でエンティティを認証に使用されます、*の信頼チェーン*です。 証明書をダブルクリックしをクリックすると、MMC スナップインを使用して証明書のチェーンを表示する、**証明書パス**タブ[!INCLUDE[crabout](../../../../includes/crabout-md.md)]証明機関の証明書チェーンをインポートするを参照してください[する方法: 署名の検証に使用される証明書機関の証明書チェーンを指定する](../../../../docs/framework/wcf/feature-details/specify-the-certificate-authority-chain-verify-signatures-wcf.md)です。  
  
> [!NOTE]
>  証明書を "信頼されたルート証明機関" 証明書ストアに配置することにより、その証明書の発行者を信頼されたルート証明機関として指定できます。  
  
### <a name="disabling-chain-trust"></a>信頼チェーンの無効化  
 新しいサービスの作成時には、信頼されたルート証明書によって発行されていない証明書を使用できます。また、発行する証明書が、信頼されたルート証明機関ストアになくてもかまいません。 開発だけを目的としている場合は、証明書の信頼チェーンをチェックする機構を一時的に無効にできます。 これを行うには、`CertificateValidationMode` プロパティを `PeerTrust` または `PeerOrChainTrust` に設定します。 これらのモードにより、証明書を自己発行するか (ピア信頼)、信頼チェーンに含めるかを指定できます。 このプロパティは、次のどのクラスでも設定できます。  
  
|クラス|プロパティ|  
|-----------|--------------|  
|<xref:System.ServiceModel.Security.X509ClientCertificateAuthentication>|<xref:System.ServiceModel.Security.X509ClientCertificateAuthentication.CertificateValidationMode%2A?displayProperty=nameWithType>|  
|<xref:System.ServiceModel.Security.X509PeerCertificateAuthentication>|<xref:System.ServiceModel.Security.X509PeerCertificateAuthentication.CertificateValidationMode%2A?displayProperty=nameWithType>|  
|<xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication>|<xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication.CertificateValidationMode%2A?displayProperty=nameWithType>|  
|<xref:System.ServiceModel.Security.IssuedTokenServiceCredential>|<xref:System.ServiceModel.Security.IssuedTokenServiceCredential.CertificateValidationMode%2A?displayProperty=nameWithType>|  
  
 構成を使用して、このプロパティを設定することもできます。 検証モードを指定するには、次の要素を使用します。  
  
-   [\<認証 >](../../../../docs/framework/configure-apps/file-schema/wcf/authentication-of-servicecertificate-element.md)  
  
-   [\<peerAuthentication >](../../../../docs/framework/configure-apps/file-schema/wcf/peerauthentication-element.md)  
  
-   [\<messageSenderAuthentication >](../../../../docs/framework/configure-apps/file-schema/wcf/messagesenderauthentication-element.md)  
  
## <a name="custom-authentication"></a>カスタム認証  
 `CertificateValidationMode` プロパティを使用すると、証明書の認証方法をカスタマイズすることもできます。 既定では、レベルは `ChainTrust` に設定されています。 <xref:System.ServiceModel.Security.X509CertificateValidationMode.Custom> 値を使用するには、`CustomCertificateValidatorType` 属性を証明書の検証に使用するアセンブリと型に設定することも必要です。 カスタム検証を作成するには、抽象 <xref:System.IdentityModel.Selectors.X509CertificateValidator> クラスから継承する必要があります。  
  
 カスタム認証システムを作成する場合、オーバーライドする最も重要なメソッドは <xref:System.IdentityModel.Selectors.X509CertificateValidator.Validate%2A> メソッドです。 カスタム認証の例は、次を参照してください。、 [X.509 証明書検証](../../../../docs/framework/wcf/samples/x-509-certificate-validator.md)サンプルです。 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][カスタム資格情報と資格情報の検証](../../../../docs/framework/wcf/extending/custom-credential-and-credential-validation.md)です。  
  
## <a name="using-makecertexe-to-build-a-certificate-chain"></a>Makecert.exe を使用した証明書チェーンの構築  
 証明書作成ツール (Makecert.exe) では、X.509 証明書および秘密キーと公開キーのペアを作成します。 秘密キーをディスクに保存し、新しい証明書の発行と署名に使用できるため、チェーンになった証明書の階層をシミュレートできます。 このツールは、サービスの開発時に支援ツールとして使用することだけを目的としています。実際の展開に使用する証明書の作成には使用しないでください。 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] サービスの開発時に、Makecert.exe を使用して信頼チェーンを構築するには、次の手順に従います。  
  
#### <a name="to-build-a-chain-of-trust-with-makecertexe"></a>Makecert.exe を使用して証明書チェーンを構築するには  
  
1.  MakeCert.exe ツールを使用して、(自己発行された) 一時的なルート証明機関証明書を作成します。 秘密キーをディスクに保存します。  
  
2.  この新しい証明書を使用して、公開キーを含む別の証明書を発行します。  
  
3.  信頼されたルート証明機関ストアに、ルート証明機関証明書をインポートします。  
  
4.  手順については、次を参照してください。[する方法: 開発中に使用する一時的な証明書を作成](../../../../docs/framework/wcf/feature-details/how-to-create-temporary-certificates-for-use-during-development.md)です。  
  
## <a name="which-certificate-to-use"></a>使用する証明書の選択  
 証明書に関する一般的な質問は、どの証明書を使用するかということとその理由に関するものです。 その答えは、クライアントとサービスのどちらをプログラミングするかによって異なります。 以下に一般的なガイドラインを示します (これらの質問に対する包括的な答えではありません)。  
  
### <a name="service-certificates"></a>サービス証明書  
 サービス証明書の第一のタスクは、クライアントに対してサーバーを認証することです。 クライアントがサーバーを認証する場合は、初期チェックの 1 つの値を比較するが、**サブジェクト**フィールドに、Uniform Resource Identifier ()、サービスに接続するために使用: 両方の DNS が一致する必要があります。 たとえば、サービスの URI が"http://www.contoso.com/endpoint/"の場合、**サブジェクト**フィールドには、値"www.contoso.com"が含まれてもする必要があります。  
  
 このフィールドには複数の値を含めることができますが、各値の先頭にはその値を示す初期化コードが付加されます。 通常、初期化コードは共通名 (Common Name) を表す "CN" です。たとえば、"CN = www.contoso.com" のようになります。 ことも、**サブジェクト**いる場合は、空白にするフィールド、**サブジェクトの別名**フィールドを含めることができます、 **DNS 名**値。  
  
 値にも注意してください、 **Intended Purposes**証明書のフィールドは、「サーバー認証」や「クライアント認証」などの適切な値を含める必要があります。  
  
### <a name="client-certificates"></a>クライアント証明書  
 通常、クライアント証明書はサードパーティ証明機関によって発行されません。 通常は、"クライアント認証" という目的で、ルート証明機関によって、この証明書が現在のユーザー ストアの個人ストアに配置されます。 クライアントは、相互認証が必要なときにこのような証明書を使用できます。  
  
## <a name="online-revocation-and-offline-revocation"></a>オンラインの失効とオフラインの失効  
  
### <a name="certificate-validity"></a>証明書の有効期間  
 すべての証明書の有効期間はだけ一定の時間と呼ばれる、*有効期間*です。 有効期間がによって定義された、 **Valid from**と**有効期間の終了**X.509 証明書のフィールドです。 認証時に、証明書がまだ有効期間内かどうかを確認するためのチェックが行われます。  
  
### <a name="certificate-revocation-list"></a>証明書失効リスト  
 有効期間中であっても、証明機関が証明書を失効させる場合があります。 これは、証明書の秘密キーの侵害など、さまざまな理由によって行われます。  
  
 証明書が失効した場合、失効した証明書から発生した下位のチェーンも無効になり、認証手順において信頼されなくなります。 どの証明書の失効については、各発行者が発行、および日時のタイムスタンプ*証明書失効リスト*(CRL)。 このリストは、オンラインの失効またはオフラインの失効を使用してチェックできます。これを使用するには、`RevocationMode`、`DefaultRevocationMode`、<xref:System.Security.Cryptography.X509Certificates.X509RevocationMode>、および <xref:System.ServiceModel.Security.X509ClientCertificateAuthentication> の各クラスの <xref:System.ServiceModel.Security.X509PeerCertificateAuthentication> プロパティまたは <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication> プロパティを <xref:System.ServiceModel.Security.IssuedTokenServiceCredential> 列挙値のいずれかに設定します。 すべてのプロパティの既定値は、`Online` です。  
  
 使用して構成でモードを設定することも、`revocationMode`両方の属性、 [\<認証 >](../../../../docs/framework/configure-apps/file-schema/wcf/authentication-of-clientcertificate-element.md) (の[ \<serviceBehaviors >](../../../../docs/framework/configure-apps/file-schema/wcf/servicebehaviors.md)) と、 [\<認証 >](../../../../docs/framework/configure-apps/file-schema/wcf/authentication-of-clientcertificate-element.md) (の[ \<endpointBehaviors >](../../../../docs/framework/configure-apps/file-schema/wcf/endpointbehaviors.md))。  
  
## <a name="the-setcertificate-method"></a>SetCertificate メソッド  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] では、認証、暗号化、またはメッセージのデジタル署名を行うために、多くの場合、サービスまたはクライアントが使用する証明書または証明書のセットを指定する必要があります。 これは、X.509 証明書を表すさまざまなクラスの `SetCertificate` メソッドを使用することで、プログラムによって実行できます。 `SetCertificate` メソッドを使用して証明書を指定するクラスは次のとおりです。  
  
|クラス|メソッド|  
|-----------|------------|  
|<xref:System.ServiceModel.Security.PeerCredential>|<xref:System.ServiceModel.Security.PeerCredential.SetCertificate%2A>|  
|<xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential>|<xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential.SetCertificate%2A>|  
|<xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential>|<xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential.SetCertificate%2A>|  
|<xref:System.ServiceModel.Security.X509CertificateInitiatorServiceCredential>|  
|<xref:System.ServiceModel.Security.X509CertificateInitiatorServiceCredential.SetCertificate%2A>|  
  
 `SetCertificate` メソッドを使用するには、ストアの場所とストア、証明書のフィールドを指定する "検索" の種類 (`x509FindType` パラメーター)、および該当のフィールドで検索する値を指定します。 たとえば、次のコードを作成、<xref:System.ServiceModel.ServiceHost>インスタンスおよびクライアントに対するサービスの認証に使用されるサービス証明書を設定、`SetCertificate`メソッドです。  
  
 [!code-csharp[c_WorkingWithCertificates#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_workingwithcertificates/cs/source.cs#1)]
 [!code-vb[c_WorkingWithCertificates#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_workingwithcertificates/vb/source.vb#1)]  
  
### <a name="multiple-certificates-with-the-same-value"></a>同じ値が含まれた複数の証明書  
 ストアには、同じサブジェクト名が含まれた複数の証明書が格納されていることがあります。 つまり、設定した場合、`x509FindType`は<xref:System.Security.Cryptography.X509Certificates.X509FindType.FindBySubjectName>または<xref:System.Security.Cryptography.X509Certificates.X509FindType.FindBySubjectDistinguishedName>、もう 1 つ以上の証明書が同じ値を持つ、becausethereisno 方法には、どの証明書が必要なを区別するために、例外がスローされます。 この状況は、`x509FindType` を <xref:System.Security.Cryptography.X509Certificates.X509FindType.FindByThumbprint> に設定することによってある程度防ぐことができます。 拇印フィールドには一意の値が含まれるため、このフィールドを使用することで、ストア内の特定の証明書を検索できます。 ただし、この方法には欠点があります。証明書が失効したり、更新されたりした場合、拇印も失われてしまうため、`SetCertificate` メソッドは失敗します。 また、証明書が有効でなくなると、認証が失敗します。 このような状況が発生する可能性を軽減する方法として、`x590FindType` パラメーターを <xref:System.Security.Cryptography.X509Certificates.X509FindType.FindByIssuerName> に設定し、発行者の名前を指定します。 特定の発行者が必要ではない場合は、その他の <xref:System.Security.Cryptography.X509Certificates.X509FindType> 列挙値のいずれか (<xref:System.Security.Cryptography.X509Certificates.X509FindType.FindByTimeValid> など) を設定することもできます。  
  
## <a name="certificates-in-configuration"></a>構成における証明書  
 証明書は、構成を使用して設定することもできます。 証明書を含む、資格情報が指定されたサービスを作成する場合、 [ \<serviceBehaviors >](../../../../docs/framework/configure-apps/file-schema/wcf/servicebehaviors.md)です。 証明書が指定されたクライアントをプログラミングする際に、 [ \<endpointBehaviors >](../../../../docs/framework/configure-apps/file-schema/wcf/endpointbehaviors.md)です。  
  
## <a name="mapping-a-certificate-to-a-user-account"></a>ユーザー アカウントへの証明書のマッピング  
 IIS と Active Directory には、証明書を Windows ユーザー アカウントにマップできる機能があります。 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]この機能を参照してください[証明書をユーザー アカウントにマップ](http://go.microsoft.com/fwlink/?LinkId=88917)です。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]Active Directory のマッピングを使用して、参照してください[ディレクトリ サービスのマッピングでクライアント証明書のマッピング](http://go.microsoft.com/fwlink/?LinkId=88918)です。  
  
 この機能が有効になっている場合、<xref:System.ServiceModel.Security.X509ClientCertificateAuthentication.MapClientCertificateToWindowsAccount%2A> クラスの <xref:System.ServiceModel.Security.X509ClientCertificateAuthentication> プロパティを `true` に設定できます。 構成では、設定することができます、`mapClientCertificateToWindowsAccount`の属性、 [\<認証 >](../../../../docs/framework/configure-apps/file-schema/wcf/authentication-of-servicecertificate-element.md)要素`true`次のコードに示すように、します。  
  
```xml  
<serviceBehaviors>  
 <behavior name="MappingBehavior">  
  <serviceCredentials>  
   <clientCertificate>  
    <authentication certificateValidationMode="None" mapClientCertificateToWindowsAccount="true" />  
   </clientCertificate>  
  </serviceCredentials>  
 </behavior>  
</serviceBehaviors>  
```  
  
 Windows ユーザー アカウントを表すトークンに X.509 証明書をマップすると、Windows トークンを使用して保護されたリソースにアクセスできるため、このマッピングが特権の昇格と見なされます。 したがって、マッピングを行う前に、ドメイン ポリシーにそのポリシーに準拠する X.509 証明書が必要となります。 *SChannel*セキュリティ パッケージは、この要件を強制します。  
  
 [!INCLUDE[netfx35_long](../../../../includes/netfx35-long-md.md)] 以降を使用している場合は、Windows アカウントにマッピングされる前に、証明書がドメイン ポリシーに準拠していることが [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] によって確認されます。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] の最初のリリースでは、ドメイン ポリシーを参照せずにマッピングが実行されます。 そのため、マッピングが有効になっており、X.509 証明書がドメイン ポリシーを満たしていない場合は、最初のリリースの下で実行しているときには動作していた古いアプリケーションが動作しなくなる可能性があります。  
  
## <a name="see-also"></a>関連項目  
 <xref:System.ServiceModel.Channels>  
 <xref:System.ServiceModel.Security>  
 <xref:System.ServiceModel>  
 <xref:System.Security.Cryptography.X509Certificates.X509FindType>  
 [サービスとクライアントのセキュリティ保護](../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)
