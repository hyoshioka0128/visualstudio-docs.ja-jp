---
title: Analyzer ルールの重要度と抑制
ms.date: 03/04/2020
ms.topic: conceptual
helpviewer_keywords:
- code analysis, managed code
- analyzers
- Roslyn analyzers
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 7e7349717478f18b676b74908da8fb8a6a2fc413
ms.sourcegitcommit: d20ce855461c240ac5eee0fcfe373f166b4a04a9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2020
ms.locfileid: "84184589"
---
# <a name="use-code-analyzers"></a>コードアナライザーを使用する

.NET Compiler Platform ("Roslyn") コードアナライザーは、入力に応じて C# または Visual Basic コードを分析します。 各*診断*または規則には、プロジェクトで上書きできる既定の重大度と抑制状態があります。 この記事では、ルールの重要度の設定、ルールセットの使用、および違反の抑制について説明します。

## <a name="analyzers-in-solution-explorer"></a>ソリューションエクスプローラーのアナライザー

**ソリューションエクスプローラー**から、analyzer 診断のカスタマイズの多くを行うことができます。 アナライザーを NuGet パッケージとして[インストール](../code-quality/install-roslyn-analyzers.md)すると、**ソリューションエクスプローラー**の [**参照**] ノードまたは [**依存関係**] ノードの下に [**アナライザー** ] ノードが表示されます。 [アナライザー] を展開して**から、いずれ**かのアナライザーアセンブリを展開すると、アセンブリ内のすべての診断が表示されます。

![ソリューションエクスプローラーのアナライザーノード](media/analyzers-expanded-in-solution-explorer.png)

[**プロパティ**] ウィンドウでは、診断のプロパティや既定の重要度などを表示できます。 プロパティを表示するには、ルールを右クリックして [**プロパティ**] を選択するか、ルールを選択して、 **Alt**キーを押し + **Enter**ます。

![プロパティウィンドウの診断プロパティ](media/analyzer-diagnostic-properties.png)

診断のオンラインドキュメントを表示するには、診断を右クリックし、[**ヘルプの表示**] を選択します。

**ソリューションエクスプローラー**の各診断の横にあるアイコンは、エディターで開いたときにルールセットに表示されるアイコンに対応します。

