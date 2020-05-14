---
title: 言語サービスとエディターの拡張ポイント |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - extension points
ms.assetid: 91a6417e-a6fe-4bc2-9d9f-5173c634a99b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 28bb086eb99e4b8128c04f62f9b370eb2eab8fa3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703059"
---
# <a name="language-service-and-editor-extension-points"></a>言語サービスとエディターの拡張ポイント
エディターには、ほとんどの言語サービス機能を含むマネージ機能拡張フレームワーク (MEF) コンポーネントパーツとして拡張できる拡張ポイントが用意されています。 主な拡張ポイントカテゴリは次のとおりです。

- コンテンツの種類

- 分類タイプと分類形式

- 余白とスクロール バー

- Tags

- 装飾

- マウスプロセッサ

- ドロップハンドラ

- オプション

- IntelliSense

## <a name="extend-content-types"></a>コンテンツ タイプの拡張
 コンテンツ タイプは、エディタで処理されるテキストの種類の定義です。 新しいコンテンツ タイプを定義するには、その型<xref:Microsoft.VisualStudio.Utilities.ContentTypeDefinition>の変数を宣言し、新しいコンテンツ タイプに一意の名前を付けます。 コンテンツ タイプをエディターに登録するには、次の属性と共にエクスポートします。

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>はコンテンツ タイプの名前です。

- <xref:Microsoft.VisualStudio.Utilities.BaseDefinitionAttribute>は、このコンテンツ タイプの派生元のコンテンツ タイプの名前です。 コンテンツ タイプは、他の複数のコンテンツ タイプから継承できます。

  クラスは<xref:Microsoft.VisualStudio.Utilities.ContentTypeDefinition>シールされているため、型パラメーターを指定しない状態でエクスポートできます。

  コンテンツ タイプ定義のエクスポート属性の例を次に示します。

```
[Export]
[Name("test")]
[BaseDefinition("code")]
[BaseDefinition("projection")]
internal static ContentTypeDefinition TestContentTypeDefinition;
```

 コンテンツ タイプは、ゼロ個以上の既存のコンテンツ タイプに基づいて作成できます。 組み込みの型は次のとおりです。

- 任意: 基本的なコンテンツタイプ。 その他のすべてのコンテンツ タイプの親。

- テキスト: 非投影コンテンツの基本タイプ。 「any」から継承します。

- プレーンテキスト: 非コードテキストの場合。 "テキスト" から継承します。

- コード: すべての種類のコード。 "テキスト" から継承します。

- Inert: 任意の種類の処理からテキストを除外します。 このコンテンツ タイプのテキストには、拡張子が適用されることはありません。

- 投影: 投影バッファーの内容。 「any」から継承します。

- インテリセンス:インテライセンスの内容。 "テキスト" から継承します。

- シグヘルプ:署名のヘルプ。 「インテッリ感」から継承します。

- シグヘルプドキュメント: 署名ヘルプドキュメント。 「インテッリ感」から継承します。

  これらは、Visual Studio で定義されているコンテンツの種類と、Visual Studio でホストされている言語の一部です。

- Basic

- C/C++

- コンソール出力

- csharp

- CSS

- Enc

- 結果を検索する

- F#

- HTML

- JScript

- XAML

- XML

  使用可能なコンテンツ タイプの一覧を見つける<xref:Microsoft.VisualStudio.Utilities.IContentTypeRegistryService>には、エディターのコンテンツ タイプのコレクションを保持する をインポートします。 次のコードは、このサービスをプロパティとしてインポートします。

```
[Import]
internal IContentTypeRegistryService ContentTypeRegistryService { get; set; }
```

 コンテンツ タイプをファイル名拡張子に関連付けるには<xref:Microsoft.VisualStudio.Utilities.FileExtensionToContentTypeDefinition>、 を使用します。

