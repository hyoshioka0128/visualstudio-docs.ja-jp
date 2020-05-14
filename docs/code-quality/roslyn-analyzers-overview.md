---
title: Roslyn アナライザーを使用したコード分析
ms.date: 10/03/2019
ms.topic: overview
helpviewer_keywords:
- code analysis, managed code
- analyzers
- Roslyn analyzers
- code analyzers
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 78a47cb2a5aefd7d20e0b8087f5f3ad735716175
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2020
ms.locfileid: "79431281"
---
# <a name="overview-of-source-code-analyzers"></a>ソース コード アナライザーの概要

.NET Compiler Platform ("Roslyn") のコード アナライザーでは、C# または Visual Basic コードのスタイル、品質と保守容易性、設計、その他の問題が検査されます。

- 一部のアナライザーは、Visual Studio に組み込まれています。 これらのアナライザーの診断 ID (コード) は、IDE0067 のように、IDExxxx の形式です。 これらのほとんどの組み込みアナライザーでは、[コードのスタイル](../ide/code-styles-and-code-cleanup.md)が検査され、[テキスト エディターの [オプション] ページ](../ide/code-styles-and-code-cleanup.md)または [EditorConfig ファイル](../ide/editorconfig-code-style-settings-reference.md)でユーザー設定を構成できます。 いくつかの組み込みアナライザーでは、コードの品質が確認されます。

