---
title: Visual Studio コンテナー ツールを構成する
description: Docker コンテナーを操作するために Visual Studio で使用できるツールを構成します。
author: ghogen
ms.author: ghogen
ms.topic: how-to
ms.date: 03/20/2019
ms.technology: vs-azure
ms.openlocfilehash: d2b3e2821e7697ad53b10a7148c22140aa1a07af
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85283217"
---
# <a name="how-to-configure-visual-studio-container-tools"></a>Visual Studio コンテナー ツールの構成方法

Visual Studio の設定を使用すると、Visual Studio での Docker コンテナーの使用方法のいくつかの側面を制御できます。これには、Docker コンテナーを操作するときのパフォーマンスとリソースの使用状況に影響する設定などが含まれます。

## <a name="container-tools-settings"></a>コンテナー ツールの設定

メイン メニューから **[ツール] > [オプション]** を選択し、 **[コンテナー ツール] > [設定]** を展開します。 コンテナー ツールの設定が表示されます。

::: moniker range="vs-2017"

![次のような Visual Studio コンテナー ツールのオプションが表示されます。[必要な Docker イメージをプロジェクト読み込み時に自動的にプルする]、[コンテナーをバックグラウンドで自動的に開始する]、[ソリューションを閉じる際に、コンテナーを自動的に強制終了します]、[localhost SSL 証明書を信頼するためのメッセージを表示しない]。](./media/overview/visual-studio-docker-tools-options.png)
::: moniker-end

::: moniker range=">=vs-2019"

コンテナー ツールの **[全般]** 設定:

![次のような Visual Studio コンテナー ツールのオプションが表示されます。[必要に応じて Docker Desktop をインストールします] および [ASP.NET Core SSL 証明書を信頼する]。](./media/configure-container-tools/tools-options-1.png)

コンテナー ツールの **[1 つのプロジェクト]** 設定と **[Docker Compose]** 設定:

![次のような Visual Studio コンテナー ツールのオプションが表示されます。[プロジェクトを閉じるときにコンテナーを中止する]、[プロジェクトを開く際に必要な Docker イメージをプルする]、[プロジェクトを開くときにコンテナーを実行する]。](./media/configure-container-tools/tools-options-2.png)
::: moniker-end

これらのオプションの設定方法を判断する際に、次の表を参照してください。

::: moniker range="vs-2017"
| 名前 | 既定の設定 | 対象 | 説明 |
| -----|:---------------:|:----------:| ----------- |
| 必要な Docker イメージをプロジェクト読み込み時に自動的にプルする | オン | Docker Compose | プロジェクトを読み込むときのパフォーマンスを向上するために、Visual Studio ではバックグラウンドで Docker のプル操作が開始されます。そのため、コードを実行する準備ができたら、イメージは既にダウンロードされているかダウンロード中です。 プロジェクトを読み込んでコードを参照するだけの場合は、これをオフにして不要なコンテナー イメージをダウンロードしないようにすることができます。 |
| コンテナーをバックグラウンドで自動的に開始する | オン | Docker Compose | また、パフォーマンスを向上するために、Visual Studio では、ユーザーがコンテナーを作成して実行するときに備えてボリュームのマウントを使用してコンテナーが作成されます。 コンテナーを作成するタイミングを制御する場合は、これをオフにします。 |
| ソリューションを閉じる際に、コンテナーを自動的に強制終了します | オン | Docker Compose | ソリューションを閉じた後または Visual Studio を終了した後もソリューションのコンテナーを実行し続ける場合は、これをオフにします。 |
| localhost SSL 証明書を信頼するためのメッセージを表示しない | オフ | ASP.NET Core 2.1 プロジェクト | localhost SSL 証明書が信頼されていない場合、このチェックボックスがオンになっていない限り、プロジェクトを実行するたびに Visual Studio によって確認メッセージが表示されます。 |
::: moniker-end

::: moniker range=">=vs-2019"

次の表で、 **[全般]** 設定について説明します。

| 名前 | 既定の設定 | 対象 | 説明 |
| -----|:---------------:|:----------:| ----------- |
| 必要に応じて Docker Desktop をインストールします | プロンプトを表示する | 1 つのプロジェクト、Docker Compose | Docker Desktop がインストールされていない場合にプロンプトを表示するかどうかを選択します。 |
| ASP.NET Core SSL 証明書を信頼する | プロンプトを表示する | ASP.NET Core 2.x プロジェクト | localhost SSL 証明書が信頼されていない場合に、 **[プロンプトを表示する]** に設定すると、プロジェクトを実行するたびに Visual Studio によって確認メッセージが表示されます。 |

次の表で、 **[1 つのプロジェクト]** 設定と **[Docker Compose]** 設定について説明します。

| 名前 | 既定の設定 | 対象 | 説明 |
| -----|:---------------:|:----------:| ----------- |
| プロジェクトを開く際に必要な Docker イメージをプルします | True | 1 つのプロジェクト、Docker Compose | プロジェクトを読み込むときのパフォーマンスを向上するために、Visual Studio ではバックグラウンドで Docker のプル操作が開始されます。そのため、コードを実行する準備ができたら、イメージは既にダウンロードされているかダウンロード中です。 プロジェクトを読み込んでコードを参照するだけの場合は、**False** に設定して不要なコンテナー イメージをダウンロードしないようにすることができます。 |
| プロジェクトを開くときにコンテナーを実行する | True | 1 つのプロジェクト、Docker Compose | また、パフォーマンスを向上するために、Visual Studio では、ユーザーがコンテナーを作成して実行するときに備えて、事前にコンテナーが作成されます。 コンテナーが作成されるタイミングを制御する場合は、**False** に設定します。 |
| Stop containers on project close (プロジェクトを閉じるときにコンテナーを中止する) | True | 1 つのプロジェクトと Docker Compose | ソリューションを閉じた後または Visual Studio を終了した後もソリューションのコンテナーを実行し続ける場合は、**False** に設定します。 |

::: moniker-end
> [!WARNING]
> localhost SSL 証明書が信頼されていない場合に、プロンプトが表示されないようにチェックボックスをオンにすると、HTTPS Web 要求はアプリまたはサービスの実行時に失敗する可能性があります。 その場合は、 **[メッセージを表示しない]** チェックボックスをオフにしてプロジェクトを実行し、プロンプトで信頼を示します。

## <a name="next-steps"></a>次の手順

この[概要](overview.md)で、Visual Studio でのコンテナーの操作の詳細について確認します。