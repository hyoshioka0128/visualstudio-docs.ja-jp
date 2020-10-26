---
title: EditorConfig とアナライザー
ms.date: 03/11/2019
ms.topic: conceptual
helpviewer_keywords:
- analyzers, faq
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9408e8615e2a3591a5e93f569546b6161fe40e4c
ms.sourcegitcommit: 4ae5e9817ad13edd05425febb322b5be6d3c3425
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2020
ms.locfileid: "90037251"
---
# <a name="code-analysis-faq"></a>コード分析に関する FAQ

このページには、Visual Studio での .NET Compiler Platform ベースのコード分析に関してよく寄せられる質問への回答が含まれています。

## <a name="code-analysis-versus-editorconfig"></a>コード分析と EditorConfig

**Q**: コードのスタイルを確認するためにコード分析または editorconfig を使用する必要がありますか。

**A**: コード分析と editorconfig ファイルは手動で機能します。 [EditorConfig ファイル](../ide/editorconfig-code-style-settings-reference.md)または [[テキストエディター] オプション](../ide/code-styles-and-code-cleanup.md)ページでコードスタイルを定義する場合、実際には Visual Studio に組み込まれているコードアナライザーを構成します。 EditorConfig ファイルを使用すると、アナライザーの規則を有効または無効にすることができます。また、NuGet アナライザーパッケージを構成することもできます。

## <a name="editorconfig-versus-rule-sets"></a>EditorConfig とルールセット

**Q**: 規則セットまたは editorconfig ファイルを使用してアナライザーを構成する必要がありますか。

**A**: 規則セットと editorconfig ファイルは共存させることができ、どちらもアナライザーの構成に使用できます。 EditorConfig ファイルとルールセットの両方を使用して、ルールを有効または無効にしたり、その重要度を設定したりできます。

ただし、EditorConfig ファイルでは、ルールを構成するための追加の方法が提供されるようになります。

- .NET コード品質アナライザーでは、EditorConfig ファイルを使用して、 [分析するコードの種類を定義](fxcop-analyzer-options.md)できます。
- Visual Studio に組み込まれている .NET コードスタイルアナライザーの場合、EditorConfig ファイルを使用すると、コードベースに [適したコードスタイルを定義](../ide/editorconfig-code-style-settings-reference.md) できます。

規則セットと EditorConfig ファイルに加えて、一部のアナライザーは、C# および VB コンパイラの [追加ファイル](../ide/build-actions.md#build-action-values) としてマークされたテキストファイルを使用して構成されます。

> [!NOTE]
> - EditorConfig ファイルは、Visual Studio 2019 バージョン16.3 以降でルールを有効にし、重要度を設定するためにのみ使用できます。
> - EditorConfig ファイルを使用してレガシ分析を構成することはできませんが、ルールセットはできます。

## <a name="code-analysis-in-ci-builds"></a>CI ビルドでのコード分析

**Q**: 継続的インテグレーション (CI) ビルドでは、.NET Compiler Platform ベースのコード分析は機能しますか。

