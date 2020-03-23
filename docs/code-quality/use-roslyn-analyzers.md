---
title: アナライザー ルールの重大度と抑制
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
ms.openlocfilehash: 67fd157ad4db24acbc1676ea0a9a1d79e9eb34f9
ms.sourcegitcommit: 92361aac3665a934faa081e1d1ea89a067b01c5b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/17/2020
ms.locfileid: "79431411"
---
# <a name="use-code-analyzers"></a>コード アナライザーを使用する

.NET コンパイラ プラットフォーム ("Roslyn") コード アナライザーは、入力時に C# または Visual Basic コードを分析します。 各*診断*またはルールには、プロジェクトに対して上書きできる既定の重大度と抑制状態があります。 この記事では、ルールの重大度の設定、ルール セットの使用、および違反の抑制について説明します。

## <a name="analyzers-in-solution-explorer"></a>ソリューション エクスプローラーのアナライザー

アナライザー診断のカスタマイズの多くは、**ソリューション エクスプローラ**から実行できます。 [アナライザーを](../code-quality/install-roslyn-analyzers.md)NuGet パッケージとしてインストールすると、**ソリューション エクスプローラー**の **[参照**] ノードまたは [**依存関係**] ノードの下に **[アナライザー]** ノードが表示されます。 **[Analyzers]** を展開し、いずれかのアナライザ アセンブリを展開すると、アセンブリ内のすべての診断が表示されます。

![ソリューション エクスプローラーの [アナライザー] ノード](media/analyzers-expanded-in-solution-explorer.png)

診断のプロパティ (説明や既定の重要度など) は、[**プロパティ]** ウィンドウに表示できます。 プロパティを表示するには、ルールを右クリックして **[プロパティ]** を選択するか、ルールを選択して**Alt キーを**+**Enter**押します。

![[プロパティ] ウィンドウの診断プロパティ](media/analyzer-diagnostic-properties.png)

診断のオンライン ドキュメントを表示するには、診断を右クリックし、[**ヘルプの表示**] を選択します。

**ソリューション エクスプローラー**で各診断の横にあるアイコンは、エディターで開いたときにルール セットに表示されるアイコンに対応します。