> [!NOTE]
> Visual Studio では、ファイル名拡張子は、言語<xref:Microsoft.VisualStudio.Shell.ProvideLanguageExtensionAttribute>サービス パッケージを使用して登録されます。 MEF<xref:Microsoft.VisualStudio.Utilities.FileExtensionToContentTypeDefinition>コンテンツ タイプを、この方法で登録されたファイル名拡張子に関連付けます。

 ファイル名拡張子をコンテンツ タイプ定義にエクスポートするには、次の属性を含める必要があります。

- <xref:Microsoft.VisualStudio.Utilities.FileExtensionAttribute>: ファイル名拡張子を指定します。

- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>: コンテンツタイプを指定します。

  クラスは<xref:Microsoft.VisualStudio.Utilities.FileExtensionToContentTypeDefinition>シールされているため、型パラメーターを指定しない状態でエクスポートできます。

  ファイル名拡張子の属性をコンテンツ タイプ定義にエクスポートする例を次に示します。

```
[Export]
[FileExtension(".test")]
[ContentType("test")]
internal static FileExtensionToContentTypeDefinition TestFileExtensionDefinition;
```

 ファイル<xref:Microsoft.VisualStudio.Utilities.IFileExtensionRegistryService>名拡張子とコンテンツ タイプの関連付けを管理します。

## <a name="extend-classification-types-and-classification-formats"></a>分類タイプと分類形式の拡張
 分類タイプを使用して、さまざまな処理を行うテキストの種類を定義できます (たとえば、「キーワード」テキストの青色と「コメント」テキストの緑色の色付け)。 型の変数を宣言し、その変数に一<xref:Microsoft.VisualStudio.Text.Classification.ClassificationTypeDefinition>意の名前を付けることによって、新しい分類型を定義します。

 分類タイプをエディターに登録するには、次の属性と共にエクスポートします。

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: 分類タイプの名前。

- <xref:Microsoft.VisualStudio.Utilities.BaseDefinitionAttribute>: この分類型を継承する分類型の名前。 すべての分類タイプは"text"から継承され、分類タイプは他の複数の分類タイプから継承できます。

  クラスは<xref:Microsoft.VisualStudio.Text.Classification.ClassificationTypeDefinition>シールされているため、型パラメーターを指定しない状態でエクスポートできます。

  次の例は、分類型定義のエクスポート属性を示しています。

```
[Export]
[Name("csharp.test")]
[BaseDefinition("test")]
internal static ClassificationTypeDefinition CSharpTestDefinition;
```

 標準<xref:Microsoft.VisualStudio.Language.StandardClassification.IStandardClassificationService>分類へのアクセスを提供します。 組み込みの分類タイプには、次のようなものがあります。

- "text"

- 「自然言語」(「テキスト」から派生)

- 「形式言語」(「テキスト」から派生)

- "文字列" ("リテラル" から派生)

- "文字" ("リテラル" から派生)

- "数値" ("リテラル" から派生)

  さまざまなエラータイプのセットが. <xref:Microsoft.VisualStudio.Text.Adornments.ErrorTypeDefinition> 次のエラータイプが含まれます。

- "構文エラー"

- "コンパイラ エラー"

- "その他のエラー"

- 「警告」

  使用可能な分類タイプのリストを検出するには、エディター<xref:Microsoft.VisualStudio.Text.Classification.IClassificationTypeRegistryService>の分類タイプのコレクションを保持する をインポートします。 次のコードは、このサービスをプロパティとしてインポートします。

```
[Import]
internal IClassificationTypeRegistryService ClassificationTypeRegistryService { get; set; }
```

 新しい分類タイプの分類形式定義を定義できます。 から<xref:Microsoft.VisualStudio.Text.Classification.ClassificationFormatDefinition>クラスを派生し、 type<xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition>を使用して、次の属性と共にエクスポートします。

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: 形式の名前。

- <xref:Microsoft.VisualStudio.Utilities.DisplayNameAttribute>: 形式の表示名。

- <xref:Microsoft.VisualStudio.Text.Classification.UserVisibleAttribute>: **[オプション]** ダイアログ ボックスの [**フォントと色**] ページに書式を表示するかどうかを指定します。

- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>: 形式の優先順位。 有効な値は<xref:Microsoft.VisualStudio.Text.Classification.Priority>からです。

- <xref:Microsoft.VisualStudio.Text.Classification.ClassificationTypeAttribute>: この形式がマップされる分類タイプの名前。

  分類形式定義のエクスポート属性の例を次に示します。

```
[Export(typeof(EditorFormatDefinition))]
[ClassificationType(ClassificationTypeNames = "test")]
[Name("test")]
[DisplayName("Test")]
[UserVisible(true)]
[Order(After = Priority.Default, Before = Priority.High)]
internal sealed class TestFormat : ClassificationFormatDefinition
```

 使用可能な形式の一覧を見つけるには<xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMapService>、エディターの形式のコレクションを保持する をインポートします。 次のコードは、このサービスをプロパティとしてインポートします。

```
[Import]
internal IEditorFormatMapService FormatMapService { get; set; }
```

## <a name="extend-margins-and-scrollbars"></a>余白とスクロール バーを拡張する
 余白とスクロール バーは、テキスト ビュー自体に加えて、エディターのメイン ビュー要素です。 テキスト ビューの周囲に表示される標準の余白に加えて、任意の数の余白を指定できます。

 マージンを<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewMargin>定義するインターフェイスを実装します。 また、マージンを<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewMarginProvider>作成するインターフェイスも実装する必要があります。

 エディターでマージン プロバイダーを登録するには、次の属性と共にプロバイダーをエクスポートする必要があります。

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: 余白の名前。

- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>: 余白が表示される順序で、他の余白を基準にします。

   組み込みの余白は次のとおりです。

  - "Wpf 水平スクロールバー"

  - "縦スクロール バーの WPF"

  - "WPF 行番号の余白"

    の順序属性を持つ水平マージン`After="Wpf Horizontal Scrollbar"`は、組み込みのマージンの下に表示され、注文属性を持つ`Before ="Wpf Horizontal Scrollbar"`水平マージンは組み込みマージンの上に表示されます。 の順序属性を持つ右の`After="Wpf Vertical Scrollbar"`垂直マージンは、スクロールバーの右側に表示されます。 順序属性がの左の`After="Wpf Line Number Margin"`垂直マージンは、行番号の余白の左側に表示されます (表示されている場合)。

- <xref:Microsoft.VisualStudio.Text.Editor.MarginContainerAttribute>: 余白の種類 (左、右、上、または下)。

- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>: 余白が有効なコンテンツの種類 ("text" や "code" など) です。

  次の例は、行番号の余白の右側に表示される余白の余白プロバイダーのエクスポート属性を示しています。

```
[Export(typeof(IWpfTextViewMarginProvider))]
[Name("TestMargin")]
[Order(Before = "Wpf Line Number Margin")]
[MarginContainer(PredefinedMarginNames.Left)]
[ContentType("text")]
```

## <a name="extend-tags"></a>タグを拡張する
 タグは、データをさまざまな種類のテキストに関連付ける方法です。 多くの場合、関連付けられたデータは視覚効果として表示されますが、すべてのタグに視覚的な表示が含まれるわけではありません。 を実装<xref:Microsoft.VisualStudio.Text.Tagging.ITag>することで、独自の種類のタグを定義できます。 また、特定の<xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601>テキスト範囲のセットにタグを提供するために実装し、タグを提供<xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider>するためにを実装する必要があります。 次の属性と共に、タガー プロバイダーをエクスポートする必要があります。

- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>: タグが有効なコンテンツの種類 ("text" や "code" など) です。

- <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute>: タグの種類。

  次の例は、タガー プロバイダーのエクスポート属性を示しています。

\<コードコンテンツプレースホルダー</CodeContentPlaceHolder>>8 次の種類のタグが組み込まれています。

- <xref:Microsoft.VisualStudio.Text.Tagging.ClassificationTag>:<xref:Microsoft.VisualStudio.Text.Classification.IClassificationType>に関連付けられている 。

