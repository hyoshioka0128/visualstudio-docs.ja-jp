---
title: エディターのインポート |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80712009"
---
# <a name="editor-imports"></a>エディターのインポート
拡張機能を提供するさまざまなエディターサービス、ファクトリ、ブローカーを、コアエディターへのさまざまな種類のアクセスでインポートできます。 たとえば、をインポートして、 <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigator> 特定のコンテンツタイプのを提供できます。 (このナビゲーターを使用すると、テキストバッファーに対してさまざまな種類の検索を実行できます)。

 エディターインポートを使用するには、Managed Extensibility Framework コンポーネントパーツをエクスポートするクラスのフィールドまたはプロパティとしてインポートします。

> [!NOTE]
> Managed Extensibility Framework の詳細については、「 [Managed Extensibility Framework (MEF)](/dotnet/framework/mef/index)」を参照してください。

## <a name="import-syntax"></a>インポート構文
 次の例は、エディターオプションのファクトリサービスをインポートする方法を示しています。

```
[Import]
internal IEditorOptionsFactoryService EditorOptions { get; set; }
```

 サービスをプロパティではなくフィールドとしてインポートする場合は、 `null` 変数に割り当てられていないことに関するコンパイラの警告が表示されないように、宣言でをに設定する必要があります。

```
[Import]
internal IEditorOptionsFactoryService m_editorOptions = null;
```

 インポートの使用例については、次のチュートリアルを参照してください。

- [チュートリアル: 余白のグリフの作成](../extensibility/walkthrough-creating-a-margin-glyph.md)

- [チュートリアル: テキストビューのカスタマイズ](../extensibility/walkthrough-customizing-the-text-view.md)

- [チュートリアル: テキストの強調表示](../extensibility/walkthrough-highlighting-text.md)

- [チュートリアル: QuickInfo ツールヒントの表示](../extensibility/walkthrough-displaying-quickinfo-tooltips.md)

- [チュートリアル: 署名のヘルプを表示する](../extensibility/walkthrough-displaying-signature-help.md)

- [チュートリアル: 入力候補の表示](../extensibility/walkthrough-displaying-statement-completion.md)

- [チュートリアル: 電球の提案を表示する](../extensibility/walkthrough-displaying-light-bulb-suggestions.md)

## <a name="import-the-service-provider"></a>サービスプロバイダーのインポート
 また、 <xref:Microsoft.VisualStudio.Shell.SVsServiceProvider> 同じ方法で (アセンブリ VisualStudio にある) をインポートして、Visual Studio サービスへのアクセスを取得することもできます。

```csharp
[Import]
internal SVsServiceProvider ServiceProvider = null;
```

 詳細については、「 [チュートリアル: エディター拡張機能から DTE オブジェクトにアクセス](../extensibility/walkthrough-accessing-the-dte-object-from-an-editor-extension.md) する」を参照してください。

## <a name="services"></a>サービス
 通常、エディターサービスは1つのエンティティであり、サービスを提供し、複数のコンポーネント間で共有されます。

