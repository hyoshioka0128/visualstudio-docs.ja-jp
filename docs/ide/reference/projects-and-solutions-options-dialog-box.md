---
title: '[プロジェクトおよびソリューション] の [オプション] ダイアログ ボックス'
description: '[プロジェクトおよびソリューション] セクションの [全般] ページを使用して、プロジェクトおよびソリューションに関連する Visual Studio の動作を定義する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 07/26/2019
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Projects.General
helpviewer_keywords:
- Projects and Solutions Options dialog box
- Options dialog box, Projects and Solutions
ms.assetid: 2801f24e-a138-488a-ae3c-e1f99a678ac0
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 2fab59a590b59452362a47d48bcdfa7dd8661f57
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99907507"
---
# <a name="options-dialog-box-projects-and-solutions--general"></a>[オプション] ダイアログ ボックス:[プロジェクトおよびソリューション]\> [全般]

このページを使用して、プロジェクトおよびソリューションに関連する Visual Studio の動作を定義します。 これらのオプションにアクセスするには、 **[ツール]** 、 **[オプション]** の順に選択し、 **[プロジェクトおよびソリューション]** を展開し、 **[全般]** をクリックします。

**[全般]** ページで使用できるオプションは次のとおりです。

## <a name="always-show-error-list-if-build-finishes-with-errors"></a>ビルドがエラーで終了した場合には常にエラー一覧を表示する

プロジェクトのビルドが失敗した場合にのみ、ビルドの完了時に [**エラー一覧**] ウィンドウを開きます。 ビルド処理中に発生したエラーが表示されます。 このオプションがオフの場合、エラーは引き続き発生しますが、ビルドの完了時にウィンドウは開きません。 このオプションは、既定で有効です。

## <a name="track-active-item-in-solution-explorer"></a>ソリューション エクスプローラーでアクティブなアイテムを追跡する

選択した場合、**ソリューション エクスプローラー** が自動的に開いて、アクティブな項目が選択されます。 選択される項目は、プロジェクトまたはソリューション内の別のファイルや、デザイナー内の異なるコンポーネントを処理の対象にすると変更されます。 このオプションがオフのとき、**ソリューション エクスプローラー** での選択内容は自動的に変更されません。 このオプションは、既定で有効です。

## <a name="show-advanced-build-configurations"></a>ビルド構成の詳細を表示

選択した場合、ビルドの構成オプションが [**プロジェクト プロパティ ページ**] ダイアログ ボックスおよび [**ソリューション プロパティ ページ**] ダイアログ ボックスに表示されます。 オフにすると、ビルドの構成オプションは、1 つの構成または 2 つの構成のデバッグとリリースを含む Visual Basic および C# プロジェクトのための、[**プロジェクト プロパティ ページ**] ダイアログ ボックスや [**ソリューション プロパティ ページ**] ダイアログ ボックスに表示されません。 プロジェクトにユーザー定義の構成がある場合、ビルドの構成オプションが表示されます。

オフの場合、[**ビルド**] メニューのコマンド ([**ソリューションのビルド**]、[**ソリューションのリビルド**]、[**ソリューションのクリーン**] など) はリリース構成で実行され、[**デバッグ**] メニューのコマンド ([**デバッグ開始**]、[**デバッグなしで開始**] など) はデバッグ構成で実行されます。

## <a name="always-show-solution"></a>常にソリューションを表示

選択した場合、ソリューションおよびソリューションで動作するすべてのコマンドが常に IDE に表示されます。 オフの場合、すべてのプロジェクトはスタンドアロン プロジェクトとして作成され、ソリューションに 1 つのプロジェクトだけが含まれている場合、ソリューション エクスプローラー内のソリューションや、IDE 内のソリューションで動作するコマンドは表示されません。

::: moniker range="vs-2017"

## <a name="save-new-projects-when-created"></a>新しいプロジェクトを作成時に保存する

選択すると、[**新しいプロジェクト**] ダイアログ ボックスにプロジェクトの場所を指定できます。 オフの場合、すべての新しいプロジェクトは一時プロジェクトとして作成されます。 一時プロジェクトで作業する場合、ディスクの場所を指定しなくても、プロジェクトを作成して試してみることができます。

::: moniker-end

## <a name="warn-user-when-the-project-location-is-not-trusted"></a>プロジェクトの場所が信頼されていないときにユーザーに警告

完全に信頼されていない場所 (UNC パスの上や HTTP パスの上など) で、新しいプロジェクトの作成または既存のプロジェクトのオープンを試行すると、メッセージが表示されます。 このオプションを使用して、完全に信頼されていない場所でプロジェクトの作成またはオープンを試行するたびにメッセージを表示するかどうかを指定します。

