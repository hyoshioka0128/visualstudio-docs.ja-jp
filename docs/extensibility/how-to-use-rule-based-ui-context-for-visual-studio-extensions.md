---
title: '方法: Visual Studio 拡張機能のルール ベースの UI コンテキストを使用する |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 8dd2cd1d-d8ba-49b9-870a-45acf3a3259d
author: acangialosi
ms.author: anthc
ms.workload:
- vssdk
ms.openlocfilehash: de1a1e0a2022482433f81b0b2810b0d201ab7b8f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710595"
---
# <a name="how-to-use-rule-based-ui-context-for-visual-studio-extensions"></a>方法: Visual Studio 拡張機能のルール ベースの UI コンテキストを使用する

Visual Studio では、特定の既知<xref:Microsoft.VisualStudio.Shell.UIContext>のパッケージがアクティブ化されている場合に VS パッケージの読み込みを許可します。 ただし、これらの UI コンテキストは細かく表示されておらず、拡張機能の作成者は、VSPackage を実際に読み込みたいポイントの前にアクティブ化する UI コンテキストを選択する以外に選択肢はありません。 既知の UI コンテキストの一覧については、を<xref:Microsoft.VisualStudio.Shell.KnownUIContexts>参照してください。

パッケージの読み込みはパフォーマンスに影響を与える可能性があり、必要以上に早く読み込むのがベスト プラクティスではありません。 Visual Studio 2015 では、ルール ベースの UI コンテキストの概念が導入されました。

## <a name="rule-based-ui-context"></a>ルールベースの UI コンテキスト

"ルール" は、新しい UI コンテキスト (GUID) と論理 "and" 、"or"、"not" 操作と組み合わせた 1 つ以上の "Terms" を参照するブール式で構成されます。 「用語」は実行時に動的に評価され、条件が変更されるたびに式が再評価されます。 式が true と評価されると、関連付けられた UI コンテキストがアクティブになります。 それ以外の場合、UI コンテキストはアクティブ化解除されます。

ルールベースの UI コンテキストは、さまざまな方法で使用できます。

1. コマンドとツール ウィンドウの表示設定の制約を指定します。 UI コンテキスト ルールが満たされるまで、コマンド/ツール ウィンドウを非表示にすることができます。

2. 自動ロード制約として: 自動ロードパッケージはルールが満たされた場合のみ行われます。

3. 遅延タスクとして:指定された間隔が経過し、ルールが満たされるまで読み込みを遅延します。

   このメカニズムは、任意の Visual Studio 拡張機能で使用できます。

## <a name="create-a-rule-based-ui-context"></a>ルールベースの UI コンテキストを作成する
 TestPackage という拡張子があり *、.config*拡張子を持つファイルにのみ適用されるメニュー コマンドが用意されています。 VS2015 より前の最善のオプションは、UI<xref:Microsoft.VisualStudio.Shell.KnownUIContexts.SolutionExistsAndFullyLoadedContext%2A>コンテキストがアクティブ化されたときに TestPackage を読み込むことでした。 この方法で TestPackage を読み込む方法は効率的ではありません、 読み込まれたソリューションも *.config*ファイルを含まない可能性があります。 これらの手順では *、.config*拡張子を持つファイルが選択されている場合にのみ、ルールベースの UI コンテキストを使用して UI コンテキストをアクティブにし、その UI コンテキストがアクティブになったときに TestPackage を読み込む方法を示します。

1. 新しい UI コンテキスト GUID を定義し、VSPackage クラス<xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute>と<xref:Microsoft.VisualStudio.Shell.ProvideUIContextRuleAttribute>に追加します。

    たとえば、新しい UI コンテキスト "UIContextGuid" が追加されると仮定します。 作成された GUID (**ツール** > 作成 GUID をクリックして**GUID を作成**できます) は "8B40D5E2-5626-42AE-99EF-3DD1EFF46E7B" です。 次に、パッケージ クラス内に次の宣言を追加します。

   ```csharp
   public const string UIContextGuid = "8B40D5E2-5626-42AE-99EF-3DD1EFF46E7B";
   ```

    属性については、次の値を追加します(これらの属性の詳細については後述します)

   ```csharp
   [ProvideAutoLoad(TestPackage.UIContextGuid)]
   [ProvideUIContextRule(TestPackage.UIContextGuid,
       name: "Test auto load",
       expression: "DotConfig",
       termNames: new[] { "DotConfig" },
       termValues: new[] { "HierSingleSelectionName:.config$" })]
   ```

    これらのメタデータは、新しい UI コンテキスト GUID (8B40D5E2-5626-42AE-99EF-3DD1EFF46E7B) と単一の用語 "DotConfig" を参照する式を定義します。 "DotConfig" という用語は、アクティブな階層内の現在の選択項目に正規表現パターン ".config$"\\ *(.config$* で終わる) と一致する名前が付いている場合、必ず true と評価されます。 (デフォルト) 値は、デバッグに役立つルールの名前をオプションで定義します。

    属性の値は、ビルド後のビルド時に生成される pkgdef に追加されます。

