---
title: コード分析を無効にする
ms.date: 09/01/2020
ms.topic: how-to
helpviewer_keywords:
- code analysis, disable
- disable code analysis
author: mikadumont
ms.author: midumont
manager: jillfra
ms.openlocfilehash: 28a95038db83e2a03975b0a5baccdabdd18452d9
ms.sourcegitcommit: 4ae5e9817ad13edd05425febb322b5be6d3c3425
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2020
ms.locfileid: "90037147"
---
# <a name="disable-source-code-analysis-for-net"></a>.NET のソースコード分析を無効にする

::: moniker range=">=vs-2019"

このページを使用すると、Visual Studio でコード分析を無効にすることができます。 無効にできるものには制限があります。また、コード分析を無効にする手順は、いくつかの要因によって異なります。

- プロジェクトの種類 (.NET Core/Standard と .NET Framework)

  .NET Core および .NET Standard プロジェクトには、NuGet パッケージとしてインストールされたアナライザーからのコード分析を無効にするための [コード分析のプロパティ] ページにオプションがあります。 詳細については、「 [.Net Core と .NET Standard のプロジェクト](#net-core-and-net-standard-projects)」を参照してください。 .NET Framework プロジェクトのソースコード分析を無効にするには、「 [プロジェクトの .NET Framework](#net-framework-projects)」を参照してください。

- ソース分析と従来の分析

  このトピックは、レガシ (バイナリ) 分析ではなく、ソースコード分析に適用されます。 レガシ分析を無効にする方法の詳細については、「 [方法: レガシコード分析を有効または無効](how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)にする」を参照してください。

## <a name="net-core-and-net-standard-projects"></a>.NET Core と .NET Standard のプロジェクト

Visual Studio 2019 バージョン16.3 以降では、[コード分析] プロパティページで使用できるチェックボックスが2つあります。このチェックボックスを使用すると、アナライザーをビルド時に実行するか、デザイン時に実行するかを制御できます。 これらのオプションはプロジェクト固有です。

![Visual Studio でライブコード分析またはビルドを有効または無効にする](media/run-on-build-run-live-analysis.png)

このページを開くには、 **ソリューションエクスプローラー** でプロジェクトノードを右クリックし、[ **プロパティ**] を選択します。 [ **コード分析** ] タブを選択します。

- ビルド時にソース分析を無効にするには、 **[ビルド時に実行** ] オプションをオフにします。
- ライブソース分析を無効にするには、 **[ライブ分析で実行** する] オプションをオフにします。

> [!NOTE]
> Visual Studio 2019 バージョン16.5 以降では、オンデマンドのコード分析実行ワークフローを使用する場合は、ライブ分析中にアナライザーの実行を無効にしたり、プロジェクトまたはソリューションを必要に応じて手動でコード分析をトリガーしたりすることができます。 コード分析を手動で実行する方法については、「 [方法: マネージコードのコード分析を手動で実行する](how-to-run-code-analysis-manually-for-managed-code.md)」を参照してください。

## <a name="net-framework-projects"></a>.NET Framework プロジェクト

アナライザーのソースコード分析をオフにするには、次の MSBuild プロパティの1つまたは複数を [プロジェクトファイル](../ide/solutions-and-projects-in-visual-studio.md#project-file)に追加します。

| MSBuild のプロパティ | 説明 | Default |
| - | - | - |
| `RunAnalyzersDuringBuild` | アナライザーをビルド時に実行するかどうかを制御します。 | `true` |
| `RunAnalyzersDuringLiveAnalysis` | アナライザーがデザイン時にコードをライブで分析するかどうかを制御します。 | `true` |
| `RunAnalyzers` | ビルド時とデザイン時の両方でアナライザーを無効にします。 このプロパティは、およびよりも優先さ `RunAnalyzersDuringBuild` `RunAnalyzersDuringLiveAnalysis` れます。 | `true` |

次に例を示します。

```xml
<RunAnalyzersDuringBuild>false</RunAnalyzersDuringBuild>
<RunAnalyzersDuringLiveAnalysis>false</RunAnalyzersDuringLiveAnalysis>
<RunAnalyzers>false</RunAnalyzers>
```

::: moniker-end

::: moniker range="vs-2017"

## <a name="source-analysis"></a>ソース解析

Visual Studio 2017 では、 [ソース分析](roslyn-analyzers-overview.md) を無効にすることはできません。 **エラー一覧**からアナライザーのエラーをクリアする場合は、 **Analyze**  >  メニューバーの [**実行コード分析を分析し、アクティブな問題を抑制**する] を選択して、現在のすべての違反を抑制できます。 詳細については、「 [違反の抑制](use-roslyn-analyzers.md#suppress-violations)」を参照してください。

Visual Studio 2019 バージョン16.3 以降では、ソースコード分析を無効にしたり、オンデマンドで実行したりすることができます。 Visual Studio 2019 へのアップグレードを検討してください。

## <a name="legacy-analysis"></a>レガシ分析

[ **コード分析** のプロパティ] ページで、レガシのビルド時分析を無効にすることができます。 詳細については、「 [方法: レガシコード分析を有効または無効](how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)にする」を参照してください。

::: moniker-end

## <a name="see-also"></a>参照

- [違反を抑制する](use-roslyn-analyzers.md#suppress-violations)
- [方法: レガシコード分析を有効または無効にする](how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)
