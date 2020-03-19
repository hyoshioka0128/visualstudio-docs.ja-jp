---
title: IDE をカスタマイズする
ms.date: 11/20/2017
ms.topic: conceptual
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 39c9edbf5e96a59912c0cf16d7b4178f6fba2a62
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75585744"
---
# <a name="personalize-the-visual-studio-ide"></a>Visual Studio IDE のカスタマイズ

ユーザー独自の開発スタイルと要件に最適なサポートを行うために Visual Studio をさまざまな方法でカスタマイズすることができます。 設定の多くは Visual Studio インスタンス間でローミングできます &mdash;[同期された設定](../ide/synchronized-settings-in-visual-studio.md)に関するページを参照してください。 この記事では、さまざまなカスタマイズ方法と、詳細情報の参照先について簡単に説明します。

> [!NOTE]
> このトピックは、Windows 上の Visual Studio に適用されます。 Visual Studio for Mac については、[Visual Studio for Mac IDE のカスタマイズ](/visualstudio/mac/customizing-the-ide)に関するページを参照してください。

## <a name="default-settings"></a>既定の設定

開発の種類に合わせて Visual Studio を最適化する既定の一連の設定を選択できます。 詳細については、[環境設定](environment-settings.md)に関するページを参照してください。

## <a name="general-environment-options"></a>一般的な環境オプション

多くのカスタマイズ オプションが [[環境オプション]](../ide/reference/general-environment-options-dialog-box.md) ダイアログ ボックスで公開されています。 このダイアログ ボックスにアクセスするには、次の 2 つの方法があります。

- メニュー バーで、 **[ツール]**  >  **[オプション]** の順に選択します。 **[環境]** ノードがまだ展開されていない場合は展開します。

- **Ctrl**+ キーを押しながら **Q** キーを押し、検索ボックスに「**環境**」と入力します。結果から **[環境] > [全般]** の順に選択します。

> [!TIP]
> [オプション] ダイアログ ボックスが表示されたら、**F1** キーを押して、そのページのさまざまな設定に関するヘルプを表示できます。

## <a name="environment-color-themes"></a>環境の配色テーマ

明色、暗色、青の配色テーマを変更するには、検索ボックスに「**環境**」と入力した後、 **[環境] > [全般]** の順に選択します。 **[オプション]** ダイアログ ボックスで、 **[配色テーマ]** オプションを変更します。

エディターで配色オプションを変更するには、検索ボックスに「**環境**」と入力した後、 **[環境] > [フォントおよび色]** の順に選択します。 「[方法: フォントと色を変更する](../ide/how-to-change-fonts-and-colors-in-visual-studio.md)」を参照してください。

### <a name="main-menu-casing"></a>メイン メニューの大文字小文字の区別

メイン メニューの大文字小文字の区別は、 **[タイトル文字]** ("File") と **[すべて大文字]** ("FILE") の間で変更できます。 検索ボックスに「**環境**」と入力し、 **[環境] > [全般]** の順に選択し、 **[タイトルの文字スタイルをメニュー バーに適用する]** オプションを変更します。

### <a name="customize-menus-and-toolbars"></a>メニューおよびツール バーをカスタマイズする

メニュー項目やツールバーの項目を追加または削除するには、「[方法: メニューおよびツールバーをカスタマイズする](../ide/how-to-customize-menus-and-toolbars-in-visual-studio.md)」を参照してください。

::: moniker range="vs-2017"

## <a name="start-page"></a>スタート ページ

自分とチームのカスタム スタート ページを作成するには、「[スタート ページのカスタマイズ](../ide/customizing-the-start-page-for-visual-studio.md)」を参照してください。

::: moniker-end

## <a name="window-layouts"></a>ウィンドウのレイアウト

複数のウィンドウ レイアウトを定義して保存し、それらを切り替えることができます。 たとえば、コーディング用の 1 つのレイアウトとデバッグ用のレイアウトを定義できます。 ウィンドウの位置と動作を設定し、カスタム レイアウトを保存するには、「[ウィンドウ レイアウトをカスタマイズする](../ide/customizing-window-layouts-in-visual-studio.md)」を参照してください。

## <a name="external-tools"></a>外部ツール

**[ツール]** メニューをカスタマイズして、外部ツールを起動することができます。 詳細については、「[外部ツールの管理](../ide/managing-external-tools.md)」を参照してください。

## <a name="see-also"></a>参照

- [環境設定](environment-settings.md)
- [Visual Studio IDE の概要](../get-started/visual-studio-ide.md)
- [クイックスタート: Visual Studio IDE の表示の紹介](../ide/quickstart-ide-orientation.md)
- [Visual Studio for Mac IDE のカスタマイズ](/visualstudio/mac/customizing-the-ide)
