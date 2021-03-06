---
title: "dotnet コマンド - .NET Core CLI"
description: "dotnet コマンド (.NET Core CLI ツールの一般的なドライバー) とその使用法について説明します。"
author: mairaw
ms.author: mairaw
ms.date: 08/14/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.openlocfilehash: bba8d77cda7538bf008dc0f510f9279d3c695c3d
ms.sourcegitcommit: a19548e5167cbe7e9e58df4ffd8c3b23f17d5c7a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2017
---
# <a name="dotnet-command"></a>dotnet コマンド

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>名前

`dotnet` - コマンドラインのコマンドを実行するための一般的なドライバーです。

## <a name="synopsis"></a>構文

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)
```
dotnet [command] [arguments] [--additional-deps] [--additionalprobingpath] [-d|--diagnostics] [--fx-version] [-h|--help] [--info] [--roll-forward-on-no-candidate-fx] [-v|--verbose] [--version]
```
# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)
```
dotnet [command] [arguments] [--additionalprobingpath] [-d|--diagnostics] [--fx-version] [-h|--help] [--info] [-v|--verbose] [--version]
```
---

## <a name="description"></a>説明

`dotnet` は、コマンド ライン インターフェイス (CLI) ツールチェーンの一般的なドライバーです。 単独で呼び出され、簡単な使用方法を提供します。

特定の機能がそれぞれコマンドとして実装されます。 機能を使用するには、[`dotnet build`](dotnet-build.md) のように、`dotnet` の後にコマンドを指定します。 コマンドに続く引数はすべて独自の引数です。

`dotnet` が単独でコマンドとして使用されるのは、[フレームワークに依存するアプリ](../deploying/index.md)を実行する場合のみです。 アプリケーションを実行する場合は、`dotnet` の動詞の後にアプリケーション DLL を指定します (`dotnet myapp.dll` など)。

## <a name="options"></a>オプション

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

`--additionaldeps <PATH>`

その他へのパス*deps.json*ファイル。

`--additionalprobingpath <PATH>`

プローブ ポリシーとプローブするアセンブリを含むパスです。

`-d|--diagnostics`

診断出力を有効にします。

`--fx-version <VERSION>`

アプリケーションを実行するために使用するインストール済み .NET Core ランタイムのバージョンです。

`-h|--help`

コマンドの短いヘルプを印刷します。 `dotnet` で使用すると、使用可能なコマンドのリストも印刷されます。

`--info`

現在のオペレーティング システム、バージョンのコミット SHA、およびその他の情報など、CLI ツールと環境の詳細情報を印刷します。

`--roll-forward-on-no-candidate-fx`

 共有フレームワークの候補なしでロールフォワードします。

`-v|--verbose`

詳細出力を有効にします。

`--version`

使用中の .NET Core SDK のバージョンを印刷します。

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

`--additionalprobingpath <PATH>`

プローブ ポリシーとプローブするアセンブリを含むパスです。

`-d|--diagnostics`

診断出力を有効にします。

`--fx-version <VERSION>`

アプリケーションを実行するために使用するインストール済み .NET Core ランタイムのバージョンです。

`-h|--help`

コマンドの短いヘルプを印刷します。 `dotnet` で使用すると、使用可能なコマンドのリストも印刷されます。

`--info`

現在のオペレーティング システム、バージョンのコミット SHA、およびその他の情報など、CLI ツールと環境の詳細情報を印刷します。

`-v|--verbose`

詳細出力を有効にします。

`--version`

使用中の .NET Core SDK のバージョンを印刷します。

---

## <a name="dotnet-commands"></a>dotnet コマンド

### <a name="general"></a>全般

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

| コマンド                             | 関数                                                            |
| ----------------------------------- | ------------------------------------------------------------------- |
| [dotnet build](dotnet-build.md)     | .NET Core アプリケーションをビルドします。                                     |
| [dotnet clean](dotnet-clean.md)     | クリーン ビルド出力です。                                              |
| [dotnet help](dotnet-help.md)       | コマンドのより詳細なドキュメントをオンラインで表示します。           |
| [dotnet migrate](dotnet-migrate.md) | 有効な Preview 2 プロジェクトを .NET Core SDK 1.0 プロジェクトに移行します。  |
| [dotnet msbuild](dotnet-msbuild.md) | MSBuild コマンド ラインへのアクセスを提供します。                        |
| [dotnet new](dotnet-new.md)         | 指定されたテンプレートの C# または F# プロジェクトを初期化します。                |
| [dotnet pack](dotnet-pack.md)       | コードの NuGet パッケージを作成します。                               |
| [dotnet publish](dotnet-publish.md) | .NET Framework に依存するアプリケーションまたは自己完結型アプリケーションを発行します。 |
| [dotnet restore](dotnet-restore.md) | 指定されたアプリケーションの依存関係を復元します。                  |
| [dotnet run](dotnet-run.md)         | ソースからアプリケーションを実行します。                                   |
| [dotnet sln](dotnet-sln.md)         | ソリューション ファイルのプロジェクトを追加、削除、一覧表示するオプション。       |
| [dotnet store](dotnet-store.md)     | ランタイム パッケージ ストアにアセンブリを格納します。                     |
| [dotnet test](dotnet-test.md)       | テスト ランナーを使用してテストを実行します。                                     |

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