- 円の中の "x" は[、重大度](#rule-severity)が **[エラー** ] であることを示します
- 三角形の "!"は **、警告**の[重大度](#rule-severity)を示します
- 円の中の "i" は[、重大度](#rule-severity)が **[情報**] であることを示します
- 明るい色の背景上の円の中の「i」は **、隠された**[重大度](#rule-severity)を示します
- 円の下向き矢印は診断が抑制されていることを示します

![ソリューション エクスプローラーの診断アイコン](media/diagnostics-icons-solution-explorer.png)

## <a name="rule-severity"></a>ルールの重要度

::: moniker range=">=vs-2019"

アナライザーを NuGet パッケージとしてインストールする場合は、[アナライザー](../code-quality/install-roslyn-analyzers.md)ルールまたは*診断*の重大度を構成できます。 Visual Studio 2019 バージョン 16.3 以降では[、EditorConfig ファイルで](#set-rule-severity-in-an-editorconfig-file)ルールの重大度を構成できます。 また、[ソリューション エクスプローラ](#set-rule-severity-from-solution-explorer)またはルール セット ファイル[からルールの](#set-rule-severity-in-the-rule-set-file)重要度を変更することもできます。

::: moniker-end

::: moniker range="vs-2017"

アナライザーを NuGet パッケージとしてインストールする場合は、[アナライザー](../code-quality/install-roslyn-analyzers.md)ルールまたは*診断*の重大度を構成できます。 ルールの重大度は、ソリューション[エクスプローラ](#set-rule-severity-from-solution-explorer)または ルール[セット ファイル から](#set-rule-severity-in-the-rule-set-file)変更できます。

::: moniker-end

次の表に、さまざまな重大度オプションを示します。

| 重大度 (ソリューション エクスプローラー) | 重大度 (エディター構成ファイル) | ビルド時の動作 | エディタの動作 |
|-|-|-|
| エラー | `error` | 違反は *、エラー*一覧とコマンド ライン ビルド出力でエラーとして表示され、ビルドが失敗します。| 問題のあるコードには赤い波線が引かけられ、スクロールバーに小さな赤いボックスが表示されます。 |
| 警告 | `warning` | 違反は、エラー一覧とコマンド ライン ビルド出力で*警告*として表示されますが、ビルドが失敗する原因とはなりません。 | 問題のあるコードには緑色の波線が付き、スクロールバーに小さな緑色のボックスが表示されます。 |
| Info | `suggestion` | 違反はエラー一覧に*メッセージ*として表示され、コマンド ライン ビルド出力では表示されません。 | 問題のあるコードには灰色の波線が付き、スクロールバーに小さな灰色のボックスが表示されます。 |
| [非表示] | `silent` | ユーザーに対しては表示されません。 | ユーザーに対しては表示されません。 ただし、診断は IDE 診断エンジンに報告されます。 |
| なし | `none` | 完全に抑制されます。 | 完全に抑制されます。 |
| Default | `default` | ルールの既定の重要度に対応します。 ルールの既定値を確認するには、[プロパティ] ウィンドウを確認します。 | ルールの既定の重要度に対応します。 |

コード エディターの次のスクリーン ショットは、異なる複数の大台に対する 3 つの異なる違反を示しています。 波線の色と、右側のスクロール バーの小さな色の正方形に注目してください。

![コード エディターでのエラー、警告、および情報違反](media/diagnostics-severity-colors.png)

次のスクリーンショットは、エラー一覧に表示されるのと同じ 3 つの違反を示しています。

![エラー一覧のエラー、警告、および情報違反](media/diagnostics-severities-in-error-list.png)

::: moniker range=">=vs-2019"

### <a name="set-rule-severity-in-an-editorconfig-file"></a>エディタ構成ファイルでルールの重大度を設定する

(Visual Studio 2019 バージョン 16.3 以降)

次の構文を使用して、EditorConfig ファイルでコンパイラ警告またはアナライザールールの重大度を設定できます。

`dotnet_diagnostic.<rule ID>.severity = <severity>`

EditorConfig ファイルでのルールの重大度の設定は、ルール セットまたはソリューション エクスプローラーで設定されている重大度よりも優先されます。 重大度は[、EditorConfig](#manually-configure-rule-severity)ファイルで手動で構成することも、違反の横に表示される電球を[使用して自動的](#automatically-configure-rule-severity)に構成することもできます。

### <a name="set-rule-severity-of-multiple-analyzer-rules-at-once-in-an-editorconfig-file"></a>エディタ構成ファイルで複数のアナライザールールのルール重大度を一度に設定する

(Visual Studio 2019 バージョン 16.5 以降)

特定のカテゴリのアナライザー ルールに対して、または EditorConfig ファイル内の単一のエントリを持つすべてのアナライザー ルールに対して、重大度を設定できます。

- アナライザー ルールのカテゴリにルールの重大度を設定します。

`dotnet_analyzer_diagnostic.category-<rule category>.severity = <severity>`

- すべてのアナライザー ルールにルールの重大度を設定します。

`dotnet_analyzer_diagnostic.severity = <severity>`

特定のルール ID に適用可能な複数のエントリがある場合、該当するエントリを選択する優先順位は次のとおりです。

- ID による個々のルールの重大度エントリは、カテゴリの重大度エントリよりも優先されます。
- カテゴリの重大度エントリは、すべてのアナライザー ルールの重大度エントリよりも優先されます。

[CA1822](https://docs.microsoft.com/visualstudio/code-quality/ca1822)のカテゴリが "パフォーマンス" である次の EditorConfig の例を考えてみましょう。

   ```ini
   [*.cs]
   dotnet_diagnostic.CA1822.severity = error
   dotnet_analyzer_diagnostic.category-performance.severity = warning
   dotnet_analyzer_diagnostic.severity = suggestion
   ```

前の例では、3 つのエントリすべてが CA1822 に適用されます。 ただし、指定された優先順位規則を使用すると、最初のルール ID ベースの重大度エントリが次のエントリに優先されます。 この例では、CA1822 の重大度は "エラー" です。 "パフォーマンス" カテゴリを持つ残りのすべてのルールには、重大度 "警告" があります。 「パフォーマンス」カテゴリを持たない残りのすべてのアナライザールールには、重大度"提案"があります。

#### <a name="manually-configure-rule-severity"></a>ルールの重要度を手動で構成する

1. プロジェクトの EditorConfig ファイルがまだない場合は、ファイルを[追加](../ide/create-portable-custom-editor-options.md#add-an-editorconfig-file-to-a-project)します。

2. 対応するファイル拡張子の下に設定する各ルールのエントリを追加します。 たとえば[、CA1822](ca1822.md)の重要度を C# ファイルに`error`設定するには、エントリは次のようになります。

   ```ini
   [*.cs]
   dotnet_diagnostic.CA1822.severity = error
   ```

> [!NOTE]
> IDE コードスタイルのアナライザーでは、EditorConfig ファイルで、別の構文を使用して構成することもできます`dotnet_style_qualification_for_field = false:suggestion`。 ただし、構文を使用して重大度を`dotnet_diagnostic`設定した場合は、その重大度が優先されます。 詳細については、「 [EditorConfig の言語表記規則](../ide/editorconfig-language-conventions.md)」を参照してください。

#### <a name="convert-an-existing-ruleset-file-to-editorconfig-file"></a>既存のルールセット ファイルをエディタ構成ファイルに変換する

Visual Studio 2019 バージョン 16.5 以降、マネージ コードのアナライザー構成の EditorConfig ファイルを使用して、ルール セット ファイルは非推奨になりました。 アナライザー ルールの重要度の構成用の Visual Studio ツールの大部分は、ルール セット ファイルではなく EditorConfig ファイルで動作するように更新されました。 エディター構成ファイルを使用すると、アナライザー ルールの問題とアナライザー オプションの両方を構成できます。 既存のルールセット ファイルを EditorConfig ファイルに変換することを強くお勧めします。 また、EditorConfig ファイルは、レポのルートまたはソリューション フォルダーに保存することをお勧めします。 レポまたはソリューション フォルダーのルートを使用して、このファイルの重大度設定が、それぞれレポまたはソリューション全体に自動的に適用されるようにします。

既存のルールセットファイルを EditorConfig ファイルに変換するには、いくつかの方法があります。

- Visual Studio のルール セット エディターから (Visual Studio 2019 16.5 以降が必要です)。 プロジェクトで特定のルールセット ファイルが既に`CodeAnalysisRuleSet`使用されている場合は、Visual Studio 内のルールセット エディタから同等の EditorConfig ファイルに変換できます。

    1. ソリューション エクスプローラーでルール セット ファイルをダブルクリックします。

       ルールセットファイルがルールセットエディタで開きます。 ルールセット エディタの上部に、クリック可能な**情報バー**が表示されます。

       ![ルールセットエディタでのエディタ構成ファイルへの変換](media/convert-ruleset-to-editorconfig-file-ruleset-editor.png)

    2. 情報バーのリンクを**クリック**します。

       EditorConfig ファイルを生成するディレクトリを選択できる [**名前を付けて保存**] ダイアログが開きます。

    3. **[****保存**] ボタンをクリックして、エディタ構成ファイルを生成します。

       生成されたエディタ構成がエディタで開くはずです。 また、MSBuild プロパティ`CodeAnalysisRuleSet`は、元のルールセット ファイルを参照しなくなったプロジェクト ファイルで更新されます。

- コマンドラインから:

    1. をインストール[します。](https://www.nuget.org/packages/Microsoft.CodeAnalysis.RulesetToEditorconfigConverter)

    2. インストール`RulesetToEditorconfigConverter.exe`されたパッケージから、コマンドライン引数としてルールセットファイルとEditorConfigファイルへのパスを使用して実行します。

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

変換されたエディタ構成ファイルを次に示します。

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

#### <a name="automatically-configure-rule-severity"></a>ルールの重要度を自動的に構成する

##### <a name="configure-from-light-bulb-menu"></a>電球メニューから設定

Visual Studio では、[クイック アクション](../ide/quick-actions.md)の電球メニューからルールの重大度を構成する便利な方法が用意されています。

1. 違反が発生した後、エディタで違反波線の上にカーソルを合わせ、電球メニューを開きます。 または、カーソルを行に置き **、Ctrl**+**キーを押します。** (ピリオド) を押します。

2. 電球メニューから、[重大度を**構成] または [**>**問題の抑制] ルール ID>重大度を構成\<** する を選択します。

   ![Visual Studio の電球メニューからルールの重要度を構成する](media/configure-rule-severity.png)

3. そこから、重大度オプションのいずれかを選択します。

   ![ルールの重要度を提案として構成する](media/configure-rule-severity-suggestion.png)

   Visual Studio は、プレビュー ボックスに示すように、要求されたレベルにルールを構成する EditorConfig ファイルにエントリを追加します。

   > [!TIP]
   > プロジェクトにまだエディタ構成ファイルがない場合は、Visual Studio によって作成されます。

##### <a name="configure-from-error-list"></a>エラー一覧から構成

Visual Studio には、エラー一覧のコンテキスト メニューからルールの重大度を構成する便利な方法もあります。

1. 違反が発生した後、エラーリストの診断エントリを右クリックします。

2. コンテキスト メニューで、[**重大度の設定**] を選択します。

   ![エラー一覧からルールの重大度を構成する](media/configure-rule-severity-error-list.png)

3. そこから、重大度オプションのいずれかを選択します。

   要求されたレベルにルールを構成するエントリをエディター構成ファイルに追加します。

   > [!TIP]
   > プロジェクトにまだエディタ構成ファイルがない場合は、Visual Studio によって作成されます。

::: moniker-end

### <a name="set-rule-severity-from-solution-explorer"></a>ソリューション エクスプローラーからルールの重大度を設定する

1. ソリューション エクスプローラーで、**参照** > **アナライザ**(または .NET Core プロジェクトの**依存関係** > **アナライザー)** を展開します。

2. 重大度を設定するルールを含むアセンブリを展開します。

::: moniker range=">=vs-2019"
3. ルールを右クリックし、[**重大度の設定**] を選択します。 コンテキスト メニューで、重大度オプションのいずれかを選択します。

   要求されたレベルにルールを構成するエントリをエディター構成ファイルに追加します。 プロジェクトで EditorConfig ファイルではなくルールセット ファイルを使用している場合、重大度エントリがルールセット ファイルに追加されます。

   > [!TIP]
   > プロジェクトにまだエディタ構成ファイルまたはルールセット ファイルがない場合は、新しいエディタ構成ファイルが作成されます。
::: moniker-end

::: moniker range="vs-2017"
3. ルールを右クリックし、[**ルール セットの重要度の設定**] を選択します。 コンテキスト メニューで、重大度オプションのいずれかを選択します。

   ルールの重大度は、アクティブなルール セット ファイルに保存されます。
::: moniker-end

### <a name="set-rule-severity-in-the-rule-set-file"></a>ルール セット ファイルでルールの重要度を設定する

![ソリューション エクスプローラーのルール セット ファイル](media/ruleset-in-solution-explorer.png)

1. アクティブなルール セット ファイルを開くには、**ソリューション エクスプローラー**でファイルをダブルクリックし、[**参照** > **アナライザー]** ノードの右クリック メニューで **[アクティブなルール セットを開く**] を選択するか、プロジェクトの [**コード分析**] プロパティ ページで **[開く**] を選択します。

   ルール セットを初めて編集する場合は、既定の規則セット ファイルのコピーが作成され*\<、projectname>.ruleset*という名前が付け、プロジェクトに追加されます。 このカスタムルールセットは、プロジェクトに対して有効なルールセットにもなります。

   > [!NOTE]
   > .NET Core プロジェクトおよび .NET Standard プロジェクトでは、ソリューション**エクスプローラ**のルール セットのメニュー コマンドをサポート**していません。** NET Core または .NET 標準プロジェクトの既定以外の規則セットを指定するには、プロジェクト ファイル[に **"CodeAnalysisRuleSet/コード分析ルールセット"** プロパティ](using-rule-sets-to-group-code-analysis-rules.md#specify-a-rule-set-for-a-project)を手動で追加します。 Visual Studio のルール セット エディター UI でルール セット内のルールを構成できます。

1. 含まれているアセンブリを展開して、ルールを参照します。

1. [**アクション**] 列で、ドロップダウン リストを開く値を選択し、リストから必要な重大度を選択します。

   ![エディタで開くルール セット ファイル](media/ruleset-file-in-editor.png)

## <a name="suppress-violations"></a>違反を抑制する

ルール違反を抑制するには、複数の方法があります。

::: moniker range=">=vs-2019"

- **エディタ構成ファイル**内

  重要度を`none`に設定`dotnet_diagnostic.CA1822.severity = none`します。

- **[分析**] メニューから

  メニューバーの[ビルド**を分析** > **]および[アクティブな問題を抑制**]を選択して、現在のすべての違反を抑制します。 これは「ベースライニング」と呼ばれることもあります。

::: moniker-end

::: moniker range="vs-2017"

- **[分析**] メニューから

  メニュー バーの [実行コード分析の**分析** > **] と [アクティブな問題の抑制**] を選択して、現在のすべての違反を抑制します。 これは「ベースライニング」と呼ばれることもあります。

::: moniker-end

- **ソリューション エクスプローラー**から

  ルールの重大度を **[なし]** に設定します。

- ルール**セット エディタ**から

  名前の横にあるチェックボックスをオフにするか、[**アクション] を** **[なし]** に設定します。

- コード**エディター**から

  違反のあるコード行にカーソルを置き **、Ctrl**+**の期間 (.) を**押して**クイックアクション**メニューを開きます。 [**ソース/イン抑制ファイルで** **CAXXXX** > を抑制]を選択します。

  ![クイック アクション メニューからの診断を抑制する](media/suppress-diagnostic-from-editor.png)

- **エラー一覧**から

  抑制するルールを選択し、右クリックして [ > **ソース/イン抑制ファイルで抑制]** を選択します。 **Suppress**

  - [**ソース内]** を表示しない場合は、[**変更のプレビュー** ] ダイアログが開き、ソース コードに追加された C# [#pragma警告](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-pragma-warning)または Visual Basic [#Disable警告](/dotnet/visual-basic/language-reference/directives/directives)ディレクティブのプレビューが表示されます。

    ![コード ファイルに警告#pragma追加するプレビュー](media/pragma-warning-preview.png)

  - **[抑制ファイル]** を選択すると、[**変更のプレビュー** ] ダイアログが開き<xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute>、グローバル抑制ファイルに追加された属性のプレビューが表示されます。

    ![抑制ファイルに SuppressMessage 属性を追加するプレビュー](media/preview-changes-in-suppression-file.png)

  [**変更のプレビュー** ] ダイアログで、[**適用**] を選択します。

  > [!NOTE]
  > **ソリューション エクスプローラ**に [**抑制**] メニュー オプションが表示されない場合、違反はビルドから発生したものであり、実際の分析ではありません。 **[エラー一覧]** には、ライブ コード分析とビルドの両方から診断またはルール違反が表示されます。 たとえば、違反を修正するためにコードを編集しても再構築されていない場合は、ビルド診断が古くなる可能性があるため、**エラー一覧**からこれらの診断を抑制することはできません。 ライブ分析(IntelliSense)からの診断は常に最新の状態で、**エラー一覧**から抑制できます。 *ビルド*診断を選択から除外するには、[**エラー一覧]** ソース フィルタを **[ビルド + IntelliSense]** から **[IntelliSense のみ]** に切り替えます。 次に、抑制する診断を選択し、前述の手順に従って続行します。
  >
  > ![エラー リストのソース フィルターの Visual Studio](media/error-list-filter.png)

## <a name="command-line-usage"></a>コマンドラインの使用法

コマンド ラインでプロジェクトをビルドすると、次の条件が満たされた場合に、規則違反がビルド出力に表示されます。

- アナライザーは、VSIX 拡張機能ではなく、NuGet パッケージとしてインストールされます。

- プロジェクトのコードで 1 つ以上のルールに違反しています。

- 違反したルールの[重大度](#rule-severity)は **、** warning に設定され、その場合は違反によってビルドが**失敗しないか**、エラー が発生するとビルドが失敗します。

ビルド出力の詳細度は、ルール違反を表示するかどうかには影響しません。 **静かな**冗長性を持っていても、ルール違反はビルド出力に表示されます。

> [!TIP]
> コマンド ラインから *、FxCopCmd.exe*または**RunCodeAnalysis**フラグを使用した msbuild を使用して、レガシ分析を実行することに慣れている場合は、コード アナライザを使用して実行する方法を次に示します。

msbuild を使用してプロジェクトをビルドするときに、コマンド ラインでアナライザー違反を表示するには、次のようなコマンドを実行します。

```cmd
msbuild myproject.csproj /target:rebuild /verbosity:minimal
```

次のイメージは、アナライザー ルール違反を含むプロジェクトのビルドからのコマンドライン ビルド出力を示しています。

![ルール違反を示す MSBuild 出力](media/command-line-build-analyzers.png)

## <a name="dependent-projects"></a>依存プロジェクト

NET Core プロジェクトでは、NuGet アナライザーを持つプロジェクトへの参照を追加すると、それらのアナライザーも依存プロジェクトにも自動的に追加されます。 この動作を無効にするには(たとえば、依存プロジェクトが単体テスト プロジェクトの場合)、参照先プロジェクトの *.csproj*ファイルまたは *.vbproj*ファイルで **、Private**として NuGet パッケージをマークします。

```xml
<PackageReference Include="Microsoft.CodeAnalysis.FxCopAnalyzers" Version="2.9.0" PrivateAssets="all" />
```

## <a name="see-also"></a>関連項目

- [コード アナライザーの概要](../code-quality/roslyn-analyzers-overview.md)
- [コード アナライザのバグを送信する](https://github.com/dotnet/roslyn-analyzers/issues)
- [ルール セットを使用する](../code-quality/using-rule-sets-to-group-code-analysis-rules.md)
- [コード分析の警告を抑制する](../code-quality/in-source-suppression-overview.md)
