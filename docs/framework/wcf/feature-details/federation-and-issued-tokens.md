---
title: "フェデレーションと発行済みトークン"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- WCF, federation
- issued tokens [WCF]
- federation [WCF], issued tokens
ms.assetid: 4c31ee7d-a820-4067-8b84-a83049021bb6
caps.latest.revision: "16"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: 05a110318bbe92f18d0bc6becb453a5d7851821c
ms.sourcegitcommit: ce279f2d7fe2220e6ea0a25a8a7a5370ddf8d9f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2017
---
# <a name="federation-and-issued-tokens"></a>フェデレーションと発行済みトークン
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] を使用すれば、WS-Federation および WS-Trust 仕様を実装したサービスとセキュリティで保護された通信を行うクライアントを作成できます。 これらの仕様では、異なる信頼領域間での認証と承認を可能にする機構を提供するために、XML、SOAP、および Web サービス記述言語 (WSDL: Web Services Description Language) が使用されます。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [フェデレーション](../../../../docs/framework/wcf/feature-details/federation.md)  
 フェデレーションの概要を説明します。  
  
 [フェデレーションと信頼](../../../../docs/framework/wcf/feature-details/federation-and-trust.md)  
 フェデレーション サービスまたはクライアントを作成するときに注意する必要がある設計上の問題を示します。  
  
 [方法: フェデレーション クライアントを作成します。](../../../../docs/framework/wcf/feature-details/how-to-create-a-federated-client.md)  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] でフェデレーション クライアントを作成するための基本を説明します。  
  
 [方法: フェデレーション サービスの資格情報を構成します。](../../../../docs/framework/wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md)  
 フェデレーション サービスを作成する手順を説明します。  
  
 [方法: WSFederationHttpBinding を作成します。](../../../../docs/framework/wcf/feature-details/how-to-create-a-wsfederationhttpbinding.md)  
 `WSFederationHttpBinding` を使用するクライアントおよびサービスを構成する方法を説明します。  
  
 [方法: セキュリティ トークン サービスの作成](../../../../docs/framework/wcf/feature-details/how-to-create-a-security-token-service.md)  
 セキュリティ トークン サービスを作成する手順を説明します。  
  
 [セキュリティ アサーション マークアップ言語 (SAML) トークンとクレーム](../../../../docs/framework/wcf/feature-details/saml-tokens-and-claims.md)  
 多様なクレームの種類を作成できる拡張可能な SAML (Security Assertions Markup Language) トークンについて説明します。  
  
 [方法: ローカル発行者を構成します。](../../../../docs/framework/wcf/feature-details/how-to-configure-a-local-issuer.md)  
 セキュリティ トークンのローカル発行者の作成方法を説明します。  
  
 [方法: WSFederationHttpBinding 上のセッションが無効にするにセキュリティで保護](../../../../docs/framework/wcf/feature-details/how-to-disable-secure-sessions-on-a-wsfederationhttpbinding.md)  
 `WSFederationHttpBinding` のセキュリティで保護されたセッションを無効にする方法を説明します。 クライアントごとにセッションが必要になる Web ファームを作成する場合には、セキュリティで保護されたセッションを無効化する必要があります。  
  
## <a name="reference"></a>参照  
 <xref:System.IdentityModel.Claims>  
  
 <xref:System.ServiceModel.ServiceAuthorizationManager>  
  
 <xref:System.IdentityModel.Tokens.SamlSecurityToken>  
  
 <xref:System.ServiceModel.Security.IssuedTokenClientCredential>  
  
 <xref:System.ServiceModel.Security.IssuedTokenServiceCredential>  
  
 <xref:System.ServiceModel.Security.Tokens.IssuedSecurityTokenParameters>  
  
 <xref:System.ServiceModel.Security.Tokens.IssuedSecurityTokenProvider>  
  
 <xref:System.ServiceModel.WSFederationHttpBinding>  
  
## <a name="see-also"></a>関連項目  
 [承認](../../../../docs/framework/wcf/feature-details/authorization-in-wcf.md)  
 [カスタム トークン](../../../../docs/framework/wcf/extending/custom-tokens.md)  
 [Windows Server App Fabric のセキュリティ モデル](http://go.microsoft.com/fwlink/?LinkID=201279&clcid=0x409)