| コマンド                             | 関数                                                            |
| ----------------------------------- | ------------------------------------------------------------------- |
| [dotnet build](dotnet-build.md)     | .NET Core アプリケーションをビルドします。                                     |
| [dotnet clean](dotnet-clean.md)     | クリーン ビルド出力です。                                              |
| [dotnet migrate](dotnet-migrate.md) | 有効な Preview 2 プロジェクトを .NET Core SDK 1.0 プロジェクトに移行します。  |
| [dotnet msbuild](dotnet-msbuild.md) | MSBuild コマンド ラインへのアクセスを提供します。                        |
| [dotnet new](dotnet-new.md)         | 指定されたテンプレートの C# または F# プロジェクトを初期化します。                |
| [dotnet pack](dotnet-pack.md)       | コードの NuGet パッケージを作成します。                               |
| [dotnet publish](dotnet-publish.md) | .NET Framework に依存するアプリケーションまたは自己完結型アプリケーションを発行します。 |
| [dotnet restore](dotnet-restore.md) | 指定されたアプリケーションの依存関係を復元します。                  |
| [dotnet run](dotnet-run.md)         | ソースからアプリケーションを実行します。                                   |
| [dotnet sln](dotnet-sln.md)         | ソリューション ファイルのプロジェクトを追加、削除、一覧表示するオプション。       |
| [dotnet test](dotnet-test.md)       | テスト ランナーを使用してテストを実行します。                                     |

---

### <a name="project-references"></a>プロジェクト参照

コマンド | 関数
--- | ---
[dotnet add reference](dotnet-add-reference.md) | プロジェクト参照を追加します。
[dotnet list reference](dotnet-list-reference.md) | プロジェクト参照をリストします。
[dotnet remove reference](dotnet-remove-reference.md) | プロジェクト参照を削除します。

### <a name="nuget-packages"></a>NuGet パッケージ

コマンド | 関数
--- | ---
[dotnet add package](dotnet-add-package.md) | NuGet パッケージを追加します。
[dotnet remove package](dotnet-remove-package.md) | NuGet パッケージを削除します。

### <a name="nuget-commands"></a>NuGet コマンド

コマンド | 関数
--- | ---
[dotnet nuget delete](dotnet-nuget-delete.md) | サーバーからパッケージを削除または一覧から削除します。
[dotnet nuget locals](dotnet-nuget-locals.md) | HTTP 要求キャッシュ、一時的なキャッシュ、コンピューター全体のグローバル パッケージ フォルダーなどのローカルの NuGet リソースをクリアまたは一覧表示します。
[dotnet nuget push](dotnet-nuget-push.md) | パッケージをサーバーにプッシュして発行します。

## <a name="examples"></a>例

コンパイルして実行できるサンプルの .NET Core コンソール アプリケーションを初期化します。

`dotnet new console`

指定されたアプリケーションの依存関係を復元します。

`dotnet restore`

[!INCLUDE[DotNet Restore Note](~/includes/dotnet-restore-note.md)]

指定されたディレクトリにプロジェクトとその依存関係をビルドします。

`dotnet build`

`myapp.dll` という名前のフレームワークに依存するアプリを実行します。

`dotnet myapp.dll`

## <a name="environment-variables"></a>環境変数

`DOTNET_PACKAGES`

プライマリ パッケージのキャッシュです。 設定されていない場合は、既定で `$HOME/.nuget/packages` (Unix の場合) または `%HOME%\NuGet\Packages` (Windows の場合) になります。

`DOTNET_SERVICING`

ランタイムの読み込み時に共有ホストで使用するサービス インデックスの場所を指定します。

`DOTNET_CLI_TELEMETRY_OPTOUT`

.NET Core ツールの使用に関するデータを収集し、Microsoft に送信するかどうかを指定します。 `true` に設定するとテレメトリ機能が無効になります (指定できる値は `true`、`1`、または `yes` です)。それ以外の場合は `false` に設定します。この場合、テレメトリ機能が有効になります (指定できる値は `false`、`0`、または `no` です)。 設定されていない場合、既定で `false` になり、テレメトリ機能はアクティブになります。
