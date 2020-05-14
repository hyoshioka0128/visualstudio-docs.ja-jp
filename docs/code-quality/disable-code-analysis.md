---
title: コード分析を無効にする
ms.date: 10/03/2019
ms.topic: conceptual
helpviewer_keywords:
- code analysis, disable
- disable code analysis
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 8db6ad7bed4b1526d87112f33d3586728728d7f5
ms.sourcegitcommit: 92361aac3665a934faa081e1d1ea89a067b01c5b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/17/2020
ms.locfileid: "79431398"
---
# <a name="how-to-disable-source-code-analysis-for-managed-code"></a>マネージ コードのソース コード分析を無効にする方法

::: moniker range=">=vs-2019"

このページでは、Visual Studio でコード分析を無効にするのに役立ちます。 無効にできる内容には制限があり、コード分析を無効にする手順は、いくつかの要因によって異なります。

- プロジェクトの種類 (.NET コア/標準対 .NET フレームワーク)

  .NET Core プロジェクトと .NET Standard プロジェクトの [コード分析] プロパティ ページには、NuGet パッケージとしてインストールされたアナライザーからのコード分析を無効にするオプションがあります。 詳細については、「 [.NET Core および .NET 標準プロジェクト](#net-core-and-net-standard-projects)」を参照してください。 .NET Framework プロジェクトのソース コード分析を無効にするには[、「.NET Framework プロジェクト](#net-framework-projects)」を参照してください。

- ソース分析と従来の分析

  このトピックは、ソース コード分析に適用され、従来の (バイナリ) 分析には適用されません。 レガシ分析の無効化については、「[方法 : レガシ コード分析を有効または無効にする](how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)」を参照してください。

## <a name="net-core-and-net-standard-projects"></a>.NET コアプロジェクトおよび .NET 標準プロジェクト

Visual Studio 2019 バージョン 16.3 以降では、ビルド時とデザイン時にアナライザーを実行するかどうかを制御できる 2 つのチェック ボックスが [コード分析] プロパティ ページに用意されています。 これらのオプションはプロジェクト固有です。

![ライブ コード分析または Visual Studio でのビルド時の有効または無効を切り上げる](media/run-on-build-run-live-analysis.png)

このページを開くには、**ソリューション エクスプローラ**でプロジェクト ノードを右クリックし、[**プロパティ]** を選択します。 [**コード分析**] タブを選択します。

- ビルド時にソース分析を無効にするには、[**ビルド時に実行**] オプションのチェックを外します。
- ライブ ソース分析を無効にするには、[**ライブ解析時に実行**] オプションをオフにします。

> [!NOTE]
> Visual Studio 2019 バージョン 16.5 以降、オンデマンドのコード分析実行ワークフローを希望する場合は、ライブ分析中にアナライザーの実行を無効にしたり、プロジェクトまたはオンデマンドソリューションでコード分析を手動で実行したりできます。 コード分析を手動で実行する方法については、「[方法 : マネージ コードのコード分析を手動で実行する](how-to-run-code-analysis-manually-for-managed-code.md)」を参照してください。  

## <a name="net-framework-projects"></a>.NET フレームワーク プロジェクト

アナライザーのソース コード分析を無効にするには、次の MSBuild プロパティを 1 つ以上[プロジェクト ファイル](../ide/solutions-and-projects-in-visual-studio.md#project-file)に追加します。

| MSBuild のプロパティ | 説明 | Default |
| - | - | - |
| `RunAnalyzersDuringBuild` | ビルド時にアナライザーを実行するかどうかを制御します。 | `true` |
| `RunAnalyzersDuringLiveAnalysis` | アナライザーがデザイン時にコードをライブで分析するかどうかを制御します。 | `true` |
| `RunAnalyzers` | ビルド時と設計時の両方でアナライザーを無効にします。 このプロパティは、 および`RunAnalyzersDuringBuild``RunAnalyzersDuringLiveAnalysis`より優先されます。 | `true` |

例 :

```xml
<RunAnalyzersDuringBuild>false</RunAnalyzersDuringBuild>
<RunAnalyzersDuringLiveAnalysis>false</RunAnalyzersDuringLiveAnalysis>
<RunAnalyzers>false</RunAnalyzers>
```

::: moniker-end

::: moniker range="vs-2017"

## <a name="source-analysis"></a>ソース解析

ソース[分析](roslyn-analyzers-overview.md)を 2017 でオフにすることはできません。 エラー一覧からアナライザ エラーをクリアする場合は、メニュー バーで [実行コード分析の**分析** > **] と [アクティブな問題を抑制**] を選択して、現在のすべての違反を抑制できます。 詳細については、[違反の抑制](use-roslyn-analyzers.md#suppress-violations)を参照してください。

Visual Studio 2019 バージョン 16.3 以降では、ソース コード分析をオフにしたり、オンデマンドで実行したりできます。 Visual Studio 2019 へのアップグレードを検討してください。

## <a name="legacy-analysis"></a>レガシ分析

**[コード分析**] プロパティ ページで、従来のビルド時分析を無効にすることができます。 詳細については、「[方法 : レガシ コード分析を有効または無効に](how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)する 」を参照してください。

::: moniker-end

## <a name="see-also"></a>関連項目

- [違反を抑制する](use-roslyn-analyzers.md#suppress-violations)
- [方法: レガシ コード分析を有効または無効にする](how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)
