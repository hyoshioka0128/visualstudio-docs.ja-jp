---
title: 言語サービスとエディターの拡張機能のポイント |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - extension points
ms.assetid: 91a6417e-a6fe-4bc2-9d9f-5173c634a99b
caps.latest.revision: 34
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5bf0e34c76406b054ea2d27434f749b676b0b30c
ms.sourcegitcommit: 4ae5e9817ad13edd05425febb322b5be6d3c3425
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2020
ms.locfileid: "91403855"
---
# <a name="language-service-and-editor-extension-points"></a>言語サービスとエディターの拡張ポイント
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

エディターには、Managed Extensibility Framework (MEF) コンポーネントパーツとして拡張できる拡張ポイントが用意されています。これには、ほとんどの言語サービス機能が含まれます。 拡張ポイントの主なカテゴリは次のとおりです。  
  
- コンテンツの種類  
  
- 分類の種類と分類の形式  
  
- 余白とスクロールバー  
  
- Tags  
  
- 修飾  
  
- マウスプロセッサ  
  
- ハンドラーの削除  
  
- オプション  
  
- IntelliSense  
  
## <a name="extending-content-types"></a>コンテンツの種類の拡張  
 コンテンツの種類は、"text"、"code"、"CSharp" など、エディターによって処理されるテキストの種類の定義です。 新しいコンテンツの種類を定義するには、型の変数を宣言 <xref:Microsoft.VisualStudio.Utilities.ContentTypeDefinition> し、新しいコンテンツの種類に一意の名前を付けます。 コンテンツタイプをエディターに登録するには、次の属性と一緒にエクスポートします。  
  
- <xref:Microsoft.VisualStudio.Utilities.NameAttribute> コンテンツタイプの名前を指定します。  
  
- <xref:Microsoft.VisualStudio.Utilities.BaseDefinitionAttribute> このコンテンツタイプの派生元のコンテンツタイプの名前を指定します。 コンテンツの種類は、他の複数のコンテンツの種類から継承できます。  
  
  <xref:Microsoft.VisualStudio.Utilities.ContentTypeDefinition>クラスはシールされているため、型パラメーターを指定せずにエクスポートできます。  
  
  次の例では、コンテンツタイプ定義の export 属性を示します。  
  
```  
[Export]  
[Name("test")]  
[BaseDefinition("code")]  
[BaseDefinition("projection")]  
internal static ContentTypeDefinition TestContentTypeDefinition;  
```  
  
 コンテンツの種類は、0個以上の既存のコンテンツの種類に基づいて作成できます。 組み込み型は次のとおりです。  
  
- Any: 基本的なコンテンツの種類。 他のすべてのコンテンツタイプの親。  
  
- Text: 非投影コンテンツの基本型。 "Any" から継承します。  
  
- Plaintext: 非コードテキストの場合。 "Text" から継承します。  
  
- Code: すべての種類のコードを対象としています。 "Text" から継承します。  
  
- のみ: 任意の種類の処理からテキストを除外します。 このコンテンツの種類のテキストには、どのような拡張子も適用されません。  
  
- 射影: プロジェクションバッファーの内容。 "Any" から継承します。  
  
- Intellisense: IntelliSense の内容。 "Text" から継承します。  
  
- Sighelp: シグネチャのヘルプ。 "Intellisense" から継承します。  
  
- Sighelp-doc: シグネチャヘルプドキュメント。 "Intellisense" から継承します。  
  
  Visual Studio で定義されているコンテンツの種類と、Visual Studio でホストされている言語の一部を次に示します。  
  
- Basic  
  
- C/C++  
  
- ConsoleOutput  
  
- CSharp  
  
- CSS  
  
- ENC  
  
- FindResults  
  
- F#  
  
- HTML  
  
- JScript  
  
- XAML  
  
- XML  
  
  使用可能なコンテンツの種類の一覧を検出するには、 <xref:Microsoft.VisualStudio.Utilities.IContentTypeRegistryService> エディターのコンテンツタイプのコレクションを保持するをインポートします。 次のコードでは、このサービスをプロパティとしてインポートします。  
  
```  
[Import]  
internal IContentTypeRegistryService ContentTypeRegistryService { get; set; }  
```  
  
 コンテンツの種類をファイル名拡張子に関連付けるには、を使用し <xref:Microsoft.VisualStudio.Utilities.FileExtensionToContentTypeDefinition> ます。  
  
