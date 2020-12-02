---
title: '[全般] ([オプション] ダイアログ ボックス - [環境])'
ms.date: 07/26/2019
ms.topic: reference
f1_keywords:
- VS.Environment.General
- VS.Message.0x800a002e
- VS.OptionsDialog.Environment
- VS.ToolsOptionsPages.Environment
- VS.ToolsOptionsPages.Environment.General
helpviewer_keywords:
- recently used file lists
- Windows menu, customizing
- status bar, displaying
- Options dialog box, General Environment
- General Environment Options dialog box
- Environment Options dialog box
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: dfd1b876e58c05c668fd74087d5131bb1e9fcd40
ms.sourcegitcommit: b1b747063ce0bba63ad2558fa521b823f952ab51
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "96189785"
---
# <a name="options-dialog-box-environment--general"></a>[オプション] ダイアログ ボックス:[環境] \> [全般]

このページを使用して、統合開発環境 (IDE: Integrated Development Environment) のオプションのうち特に配色テーマ、ステータス バーの設定、およびファイル拡張子の関連付けを変更します。 **[オプション]** ダイアログ ボックスを表示するには、 **[ツール]** メニューを開いて、 **[オプション]** をクリックし、 **[環境]** フォルダーを開き、 **[全般]** ページをクリックします。

## <a name="visual-experience"></a>視覚的効果

**配色テーマ**

IDE の配色テーマ (**[青]**、**[淡色]**、**[濃色]**、または **[青 (エクストラ コントラスト)]**) を選択します。

[Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=VisualStudioPlatformTeam.VisualStudio2017ColorThemeEditor) から **Visual Studio 配色テーマ エディター** をダウンロードしてインストールすることで、定義済みテーマを追加でインストールしたりカスタム テーマを作成したりすることもできます。 このツールをインストールすると、追加の配色テーマが **[配色テーマ]** ボックスの一覧に表示されます。

**タイトルの文字スタイルをメニュー バーに適用する**

メニューでは、タイトルの大文字と小文字のスタイルが既定で使用されます。 すべて大文字のスタイルを使用するには、このオプションをオフにします。

::: moniker range=">=vs-2019"

**ピクセルの密度が異なる画面のレンダリングを最適化する (再起動が必要)**

このオプションを使用して、モニターごとの 1インチあたりのドット数 (DPI) の認識 (または *PMA*) を有効または無効にします。 PMA を有効にすると、Visual Studio ユーザー インターフェイスは、表示倍率と DPI 構成に関係なく、すべてのモニターで鮮明に表示されます (複数のモニター間の表示も含まれます)。 PMA を有効にするには、Windows 10 April 2018 Update 以降および .NET Framework 4.8 以降が必要です  (これら 2 つの前提条件が満たされていない場合、このオプションは灰色表示されます)。

> [!TIP]
> - Windows 10 には、**[Let Windows try to fix apps so they're not blurry]\(ぼやけないように Windows でアプリの修正を試みる\)** という設定があります。 **[Optimize rendering for screens with different pixel densities]\(ピクセルの密度が異なる画面のレンダリングを最適化する\)** オプションがオンの場合は、この Windows 設定を **オン** にしても、効果はほとんどありません。
> - Windows 10 には、**[プログラム互換性のトラブルシューティング ツール]** という設定もあります。 Visual Studio の外観の修正を試みるときは、このトラブルシューティング ツールを使用しないことをお勧めします。

::: moniker-end

**クライアントのパフォーマンスに基づいて視覚的効果を自動的に調整する**

Visual Studio で視覚的効果を自動的に調整するか、ユーザーが明示的に調整するかを指定します。 この調整によって、色の表示がグラデーションからフラットに変わったり、メニューまたはポップアップ ウィンドウでのアニメーションの使用が制限されたりすることがあります。

::: moniker range="vs-2017"

> [!TIP]
> Windows 10 には、**[Let Windows try to fix apps so they're not blurry]\(ぼやけないように Windows でアプリの修正を試みる\)** という設定があります。 Visual Studio がモニター上でぼやけて見える場合は、この設定を **オン** にすることをお勧めします。 [Visual Studio 2019](https://visualstudio.microsoft.com/downloads) へのアップグレードを検討してください。Visual Studio 2019 は、モニターごとの DPI に対応したアプリケーションであるため、表示の明瞭度が大幅に向上しています。

::: moniker-end

**リッチ クライアント エクスペリエンスを有効にする**

グラデーションやアニメーションなど、Visual Studio の視覚的効果のすべてを有効にします。 リモート デスクトップ接続や古いグラフィックス アダプターを使用している場合は、これらの機能のパフォーマンスが低下する可能性があるため、このオプションをオフにします。 このオプションをオンにできるのは、**[クライアントのパフォーマンスに基づいて視覚的効果を自動的に調整する]** をオフにした場合だけです。

**可能ならハードウェアのグラフィックス アクセラレータを使用する**

可能な場合は、ソフトウェア アクセラレータではなく、ハードウェアのグラフィックス アクセラレータを使用します。

## <a name="other"></a>その他

**ウィンドウ メニューに表示する項目**

**[ウィンドウ]** メニューの [ウィンドウ] の一覧に表示されるウィンドウ数をカスタマイズします。 1 から 24 の範囲の数字を入力してください。 既定値は 10 です。

**項目を最近使用した一覧に表示**

**[ファイル]** メニューに表示される、最近使ったプロジェクトとファイルの数をカスタマイズします。 1 から 24 の範囲の数字を入力してください。 既定値は 10 です。 このオプションを使用すると、最近使用したプロジェクトやファイルを簡単に表示できます。

**ステータス バーの表示**

ステータス バーが表示されます。 ステータス バーは IDE ウィンドウの一番下にあり、処理中の操作の進行状況が表示されます。

**[Close button affects active tool window only] ([閉じる] ボタンを、アクティブになっているツール ウィンドウに対してのみ実行する\)**

**[閉じる]** をクリックしたときに、ドッキング セット内のすべてのツール ウィンドウではなく、フォーカスのあるツール ウィンドウだけを閉じるように指定します。 既定では、このオプションが選択されています。

**[Auto Hide button affects active tool window only] ([自動的に隠す] ボタンを、アクティブになっているツール ウィンドウに対してのみ実行する\)**

**[自動的に隠す]** をクリックしたときに、ドッキング セット内のすべてのツール ウィンドウではなく、フォーカスのあるツール ウィンドウだけを自動的に非表示にするように指定します。 既定では、このチェック ボックスはオフになっています。

## <a name="see-also"></a>関連項目

- [ウィンドウ レイアウトをカスタマイズする](../../ide/customizing-window-layouts-in-visual-studio.md)
