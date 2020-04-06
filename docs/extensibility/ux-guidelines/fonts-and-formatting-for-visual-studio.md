---
title: Visual Studio のフォントと書式設定 |マイクロソフトドキュメント
ms.date: 04/26/2017
ms.topic: conceptual
ms.assetid: c3c3df69-83b4-4fd0-b5b1-e18c33f39376
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bf1550026fb5c9d9395d931f21d48bc4739ea8c3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80698584"
---
# <a name="fonts-and-formatting-for-visual-studio"></a>Visual Studio のフォントと書式設定
## <a name="the-environment-font"></a><a name="BKMK_TheEnvironmentFont"></a>環境フォント
 Visual Studio 内のすべてのフォントは、カスタマイズのためにユーザーに公開する必要があります。 これは主に、[ツール] メニューの **[オプション**] ダイアログ ボックスの [**フォントと色**] >クリックします。 フォント設定の主なカテゴリは次の 3 つになります。

- **環境フォント**- ダイアログ、メニュー、ツール ウィンドウ、ドキュメント ウィンドウなど、すべてのインターフェイス要素に使用される IDE (統合開発環境) のプライマリ フォントです。 既定では、環境フォントは、現在のバージョンの Windows で 9 pt Segoe UI として表示されるシステム フォントに関連付けられています。 すべてのインターフェイス要素に 1 つのフォントを使用すると、IDE 全体で一貫したフォントの外観を確保できます。

- **テキスト エディタ**- コードやその他のテキスト ベースのエディタで表示される要素は **、ツール > オプション**の [テキスト エディタ] ページでカスタマイズできます。

- **特定のコレクション**- ユーザーがインターフェイス要素をカスタマイズできるデザイナー ウィンドウは **、[ツール > オプション]** の独自の設定ページで、デザイン サーフェイスに固有のフォントを公開する場合があります。

### <a name="editor-font-customization-and-resizing"></a>エディターのフォントのカスタマイズとサイズ変更
 ユーザーは、一般的なユーザー インターフェイスに依存しない、自分の好みに応じて、エディタ内のテキストのサイズや色を拡大または拡大します。 環境フォントは、エディタやデザイナーの一部として、またはエディター/デザイナーの一部として表示される要素で使用されるため、これらのフォント分類の 1 つが変更されたときに予想される動作に注意することが重要です。

 エディターに表示されるが*コンテンツ*の一部ではない UI 要素を作成する場合は、予測可能な方法で要素のサイズを変更できるように、テキスト フォントではなく環境フォントを使用することが重要です。

1. エディターのコード テキストの場合は、コード テキストフォント設定でサイズを変更し、エディター テキストのズーム レベルに応答します。

2. インターフェイスの他のすべての要素は、環境フォント設定に関連付けられ、環境内のグローバルな変更に対応する必要があります。 これには次の項目が含まれます (ただし、これらに限定されません)。

    - コンテキスト メニュー内のテキスト

    - 電球メニューのテキスト、クイック検索エディターペイン、ペインへの移動などのエディタの表示要素内のテキスト

    - **[ファイル**内を検索] や [**リファクタリング**] などのダイアログ ボックスのテキストにラベルを付ける

### <a name="accessing-the-environment-font"></a>環境フォントへのアクセス
 ネイティブまたは WinForms コードでは、サービスからインターフェイスを照会した後、`IUIHostLocale::GetDialogFont`メソッドを呼び出すことによって環境`SID_SUIHostLocale`フォントにアクセスできます。

 Windows プレゼンテーション基盤 (WPF) の場合は、WPF のクラス`DialogWindow`ではなくシェルのクラスからダイアログ`Window`ウィンドウ クラスを派生します。

 XAML では、コードは次のようになります。

```xaml
<ui:DialogWindow
    x:Class"MyNameSpace.MyWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:s="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:ui="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.11.0"
    ShowInTaskbar="False"
    WindowStartupLocation="CenterOwner"
    Title="My Dialog">
</ui:DialogWindow>
```

分離コード:

