---
title: 遅延ドキュメントの読み込み |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: fb07b8e2-a4e3-4cb0-b04f-8eb11c491f35
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2f78d49013c1f0bd359d4439b73620a159a9ccc0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708814"
---
# <a name="delayed-document-loading"></a>遅延ドキュメントの読み込み

ユーザーが Visual Studio ソリューションを再度開くと、関連付けられているドキュメントのほとんどはすぐに読み込まれません。 ドキュメント ウィンドウ フレームは、初期化が保留状態で作成され、プレースホルダー ドキュメント (スタブ フレームと呼ばれます) が実行中のドキュメント テーブル (RDT) に配置されます。

拡張機能を使用すると、ドキュメント内の要素を読み込む前にクエリを実行してプロジェクト ドキュメントを不必要に読み込むことがあり、Visual Studio の全体的なメモリ使用量が増加する可能性があります。

## <a name="document-loading"></a>ドキュメントの読み込み

スタブ フレームとドキュメントは、たとえばウィンドウ フレームのタブを選択して、ユーザーがドキュメントにアクセスすると完全に初期化されます。 また、ドキュメントのデータを要求する拡張機能によって、RDT に直接アクセスしてドキュメント データを取得するか、次のいずれかの呼び出しを行って間接的に RDT にアクセスして、ドキュメントを初期化することもできます。

- ウィンドウ フレーム<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.Show%2A>メソッド。

- 次のいずれかのプロパティ<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A>のウィンドウ フレーム メソッド。

  - [__VSFPROPID。VSFPROPID_DocView](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_DocView>)

  - [__VSFPROPID。VSFPROPID_ViewHelper](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_ViewHelper>)

  - [__VSFPROPID。VSFPROPID_DocData](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_DocData>)

  - [__VSFPROPID。VSFPROPID_AltDocData](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_AltDocData>)

  - [__VSFPROPID。VSFPROPID_RDTDocData](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_RDTDocData>)

  - [__VSFPROPID。VSFPROPID_SPProjContext](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_SPProjContext>)

- 拡張機能でマネージ コードを使用している場合は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.GetDocumentInfo%2A>ドキュメントが初期化の保留中の状態でないことが確実であるか、またはドキュメントを完全に初期化する必要がある場合以外は呼び出す必要があります。 このメソッドは常に doc データ オブジェクトを返し、必要に応じて作成するためです。 代わりに、インターフェイスのメソッドのいずれかを呼び出す`IVsRunningDocumentTable4`必要があります。

- 拡張機能で C++ を使用している場合`null`は、必要ないパラメーターを渡すことができます。

- 他のプロパティを要求する前に、関連するプロパティを要求する前に、次のいずれかのメソッドを呼び出すことによって、不要なドキュメントの読み込みを回避できます。

  - <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A>__VSFPROPID6を使用します[。VSFPROPID_PendingInitialization](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID6.VSFPROPID_PendingInitialization>).

  - <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentFlags%2A>. このメソッドは、_VSRDTFLAGS4の<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4>値を含むオブジェクトを返[します。](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4.RDT_PendingInitialization>)ドキュメントがまだ初期化されていない場合はRDT_PendingInitializationします。

ドキュメントが完全に初期化されたときに発生する RDT イベントをサブスクライブすることで、ドキュメントが読み込まれたタイミングを確認できます。 次の 2 つの可能性があります。

- イベント シンクが 実装<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents2>されている場合は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents2.OnAfterAttributeChangeEx%2A>をサブスクライブできます。

- それ以外の場合は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents.OnAfterAttributeChange%2A>をサブスクライブできます。

次の例は、架空のドキュメント アクセス シナリオです: Visual Studio 拡張機能は、ロックの編集数やドキュメント データに関する情報など、開いているドキュメントに関する情報を表示します。 RDT のドキュメントををを列挙するには<xref:Microsoft.VisualStudio.Shell.Interop.IEnumRunningDocuments>、 を<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.GetDocumentInfo%2A>使用して、各ドキュメントを呼び出して、編集ロック数とドキュメント データを取得します。 ドキュメントが初期化保留中の状態にある場合、ドキュメント データを要求すると、ドキュメントデータが不必要に初期化されます。

ドキュメントにアクセスするより効率的な方法は、編集ロック<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentEditLockCount%2A>数を取得するために使用し、ドキュメントが初期化<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentFlags%2A>されたかどうかを判断するために使用することです。 フラグに_VSRDTFLAGS4が含まれていない場合[。RDT_PendingInitialization、](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4.RDT_PendingInitialization>)ドキュメントは既に初期化されており、ドキュメント データを要求<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentData%2A>しても不要な初期化は行われません。 フラグに_VSRDTFLAGS4が含まれている場合[。RDT_PendingInitialization、](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4.RDT_PendingInitialization>)ドキュメントが初期化されるまで、拡張機能はドキュメント データの要求を避ける必要があります。 この初期化は`OnAfterAttributeChange(Ex)`、イベント ハンドラで検出できます。

## <a name="test-extensions-to-see-if-they-force-initialization"></a>拡張機能をテストして、強制的に初期化を行っているかどうかを確認する

ドキュメントが初期化されたかどうかを示す表示キューがないため、拡張機能が強制的に初期化されているかどうかを調べるのが難しい場合があります。 完全に初期化されていないすべてのドキュメントのタイトルがタイトルにテキスト *[Stub] を*含むため、検証を容易にするレジストリ キーを設定できます。

**HKEY_CURRENT_USER\ソフトウェア\マイクロソフト\VisualStudio\14.0\バックグラウンドソリューションロード**で、**スタブタブタイトルフォーマット文字列**を*{0}[スタブ]* に設定します。
