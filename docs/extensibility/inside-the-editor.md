---
title: エディターの内部
description: エディターのサブシステムと機能について説明します。 Visual Studio エディターの機能を拡張できます。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 14193c0806c4b45f721ee97b101969de8437448d
ms.sourcegitcommit: 19061b61759ce8e3b083a0e01a858e5435580b3e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/15/2020
ms.locfileid: "97487531"
---
# <a name="inside-the-editor"></a>エディター内

エディターはいくつかの異なるサブシステムで構成されています。これは、テキストビューとユーザーインターフェイスとは別にエディターテキストモデルを保持するように設計されています。

これらのセクションでは、エディターのさまざまな側面について説明します。

- [サブシステムの概要](../extensibility/inside-the-editor.md#overview-of-the-subsystems)

- [テキストモデル](../extensibility/inside-the-editor.md#the-text-model)

- [テキストビュー](../extensibility/inside-the-editor.md#the-text-view)

以下のセクションでは、エディターの機能について説明します。

- [タグと分類子](../extensibility/inside-the-editor.md#tags-and-classifiers)

- [修飾](../extensibility/inside-the-editor.md#adornments)

- [射影](../extensibility/inside-the-editor.md#projection)

- [アウトライン](../extensibility/inside-the-editor.md#outlining)

- [マウスバインド](../extensibility/inside-the-editor.md#mouse-bindings)

- [エディターの操作](../extensibility/inside-the-editor.md#editor-operations)

- [IntelliSense](../extensibility/inside-the-editor.md#intellisense)

## <a name="overview-of-the-subsystems"></a>サブシステムの概要

### <a name="text-model-subsystem"></a>テキストモデルサブシステム

テキストモデルサブシステムは、テキストを表現し、その操作を有効にする役割を担います。 テキストモデルサブシステムには、 <xref:Microsoft.VisualStudio.Text.ITextBuffer> エディターによって表示される文字のシーケンスを記述するインターフェイスが含まれています。 このテキストは、さまざまな方法で変更、追跡、または操作できます。 テキストモデルには、次の側面の型も用意されています。

- テキストをファイルに関連付け、ファイルシステムでの読み取りと書き込みを管理するサービス。

- 2つのオブジェクトのシーケンス間の最小限の違いを検出する差分サービス。

- 他のバッファー内のテキストのサブセットに関してバッファー内のテキストを記述するシステム。

テキストモデルサブシステムは、ユーザーインターフェイス (UI) の概念を自由に利用できます。 たとえば、テキストの書式設定やテキストレイアウトについては責任を負いません。テキストに関連付けられている視覚的な装飾についての情報はありません。

テキストモデルサブシステムのパブリック型は *Microsoft.VisualStudio.Text.Data.dll* と *Microsoft.VisualStudio.CoreUtility.dll* に含まれており、.NET Framework 基本クラスライブラリと Managed Extensibility Framework (MEF) にのみ依存します。

### <a name="text-view-subsystem"></a>テキストビューサブシステム

テキストビューサブシステムは、テキストの書式設定と表示を行います。 このサブシステムの型は、型が Windows Presentation Foundation (WPF) に依存しているかどうかに応じて、2つの層に分割されます。 最も重要な型は <xref:Microsoft.VisualStudio.Text.Editor.ITextView> とです <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextView> 。これは、表示されるテキスト行のセット、および、WPF UI 要素を使用してテキストを装飾するためのカレット、選択、および機能を制御します。 また、このサブシステムでは、テキスト表示領域の周りに余白が表示されます。 これらの余白は拡張でき、さまざまな種類のコンテンツと視覚効果を含めることができます。 余白の例としては、行番号の表示とスクロールバーがあります。

テキストビューサブシステムのパブリック型は、 *Microsoft.VisualStudio.Text.UI.dll* と *Microsoft.VisualStudio.Text.UI.Wpf.dll* に含まれています。 最初のアセンブリには、プラットフォームに依存しない要素が含まれ、2番目のアセンブリには WPF 固有の要素が含まれます。

### <a name="classification-subsystem"></a>分類サブシステム

分類サブシステムでは、テキストのフォントプロパティを決定します。 分類子は、"keyword" や "comment" など、テキストを異なるクラスに分割します。 分類形式マップは、これらのクラスを実際のフォントプロパティ ("Blue Consolas, 10 pt" など) に関連付けます。 この情報は、テキストを書式設定および表示するときにテキストビューによって使用されます。 タグ付けについては、このトピックの後半で詳しく説明します。データをテキストの範囲に関連付けることができます。

分類サブシステムのパブリック型は Microsoft.VisualStudio.Text.Logic.dll に含まれ、Microsoft.VisualStudio.Text.UI.Wpf.dll に含まれる分類の視覚的な側面と対話します。

### <a name="operations-subsystem"></a>オペレーションサブシステム

Operations サブシステムは、エディターの動作を定義します。 これにより、Visual Studio エディターのコマンドと元に戻すシステムの実装が提供されます。

## <a name="a-closer-look-at-the-text-model-and-the-text-view"></a>テキストモデルとテキストビューの詳細

### <a name="the-text-model"></a>テキストモデル

テキストモデルサブシステムは、さまざまなテキスト型のグループで構成されます。 これには、テキストバッファー、テキストスナップショット、テキスト範囲などが含まれます。

#### <a name="text-buffers-and-text-snapshots"></a>テキストバッファーとテキストスナップショット

インターフェイスは、 <xref:Microsoft.VisualStudio.Text.ITextBuffer> utf-16 を使用してエンコードされた Unicode 文字のシーケンスを表します。これは、.NET Framework の型によって使用されるエンコーディングです `String` 。 テキストバッファーはファイルシステムドキュメントとして保存できますが、これは必須ではありません。

は、 <xref:Microsoft.VisualStudio.Text.ITextBufferFactoryService> 空のテキストバッファー、または文字列またはから初期化されたテキストバッファーを作成するために使用され <xref:System.IO.TextReader> ます。 テキストバッファーは、としてファイルシステムに保存でき <xref:Microsoft.VisualStudio.Text.ITextDocument> ます。

スレッドは、を呼び出すことによってテキストバッファーの所有権を取得するまで、テキストバッファーを編集でき <xref:Microsoft.VisualStudio.Text.ITextBuffer.TakeThreadOwnership%2A> ます。 その後、そのスレッドだけが編集を実行できます。

テキストバッファーは、有効期間中に多くのバージョンを経由することができます。 新しいバージョンは、バッファーが編集されるたびに生成され、変更 <xref:Microsoft.VisualStudio.Text.ITextSnapshot> できないはそのバージョンのバッファーの内容を表します。 テキストスナップショットは不変であるため、表示されているテキストバッファーが変化し続ける場合でも、制限なく、任意のスレッドでテキストスナップショットにアクセスできます。

#### <a name="text-snapshots-and-text-snapshot-lines"></a>テキストスナップショットとテキストスナップショット行

テキストスナップショットの内容は、一連の文字として、または一連の行として表示できます。 文字と行はどちらも0から始まるインデックスが作成されます。 空のテキストスナップショットには、ゼロ文字と1つの空の行が含まれます。 行は、有効な Unicode 改行文字シーケンス、またはバッファーの先頭または末尾で区切られます。 改行文字はテキストスナップショットで明示的に表され、テキストスナップショット内の改行はすべて同じである必要はありません。

> [!NOTE]
> Visual Studio エディターの改行文字の詳細については、「 [エンコーディングと改行](../ide/encodings-and-line-breaks.md)」を参照してください。

1行のテキストはオブジェクトによって表されます <xref:Microsoft.VisualStudio.Text.ITextSnapshotLine> 。これは、特定の行番号または特定の文字位置のテキストスナップショットから取得できます。

#### <a name="snapshotpoints-snapshotspans-and-normalizedsnapshotspancollections"></a>SnapshotPoints、Snapshotpoints、NormalizedSnapshotSpanCollections

は、 <xref:Microsoft.VisualStudio.Text.SnapshotPoint> スナップショット内の文字位置を表します。 位置は、0とスナップショットの長さの間であることが保証されます。 は、 <xref:Microsoft.VisualStudio.Text.SnapshotSpan> スナップショット内のテキストの範囲を表します。 最終的な位置は、0とスナップショットの長さの間であることが保証されます。 は、 <xref:Microsoft.VisualStudio.Text.NormalizedSnapshotSpanCollection> 同じスナップショットからの一連のオブジェクトで構成され <xref:Microsoft.VisualStudio.Text.SnapshotSpan> ます。

#### <a name="spans-and-normalizedspancollections"></a>Span と NormalizedSpanCollections

は、 <xref:Microsoft.VisualStudio.Text.Span> テキストスナップショット内のテキストの範囲に適用できる間隔を表します。 スナップショットの位置は0から始まるため、スパンはゼロを含む任意の位置から始めることができます。 `End`Span のプロパティは、そのプロパティとそのプロパティの合計と等しく `Start` `Length` なります。 には、 `Span` プロパティによってインデックス付けされた文字は含まれません `End` 。 たとえば、Start = 5 および Length = 3 のスパンは終了 = 8 で、5、6、および7の位置の文字が含まれます。 このスパンの表記は [5.. 8] です。

両端が共通である場合 (終了位置を含む)、2つの範囲が交差します。 このため、[3, 5) と [2, 7] の積集合は [3, 5)、[3, 5) と [5, 7] の交差部分は [5, 5) です。 ([5, 5) は空のスパンであることに注意してください)。

2つの範囲が重複している場合は、終了位置を除き、2つのスパンが重なっています。 空のスパンは他のスパンと重複しないため、2つの範囲の重なりが空になることはありません。

は、 <xref:Microsoft.VisualStudio.Text.NormalizedSpanCollection> 範囲の開始プロパティの順序での範囲のリストです。 一覧では、重複するスパンまたは隣接するスパンがマージされます。 たとえば、範囲 [5...]、[0 ..1)、[3.. 6]、[9.. 10] のセットがある場合、範囲の正規化された一覧は [0 ..1)、[3.. 10] になります。

#### <a name="itextedit-textversion-and-text-change-notifications"></a>ITextEdit、TextVersion、テキスト変更通知

テキストバッファーの内容は、オブジェクトを使用して変更でき <xref:Microsoft.VisualStudio.Text.ITextEdit> ます。 のメソッドのいずれかを使用してこのようなオブジェクトを作成すると `CreateEdit()` <xref:Microsoft.VisualStudio.Text.ITextBuffer> 、テキスト編集で構成されるテキストトランザクションが開始されます。 すべての編集は、バッファー内のテキストの一部を文字列で置き換えるものです。 各編集の座標と内容は、トランザクションの開始時にバッファーのスナップショットに対して相対的に表されます。 オブジェクトは、 <xref:Microsoft.VisualStudio.Text.ITextEdit> 同じトランザクション内の他の編集によって影響を受ける編集の座標を調整します。

たとえば、次の文字列を含むテキストバッファーを考えてみます。

```
abcdefghij
```

2つの編集を含むトランザクションを適用します。1つは、文字を使用して [2.. 4] のスパンを置き換える編集、もう1つは、文字を使用して `X` [6... 9] のスパンを置き換える2番目の編集です。 `Y` このバッファーは次のようになります。

```
abXefYj
```

2番目の編集の座標は、最初の編集が適用される前に、トランザクションの開始時のバッファーの内容に対して計算されました。

バッファーへの変更は、 <xref:Microsoft.VisualStudio.Text.ITextEdit> オブジェクトがメソッドを呼び出すことによってコミットされると有効になり `Apply()` ます。 空でない編集が少なくとも1つある場合は、新しいが作成され、 <xref:Microsoft.VisualStudio.Text.ITextVersion> 新しい <xref:Microsoft.VisualStudio.Text.ITextSnapshot> が作成されて、1つの `Changed` イベントが発生します。 すべてのテキストバージョンには、異なるテキストスナップショットがあります。 テキストスナップショットは、編集トランザクションの後のテキストバッファーの完全な状態を表しますが、テキストバージョンでは、1つのスナップショットから次のスナップショットへの変更のみが記述されます。 一般に、テキストスナップショットは一度だけ使用してから破棄しますが、テキストのバージョンはしばらくの間は維持される必要があります。

テキストバージョンにはが含まれてい <xref:Microsoft.VisualStudio.Text.INormalizedTextChangeCollection> ます。 このコレクションでは、スナップショットに適用されると、後続のスナップショットが生成される変更について説明します。 コレクション内のすべてのには、 <xref:Microsoft.VisualStudio.Text.ITextChange> 変更の文字位置、置換された文字列、および置換文字列が含まれています。 基本的な挿入では、置き換えられた文字列は空で、基本的な削除の場合、置換後の文字列は空になります。 正規化されたコレクションは、 `null` テキストバッファーの最新バージョンに対して常にです。

<xref:Microsoft.VisualStudio.Text.ITextEdit>テキストバッファーに対していつでもインスタンス化できるオブジェクトは1つだけです。また、テキストバッファーを所有しているスレッドですべてのテキスト編集を実行する必要があります (所有権が要求されている場合)。 テキスト編集は、メソッドまたはメソッドを呼び出すことによって破棄でき `Cancel` `Dispose` ます。

<xref:Microsoft.VisualStudio.Text.ITextBuffer> また、は `Insert()` 、 `Delete()` `Replace()` インターフェイス上で検出されたものと類似した、、およびの各メソッドも提供し <xref:Microsoft.VisualStudio.Text.ITextEdit> ます。 これらの呼び出しは、オブジェクトを作成し、同様の呼び出しを行って、編集を適用するのと同じ効果があり <xref:Microsoft.VisualStudio.Text.ITextEdit> ます。

#### <a name="tracking-points-and-tracking-spans"></a>追跡ポイントと追跡スパン

は、 <xref:Microsoft.VisualStudio.Text.ITrackingPoint> テキストバッファー内の文字位置を表します。 文字の位置をシフトするようにバッファーが編集されている場合、追跡ポイントはそれをシフトします。 たとえば、追跡ポイントがバッファー内の位置10を参照し、5文字がバッファーの先頭に挿入されている場合、追跡ポイントは位置15を表します。 追跡ポイントによって示される位置だけで挿入が行われる場合、その動作は <xref:Microsoft.VisualStudio.Text.PointTrackingMode> 、またはのいずれかであるによって決まり `Positive` `Negative` ます。 追跡モードが正の場合、追跡ポイントは同じ文字を参照しますが、これは挿入の最後にあります。 追跡モードが負の場合、追跡ポイントは元の位置に挿入された最初の文字を参照します。 追跡ポイントによって表される位置にある文字が削除されると、追跡ポイントは削除された範囲の後の最初の文字に移動します。 たとえば、追跡ポイントが位置5の文字を参照し、位置 3 ~ 6 の文字が削除された場合、追跡ポイントは位置3の文字を参照します。

は、 <xref:Microsoft.VisualStudio.Text.ITrackingSpan> 1 つの位置だけではなく、文字の範囲を表します。 その動作は、によって決まり <xref:Microsoft.VisualStudio.Text.SpanTrackingMode> ます。 スパントラッキングモードが [SpanTrackingMode](xref:Microsoft.VisualStudio.Text.SpanTrackingMode.EdgeInclusive)の場合、追跡スパンは、端に挿入されたテキストを組み込むように拡大されます。 スパントラッキングモードが [SpanTrackingMode](xref:Microsoft.VisualStudio.Text.SpanTrackingMode.EdgeExclusive)の場合、追跡スパンには、端に挿入されたテキストは組み込まれません。 ただし、スパントラッキングモードが [SpanTrackingMode](xref:Microsoft.VisualStudio.Text.SpanTrackingMode.EdgePositive)の場合、挿入は開始位置に向かって現在位置をプッシュします。スパントラッキングモードが [SpanTrackingMode](xref:Microsoft.VisualStudio.Text.SpanTrackingMode.EdgeNegative)の場合は、挿入によって末尾に向かって現在位置がプッシュされます。

追跡ポイントの位置または追跡範囲の範囲を取得して、それらが属するテキストバッファーのスナップショットを取得できます。 追跡ポイントと追跡範囲は、どのスレッドからも安全に参照できます。

#### <a name="content-types"></a>コンテンツの種類

コンテンツの種類は、さまざまな種類のコンテンツを定義するためのメカニズムです。 コンテンツの種類には、"text"、"code"、"binary" などのファイルの種類や、"xml"、"vb"、"c#" などのテクノロジの種類を使用できます。 たとえば、"using" という語は C# と Visual Basic の両方でキーワードですが、他のプログラミング言語では使用できません。 したがって、このキーワードの定義は、"c#" および "vb" のコンテンツ型に制限されます。

コンテンツタイプは、エディターの修飾要素およびその他の要素のフィルターとして使用されます。 多くのエディター機能と拡張ポイントは、コンテンツの種類ごとに定義されます。 たとえば、テキストの色分けは、プレーンテキストファイル、XML ファイル、Visual Basic ソースコードファイルによって異なります。 通常、テキストバッファーには、作成時にコンテンツタイプが割り当てられ、テキストバッファーのコンテンツタイプを変更できます。

コンテンツの種類は、他のコンテンツの種類から複数継承できます。 では、 <xref:Microsoft.VisualStudio.Utilities.ContentTypeDefinition> 特定のコンテンツタイプの親として複数の基本型を指定できます。

開発者は、独自のコンテンツタイプを定義し、を使用して登録でき <xref:Microsoft.VisualStudio.Utilities.IContentTypeRegistryService> ます。 を使用すると、特定のコンテンツの種類に対してさまざまなエディター機能を定義でき <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> ます。 たとえば、エディターの余白、装飾、およびマウスハンドラーは、特定のコンテンツの種類を表示するエディターにのみ適用されるように定義できます。

### <a name="the-text-view"></a>テキストビュー

モデルビューコントローラー (MVC) パターンのビューパーツには、テキストビュー、ビューの書式設定、スクロールバーなどのグラフィック要素、およびカレットが定義されています。 Visual Studio エディターのすべてのプレゼンテーション要素は、WPF に基づいています。

#### <a name="text-views"></a>テキストビュー

インターフェイスは、 <xref:Microsoft.VisualStudio.Text.Editor.ITextView> プラットフォームに依存しないテキストビューの表現です。 これは主に、テキストドキュメントをウィンドウに表示するために使用されますが、他の目的 (ツールヒントなど) でも使用できます。

テキストビューでは、さまざまな種類のテキストバッファーが参照されます。 プロパティは、 <xref:Microsoft.VisualStudio.Text.Editor.ITextView.TextViewModel%2A> <xref:Microsoft.VisualStudio.Text.Editor.ITextViewModel> この3つの異なるテキストバッファーを参照するオブジェクトを参照します。データバッファーは、最上位のデータレベルバッファー、編集バッファー、編集が発生します。ビジュアルバッファー (テキストビューに表示されるバッファー) です。

テキストは、基になるテキストバッファーに関連付けられている分類子に基づいて書式設定され、テキストビュー自体に関連付けられている表示設定プロバイダーを使用して装飾されます。

#### <a name="the-text-view-coordinate-system"></a>テキストビューの座標系

テキストビューの座標系は、テキストビュー内の位置を指定します。 この座標系では、x 値0.0 は表示されているテキストの左端に対応し、y 値0.0 は表示されるテキストの上端に対応します。 X 座標は左から右に増加し、y 座標は上から下に増加します。

ビューポート (テキストウィンドウに表示されるテキストの一部) は、垂直方向にスクロールされるのと同じ方法で水平方向にスクロールすることはできません。 ビューポートは、描画サーフェイスに合わせて左の座標を変更することで水平方向にスクロールされます。 ただし、ビューポートは、表示されるテキストを変更することによってのみ垂直方向にスクロールできます。これにより、 <xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged> イベントが発生します。

座標系の距離は、論理ピクセルに対応します。 テキストレンダリングサーフェイスが拡大縮小変換なしで表示されている場合、テキストレンダリングの座標系の1つの単位が、ディスプレイの1ピクセルに対応します。

#### <a name="margins"></a>余白

インターフェイスは、余白を <xref:Microsoft.VisualStudio.Text.Editor.ITextViewMargin> 表し、余白とそのサイズの表示を制御できるようにします。 定義済みの余白が4つあります。このマージンには、"Top"、"Left"、"Right"、および "Bottom" という名前が付けられ、ビューの上、下、左、または右の端にアタッチされます。 これらの余白は、他の余白を配置できるコンテナーです。 インターフェイスは、余白のサイズと余白の表示を返すメソッドを定義します。 余白は、添付されているテキストビューに関する追加情報を提供するビジュアル要素です。 たとえば、行番号の余白には、テキストビューの行番号が表示されます。 グリフの余白には UI 要素が表示されます。

インターフェイスは、 <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewMarginProvider> 余白の作成と配置を処理します。 余白は、他の余白に対して並べ替えることができます。 優先順位の高い余白は、テキストビューの近くに配置されます。 たとえば、左余白が2つあり、余白 A と余白 B があり、余白 B の優先度が余白 A より低い場合、余白 B は余白 A の左側に表示されます。

#### <a name="the-text-view-host"></a>テキストビューのホスト

インターフェイスには、 <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewHost> テキストビューと、スクロールバーなど、ビューに付随するすべての装飾が含まれています。 テキストビューのホストには、ビューの境界線に関連付けられている余白も含まれています。

#### <a name="formatted-text"></a>書式付きテキスト

テキストビューに表示されるテキストは、オブジェクトで構成され <xref:Microsoft.VisualStudio.Text.Formatting.ITextViewLine> ます。 すべてのテキストビュー行は、テキストビュー内の1行のテキストに対応します。 基になるテキストバッファー内の長い行は、部分的に隠されているか (ワードラップが有効になっていない場合)、または複数のテキストビュー線に分割されている場合があります。 インターフェイスには、 <xref:Microsoft.VisualStudio.Text.Formatting.ITextViewLine> 座標と文字の間のマッピングを行うためのメソッドとプロパティ、およびその行に関連付けられる可能性のある修飾要素が含まれています。

<xref:Microsoft.VisualStudio.Text.Formatting.ITextViewLine> オブジェクトは、インターフェイスを使用して作成され <xref:Microsoft.VisualStudio.Text.Formatting.IFormattedLineSource> ます。 現在ビューに表示されているテキストを気にするだけの場合は、書式設定ソースを無視できます。 ビューに表示されないテキストの形式 (リッチテキストの切り取りと貼り付けをサポートする場合など) に関心がある場合は、を使用してテキスト <xref:Microsoft.VisualStudio.Text.Formatting.IFormattedLineSource> バッファー内のテキストの書式を設定できます。

テキストビューでは、一度に1つずつ書式設定され <xref:Microsoft.VisualStudio.Text.ITextSnapshotLine> ます。

## <a name="editor-features"></a>エディターの機能

エディターの機能は、機能の定義が実装とは別のものになるように設計されています。 エディターには次の機能が含まれています。

- タグと分類子

- 修飾

- プロジェクション

- アウトライン

- マウスとキーのバインド

- 操作とプリミティブ

- IntelliSense

### <a name="tags-and-classifiers"></a>タグと分類子

タグは、テキストの範囲に関連付けられているマーカーです。 たとえば、テキストの色分け、下線、グラフィックス、ポップアップなどを使用して、さまざまな方法で表示できます。 分類子は、1つの種類のタグです。

他の種類のタグは <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> 、テキストの強調表示、アウトラインの表示、およびコンパイルエラーに使用され <xref:Microsoft.VisualStudio.Text.Tagging.OutliningRegionTag> <xref:Microsoft.VisualStudio.Text.Tagging.ErrorTag> ます。

#### <a name="classification-types"></a>分類の種類

<xref:Microsoft.VisualStudio.Text.Classification.IClassificationType>インターフェイスは、テキストの抽象カテゴリである等価クラスを表します。 分類の種類は、他の分類の種類から多重継承できます。 たとえば、プログラミング言語の分類には、"keyword"、"comment"、"identifier" などがあります。これらはすべて "code" から継承されます。 自然言語分類型には、"名詞"、"verb"、"形容詞" などがあります。これらはすべて "自然言語" から継承されます。

#### <a name="classifications"></a>分類

分類は、特定の分類の種類のインスタンスであり、通常はテキストの範囲を超えています。 は、 <xref:Microsoft.VisualStudio.Text.Classification.ClassificationSpan> 分類を表すために使用されます。 分類スパンは、特定のテキスト範囲をカバーするラベルと考えることができ、このテキストの範囲が特定の分類の種類であることがシステムに通知されます。

#### <a name="classifiers"></a>分類子

<xref:Microsoft.VisualStudio.Text.Classification.IClassifier>は、テキストを分類のセットに分割するメカニズムです。 特定のコンテンツタイプに対して分類子を定義し、特定のテキストバッファー用にインスタンス化する必要があります。 <xref:Microsoft.VisualStudio.Text.Classification.IClassifier>テキスト分類に参加するには、クライアントがを実装する必要があります。

#### <a name="classifier-aggregators"></a>分類子アグリゲーター

分類子アグリゲーターは、1つのテキストバッファーのすべての分類子を1つの分類セットにまとめるメカニズムです。 たとえば、C# 分類子と英語の分類子の両方で、C# ファイル内のコメントに対して分類を作成できます。 次のコメントを検討してください。

```
// This method produces a classifier
```

C# 分類子は、スパン全体にコメントとしてラベルを付けることができます。また、英語の分類子は、"生成" を "動詞" および "method" として "名詞" として分類します。 アグリゲーターは、重複しない分類のセットを生成し、セットの型はすべての貢献に基づいています。

分類子アグリゲーターは、テキストを分類のセットに分割するため、分類器でもあります。 また、分類子アグリゲーターは、重複する分類がなく、分類が並べ替えられていることも確認します。 個々の分類子は、任意の順序で任意の順序で任意の分類の任意のセットを返すことができ、任意の方法で重複します。

#### <a name="classification-formatting-and-text-coloring"></a>分類の書式設定とテキストの色分け

テキストの書式設定は、テキスト分類に基づいて作成された機能の一例です。 これは、テキストビューレイヤーによって、アプリケーションのテキストの表示を決定するために使用されます。 テキストの書式設定領域は WPF に依存しますが、分類の論理定義は異なります。

分類形式とは、特定の分類の種類に対する一連の書式設定プロパティのことです。 これらの形式は、分類の種類の親の形式から継承されます。

<xref:Microsoft.VisualStudio.Text.Classification.IClassificationFormatMap>は、分類の種類から一連のテキスト書式設定プロパティへのマップです。 エディターでの書式マップの実装によって、分類形式のすべてのエクスポートが処理されます。

### <a name="adornments"></a>修飾

装飾は、テキストビュー内の文字のフォントと色に直接関係しないグラフィック効果です。 たとえば、多くのプログラミング言語で非コンパイルコードをマークするために使用される赤い波線の下線は埋め込まれた表示要素で、ツールヒントはポップアップ表示されます。 装飾はから派生 <xref:System.Windows.UIElement> し、を実装 <xref:Microsoft.VisualStudio.Text.Tagging.ITag> します。 表示要素の2つの特殊な型には、 <xref:Microsoft.VisualStudio.Text.Tagging.SpaceNegotiatingAdornmentTag> ビュー内のテキストと同じスペースを使用する装飾、および <xref:Microsoft.VisualStudio.Text.Tagging.ErrorTag> 波線の下線のがあります。

埋め込み装飾は、書式設定されたテキストビューの一部を形成するグラフィックスです。 これらは、異なる Z オーダーレイヤーに編成されています。 次の3つの組み込みレイヤーがあります。テキスト、キャレット、および選択です。 ただし、開発者はさらに多くのレイヤーを定義し、互いに対して順番に配置することができます。 埋め込まれた装飾の3種類は、テキスト相対装飾 (テキストが移動されたときに移動され、テキストが削除されると削除される)、ビュー相対装飾 (ビューのテキスト以外の部分で実行する必要があります)、およびオーナー制御の装飾 (開発者が配置を管理する必要があります) です。

ポップアップ表示文字は、テキストビューの上の小さなウィンドウ (ツールヒントなど) に表示されるグラフィックスです。

### <a name="projection"></a><a name="projection"></a> アイソメトリック

射影は、実際にはテキストを格納せず、他のテキストバッファーのテキストを結合する、別の種類のテキストバッファーを構築するための手法です。 たとえば、2つのバッファーのテキストを連結し、1つのバッファーにあるかのように結果を表示したり、1つのバッファー内のテキストの一部を非表示にしたりするために、プロジェクションバッファーを使用できます。 プロジェクションバッファーは、別のプロジェクションバッファーへのソースバッファーとして機能することができます。 プロジェクションによって関連付けられた一連のバッファーを構築して、さまざまな方法でテキストを並べ替えることができます。 (このようなセットは、 *バッファーグラフ* とも呼ばれます)。Visual Studio のテキストアウトライン機能は、折りたたまれたテキストを非表示にするためのプロジェクションバッファーを使用して実装されます。また、ASP.NET ページの Visual Studio エディターでは、射影を使用して Visual Basic や C# などの埋め込み言語をサポートしています。

<xref:Microsoft.VisualStudio.Text.Projection.IProjectionBuffer>は、を使用して作成され <xref:Microsoft.VisualStudio.Text.Projection.IProjectionBufferFactoryService> ます。 プロジェクションバッファーは、 <xref:Microsoft.VisualStudio.Text.ITrackingSpan> *ソース範囲* と呼ばれる順序付けられたオブジェクトのシーケンスによって表されます。 これらの範囲の内容は、文字のシーケンスとして表示されます。 ソース範囲の描画元となるテキストバッファーには、" *ソースバッファー*" という名前が付けられます。 プロジェクションバッファーのクライアントは、通常のテキストバッファーとは異なることを認識している必要はありません。

プロジェクションバッファーは、ソースバッファーのテキスト変更イベントをリッスンします。 ソーススパン内のテキストが変化すると、プロジェクションバッファーは、変更されたテキスト座標を独自の座標にマップし、適切なテキスト変更イベントを発生させます。 たとえば、次の内容を含むソースバッファー A と B を考えてみます。

```
A: ABCDE
B: vwxyz
```

プロジェクションバッファー P が2つのテキスト範囲から形成されている場合 (1 つはバッファー A を持ち、もう1つはバッファー B を含む)、P の内容は次のようになります。

```
P: ABCDEvwxyz
```

部分文字列 `xy` がバッファー B から削除されると、バッファー P は、位置7と8の文字が削除されたことを示すイベントを生成します。

また、プロジェクションバッファーを直接編集することもできます。 適切なソースバッファーに編集を反映します。 たとえば、文字列が位置 6 (文字 "v" の元の位置) にある buffer P に挿入される場合、挿入はバッファー B の位置1に反映されます。

プロジェクションバッファーに寄与するソース範囲には制限があります。 コピー元のスパンは重複してはなりません。プロジェクションバッファー内の位置は、ソースバッファー内の複数の場所にマップすることはできません。また、ソースバッファー内の位置は、プロジェクションバッファー内の複数の場所にマップすることはできません。 ソースバッファーリレーションシップでは、circularities は許可されません。

イベントは、プロジェクションバッファーのソースバッファーのセットが変更されたときと、ソースのセットが変化したときに発生します。
省略バッファーは、特別な種類のプロジェクションバッファーです。 これは主に、テキストのブロックを展開したり折りたたんだりする操作に使用されます。 省略バッファーは、1つのソースバッファーにのみ基づいています。省略バッファー内の範囲は、ソースバッファーで順序付けられているものと同じ順序にする必要があります。

#### <a name="the-buffer-graph"></a>バッファーグラフ

<xref:Microsoft.VisualStudio.Text.Projection.IBufferGraph>インターフェイスを使用すると、プロジェクションバッファーのグラフ間でマッピングを行うことができます。 すべてのテキストバッファーとプロジェクションバッファーは、言語コンパイラによって生成される抽象構文ツリーと同様に、有向非循環グラフで収集されます。 グラフは、任意のテキストバッファーにすることができる、上位バッファーによって定義されます。 バッファーグラフは、上位バッファーのポイントからソースバッファー内のポイント、または上部バッファーのスパンからソースバッファー内の一連のスパンにマップできます。 同様に、ポイントまたはスパンをソースバッファーから上位バッファーのポイントにマップすることもできます。 バッファーグラフは、を使用して作成され <xref:Microsoft.VisualStudio.Text.Projection.IBufferGraphFactoryService> ます。

#### <a name="events-and-projection-buffers"></a>イベントとプロジェクションバッファー

プロジェクションバッファーを変更すると、その変更は、プロジェクションバッファーから、それに依存するバッファーに送信されます。 すべてのバッファーが変更されると、最も深いバッファーから開始して、バッファー変更イベントが発生します。

### <a name="outlining"></a>アウトライン

アウトラインは、テキストビュー内の異なるテキストブロックを展開または折りたたむことができます。 アウトラインは <xref:Microsoft.VisualStudio.Text.Tagging.ITag> 、装飾が定義されている場合と同じように、一種として定義されます。 は、 <xref:Microsoft.VisualStudio.Text.Tagging.OutliningRegionTag> 展開または折りたたみが可能なテキスト領域を定義するタグです。 アウトラインを使用するには、をインポートしてを取得する必要があり <xref:Microsoft.VisualStudio.Text.Outlining.IOutliningManagerService> <xref:Microsoft.VisualStudio.Text.Outlining.IOutliningManager> ます。 アウトラインマネージャーでは、オブジェクトとして表されるさまざまなブロックを列挙、折りたたみ、展開し、 <xref:Microsoft.VisualStudio.Text.Outlining.ICollapsible> それに応じてイベントを発生させます。

### <a name="mouse-bindings"></a>マウスバインド

マウスのバインドは、マウスの移動を別のコマンドにリンクします。 マウスバインドはを使用して定義され、 <xref:Microsoft.VisualStudio.Text.Editor.IMouseProcessorProvider> キーバインドはを使用して定義され <xref:Microsoft.VisualStudio.Text.Editor.IKeyProcessorProvider> ます。 では、すべてのバインドが自動的にインスタンス化され、 <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewHost> ビュー内のマウスイベントに接続されます。

インターフェイスには、 <xref:Microsoft.VisualStudio.Text.Editor.IMouseProcessor> さまざまなマウスイベントの処理前および処理後のイベントハンドラーが含まれています。 イベントの1つを処理するには、のメソッドの一部をオーバーライドでき <xref:Microsoft.VisualStudio.Text.Editor.MouseProcessorBase> ます。

### <a name="editor-operations"></a>エディターの操作

エディター操作は、スクリプトやその他の目的で、エディターとの対話を自動化するために使用できます。 は、指定されたに <xref:Microsoft.VisualStudio.Text.Operations.IEditorOperationsFactoryService> 対するアクセス操作にインポートでき <xref:Microsoft.VisualStudio.Text.Editor.ITextView> ます。 これらのオブジェクトを使用して、選択の変更、ビューのスクロール、またはカレットをビューのさまざまな部分に移動できます。

### <a name="intellisense"></a>IntelliSense

IntelliSense では、ステートメント入力候補、シグネチャヘルプ (パラメーターヒントとも呼ばれます)、クイックヒント、および電球がサポートされています。

ステートメント入力候補には、メソッド名、XML 要素、およびその他のコーディング要素やマークアップ要素に対して候補となる候補のポップアップリストが表示されます。 一般に、ユーザージェスチャは、完了セッションを呼び出します。 このセッションでは、候補となる候補の一覧が表示されます。ユーザーはこの一覧を選択するか、一覧を無視することができます。 は <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionBroker> 、を作成およびトリガーする役割を担い <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSession> ます。 は、 <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource> <xref:Microsoft.VisualStudio.Language.Intellisense.CompletionSet> セッションの完了項目のを計算します。

## <a name="see-also"></a>こちらもご覧ください

- [言語サービスとエディターの拡張点](../extensibility/language-service-and-editor-extension-points.md)
- [エディターのインポート](../extensibility/editor-imports.md)
