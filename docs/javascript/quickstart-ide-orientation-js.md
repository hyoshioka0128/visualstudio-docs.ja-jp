---
title: Visual Studio IDE のツアー
titleSuffix: ''
ms.date: 02/05/2019
ms.topic: quickstart
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 713e7319618b42e2cdc4b8c0951bd79c225ac1b6
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2020
ms.locfileid: "73636588"
---
# <a name="first-look-at-the-visual-studio-ide"></a>Visual Studio IDE の表示の紹介

この 5 - 10 分程度の Visual Studio 統合開発環境 (IDE) の紹介では、ウィンドウやメニューなどの UI 機能の一部を説明します。

::: moniker range="vs-2017"

Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) ページに移動し、無料試用版をインストールしてください。

::: moniker-end

::: moniker range="vs-2019"

Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads) ページに移動し、無料試用版をインストールしてください。

::: moniker-end

::: moniker range=">=vs-2019"

## <a name="start-window"></a>スタート ウィンドウ

Visual Studio を起動するとまずスタート ウィンドウが表示されます。 スタート ウィンドウは、速やかに "コードに移動" できるようなデザインになっています。 コードを閉じる/チェックアウトするオプション、既存のプロジェクトまたはソリューションを開くオプション、新しいプロジェクトを作成するオプション、いくつかのコード ファイルが含まれるフォルダーを開くためのオプションがあります。

[![Visual Studio 2019 のスタート画面](media/vs-2019/start-window.png)](media/vs-2019/start-window.png)

Visual Studio を初めて使用する場合、最近使用したプロジェクト リストは空になります。

MSBuild ベースではないコードベースを使用している場合、**[ローカル フォルダーを開く]** オプションを使用し、Visual Studio でコードを開きます。 詳細については、「[プロジェクトまたはソリューションを使用せずに Visual Studio でコードを開発する](develop-javascript-code-without-solutions-projects.md)」を参照してください。 そうでなければ、GitHub や Azure DevOps など、ソース プロバイダーから新しいプロジェクトを作成したり、プロジェクトを複製したりできます。

**[コードなしで続行]** オプションを使用すると、特定のプロジェクトやコードが読み込まれることなく、Visual Studio 開発環境が起動します。 [Live Share](/visualstudio/liveshare/) セッションに参加したり、デバッグ目的でプロセスに接続したりするとき、このオプションを選択することがあります。 **Esc** を押してスタート ウィンドウを閉じ、IDE を開くこともできます。

::: moniker-end

::: moniker range="vs-2017"

## <a name="start-page"></a>スタート ページ

ほとんどの場合、Visual Studio を起動するとまず**スタート ページ**が表示されます。 **スタート ページ**は、必要なコマンドとプロジェクト ファイルを見つけやすくする "ハブ" として設計されています。 **[最近]** セクションには、プロジェクトと最近作業したフォルダーが表示されます。 **[新しいプロジェクト]** の下にあるリンクをクリックすると、**[新しいプロジェクト]** ダイアログ ボックスが開きます。また、**[開く]** では、既存のコード プロジェクトやフォルダーを開くことができます。 右側には、最新の開発者向けニュース フィードが表示されます。

![Visual Studio の [スタート ページ]](media/start-page.png)

**スタート ページ**を閉じた後でもう一度表示する場合は、**[ファイル]** メニューで再度開くことができます。

![Visual Studio の [ファイル] メニュー](media/quickstart-IDE-file-menu-large.png)

::: moniker-end

## <a name="create-a-project"></a>プロジェクトの作成

Visual Studio の機能を引き続き確認するために、新しいプロジェクトを作成しましょう。

::: moniker range=">=vs-2019"

1. [スタート ウィンドウ] で **[新しいプロジェクトの作成]** を選択し、検索ボックスに「**javascript**」と入力し、プロジェクトの種類の一覧にフィルターを適用し、名前または言語タイプに "javascript" が含まれるものに絞り込みます。

   Visual Studio には、すぐにコーディングを開始するのに役立つ、さまざまな種類のプロジェクト テンプレートが用意されています。 (あるいは、TypeScript の開発者であれば、その言語でプロジェクトを作成できます。 表示される UI はすべてのプログラミング言語でほぼ同じです)。

   ![Visual Studio の [スタート ウィンドウ] でプロジェクト テンプレートを検索する](media/vs-2019/create-new-project.png)

1. **Blank Node.js Web Application** プロジェクト テンプレートを選択し、**[次へ]** をクリックします。

1. 表示された **[新しいプロジェクトの構成]** ダイアログ ボックスで、既定のプロジェクト名をそのまま使用し、**[作成]** を選択します。

::: moniker-end

::: moniker range="vs-2017"

1. **[スタート ページ]** の **[新しいプロジェクト]** の下にある検索ボックスに「**javascript**」と入力し、プロジェクトの種類の一覧にフィルターを適用し、名前または言語タイプに "javascript" が含まれるものに絞り込みます。

   ![Visual Studio の [スタート ページ] でプロジェクト テンプレートを検索する](media/start-page-search-templates.png)

   Visual Studio には、すぐにコーディングを開始するのに役立つ、さまざまな種類のプロジェクト テンプレートが用意されています。 **Blank Node.js Web Application** プロジェクト テンプレートを選択します。 (あるいは、TypeScript の開発者であれば、その言語でプロジェクトを作成できます。 表示される UI はすべてのプログラミング言語でほぼ同じです)。

