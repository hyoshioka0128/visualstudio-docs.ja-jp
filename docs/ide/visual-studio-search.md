---
title: Visual Studio Search を使用する
description: Visual Studio の検索を使用して、設定、メニュー、コードを検索する方法について説明します。
ms.date: 10/08/2020
ms.topic: how-to
helpviewer_keywords:
- environments [Visual Studio], navigation
- documents [Visual Studio], navigating
- IDE, navigation
- navigation [Visual Studio]
- files [Visual Studio], navigating between
- windows [Visual Studio], navigating
- Window.QuickLaunch
- IDE navigator
ms.assetid: 3870a8fd-4afa-4f1e-a811-9fdf41a9e82d
monikerRange: vs-2019
author: profexorgeek
ms.author: jusjohns
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b9f8182646af4facb0f2f86c74f95dff091d55d1
ms.sourcegitcommit: cea9e5787ff33e0e18aa1942bf4236748e0ef547
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92199695"
---
# <a name="use-visual-studio-search"></a>Visual Studio の検索を使用する

Visual Studio 統合開発環境 (IDE) には、多くのメニュー、オプション、機能があり、覚えにくい場合があります。 Visual Studio の検索機能は、開発者がコードを検索しながら IDE のメニューとオプションを検索するのに役立つ単一の検索ボックスです。 Visual Studio を初めて使用する場合でも、経験豊富な開発者の方でも、この機能を使用すると、IDE の機能とコードを簡単に検索できます。

キーボード ショートカット **Ctrl**+**Q** キーを使用して検索ボックスにアクセスするか、既定でメニュー バーの横にある Visual Studio の検索入力ボックスをクリックします。

:::image type="content" source="media/visual-studio-search-cropped.png" alt-text="Visual Studio の検索ボックス" lightbox="media/visual-studio-search.png":::

> [!NOTE]
> Visual Studio の検索によって実行されるコマンドは `Window.QuickLaunch` です。この機能はクイック検索またはクイック起動と呼ばれる場合があります。

"フォルダーを指定して検索" や "ソリューション エクスプローラーの検索" などの他の検索機能とは異なり、Visual Studio の結果の検索には、IDE の機能、メニュー オプション、ファイル名などが含まれます。 以降のセクションでは、Visual Studio の検索で見つけることができるさまざまな種類の結果について説明します。

## <a name="search-menus-options-and-windows"></a>メニュー、オプション、ウィンドウの検索

Visual Studio の検索ボックスを使用して、設定、オプション、および同様の構成項目を見つけることができます。 たとえば Visual Studio の配色テーマを変更できるダイアログをすばやく見つけて開くには、次のスクリーンショットに示されているように、" *テーマの変更* " を検索します。

:::image type="content" source="media/visual-studio-search-options.png" alt-text="Visual Studio の検索ボックス":::

> [!TIP]
> Visual Studio の検索を使用すると、ほとんどの場合、メニュー、ショートカット キー、結果内の各項目の場所も通知されます。

Visual Studio の検索ボックスを使用して、メニュー項目とコマンドを検索できます。 たとえば、 *clean sol* を検索して、Clean Solution (ソリューションのクリーン) コマンドをすばやく見つけて実行します。 次のスクリーンショットに示されているように、検索結果には、このコマンドがメニューのどこにあるかも示されます。

:::image type="content" source="media/visual-studio-search-menu.png" alt-text="Visual Studio の検索ボックス" を検索します。

:::image type="content" source="media/visual-studio-search-window.png" alt-text="Visual Studio の検索ボックス":::

## <a name="search-files-and-code"></a>ファイルとコードの検索

また、Visual Studio の検索を使用すると、ファイル名、コード、メソッド、およびその他の一致するソリューション項目も検索されます。 次のスクリーンショットは、 *markdown* の検索によって、MarkdownMetaExtractor.cs ファイル、`MarkdownMetaExtractor` クラス、および 2 つのメソッドがソリューション内で見つったことを示しています。

:::image type="content" source="media/visual-studio-search-files.png" alt-text="Visual Studio の検索ボックス" 検索を実行することもできます。 次のスクリーンショットは、 *FSS* の検索で、 **F** older **S** ize **S** canner のファイル、クラス、メソッドが見つかったことを示しています。

:::image type="content" source="media/visual-studio-search-camel.png" alt-text="Visual Studio の検索ボックス":::

## <a name="see-also"></a>関連項目

- [Visual Studio コマンド](reference/visual-studio-commands.md)