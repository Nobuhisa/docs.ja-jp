---
title: "WPF アプリケーション (WPF) のビルド"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords: WPF application [WPF], building
ms.assetid: a58696fd-bdad-4b55-9759-136dfdf8b91c
caps.latest.revision: "45"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: cc027381ec8a5311d53077f103be035dd6c311d0
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="building-a-wpf-application-wpf"></a>WPF アプリケーション (WPF) のビルド
[!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] アプリケーションは、[!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] の実行可能ファイル (.exe)、 ライブラリ (.dll)、または両方のタイプのアセンブリの組み合わせとしてビルドできます。 このトピックでは、[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] アプリケーションをビルドする方法を紹介し、ビルド プロセスの主な手順について説明します。  
  
  
<a name="Building_a_WPF_Application_using_Command_Line"></a>   
## <a name="building-a-wpf-application"></a>WPF アプリケーションのビルド  
 WPF アプリケーションは、次の方法でコンパイルできます。  
  
-   コマンド ライン。 アプリケーションには、コード (XAML ではない) とアプリケーション定義ファイルだけを含める必要があります。 詳細については、「[csc.exe を使用したコマンド ラインからのビルド](~/docs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)」または「[コマンド ラインからのビルド (Visual Basic)](~/docs/visual-basic/reference/command-line-compiler/building-from-the-command-line.md)」を参照してください。  
  
-   Microsoft Build Engine (MSBuild)。 コードと XAML ファイルに加えて、アプリケーションには MSBuild プロジェクト ファイルを含める必要があります。 詳細については、「MSBuild」を参照してください。  
  