- 円の "x" は**エラー**の[重大度](#rule-severity)を示します。
- 三角形の "!" は**警告**の[重大度](#rule-severity)を示します。
- 円の "i" は**情報**の[重大度](#rule-severity)を示します。
- 明るい色の背景にある円の "i" は、**非表示**の[重要度](#rule-severity)を示します。
- 円の下向き矢印は、診断が抑制されていることを示します。

![ソリューションエクスプローラーの診断アイコン](media/diagnostics-icons-solution-explorer.png)

## <a name="rule-severity"></a>ルールの重要度

::: moniker range=">=vs-2019"

アナライザーを NuGet パッケージとして[インストール](../code-quality/install-roslyn-analyzers.md)した場合は、analyzer ルールまたは*診断*の重大度を構成できます。 Visual Studio 2019 バージョン16.3 以降では、 [EditorConfig ファイルで](#set-rule-severity-in-an-editorconfig-file)ルールの重要度を構成できます。 また、ソリューションエクスプローラーまたは[ルールセットファイル](#set-rule-severity-in-the-rule-set-file)[から](#set-rule-severity-from-solution-explorer)、ルールの重要度を変更することもできます。

::: moniker-end

::: moniker range="vs-2017"

アナライザーを NuGet パッケージとして[インストール](../code-quality/install-roslyn-analyzers.md)した場合は、analyzer ルールまたは*診断*の重大度を構成できます。 ルールの重要度は、ソリューションエクスプローラーまたは[ルールセットファイルの中](#set-rule-severity-in-the-rule-set-file)[から](#set-rule-severity-from-solution-explorer)変更できます。

::: moniker-end

次の表は、さまざまな重大度オプションを示しています。

| 重要度 (ソリューションエクスプローラー) | 重大度 (EditorConfig ファイル) | ビルド時の動作 | エディターの動作 |
|-|-|-|
| Error | `error` | エラー一覧とコマンドラインのビルド出力で、違反が*エラー*として表示され、ビルドが失敗します。| 問題のあるコードは、赤い波線で下線が引かれ、スクロールバーの小さな赤いボックスで示されます。 |
| 警告 | `warning` | エラー一覧とコマンドラインのビルド出力では、違反は*警告*として表示されますが、ビルドが失敗することはありません。 | 問題のあるコードは、緑の波線で下線が引かれ、スクロールバーの小さな緑色のボックスで示されます。 |
| Info | `suggestion` | 違反は、コマンドラインのビルド出力ではなく、エラー一覧に*メッセージ*として表示されます。 | 問題のあるコードは、灰色の波線で下線が引かれ、スクロールバーの小さい灰色のボックスでマークされます。 |
| [非表示] | `silent` | ユーザーに表示されません。 | ユーザーに表示されません。 ただし、診断は IDE 診断エンジンに報告されます。 |
| None | `none` | 完全に抑制されます。 | 完全に抑制されます。 |
| Default | `default` | ルールの既定の重要度に対応します。 ルールの既定値を確認するには、プロパティウィンドウを調べます。 | ルールの既定の重要度に対応します。 |

次のコードエディターのスクリーンショットは、重大度が異なる3種類の違反を示しています。 波線の色と、右側のスクロールバーの小さな色付きの正方形に注目してください。

![コードエディターのエラー、警告、および情報の違反](media/diagnostics-severity-colors.png)

次のスクリーンショットは、エラー一覧に表示されるのと同じ3つの違反を示しています。

![エラー一覧のエラー、警告、および情報の違反](media/diagnostics-severities-in-error-list.png)

::: moniker range=">=vs-2019"

### <a name="set-rule-severity-in-an-editorconfig-file"></a>EditorConfig ファイルで規則の重要度を設定する

(Visual Studio 2019 バージョン16.3 以降)

次の構文を使用して、EditorConfig ファイルでコンパイラの警告またはアナライザーの規則の重要度を設定できます。

`dotnet_diagnostic.<rule ID>.severity = <severity>`

EditorConfig ファイルでのルールの重要度の設定は、ルールセットまたはソリューションエクスプローラーで設定されている重要度よりも優先されます。 EditorConfig ファイルで重大度を[手動で](#manually-configure-rule-severity)構成することも、違反の隣に表示される電球を介して[自動的に](#automatically-configure-rule-severity)構成することもできます。

### <a name="set-rule-severity-of-multiple-analyzer-rules-at-once-in-an-editorconfig-file"></a>EditorConfig ファイルで一度に複数のアナライザールールのルールの重要度を設定する

(Visual Studio 2019 バージョン16.5 以降)

アナライザーの規則の特定のカテゴリの重要度を設定することも、EditorConfig ファイル内の1つのエントリを含むすべてのアナライザー規則に対して重大度を設定することもできます。

- アナライザールールのカテゴリのルールの重要度を設定します。

`dotnet_analyzer_diagnostic.category-<rule category>.severity = <severity>`

- すべてのアナライザールールのルールの重要度を設定します:

`dotnet_analyzer_diagnostic.severity = <severity>`

特定の規則 ID に適用できるエントリが複数ある場合、該当するエントリを選択するための優先順位は次のとおりです。

- ID による個々のルールの重大度エントリは、カテゴリの重要度エントリよりも優先されます。
- カテゴリの重大度エントリは、すべてのアナライザールールの重大度エントリよりも優先されます。

次の EditorConfig の例を考えてみます。 [CA1822](https://docs.microsoft.com/visualstudio/code-quality/ca1822)には "Performance" というカテゴリがあります。

   ```ini
   [*.cs]
   dotnet_diagnostic.CA1822.severity = error
   dotnet_analyzer_diagnostic.category-performance.severity = warning
   dotnet_analyzer_diagnostic.severity = suggestion
   ```

前の例では、3つのエントリすべてが CA1822 に適用されます。 ただし、指定した優先順位規則を使用すると、最初の規則 ID ベースの重要度エントリが次のエントリに優先されます。 この例では、CA1822 の有効度が "error" になります。 "パフォーマンス" カテゴリの残りのすべてのルールの重大度は "warning" になります。 "Performance" カテゴリのないすべての analyzer ルールには、重要度 "提案" があります。

#### <a name="manually-configure-rule-severity"></a>規則の重要度を手動で構成する

1. プロジェクトの EditorConfig ファイルがまだない場合は、プロジェクトを[追加](../ide/create-portable-custom-editor-options.md#add-an-editorconfig-file-to-a-project)します。

2. 対応するファイル拡張子の下で、構成する各ルールのエントリを追加します。 たとえば、 [CA1822](ca1822.md)の重大度を C# ファイルに対して設定する場合、エントリは次のように `error` なります。

   ```ini
   [*.cs]
   dotnet_diagnostic.CA1822.severity = error
   ```

> [!NOTE]
> IDE コードスタイルのアナライザーの場合は、別の構文を使用して、EditorConfig ファイルで構成することもできます (例:) `dotnet_style_qualification_for_field = false:suggestion` 。 ただし、構文を使用して重要度を設定した場合は、 `dotnet_diagnostic` それが優先されます。 詳細については、「 [EditorConfig の言語規則](../ide/editorconfig-language-conventions.md)」を参照してください。

#### <a name="convert-an-existing-ruleset-file-to-editorconfig-file"></a>既存のルールセットファイルを EditorConfig ファイルに変換する

Visual Studio 2019 バージョン16.5 以降では、マネージコードのアナライザー構成の EditorConfig ファイルを優先して、ルールセットファイルが非推奨とされます。 Visual Studio ツールの analyzer ルールの重要度の構成のほとんどは、ルールセットファイルではなく EditorConfig ファイルで動作するように更新されています。 EditorConfig ファイルを使用すると、Visual Studio IDE のコードスタイルオプションを含む、アナライザーの規則の重大度とアナライザーのオプションの両方を構成できます。 既存のルールセットファイルを EditorConfig ファイルに変換することを強くお勧めします。 また、EditorConfig ファイルは、リポジトリのルートまたはソリューションフォルダーに保存することをお勧めします。 リポジトリまたはソリューションフォルダーのルートを使用して、このファイルからの重要度設定が、それぞれリポジトリまたはソリューション全体に自動的に適用されるようにします。

既存のルールセットファイルを EditorConfig ファイルに変換するには、いくつかの方法があります。

- Visual Studio のルールセットエディターから (Visual Studio 2019 16.5 以降が必要)。 プロジェクトが特定のルールセットファイルをとして既に使用している場合は `CodeAnalysisRuleSet` 、Visual Studio 内のルールセットエディターから同等の EditorConfig ファイルに変換できます。

    1. ソリューションエクスプローラーで、ルールセットファイルをダブルクリックします。

       ルールセットエディターでルールセットファイルが開きます。 ルールセットエディターの上部にクリック可能な**情報バー**が表示されます。

       ![ルールセットエディターでルールセットを EditorConfig ファイルに変換する](media/convert-ruleset-to-editorconfig-file-ruleset-editor.png)

    2. **[** 情報バー] リンクをクリックします。

       これにより、[**名前を付けて保存**] ダイアログボックスが開き、editorconfig ファイルを生成するディレクトリを選択できます。

    3. **[** **保存**] ボタンをクリックして、editorconfig ファイルを生成します。

       生成された EditorConfig はエディターで開く必要があります。 また、MSBuild プロパティは、 `CodeAnalysisRuleSet` 元のルールセットファイルを参照しないように、プロジェクトファイルで更新されます。

- コマンドラインから:

    1. NuGet パッケージの[Microsoft CodeAnalysis. RulesetToEditorconfigConverter](https://www.nuget.org/packages/Microsoft.CodeAnalysis.RulesetToEditorconfigConverter)をインストールします。

    2. `RulesetToEditorconfigConverter.exe`インストールされているパッケージから、ルールセットファイルと EditorConfig ファイルへのパスをコマンドライン引数として実行します。

   ```
   Usage: RulesetToEditorconfigConverter.exe <%ruleset_file%> [<%path_to_editorconfig%>]
   ```

変換するルールセットファイルの例を次に示します。

```xml
<?xml version="1.0" encoding="utf-8"?>
<RuleSet Name="Rules for ConsoleApp" Description="Code analysis rules for ConsoleApp.csproj." ToolsVersion="16.0">
  <Rules AnalyzerId="Microsoft.Analyzers.ManagedCodeAnalysis" RuleNamespace="Microsoft.Rules.Managed">
    <Rule Id="CA1001" Action="Warning" />
    <Rule Id="CA1821" Action="Warning" />
    <Rule Id="CA2213" Action="Warning" />
    <Rule Id="CA2231" Action="Warning" />
  </Rules>
</RuleSet>
```

変換された EditorConfig ファイルを次に示します。

```ini
# NOTE: Requires **VS2019 16.3** or later

# Rules for ConsoleApp
# Description: Code analysis rules for ConsoleApp.csproj.

# Code files
[*.{cs,vb}]


dotnet_diagnostic.CA1001.severity = warning

dotnet_diagnostic.CA1821.severity = warning

dotnet_diagnostic.CA2213.severity = warning

dotnet_diagnostic.CA2231.severity = warning
```

#### <a name="automatically-configure-rule-severity"></a>規則の重要度を自動的に構成する

##### <a name="configure-from-light-bulb-menu"></a>電球メニューから構成する

Visual Studio には、[クイックアクション](../ide/quick-actions.md)の電球メニューからルールの重要度を構成する便利な方法が用意されています。

1. 違反が発生した後、エディターで違反波線をポイントし、電球メニューを開きます。 または、行にカーソルを置き、 **ctrl**キーを押し + **ます。** (ピリオド) を押します。

2. 電球メニューの [問題の構成]**または**[ > ** \<rule ID> 重要度の構成**] を選択します。

   ![Visual Studio の電球メニューからルールの重要度を構成する](media/configure-rule-severity.png)

3. そこから、重大度オプションの1つを選択します。

   ![規則の重要度を提案として構成する](media/configure-rule-severity-suggestion.png)

   Visual Studio によって EditorConfig ファイルにエントリが追加され、[プレビュー] ボックスに示されているように、要求されたレベルに規則が構成されます。

   > [!TIP]
   > プロジェクトに EditorConfig ファイルがまだない場合は、Visual Studio によって作成されます。

##### <a name="configure-from-error-list"></a>[エラー一覧から構成する]

また、Visual Studio では、[エラー一覧] コンテキストメニューからルールの重要度を構成する便利な方法も提供されています。

1. 違反が発生した後、[エラー一覧] の診断エントリを右クリックします。

2. コンテキストメニューから、[**重大度の設定**] を選択します。

   ![Visual Studio の [エラー一覧] から規則の重要度を構成する](media/configure-rule-severity-error-list.png)

3. そこから、重大度オプションの1つを選択します。

   Visual Studio は、EditorConfig ファイルにエントリを追加して、要求されたレベルに規則を構成します。

   > [!TIP]
   > プロジェクトに EditorConfig ファイルがまだない場合は、Visual Studio によって作成されます。

::: moniker-end

### <a name="set-rule-severity-from-solution-explorer"></a>ルールの重要度をソリューションエクスプローラーから設定

1. ソリューションエクスプローラーで、[**参照**  >  **アナライザー** ] (または .net Core プロジェクトの**依存関係**  >  **アナライザー** ) を展開します。

2. 重要度を設定するルールが含まれているアセンブリを展開します。

::: moniker range=">=vs-2019"
3. ルールを右クリックし、[**重要度の設定**] を選択します。 コンテキストメニューで、重大度オプションの1つを選択します。

   Visual Studio は、EditorConfig ファイルにエントリを追加して、要求されたレベルに規則を構成します。 プロジェクトで EditorConfig ファイルではなくルールセットファイルを使用すると、重大度エントリがルールセットファイルに追加されます。

   > [!TIP]
   > プロジェクトに EditorConfig ファイルまたはルールセットファイルがまだない場合は、Visual Studio によって新しい EditorConfig ファイルが作成されます。
::: moniker-end

::: moniker range="vs-2017"
3. ルールを右クリックし、[**ルールセットの重要度の設定**] を選択します。 コンテキストメニューで、重大度オプションの1つを選択します。

   ルールの重要度は、アクティブなルールセットファイルに保存されます。
::: moniker-end

### <a name="set-rule-severity-in-the-rule-set-file"></a>規則セットファイルで規則の重要度を設定する

![ソリューションエクスプローラーの規則セットファイル](media/ruleset-in-solution-explorer.png)

1. アクティブなルールセットファイルを開くには、**ソリューションエクスプローラー**でダブルクリックし、[**参照**アナライザー] ノードの右クリックメニューで [**アクティブなルールセットを開く**] を選択するか、  >  **Analyzers**プロジェクトの [**コード分析**] プロパティページで [**開く**] を選択します。

   規則セットを初めて編集する場合は、Visual Studio によって既定の規則セットファイルのコピーが作成され、ルールセット* \<projectname> という名前*が付いて、プロジェクトに追加されます。 このカスタム規則セットは、プロジェクトのアクティブな規則セットにもなります。

   > [!NOTE]
   > .NET Core と .NET Standard のプロジェクトでは、[**アクティブな規則セットを開く**] など、**ソリューションエクスプローラー**の規則セットのメニューコマンドはサポートされていません。 .NET Core または .NET Standard プロジェクトに対して既定以外の規則セットを指定するには、 [ **CodeAnalysisRuleSet**プロパティ](using-rule-sets-to-group-code-analysis-rules.md#specify-a-rule-set-for-a-project)をプロジェクトファイルに手動で追加します。 ただし、Visual Studio の規則セットエディター UI で規則セット内の規則を構成することはできます。

1. コンテナーのアセンブリを展開して、規則を参照します。

1. [**アクション**] 列で、値を選択してドロップダウンリストを開き、一覧から目的の重要度を選択します。

   ![エディターでルールセットファイルを開く](media/ruleset-file-in-editor.png)

::: moniker range=">=vs-2019"

## <a name="configure-generated-code"></a>生成されたコードの構成

アナライザーは、プロジェクト内のすべてのソースファイルで実行され、違反を報告します。 ただし、これらの違反は、生成されたコードファイル (デザイナーで生成されたコードファイル、ビルドシステムによって生成された一時ソースファイルなど) では役に立ちません。ユーザーはこれらのファイルを手動で編集することはできません。また、これらの種類のツールで生成されたファイルの違反を修正することもありません。

既定では、アナライザーを実行するアナライザードライバーは、特定の名前、ファイル拡張子、または自動生成されたファイルヘッダーを持つファイルを生成コードファイルとして扱います。 たとえば、またはで終わるファイル名 `.designer.cs` `.generated.cs` は、生成されたコードと見なされます。 ただし、これらのヒューリスティックは、ユーザーのソースコード内のカスタム生成コードファイルをすべて特定できない可能性があります。

Visual Studio 2019 16.5 以降では、エンドユーザーは、 [Editorconfig ファイル](https://editorconfig.org/)で、生成されたコードとして扱う特定のファイルやフォルダーを構成できます。 このような構成を追加するには、次の手順に従います。

1. プロジェクトの EditorConfig ファイルがまだない場合は、プロジェクトを[追加](../ide/create-portable-custom-editor-options.md#add-an-editorconfig-file-to-a-project)します。

2. 特定の `generated_code = true | false` ファイルやフォルダーのエントリを追加します。 たとえば、名前がで終わるすべてのファイルを、 `.MyGenerated.cs` 生成されたコードとして扱う場合、エントリは次のようになります。

   ```ini
   [*.MyGenerated.cs]
   generated_code = true
   ```

::: moniker-end

## <a name="suppress-violations"></a>違反を抑制する

規則違反を抑制する方法は複数あります。

::: moniker range=">=vs-2019"

- **Editorconfig ファイル**内

  重要度をに設定し `none` ます。たとえば、のように `dotnet_diagnostic.CA1822.severity = none` します。

- [**分析**] メニューから

  **Analyze**  >  現在のすべての違反を抑制するには、メニューバーの [ビルドの分析]**と [アクティブな問題の非**表示] を選択します。 これは、"基準" と呼ばれることもあります。

::: moniker-end

::: moniker range="vs-2017"

- [**分析**] メニューから

  **Analyze**  >  現在のすべての違反を抑制するには、メニューバーの [**実行コード分析を分析し、アクティブな問題を抑制**する] を選択します。 これは、"基準" と呼ばれることもあります。

::: moniker-end

- **ソリューションエクスプローラー**から

  規則の重要度を **[なし**] に設定します。

- **規則セットエディター**から

  名前の横にあるボックスをオフにするか、[**アクション**] を **[なし**] に設定します。

- **コードエディター**から

  違反があるコード行にカーソルを置き、 **Ctrl** + **Period (.)** キーを押して [**クイックアクション**] メニューを開きます。 [ **Suppress CAXXXX**  >  **ソース/抑制ファイル**での caxxxx の抑制] を選択します。

  ![クイックアクションメニューの診断を抑制する](media/suppress-diagnostic-from-editor.png)

- **エラー一覧**から

  抑制するルールを選択し、右クリックして、[ **Suppress**  >  **ソース/抑制ファイルで**抑制する] を選択します。

  - **ソースで**非表示にすると、[**変更のプレビュー** ] ダイアログが開き、ソースコードに追加された C# [#pragma warning](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-pragma-warning)または Visual Basic [#Disable warning](/dotnet/visual-basic/language-reference/directives/directives)ディレクティブのプレビューが表示されます。

    ![コードファイルでの #pragma 警告の追加のプレビュー](media/pragma-warning-preview.png)

  - [**抑制ファイル内**] を選択すると、[**変更のプレビュー** ] ダイアログが開き、 <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> グローバル抑制ファイルに追加された属性のプレビューが表示されます。

    ![抑制ファイルへの SuppressMessage 属性の追加のプレビュー](media/preview-changes-in-suppression-file.png)

  [**変更のプレビュー** ] ダイアログで、[**適用**] を選択します。

  > [!NOTE]
  > **ソリューションエクスプローラー**に [**抑制**] メニューオプションが表示されない場合、違反はビルドから発生し、ライブ分析は行われない可能性があります。 **エラー一覧**には、ライブコード分析とビルドの両方からの診断または規則違反が表示されます。 ビルド診断は古くなる可能性があるため、たとえば、違反を修正するようにコードを編集してもリビルドされていない場合は、**エラー一覧**からこれらの診断を抑制することはできません。 ライブ分析または IntelliSense からの診断は、常に最新のソースを使用して最新の状態にあり、**エラー一覧**によって抑制できます。 選択した*ビルド*診断を除外するには、**エラー一覧**ソースフィルターを [ビルド] + [ **Intellisense** ] から [ **intellisense のみ**] に切り替えます。 次に、非表示にする診断を選択し、前述のように続行します。
  >
  > ![Visual Studio でのエラー一覧ソースフィルター](media/error-list-filter.png)

## <a name="command-line-usage"></a>コマンドラインの使用方法

コマンドラインでプロジェクトをビルドすると、次の条件が満たされた場合に、規則違反がビルド出力に表示されます。

- アナライザーは、VSIX 拡張機能としてではなく、NuGet パッケージとしてインストールされます。

- プロジェクトのコードで1つ以上の規則に違反しています。

- 違反しているルールの[重要度](#rule-severity)は、いずれかの**警告**に設定されます。この場合、違反が発生してもビルドは失敗しません。**エラー**の場合は、違反が発生してもビルドは失敗します。

ビルド出力の詳細度は、規則違反が表示されるかどうかには影響しません。 **低**レベルの詳細度でも、ルール違反はビルド出力に表示されます。

> [!TIP]
> *FxCopCmd* 、または**runcodeanalysis**フラグを使用した msbuild を使用してコマンドラインからレガシ分析を実行することに慣れている場合は、コードアナライザーを使用してこれを行う方法を次に示します。

Msbuild を使用してプロジェクトをビルドするときに、コマンドラインでアナライザーの違反を確認するには、次のようなコマンドを実行します。

```cmd
msbuild myproject.csproj /target:rebuild /verbosity:minimal
```

次のイメージは、アナライザー ルール違反を含むプロジェクトのビルドからのコマンドライン ビルド出力を示しています。

![ルール違反を示す MSBuild 出力](media/command-line-build-analyzers.png)

## <a name="dependent-projects"></a>依存プロジェクト

.NET Core プロジェクトでは、NuGet アナライザーを含むプロジェクトへの参照を追加すると、それらのアナライザーも依存プロジェクトに自動的に追加されます。 この動作を無効にするには、たとえば、依存プロジェクトが単体テストプロジェクトの場合、 **Privateassets**属性を設定して、参照されるプロジェクトの *.csproj*ファイルまたは *.vbproj*ファイルで NuGet パッケージを private としてマークします。

```xml
<PackageReference Include="Microsoft.CodeAnalysis.FxCopAnalyzers" Version="2.9.0" PrivateAssets="all" />
```

## <a name="see-also"></a>関連項目

- [Visual Studio のコードアナライザーの概要](../code-quality/roslyn-analyzers-overview.md)
- [コードアナライザーのバグを送信する](https://github.com/dotnet/roslyn-analyzers/issues)
- [規則セットを使用する](../code-quality/using-rule-sets-to-group-code-analysis-rules.md)
- [コード分析の警告を表示しない](../code-quality/in-source-suppression-overview.md)
