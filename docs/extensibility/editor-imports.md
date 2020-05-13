---
title: エディタのインポート |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - services
ms.assetid: 8d096de3-33b4-427a-a122-4aeff8a72da0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c6af95b452166aa71950ac1e869d333d12d857b9
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712009"
---
# <a name="editor-imports"></a>エディターのインポート
コア・エディターに対してさまざまな種類のアクセス権を持つ拡張機能を提供する、エディター・サービス、ファクトリー、ブローカーの数をインポートできます。 たとえば、 を<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>インポートして、特定のコンテンツ タイプ<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigator>の を提供できます。 (このナビゲーターを使用すると、テキストバッファーに対してさまざまな種類の検索を実行できます)。

 エディターのインポートを使用するには、マネージ機能拡張フレームワーク コンポーネントパーツをエクスポートするクラスのフィールドまたはプロパティとしてインポートします。

> [!NOTE]
> マネージ機能拡張フレームワークの詳細については、「マネージ機能拡張フレームワーク[(MEF) 」](/dotnet/framework/mef/index)を参照してください。

## <a name="import-syntax"></a>インポート構文
 次の例は、エディター オプション ファクトリ サービスをインポートする方法を示しています。

```
[Import]
internal IEditorOptionsFactoryService EditorOptions { get; set; }
```

 プロパティではなくフィールドとしてサービスをインポートする場合は、変数に割り当てられていないというコンパイラ`null`警告を避けるために、宣言でサービスをに設定する必要があります。

```
[Import]
internal IEditorOptionsFactoryService m_editorOptions = null;
```

 インポートの使用例については、次のチュートリアルを参照してください。

- [チュートリアル: 余白グリフを作成する](../extensibility/walkthrough-creating-a-margin-glyph.md)

- [チュートリアル: テキスト ビューをカスタマイズする](../extensibility/walkthrough-customizing-the-text-view.md)

- [チュートリアル: テキストを強調表示する](../extensibility/walkthrough-highlighting-text.md)

- [チュートリアル: クイック ヒントヒントを表示する](../extensibility/walkthrough-displaying-quickinfo-tooltips.md)

- [チュートリアル: 署名ヘルプの表示](../extensibility/walkthrough-displaying-signature-help.md)

- [チュートリアル: 入力候補の表示](../extensibility/walkthrough-displaying-statement-completion.md)

- [チュートリアル: 電球候補を表示する](../extensibility/walkthrough-displaying-light-bulb-suggestions.md)

## <a name="import-the-service-provider"></a>サービス プロバイダーをインポートする
 Visual Studio サービス<xref:Microsoft.VisualStudio.Shell.SVsServiceProvider>にアクセスするのと同じ方法で (アセンブリで見つかった) をインポートすることもできます。

```csharp
[Import]
internal SVsServiceProvider ServiceProvider = null;
```

 詳細については、「[チュートリアル: エディター拡張機能から DTE オブジェクトにアクセス](../extensibility/walkthrough-accessing-the-dte-object-from-an-editor-extension.md)する」を参照してください。

## <a name="services"></a>サービス
 エディター サービスは、一般にサービスを提供する単一のエンティティであり、複数のコンポーネント間で共有されます。