**A**: はい。 NuGet パッケージからインストールされたアナライザーでは、これらの規則は [ビルド時に適用](roslyn-analyzers-overview.md#build-errors)されます。これには、CI ビルドの実行中も含まれます。 CI ビルドで使用されるアナライザーは、規則セットと EditorConfig ファイルの両方からの規則の構成を尊重します。 現時点では、Visual Studio に組み込まれているコードアナライザーは NuGet パッケージとして使用できないため、これらの規則は CI ビルドでは適用できません。

## <a name="ide-analyzers-versus-stylecop"></a>IDE アナライザーと StyleCop

**Q**: VISUAL Studio IDE のコードアナライザーと StyleCop アナライザーの違いは何ですか。

**A**: VISUAL Studio IDE には、コードスタイルと品質の問題の両方を検索する組み込みアナライザーが含まれています。 これらの規則は、新しく導入された言語機能を使用して、コードの保守性を向上させるのに役立ちます。 IDE アナライザーは、Visual Studio のリリースごとに継続的に更新されます。

[StyleCop アナライザー](https://github.com/DotNetAnalyzers/StyleCopAnalyzers) は、コード内のスタイルの一貫性をチェックする NuGet パッケージとしてインストールされたサードパーティのアナライザーです。 一般に、StyleCop の規則を使用すると、コードベースに対して個人設定を設定できます。

## <a name="code-analyzers-versus-legacy-analysis"></a>コードアナライザーと従来の分析

**Q**: 従来の分析と .NET Compiler Platform ベースのコード分析の違いは何ですか。

**A**: .NET Compiler Platform ベースのコード分析では、ソースコードがリアルタイムで分析され、コンパイル中に分析されます。一方、レガシ分析では、ビルドの完了後にバイナリファイルが分析されます。 詳細については、「 [.NET Compiler Platform ベースの分析とレガシ分析](../code-quality/fxcop-analyzers-faq.md#whats-the-difference-between-legacy-fxcop-and-fxcop-analyzers)」を参照してください。

## <a name="treat-warnings-as-errors"></a>警告をエラーとして扱う

**Q**: プロジェクトでは、ビルドオプションを使用して警告をエラーとして扱います。 レガシ分析からソースコード分析に移行した後、すべてのコード分析警告がエラーとして表示されるようになりました。 これを回避するにはどうすればよいですか。

**A**: コード分析の警告がエラーとして扱われないようにするには、次の手順を実行します。

  1. 次の内容を含む props ファイルを作成します。

     ```xml
     <Project>
        <PropertyGroup>
           <CodeAnalysisTreatWarningsAsErrors>false</CodeAnalysisTreatWarningsAsErrors>
        </PropertyGroup>
     </Project>
     ```

  2. .Csproj または .vbproj プロジェクトファイルに行を追加して、前の手順で作成した props ファイルをインポートします。 この行は、FxCop アナライザーの props ファイルをインポートする行の前に配置する必要があります。 たとえば、props ファイルの名前が codeanalysis. props:

     ```xml
     ...
     <Import Project="..\..\codeanalysis.props" Condition="Exists('..\..\codeanalysis.props')" />
     <Import Project="..\packages\Microsoft.CodeAnalysis.FxCopAnalyzers.2.6.5\build\Microsoft.CodeAnalysis.FxCopAnalyzers.props" Condition="Exists('..\packages\Microsoft.CodeAnalysis.FxCopAnalyzers.2.6.5\build\Microsoft.CodeAnalysis.FxCopAnalyzers.props')" />
     ...
     ```

## <a name="code-analysis-solution-property-page"></a>コード分析ソリューションプロパティページ

**Q**: ソリューションのコード分析プロパティページはどこにありますか。

**A**: ソリューションレベルの [コード分析] プロパティページは、より信頼性の高い共有プロパティグループを優先するように削除されました。 プロジェクトレベルでコード分析を管理する場合、[コード分析] プロパティページは引き続き使用できます。 (マネージプロジェクトの場合は、ルールの構成に対して、ルールセットから EditorConfig への移行もお勧めします)。 ソリューションまたはリポジトリ内の複数のプロジェクト間でルールセットを共有するには、CodeAnalysisRuleSet プロパティを使用して、プロパティグループを共有 props/targets ファイルまたはディレクトリに定義することをお勧めします。 すべてのプロジェクトがインポートする一般的な props やターゲットがない場合は、その [ようなプロパティグループを最上位レベルのソリューションディレクトリに追加することを検討してください。このディレクトリは、ディレクトリまたはサブディレクトリで定義されているすべてのプロジェクトファイルに自動的にインポートされ](../msbuild/customize-your-build.md)ます。

## <a name="see-also"></a>参照

- [アナライザーの概要](roslyn-analyzers-overview.md)
- [EditorConfig の .NET コーディング規則の設定](../ide/editorconfig-code-style-settings-reference.md)