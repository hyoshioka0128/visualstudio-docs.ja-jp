---
title: Visual Studio 拡張機能のルールベースの UI コンテキストを使用する
titleSuffix: ''
description: ルールベースの UI コンテキストを使用する方法について説明します。これにより、拡張機能の作成者は、UI コンテキストがアクティブになって Vspackage が読み込まれたときに条件を定義できます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 8dd2cd1d-d8ba-49b9-870a-45acf3a3259d
author: leslierichardson95
ms.author: lerich
ms.workload:
- vssdk
ms.openlocfilehash: 0ce09edd20c0c46a6b93ace77808fdfc7d5d1c5d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057365"
---
# <a name="how-to-use-rule-based-ui-context-for-visual-studio-extensions"></a>方法: 規則ベースの UI コンテキストを Visual Studio 拡張機能に使用する

Visual Studio では、特定の既知のがアクティブになったときに Vspackage を読み込むことができ <xref:Microsoft.VisualStudio.Shell.UIContext> ます。 ただし、これらの UI コンテキストは不十分であるため、拡張機能の作成者には何も選択されませんが、VSPackage の読み込みに必要なポイントの前にアクティブになる UI コンテキストを選択することはできません。 よく知られている UI コンテキストの一覧については、「」を参照してください <xref:Microsoft.VisualStudio.Shell.KnownUIContexts> 。

パッケージの読み込みは、パフォーマンスに影響を与える可能性があり、必要以上に迅速に読み込むことがベストプラクティスではありません。 Visual Studio 2015 では、ルールベースの UI コンテキストの概念が導入されました。これは、拡張機能の作成者が UI コンテキストをアクティブ化し、関連付けられている Vspackage を読み込んだ正確な条件を定義できるようにするメカニズムです。

## <a name="rule-based-ui-context"></a>ルールベースの UI コンテキスト

"ルール" は、新しい UI コンテキスト (GUID) と、論理 "and"、"or"、"not" の各操作を組み合わせた1つ以上の "Terms" を参照するブール式で構成されます。 "Terms" は実行時に動的に評価され、その条件が変更されるたびに式が再評価されます。 式が true と評価されると、関連付けられた UI コンテキストがアクティブになります。 それ以外の場合、UI コンテキストは非アクティブ化されます。

ルールベースの UI コンテキストは、さまざまな方法で使用できます。

1. コマンドおよびツールウィンドウの表示の制約を指定します。 UI コンテキストルールが満たされるまでは、コマンド/ツールウィンドウを非表示にすることができます。

2. 自動読み込み制約として: 規則が満たされた場合にのみパッケージを自動読み込みます。

3. 遅延タスクとして: 指定された間隔が経過してもルールが満たされるまで、読み込みを遅延します。

   このメカニズムは、すべての Visual Studio 拡張機能で使用できます。

## <a name="create-a-rule-based-ui-context"></a>ルールベースの UI コンテキストを作成する
 たとえば、TestPackage という名前の拡張機能を使用しているとします。これには、 *.config* 拡張子を持つファイルにのみ適用されるメニューコマンドが用意されています。 VS2015 より前のベストオプションは、 <xref:Microsoft.VisualStudio.Shell.KnownUIContexts.SolutionExistsAndFullyLoadedContext%2A> UI コンテキストがアクティブになったときに TestPackage を読み込むことでした。 この方法で TestPackage を読み込むことは効率的ではありません。読み込まれたソリューションに *.config* ファイルが含まれていない可能性があるためです。 次の手順では、 *.config* 拡張子を持つファイルが選択されている場合にのみ、規則ベースの ui コンテキストを使用して ui コンテキストをアクティブ化する方法を示し、その ui コンテキストがアクティブになったときに testpackage を読み込みます。

1. 新しい UIContext GUID を定義し、VSPackage クラスとにを追加し <xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute> <xref:Microsoft.VisualStudio.Shell.ProvideUIContextRuleAttribute> ます。

    たとえば、新しい UIContext "UIContextGuid" が追加されるとします。 作成された guid ([**ツール**] [guid の作成] をクリックして guid を作成でき  >  ます) は、"8B40D5E2-5626-42AE-99EF-3DD1EFF46E7B" です。 次に、パッケージクラス内に次の宣言を追加します。

   ```csharp
   public const string UIContextGuid = "8B40D5E2-5626-42AE-99EF-3DD1EFF46E7B";
   ```

    属性には、次の値を追加します (これらの属性の詳細については後で説明します)。

   ```csharp
   [ProvideAutoLoad(TestPackage.UIContextGuid)]
   [ProvideUIContextRule(TestPackage.UIContextGuid,
       name: "Test auto load",
       expression: "DotConfig",
       termNames: new[] { "DotConfig" },
       termValues: new[] { "HierSingleSelectionName:.config$" })]
   ```

    これらのメタデータは、新しい UIContext GUID (8B40D5E2-5626-42AE-99EF-3DD1EFF46E7B) と1つの用語 "DotConfig" を参照する式を定義します。 "DotConfig" という用語は、アクティブ階層内の現在の選択範囲の名前が、正規表現パターン " \\ . .config $" ( *.config* で終わる) と一致する場合に true に評価されます。 (既定値) 値は、デバッグに便利な規則の名前を定義します (省略可能)。

    属性の値は、後でビルド時に生成された .pkgdef に追加されます。