> [!NOTE]
> Visual Studio では、言語サービスパッケージでを使用してファイル名拡張子が登録され <xref:Microsoft.VisualStudio.Shell.ProvideLanguageExtensionAttribute> ます。 は、 <xref:Microsoft.VisualStudio.Utilities.FileExtensionToContentTypeDefinition> この方法で登録されたファイル名拡張子を持つ MEF コンテンツタイプを関連付けます。  
  
 ファイル名の拡張子をコンテンツの種類の定義にエクスポートするには、次の属性を含める必要があります。  
  
- <xref:Microsoft.VisualStudio.Utilities.FileExtensionAttribute>: ファイル名拡張子を指定します。  
  
- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>: コンテンツの種類を指定します。  
  
  <xref:Microsoft.VisualStudio.Utilities.FileExtensionToContentTypeDefinition>クラスはシールされているため、型パラメーターを指定せずにエクスポートできます。  
  
  次の例では、ファイル名拡張子の属性をコンテンツタイプ定義にエクスポートする方法を示します。  
  
```  
[Export]  
[FileExtension(".test")]  
[ContentType("test")]  
internal static FileExtensionToContentTypeDefinition TestFileExtensionDefinition;  
```  
  
 は、 <xref:Microsoft.VisualStudio.Utilities.IFileExtensionRegistryService> ファイル名拡張子とコンテンツタイプの間の関連付けを管理します。  
  
## <a name="extending-classification-types-and-classification-formats"></a>分類の種類と分類の形式の拡張  
 分類の種類を使用すると、さまざまな処理を提供するテキストの種類を定義できます (たとえば、"keyword" というテキストを緑色にし、"comment" というテキストを緑色にするなど)。 型の変数を宣言し、それに一意の名前を付けることによって、新しい分類の種類を定義し <xref:Microsoft.VisualStudio.Text.Classification.ClassificationTypeDefinition> ます。  
  
 エディターに分類の種類を登録するには、次の属性を使用して分類の種類をエクスポートします。  
  
- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: 分類の種類の名前。  
  
- <xref:Microsoft.VisualStudio.Utilities.BaseDefinitionAttribute>: この分類の種類の継承元となる分類の種類の名前。 すべての分類の種類は "テキスト" を継承し、分類の種類は他の複数の分類の種類から継承できます。  
  
  <xref:Microsoft.VisualStudio.Text.Classification.ClassificationTypeDefinition>クラスはシールされているため、型パラメーターを指定せずにエクスポートできます。  
  
  次の例では、分類の種類の定義に対する export 属性を示します。  
  
```  
[Export]  
[Name("csharp.test")]  
[BaseDefinition("test")]  
internal static ClassificationTypeDefinition CSharpTestDefinition;  
```  
  
 は、 <xref:Microsoft.VisualStudio.Language.StandardClassification.IStandardClassificationService> 標準分類へのアクセスを提供します。 組み込みの分類の種類には、次のものが含まれます。  
  
- "text"  
  
- "自然言語" ("テキスト" から派生)  
  
- "正式な言語" ("text" から派生)  
  
- "string" ("literal" から派生)  
  
- "character" ("literal" から派生)  
  
- "数値" ("literal" から派生)  
  
  さまざまなエラーの種類のセットがから継承 <xref:Microsoft.VisualStudio.Text.Adornments.ErrorTypeDefinition> しています。 次のエラーの種類が含まれます。  
  
- "構文エラー"  
  
- "コンパイラエラー"  
  
- "その他のエラー"  
  
- 要する  
  
  使用可能な分類の種類の一覧を確認するには、をインポートし <xref:Microsoft.VisualStudio.Text.Classification.IClassificationTypeRegistryService> ます。これにより、エディターの分類の種類のコレクションが保持されます。 次のコードでは、このサービスをプロパティとしてインポートします。  
  
```  
[Import]  
internal IClassificationTypeRegistryService ClassificationTypeRegistryService { get; set; }  
```  
  
 新しい分類の種類の分類形式の定義を定義できます。 からクラスを派生させ、型を使用して <xref:Microsoft.VisualStudio.Text.Classification.ClassificationFormatDefinition> 、次の属性と共にエクスポートし <xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition> ます。  
  
- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: 形式の名前。  
  
- <xref:Microsoft.VisualStudio.Utilities.DisplayNameAttribute>: 形式の表示名。  
  
- <xref:Microsoft.VisualStudio.Text.Classification.UserVisibleAttribute>: [**オプション**] ダイアログボックスの [**フォントおよび色**] ページに書式を表示するかどうかを指定します。  
  
- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>: 形式の優先順位。 有効な値はから <xref:Microsoft.VisualStudio.Text.Classification.Priority> です。  
  
- <xref:Microsoft.VisualStudio.Text.Classification.ClassificationTypeAttribute>: この形式のマップ先となる分類の種類の名前。  
  
  次の例では、分類形式の定義のエクスポート属性を示します。  
  
```  
[Export(typeof(EditorFormatDefinition))]  
[ClassificationType(ClassificationTypeNames = "test")]  
[Name("test")]  
[DisplayName("Test")]  
[UserVisible(true)]  
[Order(After = Priority.Default, Before = Priority.High)]  
internal sealed class TestFormat : ClassificationFormatDefinition  
```  
  
 使用可能な形式の一覧を検出するには、 <xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMapService> エディターの形式のコレクションを保持するをインポートします。 次のコードでは、このサービスをプロパティとしてインポートします。  
  
```  
[Import]  
internal IEditorFormatMapService FormatMapService { get; set; }  
```  
  
## <a name="extending-margins-and-scrollbars"></a>余白とスクロールバーの拡張  
 余白とスクロールバーは、テキストビュー自体に加えて、エディターのメインビュー要素です。 テキストビューの周囲に表示される標準の余白に加えて、任意の数の余白を指定できます。  
  
 <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewMargin>余白を定義するインターフェイスを実装します。 また、 <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewMarginProvider> 余白を作成するには、インターフェイスも実装する必要があります。  
  
 余白プロバイダーをエディターに登録するには、次の属性を使用してプロバイダーをエクスポートする必要があります。  
  
- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: 余白の名前。  
  
- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>: 他の余白を基準とする余白の表示順序。  
  
   組み込みの余白は次のとおりです。  
  
  - "Wpf 水平スクロールバー"  
  
  - "Wpf 垂直スクロールバー"  
  
  - "Wpf の行番号の余白"  
  
    の order 属性を持つ水平余白 `After="Wpf Horizontal Scrollbar"` は、組み込みの余白の下に表示されます。また、order 属性がの水平余白は `Before ="Wpf Horizontal Scrollbar"` 、組み込みの余白の上に表示されます。 Order 属性がの右縦余白 `After="Wpf Vertical Scrollbar"` がスクロールバーの右側に表示されます。 順序の属性がの左の垂直方向の余白 `After="Wpf Line Number Margin"` は、行番号の余白の左側に表示されます (表示されている場合)。  
  
- <xref:Microsoft.VisualStudio.Text.Editor.MarginContainerAttribute>: 余白の種類 (left、right、top、または bottom)。  
  
- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>: 余白が有効なコンテンツの種類 (たとえば、"text" または "code")。  
  
  次の例は、行番号の余白の右側に表示される余白の余白プロバイダーに対するエクスポート属性を示しています。  
  
```  
[Export(typeof(IWpfTextViewMarginProvider))]  
[Name("TestMargin")]  
[Order(Before = "Wpf Line Number Margin")]  
[MarginContainer(PredefinedMarginNames.Left)]  
[ContentType("text")]   
```  
  
## <a name="extending-tags"></a>タグの拡張  
 タグを使用すると、データをさまざまな種類のテキストに関連付けることができます。 多くの場合、関連付けられたデータは視覚的な効果として表示されますが、すべてのタグが視覚的に表示されるわけではありません。 を実装することで、独自の種類のタグを定義でき <xref:Microsoft.VisualStudio.Text.Tagging.ITag> ます。 また、を実装して、 <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> 特定のテキスト範囲のセットにタグを指定し、を使用してタグを提供する必要があり <xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider> ます。 タガープロバイダーを次の属性と共にエクスポートする必要があります。  
  
- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>: タグが有効なコンテンツの種類 (たとえば、"text" または "code")。  
  
- <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute>: タグの種類。  
  
  次の例では、タグプロバイダーの export 属性を示します。  
  
