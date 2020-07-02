---
title: フォントと書式設定
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: c3c3df69-83b4-4fd0-b5b1-e18c33f39376
caps.latest.revision: 6
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3e88f314ccdf2b91215fdfe579741591c7eb724d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544210"
---
# <a name="fonts-and-formatting-for-visual-studio"></a>Visual Studio のフォントと書式設定
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

## <a name="the-environment-font"></a><a name="BKMK_TheEnvironmentFont"></a>環境フォント
 カスタマイズするには、Visual Studio 内のすべてのフォントがユーザーに公開されている必要があります。 これは、主に [**ツール > オプション**] ダイアログボックスの [**フォントおよび色**] ページで行います。 フォント設定には、主に次の3つのカテゴリがあります。

- **環境フォント**-IDE (統合開発環境) の主要なフォント。ダイアログ、メニュー、ツールウィンドウ、ドキュメントウィンドウを含むすべてのインターフェイス要素に使用されます。 既定では、環境フォントは、現在のバージョンの Windows で 9 pt Segoe UI として表示されるシステムフォントに関連付けられています。 すべてのインターフェイス要素に1つのフォントを使用すると、IDE 全体で一貫したフォントの外観を確保できます。

- **テキストエディター** : コードおよびその他のテキストベースのエディターで表示される要素は、[**ツール > オプション]** の [テキストエディター] ページでカスタマイズできます。

- **特定のコレクション**-インターフェイス要素のユーザーカスタマイズを提供するデザイナーウィンドウは、[**ツール > オプション]** の独自の設定ページで、デザインサーフェイスに固有のフォントを公開する場合があります。

### <a name="editor-font-customization-and-resizing"></a>エディターのフォントのカスタマイズとサイズ変更
 ユーザーは、一般的なユーザーインターフェイスに関係なく、エディター内のテキストのサイズや色を設定に応じて拡大または縮小することがよくあります。 環境フォントは、エディターまたはデザイナーの一部としてまたはの一部として表示される要素で使用されるため、これらのフォント分類のいずれかが変更された場合は、予期される動作に注意する必要があります。

 エディターに表示されるが*コンテンツ*に含まれない UI 要素を作成する場合は、要素が予測可能な方法でサイズ変更されるように、テキストフォントではなく環境フォントを使用することが重要です。

1. エディターのコードテキストの場合は、[コードテキストのフォント] 設定でサイズを変更し、エディターのテキストのズームレベルに応答します。

2. インターフェイスの他のすべての要素は、環境のフォント設定に関連付けられており、環境内のグローバルな変更に対応している必要があります。 これには次のものが含まれます (ただし、に限定されません)。

    - コンテキストメニュー内のテキスト

    - 電球のメニューテキスト、クイック検索エディターペイン、ウィンドウに移動するなど、エディターの表示要素内のテキスト

    - [フォルダーを選択して検索] や [リファクター] など、ダイアログボックス内のテキストにラベルを付ける

### <a name="accessing-the-environment-font"></a>環境フォントへのアクセス
 ネイティブコードまたは WinForms コードでは、SID_SUIHostLocale サービスからインターフェイスを照会した後、 **Iuihostlocale:: Get フォント**メソッドを呼び出すことによって、環境フォントにアクセスできます。

 Windows Presentation Foundation (WPF) の場合は、WPF の**ウィンドウ**クラスではなく、シェルの表示**ウィンドウ**クラスからダイアログウィンドウクラスを派生させます。

 XAML では、コードは次のようになります。

```
<ui:DialogWindow
    x:Class"MyNameSpace.MyWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:s="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:ui="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.11.0"
    ShowInTaskbar="False"
    WindowStartupLocation="CenterOwner"
    Title="My Dialog">
</ui:DialogWindow>

code behind:

internal partial class WebConfigModificationWindow : DialogWindow
{
}

```

 (は `Microsoft.VisualStudio.Shell.11.0` 、MPF dll の現在のバージョンに置き換えてください)。

 ダイアログを表示するには、クラスで**ShowDialog ()** を介して "**showmodal ()**" を呼び出します。 **Showmodal ()** は、シェルで正しいモーダル状態を設定し、ダイアログが親ウィンドウの中央に配置されるようにします。

 コードは次のとおりです。

