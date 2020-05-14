---
title: '方法 : マネージ コードのコード分析を手動で実行する'
ms.date: 11/04/2019
ms.topic: conceptual
helpviewer_keywords:
- code analysis, running
- run code analysis
ms.assetid: 5086d228-f92e-4515-9708-c5b89b9e9a03
author: mavasani
ms.author: jillfra
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 5fdeb56a0c0f4c5904a00ec53d64dae87aa4e9a5
ms.sourcegitcommit: 92361aac3665a934faa081e1d1ea89a067b01c5b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/17/2020
ms.locfileid: "79431385"
---
# <a name="how-to-run-code-analysis-manually-for-managed-code-requires-visual-studio-2019-version-165-or-later"></a>方法: マネージ コードのコード分析を手動で実行する (Visual Studio 2019 バージョン 16.5 以降が必要)
既定では、.NET コンパイラ プラットフォーム ("Roslyn") コード アナライザーは、ビルド中だけでなく、ライブ分析を行うことによって、入力時に C# または Visual Basic コードを分析します。 したがって、通常はコード分析を手動でトリガーする必要はありません。 ただし、コード分析を手動でトリガーするシナリオがいくつかあります。

- 既定では、ライブ コード分析は、Visual Studio で開いているファイルに対してのみアナライザーを実行します。 ただし、特定のプロジェクトまたはソリューション内のすべてのファイルに対してコード分析の警告を表示する場合があります。 その場合は、プロジェクトまたはソリューションでコード分析を 1 回実行します。 または、ソリューション全体で継続的なライブ コード分析を実行できるようにすることもできます。 詳細については、「[方法 : マネージ コードのライブ コード分析スコープを構成する](./configure-live-code-analysis-scope-managed-code.md)」を参照してください。
- オンデマンド コード分析実行ワークフローは、継続的なライブ分析やビルド時分析よりも好まれます。 その場合は、ライブ分析やビルド中にアナライザーの実行を無効にすることができます。 分析を無効にする方法については、「[ソース コード分析を無効にする方法](disable-code-analysis.md)」を参照してください。 次に、プロジェクトまたはソリューションでコード分析を手動でトリガーする必要があります。 

### <a name="run-code-analysis-manually"></a>手動でのコード分析の実行

1. **ソリューション エクスプローラー**で、プロジェクトをクリックします。

2. [**分析**] メニューの [*プロジェクト名***でコード分析を実行**] をクリックします。

コード分析はバックグラウンドで実行を開始します。 Visual Studio のステータス バーの左下隅に"**プロジェクト>..\<のコード分析を実行しています"** というメッセージが表示されます。 コード分析が完了すると、ステータス メッセージはプロジェクト **>のコード\<分析が完了に**変わります。 すべてのコード分析診断でエラー一覧がすぐに更新されます。