```  
[Export(typeof(ITaggerProvider))]  
[ContentType("text")]  
[TagType(typeof(TestTag))]  
internal class TestTaggerProvider : ITaggerProvider  
```  
  
 次の種類のタグが組み込まれています。  
  
- <xref:Microsoft.VisualStudio.Text.Tagging.ClassificationTag>: に関連付けられて <xref:Microsoft.VisualStudio.Text.Classification.IClassificationType> います。  
  
- <xref:Microsoft.VisualStudio.Text.Tagging.ErrorTag>: エラーの種類に関連付けられています。  
  
- <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>: 装飾に関連付けられています。  
  
  > [!NOTE]
  > の例につい <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> ては、「 [チュートリアル: テキストの強調表示](../extensibility/walkthrough-highlighting-text.md)」の HighlightWordTag の定義を参照してください。  
  
- <xref:Microsoft.VisualStudio.Text.Tagging.OutliningRegionTag>: アウトラインで展開または折りたたむことができる領域に関連付けられています。  
  
- <xref:Microsoft.VisualStudio.Text.Tagging.SpaceNegotiatingAdornmentTag>: テキストビューでの表示要素の占有領域を定義します。 領域をネゴシエートする装飾の詳細については、次のセクションを参照してください。  
  
- <xref:Microsoft.VisualStudio.Text.Editor.IntraTextAdornmentTag>: 表示要素の間隔とサイズを自動調整します。  
  
  バッファーとビューのタグを検索して使用するに <xref:Microsoft.VisualStudio.Text.Tagging.IViewTagAggregatorFactoryService> は、またはをインポートし <xref:Microsoft.VisualStudio.Text.Tagging.IBufferTagAggregatorFactoryService> ます。これにより、要求された型のが得られ <xref:Microsoft.VisualStudio.Text.Tagging.ITagAggregator%601> ます。 次のコードでは、このサービスをプロパティとしてインポートします。  
  
```  
[Import]  
internal IViewTagAggregatorFactoryService ViewTagAggregatorFactoryService { get; set; }  
```  
  
#### <a name="tags-and-markerformatdefinitions"></a>タグと MarkerFormatDefinitions  
 クラスを拡張し <xref:Microsoft.VisualStudio.Text.Classification.MarkerFormatDefinition> て、タグの外観を定義できます。 次の属性を使用して、クラスを (として) エクスポートする必要があり <xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition> ます。  
  
- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: この形式を参照するために使用される名前  
  
- <xref:Microsoft.VisualStudio.Text.Classification.UserVisibleAttribute>: これにより、形式が UI に表示されます。  
  
  コンストラクターでは、タグの表示名と外観を定義します。 <xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition.BackgroundColor%2A> 塗りつぶしの色を定義し、 <xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition.ForegroundColor%2A> 境界線の色を定義します。 は、 <xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition.DisplayName%2A> 形式定義のローカライズ可能な名前です。  
  
  書式定義の例を次に示します。  
  
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
  
 この書式定義をタグに適用するには、(表示名ではなく) クラスの name 属性で設定した名前を参照します。  
  
> [!NOTE]
> の例につい <xref:Microsoft.VisualStudio.Text.Classification.MarkerFormatDefinition> ては、「 [チュートリアル: テキストの強調表示](../extensibility/walkthrough-highlighting-text.md)」の HighlightWordFormatDefinition クラスを参照してください。  
  
## <a name="extending-adornments"></a>装飾の拡張  
 装飾は、テキストビューに表示されるテキストか、テキストビュー自体に追加できる視覚効果を定義します。 独自の表示形式は、任意の型として定義でき <xref:System.Windows.UIElement> ます。  
  
 表示要素では、を宣言する必要があり <xref:Microsoft.VisualStudio.Text.Editor.AdornmentLayerDefinition> ます。 装飾レイヤーを登録するには、次の属性を使用してそれをエクスポートします。  
  
- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: 装飾の名前。  
  
- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>: 他の装飾層に対する装飾の順序。 クラスは、 <xref:Microsoft.VisualStudio.Text.Editor.PredefinedAdornmentLayers> 選択、アウトライン、キャレット、テキストという4つの既定のレイヤーを定義します。  
  
  次の例では、表示要素層の定義に対するエクスポート属性を示します。  
  
