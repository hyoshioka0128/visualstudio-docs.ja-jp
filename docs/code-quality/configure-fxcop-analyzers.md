---
title: Editorconfig を使用した FxCop アナライザーの構成
ms.date: 09/23/2019
ms.topic: conceptual
helpviewer_keywords:
- FxCop analyzers, configuring
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 182042db9a744d037e295a8448f8c49a9c7b3a97
ms.sourcegitcommit: d20ce855461c240ac5eee0fcfe373f166b4a04a9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2020
ms.locfileid: "84184797"
---
# <a name="configure-fxcop-analyzers"></a>FxCop アナライザーの構成

[Fxcop アナライザーパッケージ](install-fxcop-analyzers.md)は、.NET Compiler Platform ベースのコードアナライザーに変換されたレガシ分析から最も重要な "fxcop" 規則で構成されています。 特定の FxCop 規則については、[構成可能なオプション](fxcop-analyzer-options.md)を使用して、コードベースのどの部分を適用するかを調整できます。 各オプションは、キーと値のペアを[Editorconfig](https://editorconfig.org)ファイルに追加することによって指定します。 構成ファイルは、[プロジェクトに固有](#per-project-configuration)のものもあれば、2つ以上のプロジェクト間で[共有](#shared-configuration)することもできます。

> [!TIP]
> **ソリューションエクスプローラー**でプロジェクトを右クリックし、[ **Add**  >  **新しい項目**の追加] を選択して、プロジェクトに editorconfig ファイルを追加します。 [**新しい項目の追加**] ウィンドウで、検索ボックスに「 **editorconfig** 」と入力します。 [ **Editorconfig ファイル (既定)** ] テンプレートを選択し、[**追加**] を選択します。
>
> ![Visual Studio で editorconfig ファイルをプロジェクトに追加する](media/add-editorconfig-file.png)

::: moniker range=">=vs-2019"

規則の重要度の構成 (エラーや警告など) については、「 [EditorConfig ファイルで規則の重要度を設定](use-roslyn-analyzers.md#set-rule-severity-in-an-editorconfig-file)する」を参照してください。 または、組み込みの[Editorconfig ファイルまたはルールセット](analyzer-rule-sets.md)の1つを選択して、ルールのカテゴリをすばやく有効または無効にすることができます。

::: moniker-end

この記事の残りの部分では、FxCop 規則が適用される場所を[調整するオプション](fxcop-analyzer-options.md)の一般的な構文について説明します。

> [!NOTE]
> EditorConfig ファイルを使用して、従来の FxCop 規則を構成することはできません。 レガシ分析と FxCop アナライザーの違いについては、「 [fxcop アナライザー](fxcop-analyzers-faq.md)に関する FAQ」を参照してください。

## <a name="option-scopes"></a>オプションスコープ

各 [調整] オプションは、ルールのカテゴリ (名前付けや設計など)、または特定のルールに対して、すべてのルールに対して構成できます。

### <a name="all-rules"></a>すべてのルール

*すべて*のルールのオプションを構成するための構文は次のとおりです。

|構文|例|
|-|-|
| dotnet_code_quality。OptionName = OptionValue | `dotnet_code_quality.api_surface = public` |

### <a name="category-of-rules"></a>ルールのカテゴリ

ルールの*カテゴリ*(名前付け、設計、パフォーマンスなど) のオプションを構成するための構文は次のとおりです。

|構文|例|
|-|-|
| dotnet_code_quality。RuleCategory OptionName = OptionValue | `dotnet_code_quality.Naming.api_surface = public` |

### <a name="specific-rule"></a>特定のルール

*特定*のルールのオプションを構成するための構文は次のとおりです。

|構文|例|
|-|-|
| dotnet_code_quality。RuleId OptionName = OptionValue | `dotnet_code_quality.CA1040.api_surface = public` |

## <a name="enabling-editorconfig-based-configuration"></a>Editorconfig ベースの構成を有効にする

### <a name="vs2019-163-and-later--fxcopanalyzers-package-version-33x-and-later"></a>VS2019 16.3 以降 + FxCopAnalyzers パッケージバージョン 3.3. x 以降

EditorConfig ベースのアナライザーの構成は、次のスコープに対して有効にすることができます。

- 特定のドキュメント
- 特定のフォルダー
- 特定のプロジェクト
- 特定のソリューション
- リポジトリ全体

構成を有効にするには、対応するディレクトリのオプションを使用して、 *editorconfig*ファイルを追加します。 このファイルには、EditorConfig ベースの診断重大度構成エントリも含まれます。 詳細については、[こちら](use-roslyn-analyzers.md#rule-severity)をご覧ください。

### <a name="prior-to-vs2019-163-or-using-an-fxcopanalyzers-package-version-prior-to-33x"></a>VS2019 16.3 より前、または 3.3. x より前の FxCopAnalyzers パッケージバージョンを使用する

#### <a name="per-project-configuration"></a>プロジェクトごとの構成

特定のプロジェクトに対して EditorConfig ベースのアナライザーの構成を有効にするには、プロジェクトのルートディレクトリに*editorconfig*ファイルを追加します。

#### <a name="shared-configuration"></a>共有構成

FxCop アナライザーの構成ファイルは2つ以上のプロジェクト間で共有できますが、いくつかの追加の手順が必要です。

1. *Editorconfig*ファイルを共通の場所に保存します。

2. 次の内容を含む props ファイルを作成*し*ます。

   ```xml
   <Project DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
     <PropertyGroup>
       <SkipDefaultEditorConfigAsAdditionalFile>true</SkipDefaultEditorConfigAsAdditionalFile>
     </PropertyGroup>
     <ItemGroup Condition="Exists('<your path>\.editorconfig')" >
       <AdditionalFiles Include="<your path>\.editorconfig" />
     </ItemGroup>
   </Project>
   ```

3. *.Csproj*ファイルまたは *.vbproj*ファイルに行を追加して、前の手順で作成した*props*ファイルをインポートします。 この行は、FxCop アナライザーの*props*ファイルをインポートする行の前に配置する必要があります。 たとえば、props ファイルに*editorconfig. props*という名前が付けられているとします。

   ```xml
   ...
   <Import Project="..\..\editorconfig.props" Condition="Exists('..\..\editorconfig.props')" />
   <Import Project="..\packages\Microsoft.CodeAnalysis.FxCopAnalyzers.2.6.3\build\Microsoft.CodeAnalysis.FxCopAnalyzers.props" Condition="Exists('..\packages\Microsoft.CodeAnalysis.FxCopAnalyzers.2.6.3\build\Microsoft.CodeAnalysis.FxCopAnalyzers.props')" />
   ...
   ```

4. プロジェクトを再度読み込みます。

> [!NOTE]
> ここで説明する EditorConfig ファイルの任意の共有の場所は、特定の FxCop analyzer ルールのスコープを構成する場合にのみ適用されます。 [規則の重要度]、[全般エディターの設定]、[コードスタイル] などの他の設定については、EditorConfig ファイルが常にプロジェクトフォルダーまたは親フォルダーに配置されている必要があります。

## <a name="see-also"></a>関連項目

- [FxCop アナライザーの規則のスコープオプション](fxcop-analyzer-options.md)
- [アナライザーの構成](https://github.com/dotnet/roslyn-analyzers/blob/master/docs/Analyzer%20Configuration.md)
- [FXCop アナライザー](install-fxcop-analyzers.md)
- [EditorConfig の .NET コーディング規則](../ide/editorconfig-code-style-settings-reference.md)