```
MyWindow window = new MyWindow();
window.ShowModal()

```

 **Showmodal**はブール値を返しますか? (null 許容のブール値) を使用する**と、必要**に応じて使用できます。 ダイアログが**OK**で閉じられた場合、戻り値は true になります。

 ダイアログではなく、独自の**system.windows.interop.hwndsource>** でホストされている wpf UI を表示する必要がある場合 (たとえば、ポップアップウィンドウや、Win32/WinForms の親ウィンドウウィンドウの wpf 子ウィンドウ)、wpf 要素のルート要素に対して**FontFamily**と**FontSize**を設定する必要があります。 (シェルでは、メインウィンドウにプロパティが設定されますが、HWND を超えて継承されることはありません)。 シェルには、次のようなプロパティをバインドできるリソースが用意されています。

```
<Setter property="FontFamily" Value="{DynamicResource VsFont.EnvironmentFontFamily}" />
<Setter property="FontSize" Value="{DynamicResource VsFont.EnvironmentFontSize}" />

```

### <a name="formatting-scalingbolding-reference"></a><a name="BKMK_Formatting"></a>書式設定 (倍率/太字) のリファレンス
 一部のダイアログでは、特定のテキストが太字になっている必要があります。または、環境フォント以外のサイズが必要です。 以前は、環境フォントより大きいフォントは、"環境フォント + 2" または同様にコード化されていました。 指定されたコードスニペットを使用すると、高 DPI モニターがサポートされ、表示テキストが常に正しいサイズと重み (Light、Semilight など) で表示されるようになります。

> **注: 書式設定を適用する前に、「[テキストスタイル](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TextStyle)」に記載されているガイダンスに従っていることを確認してください。**

 環境フォントをスケーリングするには、TextBlock またはラベルのスタイルを、示されているとおりに設定します。 適切に使用されたこれらの各コードスニペットでは、適切なサイズと重みのバリエーションを含む正しいフォントが生成されます。

 ここで、"組み込み vsui" は名前空間 VisualStudio への参照です。

```
xmlns:vsui="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.14.0"

```

#### <a name="375-environment-font--light"></a>375% 環境フォント + ライト
 **次のように表示されます:** 34 Pt Segoe UI ライト

 **For:** (まれな) 一意のブランド化 UI (スタートページのなど) を使用します。

 **手続き型コード:**"TextBlock" は以前に定義された TextBlock で、"label" は以前に定義されたラベルです。

```
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment375PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment375PercentFontSizeStyleKey);

```

 **XAML:** 以下に示すように、TextBlock またはラベルのスタイルを設定します。

```
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment375PercentFontSizeStyleKey}}">TextBlock: 375 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment375PercentFontSizeStyleKey}}">Label: 375 Percent Scaling</Label>

```

#### <a name="310-environment-font--light"></a>310% 環境フォント + ライト
 **表示形式:** 28 Pt Segoe UI ライト

 **用途:** 大きな署名ダイアログタイトル、レポートのメインの見出し

 **手続き型コード:**"TextBlock" は以前に定義された TextBlock で、"label" は以前に定義されたラベルです。

```
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment310PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment310PercentFontSizeStyleKey);

```

 **XAML:** 以下に示すように、TextBlock またはラベルのスタイルを設定します。

```
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment310PercentFontSizeStyleKey}}">TextBlock: 310 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment310PercentFontSizeStyleKey}}">Label: 310 Percent Scaling</Label>

```

#### <a name="200-environment-font--semilight"></a>200% 環境フォント + Semilight
 **次のように表示:** 18 Pt Segoe UI Semilight

 **用途:** 小見出し、s/medium ダイアログのタイトル

 **手続き型コード:**"TextBlock" は以前に定義された TextBlock で、"label" は以前に定義されたラベルです。

```
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment200PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment200PercentFontSizeStyleKey);

```

 **XAML:** 以下に示すように、TextBlock またはラベルのスタイルを設定します。

