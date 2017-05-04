---
title: ".NET Framework の概要 |Microsoft Docs"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- application development [.NET Framework]
- common language runtime
- common language runtime, about
- common language runtime, overview
ms.assetid: 29848c96-fc36-462d-8072-ba223a40b697
caps.latest.revision: 34
author: rpetrusha
ms.author: ronpet
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: bed74cee6db01a38bc0bc3c6eeffa33b682bbd80
ms.lasthandoff: 04/18/2017

---
# <a name="overview-of-the-net-framework"></a>.NET Framework の概要
.NET Framework は、次世代アプリケーションや XML Web サービスのビルドと実行をサポートするテクノロジです。 .NET Framework は、次の目的を実現するためにデザインされています。  
  
-   オブジェクト コードがローカルに保存され実行されるか、インターネットに分散されローカルに実行されるか、リモートで実行されるかにかかわらず、一貫したオブジェクト指向プログラミング環境を提供すること。  
  
-   ソフトウェア配置やバージョン管理の競合を最小化するコード実行環境を提供すること。  
  
-   作成者が不明なコードや、完全には信頼できないサード パーティ製のコードも含めて、コードを安全に実行できるようにするためのコード実行環境を提供すること。  
  
-   スクリプトやインタープリターが実行される環境でのパフォーマンスの問題を回避するコード実行環境を提供すること。  
  
-   Windows ベースのアプリケーションや Windows ベースや Web ベースのアプリケーションなど、多種のアプリケーションの開発において、ユーザーが一貫した方法で作業できること。  
  
-   .NET Framework に基づいたコードを他の任意のコードと統合できるように、すべての通信を業界標準に準拠して構築すること。  
  
> [!NOTE]
>  ユーザーと開発者のための .NET Framework の概要については、「[.NET Framework の概要](../../../docs/framework/get-started/index.md)」を参照してください。 .NET Framework をダウンロードするには、「[インストール ガイド](../../../docs/framework/install/guide-for-developers.md)」を参照してください。  
  
 .NET Framework は、共通言語ランタイムと .NET Framework クラス ライブラリから構成されます。 共通言語ランタイムは、.NET Framework の基礎となるコンポーネントです。 このランタイムは、実行時のコード管理を行うエージェントのようなものであり、メモリ管理、スレッド管理、リモート処理などの重要なサービスを提供したり、セキュリティや保全性を促進するために厳密なタイプ セーフやその他のコード整合性を強制的に適用したりします。 実際、コード管理の概念はこのランタイムの基本原理です。 このランタイムを使用して実行するように作成されたコードはマネージ コードと呼ばれ、そうでないコードはアンマネージ コードと呼ばれます。 クラス ライブラリは、従来のコマンド ラインやグラフィカル ユーザー インターフェイス (GUI) を使用したアプリケーションから、ASP.NET がもたらした最新の機構に基づく Web フォームや XML Web サービスなどのアプリケーションに至るまでのアプリケーション開発に使用できる、再利用可能な型の包括的なオブジェクト指向コレクションです。  
  
 .NET Framework は、アンマネージ コンポーネントでホストすることもできます。アンマネージ コンポーネントは、共通言語ランタイムをプロセスに読み込み、マネージ コードの実行を開始することで、マネージ機能とアンマネージ機能の両方を利用できるソフトウェア環境を構築できます。 .NET Framework には、いくつかのランタイム ホストが用意されているだけでなく、サードパーティ製ランタイム ホストの開発もサポートします。  
  
 たとえば、ASP.NET は、このランタイムをホストして、マネージ コードのためのスケーラブルなサーバー側環境を提供します。 ASP.NET はこのランタイムを直接利用して、ASP.NET アプリケーションや XML Web サービスを有効にします。Web フォーム アプリケーションと XML Web サービスについては、このトピックで後に説明します。  
  
 共通言語ランタイムを MIME 型拡張機能としてホストするアンマネージ アプリケーションの例として、Internet Explorer があります。 Internet Explorer を使用してこのランタイムをホストすることにより、マネージ コンポーネントや Windows フォーム コントロールを HTML ドキュメントに埋め込むことができます。 このランタイムをこの方法でホストすると、マネージ モバイル コードを実現できるだけでなく、それと同時に、中程度に信頼されたコードの実行や、分離ファイル ストレージなどのマネージ コードだけが提供できる重要な拡張機能も利用できます。  
  
 共通言語ランタイムおよびクラス ライブラリの、アプリケーションおよびシステム全体に対する関係を次の図に示します。 この図には、比較的大規模なアーキテクチャの内部でマネージ コードが動作する方法も示されています。  
  
 ![大規模アーキテクチャのマネージ コード](../../../docs/framework/get-started/media/circle.gif "circle")  