```  
[Export]  
[Name("TestEmbeddedAdornment")]  
[Order(After = PredefinedAdornmentLayers.Selection, Before = PredefinedAdornmentLayers.Text)]  
internal AdornmentLayerDefinition testLayerDefinition;  
```  
  
 表示要素をインスタンス化する <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener> ことによって、そのイベントを実装して処理する2番目のクラスを作成する必要があり <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener.TextViewCreated%2A> ます。 このクラスは、次の属性と共にエクスポートする必要があります。  
  
- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>: 装飾が有効なコンテンツの種類 (例: "テキスト" または "コード")。  
  
- <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute>: この表示要素が有効なテキストビューの種類。 クラスには、 <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles> 定義済みのテキストビューロールのセットがあります。 たとえば、 <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Document> は、主にファイルのテキストビューに使用されます。 <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Interactive> は、ユーザーがマウスやキーボードを使用して編集または移動できるテキストビューに使用されます。 ビューの例として <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Interactive> は、エディターのテキストビューや **出力** ウィンドウなどがあります。  
  
  次の例は、表示要素のエクスポート属性を示しています。  
  
```  
[Export(typeof(IWpfTextViewCreationListener))]  
[ContentType("csharp")]  
[TextViewRole(PredefinedTextViewRoles.Document)]  
internal sealed class TestAdornmentProvider : IWpfTextViewCreationListener  
```  
  
 スペースをネゴシエートする表示要素とは、テキストと同じレベルにある領域を占有するものです。 この種類の表示要素を作成するには、を継承するタグクラスを定義する必要があり <xref:Microsoft.VisualStudio.Text.Tagging.SpaceNegotiatingAdornmentTag> ます。これは、表示要素が占める領域の量を定義します。  
  
 すべての修飾要素と同様に、表示要素レイヤーの定義をエクスポートする必要があります。  
  
```  
[Export]  
[Name("TestAdornment")]  
[Order(After = DefaultAdornmentLayers.Text)]  
internal AdornmentLayerDefinition testAdornmentLayer;  
```  
  
 領域をネゴシエートする装飾をインスタンス化するには、 <xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider> を実装するクラスに加えて、を実装するクラスを <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener> (他の種類の装飾と同様に) 作成する必要があります。  
  
 タガープロバイダーを登録するには、次の属性を使用して、そのプロバイダーをエクスポートする必要があります。  
  
- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>: 表示要素が有効なコンテンツの種類 (たとえば、"text" または "code")。  
  
- <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute>: このタグまたは装飾が有効なテキストビューの種類。 クラスには、 <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles> 定義済みのテキストビューロールのセットがあります。 たとえば、 <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Document> は、主にファイルのテキストビューに使用されます。 <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Interactive> は、ユーザーがマウスやキーボードを使用して編集または移動できるテキストビューに使用されます。 ビューの例として <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Interactive> は、エディターのテキストビューや **出力** ウィンドウなどがあります。  
  
- <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute>: 定義したタグまたは表示要素の種類。 の2つ目のを追加する必要があり <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute> <xref:Microsoft.VisualStudio.Text.Tagging.SpaceNegotiatingAdornmentTag> ます。  
  
  次の例では、スペースをネゴシエートする表示要素のタグについて、タガープロバイダーの export 属性を示しています。  
  
```  
[Export(typeof(ITaggerProvider))]  
[ContentType("text")]  
[TextViewRole(PredefinedTextViewRoles.Document)]  
[TagType(typeof(SpaceNegotiatingAdornmentTag))]  
[TagType(typeof(TestSpaceNegotiatingTag))]  
internal sealed class TestTaggerProvider : ITaggerProvider  
```  
  
## <a name="extending-mouse-processors"></a>マウスプロセッサの拡張  
 マウス入力の特別な処理を追加できます。 を継承するクラスを作成 <xref:Microsoft.VisualStudio.Text.Editor.MouseProcessorBase> し、処理する入力のマウスイベントをオーバーライドします。 また <xref:Microsoft.VisualStudio.Text.Editor.IMouseProcessorProvider> 、2番目のクラスでを実装し、 <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> マウスハンドラーが有効であるコンテンツの種類 (たとえば、"text" または "code") を指定するをと共にエクスポートする必要があります。  
  
 次の例は、マウスプロセッサプロバイダーのエクスポート属性を示しています。  
  