2. TestPackage のコマンドの VSCT ファイルで、"DynamicVisibility" フラグを適切なコマンドに追加します。

   ```xml
   <CommandFlag>DynamicVisibility</CommandFlag>
   ```

3. VSCT の可視性セクションで、適切なコマンドを #1 で定義されている新しい UIContext GUID に関連付けます。

   ```xml
   <VisibilityConstraints>
       <VisibilityItem guid="guidTestPackageCmdSet" id="TestId"  context="UIContextGuid"/>
   </VisibilityConstraints>
   ```

4. [シンボル] セクションで、UIContext の定義を追加します。

   ```xml
   <GuidSymbol name="UIContextGuid" value="{8B40D5E2-5626-42AE-99EF-3DD1EFF46E7B}" />
   ```

    これで、 *\* .config* ファイルのコンテキストメニューコマンドは、ソリューションエクスプローラーで選択された項目が *.config* ファイルの場合にのみ表示され、これらのコマンドのいずれかが選択されるまで、パッケージは読み込まれません。

   次に、デバッガーを使用して、パッケージがであると予想される場合にのみ読み込まれることを確認します。 TestPackage をデバッグするには:

5. メソッドにブレークポイントを設定 <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> します。

6. TestPackage をビルドし、デバッグを開始します。

7. プロジェクトを作成するか、プロジェクトを開きます。

8. 拡張子が *.config* 以外のファイルを選択します。ブレークポイントにヒットすることはできません。

9. *App.Config* ファイルを選択します。

   TestPackage は、ブレークポイントで読み込みと停止を行います。

## <a name="add-more-rules-for-ui-context"></a>UI コンテキストのルールを追加する
 UI コンテキストの規則はブール式であるため、UI コンテキストに対して制限された規則を追加できます。 たとえば、上記の UI コンテキストでは、プロジェクトを含むソリューションが読み込まれた場合にのみ規則を適用するように指定できます。 この方法では、プロジェクトの一部としてではなく、スタンドアロンファイルとして *.config* ファイルを開くと、コマンドが表示されません。

```csharp
[ProvideAutoLoad(TestPackage.UIContextGuid)]
[ProvideUIContextRule(TestPackage.UIContextGuid,
    name: "Test auto load",
    expression: "(SingleProject | MultipleProjects) & DotConfig",
    termNames: new[] { "SingleProject", "MultipleProjects","DotConfig" },
    termValues: new[] { VSConstants.UICONTEXT.SolutionHasSingleProject_string , VSConstants.UICONTEXT.SolutionHasMultipleProjects_string , "HierSingleSelectionName:.config$" })]
```

 これで、式は3つの用語を参照します。 最初の2つの用語では、"SingleProject" と "複数のプロジェクト" が、他のよく知られている UI コンテキスト (Guid) を参照しています。 3つ目の用語 "DotConfig" は、この記事で既に定義されている規則ベースの UI コンテキストです。

## <a name="delayed-activation"></a>遅延アクティブ化
 ルールには、省略可能な "Delay" を指定できます。 遅延はミリ秒単位で指定します。 存在する場合、遅延によって、ルールの UI コンテキストのアクティブ化または非アクティブ化が、その時間間隔で遅延されます。 ルールが遅延間隔の前に戻された場合、何も起こりません。 このメカニズムを使用すると、タイマーに依存せず、またはアイドル状態の通知に登録しなくても、初期化手順を "ずらす" ことができます。

 たとえば、テスト負荷ルールを指定して、100ミリ秒の遅延を設定できます。

```csharp
[ProvideAutoLoad(TestPackage.UIContextGuid)]
[ProvideUIContextRule(TestPackage.UIContextGuid,
    name: "Test auto load",
    expression: "DotConfig",
    termNames: new[] { "DotConfig" },
    termValues: new[] { "HierSingleSelectionName:.config$" },
    delay: 100)]
```

## <a name="term-types"></a>用語の種類

サポートされているさまざまな種類の用語を次に示します。

