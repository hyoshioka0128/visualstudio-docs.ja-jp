---
title: エディターアダプターを使用した新しいまたは変更された動作 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - adapter behavior
ms.assetid: 5555b116-cfdb-4773-ba62-af80fda64abd
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: fc7ddaf7ec67a1e33248d5ce424868849200d3e6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68194175"
---
# <a name="new-or-changed-behavior-with-editor-adapters"></a>エディター アダプターの新規または変更された動作
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

以前のバージョンの Visual Studio コアエディターに対して記述されたコードを更新していて、新しい API を使用するのではなく、エディターアダプター (または shim) を使用する予定がある場合は、前のコアエディターに関して、エディターアダプターの動作の次の相違点に注意する必要があります。  
  
## <a name="features"></a>特徴  
  
#### <a name="using-setsite"></a>SetSite () の使用  
 <xref:Microsoft.VisualStudio.OLE.Interop.IObjectWithSite.SetSite%2A>他の操作を実行する前に、テキストバッファー、テキストビュー、およびコードウィンドウを CoCreate する場合は、を呼び出す必要があります。 ただし、この <xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService> サービスの create () メソッド自体はを呼び出すため、を使用して作成する場合は必要ありません <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.SetSite%2A> 。  
  
#### <a name="hosting-ivscodewindow-and-ivstextview-in-your-own-content"></a>独自のコンテンツで IVsCodeWindow と Ivscodewindow をホストする  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> Win32 モードと WPF モードのどちらかを使用して、独自のコンテンツでとの両方をホストできます。 ただし、2つのモードにはいくつかの違いがあることに注意してください。  
  
##### <a name="using-win32-and-wpf-versions-of-ivscodewindow"></a>IVsCodeWindow の Win32 バージョンと WPF バージョンの使用  
 エディターコードウィンドウはから派生したもの <xref:Microsoft.VisualStudio.Shell.WindowPane> で、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane> 新しい WPF インターフェイスだけでなく、古い Win32 インターフェイスも実装して <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIElementPane> います。 メソッドを使用すると、 <xref:Microsoft.VisualStudio.Shell.WindowPane.Microsoft%23VisualStudio%23Shell%23Interop%23IVsWindowPane%23CreatePaneWindow%2A> HWND ベースのホスト環境を作成できます。また、メソッドを使用して WPF ホスティング環境を作成することもでき <xref:Microsoft.VisualStudio.Shell.WindowPane.Microsoft%23VisualStudio%23Shell%23Interop%23IVsUIElementPane%23CreateUIElementPane%2A> ます。 基になるエディターは常に WPF を使用しますが、独自のコンテンツにこのウィンドウペインを直接埋め込む場合は、ホストの要件に適したウィンドウウィンドウの種類を作成できます。  
  
##### <a name="using-win32-and-wpf-versions-of-ivstextview"></a>IVsTextView の Win32 バージョンと WPF バージョンの使用  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>を Win32 モードまたは WPF モードに設定できます。  
  
 エディターファクトリがテキストビューを作成すると、既定では HWND の内部でホストされ、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.GetWindowHandle%2A> hwnd が返されます。 このモードを使用して、WPF コントロール内にエディターを埋め込むことはできません。  
  
 テキストビューを WPF モードに設定するには、を呼び出し、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.Initialize%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.TextViewInitFlags3> パラメーターの初期化フラグの1つとしてを渡す必要があり `InitView` ます。 を <xref:System.Windows.FrameworkElement> 呼び出すことによってを取得でき <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIElementPane.CreateUIElementPane%2A> ます。  
  
 WPF モードは、2つの方法で Win32 モードと異なります。 まず、テキストビューを WPF コンテキストでホストできます。 WPF ペインにアクセスするには、をにキャストし、を <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIElementPane> 呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIElement.GetUIObject%2A> ます。 2番目のは <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.GetWindowHandle%2A> hwnd を返しますが、この hwnd はその位置を確認し、それにフォーカスを設定するためにのみ使用できます。 WM_PAINT メッセージに応答するためにこの HWND を使用することはできません。これは、エディターがウィンドウを描画する方法には影響しないためです。 この HWND は、アダプターを使って新しいエディターコードへの切り替えを容易にするためだけに存在します。 コンポーネントで HWND が必要な場合は、を使用しないことを強くお勧めし `VIF_NO_HWND_SUPPORT` `GetWindowHandle` ます。このモードでは、から返された hwnd の制限が原因です。  
  