```  
[Export(typeof(IMouseProcessorProvider))]  
[Name("test mouse processor")]  
[ContentType("text")]  
[TextViewRole(PredefinedTextViewRoles.Interactive)]   
internal sealed class TestMouseProcessorProvider : IMouseProcessorProvider  
```  
  
## <a name="extending-drop-handlers"></a>拡張 (ドロップハンドラーを)  
 を実装するクラスを作成し、 <xref:Microsoft.VisualStudio.Text.Editor.DragDrop.IDropHandler> <xref:Microsoft.VisualStudio.Text.Editor.DragDrop.IDropHandlerProvider> ドロップハンドラーを作成するためにを実装する2番目のクラスを作成することによって、特定の種類のテキストのドロップハンドラーの動作をカスタマイズできます。 ドロップハンドラーは、次の属性と共にエクスポートする必要があります。  
  
- <xref:Microsoft.VisualStudio.Text.Editor.DragDrop.DropFormatAttribute>: このドロップハンドラーが有効なテキスト形式。 次の形式は、優先順位の高いものから順に処理されます。  
  
  1. 任意のカスタム書式  
  
  2. FileDrop  
  
  3. EnhancedMetafile  
  
  4. WaveAudio  
  
  5. Riff  
  
  6. 差分  
  
  7. ロケール  
  
  8. [パレット]  
  
  9. ペンデータ  
  
  10. シリアル化可能  
  
  11. SymbolicLink  
  
  12. Xaml  
  
  13. XamlPackage  
  
  14. Tiff  
  
  15. Bitmap  
  
  16. .Dib  
  
  17. メタファイルの画像  
  
  18. CSV  
  
  19. System.String  
  
  20. HTML 形式  
  
  21. UnicodeText  
  
  22. OEMText  
  
  23. Text  
  
- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: ドロップハンドラーの名前。  
  
- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>: 既定のドロップハンドラーの前または後のドロップハンドラーの順序。 Visual Studio の既定のドロップハンドラーには、"DefaultFileDropHandler" という名前が付けられています。  
  
  次の例では、drop handler プロバイダーの export 属性を示します。  
  
```  
[Export(typeof(IDropHandlerProvider))]  
[DropFormat("Text")]   
[Name("TestDropHandler")]  
[Order(Before="DefaultFileDropHandler")]   
internal class TestDropHandlerProvider : IDropHandlerProvider  
```  
  
## <a name="extending-editor-options"></a>拡張 (エディターオプションを)  
 たとえば、テキストビューでは、特定のスコープでのみ有効なオプションを定義できます。 エディターには、エディターオプション、表示オプション、および Windows Presentation Foundation (WPF) ビューオプションの一連の定義済みオプションが用意されています。 これらのオプションについては、「」、「」、および「」を参照し <xref:Microsoft.VisualStudio.Text.Editor.DefaultOptions> <xref:Microsoft.VisualStudio.Text.Editor.DefaultTextViewOptions> て <xref:Microsoft.VisualStudio.Text.Editor.DefaultWpfViewOptions> ください。  
  
 新しいオプションを追加するには、次のいずれかのオプション定義クラスからクラスを派生させます。  
  
- <xref:Microsoft.VisualStudio.Text.Editor.EditorOptionDefinition%601>  
  
- <xref:Microsoft.VisualStudio.Text.Editor.ViewOptionDefinition%601>  
  
- <xref:Microsoft.VisualStudio.Text.Editor.WpfViewOptionDefinition%601>  
  
  次の例では、ブール値を持つオプション定義をエクスポートする方法を示します。  
  
```  
[Export(typeof(EditorOptionDefinition))]  
internal sealed class TestOption : EditorOptionDefinition<bool>  
```  
  
## <a name="extending-intellisense"></a>拡張 (IntelliSense を)  
 IntelliSense は、構造化されたテキストに関する情報を提供する機能のグループと、それに対するステートメント入力候補に関する一般的な用語です。 これらの機能には、ステートメント入力候補、署名ヘルプ、クイックヒント、電球などがあります。 ユーザーは、ステートメント入力候補を使用して、言語キーワードまたはメンバー名を正しく入力できます。 署名のヘルプでは、ユーザーが入力したメソッドの署名または署名が表示されます。 クイックヒントを使用すると、型またはメンバー名の完全な署名が表示されます。 電球は、特定のコンテキストの特定の識別子に対して追加のアクションを提供します。たとえば、1回の出現後にすべての変数の名前を変更した場合などです。  
  
 IntelliSense 機能の設計は、どのような場合でもほぼ同じです。  
  
