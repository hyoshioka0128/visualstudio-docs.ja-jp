---
title: 配色テーマとフォントを設定する
ms.date: 11/20/2017
ms.topic: quickstart
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 11cd73574f42fffb7bcfcda5ab47496fe92565c7
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75596945"
---
# <a name="personalize-the-visual-studio-ide-and-editor"></a>Visual Studio IDE とエディターのカスタマイズ

この 5 分から 10 分程度のチュートリアルでは、ダーク テーマを選択して、Visual Studio の配色テーマをカスタマイズします。 テキスト エディターで 2 つの異なる種類のテキスト用の色もカスタマイズします。

::: moniker range="vs-2017"

Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) ページに移動し、無料試用版をインストールしてください。

::: moniker-end

::: moniker range=">=vs-2019"

Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads) ページに移動し、無料試用版をインストールしてください。

::: moniker-end

## <a name="set-the-color-theme"></a>配色テーマの設定

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

> [!TIP]
> **Visual Studio 配色テーマ エディター**を [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=VisualStudioPlatformTeam.VisualStudio2017ColorThemeEditor) からインストールして、定義済みテーマを追加でインストールすることもできます。 このツールをインストールすると、追加の配色テーマが **[配色テーマ]** ドロップダウン リストに表示されます。

## <a name="change-text-color"></a>テキストの色の変更

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

Visual Studio の色をカスタマイズするいくつかの方法について学習しました。 ぜひ **[オプション]** ダイアログ ボックスの他のカスタマイズ オプションも試して、Visual Studio を完全にカスタマイズしてください。

## <a name="see-also"></a>関連項目

- [エディターのカスタマイズ](../ide/how-to-change-text-case-in-the-editor.md)
- [Visual Studio IDE の概要](../get-started/visual-studio-ide.md)