```csharp
internal partial class WebConfigModificationWindow : DialogWindow
{
}
```

 (現在`Microsoft.VisualStudio.Shell.11.0`のバージョンの MPF dll に置き換えます。

 ダイアログを表示するには、クラスで`ShowModal()`" "`ShowDialog()`を呼び出します。 `ShowModal()`シェルで正しいモーダル状態を設定し、ダイアログが親ウィンドウの中央に配置されるようにします。

 コードは次のとおりです。

```csharp
MyWindow window = new MyWindow();
window.ShowModal()
```

 `ShowModal`ブールを返す? (null 許容ブール)`DialogResult`と共に、 を使用できます。 ダイアログが OK で閉じられた場合、戻り値は true**です**。

 ダイアログではなく、独自`HwndSource`のでホストされているいくつかの WPF UI を表示する必要がある場合は、ポップアップ ウィンドウや Win32/WinForms 親ウィンドウの WPF 子ウィンドウなど、WPF 要素のルート`FontFamily`要素`FontSize`に、 および を設定する必要があります。 (シェルはメイン ウィンドウにプロパティを設定しますが、a`HWND`を超えて継承されるわけではありません)。 シェルは、次のように、プロパティをバインドできるリソースを提供します。

```xaml
<Setter Property="FontFamily" Value="{DynamicResource VsFont.EnvironmentFontFamily}" />
<Setter Property="FontSize" Value="{DynamicResource VsFont.EnvironmentFontSize}" />
```

### <a name="formatting-scalingbolding-reference"></a><a name="BKMK_Formatting"></a>書式設定 (スケーリング/太字) リファレンス
 ダイアログの中には、特定のテキストを太字にしたり、環境フォント以外のサイズにする必要があるものもあります。 以前は、環境フォントより大きなフォントは "`environment font +2`" または類似のフォントとしてコーディングされていました。 提供されたコード スニペットを使用すると、高 DPI モニターがサポートされ、表示テキストが常に正しいサイズと重み (ライトやセミライトなど) で表示されることを確認します。

> [!NOTE]
> 書式を適用する前に、「[テキストスタイル](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TextStyle)」に記載されているガイダンスに従っていることを確認してください。

 環境フォントを拡大縮小するには、示されているとおりに TextBlock または Label のスタイルを設定します。 これらのコード スニペットは、適切に使用され、適切なサイズと重みのバリエーションを含む、正しいフォントを生成します。

 ここで"`vsui`は名前空間`Microsoft.VisualStudio.Shell`への参照です。

```xaml
xmlns:vsui="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.14.0"
```

#### <a name="375-environment-font--light"></a>375% 環境フォント + ライト

**次のように表示されます:** 34 pt セゴエ UI ライト

::: moniker range="vs-2017"

**の使用:** (まれな) 一意のブランド化された UI (スタート ページなど)

::: moniker-end

::: moniker range=">=vs-2019"

**の用途:** (まれ) 一意のブランド UI

::: moniker-end

**手続き型コード:** は`textBlock`、以前に定義された TextBlock であり、`label`以前に定義されたラベルです。

```csharp
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment375PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment375PercentFontSizeStyleKey);
```

**XAML:** 次に示すように、テキストブロックまたはラベルのスタイルを設定します。

```xaml
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment375PercentFontSizeStyleKey}}">TextBlock: 375 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment375PercentFontSizeStyleKey}}">Label: 375 Percent Scaling</Label>
```

#### <a name="310-environment-font--light"></a>310% 環境フォント + ライト
 **次のように表示されます:** 28 pt Segoe UI ライト**使用:** 大きな署名ダイアログ タイトル, レポートのメイン見出し

 **手続き型コード:** は`textBlock`、以前に定義された TextBlock であり、`label`以前に定義されたラベルです。

```csharp
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment310PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment310PercentFontSizeStyleKey);
```

 **XAML:** 次に示すように、テキストブロックまたはラベルのスタイルを設定します。

```xaml
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment310PercentFontSizeStyleKey}}">TextBlock: 310 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment310PercentFontSizeStyleKey}}">Label: 310 Percent Scaling</Label>
```

#### <a name="200-environment-font--semilight"></a>200% 環境フォント + セミライト
 **次のように表示されます:** 18 pt Segoe UI 半光**用途:** 小見出し、 小中のダイアログボックスのタイトル

 **手続き型コード:** は`textBlock`、以前に定義された TextBlock であり、`label`以前に定義されたラベルです。

```csharp
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment200PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment200PercentFontSizeStyleKey);
```

 **XAML:** 次のように、テキストブロックまたはラベルのスタイルを設定します。

```xaml
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment200PercentFontSizeStyleKey}}">TextBlock: 200 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment200PercentFontSizeStyleKey}}">Label: 200 Percent Scaling</Label>
```

#### <a name="155-environment-font"></a>155% 環境フォント
 **次のように表示されます:** 14 pt Segoe UI**使用:** ドキュメントのセクション見出しの UI またはレポート

 **手続き型コード:** は`textBlock`、以前に定義された TextBlock であり、`label`以前に定義されたラベルです。

```csharp
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment155PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment155PercentFontSizeStyleKey);
```

 **XAML:** 次のように、テキストブロックまたはラベルのスタイルを設定します。

```xaml
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment155PercentFontSizeStyleKey}}">TextBlock: 155 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment155PercentFontSizeStyleKey}}">Label: 155 Percent Scaling</Label>
```

#### <a name="133-environment-font"></a>133% 環境フォント
 **次のように表示されます:** 12 pt Segoe UI**使用:** 署名ダイアログとドキュメント UI の小さな小見出し

 **手続き型コード:** は`textBlock`、以前に定義された TextBlock であり、`label`以前に定義されたラベルです。

```csharp
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment133PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment133PercentFontSizeStyleKey);
```

 **XAML:** 次のように、テキストブロックまたはラベルのスタイルを設定します。

```xaml
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment133PercentFontSizeStyleKey}}">TextBlock: 133 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment133PercentFontSizeStyleKey}}">Label: 133 Percent Scaling</Label>
```

#### <a name="122-environment-font"></a>122% 環境フォント
 **11** pt Segoe UI**使用:** 署名ダイアログのセクション見出し、ツリービューのトップノード、垂直タブナビゲーション

 **手続き型コード:** は`textBlock`、以前に定義された TextBlock であり、`label`以前に定義されたラベルです。

```csharp
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment122PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment122PercentFontSizeStyleKey);
```

 **XAML:** 次のように、テキストブロックまたはラベルのスタイルを設定します。

```xaml
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment122PercentFontSizeStyleKey}}">TextBlock: 122 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment122PercentFontSizeStyleKey}}">Label: 122 Percent Scaling</Label>
```

#### <a name="environment-font--bold"></a>環境フォント + 太字
 **太字**の 9 pt Segoe UI**使用:** 署名ダイアログ、レポート、およびドキュメント UI のラベルとサブヘッド

 **手続き型コード:** は`textBlock`、以前に定義された TextBlock であり、`label`以前に定義されたラベルです。

```csharp
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironmentBoldStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironmentBoldStyleKey);
```

 **XAML:** 次のように、テキストブロックまたはラベルのスタイルを設定します。

```xaml
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironmentBoldStyleKey}}"> Bold TextBlock</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironmentBoldStyleKey}}"> Bold Label</Label>
```

### <a name="localizable-styles"></a>ローカライズ可能なスタイル
 場合によっては、ローカライズの場合、ローカライズの言語のフォント スタイルを変更する必要があります。 フォント スタイルのローカライズを可能にするには、これらのスタイルが .resx ファイル内にある必要があります。 Visual Studio フォーム デザイナーでフォント スタイルを編集する場合、デザイン時にフォント スタイルを明示的に設定するのが最善の方法です。 この場合、フォント オブジェクト全体が作成され、親フォントの継承が壊れる可能性がありますが、FontStyle プロパティだけがフォントの設定に使用されます。

 解決策は、ダイアログ フォームの`FontChanged`イベントをフックすることです。 イベントでは`FontChanged`、すべてのコントロールをウォークし、そのフォントが設定されているかどうかを確認します。 設定されている場合は、フォームのフォントとコントロールの前のフォント スタイルに基づいて、新しいフォントに変更します。 コードの例を次に示します。

```csharp
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

 このコードを使用すると、フォームのフォントが更新されると、コントロールのフォントも更新されます。 ダイアログがインスタンスを取得できず、イベントが発生しないため、このメソッドはフォームの`IUIService`コンストラクタからも呼び出す`FontChanged`必要があります。 フック`FontChanged`を使用すると、ダイアログがすでに開いている場合でも、ダイアログが動的に新しいフォントを選択できるようになります。

### <a name="testing-the-environment-font"></a>環境フォントのテスト
 UI が環境フォントを使用し、サイズ設定を尊重していることを確認するには、[**ツール] >オプション> [環境] >フォントと色**] を開き、[設定を表示する]ドロップダウン メニューの [環境フォント] を選択します。

 ![[ツール&gt;オプション] ダイアログのフォントと色の設定](../../extensibility/ux-guidelines/media/0201-a_optionsfonts.png "0201-a_OptionsFonts")<br />[ツール&gt;オプション] ダイアログのフォントと色の設定

 フォントをデフォルトとは非常に異なるフォントに設定します。 どの UI が更新されないかを明らかにするには、セリフ付きのフォント (「タイムズ ニューローマ」など) を選択し、非常に大きなサイズを設定します。 その後、UI をテストして、環境に従っていることを確認します。 ライセンスダイアログを使用した例を次に示します。

 ![環境フォントを尊重しない UI テキストの例](../../extensibility/ux-guidelines/media/0201-b_wrongfontdialog.png "0201-b_WrongFontDialog")<br />環境フォントを尊重しない UI テキストの例

 この場合、「ユーザー情報」と「製品情報」はフォントを尊重しません。 場合によっては、明示的なデザインの選択が可能ですが、明示的なフォントが Redline 仕様の一部として指定されていない場合はバグになる可能性があります。

 フォントをリセットするには、[ツール] >オプション> [**フォントと色] > [既定 >の設定]** をクリックします。

## <a name="text-style"></a><a name="BKMK_TextStyle"></a>テキストスタイル
 テキストスタイルとは、フォントサイズ、太さ、大文字と小文字を指します。 実装のガイダンスについては、「[環境フォント](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TheEnvironmentFont)」を参照してください。

### <a name="text-casing"></a>テキスト大文字と小文字

#### <a name="all-caps"></a>すべて大文字
 タイトルまたはラベルのすべてのキャップを使用しないでください。

#### <a name="all-lowercase"></a>すべて小文字
 タイトルまたはラベルにはすべて小文字を使用しないでください。

#### <a name="sentence-and-title-case"></a>文とタイトルの大文字と小文字
 Visual Studio のテキストでは、状況に応じて、タイトルの大文字と小文字または文の大文字小文字を使用する必要があります。

|タイトルケースの使用:|次の場合に文の大文字と小文字を使用します。|
|-------------------------|----------------------------|
|ダイアログ タイトル|ラベル|
|グループボックス|チェック ボックス|
|メニュー項目|ラジオ ボタン|
|コンテキスト メニュー項目|リスト ボックスの項目|
|Buttons (ボタン)|ステータス バー|
|テーブルラベル||
|列見出し||
|ツールヒント||

##### <a name="title-case"></a>先頭文字が大文字
 タイトルケースは、フレーズ内の単語のほとんどまたは全部の最初の文字を大文字にするスタイルです。 Visual Studio では、タイトル ケースは次の項目に使用されます。

- **ツールヒント。** 例:「選択した項目のプレビュー」

- **列ヘッダー。** 例: "システム応答"

- **メニュー項目。** 例: "すべて保存"

  タイトルケースを使用する場合、単語を大文字にする場合と、小文字を使用するタイミングに関するガイドラインを次に示します。

|大文字|コメントと例|
|---------------|---------------------------|
|すべての名詞||
|すべての動詞|「Is」やその他の形態の「あるべき」を含む|
|すべての副詞|「タン」と「いつ」を含む|
|すべての形容詞|「これ」と「その」を含む|
|すべての代名詞|所有的な「Its」と「それは」を含む代名詞「それ」と動詞「is」|
|最初と最後の言葉、スピーチの部分に関係なく||
|動詞句の一部である前置詞|「すべてのウィンドウを閉じる」または「システムのシャットダウン」|
|頭字語のすべての文字|HTML、 XML、 URL、IDE、RGB|
|複合語の 2 番目の単語が名詞または適切な形容詞である場合、または単語の重みが等しい場合|相互参照、マイクロソフトプレマイクロソフト ソフトウェア、読み取り/書き込みアクセス、ランタイム|

|小文字|使用例|
|---------------|--------------|
|合成語の 2 番目の単語が、音声の別の部分または最初の単語を変更する別の単語である場合|ハウツー、離陸|
|記事 (タイトルの最初の単語でない限り)|a、an、the|
|座標の接続詞|そして、しかし、のために、または、|
|動詞句以外の 4 文字以下の文字を含む前置詞|に, オン, に, アウト, の上に|
|不定詞で使用する場合は「To」を使用する|"ハード ディスクのフォーマット方法"|

##### <a name="sentence-case"></a>文ケース
 文ケースは、文の最初の単語のみが大文字にされる、適切な名詞と代名詞「I」と共に、標準的な大文字化方法です。 一般に、文章のケースは、特にコンテンツが機械によって翻訳される場合、世界中の聴衆が読みやすくなります。 次の場合に文の大文字と小文字を使用します。

1. **ステータス バー のメッセージ。** これらは単純で短く、ステータス情報のみを提供します。 例: "プロジェクト ファイルを読み込んでいます"

2. ラベル、チェック ボックス、ラジオ ボタン、リスト ボックス項目など、**その他のすべての UI 要素**。 例: "リスト内のすべての項目を選択する"

### <a name="text-formatting"></a>テキストの書式設定
 Visual Studio 2013 の既定のテキストの書式設定[は、環境フォント](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TheEnvironmentFont)で制御されます。 このサービスは、IDE (統合開発環境) 全体で一貫したフォントの外観を確保するのに役立ちます。

 Visual Studio フォント サービスで使用される既定のサイズは Windows から取得され、9 pt として表示されます。

 環境フォントに書式を適用できます。 このトピックでは、スタイルの使用方法と使用方法について説明します。 実装情報については、[環境フォント](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TheEnvironmentFont)を参照してください。

#### <a name="bold-text"></a>太字のテキスト
 太字のテキストは、Visual Studio では控えめに使用され、次の目的で予約する必要があります。

- ウィザードの質問ラベル

- ソリューション エクスプローラでのアクティブ なプロジェクトの指定

- [プロパティ] ツール ウィンドウでオーバーライドされた値

- Visual Basic エディターのドロップダウン リストの特定のイベント

- Web ページのドキュメント アウトライン内のサーバーで生成されたコンテンツ

- 複雑なダイアログまたはデザイナー UI のセクション ヘッダー

#### <a name="italics"></a>斜体
 斜体または太字の斜体のテキストは使用しません。

#### <a name="color"></a>Color

- Blue はハイパーリンク (ナビゲーションとコマンド) 用に予約されており、方向には使用しないでください。

- 大きな見出し (環境フォント x 155% 以上) は、次の目的で色分けできます。

  - 署名の Visual Studio UI に視覚的なアピールを提供するには

  - 特定のエリアに注意を促す

  - 標準のダークグレー/ブラック環境テキストカラーからのリリーフを提供する

- 見出しの色は、主にメインの紫色の#FF68217Aの既存の Visual Studio ブランドの色を活用する必要があります。

- 見出しに色を使用する場合は、コントラスト比やその他のアクセシビリティに関する考慮事項など[、Windows の色ガイドライン](/windows/desktop/uxguide/vis-color)に従う必要があります。

### <a name="font-size"></a>[フォント サイズ]
 Visual Studio UI のデザインは、より多くの空白を持つ明るい外観を備えています。 可能な場合は、クロムバーとタイトル バーが縮小または削除されています。 情報密度は Visual Studio では必須ですが、文字体裁は引き続き重要であり、より多くのオープン行間隔とフォント サイズと太さのバリエーションが強調されています。

 次の表は、Visual Studio で使用される表示フォントのデザインの詳細と視覚的な例を示しています。 表示フォントのバリエーションによっては、外観にセミライトやライトなどのサイズと太さの両方が含まれています。

 すべての表示フォントの実装コード スニペットは、フォーマット[(スケーリング/太字) リファレンス を](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_Formatting)参照してください。

#### <a name="375-environment-font--light"></a>375% 環境フォント + ライト

|||
|-|-|
|**使用法:** 珍しい。 独自のブランド UI のみ。<br /><br /> **行います:**<br /><br /> - 文の大文字小文字を使用する<br />- 常に軽量を使用<br /><br /> **できません：**<br /><br /> - スタート ページなどの署名 UI 以外の UI 用に使用します。<br />- 太字、斜体、または太字斜体<br />- 本文に使用<br />- ツールウィンドウで使用|**次のように表示されます:** 34 pt セゴエ UI ライト<br /><br /> **視覚的な例:**<br /><br /> *現在使用されていません。Visual Studio 2017 のスタート ページで使用できます。*|

#### <a name="310-environment-font--light"></a>310% 環境フォント + ライト

::: moniker range="vs-2017"

|||
|-|-|
|**使用：**<br /><br /> - 署名ダイアログの大きな見出し<br />- メインレポートの見出し<br /><br /> **行います:**<br /><br /> - 文の大文字小文字を使用する<br />- 常に軽量を使用<br /><br /> **できません：**<br /><br /> - スタート ページなどの署名 UI 以外の UI 用に使用します。<br />- 太字、斜体、または太字斜体<br />- 本文に使用<br />- ツールウィンドウで使用|**次のように表示されます:** 28 pt セゴエ UI ライト<br /><br /> **視覚的な例:**<br /><br /> ![310% 環境フォントの例 &#43; ライト見出し](../../extensibility/ux-guidelines/media/0202-a_ef310.png "0202-a_EF310")|

::: moniker-end

::: moniker range=">=vs-2019"

|||
|-|-|
|**使用：**<br /><br /> - 署名ダイアログの大きな見出し<br />- メインレポートの見出し<br /><br /> **行います:**<br /><br /> - 文の大文字小文字を使用する<br />- 常に軽量を使用<br /><br /> **できません：**<br /><br /> - 署名 UI 以外の UI に使用<br />- 太字、斜体、または太字斜体<br />- 本文に使用<br />- ツールウィンドウで使用|**次のように表示されます:** 28 pt セゴエ UI ライト<br /><br /> **視覚的な例:**<br /><br /> ![310% 環境フォントの例 &#43; ライト見出し](../../extensibility/ux-guidelines/media/0202-a_ef310.png "0202-a_EF310")|

::: moniker-end

#### <a name="200-environment-font--semilight"></a>200% 環境フォント + セミライト

|||
|-|-|
|**使用：**<br /><br /> - 小見出し<br />- 中小規模ダイアログのタイトル<br /><br /> **行います:**<br /><br /> - 文の大文字小文字を使用する<br />- 常に半光の重量を使用してください<br /><br /> **できません：**<br /><br /> - 太字、斜体、または太字斜体<br />- 本文に使用<br />- ツールウィンドウで使用|**次のように表示されます:** 18 pt セゴエ UI セミライト<br /><br /> **視覚的な例:**<br /><br /> ![200% 環境フォントの例 &#43;セミライト](../../extensibility/ux-guidelines/media/0202-b_ef200.png "0202-b_EF200")|

#### <a name="155-environment-font"></a>155% 環境フォント

|||
|-|-|
|**使用：**<br /><br /> - ドキュメントのセクション見出しの UI<br />- レポート<br /><br /> **行います:** 使用文の大文字小文字<br /><br /> **できません：**<br /><br /> - 太字、斜体、または太字斜体<br />- 本文に使用<br />- 標準の Visual Studio コントロールで使用<br />- ツールウィンドウで使用|**次のように表示されます:** 14 pt セゴエ UI<br /><br /> **視覚的な例:**<br /><br /> ![155% 環境フォントの見出しの例](../../extensibility/ux-guidelines/media/0202-c_ef155.png "0202-c_EF155")|

#### <a name="133-environment-font"></a>133% 環境フォント

|||
|-|-|
|**使用：**<br /><br /> - 署名ダイアログの小さい小見出し<br />- ドキュメントの小さな小見出しの UI<br /><br /> **行います:** 使用文の大文字小文字<br /><br /> **できません：**<br /><br /> - 太字、斜体、または太字斜体<br />- 本文に使用<br />- 標準の Visual Studio コントロールで使用<br />- ツールウィンドウで使用|**次のように表示されます:** 12 pt セゴエ UI<br /><br /> **視覚的な例:**<br /><br /> ![133% 環境フォントの見出しの例](../../extensibility/ux-guidelines/media/0202-d_ef133.png "0202-d_EF133")|

#### <a name="122-environment-font"></a>122% 環境フォント

|||
|-|-|
|**使用：**<br /><br /> - 署名ダイアログのセクション見出し<br />- ツリービューの最上位ノード<br />- 垂直タブナビゲーション<br /><br /> **行います:** 使用文の大文字小文字<br /><br /> **できません：**<br /><br /> - 太字、斜体、または太字斜体<br />- 本文に使用<br />- 標準の Visual Studio コントロールで使用<br />- ツールウィンドウで使用|**次のように表示されます:** 11 pt セゴエ UI<br /><br /> **視覚的な例:**<br /><br /> ![122% 環境フォントの見出しの例](../../extensibility/ux-guidelines/media/0202-e_ef122.png "0202-e_EF122")|

#### <a name="environment-font--bold"></a>環境フォント + 太字

|||
|-|-|
|**使用：**<br /><br /> - 署名ダイアログのラベルとサブヘッド<br />- レポートのラベルとサブヘッド<br />- ドキュメントのラベルとサブヘッドの UI<br /><br /> **行います:**<br /><br /> - 文の大文字小文字を使用する<br />- 太字の太さを使用<br /><br /> **できません：**<br /><br /> - 斜体または太字斜体<br />- 本文に使用<br />- 標準の Visual Studio コントロールで使用<br />- ツールウィンドウで使用|**次のように表示されます:** 太字 9 pt Segoe UI<br /><br /> **視覚的な例:**<br /><br /> ![環境フォント&#43;太字の見出しの例](../../extensibility/ux-guidelines/media/0202-f_efb.png "0202-f_EFB")|

#### <a name="environment-font"></a>環境フォント

|||
|-|-|
|**使用法:** その他のすべてのテキスト<br /><br /> **行います:** 使用文の大文字小文字<br /><br /> **しないでください:** 斜体または太字斜体|**次のように表示されます:** 9 pt セゴエ UI<br /><br /> **視覚的な例:**<br /><br /> ![環境フォントの例](../../extensibility/ux-guidelines/media/0202-g_ef.png "0202-g_EF")|

### <a name="padding-and-spacing"></a>パディングとスペース
 見出しは、適切な強調を与えるために、周囲のスペースを必要とします。 このスペースは、ポイントのサイズや、環境フォントの横書きやテキスト行など、見出しの近くにあるものによって異なります。

- 見出しの理想的なパディングは、大文字の文字の高さのスペースの 90% にする必要があります。 たとえば、28 pt Segoe UI ライトの見出しのキャップ高さは 26 pt で、パディングは約 23 pt、つまり約 31 ピクセルである必要があります。

- 見出しの周囲の最小スペースは、大文字の文字の高さの 50% にする必要があります。 見出しにルールやその他のぴったりフィット要素が伴う場合は、使用するスペースが少なくなることがあります。

- 太字の環境フォントテキストは、デフォルトの行の高さの間隔とパディングに従う必要があります。

## <a name="see-also"></a>関連項目

- [MSDN: フォント (ウィンドウズ)](/windows/desktop/uxguide/vis-fonts)
- [MSDN: ユーザー インターフェイス テキスト (ウィンドウ)](/windows/desktop/uxguide/text-ui)