- IntelliSense *ブローカー* は、プロセス全体を担当します。  
  
- IntelliSense *セッション* は、プレゼンターのトリガーと選択のコミットまたは取り消しの間のイベントのシーケンスを表します。 通常、セッションはユーザージェスチャによってトリガーされます。  
  
- IntelliSense *コントローラー* は、セッションの開始と終了のタイミングを決定する役割を担います。 また、情報をコミットするタイミングと、セッションをいつキャンセルするかを決定します。  
  
- IntelliSense *ソース* はコンテンツを提供し、最も一致するものを決定します。  
  
- IntelliSense *プレゼンター* は、コンテンツを表示する役割を担います。  
  
  ほとんどの場合、少なくともソースとコントローラーを指定することをお勧めします。 表示をカスタマイズする場合は、プレゼンターを指定することもできます。  
  
### <a name="implementing-an-intellisense-source"></a>IntelliSense ソースの実装  
 ソースをカスタマイズするには、次のソースインターフェイスの1つ (または複数) を実装する必要があります。  
  
- <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource>  
  
- <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSource>  
  
- <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource>  
  
- <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource>  
  
> [!IMPORTANT]
> <xref:Microsoft.VisualStudio.Language.Intellisense.ISmartTagSource> は、を優先するために非推奨とされました <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource> 。  
  
 さらに、同じ種類のプロバイダーを実装する必要があります。  
  
- <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider>  
  
- <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSourceProvider>  
  
- <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider>  
  
- <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSourceProvider>  
  
> [!IMPORTANT]
> <xref:Microsoft.VisualStudio.Language.Intellisense.ISmartTagSourceProvider> は、を優先するために非推奨とされました <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSourceProvider> 。  
  
 次の属性を使用して、プロバイダーをエクスポートする必要があります。  
  
- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: ソースの名前。  
  
- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>: ソースが適用されるコンテンツの種類 (たとえば、"text" または "code")。  
  
- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>: ソースが表示される順序 (他のソースに関して)。  
  
- 次の例は、完了ソースプロバイダーでのエクスポート属性を示しています。  
  
```  
Export(typeof(ICompletionSourceProvider))]  
[Name(" Test Statement Completion Provider")]  
[Order(Before = "default")]  
[ContentType("text")]  
internal class TestCompletionSourceProvider : ICompletionSourceProvider  
```  
  
 IntelliSense ソースの実装の詳細については、次のチュートリアルを参照してください。  
  
 [チュートリアル: クイック ヒントの表示](../extensibility/walkthrough-displaying-quickinfo-tooltips.md)  
  
 [チュートリアル: シグネチャ ヘルプの表示](../extensibility/walkthrough-displaying-signature-help.md)  
  
 [チュートリアル: 入力候補の表示](../extensibility/walkthrough-displaying-statement-completion.md)  
  
### <a name="implementing-an-intellisense-controller"></a>IntelliSense コントローラーの実装  
 コントローラーをカスタマイズするには、インターフェイスを実装する必要があり <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController> ます。 さらに、次の属性と共にコントローラープロバイダーを実装する必要があります。  
  
- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: コントローラーの名前。  
  
- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>: コントローラーが適用されるコンテンツの種類 (たとえば、"text" または "code")。  
  
- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>: コントローラーが表示される順序 (他のコントローラーに対して)。  
  
  次の例は、完了コントローラープロバイダーのエクスポート属性を示しています。  
  
```  
Export(typeof(IIntellisenseControllerProvider))]  
[Name(" Test Controller Provider")]  
[Order(Before = "default")]  
[ContentType("text")]  
internal class TestIntellisenseControllerProvider : IIntellisenseControllerProvider  
```  
  
 IntelliSense コントローラーの使用方法の詳細については、次のチュートリアルを参照してください。  
  
 [チュートリアル: クイック ヒントの表示](../extensibility/walkthrough-displaying-quickinfo-tooltips.md)