|項目|Description|
|-|-|
|{nnnnnnnn-nnnn-nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn}|GUID は、UI コンテキストを参照します。 この用語は、UI コンテキストがアクティブである場合は true、それ以外の場合は false になります。|
|HierSingleSelectionName:\<pattern>|この用語は、アクティブ階層内の選択が単一の項目であり、選択した項目の名前が "pattern" で指定された .Net 正規表現と一致する場合に true になります。|
|UserSettingsStoreQuery:\<query>|"query" は、0以外の値に評価される必要がある、ユーザー設定ストアへの完全なパスを表します。 クエリは、最後のスラッシュで "collection" および "propertyName" に分割されます。|
|ConfigSettingsStoreQuery:\<query>|"query" は、構成設定ストアへの完全パスを表します。これは、0以外の値に評価される必要があります。 クエリは、最後のスラッシュで "collection" および "propertyName" に分割されます。|
|ActiveProjectFlavor:\<projectTypeGuid>|現在選択されているプロジェクトが flavored (集計) され、指定されたプロジェクトの種類の GUID と一致するフレーバーがある場合、この用語は true になります。|
|ActiveEditorContentType:\<contentType>|選択したドキュメントが、指定されたコンテンツタイプのテキストエディターである場合、用語は true になります。 注: 選択したドキュメントの名前を変更しても、ファイルを閉じて再度開くまで、この用語は更新されません。|
|ActiveProjectCapability:\<Expression>|アクティブなプロジェクトの機能が指定された式と一致する場合は、という用語が当てはまります。 式は、VB &#124; CSharp のようなものにすることができます。|
|SolutionHasProjectCapability:\<Expression>|上記と同様ですが、式に一致する読み込み済みのプロジェクトがソリューションに含まれている場合は、という用語が当てはまります。|
|SolutionHasProjectFlavor:\<projectTypeGuid>|ソリューションに flavored (集計) され、指定されたプロジェクトの種類の GUID に一致するフレーバーがあるプロジェクトがある場合、この用語は true になります。|
|ProjectAddedItem:\<pattern>| "Pattern" と一致するファイルが、開いている soluion 内のプロジェクトに追加された場合、この用語は true になります。|
|ActiveProjectOutputType:\<outputType>|アクティブプロジェクトの出力の種類が完全に一致する場合は、という用語が当てはまります。  OutputType には、整数または型を指定でき <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROJOUTPUTTYPE> ます。|
|ActiveProjectBuildProperty:\<buildProperty>=\<regex>|アクティブなプロジェクトに指定されたビルドプロパティがあり、プロパティ値が指定された regex フィルターと一致する場合は、という用語が当てはまります。 ビルドプロパティの詳細については、「 [MSBuild プロジェクトファイルでのデータの永続化」](internals/persisting-data-in-the-msbuild-project-file.md) を参照してください。|
|SolutionHasProjectBuildProperty:\<buildProperty>=\<regex>|ソリューションに、指定したビルドプロパティとプロパティ値が指定された regex フィルターに一致するプロジェクトが読み込まれている場合は、という用語が当てはまります。|

## <a name="compatibility-with-cross-version-extension"></a>バージョン間の拡張機能との互換性

ルールベースの UI コンテキストは、Visual Studio 2015 の新機能であり、以前のバージョンに移植されることはありません。 以前のバージョンに移植しないと、Visual Studio の複数のバージョンを対象とする拡張機能やパッケージに問題が発生します。 これらのバージョンは Visual Studio 2013 以前で自動読み込みする必要がありますが、Visual Studio 2015 で自動読み込みが行われないようにするには、ルールベースの UI コンテキストを利用できます。

このようなパッケージをサポートするために、レジストリの AutoLoadPackages エントリは、Visual Studio 2015 以降でエントリをスキップする必要があることを示すフラグを値フィールドに提供できるようになりました。 これを行うには、flags オプションをに追加し <xref:Microsoft.VisualStudio.Shell.PackageAutoLoadFlags> ます。 Vspackage は、 **SkipWhenUIContextRulesActive** オプションを属性に追加して <xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute> 、Visual Studio 2015 以降ではエントリを無視することを示すことができるようになりました。
## <a name="extensible-ui-context-rules"></a>拡張可能な UI コンテキストの規則

場合によっては、パッケージが静的 UI コンテキストルールを使用できないことがあります。 たとえば、コマンドの状態が、インポートされた MEF プロバイダーでサポートされているエディターの種類に基づいているように、拡張をサポートするパッケージがあるとします。 現在の編集の種類をサポートする拡張機能がある場合は、コマンドが有効になります。 このような場合、パッケージ自体は、使用可能な MEF 拡張機能に応じて変更されるため、静的な UI コンテキストルールを使用できません。

このようなパッケージをサポートするために、ルールベースの UI コンテキストでは、ハードコーディングされた式 "*" をサポートしています。これは、その下にあるすべての用語をまたはと結合することを示します。 これにより、マスターパッケージは既知のルールベースの UI コンテキストを定義し、そのコマンドの状態をこのコンテキストに関連付けることができます。 その後、マスターパッケージを対象とする MEF 拡張機能では、他の用語やマスター式に影響を与えることなく、サポートされているエディターの条件を追加できます。

コンストラクターの <xref:Microsoft.VisualStudio.Shell.ProvideExtensibleUIContextRuleAttribute.%23ctor%2A> ドキュメントは、拡張可能な UI コンテキストの規則の構文を示しています。