- <xref:Microsoft.VisualStudio.Text.Tagging.ErrorTag>: エラーの種類に関連付けられます。

- <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>: 表示要素に関連付けられます。

  > [!NOTE]
  > の例については、「[チュートリアル : テキストの強調表示](../extensibility/walkthrough-highlighting-text.md)」の「HighlightWordTag の定義」を参照してください。 <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>

- <xref:Microsoft.VisualStudio.Text.Tagging.OutliningRegionTag>: アウトラインで展開または折りたたむことができる領域に関連付けられます。

- <xref:Microsoft.VisualStudio.Text.Tagging.SpaceNegotiatingAdornmentTag>: テキスト ビューで表示要素が占めるスペースを定義します。 スペースネゴシエーションの表示要素の詳細については、次のセクションを参照してください。

- <xref:Microsoft.VisualStudio.Text.Editor.IntraTextAdornmentTag>: 表示要素の自動間隔とサイズ設定を提供します。

  バッファーとビューのタグを検索して使用するには、<xref:Microsoft.VisualStudio.Text.Tagging.IViewTagAggregatorFactoryService>または を<xref:Microsoft.VisualStudio.Text.Tagging.IBufferTagAggregatorFactoryService><xref:Microsoft.VisualStudio.Text.Tagging.ITagAggregator%601>インポートします。 次のコードは、このサービスをプロパティとしてインポートします。

```
[Import]
internal IViewTagAggregatorFactoryService ViewTagAggregatorFactoryService { get; set; }
```

#### <a name="tags-and-markerformatdefinitions"></a>タグとマーカーの書式定義
 クラスを<xref:Microsoft.VisualStudio.Text.Classification.MarkerFormatDefinition>拡張して、タグの外観を定義できます。 クラスをエクスポートする必要があります (<xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition>として) 次の属性を使用します。

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: この形式を参照するために使用される名前

- <xref:Microsoft.VisualStudio.Text.Classification.UserVisibleAttribute>: これにより、UI に表示される形式が表示されます。

  コンストラクターでは、タグの表示名と外観を定義します。 <xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition.BackgroundColor%2A>塗りつぶしの色を定義<xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition.ForegroundColor%2A>し、境界線の色を定義します。 <xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition.DisplayName%2A>は、書式定義のローカライズ可能な名前です。

  以下は、フォーマット定義の例です。

```
[Export(typeof(EditorFormatDefinition))]
[Name("MarkerFormatDefinition/HighlightWordFormatDefinition")]
[UserVisible(true)]
internal class HighlightWordFormatDefinition : MarkerFormatDefinition
{
    public HighlightWordFormatDefinition()
    {
        this.BackgroundColor = Colors.LightBlue;
        this.ForegroundColor = Colors.DarkBlue;
        this.DisplayName = "Highlight Word";
        this.ZOrder = 5;
    }
}

```

 この書式定義をタグに適用するには、クラスの name 属性で設定した名前を参照します (表示名ではありません)。

> [!NOTE]
> の例については、「チュートリアル: テキストの強調表示」のクラスを[参照してください。](../extensibility/walkthrough-highlighting-text.md) <xref:Microsoft.VisualStudio.Text.Classification.MarkerFormatDefinition>

## <a name="extend-adornments"></a>表示要素を拡張する
 表示要素は、テキスト ビューに表示されるテキストまたはテキスト ビュー自体に追加できる視覚効果を定義します。 独自の表示要素は、 の任意の<xref:System.Windows.UIElement>型として定義できます。

 表示要素クラスでは、 を宣言する<xref:Microsoft.VisualStudio.Text.Editor.AdornmentLayerDefinition>必要があります。 表示要素レイヤーを登録するには、次の属性と共にエクスポートします。

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: 表示要素の名前。

- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>: 他の表示要素レイヤーに対する表示要素の順序。 このクラス<xref:Microsoft.VisualStudio.Text.Editor.PredefinedAdornmentLayers>は、選択、アウトライン、キャレット、およびテキストの 4 つのデフォルトレイヤーを定義します。

  次の例は、表示要素レイヤー定義のエクスポート属性を示しています。

