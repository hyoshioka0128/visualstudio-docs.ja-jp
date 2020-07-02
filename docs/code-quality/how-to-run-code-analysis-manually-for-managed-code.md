---
title: マネージコードのコード分析を手動で実行する方法
ms.date: 11/04/2019
ms.topic: how-to
helpviewer_keywords:
- code analysis, running
- run code analysis
ms.assetid: 5086d228-f92e-4515-9708-c5b89b9e9a03
author: mavasani
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 874d95b65b99af4b5a6b00d45101236f62db3df1
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85769362"
---
# <a name="how-to-run-code-analysis-manually-for-managed-code-requires-visual-studio-2019-version-165-or-later"></a>方法: マネージコードのコード分析を手動で実行する (Visual Studio 2019 バージョン16.5 以降が必要)
既定では、.NET Compiler Platform ("Roslyn") コードアナライザーは、ビルド時だけでなく、ライブ分析を行うことによって、C# または Visual Basic コードを分析します。 そのため、通常は手動でコード分析をトリガーする必要がありません。 ただし、コード分析を手動でトリガーする必要があるシナリオもあります。

- 既定では、ライブコード分析は Visual Studio で開いているファイルに対してのみアナライザーを実行します。 ただし、特定のプロジェクトまたはソリューション内のすべてのファイルについて、コード分析の警告を表示することをお勧めします。 その場合は、プロジェクトまたはソリューションでコード分析を1回トリガーする必要があります。 または、継続的なライブコード分析を有効にして、ソリューション全体で実行できるようにすることもできます。 詳細については、「[方法: マネージコードのライブコード分析スコープを構成する](./configure-live-code-analysis-scope-managed-code.md)」を参照してください。
- 継続的なライブ分析またはビルド時の分析により、オンデマンドのコード分析実行ワークフローを使用することもできます。 その場合は、ライブ分析やビルド中にアナライザーの実行を無効にすることができます。 分析を無効にする方法の詳細については、「[ソースコード分析を無効にする方法](disable-code-analysis.md)」を参照してください。 次に、プロジェクトまたはソリューションで手動でコード分析をトリガーします。 

### <a name="run-code-analysis-manually"></a>手動でのコード分析の実行

1. **ソリューションエクスプローラー**で、プロジェクトをクリックします。

2. [**分析**] メニューの [*プロジェクト名***に対してコード分析を実行**] をクリックします。

コード分析は、バックグラウンドで実行を開始します。 Visual Studio のステータスバーの左下隅に、**コード分析を実行 \<project> **していることを確認するメッセージが表示されます。 コード分析が完了すると、ステータスメッセージが**に対して \<project> 完了したコード分析**に変わります。 エラー一覧は、すべてのコード分析診断でまもなく更新されます。
