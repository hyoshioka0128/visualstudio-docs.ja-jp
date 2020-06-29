---
title: フォントと色を変更する
ms.date: 06/01/2020
ms.topic: how-to
helpviewer_keywords:
- Visual Studio, color themes
- color themes, Visual Studio
ms.assetid: 60d91ba1-244b-4c43-847f-60b744f1352a
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0eb2373117b382cb19f374581ada45a5732b9c4c
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85284687"
---
# <a name="how-to-change-fonts-and-colors-in-visual-studio"></a>方法: Visual Studio で使用するフォントと色を変更する

Visual Studio では、さまざまな方法でフォントと色を変更できます。 たとえば、既定の青の配色テーマをダークテーマ ("ダーク モード" とも呼ばれます) に変更できます。また、既定のフォントおよびテキスト サイズを別のフォントとサイズに変更することもできます。

## <a name="change-the-color-theme"></a>[配色テーマ] を変更する

ここでは、Visual Studio で IDE フレームとツール ウィンドウの配色テーマを変更する方法について説明します。

1. メニュー バーで、 **[ツール]**  >  **[オプション]** の順に選択します。

1. オプションの一覧で、 **[環境]**  >  **[全般]** の順に選びます。

1. **[配色テーマ]** の一覧で、既定の **[青]** のテーマ、 **[ライト]** テーマ、 **[ダーク]** テーマ、または **[青 (エクストラ コントラスト)]** テーマのいずれかを選択します。

   ![配色テーマを変更する [オプション] ダイアログ ボックスのスクリーンショット](media/fonts-colors-theme.png "配色テーマを変更するために使用できる [オプション] ダイアログ ボックスのスクリーンショット")

    > [!NOTE]
    > テーマの色を変更すると、IDE のテキストは既定値またはそのテーマについて前にカスタマイズしたフォントとサイズに戻ります。

    :::moniker range="vs-2017"

    > [!TIP]
    > [Color Theme Editor for Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=VisualStudioPlatformTeam.VisualStudio2017ColorThemeEditor) をインストールすることで、Visual Studio のテーマを作成して編集できます。

    :::moniker-end

    :::moniker range="vs-2019"

    > [!TIP]
    > [Visual Studio Color Theme Designer](https://marketplace.visualstudio.com/items?itemName=ms-madsk.ColorThemeDesigner) をインストールすることで、Visual Studio のテーマを作成して編集できます。

    :::moniker-end

## <a name="change-fonts-and-text-size"></a>フォントとテキスト サイズの変更

すべての IDE フレームおよびツール ウィンドウのフォントとテキスト サイズを変更することも、特定のウィンドウまたはテキスト要素についてのみ変更することもできます。 エディター内のフォントとテキスト サイズも変更できます。

### <a name="to-change-the-font-and-text-size-in-the-ide"></a>IDE 内のフォントとテキスト サイズを変更するには

1. メニュー バーで、 **[ツール]**  >  **[オプション]** の順に選択します。

1. オプションの一覧で、 **[環境]**  >  **[フォントおよび色]** の順に選びます。

1. **[設定の表示]** の一覧で、 **[環境]** を選びます。

   ![IDE 内のフォントと色を変更するための [オプション] ダイアログ ボックスのスクリーンショット](media/fonts-colors-environment.png "IDE 内のフォントと色を変更するための [オプション] ダイアログ ボックスのスクリーンショット")

    > [!NOTE]
    > ツール ウィンドウのみのフォントを変更する場合は、 **[設定の表示]** の一覧で、 **[すべてのテキスト ツール ウィンドウ]** を選びます。

1. IDE のフォントとテキスト サイズを変更するには、 **[フォント]** および **[サイズ]** オプションを変更します。

1. **[表示項目]** で適切な項目を選択し、 **[前景色]** および **[背景色]** オプションを変更します。

### <a name="to-change-the-font-and-text-size-in-the-editor"></a>エディターでフォントとテキスト サイズを変更するには

1. メニュー バーで、 **[ツール]**  >  **[オプション]** の順に選択します。

1. オプションの一覧で、 **[環境]**  >  **[フォントおよび色]** の順に選びます。

1. **[設定の表示]** の一覧の **[テキスト エディター]** を選択します。

   ![エディター内のフォントと色を変更するための [オプション] ダイアログ ボックスのスクリーンショット](media/fonts-colors-text-editor.png "エディター内のフォントと色を変更するための [オプション] ダイアログ ボックスのスクリーンショット")

1. エディターのフォントとテキスト サイズを変更するには、 **[フォント]** および **[サイズ]** オプションを変更します。

1. **[表示項目]** で適切な項目を選択し、 **[前景色]** および **[背景色]** オプションを変更します。

詳細については、[エディターのフォントと色の変更](../ide/reference/how-to-change-fonts-and-colors-in-the-editor.md)に関するページを参照してください。

## <a name="accessibility-options"></a>アクセシビリティ オプション

色覚に障がいがある方のために、配色テーマのオプションがあります。 コンピューター上の "*すべて*" のアプリと UI に対するハイコントラスト オプション、または Visual Studio 専用のエクストラ コントラスト オプションを使用できます。

### <a name="use-windows-high-contrast"></a>Windows のハイ コントラストを使用する

Windows のハイ コントラスト オプションを切り替えるには、次のいずれかの手順を使用します。

- Windows または任意の Microsoft アプリケーションで、**左 Alt**+**左 Shift**+**PrtScn** キーを押します。

- Windows で、 **[スタート]**  >  **[設定]**  >  **[簡単操作]**  >  **[ハイ コントラスト]** を選択します。

    > [!WARNING]
    > Windows のハイ コントラスト設定は、コンピューター上のすべてのアプリケーションと UI に影響します。

### <a name="use-visual-studio-extra-contrast"></a>Visual Studio のエクストラ コントラストを使用する

Visual Studio のエクスロラ コントラスト オプションを切り替えるには、次の手順を使用します。

1. Visual Studio のメニュー バーで、 **[ツール]**  >  **[オプション]** を選択し、オプションの一覧で **[環境]**  >  **[全般]** を選択します。

1. **[配色テーマ]** ドロップダウン リストで、 **[青 (エクストラ コントラスト)]** テーマを選択し、 **[OK]** を選択します。

使用できるその他の Visual Studio アクセシビリティ オプションの詳細については、「[Visual Studio のユーザー補助機能](../ide/reference/accessibility-features-of-visual-studio.md)」ページを参照してください。

> [!TIP]
> 役に立つと思われるものの、Visual Studio では現在使用できない色やフォントのアクセシビリティ オプションがある場合は、[Visual Studio Developer Community](https://developercommunity.visualstudio.com/) で **[機能を提案する]** を選択してお知らせください。 このフォーラムとそのしくみの詳細については、[機能の提案](../ide/suggest-a-feature.md)に関するページを参照してください。

## <a name="next-steps"></a>次の手順

フォントおよび配色を変更できるすべてのユーザー インターフェイス (UI) 要素の詳細については、「[[フォントおよび色] ([オプション] ダイアログ ボックス - [環境])](../ide/reference/fonts-and-colors-environment-options-dialog-box.md)」ページを参照してください。

## <a name="see-also"></a>関連項目

- [コード エディターのフォントと色を変更する](../ide/reference/how-to-change-fonts-and-colors-in-the-editor.md)
- [Visual Studio のコード エディターの機能](../ide/writing-code-in-the-code-and-text-editor.md)