```
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment200PercentFontSizeStyleKey}}">TextBlock: 200 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment200PercentFontSizeStyleKey}}">Label: 200 Percent Scaling</Label>

```

#### <a name="155-environment-font"></a>155% 環境フォント
 **次のように表示:** 14 pt Segoe UI

 **用途:** ドキュメントウェル UI またはレポートのセクション見出し

 **手続き型コード:**"TextBlock" は以前に定義された TextBlock で、"label" は以前に定義されたラベルです。

```
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment155PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment155PercentFontSizeStyleKey);

```

 **XAML:** 以下に示すように、TextBlock またはラベルのスタイルを設定します。

```
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment155PercentFontSizeStyleKey}}">TextBlock: 155 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment155PercentFontSizeStyleKey}}">Label: 155 Percent Scaling</Label>

```

#### <a name="133-environment-font"></a>133% 環境フォント
 **次のように表示:** 12 pt Segoe UI

 **用途:** 署名ダイアログ内の小さな小見出しとドキュメントウェル UI

 **手続き型コード:**"TextBlock" は以前に定義された TextBlock で、"label" は以前に定義されたラベルです。

```
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment133PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment133PercentFontSizeStyleKey);

```

 **XAML:** 以下に示すように、TextBlock またはラベルのスタイルを設定します。

```
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment133PercentFontSizeStyleKey}}">TextBlock: 133 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment133PercentFontSizeStyleKey}}">Label: 133 Percent Scaling</Label>

```

#### <a name="122-environment-font"></a>122% 環境フォント
 **次のように表示:** 11 pt Segoe UI

 **用途:** 署名ダイアログのセクション見出し、ツリービューの最上位ノード、垂直タブナビゲーション

 **手続き型コード:**"TextBlock" は以前に定義された TextBlock で、"label" は以前に定義されたラベルです。

```
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment122PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment122PercentFontSizeStyleKey);

```

 **XAML:** 以下に示すように、TextBlock またはラベルのスタイルを設定します。

```
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment122PercentFontSizeStyleKey}}">TextBlock: 122 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment122PercentFontSizeStyleKey}}">Label: 122 Percent Scaling</Label>

```

#### <a name="environment-font--bold"></a>環境フォント + 太字
 太字で**表示:** 9 pt Segoe UI

 **用途:** 署名ダイアログ、レポート、ドキュメントウェル UI でのラベルと小見出し

 **手続き型コード:**"TextBlock" は以前に定義された TextBlock で、"label" は以前に定義されたラベルです。

```
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironmentBoldStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironmentBoldStyleKey);

```

 **XAML:** 以下に示すように、TextBlock またはラベルのスタイルを設定します。

```
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironmentBoldStyleKey}}"> Bold TextBlock</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironmentBoldStyleKey}}"> Bold Label</Label>

```

### <a name="localizable-styles"></a>ローカライズ可能なスタイル
 場合によっては、ローカライザーが東アジア言語のテキストから太字を削除するなど、さまざまなロケールのフォントスタイルを変更する必要があります。 フォントスタイルをローカライズできるようにするには、そのスタイルを .resx ファイル内に配置する必要があります。 これを実行し、Visual Studio フォームデザイナーで引き続きフォントスタイルを編集する最善の方法は、デザイン時にフォントスタイルを明示的に設定することです。 これにより、完全なフォントオブジェクトが作成され、親フォントの継承が解除されているように見えますが、フォントを設定するために使用されるのは FontStyle プロパティだけです。

 この問題を解決するには、ダイアログフォームの**Fontchanged**イベントをフックします。 **Fontchanged**イベントで、すべてのコントロールをウォークし、フォントが設定されているかどうかを確認します。 設定されている場合は、フォームのフォントおよびコントロールの前のフォントスタイルに基づいて新しいフォントに変更します。 コードでのこの例を次に示します。

