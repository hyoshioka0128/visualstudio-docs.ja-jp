---
title: Visual Studio ダーク テーマの設定とテキストの色の変更
description: Visual Studio の既定の配色テーマをダーク モードに変更し、コード エディターのフォントの色を変更する方法について説明します。
ms.date: 08/20/2020
ms.topic: how-to
ms.custom: contperfq1
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d58bf3a00d3db208abfad23a67bd115914f14a15
ms.sourcegitcommit: a801ca3269274ce1de4f6b2c3f40b58bbaa3f460
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88801400"
---
# <a name="how-to-personalize-the-visual-studio-ide-and-the-editor"></a>方法: Visual Studio IDE とエディターのカスタマイズ

このハウツー記事では、Visual Studio の配色テーマを既定の青のテーマからダーク テーマにカスタマイズします。 その後、コード エディターで 2 つの異なる種類のテキストの色をカスタマイズします。

::: moniker range="vs-2017"

Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) ページに移動し、無料試用版をインストールしてください。

::: moniker-end

::: moniker range=">=vs-2019"

Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads) ページに移動し、無料試用版をインストールしてください。

::: moniker-end

## <a name="set-the-color-theme-for-the-ide"></a>IDE の配色テーマを設定する

Visual Studio のユーザー インターフェイスの既定の配色テーマは、 **[青]** です。 このテーマを **[濃色]** に変えてみましょう。

1. メニュー バー ( **[ファイル]** や **[編集]** などのメニューの行) で、 **[ツール]**  >  **[オプション]** の順に選択します。

1. **[環境]**  >  **[全般]** オプションのページで、 **[配色テーマ]** の選択内容を **[濃色]** に変更して **[OK]** を選択します。

   Visual Studio 開発環境 (IDE) 全体の配色テーマが、 **[濃色]** に変更されます。

   ::: moniker range="vs-2017"

   ![ダーク テーマの Visual Studio 2017](media/quickstart-personalize-dark-theme.png)

   ::: moniker-end

   ::: moniker range="vs-2019"

   ![ダーク テーマの Visual Studio 2019](media/vs-2019/dark-theme.png)

   ::: moniker-end

::: moniker range="vs-2017"

> [!TIP]
> **Visual Studio 配色テーマ エディター**を [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=VisualStudioPlatformTeam.VisualStudio2017ColorThemeEditor) からインストールして、定義済みテーマを追加でインストールすることもできます。 このツールをインストールすると、追加の配色テーマが **[配色テーマ]** ドロップダウン リストに表示されます。

::: moniker-end

::: moniker range="vs-2019"

> [!TIP]
> **Visual Studio 配色テーマ デザイナー**を [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-madsk.ColorThemeDesigner) からインストールして、独自のテーマを作成できます。

::: moniker-end

## <a name="change-text-colors-in-the-editor"></a>エディターのテキストの色を変更する

次に、エディターのテキストの色をいくつかカスタマイズします。 まず、新しい XML ファイルを作成して既定の色を確認しましょう。

1. メニュー バーの **[ファイル]** 、 **[新規作成]** 、 **[ファイル]** の順に選択します。

1. **[新しいファイル]** ダイアログ ボックスの **[全般]** カテゴリで **[XML ファイル]** を選択し、 **[開く]** を選択します。

1. `<?xml version="1.0" encoding="utf-8"?>` が含まれる行の下に、以下の XML を貼り付けます。

   ```xml
   <Catalog>
     <Book id="bk101">
     <Author>Garghentini, Davide</Author>
     <Title>XML Developer's Guide</Title>
     <Genre>Computer</Genre>
     <Price>44.95</Price>
     <PublishDate>2000-10-01</PublishDate>
     <Description>
       An in-depth look at creating applications with XML.
     </Description>
   </Book>
   <Book id="bk102">
     <Author>Garcia, Debra</Author>
     <Title>Midnight Rain</Title>
     <Genre>Fantasy</Genre>
     <Price>5.95</Price>
     <PublishDate>2000-12-16</PublishDate>
     <Description>
       A former architect battles corporate zombies, an evil
       sorceress, and her own childhood to become queen of the world.
     </Description>
   </Book>
   </Catalog>
   ```

   行番号は水色、XML 属性 (`id="bk101"` など) は薄い青色であることに注意してください。 これらの項目のテキストの色を変更します。

   ![XML ファイルのフォントの色](media/quickstart-personalize-xml-file.png)

1. **[オプション]** ダイアログ ボックスを開くには、メニュー バーから **[ツール]**  >  **[オプション]** の順に選択します。

1. **[環境]** で **[フォントおよび色]** カテゴリを選択します。

   **[設定の表示]** の下のテキストは **[テキスト エディター]** になっています&mdash;これは、これから設定を行うテキスト エディターです。 このドロップダウン リストを展開すると、フォントおよびテキストの色をカスタマイズできる場所の詳細な一覧が表示されます。

1. 行番号のテキストの色を変更するため、 **[表示項目]** リストで **[行番号]** を選択します。 **[前景色]** ボックスで **[オリーブ]** を選択します。

   ![[オプション] ダイアログ ボックスの [フォントおよび色] カテゴリ](media/quickstart-personalize-line-number-color.png)

   一部の言語には、それぞれに特有のフォントと色の設定があります。 たとえば、C++ の開発者が関数に使用する色を変更したい場合、 **[表示項目]** リストで **[C++ 関数]** を探します。

1. ダイアログ ボックスを閉じる前に、XML 属性の色も変更しましょう。 **[表示項目:]** リストで **[XML 属性]** までスクロールし、選択します。 **[前景色]** ボックスで、 **[ライム]** を選択します。 **[OK]** を選択して選択内容を保存し、ダイアログ ボックスを閉じます。

   行番号がオリーブ色に、XML 属性が明るいライム グリーンに変わりました。 C++ や C# のコード ファイルなど、別の種類のファイルを開いた場合でも、行番号はオリーブ色で表示されます。

   ![新しいフォントの色が設定された XML ファイル](media/quickstart-personalize-xml-file-new-colors.png)

Visual Studio の色をカスタマイズするいくつかの方法について学習しました。 Visual Studio を自分の好みに合わせて完全にカスタマイズするために、[ **[オプション]** ](../ide/reference/fonts-and-colors-environment-options-dialog-box.md) ダイアログ ボックスの他のカスタマイズ オプションも試してみることをお勧めします。

## <a name="see-also"></a>関連項目

- [方法: Visual Studio のフォント、色、テーマを変更する](../ide/how-to-change-fonts-and-colors-in-visual-studio.md)
- [方法 : エディター内のテキストの大文字と小文字を変更する](../ide/how-to-change-text-case-in-the-editor.md)
- [Visual Studio IDE の概要](../get-started/visual-studio-ide.md)