2. テスト パッケージのコマンドの VSCT ファイルで、適切なコマンドに"動的表示" フラグを追加します。

   ```xml
   <CommandFlag>DynamicVisibility</CommandFlag>
   ```

3. VSCT の [Visibilities] セクションで、適切なコマンドを#1で定義された新しい UIContext GUID に結び付けます。

   ```xml
   <VisibilityConstraints>
       <VisibilityItem guid="guidTestPackageCmdSet" id="TestId"  context="UIContextGuid"/>
   </VisibilityConstraints>
   ```

4. [シンボル] セクションで、UIContext の定義を追加します。

   ```xml
   <GuidSymbol name="UIContextGuid" value="{8B40D5E2-5626-42AE-99EF-3DD1EFF46E7B}" />
   ```

    これで*\*、.config*ファイルのコンテキスト メニュー コマンドは、ソリューション エクスプローラで選択された項目が *.config*ファイルで、それらのコマンドのいずれかが選択されるまでパッケージが読み込まれなかった場合にのみ表示されます。

   次に、デバッガーを使用して、パッケージが期待される場合にのみ読み込まれることを確認します。 テスト パッケージをデバッグするには、

5. メソッドにブレークポイントを設定<xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A>します。

6. テスト パッケージをビルドし、デバッグを開始します。

7. プロジェクトを作成するか、開きます。

8. *.config*以外の拡張子を持つファイルを選択します。ブレークポイントにヒットしないでください。

9. *App.Config*ファイルを選択します。

   テスト パッケージは、ブレークポイントで読み込みと停止を行います。

## <a name="add-more-rules-for-ui-context"></a>UI コンテキストのルールを追加する
 UI コンテキスト ルールはブール式であるため、UI コンテキストに対して制限されたルールを追加できます。 たとえば、上記の UI コンテキストでは、プロジェクトを含むソリューションが読み込まれる場合にのみルールが適用されることを指定できます。 このように、プロジェクトの一部としてではなく、スタンドアロン ファイルとして *.config*ファイルを開くと、コマンドは表示されません。

```csharp
[ProvideAutoLoad(TestPackage.UIContextGuid)]
[ProvideUIContextRule(TestPackage.UIContextGuid,
    name: "Test auto load",
    expression: "(SingleProject | MultipleProjects) & DotConfig",
    termNames: new[] { "SingleProject", "MultipleProjects","DotConfig" },
    termValues: new[] { VSConstants.UICONTEXT_SolutionHasSingleProject_string , VSConstants.UICONTEXT_SolutionHasMultipleProjects_string , "HierSingleSelectionName:.config$" })]
```

 これで、式は 3 つの用語を参照します。 最初の 2 つの用語 "SingleProject" と "複数プロジェクト" は、他のよく知られた UI コンテキスト (GUID) を参照します。 3 番目の用語 "DotConfig" は、この記事で前に定義したルール ベースの UI コンテキストです。

## <a name="delayed-activation"></a>遅延アクティベーション
 ルールにはオプションの「遅延」を設定できます。 遅延はミリ秒単位で指定されます。 この遅延が存在する場合、ルールの UI コンテキストのアクティブ化または非アクティブ化は、その時間間隔までに遅延します。 ルールが遅延間隔の前に戻っても、何も起こりません。 このメカニズムは、タイマーに依存したり、アイドル状態の通知を登録したりすることなく、初期化ステップ(特にワンタイム初期化)を「ずらす」ために使用できます。

 たとえば、テストロードルールを100ミリ秒の遅延に指定できます。

```csharp
[ProvideAutoLoad(TestPackage.UIContextGuid)]
[ProvideUIContextRule(TestPackage.UIContextGuid,
    name: "Test auto load",
    expression: "DotConfig",
    termNames: new[] { "DotConfig" },
    termValues: new[] { "HierSingleSelectionName:.config$" },
    delay: 100)]
```

## <a name="term-types"></a>用語タイプ

サポートされる用語の種類は次のとおりです。