```
private void Form1_FontChanged(object sender, System.EventArgs e)
{
          SetFontStyles();
}

/// <summary>
/// SetFontStyles - This function will iterate all controls on a page
/// and recreate their font with the desired fontstyle.
/// It should be called in the OnFontChanged handler (and also in the constructor
/// in case the IUIService is not available so OnFontChange doesn't fire).
/// This way, when the VS shell font is given to us the controls that have
/// a different style for the font (bolded for example) will recreate their font
/// and use the VS shell font but with a style variation (bolded ...).
/// </summary>
protected void SetFontStyles()
{
     SetFontStyles(this, this, this.Font);
}

protected static void SetFontStyles(Control topControl, Control parent, Font referenceFont)
{
     foreach(Control c in parent.Controls)
     {
          if (c.Controls != null && c.Controls.Count > 0) {
               SetFontStyles(topControl, c, referenceFont);
          }
          if (c.Font != topControl.Font) {
               c.Font = new Font(referenceFont, c.Font.Style);
          }
     }
}
```

 このコードを使用すると、フォームのフォントが更新されたときに、コントロールのフォントも更新されることが保証されます。 このメソッドは、フォームのコンストラクターからも呼び出す必要があります。これは、ダイアログが**Iuiservice**のインスタンスを取得できず、 **fontchanged**イベントが起動されない場合があるためです。 **フォントを変更**すると、ダイアログが既に開いている場合でも、ダイアログが新しいフォントを動的に選択できるようになります。