|[インポート]|提供する|
|------------|--------------|
|<xref:Microsoft.VisualStudio.Utilities.IFileExtensionRegistryService>|ファイル拡張子とオブジェクトの<xref:Microsoft.VisualStudio.Utilities.IContentType>関係。|
|<xref:Microsoft.VisualStudio.Utilities.IContentTypeRegistryService>|<xref:Microsoft.VisualStudio.Utilities.IContentType> オブジェクトのコレクション。|
|<xref:Microsoft.VisualStudio.Editor.IVsFontsAndColorsInformationService>|<xref:Microsoft.VisualStudio.Editor.IVsFontsAndColorsInformation>オブジェクト。|
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService>|多くのエディター アダプター オブジェクト:<br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>|
|<xref:Microsoft.VisualStudio.Text.IncrementalSearch.IIncrementalSearchFactoryService>|指定<xref:Microsoft.VisualStudio.Text.IncrementalSearch.IIncrementalSearch>したテキスト ビューのオブジェクト。|
|<xref:Microsoft.VisualStudio.Text.ITextBufferFactoryService>|<xref:Microsoft.VisualStudio.Text.ITextBuffer>。|
|<xref:Microsoft.VisualStudio.Text.ITextDocumentFactoryService>|<xref:Microsoft.VisualStudio.Text.ITextDocument>。|
|<xref:Microsoft.VisualStudio.Text.Differencing.IDifferenceService>|違<xref:Microsoft.VisualStudio.Text.Differencing.IDifferenceCollection%601>いの一種。|
|<xref:Microsoft.VisualStudio.Text.Differencing.IHierarchicalStringDifferenceService>|違<xref:Microsoft.VisualStudio.Text.Differencing.IHierarchicalDifferenceCollection>いの一種。|
|<xref:Microsoft.VisualStudio.Text.Projection.IProjectionBufferFactoryService>|または<xref:Microsoft.VisualStudio.Text.Projection.IProjectionBuffer>、 <xref:Microsoft.VisualStudio.Text.Projection.IElisionBuffer>.|
|<xref:Microsoft.VisualStudio.Text.Projection.IBufferGraphFactoryService>|オブジェクト<xref:Microsoft.VisualStudio.Text.Projection.IBufferGraph>のセットの場合<xref:Microsoft.VisualStudio.Text.ITextBuffer>。|
|<xref:Microsoft.VisualStudio.Text.Classification.IClassifierAggregatorService>|の<xref:Microsoft.VisualStudio.Text.Classification.IClassifier>場合は<xref:Microsoft.VisualStudio.Text.ITextBuffer>.|
|<xref:Microsoft.VisualStudio.Text.Classification.IViewClassifierAggregatorService>|の<xref:Microsoft.VisualStudio.Text.Classification.IClassifier>場合は<xref:Microsoft.VisualStudio.Text.Editor.ITextView>.|
|<xref:Microsoft.VisualStudio.Text.Classification.IClassificationFormatMapService>|の<xref:Microsoft.VisualStudio.Text.Classification.IClassificationFormatMap>場合は<xref:Microsoft.VisualStudio.Text.Editor.ITextView>.|
|<xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMapService>|の<xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMap>場合は<xref:Microsoft.VisualStudio.Text.Editor.ITextView>.|
|<xref:Microsoft.VisualStudio.Text.Classification.IClassificationTypeRegistryService>|オブジェクトのコレクションを<xref:Microsoft.VisualStudio.Text.Classification.IClassificationType>保持します。|
|<xref:Microsoft.VisualStudio.Text.Tagging.IBufferTagAggregatorFactoryService>|テキスト<xref:Microsoft.VisualStudio.Text.Tagging.ITagAggregator%601>バッファーの場合。|
|<xref:Microsoft.VisualStudio.Text.Tagging.IViewTagAggregatorFactoryService>|テキスト<xref:Microsoft.VisualStudio.Text.Tagging.ITagAggregator%601>ビューの場合。|
|<xref:Microsoft.VisualStudio.Text.Editor.IEditorOptionsFactoryService>|指定<xref:Microsoft.VisualStudio.Text.Editor.IEditorOptions>されたスコープの。|
|<xref:Microsoft.VisualStudio.Text.Editor.IScrollMapFactoryService>|テキスト<xref:Microsoft.VisualStudio.Text.Editor.IScrollMap>ビューの場合。|
|<xref:Microsoft.VisualStudio.Text.Editor.ISmartIndentationService>|の<xref:Microsoft.VisualStudio.Text.Editor.ISmartIndent>場合は<xref:Microsoft.VisualStudio.Text.Editor.ITextView>.|
|<xref:Microsoft.VisualStudio.Text.Editor.ISmartIndentationService>|オブジェクトを使用して自動的にインデントを<xref:Microsoft.VisualStudio.Text.Editor.ISmartIndentProvider>取得します。|
|<xref:Microsoft.VisualStudio.Text.Editor.ITextEditorFactoryService>|の を<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewHost>管理します<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextView>。|
|<xref:Microsoft.VisualStudio.Text.Formatting.IFormattedTextSourceFactoryService>|<xref:Microsoft.VisualStudio.Text.Formatting.IFormattedLineSource>。|
|<xref:Microsoft.VisualStudio.Text.Formatting.IRtfBuilderService>|スナップショット範囲のセットから RTF 形式のテキストを生成します。|
|<xref:Microsoft.VisualStudio.Text.Formatting.ITextAndAdornmentSequencerFactoryService>|の<xref:Microsoft.VisualStudio.Text.Formatting.ITextAndAdornmentSequencer>場合は<xref:Microsoft.VisualStudio.Text.Editor.ITextView>.|
|<xref:Microsoft.VisualStudio.Text.Formatting.ITextParagraphPropertiesFactoryService>|ビュー<xref:System.Windows.Media.TextFormatting.TextParagraphProperties>内のテキスト行を書式設定するための A。|
|<xref:Microsoft.VisualStudio.Text.Operations.IEditorOperationsFactoryService>|の<xref:Microsoft.VisualStudio.Text.Operations.IEditorOperations>オブジェクト。 <xref:Microsoft.VisualStudio.Text.Editor.ITextView>|
|<xref:Microsoft.VisualStudio.Text.Operations.ITextSearchService>|テキスト スナップショットを検索します。|
|<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>|によって<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigator>、<xref:Microsoft.VisualStudio.Text.ITextBuffer>の<xref:Microsoft.VisualStudio.Utilities.IContentType>場合の A です。|
|<xref:Microsoft.VisualStudio.Text.Outlining.IOutliningManagerService>|テキスト<xref:Microsoft.VisualStudio.Text.Outlining.IOutliningManager>ビューの場合。|
|<xref:Microsoft.VisualStudio.Language.Intellisense.IGlyphService>|グリフの標準セット。|
|<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseSessionStackMapService>|の<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseSessionStack>場合は<xref:Microsoft.VisualStudio.Text.Editor.ITextView>.|
|<xref:Microsoft.VisualStudio.Language.Intellisense.IWpfKeyboardTrackingService>|キーボードの処理を追跡します。|
|<xref:Microsoft.VisualStudio.Language.StandardClassification.IStandardClassificationService>|標準<xref:Microsoft.VisualStudio.Text.Classification.IClassificationType>オブジェクト。|
|<xref:Microsoft.VisualStudio.Text.Operations.ITextUndoHistoryRegistry>|テキスト バッファーと<xref:Microsoft.VisualStudio.Text.Operations.ITextUndoHistory>オブジェクトの関係を維持します。|