|期間|説明|
|-|-|
|{nnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnn}|GUID は、UI コンテキストを参照します。 この用語は、UI コンテキストがアクティブな場合は常に true、それ以外の場合は false になります。|
|ハイアシングル選択名:\<パターン>|この用語は、アクティブな階層内の選択項目が単一の項目で、選択された項目の名前が 「パターン」で指定された .Net 正規表現と一致する場合には必ず true になります。|
|クエリ>\<|"query" は、ユーザー設定ストアへの完全パスを表し、このパスはゼロ以外の値に評価される必要があります。 クエリは、最後のスラッシュで "コレクション" と "propertyName" に分割されます。|
|クエリ>\<|"query" は、0 以外の値に評価される必要がある構成設定ストアへの完全パスを表します。 クエリは、最後のスラッシュで "コレクション" と "propertyName" に分割されます。|
|プロジェクト\<の種類guid>|この用語は、現在選択されているプロジェクトがフレーバー (集計) され、指定されたプロジェクトの種類 GUID に一致するフレーバーを持つ場合には必ず true になります。|
|コンテンツ タイプ:\<>|この用語は、選択したドキュメントが、指定されたコンテンツ タイプのテキスト エディターである場合に当てはまります。 注: 選択したドキュメントの名前が変更されると、ファイルを閉じて再度開くまで、この用語は更新されません。|
|アクティブプロジェクトの機能\<: 式>|この用語は、アクティブなプロジェクト機能が指定された式と一致する場合に true です。 式は、VB &#124; CSharp のようなものにすることができます。|
|ソリューションはプロジェクトの機能\<: 式>|上記と同様ですが、式に一致する読み込み済みのプロジェクトがソリューションに含まれている場合は、term が true になります。|
|プロジェクトの種類を>。\<|この用語は、ソリューションにフレーバー (集計) されたプロジェクトがあり、指定されたプロジェクトの種類 GUID に一致するフレーバーがある場合には必ず当てはまります。|
|プロジェクト追加項目:\<パターン>| この用語は、"パターン" に一致するファイルが、開かれた soluion のプロジェクトに追加された場合に true です。|
|出力タイプ>\<|この用語は、アクティブなプロジェクトの出力タイプが正確に一致する場合に true です。  出力タイプは整数または型です<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROJOUTPUTTYPE>。|
|プロパティを\<ビルドプロパティ>=\<正規表現>|この用語は、アクティブなプロジェクトに指定されたビルド プロパティがあり、プロパティ値が regex フィルターに一致する場合に true です。 ビルド プロパティ[の詳細については、「MSBuild プロジェクト ファイルでのデータの保存](internals/persisting-data-in-the-msbuild-project-file.md)」を参照してください。|
|プロパティを\<ビルドプロパティ>=\<正規表現>|この用語は、ソリューションに、指定されたビルド プロパティとプロパティ値が指定された正規表現フィルターに一致する読み込み済みのプロジェクトがある場合に true です。|

## <a name="compatibility-with-cross-version-extension"></a>クロスバージョン拡張機能との互換性

ルール ベースの UI コンテキストは、Visual Studio 2015 の新機能であり、以前のバージョンには移植されません。 以前のバージョンに移植しないと、複数のバージョンの Visual Studio を対象とする拡張機能やパッケージに問題が生じます。 これらのバージョンは、Visual Studio 2013 以前では自動読み込まれる必要がありますが、ルール ベースの UI コンテキストを利用して、Visual Studio 2015 で自動読み込まれるのを防ぐことができます。

このようなパッケージをサポートするために、レジストリの AutoLoadPackages エントリは、Visual Studio 2015 以降でエントリをスキップする必要があることを示すフラグを値フィールドに提供できるようになりました。 これは、 に flags オプションを追加<xref:Microsoft.VisualStudio.Shell.PackageAutoLoadFlags>することで行うことができます。 VSPackage は、エントリを Visual Studio 2015 以降で無視する必要があることを示すために、その<xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute>属性に**SkipWhenUIContextRulesActive**オプションを追加できるようになりました。
## <a name="extensible-ui-context-rules"></a>拡張可能な UI コンテキスト ルール

パッケージで静的 UI コンテキスト ルールを使用できないことがあります。 たとえば、インポートされた MEF プロバイダーでサポートされるエディターの種類に基づいてコマンドの状態を使用するような機能拡張をサポートするパッケージがあるとします。 現在の編集タイプをサポートする拡張機能がある場合、このコマンドは有効になります。 このような場合、使用できる MEF 拡張機能によって用語が変更されるため、パッケージ自体は静的 UI コンテキスト ルールを使用できません。

このようなパッケージをサポートするために、ルール ベースの UI コンテキストは、その下のすべての用語が OR で結合されることを示すハードコードされた式 "*" をサポートします。 これにより、マスター パッケージは、既知のルール ベースの UI コンテキストを定義し、そのコマンド状態をこのコンテキストに結び付けることができ、 その後、マスターパッケージを対象とする MEF 拡張は、他の用語やマスター式に影響を与えることなく、サポートするエディターの用語を追加できます。

コンストラクター<xref:Microsoft.VisualStudio.Shell.ProvideExtensibleUIContextRuleAttribute.%23ctor%2A>のドキュメントでは、拡張可能な UI コンテキスト 規則の構文を示します。