### <a name="testing-the-environment-font"></a>環境フォントのテスト
 UI が環境フォントを使用し、サイズ設定を考慮していることを確認するには、[**ツール] > [オプション > 環境] > フォントおよび色**を開き、[設定の表示] ドロップダウンメニューで [環境フォント] を選択します。

 ![[ツール &#62; のオプション] ダイアログの [フォントおよび色] ページ](../../extensibility/ux-guidelines/media/0201-a-optionsfonts.png "0201-a_OptionsFonts")

 **[ツール > オプション] ダイアログのフォントおよび色の設定**

 フォントを既定値とは異なるものに設定します。 更新されない UI を明確にするには、セリフ付きのフォント ("Times New Roman" など) を選択し、非常に大きなサイズを設定します。 次に、UI をテストして、環境を尊重するようにします。 ライセンスダイアログの使用例を次に示します。

 ![環境フォントを使用していないダイアログの例](../../extensibility/ux-guidelines/media/0201-b-wrongfontdialog.png "0201-b_WrongFontDialog")

 **環境フォントを考慮しない UI テキストの例**

 この場合、"ユーザー情報" と "製品情報" は、フォントを考慮していません。 場合によっては、これが明示的なデザイン選択である場合がありますが、赤線仕様の一部として明示的なフォントが指定されていないと、バグになることがあります。

 フォントをリセットするには、[ツール > オプション] の [既定値を使用] をクリックし、[**フォントおよび色] > > 環境**] をクリックします。

## <a name="text-style"></a><a name="BKMK_TextStyle"></a>テキストスタイル
 テキストスタイルは、フォントサイズ、太さ、および大文字小文字の区別を表します。 実装のガイダンスについては、[環境のフォント](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TheEnvironmentFont)に関する説明を参照してください。

### <a name="text-casing"></a>テキストの文字種

#### <a name="all-caps"></a>すべて大文字
 Visual Studio のタイトルやラベルには、すべて大文字を使用しないでください。

#### <a name="all-lowercase"></a>すべて小文字
 Visual Studio でタイトルまたはラベルに小文字を使用しないようにします。

#### <a name="sentence-and-title-case"></a>文とタイトルの大文字小文字の区別
 Visual Studio のテキストでは、状況に応じて、タイトルの大文字/小文字を使用する必要があります。

|次の場合にタイトルの文字を使用する:|次の場合に文の大文字を使用します。|
|-------------------------|----------------------------|
|ダイアログタイトル|ラベル|
|グループボックス|チェック ボックス|
|メニュー項目|ラジオ ボタン|
|コンテキスト メニュー項目|リストボックスの項目|
|ボタン|ステータス バー|
|テーブルラベル||
|列見出し||
|ツール ヒント||

##### <a name="title-case"></a>先頭文字が大文字
 Title case は、語句内の単語の大部分または全部の最初の文字が大文字になるスタイルです。 Visual Studio では、次のような多くの項目にタイトルケースが使用されます。

- **ツールヒント.** 例: "選択した項目をプレビューする"

- **列ヘッダー。** 例: "システム応答"

- **メニュー項目。** 例: "すべて保存"

  Title ケースを使用する場合、単語を大文字にするタイミングと小文字を省略するタイミングのガイドラインは次のとおりです。

|大文字|コメントと例|
|---------------|---------------------------|
|すべての名詞||
|すべての動詞|"Is" とその他の形式の "to be" を含める|
|すべての副詞|"Than" と "When" を含める|
|すべての形容詞|"This" と "This" を含む|
|すべての代名詞|"省略形" と "the the 代名詞" (it) と動詞 "is" のような所有者を含めます。|
|音声の一部に関係なく、最初と最後の単語||
|動詞句の一部である前置詞|[すべてのウィンドウを閉じる] または [システムのシャットダウン]|
|頭字語のすべての文字|HTML、XML、URL、IDE、RGB|
|名詞が名詞または適切な形容詞の場合、または単語の重みが等しい場合は、複合語の2番目の単語|相互参照、マイクロソフト以前のソフトウェア、読み取り/書き込みアクセス、実行時|

|小文字|例|
|---------------|--------------|
|2番目の単語が音声の別の部分である場合、または分詞が最初の単語を変更する場合は、その単語。|方法、実行方法|
|タイトルの最初の単語以外の記事|a、an、the|
|座標接続詞|および、、、、または|
|動詞句の外側に4文字以上の単語を含む前置詞|に対して、on、on、out、|
|無限直線句で使用されている場合は "To"|「ハードディスクをフォーマットする方法」|

##### <a name="sentence-case"></a>文の大文字/小文字
 文の大文字と小文字は、文の最初の単語だけを大文字にし、適切な名詞と代名詞 "I" を使用します。 一般に、文の大文字と小文字の区別は、特にコンピューターによってコンテンツが翻訳される場合に、世界中のユーザーが読みやすくなります。 次の場合に文の大文字を使用します。

1. **ステータスバーのメッセージ。** これらは単純で簡単で、ステータス情報のみを提供します。 例: "プロジェクトファイルの読み込み"

2. ラベル、チェックボックス、オプションボタン、リストボックス項目など、**他のすべての UI 要素**。 例: "リスト内のすべての項目を選択する"

### <a name="text-formatting"></a>テキストの書式設定
 Visual Studio 2013 での既定のテキストの書式設定は[、環境フォント](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TheEnvironmentFont)によって制御されます。 このサービスは、IDE (統合開発環境) 全体で一貫したフォントの外観を保証するのに役立ちます。ユーザーに一貫したエクスペリエンスを保証するには、このサービスを使用する必要があります。

 Visual Studio のフォントサービスによって使用される既定のサイズは、Windows から取得され、9 pt と表示されます。

 環境フォントに書式を適用できます。 このトピックでは、スタイルを使用する方法と場所について説明します。 実装情報については、[環境フォント](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TheEnvironmentFont)を参照してください。

#### <a name="bold-text"></a>太字のテキスト
 太字のテキストは Visual Studio では控えめに使用され、次のものに対して予約されている必要があります。

- ウィザードの質問ラベル

- ソリューションエクスプローラーでアクティブなプロジェクトを指定する

- プロパティツールウィンドウのオーバーライドされた値

- Visual Basic エディターのドロップダウンリストに表示される特定のイベント

- web ページのドキュメントアウトラインのサーバーで生成されたコンテンツ

- 複雑なダイアログまたはデザイナー UI のセクションヘッダー

#### <a name="italics"></a>斜体
 Visual Studio では、斜体または太字の斜体テキストは使用されません。

#### <a name="color"></a>色

- Blue はハイパーリンク (ナビゲーションとコマンド) 用に予約されており、向きには使用しないでください。

- 次の目的では、より大きな見出し (環境フォント x 155% 以上) に色を設定できます。

  - Visual Studio の UI に視覚的な魅力を与えるには

  - 特定の領域に注意を向けるには

  - 標準の濃い灰色/黒の環境テキストの色からレリーフを提供するには

- 見出しの色は、既存の Visual Studio ブランドの色を活用する必要があります。主に、紫色の主な #FF68217A です。

- 見出しに色を使用する場合は、コントラスト比率やその他のアクセシビリティの考慮事項など、 [Windows の色のガイドライン](https://msdn.microsoft.com/library/dn742482.aspx)に従う必要があります。

### <a name="font-size"></a>フォント サイズ
 Visual Studio UI のデザイン機能により、より多くの空白を持つ外観が薄くなります。 可能な場合は、chrome とタイトルバーが縮小または削除されています。 情報密度は Visual Studio の要件であるのに対し、さらにオープンな行間隔とフォントサイズと太さのバリエーションを強調することで、文字体裁は引き続き重要になります。

 次の表には、Visual Studio で使用される表示フォントのデザインの詳細と視覚的な例が含まれています。 一部の表示フォントバリエーションには、Semilight や Light などのサイズと太さの両方が表示されます。

 すべての表示フォントの実装コードスニペットは、 [「書式設定 (スケール/太字) の参照](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_Formatting)」にあります。

#### <a name="375-environment-font--light"></a>375% 環境フォント + ライト

|使用方法|外観|
|-|-|
|**使用法:** 珍しい. 一意のブランド化 UI のみ。<br /><br /> **ください**<br /><br /> -文の大文字小文字を使用する<br />-常にライトウェイトを使用する<br /><br /> **次の行為は禁止とします。**<br /><br /> -スタートページなどの署名 UI 以外の UI に使用します<br />-太字、斜体、または太字の斜体<br />-本文のテキストに使用<br />-ツールウィンドウで使用する|**次のように表示されます:** 34 Pt Segoe UI ライト<br /><br /> **ビジュアルの例:**<br /><br /> *現在使用されていません。は、スタートページで使用できます。*|

#### <a name="310-environment-font--light"></a>310% 環境フォント + ライト

|使用方法|外観|
|-|-|
|**使用法:**<br /><br /> -署名ダイアログの大きな見出し<br />-メインレポートの見出し<br /><br /> **ください**<br /><br /> -文の大文字小文字を使用する<br />-常にライトウェイトを使用する<br /><br /> **次の行為は禁止とします。**<br /><br /> -スタートページなどの署名 UI 以外の UI に使用します<br />-太字、斜体、または太字の斜体<br />-本文のテキストに使用<br />-ツールウィンドウで使用する|**表示形式:** 28 Pt Segoe UI ライト<br /><br /> **ビジュアルの例:**<br /><br /> ![&#43; 明るい見出しの310% 環境フォントの例](../../extensibility/ux-guidelines/media/0202-a-ef310.png "0202-a_EF310")|

#### <a name="200-environment-font--semilight"></a>200% 環境フォント + Semilight

|使用方法|外観|
|-|-|
|**使用法:**<br /><br /> -小見出し<br />-小規模および中規模のダイアログのタイトル<br /><br /> **ください**<br /><br /> -文の大文字小文字を使用する<br />-常に Semilight weight を使用する<br /><br /> **次の行為は禁止とします。**<br /><br /> -太字、斜体、または太字の斜体<br />-本文のテキストに使用<br />-ツールウィンドウで使用する|**次のように表示:** 18 Pt Segoe UI Semillight<br /><br /> **ビジュアルの例:**<br /><br /> ![200% 環境フォント &#43; Semilight の例](../../extensibility/ux-guidelines/media/0202-b-ef200.png "0202-b_EF200")|

#### <a name="155-environment-font"></a>155% 環境フォント

|使用方法|外観|
|-|-|
|**使用法:**<br /><br /> -ドキュメントウェル UI のセクション見出し<br />-レポート<br /><br /> **操作:** 文の大文字と小文字を区別する<br /><br /> **次の行為は禁止とします。**<br /><br /> -太字、斜体、または太字の斜体<br />-本文のテキストに使用<br />-標準の Visual Studio コントロールで使用する<br />-ツールウィンドウで使用する|**次のように表示:** 14 pt Segoe UI<br /><br /> **ビジュアルの例:**<br /><br /> ![155% 環境フォントの見出しの例](../../extensibility/ux-guidelines/media/0202-c-ef155.png "0202-c_EF155")|

#### <a name="133-environment-font"></a>133% 環境フォント

|使用方法|外観|
|-|-|
|**使用法:**<br /><br /> -署名ダイアログの小さいサブ見出し<br />-ドキュメントウェル UI の下位のサブ見出し<br /><br /> **操作:** 文の大文字と小文字を区別する<br /><br /> **次の行為は禁止とします。**<br /><br /> -太字、斜体、または太字の斜体<br />-本文のテキストに使用<br />-標準の Visual Studio コントロールで使用する<br />-ツールウィンドウで使用する|**次のように表示:** 12 pt Segoe UI<br /><br /> **ビジュアルの例:**<br /><br /> ![133% 環境フォントの見出しの例](../../extensibility/ux-guidelines/media/0202-d-ef133.png "0202-d_EF133")|

#### <a name="122-environment-font"></a>122% 環境フォント

|使用方法|外観|
|-|-|
|**使用法:**<br /><br /> -署名ダイアログのセクション見出し<br />-ツリービューの最上位ノード<br />-垂直タブナビゲーション<br /><br /> **操作:** 文の大文字と小文字を区別する<br /><br /> **次の行為は禁止とします。**<br /><br /> -太字、斜体、または太字の斜体<br />-本文のテキストに使用<br />-標準の Visual Studio コントロールで使用する<br />-ツールウィンドウで使用する|**次のように表示:** 11 pt Segoe UI<br /><br /> **ビジュアルの例:**<br /><br /> ![122% 環境フォントの見出しの例](../../extensibility/ux-guidelines/media/0202-e-ef122.png "0202-e_EF122")|

#### <a name="environment-font--bold"></a>環境フォント + 太字

|使用方法|外観|
|-|-|
|**使用法:**<br /><br /> -署名ダイアログのラベルと小見出し<br />-レポートのラベルと小見出し<br />-ドキュメントウェル UI のラベルと小見出し<br /><br /> **ください**<br /><br /> -文の大文字小文字を使用する<br />-太字の太さを使用します<br /><br /> **次の行為は禁止とします。**<br /><br /> -斜体または太字斜体<br />-本文のテキストに使用<br />-標準の Visual Studio コントロールで使用する<br />-ツールウィンドウで使用する|太字で**表示:** 9 pt Segoe UI<br /><br /> **ビジュアルの例:**<br /><br /> ![環境フォント &#43; 太字の見出しの例](../../extensibility/ux-guidelines/media/0202-f-efb.png "0202-f_EFB")|

#### <a name="environment-font"></a>環境フォント

|使用方法|外観|
|-|-|
|**使用法:** その他のすべてのテキスト<br /><br /> **操作:** 文の大文字と小文字を区別する<br /><br /> **実行しない:** 斜体または太字斜体|**次のように表示:** 9 pt Segoe UI<br /><br /> **ビジュアルの例:**<br /><br /> ![環境フォントの例](../../extensibility/ux-guidelines/media/0202-g-ef.png "0202-g_EF")|

### <a name="padding-and-spacing"></a>余白と間隔
 見出しには、適切な強調を付けるための領域が必要です。 この領域は、ポイントのサイズと、環境フォントの水平方向のルールやテキストの行など、見出しの近くにある内容によって異なります。

- 見出しの理想的な埋め込みは、大文字/小文字の高さ空間の90% にする必要があります。 たとえば、28 pt Segoe UI 明るい見出しのキャップの高さは 26 pt で、余白は約 23 pt、つまり約31ピクセルになります。

- 見出しの周囲の最小値は、大文字/小文字の高さの50% である必要があります。 見出しにルールやその他のきつい要素が付随する場合は、スペースを使用することはできません。

- 太字で表示される環境のフォントテキストは、行の高さの既定の間隔と余白に従う必要があります。

## <a name="see-also"></a>関連項目
 [Msdn: フォント (windows)](https://msdn.microsoft.com/library/windows/desktop/dn742483\(v=vs.85\).aspx) [Msdn: ユーザーインターフェイスのテキスト (windows)](https://msdn.microsoft.com/library/windows/desktop/dn742478\(v=vs.85\).aspx)