1. 表示された **[新しいプロジェクト]** ダイアログ ボックスで、既定のプロジェクト名をそのまま使用し、**[OK]** を選択します。
::: moniker-end

   プロジェクトが作成され、*server.js* という名前のファイルが **[エディター]** ウィンドウに開きます。 **エディター**にファイルの内容が表示されます。Visual Studio でのコード作成作業のほとんどは、このエディターで行います。

   ![Visual Studio のエディター](media/editor.png)

## <a name="solution-explorer"></a>ソリューション エクスプローラー

通常は Visual Studio の右側にある**ソリューション エクスプローラー**には、プロジェクト、ソリューション、コード フォルダー内のファイルとフォルダーの階層がグラフィカルに表示されます。 **ソリューション エクスプローラー**内で階層を移動し、ファイルを選択できます。

![Visual Studio のソリューション エクスプローラー](media/quickstart-IDE-solution-explorer.png)

## <a name="menus"></a>メニュー

Visual Studio の上部にあるメニュー バーには、コマンドがカテゴリごとにグループ化されています。 たとえば、**[プロジェクト]** メニューには、作業中のプロジェクトに関連するコマンドが含まれています。 **[ツール]** メニューでは、**[オプション]** を選択して Visual Studio の動作をカスタマイズしたり、**[ツールと機能を取得]** を選択してインストールに機能を追加したりできます。

![Visual Studio のメニュー バー](media/quickstart-IDE-menu-bar.png)

**[表示]** メニューの **[エラー一覧]** を選択して、**[エラー一覧]** ウィンドウを開いてみましょう。

## <a name="error-list"></a>エラー一覧

**[エラー一覧]** ウィンドウには、現在の状態のコードに関するエラー、警告、メッセージが表示されます。 ファイル、またはプロジェクト内のどこかにエラー (中かっこやセミコロンの欠落など) がある場合は、ここに一覧表示されます。

![Visual Studio の [エラー一覧]](media/quickstart-IDE-error-list.png)

## <a name="output-window"></a>[出力] ウィンドウ

**[出力]** ウィンドウには、プロジェクトのビルド時の出力メッセージや、ソース管理プロバイダーからの出力メッセージが表示されます。

プロジェクトをビルドして、ビルド出力をいくつか確認してみましょう。 **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。 自動的に **[出力]** ウィンドウにフォーカスされ、ビルドが成功したことを示すメッセージが表示されます。

![Visual Studio の [出力] ウィンドウ](media/build-output-minimal.png)

## <a name="search-box"></a>検索ボックス

検索ボックスでは、Visual Studio でのほぼすべての操作をすばやく簡単に行うことができます。 実行する操作に関連したテキストを入力すると、そのテキストに関係するオプションの一覧が表示されます。 たとえば、ビルドで実際に行われる内容をさらに詳しく表示するために、ビルド出力の詳細レベルを上げるとします。 これは次のように行います。

1. 検索ボックスに「**詳細度**」と入力します。 **[オプション]** カテゴリで、表示された結果から **[プロジェクトおよびソリューション] --> [ビルド/実行]** を選択します。

   ![Visual Studio の検索ボックス](media/quickstart-IDE-quick-launch.png)

   **[オプション]** ダイアログ ボックスが開き、**[ビルド/実行]** オプションのページが表示されます。

1. **[MSBuild プロジェクト ビルドの出力の詳細]** で **[標準]** を選択し、**[OK]** をクリックします。

1. **ソリューション エクスプローラー**で **[NodejsWebApp1]** プロジェクトを右クリックし、コンテキスト メニューで **[リビルド]** を選択して、プロジェクトをもう一度ビルドします。

   今度は、**[出力]** ウィンドウには、どの場所のどのファイルがコピーされたかなど、ビルド プロセスに関するより詳細なログが表示されます。

   ![Visual Studio の詳細なビルド出力](media/build-output-verbose.png)

## <a name="send-feedback-menu"></a>[フィードバックの送信] メニュー

Visual Studio の使用中に問題が発生した場合、または製品の改善案をお持ちの場合は、Visual Studio ウィンドウ上部の **[フィードバックの送信]** メニューを使用してください。

![Visual Studio の [フィードバックの送信] メニュー](../ide/media/quickstart-ide-send-feedback.png)

## <a name="next-steps"></a>次のステップ

ユーザー インターフェイスに慣れるため、Visual Studio の機能をいくつか確認しました。 下記に従って、さらに試してみてください。

> [!div class="nextstepaction"]
> [コード エディターについて学習する](write-and-edit-code.md)

> [!div class="nextstepaction"]
> [プロジェクトとソリューションについて学習する](../get-started/tutorial-projects-solutions.md)

## <a name="see-also"></a>参照

- [Visual Studio IDE の概要](../get-started/visual-studio-ide.md)
- [Visual Studio 2017 のその他の機能](../ide/advanced-feature-overview.md)
- [テーマとフォントの色を変更する](../ide/quickstart-personalize-the-ide.md)