.NET Framework とアプリケーションおよびシステム全体との関係  
  
 .NET Framework の主要な機能を以降のセクションでより詳細に説明します。  
  
## <a name="features-of-the-common-language-runtime"></a>共通言語ランタイムの機能  
 共通言語ランタイムでは、メモリ、スレッドの実行、コードの実行、コードの整合性検査、コンパイル、およびその他のシステム サービスを管理します。 これらの機能は、共通言語ランタイムで実行されるマネージ コードにあらかじめ用意されています。  
  
 セキュリティ関連では、マネージ コンポーネントには、その出所 (インターネット、企業内ネットワーク、ローカル コンピューターなど) を含めた一連の要因に基づいて、さまざまな程度の信頼が与えられます。 そのためマネージ コンポーネントは、同じアクティブなアプリケーションで使用されていても、ファイル アクセス操作、レジストリ アクセス操作、またはその他の一般に公開されない機能を、実行できる場合と実行できない場合があります。  
  
 共通言語ランタイムは、コード アクセス セキュリティを強制的に適用します。 たとえば、Web ページに埋め込まれた実行可能ファイルがアニメーションや音声を再生できても、ユーザーの個人データ、ファイル システム、またはネットワークにはアクセスできないように信頼されます。 このようにして、このランタイムのセキュリティ機能は、適切な方法でインターネットに配置されたソフトウェアに、豊富な機能を特別に持たせることができます。  
  
 共通言語ランタイムでは、共通型システム (CTS: Common Type System) と呼ばれる厳密な型検査およびコード検査のインフラストラクチャを実装することで、コード保全性を強制的に適用します。 CTS は、すべてのマネージ コードが自己言及的であることを保証します。 各種の Microsoft 製およびサードパーティ製言語コンパイラは、CTS に準拠したマネージ コードを生成します。 そのためマネージ コードは、厳密な型の忠実性やタイプ セーフを適用しながら、他のマネージ型やマネージ インスタンスを利用できます。  
  
 さらに、共通言語ランタイムのマネージ環境では、ソフトウェアに共通する多くの問題を除去できます。 たとえば、このランタイムは、オブジェクトのレイアウトを自動的に処理し、それらのオブジェクトへの参照を管理し、不要になったオブジェクトを解放します。 この自動メモリ管理により、メモリ リークおよび無効なメモリ参照という、最も頻繁に生じる 2 つのアプリケーション エラーが解決されます。  
  
 共通言語ランタイムを使用することにより、開発者の生産性も向上します。 たとえば、プログラマは任意に選択した開発言語でアプリケーションを記述しながら、このランタイムの機能を十分に利用し、他の開発者が別の言語で記述したクラス ライブラリやコンポーネントを使用できます。 このランタイムをターゲットとして選択したコンパイラの販売元も、これらの利点を享受できます。 .NET Framework をターゲットとする言語コンパイラを使用すると、その言語で記述された既存のコードでも .NET Framework の機能が利用できるようになるため、既存のアプリケーションの移行作業が簡単になります。  
  
 このランタイムは、これから開発されるソフトウェアのためにデザインされていますが、現在や過去のソフトウェアもサポートします。 マネージ コードとアンマネージ コードには相互運用性があるため、開発者は必要な COM コンポーネントや DLL を使用し続けることができます。  
  
 共通言語ランタイムは、パフォーマンスを向上させるようにデザインされています。 このランタイムには多くの標準ランタイム サービスが用意されていますが、マネージ コードのインタープリター処理が行われることはありません。 ジャスト イン タイム (JIT: Just-In-Time) コンパイルと呼ばれる機能により、すべてのマネージ コードは、それが実行されるシステムのネイティブ機械語で実行できます。 また、メモリ マネージャーは、メモリの断片化を防止し、メモリ参照ができる限りローカルで行われるようにすることで、パフォーマンスを向上させます。  
  
 最後に、共通言語ランタイムは、Microsoft SQL Server や Internet Information Services (IIS) などの高性能なサーバー側アプリケーションでホストできます。 このインフラストラクチャにより、マネージ コードを使用してビジネス ロジックを記述し、ランタイム ホストをサポートする企業向けサーバーの優れたパフォーマンスを享受できます。  
  