- NuGet パッケージまたは Visual Studio 拡張機能として、追加のアナライザーをインストールできます。 次に例を示します。

  - [FxCop アナライザー](../code-quality/install-fxcop-analyzers.md) (Microsoft が推奨しているコード品質アナライザー)
  - サードパーティのアナライザー ([StyleCop](https://www.nuget.org/packages/StyleCop.Analyzers/)、[Roslynator](https://www.nuget.org/packages/Roslynator.Analyzers/)、[XUnit Analyzers](https://www.nuget.org/packages/xunit.analyzers/)、[Sonar Analyzer](https://www.nuget.org/packages/SonarAnalyzer.CSharp/) など)

アナライザーでルール違反が見つかった場合は、コード エディター (問題のあるコードの下の "*波線*" として) および [エラー一覧] ウィンドウで報告されます。

多くのアナライザー ルール (*診断*) には、1 つ以上の*コード修正*が関連付けられており、これを適用して問題を修正できます。 Visual Studio に組み込まれているアナライザー診断には、それぞれコード修正が関連付けられています。 コード修正は、電球アイコン メニューに、他の種類の[クイック アクション](../ide/quick-actions.md)と共に示されます。 これらのコード修正については、「[共通のクイック アクション](../ide/common-quick-actions.md)」を参照してください。

![アナライザーの違反とクイック アクションのコード修正](../code-quality/media/built-in-analyzer-code-fix.png)

## <a name="source-code-analysis-versus-legacy-analysis"></a>ソース コード分析と従来の分析

マネージ コードについては、[従来の分析](../code-quality/code-analysis-for-managed-code-overview.md)が Roslyn アナライザーによるソース分析に置き換えられます。 従来の分析ルールの多くは、既に Roslyn コード アナライザーとして書き換えられています。 .NET Core プロジェクトや .NET Standard プロジェクトなどの新しいプロジェクト テンプレートでは、従来の分析は使用できません。

従来の分析のルール違反と同様に、ソース コード分析の違反は Visual Studio の [エラー一覧] ウィンドウに表示されます。 さらに、ソース コード分析の違反は、コード エディターで問題のあるコードの下に "*波線*" としても示されます。 波線の色は、ルールの[重要度設定](../code-quality/use-roslyn-analyzers.md#rule-severity)によって異なります。 次のイメージには、3 つの違反 (&mdash;赤色、緑色、灰色が 1 つずつ) が示されています。

![Visual Studio でのコード エディターの波線](media/diagnostics-severity-colors.png)

有効になっている場合は従来の分析と同様、コード アナライザーでビルド時にコードが検査されますが、入力中もライブ状態になります。 現在のドキュメントのみで実行するか、開いているすべてのドキュメントで実行するか、またはソリューション全体で実行するようにライブ コード分析のスコープを構成できます。 「[方法:ライブ コード分析スコープを構成する](./configure-live-code-analysis-scope-managed-code.md)」をご覧ください。

> [!TIP]
> コード アナライザーからのビルド時のエラーと警告が表示されるのは、アナライザーが NuGet パッケージとしてインストールされている場合のみです。 組み込みアナライザー (たとえば、IDE0067 や IDE0068) はビルド時には実行されません。

Roslyn コード アナライザーでは、従来の分析で報告されるものと同じ種類の問題が報告されるだけでなく、ファイルやプロジェクトで発生した違反の 1 つ、またはすべてを簡単に修正することができます。 これらのアクションを*コード修正*と呼びます。 コード修正は IDE に固有のものです。Visual Studio では、[クイック アクション](../ide/quick-actions.md)として実装されます。 すべてのアナライザー診断にコード修正が関連付けられているわけではありません。

> [!NOTE]
> Visual Studio 2019 16.5 リリースより前のバージョンでは、 **[分析]**  >  **[コード分析の実行]** メニュー オプションを使用するとレガシ分析が実行されます。 Visual Studio 2019 16.5 以降では、 **[コード分析の実行]** メニュー オプションを使用すると、選択したプロジェクトまたはソリューションに対して Roslyn ベースのアナライザーが実行されます。

[エラー一覧] でコード アナライザーの違反と従来の分析の違反を区別するには、 **[ツール]** 列を確認します。 **ソリューション エクスプローラー**のアナライザー アセンブリのいずれかが [ツール] の値 (**Microsoft.CodeQuality.Analyzers** など) と一致する場合、違反はコード アナライザーからのものです。 それ以外の場合、違反は従来の分析からのものです。

![[エラー一覧] の [ツール] 列](media/code-analysis-tool-in-error-list.png)

> [!TIP]
> プロジェクト ファイルにある **RunCodeAnalysis** MSBuild プロパティは、従来の分析のみに適用されます。 アナライザーをインストールする場合、プロジェクト ファイルにある **RunCodeAnalysis** を **false** に設定し、従来の分析がビルド後に実行されないようにします。
>
> ```xml
> <RunCodeAnalysis>false</RunCodeAnalysis>
> ```

## <a name="nuget-package-versus-vsix-extension"></a>NuGet パッケージと VSIX 拡張機能

Roslyn コード アナライザーは、NuGet パッケージを使用してプロジェクトごとにインストールできます。 また、Visual Studio の拡張機能として使用できるものもあります。この場合、Visual Studio で開くすべてのソリューションに適用されます。 [アナライザーをインストールする](../code-quality/install-roslyn-analyzers.md)これら 2 つの方法には、主な動作の違いがいくつかあります。

### <a name="scope"></a>スコープ

Visual Studio 拡張機能としてアナライザーをインストールする場合は、ソリューション レベルで Visual Studio のすべてのインスタンスに適用されます。 NuGet パッケージとしてアナライザーをインストールする (推奨される方法) 場合、NuGet パッケージがインストールされたプロジェクトにのみ適用されます。 チーム環境では、NuGet パッケージとしてインストールされたアナライザーは、そのプロジェクトで作業する*すべての開発者* のスコープ内にあります。

### <a name="build-errors"></a>ビルド エラー

継続的インテグレーション (CI) ビルドの一部として、あるいはコマンド ラインを使用するなどして、ビルド時にルールを適用するには、NuGet パッケージとしてアナライザーをインストールします。 拡張機能としてアナライザーをインストールする場合、アナライザーの警告とエラーはビルド レポートに示されません。

次のイメージは、アナライザー ルール違反を含むプロジェクトのビルドからのコマンドライン ビルド出力を示しています。

![ルール違反を示す MSBuild 出力](media/command-line-build-analyzers.png)

### <a name="rule-severity"></a>ルールの重要度

Visual Studio 拡張機能としてインストールされたアナライザーからルールの重要度を構成することはできません。 [ルールの重要度](../code-quality/use-roslyn-analyzers.md#rule-severity)を構成するには、NuGet パッケージとしてアナライザーをインストールします。

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [Visual Studio にコード アナライザーをインストールする](../code-quality/install-roslyn-analyzers.md)

> [!div class="nextstepaction"]
> [Visual Studio でコード アナライザーを使用する](../code-quality/use-roslyn-analyzers.md)

## <a name="see-also"></a>関連項目

- [アナライザーに関する FAQ](analyzers-faq.md)
- [独自のコード アナライザーを作成する](../extensibility/getting-started-with-roslyn-analyzers.md)
- [.NET Compiler Platform SDK](/dotnet/csharp/roslyn-sdk/)