|[インポート]|ここ|
|------------|--------------|
|<xref:Microsoft.VisualStudio.Utilities.IFileExtensionRegistryService>|ファイル拡張子とオブジェクトの間のリレーションシップ <xref:Microsoft.VisualStudio.Utilities.IContentType> 。|
|<xref:Microsoft.VisualStudio.Utilities.IContentTypeRegistryService>|<xref:Microsoft.VisualStudio.Utilities.IContentType> オブジェクトのコレクション。|
|<xref:Microsoft.VisualStudio.Editor.IVsFontsAndColorsInformationService>|<xref:Microsoft.VisualStudio.Editor.IVsFontsAndColorsInformation> 表す.|
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService>|エディターアダプターの多くのオブジェクト:<br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>|
|<xref:Microsoft.VisualStudio.Text.IncrementalSearch.IIncrementalSearchFactoryService>|<xref:Microsoft.VisualStudio.Text.IncrementalSearch.IIncrementalSearch>指定されたテキストビューのオブジェクト。|
|<xref:Microsoft.VisualStudio.Text.ITextBufferFactoryService>|<xref:Microsoft.VisualStudio.Text.ITextBuffer>。|
|<xref:Microsoft.VisualStudio.Text.ITextDocumentFactoryService>|<xref:Microsoft.VisualStudio.Text.ITextDocument>。|
|<xref:Microsoft.VisualStudio.Text.Differencing.IDifferenceService>|<xref:Microsoft.VisualStudio.Text.Differencing.IDifferenceCollection%601>相違点のです。|
|<xref:Microsoft.VisualStudio.Text.Differencing.IHierarchicalStringDifferenceService>|<xref:Microsoft.VisualStudio.Text.Differencing.IHierarchicalDifferenceCollection>相違点のです。|
|<xref:Microsoft.VisualStudio.Text.Projection.IProjectionBufferFactoryService>|<xref:Microsoft.VisualStudio.Text.Projection.IProjectionBuffer>または <xref:Microsoft.VisualStudio.Text.Projection.IElisionBuffer> 。|
|<xref:Microsoft.VisualStudio.Text.Projection.IBufferGraphFactoryService>|<xref:Microsoft.VisualStudio.Text.Projection.IBufferGraph>オブジェクトのセットの <xref:Microsoft.VisualStudio.Text.ITextBuffer> 。|
|<xref:Microsoft.VisualStudio.Text.Classification.IClassifierAggregatorService>|<xref:Microsoft.VisualStudio.Text.Classification.IClassifier>の <xref:Microsoft.VisualStudio.Text.ITextBuffer> 。|
|<xref:Microsoft.VisualStudio.Text.Classification.IViewClassifierAggregatorService>|<xref:Microsoft.VisualStudio.Text.Classification.IClassifier>の <xref:Microsoft.VisualStudio.Text.Editor.ITextView> 。|
|<xref:Microsoft.VisualStudio.Text.Classification.IClassificationFormatMapService>|<xref:Microsoft.VisualStudio.Text.Classification.IClassificationFormatMap>の <xref:Microsoft.VisualStudio.Text.Editor.ITextView> 。|
|<xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMapService>|<xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMap>の <xref:Microsoft.VisualStudio.Text.Editor.ITextView> 。|
|<xref:Microsoft.VisualStudio.Text.Classification.IClassificationTypeRegistryService>|オブジェクトのコレクションを保持 <xref:Microsoft.VisualStudio.Text.Classification.IClassificationType> します。|
|<xref:Microsoft.VisualStudio.Text.Tagging.IBufferTagAggregatorFactoryService>|<xref:Microsoft.VisualStudio.Text.Tagging.ITagAggregator%601>テキストバッファーの。|
|<xref:Microsoft.VisualStudio.Text.Tagging.IViewTagAggregatorFactoryService>|<xref:Microsoft.VisualStudio.Text.Tagging.ITagAggregator%601>テキストビューの。|
|<xref:Microsoft.VisualStudio.Text.Editor.IEditorOptionsFactoryService>|<xref:Microsoft.VisualStudio.Text.Editor.IEditorOptions>指定したスコープの。|
|<xref:Microsoft.VisualStudio.Text.Editor.IScrollMapFactoryService>|<xref:Microsoft.VisualStudio.Text.Editor.IScrollMap>テキストビューの。|
|<xref:Microsoft.VisualStudio.Text.Editor.ISmartIndentationService>|<xref:Microsoft.VisualStudio.Text.Editor.ISmartIndent>の <xref:Microsoft.VisualStudio.Text.Editor.ITextView> 。|
|<xref:Microsoft.VisualStudio.Text.Editor.ISmartIndentationService>|オブジェクトを使用した自動インデントを取得し <xref:Microsoft.VisualStudio.Text.Editor.ISmartIndentProvider> ます。|
|<xref:Microsoft.VisualStudio.Text.Editor.ITextEditorFactoryService>|のを管理 <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewHost> <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextView> します。|
|<xref:Microsoft.VisualStudio.Text.Formatting.IFormattedTextSourceFactoryService>|<xref:Microsoft.VisualStudio.Text.Formatting.IFormattedLineSource>。|
|<xref:Microsoft.VisualStudio.Text.Formatting.IRtfBuilderService>|一連のスナップショットから RTF 形式のテキストを生成します。|
|<xref:Microsoft.VisualStudio.Text.Formatting.ITextAndAdornmentSequencerFactoryService>|<xref:Microsoft.VisualStudio.Text.Formatting.ITextAndAdornmentSequencer>の <xref:Microsoft.VisualStudio.Text.Editor.ITextView> 。|
|<xref:Microsoft.VisualStudio.Text.Formatting.ITextParagraphPropertiesFactoryService>|<xref:System.Windows.Media.TextFormatting.TextParagraphProperties>ビュー内のテキスト行を書式設定するための。|
|<xref:Microsoft.VisualStudio.Text.Operations.IEditorOperationsFactoryService>|<xref:Microsoft.VisualStudio.Text.Operations.IEditorOperations>のオブジェクト <xref:Microsoft.VisualStudio.Text.Editor.ITextView> 。|
|<xref:Microsoft.VisualStudio.Text.Operations.ITextSearchService>|テキストスナップショットを検索します。|
|<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>|に <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigator> よるの <xref:Microsoft.VisualStudio.Text.ITextBuffer> <xref:Microsoft.VisualStudio.Utilities.IContentType> 。|
|<xref:Microsoft.VisualStudio.Text.Outlining.IOutliningManagerService>|<xref:Microsoft.VisualStudio.Text.Outlining.IOutliningManager>テキストビューの。|
|<xref:Microsoft.VisualStudio.Language.Intellisense.IGlyphService>|グリフの標準セット。|
|<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseSessionStackMapService>|<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseSessionStack>の <xref:Microsoft.VisualStudio.Text.Editor.ITextView> 。|
|<xref:Microsoft.VisualStudio.Language.Intellisense.IWpfKeyboardTrackingService>|キーボード処理を追跡します。|
|<xref:Microsoft.VisualStudio.Language.StandardClassification.IStandardClassificationService>|標準 <xref:Microsoft.VisualStudio.Text.Classification.IClassificationType> オブジェクト。|
|<xref:Microsoft.VisualStudio.Text.Operations.ITextUndoHistoryRegistry>|テキストバッファーとオブジェクトの間のリレーションシップを維持し  <xref:Microsoft.VisualStudio.Text.Operations.ITextUndoHistory> ます。|