```
[Export]
[Name("TestEmbeddedAdornment")]
[Order(After = PredefinedAdornmentLayers.Selection, Before = PredefinedAdornmentLayers.Text)]
internal AdornmentLayerDefinition testLayerDefinition;
```

 装飾をインスタンス化することによって、その<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener><xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener.TextViewCreated%2A>イベントを実装して処理する 2 番目のクラスを作成する必要があります。 このクラスは、次の属性と共にエクスポートする必要があります。

- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>: 表示要素が有効なコンテンツの種類 ("text" や "code" など) です。

- <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute>: この表示要素が有効なテキスト ビューの種類。 このクラス<xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles>には、定義済みのテキスト ビュー ロールのセットがあります。 たとえば、<xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Document>主にファイルのテキスト ビューに使用されます。 <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Interactive>は、ユーザーがマウスとキーボードを使用して編集または移動できるテキスト ビューに使用されます。 ビューの<xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Interactive>例としては、エディタテキストビューや **「出力**」ウィンドウがあります。

  次の例は、表示要素プロバイダーのエクスポート属性を示しています。

```
[Export(typeof(IWpfTextViewCreationListener))]
[ContentType("csharp")]
[TextViewRole(PredefinedTextViewRoles.Document)]
internal sealed class TestAdornmentProvider : IWpfTextViewCreationListener
```

 スペースネゴシエーションの表示要素は、テキストと同じレベルのスペースを占有する表示要素です。 このような表示要素を作成するには、 を継承<xref:Microsoft.VisualStudio.Text.Tagging.SpaceNegotiatingAdornmentTag>する タグ クラスを定義する必要があります。

 すべての表示要素と同様に、表示要素レイヤー定義をエクスポートする必要があります。

```
[Export]
[Name("TestAdornment")]
[Order(After = DefaultAdornmentLayers.Text)]
internal AdornmentLayerDefinition testAdornmentLayer;
```

 スペースネゴシエーションの表示要素をインスタンス化するには、(他の種類の表示要素と同様<xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider><xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener>に) 実装するクラスに加えて、 を実装するクラスを作成する必要があります。

 タガー プロバイダーを登録するには、次の属性と共にエクスポートする必要があります。

- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>: 表示要素が有効なコンテンツの種類 ("text" や "code" など) です。

- <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute>: このタグまたは表示要素が有効なテキスト ビューの種類。 このクラス<xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles>には、定義済みのテキスト ビュー ロールのセットがあります。 たとえば、<xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Document>主にファイルのテキスト ビューに使用されます。 <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Interactive>は、ユーザーがマウスとキーボードを使用して編集または移動できるテキスト ビューに使用されます。 ビューの<xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Interactive>例としては、エディタテキストビューや **「出力**」ウィンドウがあります。

- <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute>: 定義したタグまたは表示要素の種類。 に 2 つ<xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute>目<xref:Microsoft.VisualStudio.Text.Tagging.SpaceNegotiatingAdornmentTag>のを追加する必要があります。

  次の例は、スペースネゴシエーション表示要素タグのタガー プロバイダーのエクスポート属性を示しています。

```
[Export(typeof(ITaggerProvider))]
[ContentType("text")]
[TextViewRole(PredefinedTextViewRoles.Document)]
[TagType(typeof(SpaceNegotiatingAdornmentTag))]
[TagType(typeof(TestSpaceNegotiatingTag))]
internal sealed class TestTaggerProvider : ITaggerProvider
```

## <a name="extending-mouse-processors"></a>マウス プロセッサの拡張
 マウス入力に対して特別な処理を追加できます。 処理する入力のマウス イベント<xref:Microsoft.VisualStudio.Text.Editor.MouseProcessorBase>を継承し、オーバーライドするクラスを作成します。 また、2<xref:Microsoft.VisualStudio.Text.Editor.IMouseProcessorProvider>番目のクラスに実装し、マウス ハンドラー<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>が有効なコンテンツの種類 ("text" や "code" など) を指定する クラスと共にエクスポートする必要があります。

 マウス プロセッサ プロバイダーのエクスポート属性の例を次に示します。