## <a name="show-output-window-when-build-starts"></a>ビルド開始時に出力ウィンドウを表示

ソリューション ビルドの開始時に、IDE の[出力ウィンドウ](../../ide/reference/output-window.md)を自動的に表示します。

## <a name="prompt-for-symbolic-renaming-when-renaming-files"></a>ファイル名の変更時にシンボルの名前変更を求めるプロンプトを出す

選択すると、Visual Studio がコード要素に対するプロジェクト内のすべての参照も名前変更するかどうかを確認する、メッセージ ボックスが表示されます。

## <a name="prompt-before-moving-files-to-a-new-location"></a>Prompt before moving files to a new location\(新しい場所にファイルを移動する前にメッセージを表示する\)

選択すると、Visual Studio は、**ソリューション エクスプローラー** での操作によってファイルの場所が変更される前に確認メッセージ ボックスを表示します。

## <a name="reopen-documents-on-solution-load"></a>ソリューションの読み込み時にドキュメントを再度開く

オンにすると、前にこのソリューションを閉じたときに開かれていたドキュメントが、ソリューションを読み込むときに自動的に開かれます。

特定の種類のファイルまたはデザイナーを開きなおすと、ソリューションの読み込みが遅くなることがあります。 ソリューションの以前のコンテキストを復元する必要がない場合は、このオプションをオフにすると、[ソリューションの読み込みのパフォーマンス](../../ide/visual-studio-performance-tips-and-tricks.md#disable-automatic-file-restore)が向上します。

::: moniker range=">=vs-2019"

## <a name="restore-solution-explorer-project-hierarchy-state-on-solution-load"></a>ソリューションの読み込み時に、ソリューション エクスプローラーのプロジェクトの階層状態を復元する

選択されている場合、ソリューションが最後に開かれたとき、それが展開されていたか折りたたまれていたかについて、ソリューション エクスプローラーのノードの状態が復元されます。 大規模なソリューションでソリューションの読み込み時間を短縮するには、このオプションをオフにします。

> [!TIP]
> このオプションが無効なとき、**[ソリューション エクスプローラー]** ツールバーで **[アクティブ ドキュメントとの同期]** を選択すると、ソリューション エクスプローラーでアクティブなドキュメントに簡単に移動できます。
>
> ![ソリューション エクスプローラーでの [アクティブ ドキュメントとの同期]](media/sync-active-document.png)

## <a name="open-sdk-style-project-files-with-double-click-or-the-enter-key"></a>ダブルクリックまたは Enter キーで、SDK スタイルのプロジェクト ファイルを開く

このオプションがオンのとき、ソリューション エクスプローラーで SDK スタイルのプロジェクト ノードをダブルクリックするか、それを選択して **Enter** キーを押した場合、エディターでそのプロジェクト ファイル (たとえば、\*.csproj file) は XML として開きます。 オフの場合、ソリューション エクスプローラーで SDK スタイルのプロジェクト ノードをダブルクリックするか、それを選択して **Enter** キーを押すと、ノードのみが展開または折りたたまれます。

このオプションがオフのときに SDK スタイルのプロジェクト ファイルを編集したい場合は、ソリューション エクスプローラーでプロジェクト ノードを右クリックし、**[プロジェクト ファイルの編集]** を選択します。 その他の種類のプロジェクトでは、Visual Studio でプロジェクトを編集する前に、まずプロジェクトをアンロードする必要があります。

> [!TIP]
> *SDK スタイルのプロジェクト* または [プロジェクト SDK](../../msbuild/how-to-use-project-sdk.md) には、MSBuild 15.0 で導入された、より新しいより効率的なスタイルのプロジェクト ファイルがあります。 SDK スタイルのプロジェクトの `Project` 要素には `Sdk` 属性が含まれています (例: `<Project Sdk="Microsoft.NET.Sdk">`)。 Visual Studio では、たとえば Visual Studio テンプレートの 1 つを使用して新しい .NET Core プロジェクトを作成すると、SDK スタイルのプロジェクトが作成されます。

::: moniker-end

## <a name="see-also"></a>関連項目

- [[オプション] ダイアログ ボックス:[プロジェクトおよびソリューション] \> [場所]](projects-solutions-locations-options.md)
- [[オプション] ダイアログ ボックス、[プロジェクトおよびソリューション]、[ビルド/実行]](../../ide/reference/options-dialog-box-projects-and-solutions-build-and-run.md)
- [[オプション] ダイアログ ボックス、[プロジェクトおよびソリューション]、[Web プロジェクト]](../../ide/reference/options-dialog-box-projects-and-solutions-web-projects.md)
