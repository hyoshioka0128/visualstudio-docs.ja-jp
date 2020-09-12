---
title: .NET 用に手動でコード分析を実行する方法
ms.date: 09/02/2020
ms.topic: how-to
helpviewer_keywords:
- code analysis, running
- run code analysis
ms.assetid: 5086d228-f92e-4515-9708-c5b89b9e9a03
author: mikadumont
ms.author: midumont
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: c24fa8e835dced8332aa4c50870d6251bdd43e63
ms.sourcegitcommit: 4ae5e9817ad13edd05425febb322b5be6d3c3425
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2020
ms.locfileid: "90037160"
---
# <a name="run-code-analysis-manually-for-net"></a>.NET 用に手動でコード分析を実行する
既定では、.NET Compiler Platform ("Roslyn") アナライザーは、ビルド時だけでなくライブ分析を実行することで、入力時に C# または Visual Basic コードを分析します。 そのため、通常は手動でコード分析をトリガーする必要がありません。 ただし、コード分析を手動でトリガーする必要があるシナリオもあります。

> [!NOTE]
> コード分析を手動で実行するには、Visual Studio 2019 バージョン16.5 以降が必要です。

- 既定では、ライブコード分析は Visual Studio で開いているファイルに対してのみアナライザーを実行します。 ただし、特定のプロジェクトまたはソリューション内のすべてのファイルについて、コード分析の警告を表示することをお勧めします。 その場合は、プロジェクトまたはソリューションでコード分析を1回トリガーする必要があります。 または、継続的なライブコード分析を有効にして、ソリューション全体で実行できるようにすることもできます。 詳細については、[方法: マネージド コードのライブ コード分析スコープを構成する](./configure-live-code-analysis-scope-managed-code.md)」を参照してください。
- 継続的なライブ分析またはビルド時の分析により、オンデマンドのコード分析実行ワークフローを使用することもできます。 その場合は、ライブ分析やビルド中にアナライザーの実行を無効にすることができます。 分析を無効にする方法の詳細については、「 [ソースコード分析を無効にする方法](disable-code-analysis.md)」を参照してください。 次に、プロジェクトまたはソリューションで手動でコード分析をトリガーします。

### <a name="run-code-analysis-manually"></a>手動でのコード分析の実行

1. [ **ソリューションエクスプローラー**で、プロジェクトを選択します。

2. [**分析**] メニューの [*プロジェクト名***に対してコード分析を実行**] をクリックします。

コード分析は、バックグラウンドで実行を開始します。 Visual Studio のステータスバーの左下隅に、 **コード分析を実行 \<project> ** していることを確認するメッセージが表示されます。 コード分析が完了すると、ステータスメッセージが**に対して \<project> 完了したコード分析**に変わります。 エラー一覧は、すべてのコード分析診断でまもなく更新されます。