## <a name="other-imports"></a>その他のインポート
 プロバイダーファクトリとブローカーは、通常、複数のコンポーネントに複数のインスタンスを持つことができるエンティティです。

|[インポート]|ここ|
|------------|--------------|
|<xref:Microsoft.VisualStudio.Text.Adornments.IErrorProviderFactory>|<xref:Microsoft.VisualStudio.Text.Tagging.SimpleTagger%601> <xref:Microsoft.VisualStudio.Text.Tagging.ErrorTag> 指定されたバッファーの型の。|
|<xref:Microsoft.VisualStudio.Text.Adornments.ITextMarkerProviderFactory>|テキストマーカーのタガー ( <xref:Microsoft.VisualStudio.Text.Tagging.SimpleTagger%601> 型の a <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> )。|
|<xref:Microsoft.VisualStudio.Text.Adornments.IToolTipProviderFactory>|<xref:Microsoft.VisualStudio.Text.Adornments.IToolTipProvider>指定したの <xref:Microsoft.VisualStudio.Text.Editor.ITextView> 。|
|<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionBroker>|<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSession>。|
|<xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoBroker>|<xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSession>。|
|<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpBroker>|<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSession>。|

## <a name="see-also"></a>関連項目
- [言語サービスとエディターの拡張点](../extensibility/language-service-and-editor-extension-points.md)