## <a name="net-framework-class-library"></a>.NET Framework クラス ライブラリ  
 .NET Framework クラス ライブラリは、共通言語ランタイムと緊密に統合された再利用可能な型のコレクションです。 このクラス ライブラリはオブジェクト指向で、このライブラリが提供する型を使用することにより、独自に作成したマネージ コード内で機能を継承できます。 これは .NET Framework の型を使いやすくするだけでなく、.NET Framework の新機能の学習に必要な時間を減らします。 さらに、.NET Framework のクラスには、サードパーティ製のコンポーネントをシームレスに統合できます。  
  
 たとえば、.NET Framework のコレクション クラスは、独自のコレクション クラスの開発に使用できる一連のインターフェイスを実装しています。 作成したコレクション クラスは、.NET Framework のクラスとシームレスに統合して使用できます。  
  
 他のオブジェクト指向クラス ライブラリの場合と同様に、.NET Framework の型を使用することで、文字列の管理、データ コレクション、データベース接続、ファイル アクセスなどを含む、共通性のあるさまざまなプログラミング作業を行うことができます。 これらの共通の作業の他に、クラス ライブラリにはさまざまな特別の開発シナリオをサポートする型も含まれています。 たとえば、.NET Framework を使用すると、次のような種類のアプリケーションやサービスを開発できます。  
  
-   コンソール アプリケーション 「[コンソール アプリケーションの構築](../../../docs/standard/building-console-apps.md)」を参照してください。  
  
-   Windows GUI アプリケーション (Windows フォーム) 「[Windows フォーム](../../../docs/framework/winforms/index.md)」を参照してください。  
  
-   Windows Presentation Foundation (WPF) アプリケーション 「[Windows Presentation Foundation](../../../docs/framework/wpf/index.md)」を参照してください。  
  
-   ASP.NET アプリケーション 「[ASP.NET を使用した Web アプリケーション](../../../docs/framework/develop-web-apps-with-aspnet.md)」を参照してください。  
  
-   Windows サービス 「[Windows サービス アプリケーションの概要](../../../docs/framework/windows-services/introduction-to-windows-service-applications.md)」を参照してください。  
  
-   Windows Communication Foundation (WCF) を使用するサービス指向アプリケーション 「[WCF を使用したサービス指向アプリケーション](../../../docs/framework/wcf/index.md)」を参照してください。  
  
-   Windows Workflow Foundation (WF) を使用するワークフロー対応アプリケーション 「[.NET Framework におけるワークフローの作成](http://msdn.microsoft.com/en-us/cbf3880f-dc7b-466d-b808-1109b1223f4a)」を参照してください。  
  
 たとえば Windows フォーム クラスは、Windows GUI の開発を非常に簡単にする、再利用可能な型の包括的なセットです。 ASP.NET Web フォーム アプリケーションを作成する場合は、Web フォーム クラスを使用します。  
  
## <a name="see-also"></a>関連項目  
 [システム要件](../../../docs/framework/get-started/system-requirements.md)   
 [インストール ガイド](../../../docs/framework/install/guide-for-developers.md)   
 [開発ガイド](../../../docs/framework/development-guide.md)   
 [ツール](../../../docs/framework/tools/index.md)   
 [.NET Framework のサンプル](http://msdn.microsoft.com/en-us/177055f8-4a1f-43e7-aee6-995c196079b1)   
 [.NET Framework クラス ライブラリ](http://go.microsoft.com/fwlink/?LinkID=227195)