-   Visual Studio Visual Studio は、MSBuild を使用して WPF アプリケーションをコンパイルする統合開発環境であり、UI を作成するためのビジュアル デザイナーを含んでいます。 詳細については、「[Visual Studio でのアプリケーション開発](http://msdn.microsoft.com/en-us/97490c1b-a247-41fb-8f2c-bc4c201eff68)」および「[WPF デザイナー](http://msdn.microsoft.com/en-us/c6c65214-8411-4e16-b254-163ed4099c26)」を参照してください。  
  
<a name="The_Windows_Presentation_Foundation_Build_Pipeline"></a>   
## <a name="wpf-build-pipeline"></a>WPF ビルド パイプライン  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] プロジェクトがビルドされるときには、言語固有のターゲットと [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 固有のターゲットの組み合わせが呼び出されます。 これらのターゲットを実行するプロセスはビルド パイプラインと呼ばれます。主要な手順を次の図に示します。  
  
 ![WPF ビルド プロセス](../../../../docs/framework/wpf/app-development/media/wpfbuildsystem-figure1.png "WPFBuildSystem_Figure1")  
  
<a name="Pre_Build_Initializations"></a>   
### <a name="pre-build-initializations"></a>ビルド前の初期化  
 ビルドの前に、[!INCLUDE[TLA2#tla_msbuild](../../../../includes/tla2sharptla-msbuild-md.md)] は、次のような重要なツールとライブラリの場所を確認します。  
  
-   [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)]。  
  
-   [!INCLUDE[TLA2#tla_wcsdk](../../../../includes/tla2sharptla-wcsdk-md.md)] ディレクトリ。  
  
-   [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 参照アセンブリの場所。  
  
-   アセンブリ検索パスのプロパティ。  
  
 [!INCLUDE[TLA2#tla_msbuild](../../../../includes/tla2sharptla-msbuild-md.md)] がアセンブリを最初に検索する場所は、参照アセンブリ ディレクトリ (%ProgramFiles%\Reference Assemblies\Microsoft\Framework\v3.0\\) です。 この手順では、ビルド プロセスはさまざまなプロパティと項目グループを初期化し、必要なクリーンアップ作業も実行します。  
  
<a name="Resolving_references"></a>   
### <a name="resolving-references"></a>参照の解決  
 ビルド プロセスは、アプリケーション プロジェクトのビルドに必要なアセンブリを探して、バインドします。 このロジックは、`ResolveAssemblyReference` タスクに含まれます。 プロジェクト ファイル内で `Reference` として宣言されたすべてのアセンブリは、検索パスに関する情報と、すでにシステムにインストールされているアセンブリのメタデータと共にタスクに渡されます。 タスクは、アセンブリを検索し、インストールされているアセンブリのメタデータを使用して、出力マニフェストに含める必要のないコアの [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] アセンブリをフィルターして除外します。 これは、ClickOnce マニフェストに冗長な情報が含まれるのを避けるために行われます。 たとえば、PresentationFramework.dll は、[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] でビルドされた代表的なアプリケーションとみなすことができ、さらに、すべての [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] アセンブリは、[!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)] がインストールされているすべてのコンピューター上の同じ場所に存在するため、マニフェストにすべての [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)] 参照アセンブリに関するすべての情報を含める必要はありません。  
  
<a name="Markup_Compilation___Pass_1"></a>   
### <a name="markup-compilationpass-1"></a>マークアップ コンパイル - パス 1  
 この手順では、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ファイルを解析してコンパイルし、ランタイムが [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] の解析やプロパティ値の検証に時間を費やさずに済むようにします。 コンパイルされた [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ファイルを事前にトークン化するため、実行時の読み込みは、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ファイルを読み込むよりもはるかに短時間で終わります。  
  
 この手順では、`Page` ビルド項目である [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ファイルごとに、次のアクティビティが実行されます。  
  
1.  [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ファイルがマークアップ コンパイラによって解析されます。  
  
2.  [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 用にコンパイル済みの表現が作成されて、obj\Release フォルダーにコピーされます。  
  
3.  新しい部分クラスの CodeDOM 表現が作成され、obj\Release フォルダーにコピーされます。  
  
 さらに、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ファイルごとに、言語固有のコード ファイルが生成されます。 たとえば、[!INCLUDE[TLA2#tla_visualb](../../../../includes/tla2sharptla-visualb-md.md)] プロジェクトの Page1.xaml ページについては Page1.g.vb が生成されます。[!INCLUDE[TLA2#tla_cshrp](../../../../includes/tla2sharptla-cshrp-md.md)] プロジェクトの Page1.xaml ページについては Page1.g.cs が生成されます。 ファイル名の ".g" は、ファイルが生成されたコードであり、マークアップ ファイルのトップレベルの要素 (`Page` や `Window` など) に対する部分クラス宣言を持つことを示しています。 クラスは [!INCLUDE[TLA2#tla_cshrp](../../../../includes/tla2sharptla-cshrp-md.md)] の `partial` 修飾子 ([!INCLUDE[TLA2#tla_visualb](../../../../includes/tla2sharptla-visualb-md.md)] では `Extends`) によって宣言され、他の場所 (通常は分離コード ファイル Page1.xaml.cs) に別のクラス宣言があることを示します。  
  
 部分クラスが適切な基本クラスから拡張 (など<xref:System.Windows.Controls.Page>ページ) を実装し、<xref:System.Windows.Markup.IComponentConnector?displayProperty=nameWithType>インターフェイスです。 <xref:System.Windows.Markup.IComponentConnector>インターフェイスは、コンポーネントを初期化し、名前とそのコンテンツの要素のイベントに接続する方法があります。 その結果、生成されたコード ファイルには、次のようなメソッドの実装が含まれます。  
  
```csharp  
public void InitializeComponent() {  
    if (_contentLoaded) {  
        return;  
    }  
    _contentLoaded = true;  
    System.Uri resourceLocater =   
        new System.Uri(  
            "window1.xaml",   
            System.UriKind.RelativeOrAbsolute);  
    System.Windows.Application.LoadComponent(this, resourceLocater);  
}  
```  
  
```vb  
Public Sub InitializeComponent() _  
  
    If _contentLoaded Then  
        Return  
    End If  
  
    _contentLoaded = True  
    Dim resourceLocater As System.Uri = _  
        New System.Uri("mainwindow.xaml", System.UriKind.Relative)  
  
    System.Windows.Application.LoadComponent(Me, resourceLocater)  
  
End Sub  
```  
  
 既定では、マークアップ コンパイルは、同じ<xref:System.AppDomain>として、[!INCLUDE[TLA2#tla_msbuild](../../../../includes/tla2sharptla-msbuild-md.md)]エンジンです。 これにより、パフォーマンスが大幅に向上します。 この動作は、`AlwaysCompileMarkupFilesInSeparateDomain` プロパティで切り替えることができます。 これは、個別をアンロードしてすべての参照アセンブリをアンロードする利点<xref:System.AppDomain>です。  
  
<a name="Pass_2_of_Markup_Compilation"></a>   
### <a name="markup-compilationpass-2"></a>マークアップ コンパイル - パス 2  
 マークアップ コンパイルのパス 1 ですべての [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ページがコンパイルされるわけではありません。 ローカルで定義された型参照 (同じプロジェクト内の他のコードで定義された型の参照) を含む [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ファイルは、この時点ではコンパイルから除外されます。 これは、ローカルで定義された型は、ソース内にのみ存在し、まだコンパイルされていないためです。 これを判別するために、パーサーは、マークアップ ファイル内で `x:Name` などの項目を検索するヒューリスティックを使用します。 このようなインスタンスが見つかると、そのマークアップ ファイルのコンパイルは、コード ファイルがコンパイルされるまで延期され、その後、2 階目のマークアップ コンパイル パスで、これらのファイルが処理されます。  
  
<a name="File_Classification"></a>   
### <a name="file-classification"></a>ファイルの分類  
 ビルド プロセスは、配置されるアプリケーション アセンブリに基づいて、出力ファイルを異なるリソース グループに分けます。 一般的なローカライズされないアプリケーションでは、`Resource` としてマークされたすべてのデータ ファイルは、メイン アセンブリ (実行可能ファイルまたはライブラリ) に配置されます。 プロジェクトで `UICulture` が設定されると、コンパイル済みのすべての [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ファイルと、言語固有として明示的にマークされたリソースは、サテライト リソース アセンブリに配置されます。 さらに、言語に依存しないすべてのリソースは、メイン アセンブリに配置されます。 ビルド プロセスのこの手順で、この決定が行われます。  
  
 プロジェクト ファイル内の `ApplicationDefinition`、`Page`、および `Resource` ビルト アクションは、`Localizable` メタデータで拡張でき (受け入れられる値は `true` と `false`)、これによって、ファイルが言語固有か、言語に依存しないかを指定します。  
  
<a name="Core_Compilation"></a>   
### <a name="core-compilation"></a>コア コンパイル  
 コア コンパイル手順では、コード ファイルのコンパイルが行われます。 これは Microsoft.CSharp.targets や Microsoft.VisualBasic.targets など、言語固有のターゲット ファイル内のロジックによって調整されます。 ヒューリスティックによってマークアップ コンパイラの 1 回のパスでは不十分であると判断されると、メイン アセンブリが生成されます。 ただし、プロジェクト内の 1 つ以上の [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ファイルにローカルで定義された型の参照が含まれている場合、一時的な .dll ファイルが生成され、これによってマークアップ コンパイルの 2 回目のパスが完了すると、最終的なアプリケーション アセンブリが作成されます。  
  
<a name="Manifest_generation"></a>   
### <a name="manifest-generation"></a>マニフェストの生成  
 ビルド プロセスの終わりに、すべてのアプリケーション アセンブリとコンテンツ ファイルの準備が整った後で、アプリケーションの [!INCLUDE[TLA2#tla_clickonce](../../../../includes/tla2sharptla-clickonce-md.md)] マニフェストが生成されます。  
  
 配置マニフェスト ファイルは、配置モデル (現在のバージョン、更新動作、およびパブリッシャーの ID とデジタル署名) を記述します。 このマニフェストは、配置を処理する管理者が作成します。 ファイル拡張子は、.xbap ([!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)] 用) と、インストール型アプリケーションを表す .application です。 前者は `HostInBrowser` プロジェクト プロパティによって指定されるため、マニフェストはアプリケーションがブラウザーによってホストされることを識別します。  
  
 アプリケーション マニフェスト (.exe.manifest ファイル) は、アプリケーション アセンブリと依存ライブラリを記述し、アプリケーションに必要なアクセス許可をリストします。 このファイルは、アプリケーション開発者が作成します。 [!INCLUDE[TLA2#tla_clickonce](../../../../includes/tla2sharptla-clickonce-md.md)] アプリケーションを起動するために、ユーザーはアプリケーションの配置マニフェスト ファイルを開きます。  
  
 これらのマニフェスト ファイルは、常に [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)] 用に作成されます。 インストール型アプリケーションの場合、プロジェクト ファイル内で `GenerateManifests` プロパティの値が `true` に指定されない限り、作成されません。  
  
 [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)]さらに、これらのアクセス許可は、一般的なアプリケーションのインターネット ゾーンに割り当てられている 2 つの追加アクセス許可を取得します。<xref:System.Security.Permissions.WebBrowserPermission>と<xref:System.Security.Permissions.MediaPermission>です。 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] ビルド システムは、これらのアクセス許可をアプリケーション マニフェストで宣言します。  
  
<a name="Incremental_Build_Support"></a>   
## <a name="incremental-build-support"></a>インクリメンタル ビルドのサポート  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] ビルド システムは、インクリメンタル ビルドをサポートします。 これは、マークアップやコードに加えられた変更を検出し、変更の影響を受けるアイテムだけをコンパイルするという高度な機能です。 インクリメンタル ビルド メカニズムは、次のファイルを使用します。  
  
-   $(*AssemblyName*)_MarkupCompiler.Cache ファイル。コンパイラの現在の状態を保持します。  
  
-   $(*AssemblyName*)_MarkupCompiler.lref ファイル。ローカルで定義された型への参照を持つ [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ファイルをキャッシュします。  
  
 インクリメンタル ビルドを制御する規則のセットを次に示します。  
  
-   ビルド システムが変更を検出する最小単位は、ファイルです。 そのため、コード ファイルの場合、ビルド システムは、型が変更されたかどうか、またはコードが追加されたかどうかを検出できません。 プロジェクト ファイルの場合も同様です。  
  
-   インクリメンタル ビルドのメカニズムは、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ページがクラスを定義するのか、他のクラスを使用するのかを認識できなければなりません。  
  
-   `Reference` エントリが変更された場合は、すべてのページを再コンパイルします。  
  
-   コード ファイルが変更された場合は、ローカルで定義された型の参照を含むすべてのページを再コンパイルします。  
  
-   [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ファイルが変更された場合:  
  
    -   [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] がプロジェクトで `Page` として宣言されている場合: [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] にローカルで定義された型の参照が含まれていない場合は、その [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] とローカル参照を含むすべての [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ページを再コンパイルします。[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] にローカル参照が含まれる場合は、ローカル参照が含まれているすべての [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ページを再コンパイルします。  
  
    -   場合[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]として宣言されている`ApplicationDefinition`プロジェクト: すべて再コンパイル[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]ページ (理由: 各[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]への参照を持つ、<xref:System.Windows.Application>変更可能性がある型)。  
  
-   プロジェクト ファイルがコード ファイルを [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ファイルではなくアプリケーション定義として宣言している場合:  
  
    -   プロジェクト ファイル内の `ApplicationClassName` 値が変更されたかどうか (新しいアプリケーションの種類があるかどうか) を確認します。 変更されていた場合は、アプリケーション全体を再コンパイルします。  
  
    -   変更されていなかった場合は、ローカル参照を含んでいるすべての [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ページを再コンパイルします。  
  
-   プロジェクト ファイルが変更された場合、上記のすべての規則を適用し、再コンパイルする必要があるものを確認します。 `AssemblyName`、`IntermediateOutputPath`、`RootNamespace`、および `HostInBrowser` プロパティが変更された場合は、再コンパイルが必要です。  
  
 次のような再コンパイルのシナリオが考えられます。  
  
-   アプリケーション全体が再コンパイルされる。  
  
-   ローカルで定義された方参照を含んでいる [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ファイルのみが再コンパイルされる。  
  
-   何も再コンパイルされない (プロジェクトに何も変更が加えられていない場合)。  
  
## <a name="see-also"></a>関連項目  
 [WPF アプリケーションの配置](../../../../docs/framework/wpf/app-development/deploying-a-wpf-application-wpf.md)  
 [WPF MSBuild Reference (WPF MSBuild リファレンス)](/visualstudio/msbuild/wpf-msbuild-reference)  
 [WPF におけるパッケージの URI](../../../../docs/framework/wpf/app-development/pack-uris-in-wpf.md)  
 [WPF アプリケーションのリソース ファイル、コンテンツ ファイル、およびデータ ファイル](../../../../docs/framework/wpf/app-development/wpf-application-resource-content-and-data-files.md)
