---
title: エディタ構成とアナライザー
ms.date: 03/11/2019
ms.topic: conceptual
helpviewer_keywords:
- analyzers, faq
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 56b0c0defe5593c9dc0e2111ef5984a5c51eaf55
ms.sourcegitcommit: a7f781d5a089e6aab6b073a07f3d4d2967af8aa6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "81760139"
---
# <a name="code-analysis-faq"></a>コード分析に関する FAQ

このページには、Visual Studio での .NET コンパイラ プラットフォーム ベースのコード分析に関してよく寄せられる質問への回答が含まれています。

## <a name="code-analysis-versus-editorconfig"></a>コード分析とエディター構成

**Q**: コードのスタイルをチェックするためにコード分析または EditorConfig を使用する必要がありますか?

**A**: コード分析ファイルとエディタ構成ファイルは、手作業で動作します。 [EditorConfig ファイル](../ide/editorconfig-code-style-settings-reference.md)またはテキスト エディターの[[オプション]](../ide/code-styles-and-code-cleanup.md)ページでコード スタイルを定義する場合は、Visual Studio に組み込まれているコード アナライザーを実際に構成しています。 EditorConfig ファイルを使用してアナライザー ルールを有効または無効にしたり[、FxCop アナライザ](configure-fxcop-analyzers.md)ーなどの NuGet アナライザ パッケージを構成したりできます。

## <a name="editorconfig-versus-rule-sets"></a>エディタ構成対ルールセット

**Q**: ルール セットまたは EditorConfig ファイルを使用してアナライザーを設定する必要がありますか?

**A**: ルール セットと EditorConfig ファイルは共存でき、アナライザーの設定にも使用できます。 EditorConfig ファイルとルール セットの両方を使用すると、ルールを有効または無効にしたり、それらの重大度を設定したりできます。

ただし、EditorConfig ファイルには、ルールを構成する追加の方法もあります。

- FxCop アナライザーの場合、EditorConfig ファイルを使用して[、分析するコードの種類を定義](fxcop-analyzer-options.md)できます。
- Visual Studio に組み込まれているコード スタイル のアナライザーの場合、EditorConfig ファイルを使用すると、コードベース[の推奨されるコード スタイルを定義](../ide/editorconfig-code-style-settings-reference.md)できます。

ルール セットと EditorConfig ファイルに加えて、一部のアナライザーは、C# および VB コンパイラ用の[追加ファイル](../ide/build-actions.md#build-action-values)としてマークされたテキスト ファイルを使用して構成されます。

> [!NOTE]
> - EditorConfig ファイルは、ルールを有効にし、Visual Studio 2019 バージョン 16.3 以降で重大度を設定する場合にのみ使用できます。
> - EditorConfig ファイルは、従来の分析を構成するために使用することはできません。

## <a name="code-analysis-in-ci-builds"></a>CI ビルドでのコード分析

**Q**: .NET コンパイラ プラットフォーム ベースのコード分析は、継続的インテグレーション (CI) ビルドで機能しますか?