#### <a name="passing-arrays-as-parameters-in-native-code"></a>ネイティブコードでのパラメーターとしての配列の引き渡し  
 従来のエディター API には、配列とそのカウントを含むパラメーターを持つメソッドが多数あります。 次に例をいくつか示します。  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewEx.AppendViewOnlyMarkerTypes%2A>  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewEx.RemoveViewOnlyMarkerTypes%2A>  
  
 ネイティブコードでこれらのメソッドを呼び出す場合は、一度に1つの要素のみを渡す必要があります。 複数の要素を渡した場合、プライマリ相互運用機能の実装に問題があるため、呼び出しは拒否されます。  
  
 この問題は、などのメソッドを使用するとより複雑に <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewEx.SetIgnoreMarkerTypes%2A> なります。 このメソッドが呼び出されるたびに、無視されるマーカーの型の前のリストがクリアされるため、このメソッドを3つの異なるマーカーの種類を使用して3回呼び出すことはできません。 唯一の解決策は、このメソッドをマネージコードでのみ呼び出すことです。  
  
#### <a name="threading"></a>スレッド処理  
 常に UI スレッドからバッファーアダプターを呼び出す必要があります。 バッファーアダプターはマネージオブジェクトであるため、マネージコードからの呼び出しでは COM マーシャリングがバイパスされ、呼び出しは UI スレッドに自動的にマーシャリングされません。  バックグラウンドスレッドからバッファーアダプターを呼び出す場合は、 <xref:System.Windows.Threading.Dispatcher.Invoke%2A> または同様のメソッドを使用する必要があります。  
  
#### <a name="lockbuffer-methods"></a>LockBuffer メソッド  
 すべての LockBuffer () メソッドは非推奨とされます。 次に例をいくつか示します。  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer.LockBuffer%2A>  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStream.LockBuffer%2A>  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines.LockBuffer%2A>  
  
#### <a name="commit-events"></a>コミットイベント  
 コミットイベントはサポートされていません。 これらのイベントを通知するメソッドを呼び出すと、メソッドはエラーコードを返します。  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsPreliminaryTextChangeCommitEvents>  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsFinalTextChangeCommitEvents>  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsUndoRedoClusterWithCommitEvents>  
  
#### <a name="texteditorevents"></a>TextEditorEvents  
 は <xref:EnvDTE.TextEditorEvents> コミット () では起動されなくなりました。 代わりに、テキストを変更するたびに起動されます。  
  
#### <a name="text-markers"></a>テキストマーカー  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarker.Invalidate%2A>オブジェクトを削除するときは、を呼び出す必要があり <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarker> ます。 以前のバージョンでは、マーカーの解放のみが必要でした。  
  
#### <a name="line-numbers"></a>[行番号]  
 とのさまざまなメソッドについて <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewEx> 、行番号は、Visual Studio 2008 のように、アウトラインとワードラップを考慮する行番号ではなく、基になるバッファーの行番号に対応します。  
  
 影響を受けるメソッドは次のとおりです (一覧は完全ではありません)。  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.CenterLines%2A>  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.GetCaretPos%2A>  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.GetLineAndColumn%2A>  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.GetNearestPosition%2A>  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.GetPointOfLineColumn%2A>  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.GetTextStream%2A>  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.GetWordExtent%2A>  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.PositionCaretForEditing%2A>  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.ReplaceTextOnLine%2A>  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.SetCaretPos%2A>  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.SetSelection%2A>  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.SetTopLine%2A>  
  