```
[Export(typeof(IMouseProcessorProvider))]
[Name("test mouse processor")]
[ContentType("text")]
[TextViewRole(PredefinedTextViewRoles.Interactive)]
internal sealed class TestMouseProcessorProvider : IMouseProcessorProvider
```

## <a name="extend-drop-handlers"></a>ドロップ ハンドラを拡張する
 特定の種類のテキストに対するドロップ ハンドラの動作をカスタマイズするには、実装するクラス<xref:Microsoft.VisualStudio.Text.Editor.DragDrop.IDropHandler>と、ドロップ ハンドラを作成<xref:Microsoft.VisualStudio.Text.Editor.DragDrop.IDropHandlerProvider>するために実装する 2 番目のクラスを作成します。 ドロップ ハンドラは、次の属性と共にエクスポートする必要があります。

- <xref:Microsoft.VisualStudio.Text.Editor.DragDrop.DropFormatAttribute>: このドロップ ハンドラが有効なテキスト形式。 次の形式は、優先順位の高い順に処理されます。

  1. 任意のカスタム書式

  2. Filedrop

  3. 拡張メタファイル

  4. ウェーブオーディオ

  5. リフ

  6. Dif

  7. Locale

  8. [パレット]

  9. ペンデータ

  10. シリアル化可能

  11. シンボリックリンク

  12. Xaml

  13. パッケージ

  14. Tiff

  15. Bitmap

  16. Dib

  17. メタファイルピクチャー

  18. CSV

  19. System.String

  20. HTML 形式

  21. ユニコードテキスト

  22. OEM テキスト

  23. Text

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: ドロップ ハンドラの名前。

- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>: 既定のドロップ ハンドラの前または後のドロップ ハンドラの順序。 既定のドロップ ハンドラーは"既定のファイルドロップハンドラー" という名前です。

  次の例は、ドロップ ハンドラー プロバイダーのエクスポート属性を示しています。

```
[Export(typeof(IDropHandlerProvider))]
[DropFormat("Text")]
[Name("TestDropHandler")]
[Order(Before="DefaultFileDropHandler")]
internal class TestDropHandlerProvider : IDropHandlerProvider
```

## <a name="extending-editor-options"></a>エディタ オプションの拡張
 テキスト ビューなど、特定のスコープでのみ有効なオプションを定義できます。 エディターには、エディター オプション、表示オプション、および Windows プレゼンテーション基礎 (WPF) の表示オプションの定義済みのオプションのセットが用意されています。 これらのオプションは<xref:Microsoft.VisualStudio.Text.Editor.DefaultOptions>、 、<xref:Microsoft.VisualStudio.Text.Editor.DefaultTextViewOptions>および<xref:Microsoft.VisualStudio.Text.Editor.DefaultWpfViewOptions>にあります。

 新しいオプションを追加するには、次のいずれかのオプション定義クラスからクラスを派生させます。

- <xref:Microsoft.VisualStudio.Text.Editor.EditorOptionDefinition%601>

- <xref:Microsoft.VisualStudio.Text.Editor.ViewOptionDefinition%601>

- <xref:Microsoft.VisualStudio.Text.Editor.WpfViewOptionDefinition%601>

  次の例は、ブール値を持つオプション定義をエクスポートする方法を示しています。

```
[Export(typeof(EditorOptionDefinition))]
internal sealed class TestOption : EditorOptionDefinition<bool>
```

