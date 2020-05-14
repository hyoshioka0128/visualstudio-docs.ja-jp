---
title: エディターの内部
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - architecture
ms.assetid: 822cbb8d-7ab4-40ee-bd12-44016ebcce81
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bba0b5192df53b6ec837b0030c7b236bf8e08dea
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710324"
---
# <a name="inside-the-editor"></a>エディタ内

エディターは、エディターのテキスト モデルをテキスト ビューとユーザー インターフェイスから分離するように設計された複数のサブシステムで構成されています。

以下のセクションでは、エディタのさまざまな側面について説明します。

- [サブシステムの概要](../extensibility/inside-the-editor.md#overview-of-the-subsystems)

- [テキスト モデル](../extensibility/inside-the-editor.md#the-text-model)

- [テキスト ビュー](../extensibility/inside-the-editor.md#the-text-view)

以下のセクションでは、エディタの機能について説明します。

- [タグと分類子](../extensibility/inside-the-editor.md#tags-and-classifiers)

- [装飾](../extensibility/inside-the-editor.md#adornments)

- [射影](../extensibility/inside-the-editor.md#projection)

- [アウトライン](../extensibility/inside-the-editor.md#outlining)

- [マウスのバインド](../extensibility/inside-the-editor.md#mouse-bindings)

- [編集操作](../extensibility/inside-the-editor.md#editor-operations)

- [IntelliSense](../extensibility/inside-the-editor.md#intellisense)

## <a name="overview-of-the-subsystems"></a>サブシステムの概要

### <a name="text-model-subsystem"></a>テキスト モデル サブシステム

テキスト モデル サブシステムは、テキストを表し、その操作を有効にします。 テキスト モデル サブシステムには<xref:Microsoft.VisualStudio.Text.ITextBuffer>、エディターによって表示される文字のシーケンスを記述するインターフェイスが含まれています。 このテキストは、さまざまな方法で変更、追跡、および操作できます。 テキスト モデルには、次の側面の型も用意されています。

- テキストをファイルに関連付け、ファイル システムでの読み取りと書き込みを管理するサービス。

- 2 つのオブジェクト シーケンス間の最小の差異を検出する差分サービス。

- 他のバッファー内のテキストのサブセットの観点からバッファー内のテキストを記述するためのシステム。

テキスト モデル サブシステムには、ユーザー インターフェイス (UI) の概念が含まれています。 たとえば、テキストの書式設定やテキスト レイアウトの責任は負いません。

テキスト モデル サブシステムのパブリック型は、.NET Framework 基本クラス ライブラリとマネージ機能拡張フレームワーク (MEF) にのみ依存する *、Microsoft.VisualStudio.Text.Data.dll*および*Microsoft.VisualStudio.CoreUtility.dll*に含まれています。

### <a name="text-view-subsystem"></a>テキスト ビュー サブシステム

テキスト ビュー サブシステムは、テキストの書式設定と表示を行います。 このサブシステムの型は、Windows プレゼンテーション ファンデーション (WPF) に依存するかどうかに応じて、2 つの層に分かれています。 最も重要な型<xref:Microsoft.VisualStudio.Text.Editor.ITextView>は<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextView>、 とで表示されるテキスト行のセットを制御し、また、WPF UI 要素を使用してテキストを装飾するためのキャレット、選択、および機能です。 このサブシステムは、テキスト表示領域の周囲に余白も提供します。 これらの余白は拡張でき、さまざまな種類のコンテンツや視覚効果を含めることができます。 余白の例としては、行番号の表示やスクロール バーなどがあります。

テキスト ビュー サブシステムのパブリックな型は、*次*の内容で格納*されています。* 最初のアセンブリにはプラットフォームに依存しない要素が含まれ、2 つ目のアセンブリには WPF 固有の要素が含まれます。

### <a name="classification-subsystem"></a>分類サブシステム

分類サブシステムは、テキストのフォントプロパティを決定する役割を担います。 分類子は、テキストを「キーワード」や「コメント」などの異なるクラスに分割します。 分類形式マップは、これらのクラスを実際のフォント プロパティ ("Blue Consolas 10 pt" など) に関連付けます。 この情報は、テキストビューがテキストの書式設定やレンダリングを行うときに使用されます。 このトピックで後述するタグ付けでは、データをテキストの範囲に関連付けられます。

分類サブシステムのパブリック型は、Microsoft.VisualStudio.Text.Logic.dll に含まれており、分類の視覚的な側面と対話します。

### <a name="operations-subsystem"></a>操作サブシステム

操作サブシステムは、エディターの動作を定義します。 Visual Studio エディター コマンドと元に戻すシステムの実装を提供します。

## <a name="a-closer-look-at-the-text-model-and-the-text-view"></a>テキスト モデルとテキスト ビューを詳しく見る

### <a name="the-text-model"></a>テキスト モデル

テキスト モデル サブシステムは、テキスト タイプの異なるグループで構成されます。 これには、テキスト バッファー、テキスト スナップショット、およびテキスト範囲が含まれます。

#### <a name="text-buffers-and-text-snapshots"></a>テキスト バッファーとテキスト スナップショット

インターフェイス<xref:Microsoft.VisualStudio.Text.ITextBuffer>は、.NET Framework の型で使用されるエンコーディングである UTF-16 を使用してエンコードされる`String`Unicode 文字のシーケンスを表します。 テキスト バッファーはファイル システム ドキュメントとして永続化できますが、これは必須ではありません。

<xref:Microsoft.VisualStudio.Text.ITextBufferFactoryService>は、空のテキスト バッファー、または文字列または から初期化されるテキスト バッファーを作成するために使用<xref:System.IO.TextReader>されます。 テキスト バッファーは、<xref:Microsoft.VisualStudio.Text.ITextDocument>としてファイル システムに永続化できます。

スレッドがを呼び出<xref:Microsoft.VisualStudio.Text.ITextBuffer.TakeThreadOwnership%2A>してテキスト バッファーの所有権を取得するまで、どのスレッドもテキスト バッファーを編集できます。 その後、そのスレッドだけが編集を実行できます。

テキスト バッファーは、有効期間中に多くのバージョンを通過できます。 バッファーが編集されるたびに新しいバージョンが生成され、変更できないバッファー<xref:Microsoft.VisualStudio.Text.ITextSnapshot>のそのバージョンの内容を表します。 テキスト スナップショットは変更できないため、テキスト バッファーが変更され続けても、制限なしで、任意のスレッドのテキスト スナップショットにアクセスできます。

#### <a name="text-snapshots-and-text-snapshot-lines"></a>テキストスナップショットとテキストスナップショット行

テキスト スナップショットの内容は、文字のシーケンスまたは行のシーケンスとして表示できます。 文字と行は、どちらも 0 から始まるインデックスが付けられます。 空のテキスト スナップショットには、0 文字と 1 行の空行が含まれています。 行は、有効な Unicode 改行文字シーケンス、またはバッファーの先頭または末尾で区切られます。 改行文字はテキスト スナップショットで明示的に表され、テキスト スナップショット内の改行がすべて同じである必要はありません。

> [!NOTE]
> Visual Studio エディターでの改行文字の詳細については、「[エンコードと改行](../ide/encodings-and-line-breaks.md)」を参照してください。

テキスト行は<xref:Microsoft.VisualStudio.Text.ITextSnapshotLine>オブジェクトによって表され、特定の行番号または特定の文字位置のテキスト スナップショットから取得できます。

#### <a name="snapshotpoints-snapshotspans-and-normalizedsnapshotspancollections"></a>スナップショットポイント、スナップショットスパン、正規化されたスナップショットスパンコレクション

A<xref:Microsoft.VisualStudio.Text.SnapshotPoint>は、スナップショット内の文字位置を表します。 位置は、ゼロとスナップショットの長さの間に置かね保証されます。 A<xref:Microsoft.VisualStudio.Text.SnapshotSpan>は、スナップショット内のテキストの範囲を表します。 その終了位置は、ゼロとスナップショットの長さの間に置かれ、保証されます。 は<xref:Microsoft.VisualStudio.Text.NormalizedSnapshotSpanCollection>、同じスナップショットの<xref:Microsoft.VisualStudio.Text.SnapshotSpan>オブジェクトのセットで構成されます。

#### <a name="spans-and-normalizedspancollections"></a>スパンと正規化されたSpanコレクション

A<xref:Microsoft.VisualStudio.Text.Span>は、テキスト スナップショット内のテキスト範囲に適用できる間隔を表します。 スナップショット位置はゼロから始まるので、範囲はゼロを含む任意の位置から開始できます。 スパン`End`のプロパティは、その`Start`プロパティとそのプロパティの合計と`Length`同じです。 プロパティ`Span`によって`End`インデックス付けされた文字は含まれません。 たとえば、開始 = 5 と Length = 3 のスパンには End = 8 があり、5、6、および 7 の位置の文字が含まれます。 このスパンの表記は [5..8] です。

2 つのスパンは、終了位置を含む共通の位置がある場合に交差します。 したがって、[3,5)と[2,7]の交点は[3,5]であり、[3,5]と[5]と[7]の交点は[5,5]である。 ([5, 5] は空のスパンであることに注意してください。

2 つの範囲は、終了位置を除いて、共通の位置がある場合に重なります。 空のスパンは他の範囲と重複することはありません。

A<xref:Microsoft.VisualStudio.Text.NormalizedSpanCollection>は、範囲の Start プロパティの順序での範囲のリストです。 リストでは、重なり合う範囲または隣接する範囲がマージされます。 たとえば、スパン [5.9]、[0.1]、[3..6]、[9.10] のセットを指定すると、範囲の正規化されたリストは [0..1] [3..10] です。

#### <a name="itextedit-textversion-and-text-change-notifications"></a>ITextEdit、テキストバージョン、およびテキスト変更通知

テキスト バッファーの内容は、オブジェクトを<xref:Microsoft.VisualStudio.Text.ITextEdit>使用して変更できます。 このようなオブジェクトを作成する (`CreateEdit()`<xref:Microsoft.VisualStudio.Text.ITextBuffer>のメソッドのいずれかを使用して) テキスト編集で構成されるテキスト トランザクションを開始します。 すべての編集は、文字列によってバッファー内のテキストのいくつかのスパンの置き換えです。 各編集の座標と内容は、トランザクションの開始時のバッファのスナップショットを基準にして表されます。 オブジェクト<xref:Microsoft.VisualStudio.Text.ITextEdit>は、同じトランザクション内の他の編集によって影響を受ける編集の座標を調整します。

たとえば、次の文字列を含むテキスト バッファーがあるとします。

```
abcdefghij
```

2 つの編集を含むトランザクションを適用し、1 つは文字を使用して [2.4] の`X`範囲を置き換える編集と、文字`Y`を使用して [6.9] のスパンを置き換える 2 番目の編集を適用します。 結果は、このバッファです。

```
abXefYj
```

2 番目の編集の座標は、最初の編集が適用される前に、トランザクションの開始時にバッファーの内容に関して計算されました。

バッファーへの変更は、<xref:Microsoft.VisualStudio.Text.ITextEdit>`Apply()`オブジェクトがメソッドを呼び出してコミットされたときに有効になります。 空でない編集が少なくとも 1 つあった場合は<xref:Microsoft.VisualStudio.Text.ITextVersion>、新しい編集が<xref:Microsoft.VisualStudio.Text.ITextSnapshot>作成され、新しい`Changed`イベントが作成され、1 つのイベントが発生します。 すべてのテキストバージョンには異なるテキストスナップショットがあります。 テキスト スナップショットは、編集トランザクションの後のテキスト バッファーの完全な状態を表しますが、テキスト バージョンでは、あるスナップショットから次のスナップショットへの変更のみを記述します。 一般に、テキストスナップショットは一度使用した後に破棄されるものであり、テキストバージョンはしばらくの間有効でなければなりません。

テキスト バージョンには. <xref:Microsoft.VisualStudio.Text.INormalizedTextChangeCollection> このコレクションでは、スナップショットに適用された場合に後続のスナップショットを生成する変更について説明します。 コレクション<xref:Microsoft.VisualStudio.Text.ITextChange>内の各オブジェクトには、変更の文字位置、置換された文字列、および置換文字列が含まれます。 基本的な挿入では置換された文字列は空で、基本的な削除の場合は置換文字列が空です。 正規化されたコレクションは、常`null`にテキスト バッファーの最新バージョンに対して使用されます。

テキスト<xref:Microsoft.VisualStudio.Text.ITextEdit>バッファーに対してインスタンス化できるオブジェクトは常に 1 つだけで、すべてのテキスト編集は、テキスト バッファーを所有するスレッドで実行する必要があります (所有権が要求されている場合)。 テキスト編集は、そのメソッドまたはその`Cancel``Dispose`メソッドを呼び出すことによって破棄できます。

<xref:Microsoft.VisualStudio.Text.ITextBuffer>また、`Insert()`インターフェイス`Delete()`に表示`Replace()`されるメソッドに似た 、 <xref:Microsoft.VisualStudio.Text.ITextEdit> 、および メソッドも提供します。 これらを呼び出すことは、オブジェクトを作成<xref:Microsoft.VisualStudio.Text.ITextEdit>し、同様の呼び出しを行い、編集を適用するのと同じ効果があります。

#### <a name="tracking-points-and-tracking-spans"></a>追跡ポイントと追跡範囲

テキスト<xref:Microsoft.VisualStudio.Text.ITrackingPoint>バッファー内の文字位置を表します。 バッファーが文字の位置をずれる方法で編集された場合、トラッキング ポイントは、その文字と共にシフトします。 たとえば、トラッキング ポイントがバッファー内の位置 10 を参照し、バッファーの先頭に 5 文字が挿入された場合、追跡ポイントは 15 桁を参照します。 トラッキング ポイントで示される正確な位置で挿入が行われる場合、その動作は<xref:Microsoft.VisualStudio.Text.PointTrackingMode>、`Positive`または`Negative`によって決まります。 トラッキング モードが正の場合、トラッキング ポイントは同じ文字を参照し、現在は挿入の最後に表示されます。 トラッキング モードが負の場合、トラッキング ポイントは、元の位置に最初に挿入された文字を参照します。 トラッキング ポイントで表される位置にある文字が削除されると、追跡ポイントは削除された範囲の後の最初の文字に移動します。 たとえば、トラッキング ポイントが 5 桁目の文字を参照し、3 ~ 6 桁目の文字が削除された場合、トラッキング ポイントは位置 3 の文字を参照します。

1<xref:Microsoft.VisualStudio.Text.ITrackingSpan>つの位置ではなく、文字の範囲を表します。 その動作は、 によって<xref:Microsoft.VisualStudio.Text.SpanTrackingMode>決定されます。 スパン トラッキング モードが[SpanTrackingMode.EdgeInclusive](xref:Microsoft.VisualStudio.Text.SpanTrackingMode.EdgeInclusive)の場合、追跡範囲は、エッジに挿入されたテキストを組み込むまで拡大します。 スパン トラッキング モードが[SpanTrackingMode.EdgeExclusive](xref:Microsoft.VisualStudio.Text.SpanTrackingMode.EdgeExclusive)の場合、追跡範囲には、その端に挿入されたテキストは組み込まれません。 ただし、スパン トラッキング モードが[SpanTrackingMode.EdgePositive](xref:Microsoft.VisualStudio.Text.SpanTrackingMode.EdgePositive)の場合、挿入は現在の位置を開始方向にプッシュし、スパン トラッキング モードが[SpanTrackingMode.EdgeNegative の](xref:Microsoft.VisualStudio.Text.SpanTrackingMode.EdgeNegative)場合は、現在の位置が末尾に向かってプッシュされます。

追跡ポイントの位置、または追跡対象のテキスト バッファーのスナップショットの追跡範囲の範囲を取得できます。 追跡ポイントと追跡範囲は、どのスレッドからでも安全に参照できます。

#### <a name="content-types"></a>コンテンツの種類

コンテンツ タイプは、さまざまな種類のコンテンツを定義するためのメカニズムです。 コンテンツ タイプは、"text"、"code"、"binary" などのファイルの種類、または "xml" や "vb" 、"c#" などのテクノロジの種類です。 たとえば、"using" という単語は C# と Visual Basic の両方のキーワードですが、他のプログラミング言語ではキーワードではありません。 したがって、このキーワードの定義は、"c#" および "vb" コンテンツ タイプに限定されます。

コンテンツ タイプは、エディターの表示要素やその他の要素のフィルターとして使用されます。 多くのエディター機能と拡張ポイントは、コンテンツ タイプごとに定義されます。 たとえば、テキストの色付けは、プレーン テキスト ファイル、XML ファイル、および Visual Basic のソース コード ファイルで異なります。 テキスト バッファーは、通常、コンテンツ タイプを作成するときに割り当てられ、テキスト バッファーのコンテンツ タイプを変更できます。

コンテンツ タイプは、他のコンテンツ タイプから複数継承できます。 では<xref:Microsoft.VisualStudio.Utilities.ContentTypeDefinition>、特定のコンテンツ タイプの親として複数の基本型を指定できます。

開発者は、独自のコンテンツ タイプを定義し、<xref:Microsoft.VisualStudio.Utilities.IContentTypeRegistryService>を使用して登録できます。 エディターの多くの機能は、<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>を使用して特定のコンテンツ タイプに対して定義できます。 たとえば、エディターの余白、表示要素、およびマウス ハンドラーは、特定のコンテンツタイプを表示するエディターにのみ適用されるように定義できます。

### <a name="the-text-view"></a>テキスト ビュー

モデル ビュー コント ローラー (MVC) パターンのビュー部分は、テキスト ビュー、ビューの書式設定、スクロール バーなどのグラフィック要素、キャレットを定義します。 Visual Studio エディターのすべてのプレゼンテーション要素は、WPF に基づいています。

#### <a name="text-views"></a>テキストビュー

インターフェイス<xref:Microsoft.VisualStudio.Text.Editor.ITextView>は、プラットフォームに依存しないテキスト ビューの表現です。 これは主に、テキスト ドキュメントをウィンドウに表示するために使用されますが、ツールヒントなどの他の目的にも使用できます。

テキスト ビューは、さまざまな種類のテキスト バッファーを参照します。 この<xref:Microsoft.VisualStudio.Text.Editor.ITextView.TextViewModel%2A>プロパティは、データ<xref:Microsoft.VisualStudio.Text.Editor.ITextViewModel>バッファー (データ レベルの最上位バッファー) 、編集が行われる編集バッファー、およびテキスト ビューに表示されるバッファーであるビジュアル バッファーの 3 つの異なるテキスト バッファーを指すオブジェクトを参照します。

テキストは、基になるテキスト バッファーに関連付けられている分類子に基づいて書式設定され、テキスト ビュー自体にアタッチされている表示要素プロバイダーを使用して装飾されます。

#### <a name="the-text-view-coordinate-system"></a>テキスト ビューの座標系

テキスト ビューの座標系は、テキスト ビュー内の位置を指定します。 この座標系では、x 値 0.0 は表示されるテキストの左端に対応し、y 値 0.0 は表示されるテキストの上端に対応します。 x 座標は左から右に増加し、y 座標は上から下に増加します。

ビューポート (テキスト ウィンドウに表示されるテキスト部分) は、垂直方向にスクロールするのと同じ方法で水平方向にスクロールすることはできません。 ビューポートは、描画サーフェスに対して移動するように左の座標を変更することによって水平にスクロールされます。 ただし、ビューポートは、レンダリングされたテキストを変更することによってのみ垂直方向にスクロールでき、イベントが<xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged>発生します。

座標系の距離は、論理ピクセルに対応します。 テキスト レンダリング サーフェスがスケーリング変換なしで表示される場合、テキスト レンダリング座標系の 1 単位はディスプレイ上の 1 ピクセルに対応します。

#### <a name="margins"></a>余白

インターフェイス<xref:Microsoft.VisualStudio.Text.Editor.ITextViewMargin>は余白を表し、余白とそのサイズの可視性を制御できるようにします。 定義済みの 4 つの余白があり、"上"、"左"、"右"、および "下" という名前で、ビューの上端、下端、左端、または右端に関連付けられています。 これらの余白は、他の余白を配置できるコンテナーです。 インターフェイスは、余白のサイズと余白の可視性を返すメソッドを定義します。 余白は、その余白が添付されているテキスト ビューに関する追加情報を提供するビジュアル要素です。 たとえば、行番号の余白には、テキスト ビューの行番号が表示されます。 グリフの余白には UI 要素が表示されます。

インターフェイス<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewMarginProvider>は、余白の作成と配置を処理します。 余白は、他の余白に対して並べ替えることができます。 優先度の高い余白は、テキスト ビューの近くに配置されます。 たとえば、2 つの左余白、余白 A と余白 B があり、余白 B の優先順位が余白 A よりも低い場合、余白 B は余白 A の左側に表示されます。

#### <a name="the-text-view-host"></a>テキスト ビュー ホスト

<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewHost>インターフェイスには、テキスト ビューとビューに付随する隣接する装飾 (スクロール バーなど) が含まれています。 テキスト ビュー ホストには、ビューの境界線に関連付けられた余白も含まれます。

#### <a name="formatted-text"></a>書式付きテキスト

テキスト ビューに表示されるテキストは、<xref:Microsoft.VisualStudio.Text.Formatting.ITextViewLine>オブジェクトで構成されます。 テキスト ビューの各行は、テキスト ビュー内の 1 行のテキストに対応します。 基になるテキスト バッファーの長い行は、部分的に隠れている (ワード ラップが有効でない場合) か、複数のテキスト ビュー行に分割できます。 インターフェイス<xref:Microsoft.VisualStudio.Text.Formatting.ITextViewLine>には、座標と文字の間のマッピング、および線に関連付けられている表示要素のメソッドとプロパティが含まれています。

<xref:Microsoft.VisualStudio.Text.Formatting.ITextViewLine>オブジェクトはインターフェイスを<xref:Microsoft.VisualStudio.Text.Formatting.IFormattedLineSource>使用して作成されます。 現在ビューに表示されているテキストが心配な場合は、書式指定元を無視できます。 ビューに表示されないテキストの書式 (たとえば、リッチ テキストの切り取りと貼り付けのサポート) に関心がある場合は<xref:Microsoft.VisualStudio.Text.Formatting.IFormattedLineSource>、テキスト バッファー内のテキストの書式を設定できます。

テキスト ビューの書式<xref:Microsoft.VisualStudio.Text.ITextSnapshotLine>は 1 つずつです。

## <a name="editor-features"></a>エディターの機能

エディタの機能は、機能の定義が実装から分離するように設計されています。 エディターには、次の機能が含まれています。

- タグと分類子

- 装飾

- 射影

- アウトライン

- マウスとキーのバインド

- 操作とプリミティブ

- IntelliSense

### <a name="tags-and-classifiers"></a>タグと分類子

タグは、テキストのスパンに関連付けられたマーカーです。 テキストの色、下線、グラフィック、ポップアップなどを使用して、さまざまな方法で表示できます。 分類子は、タグの一種です。

その他の種類の<xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>タグは、テキストの<xref:Microsoft.VisualStudio.Text.Tagging.OutliningRegionTag>強調表示、アウトライン、コンパイル<xref:Microsoft.VisualStudio.Text.Tagging.ErrorTag>エラー用です。

#### <a name="classification-types"></a>分類タイプ

インターフェイス<xref:Microsoft.VisualStudio.Text.Classification.IClassificationType>は、テキストの抽象カテゴリである等価クラスを表します。 分類タイプは、他の分類タイプから複数継承できます。 たとえば、プログラミング言語の分類には、"キーワード"、"comment"、"identifier" が含まれ、すべて "code" から継承されます。 自然言語分類タイプには、「名詞」、「動詞」、「形容詞」が含まれ、すべて「自然言語」を継承します。

#### <a name="classifications"></a>分類

分類は、特定の分類タイプのインスタンスであり、通常はテキストの範囲にわたって使用されます。 A<xref:Microsoft.VisualStudio.Text.Classification.ClassificationSpan>は分類を表すために使用されます。 分類スパンは、特定のテキスト範囲をカバーし、このテキスト範囲が特定の分類タイプであることをシステムに伝えるラベルと考えることができます。

#### <a name="classifiers"></a>クラシファイア

A<xref:Microsoft.VisualStudio.Text.Classification.IClassifier>は、テキストを分類のセットに分割するメカニズムです。 分類子は、特定のコンテンツ タイプに対して定義し、特定のテキスト バッファーに対してインスタンス化する必要があります。 クライアントは、<xref:Microsoft.VisualStudio.Text.Classification.IClassifier>テキスト分類に参加するために実装する必要があります。

#### <a name="classifier-aggregators"></a>分類子アグリゲーター

分類子アグリゲーターは、1 つのテキスト バッファーのすべての分類子を 1 組の分類セットに結合するメカニズムです。 たとえば、C# 分類子と英語の分類子の両方が、C# ファイル内のコメントに対する分類を作成できます。 次のコメントを考えてみましょう。

```
// This method produces a classifier
```

C# 分類子は、全体の範囲にコメントのラベルを付け、英語の分類子は"生成" を "動詞" と "メソッド" を "名詞" として分類する場合があります。 アグリゲーターは重複しない分類のセットを生成し、セットのタイプはすべての貢献に基づいています。

分類子アグリゲーターは、テキストを分類のセットに分割するため、分類子でもあります。 分類子アグリゲーターは、重複する分類が存在すること、および分類がソートされるようにもします。 個々の分類子は、任意の順序で任意の分類のセットを返し、どのような方法で重複することができます。

#### <a name="classification-formatting-and-text-coloring"></a>分類の書式設定とテキストの色分け

テキストの書式設定は、テキスト分類に基づいて構築された機能の例です。 これは、アプリケーション内のテキストの表示を決定するために、テキストビューレイヤーによって使用されます。 テキストの書式設定領域は WPF によって異なりますが、分類の論理定義は異なります。

分類形式は、特定の分類タイプの書式プロパティのセットです。 これらの形式は、分類タイプの親の形式から継承されます。

A<xref:Microsoft.VisualStudio.Text.Classification.IClassificationFormatMap>は、分類タイプからテキストフォーマットプロパティのセットへのマップです。 エディターでのフォーマット マップの実装は、分類形式のすべてのエクスポートを処理します。

### <a name="adornments"></a>装飾

表示要素は、テキスト ビューの文字のフォントや色に直接関係しないグラフィック効果です。 たとえば、多くのプログラミング言語で非コンパイル コードをマークするために使用される赤い波線の下線は埋め込み表示要素であり、ツールヒントはポップアップ表示要素です。 表示要素は から派生<xref:System.Windows.UIElement>し、実装<xref:Microsoft.VisualStudio.Text.Tagging.ITag>されます。 ビュー内のテキストと同じスペースを占める表示<xref:Microsoft.VisualStudio.Text.Tagging.SpaceNegotiatingAdornmentTag>要素の場合は、特殊な 2 種類の表示要素タグと、波線の下<xref:Microsoft.VisualStudio.Text.Tagging.ErrorTag>線の場合は、 があります。

埋め込み表示要素は、書式設定されたテキスト ビューの一部を形成するグラフィックスです。 これらは異なる Z オーダー レイヤーで構成されています。 テキスト、キャレット、および選択範囲の 3 つの組み込みレイヤーがあります。 ただし、開発者は、より多くのレイヤーを定義し、互いに対して順番に配置できます。 埋め込まれた表示要素の 3 種類は、テキスト相対表示要素 (テキストが移動すると移動され、テキストが削除されると削除されます)、ビュー相対表示要素 (ビューのテキスト以外の部分に関係があります)、所有者制御の表示要素 (開発者は配置を管理する必要があります) です。

ポップアップ表示要素は、テキスト ビューの上の小さなウィンドウ (ヒントなど) に表示されるグラフィックスです。

### <a name="projection"></a><a name="projection"></a>投影

射影は、テキストを実際に格納するのではなく、他のテキスト バッファーのテキストを組み合わせた別の種類のテキスト バッファーを構築するための手法です。 たとえば、投影バッファーを使用して、他の 2 つのバッファーからテキストを連結し、1 つのバッファー内にあるかのように結果を表示したり、テキストの一部を 1 つのバッファーに隠したりできます。 投影バッファーは、別の投影バッファーへのソース バッファーとして機能できます。 投影法によって関連付けられたバッファーのセットは、さまざまな方法でテキストを再配置するために構築できます。 (このようなセットは *、バッファグラフ*とも呼ばれます。Visual Studio のテキスト のアウトライン機能は、折りたたまれたテキストを非表示にする投影バッファーを使用して実装され、ASP.NETページの Visual Studio エディターでは、Visual Basic や C# などの埋め込み言語をサポートするプロジェクションを使用します。

を<xref:Microsoft.VisualStudio.Text.Projection.IProjectionBuffer>使用<xref:Microsoft.VisualStudio.Text.Projection.IProjectionBufferFactoryService>して 作成します。 投影バッファーは、*ソース範囲*と呼ばれる<xref:Microsoft.VisualStudio.Text.ITrackingSpan>オブジェクトの順序付けられたシーケンスで表されます。 これらの範囲の内容は、文字のシーケンスとして表示されます。 ソース範囲の描画元となるテキストバッファーは、ソースバッファー という名前*です*。 投影バッファーのクライアントは、通常のテキスト バッファーとは異なることを認識する必要はありません。

投影バッファーは、ソース バッファー上のテキスト変更イベントをリッスンします。 ソース範囲内のテキストが変更されると、投影バッファーは変更されたテキスト座標を独自の座標にマップし、適切なテキスト変更イベントを発生させます。 たとえば、次の内容を持つソース バッファー A と B を考えてみます。

```
A: ABCDE
B: vwxyz
```

投影バッファー P が 2 つのテキスト範囲から形成され、1 つはバッファー A を持ち、もう 1 つはバッファー B がすべてある場合、P は次の内容になります。

```
P: ABCDEvwxyz
```

サブストリング`xy`がバッファー B から削除されると、バッファー P は、位置 7 と 8 の文字が削除されたことを示すイベントを発生させます。

投影バッファーは直接編集することもできます。 編集内容を適切なソース バッファーに反映します。 たとえば、文字列が 6 位置 (文字 "v" の元の位置) のバッファー P に挿入された場合、挿入は 1 のバッファー B に伝搬されます。

投影バッファーに影響するソース範囲には制限があります。 ソース範囲は重複しない可能性があります。投影バッファー内の場所は、任意のソース バッファー内の複数の場所にマップすることはできませんし、ソース バッファー内の場所は、投影バッファー内の複数の場所にマップできません。 ソース バッファーリレーションシップでは循環は許可されません。

イベントは、投影バッファーのソース バッファーのセットが変更されたとき、およびソースのセットが変化したときに発生します。
エリシオン バッファーは、特殊な種類の投影バッファーです。 これは主に、アウトラインを作成し、テキストブロックを展開および折りたたむ操作に使用します。 エリシオン バッファーは 1 つのソース バッファーに基づいており、elision バッファー内の範囲は、ソース バッファーで順序付けされるのと同じ順序にする必要があります。

#### <a name="the-buffer-graph"></a>バッファグラフ

この<xref:Microsoft.VisualStudio.Text.Projection.IBufferGraph>インターフェイスは、投影バッファーのグラフをマッピングできるようにします。 言語コンパイラによって生成される抽象構文ツリーと同様に、すべてのテキスト バッファーと投影バッファーは、有向非巡回グラフで収集されます。 グラフは、任意のテキスト バッファーを使用できる最上位バッファーによって定義されます。 バッファー グラフは、最上位バッファー内のポイントからソース バッファー内のポイント、または最上位バッファー内のスパンからソース バッファー内の一連の範囲にマップできます。 同様に、ソース バッファーから最上位のバッファー内のポイントにポイントまたはスパンをマップできます。 バッファー グラフは、 を使用<xref:Microsoft.VisualStudio.Text.Projection.IBufferGraphFactoryService>して作成します。

#### <a name="events-and-projection-buffers"></a>イベントと投影バッファー

投影バッファーが変更されると、変更は投影バッファーからそれに依存するバッファーに送信されます。 すべてのバッファーが変更された後、バッファー変更イベントが最も深いバッファーから始めて発生します。

### <a name="outlining"></a>アウトライン

アウトライン表示は、テキスト ビュー内のテキストブロックを展開または折りたたむ機能です。 アウトラインは、表示要素が定義される<xref:Microsoft.VisualStudio.Text.Tagging.ITag>のと同じ方法で、 の一種として定義されます。 A<xref:Microsoft.VisualStudio.Text.Tagging.OutliningRegionTag>は、展開または折りたたむことができるテキスト領域を定義するタグです。 アウトラインを使用するには、 を<xref:Microsoft.VisualStudio.Text.Outlining.IOutliningManagerService>インポートして<xref:Microsoft.VisualStudio.Text.Outlining.IOutliningManager>を取得する必要があります。 アウトライン マネージャは、オブジェクトとして<xref:Microsoft.VisualStudio.Text.Outlining.ICollapsible>表されるさまざまなブロックを列挙、折りたたみ、展開し、それに応じてイベントを発生させます。

### <a name="mouse-bindings"></a>マウスのバインド

マウスバインディングは、マウスの動きを別のコマンドにリンクします。 マウス のバインドは<xref:Microsoft.VisualStudio.Text.Editor.IMouseProcessorProvider>を使用して定義し、キー バインドは を<xref:Microsoft.VisualStudio.Text.Editor.IKeyProcessorProvider>使用して定義します。 は<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewHost>、すべてのバインディングを自動的にインスタンス化し、ビュー内のマウス イベントに接続します。

この<xref:Microsoft.VisualStudio.Text.Editor.IMouseProcessor>インターフェイスには、さまざまなマウス イベントの前処理イベント ハンドラーとポスト プロセス イベント ハンドラーが含まれています。 イベントの 1 つを処理するには、 の<xref:Microsoft.VisualStudio.Text.Editor.MouseProcessorBase>メソッドの一部をオーバーライドします。

### <a name="editor-operations"></a>編集操作

エディター操作を使用すると、スクリプトやその他の目的で、エディターとの対話を自動化できます。 をインポートして、<xref:Microsoft.VisualStudio.Text.Operations.IEditorOperationsFactoryService>特定<xref:Microsoft.VisualStudio.Text.Editor.ITextView>の . これらのオブジェクトを使用して、選択内容の変更、ビューのスクロール、ビューの別の部分へのキャレットの移動を行うことができます。

### <a name="intellisense"></a>IntelliSense

IntelliSense では、ステートメント入力候補、シグネチャ ヘルプ (パラメーター情報とも呼ばれます)、クイック ヒント、電球をサポートしています。

ステートメント入力候補は、メソッド名、XML 要素、およびその他のコーディング要素またはマークアップ要素に対して、候補の候補のポップアップ リストを提供します。 一般に、ユーザー ジェスチャは完了セッションを呼び出します。 セッションには、候補の候補の一覧が表示され、ユーザーは 1 つを選択するか、リストを閉じることができます。 は<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionBroker>、 の作成とトリガを<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSession>担当します。 セッション<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource>の完了項目<xref:Microsoft.VisualStudio.Language.Intellisense.CompletionSet>のを計算します。

## <a name="see-also"></a>関連項目

- [言語サービスとエディターの拡張ポイント](../extensibility/language-service-and-editor-extension-points.md)
- [エディターのインポート](../extensibility/editor-imports.md)