**A**: はい。 NuGet パッケージからインストールされるアナライザーの場合、CI ビルド中など、[ビルド時に](roslyn-analyzers-overview.md#build-errors)これらの規則が適用されます。 CI で使用されるアナライザーは、ルール セットと EditorConfig ファイルの両方からルール構成を尊重します。 現在、Visual Studio に組み込まれているコード アナライザーは NuGet パッケージとして使用できないので、CI ビルドではこれらの規則を適用できません。

## <a name="ide-analyzers-versus-stylecop"></a>IDE アナライザーとスタイルコップ

**Q**: Visual Studio IDE コード アナライザーとスタイルコップ アナライザーの違いは何ですか?

**A**: Visual Studio IDE には、コード スタイルと品質の問題の両方を探す組み込みのアナライザーが含まれています。 これらのルールは、新しい言語機能を導入する際に使用し、コードの保守性を向上させるために役立ちます。 IDE アナライザーは、各 Visual Studio リリースで継続的に更新されます。

[StyleCop アナライザー](https://github.com/DotNetAnalyzers/StyleCopAnalyzers)は、コード内のスタイルの一貫性をチェックする NuGet パッケージとしてインストールされたサードパーティ製のアナライザーです。 一般に、StyleCop ルールを使用すると、あるスタイルを別のスタイルよりも優先することなく、コード ベースの個人設定を設定できます。

## <a name="code-analyzers-versus-legacy-analysis"></a>コード アナライザーと従来の分析

**Q**: 従来の分析と .NET コンパイラ プラットフォーム ベースのコード分析の違いは何ですか。

**A**.NET コンパイラ プラットフォーム ベースのコード分析では、ソース コードをリアルタイムおよびコンパイル中に分析しますが、従来の分析ではビルドが完了した後にバイナリ ファイルが分析されます。 詳細については[、「.NET コンパイラ プラットフォーム ベースの分析とレガシ分析の比較](roslyn-analyzers-overview.md#source-code-analysis-versus-legacy-analysis)」および[「FxCop アナライザーに関する FAQ](fxcop-analyzers-faq.md)」を参照してください。

## <a name="treat-warnings-as-errors"></a>警告をエラーとして扱う

**Q**: プロジェクトでは、ビルド オプションを使用して警告をエラーとして扱っています。 レガシ分析からソース コード分析に移行した後、コード分析の警告はすべてエラーとして表示されます。 どうすればそれを防ぐことができますか?

**A**: コード分析の警告がエラーとして扱われないようにするには、次の手順を実行します。

  1. 次の内容の .props ファイルを作成します。

     ```xml
     <Project>
        <PropertyGroup>
           <CodeAnalysisTreatWarningsAsErrors>false</CodeAnalysisTreatWarningsAsErrors>
        </PropertyGroup>
     </Project>
     ```

  2. 前の手順で作成した .props ファイルをインポートするために.csproj または .vbproj プロジェクト ファイルに行を追加します。 この行は、FxCop アナライザー .props ファイルをインポートする行の前に配置する必要があります。 たとえば、.props ファイルの名前が codeanalysis.props の場合は、次のようになります。

     ```xml
     ...
     <Import Project="..\..\codeanalysis.props" Condition="Exists('..\..\codeanalysis.props')" />
     <Import Project="..\packages\Microsoft.CodeAnalysis.FxCopAnalyzers.2.6.5\build\Microsoft.CodeAnalysis.FxCopAnalyzers.props" Condition="Exists('..\packages\Microsoft.CodeAnalysis.FxCopAnalyzers.2.6.5\build\Microsoft.CodeAnalysis.FxCopAnalyzers.props')" />
     ...
     ```

## <a name="code-analysis-solution-property-page"></a>コード分析ソリューションのプロパティ ページ

**Q**: ソリューションのコード分析プロパティ ページはどこにありますか。

**A**: ソリューション レベルのコード分析プロパティ ページが削除され、より信頼性の高い共有プロパティ グループが使用されました。 プロジェクト レベルでコード分析を管理する場合は、[コード分析] プロパティ ページは引き続き使用できます。 (マネージド プロジェクトの場合は、ルール構成用にルールセットから EditorConfig に移行することもお勧めします。 ソリューションまたはレポ内の複数のプロジェクト間でルールセットを共有する場合は、プロパティ グループを定義して、共有の props/targets ファイルまたは Directory.props/Directory.targets ファイルに CodeAnalysisRuleSet プロパティを定義することをお勧めします。 すべてのプロジェクトがインポートするような共通の小道具やターゲットがない場合は、[そのようなプロパティグループを Directory.props に追加するか、最上位のソリューション ディレクトリに Directory.targets](https://docs.microsoft.com/visualstudio/msbuild/customize-your-build?directorybuildprops-and-directorybuildtargets)を追加することを検討してください。

## <a name="see-also"></a>関連項目

- [アナライザーの概要](roslyn-analyzers-overview.md)
- [EditorConfig の .NET コーディング規則の設定](../ide/editorconfig-code-style-settings-reference.md)