## <a name="extend-intellisense"></a>インテリセンスを拡張する
 IntelliSense は、構造化テキストに関する情報と、それに対するステートメント補完を提供する機能のグループの総称です。 これらの機能には、ステートメント入力候補、署名ヘルプ、クイック ヒント、電球などがあります。 ステートメント入力候補は、ユーザーが言語キーワードまたはメンバー名を正しく入力するのに役立ちます。 署名ヘルプには、ユーザーが入力したメソッドの署名が表示されます。 クイック ヒントでは、型またはメンバー名の完全な署名が表示されます。 電球は、特定のコンテキストで特定の識別子に対して追加のアクションを提供します(たとえば、1 つのオカレンスの名前が変更された後に変数のすべてのオカレンスの名前を変更するなど)。

 IntelliSense 機能の設計は、すべての場合で同じです。

- IntelliSense*ブローカー*は、プロセス全体を担当します。

- IntelliSense*セッション*は、プレゼンターのトリガーと、選択のコミットまたはキャンセルの間のイベントのシーケンスを表します。 セッションは通常、ユーザージェスチャによってトリガーされます。

- IntelliSense*コント ローラー*は、セッションを開始および終了するタイミングを決定する役割を担います。 また、情報をコミットするタイミングと、セッションを取り消すタイミングも決定します。

- IntelliSense*ソース*はコンテンツを提供し、最適な一致を決定します。

- IntelliSense*プレゼンター*は、コンテンツの表示を担当します。

  ほとんどの場合、少なくとも 1 つのソースとコントローラーを提供することをお勧めします。 ディスプレイをカスタマイズする場合は、発表者を提供することもできます。

### <a name="implement-an-intellisense-source"></a>インテリセンス ソースを実装する
 ソースをカスタマイズするには、次のソース インターフェイスの 1 つ (または複数) を実装する必要があります。

- <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource>

- <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSource>

- <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource>

- <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource>

> [!IMPORTANT]
> <xref:Microsoft.VisualStudio.Language.Intellisense.ISmartTagSource>は を支持して廃止されました<xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource>。

 また、同じ種類のプロバイダーを実装する必要があります。

- <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider>

- <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSourceProvider>

- <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider>

- <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSourceProvider>

> [!IMPORTANT]
> <xref:Microsoft.VisualStudio.Language.Intellisense.ISmartTagSourceProvider>は を支持して廃止されました<xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSourceProvider>。

 プロバイダは、次の属性と共にエクスポートする必要があります。

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: ソースの名前。

- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>: ソースが適用されるコンテンツの種類 ("text" や "code" など) です。

- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>: ソースが表示される順序 (他のソースに関して)。

- 完了ソース プロバイダーのエクスポート属性の例を次に示します。

```
Export(typeof(ICompletionSourceProvider))]
[Name(" Test Statement Completion Provider")]
[Order(Before = "default")]
[ContentType("text")]
internal class TestCompletionSourceProvider : ICompletionSourceProvider
```

 IntelliSense ソースの実装の詳細については、次のチュートリアルを参照してください。

- [チュートリアル: クイック ヒントヒントを表示する](../extensibility/walkthrough-displaying-quickinfo-tooltips.md)

- [チュートリアル: 署名ヘルプの表示](../extensibility/walkthrough-displaying-signature-help.md)

- [チュートリアル: 入力候補の表示](../extensibility/walkthrough-displaying-statement-completion.md)

### <a name="implement-an-intellisense-controller"></a>インテリセンス コントローラーを実装する
 コントローラをカスタマイズするには、インターフェイスを実装する<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController>必要があります。 さらに、次の属性と共にコントローラー プロバイダーを実装する必要があります。

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: コントローラの名前。

- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>: コントローラが適用されるコンテンツの種類 ("text" や "code" など) です。

- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>: コントローラが表示される順序 (他のコントローラに関して)。

  完了コントローラー プロバイダーのエクスポート属性の例を次に示します。

```
Export(typeof(IIntellisenseControllerProvider))]
[Name(" Test Controller Provider")]
[Order(Before = "default")]
[ContentType("text")]
internal class TestIntellisenseControllerProvider : IIntellisenseControllerProvider
```

 IntelliSense コントローラーの使用の詳細については、次のチュートリアルを参照してください。

- [チュートリアル: クイック ヒントヒントを表示する](../extensibility/walkthrough-displaying-quickinfo-tooltips.md)
