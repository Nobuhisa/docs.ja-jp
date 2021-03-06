---
title: "Docker コンテナー用 .NET Core と .NET Framework の選択"
description: ".NET マイクロサービス: コンテナー化された .NET アプリケーションのアーキテクチャ | Docker コンテナー用 .NET Core と .NET Framework の選択"
keywords: "Docker, マイクロサービス, ASP.NET, コンテナー"
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 05/26/2017
ms.prod: .net-core
ms.technology: dotnet-docker
ms.topic: article
ms.openlocfilehash: f7a5fee26f4d138ae22f3551a25a674b22a2f6d1
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2017
---
# <a name="choosing-between-net-core-and-net-framework-for-docker-containers"></a>Docker コンテナー用 .NET Core と .NET Framework の選択

.NET を使用してサーバー側のコンテナー化された Docker アプリケーションをビルドする場合に選択できるサポート対象の実装には、[.NET Framework](https://www.microsoft.com/net/download/framework) と [.NET Core](https://www.microsoft.com/net/download/core) の 2 つがあります。 この 2 つは多数の .NET Standard コンポーネントを共有しているため、両者でコードを共有できます。 ただし、これらには基本的な違いがあり、どちらの実装を使用するかは実行内容によって決まります。 このセクションでは、それぞれの実装を選択する場合のガイダンスを提供します。


>[!div class="step-by-step"]
[前へ] (../container-docker-introduction/docker-containers-images-registries.md) [次へ] (general-guidance.md)