## <a name="other-imports"></a>その他のインポート
 プロバイダー ファクトリとブローカーは、一般に複数のコンポーネントに複数のインスタンスを持つことができるエンティティです。

|[インポート]|提供する|
|------------|--------------|
|<xref:Microsoft.VisualStudio.Text.Adornments.IErrorProviderFactory>|指定<xref:Microsoft.VisualStudio.Text.Tagging.SimpleTagger%601>されたバッファー<xref:Microsoft.VisualStudio.Text.Tagging.ErrorTag>の型 ) の A。|
|<xref:Microsoft.VisualStudio.Text.Adornments.ITextMarkerProviderFactory>|テキスト マーカー タガー <xref:Microsoft.VisualStudio.Text.Tagging.SimpleTagger%601> (の<xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>種類)|
|<xref:Microsoft.VisualStudio.Text.Adornments.IToolTipProviderFactory>|特定<xref:Microsoft.VisualStudio.Text.Adornments.IToolTipProvider><xref:Microsoft.VisualStudio.Text.Editor.ITextView>の .|
|<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionBroker>|<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSession>。|
|<xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoBroker>|<xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSession>。|
|<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpBroker>|<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSession>。|

## <a name="see-also"></a>関連項目
- [言語サービスとエディターの拡張ポイント](../extensibility/language-service-and-editor-extension-points.md)