#### <a name="outlining"></a>アウトライン  
 のクライアント <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> では、またはを使用して追加されたアウトライン領域のみが表示され <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession.AddHiddenRegions%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSessionEx.AddHiddenRegionsEx%2A> ます。 これらは、エディターアダプターによって追加されていないため、アドホック領域は表示されません。 同様に、これらのクライアントは、エディターアダプターではなく、新しいエディターコードを使用している言語 (C# および C++ を含む) によって追加されたアウトライン領域を表示しません。  
  
#### <a name="line-heights"></a>線の高さ  
 新しいエディターでは、テキスト行の高さが異なる場合があります。これは、他の行との間で行を移動する可能性がある、フォントサイズと可能な行の変換によって異なります。 などのメソッドによって返される行 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.GetLineHeight%2A> の高さは、既定のフォントサイズを使用して行の変換が適用されていない行の高さです。 この高さは、ビューの線の実際の高さを反映している場合もあれば、表示されない場合もあります。  
  
#### <a name="eventing-and-undo"></a>イベントと元に戻す  
 新しいエディターでは、ビューは、元に戻すクラスターが開いている場合でも、イベントの表示や発生などの操作を継続して実行します。 この動作は、元に戻すクラスターが閉じられるまでこれらの操作を実行しなかった従来のビューとは異なります。  
  
#### <a name="intellisense"></a>IntelliSense  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.UpdateTipWindow%2A>またはを実装していないクラスを渡した場合、メソッドは失敗し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextTipWindow2> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow3> ます。 カスタム Win32 オーナー描画ポップアップはサポートされなくなりました。  
  
#### <a name="smarttags"></a>SmartTags  
 、、、およびの各インターフェイスで作成されたスマートタグに対するアダプターのサポートはありません <xref:Microsoft.VisualStudio.TextManager.Interop.IVsSmartTagData> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsSmartTagTipWindow> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsSmartTagTipWindow2> 。  
  
#### <a name="dte"></a>DTE  
 <xref:EnvDTE80.IncrementalSearch> が実装されていません。  
  
## <a name="unimplemented-methods"></a>実装していないメソッド  
 テキストバッファーアダプター、テキストビューアダプター、およびテキスト層アダプターに実装されていないメソッドがあります。  
  
|インターフェイス|未実装|  
|---------------|---------------------|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>|`Reload(false)` が実装されていません。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator.EnumSpans%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator.SetBufferMappingModes%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator.SetSpanMappings%2A>|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines.GetMarkerData%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines.ReleaseMarkerData%2A>|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.CanReplaceLines%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.CopyLineText%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.CreateTrackingPoint%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.EnumLayerMarkers%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.GetBaseBuffer%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.GetLengthOfLine%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.GetLineCount%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.GetLineText%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.GetMarkerData%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.LockBufferEx%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.MapLocalSpansToTextOriginatingLayer%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.ReleaseMarkerData%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.ReplaceLines%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.ReplaceLinesEx%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.UnlockBufferEx%2A>|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget.Find%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget.Replace%2A>|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLayeredTextView>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLayeredTextView.GetSelectedAtom%2A>|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.GetSelectionDataObject%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.PositionCaretForEditing%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.RestrictViewRange%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateViewFrameCaption%2A>|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewEx>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewEx.GetSmartTagRect%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewEx.InvokeInsertionUI%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewEx.SetHoverWaitTimer%2A>|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow.SetViewClassID%2A>|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.AfterCompletorCommit%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.BeforeCompletorCommit%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.Exec%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.GetContextLocation%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.GetServiceProvider%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.GetSmartTagRect%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.GetSubjectCaretPos%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.GetSubjectSelection%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.GetSubjectText%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.QueryStatus%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.ReplaceSubjectTextSpan%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.SetSubjectCaretPos%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.SetSubjectSelection%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.UpdateSmartTagWindow%2A>|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewIntellisenseHost>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewIntellisenseHost.SetSubjectFromPrimaryBuffer%2A> はアダプターに実装されますが、アウトライン UI では無視されます。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenRegionEx>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenRegionEx.GetBannerAttr%2A> はアダプターに実装されますが、アウトライン UI では無視されます。|
