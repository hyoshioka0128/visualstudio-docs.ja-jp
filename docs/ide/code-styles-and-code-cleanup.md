---
title: コード スタイルのオプションとコードのクリーンアップ
ms.date: 04/25/2019
ms.topic: conceptual
author: TerryGLee
ms.author: tglee
manager: jillfra
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.CSharp.Code_Style.General
- VS.ToolsOptionsPages.Text_Editor.Basic.Code_Style.General
ms.workload:
- multiple
ms.openlocfilehash: 9d540339ca25fc42fc05df4818a6d05204ccae0e
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "79306831"
---
# <a name="code-style-preferences"></a>コードのスタイル設定

[EditorConfig ファイル](#code-styles-in-editorconfig-files)を使用し、プロジェクト別にコード スタイル設定を定義できます。あるいは、テキスト エディターの [ **[オプション]** ページ](#code-styles-in-the-options-dialog-box)で、Visual Studio で編集するすべてのコードを対象にできます。 C# コードの場合、**コードのクリーンアップ** (Visual Studio 2019) コマンドと**ドキュメントのフォーマット** (Visual Studio 2017) コマンドを使用し、これらのコード スタイル設定を適用するように Visual Studio を構成することもできます。

> [!NOTE]
> このトピックは、Windows 上の Visual Studio に適用されます。 Visual Studio for Mac については、[Visual Studio for Mac でのエディターの動作](/visualstudio/mac/editor-behavior)に関するページを参照してください。

## <a name="code-styles-in-editorconfig-files"></a>EditorConfig ファイルのコード スタイル

.NET に対する[コード スタイルの設定](create-portable-custom-editor-options.md)は、[EditorConfig](../ide/editorconfig-code-style-settings-reference.md) ファイルをプロジェクトに追加することで指定できます。 EditorConfig ファイルは、Visual Studio のパーソナル化アカウントではなく、コードベースに関連付けられます。 EditorConfig ファイル内の設定は、 **[オプション]** ダイアログ ボックスで指定されているコード スタイルよりも優先されます。 リポジトリまたはプロジェクトに対するすべての共同作成者にコーディング スタイルを適用する場合は、EditorConfig ファイルを使用します。

::: moniker range=">=vs-2019"

EditorConfig ファイルは手動で入力できます。または、Visual Studio の **[オプション]** ダイアログ ボックスで設定したコード スタイルの設定に基づいて、ファイルを自動的に生成できます。 このオプション ページは、 **[ツール]**  >  **[オプション]**  >  **[テキスト エディター]** 、 **[C#]** または **[Basic]** 、 **[コード スタイル]**  >  **[全般]** の順に選択すると表示されます。 **[Generate .editorconfig file from settings]\(設定から .editorconfig ファイルを生成する\)** をクリックすると、この **[オプション]** ページの設定に基づいてコーディング スタイルの *.editorconfig* ファイルが自動的に生成されます。

![Visual Studio 2019 で設定から editorconfig ファイルを生成する](media/vs-2019/generate-editorconfig-file-small.png)

::: moniker-end

## <a name="code-styles-in-the-options-dialog-box"></a>[オプション] ダイアログ ボックスのコード スタイル

すべての C# プロジェクトと Visual Basic プロジェクトに対してコードのスタイルを設定するには、 **[ツール]** メニューから **[オプション]** ダイアログ ボックスを開きます。 **[オプション]** ダイアログ ボックスで、 **[テキスト エディター]** > **[C#]** または **[Basic]** > **[コード スタイル]**  >  **[全般]** の順に選択します。

選択すると、リスト内の各項目について優先順位のプレビューが表示されます。

::: moniker range="vs-2017"

![コード スタイルのオプション](media/code-style-quick-actions-dialog.png)

::: moniker-end

::: moniker range=">=vs-2019"

![コード スタイルのオプション](media/vs-2019/code-style-quick-actions-dialog.png)

::: moniker-end

このウィンドウで設定したオプションは、Visual Studio のパーソナル化アカウントに適用され、特定のプロジェクトまたはコードベースには関連付けられません。 さらに、継続的インテグレーション (CI) のビルドなど、ビルド時には適用されません。 コード スタイルのユーザー設定をプロジェクトに関連付けて、ビルド時にスタイルを適用する場合は、プロジェクトに関連付けられている [.editorconfig ファイル](#code-styles-in-editorconfig-files)でユーザー設定を指定します。

### <a name="preference-and-severity"></a>優先順位と重大度

各行のドロップダウンを使用して、このページのコード スタイル設定ごとに **[優先順位]** と **[重大度レベル]** の値を設定できます。 重大度は、 **[リファクタリングのみ]** 、 **[提案]** 、 **[警告]** 、または **[エラー]** に設定できます。 コード スタイルの[クイック アクション](../ide/quick-actions.md)を有効にする場合、 **[重大度レベル]** の設定は確実に **[リファクタリングのみ]** 以外に設定してください。 **クイック アクション**の電球 ![電球](media/light-bulb-dropdown.png)、エラー電球 ![エラー電球](media/error-bulb.png)、ねじ回し ![ねじ回し](media/screwdriver.png) アイコンは、優先されていないスタイルが使用されていて、 **[クイック アクション]** 一覧のオプションを選ぶと優先されるスタイルにコードが自動的に再作成されると表示されます。

## <a name="apply-code-styles"></a>コード スタイルの適用

::: moniker range="vs-2017"

正規の書式設定 (字下げなど) に沿って (EditorConfig ファイルまたは **[コード スタイル]** オプションから) コード スタイル設定を適用するように**ドキュメントのフォーマット** コマンドを構成できます ( **[編集]**  >  **[詳細]**  >  **[ドキュメントのフォーマット]** )。 プロジェクトに *.editorconfig* ファイルが存在する場合、その設定が優先されます。

> [!NOTE]
> **ドキュメントのフォーマット** コマンドでコード スタイルを適用することは、C# コード ファイルの場合にのみ可能です。 これは試験段階の機能です。

[[書式設定] オプション ページ](reference/options-text-editor-csharp-formatting.md#format-document-settings)で**ドキュメントのフォーマット**に適用する設定を構成します。

![Visual Studio 2017 のドキュメントのフォーマットのコード スタイル設定](media/format-document-settings-experiment.png)

> [!TIP]
> 重大度が**なし**で構成されているルールは、コードのクリーンアップには関係しませんが、 **[クイック アクションとリファクタリング]** メニューを使用して個別に適用できます。

初めて **[ドキュメントのフォーマット]** コマンドをトリガーするときに、黄色の情報バーが表示され、コードのクリーンアップ設定を構成するように求められます。

::: moniker-end

::: moniker range=">=vs-2019"

C# コード ファイルの場合、Visual Studio 2019 では、エディターの一番下に **[コードのクリーンアップ]** ボタンがあり (キーボード:**Ctrl**+**K**、**Ctrl**+**E**)、これで EditorConfig ファイルまたは **[コード スタイル]** オプション ページからのコード スタイルを適用します。 プロジェクトに *.editorconfig* ファイルが存在する場合、それが優先設定となります。

![Visual Studio 2019 でコードのクリーンアップを実行する](media/execute-code-cleanup.png)

> [!TIP]
> 重大度が**なし**で構成されているルールは、コードのクリーンアップには関係しませんが、 **[クイック アクションとリファクタリング]** メニューを使用して個別に適用できます。

まず、 **[コード クリーンアップの構成]** ダイアログ ボックスで (2 つのプロファイルのいずれかで) 適用するコード スタイルを構成します。 このダイアログ ボックスを開くには、コードのクリーンアップのほうきアイコンの横にある展開用の矢印をクリックし、 **[コード クリーンアップの構成]** を選択します。

![Visual Studio 2019 のコード クリーンアップの構成](media/configure-code-cleanup.png)

コードのクリーンアップを構成した後、ほうきアイコンをクリックするか、または **Ctrl**+**K** キー、**Ctrl**+**E** キーを順に押して、コードのクリーンアップを実行します。 プロジェクト全体またはソリューション全体に対して、コードのクリーンアップを実行することもできます。 **ソリューション エクスプローラー**でプロジェクトまたはソリューションの名前を右クリックし、 **[分析とコードのクリーンアップ]** を選択して、 **[コードのクリーンアップの実行]** を選択します。

![プロジェクト全体またはソリューション全体に対してコードのクリーンアップを実行する](media/run-code-cleanup-project-solution.png)

ファイルを保存するたびにコード スタイル設定を適用する場合、[Code Cleanup on Save](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.CodeCleanupOnSave) という拡張機能をお勧めします。

::: moniker-end

## <a name="see-also"></a>関連項目

- [クイック アクション](../ide/quick-actions.md)
- [EditorConfig の .NET コーディング規則の設定](../ide/editorconfig-code-style-settings-reference.md)
- [エディターの動作 (Visual Studio for Mac)](/visualstudio/mac/editor-behavior)
