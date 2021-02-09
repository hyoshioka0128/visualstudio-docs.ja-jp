---
title: ドキュメントの読み込みの遅延 |Microsoft Docs
description: Visual Studio でのドキュメントの遅延読み込みと、読み込まれる前にドキュメント内の要素に対してクエリを実行しないように拡張機能をコーディングする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: fb07b8e2-a4e3-4cb0-b04f-8eb11c491f35
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 80c12780b2177c6715af9dc047a5652633993127
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99902904"
---
# <a name="delayed-document-loading"></a>ドキュメントの読み込みの遅延

ユーザーが Visual Studio ソリューションを再び開くと、関連付けられているドキュメントのほとんどはすぐに読み込まれません。 ドキュメントウィンドウフレームは、保留中の初期化状態で作成され、プレースホルダードキュメント (スタブフレームと呼ばれます) が実行中のドキュメントテーブル (RDT) に配置されます。

拡張機能を使用すると、ドキュメント内の要素に対してクエリを実行することで、プロジェクトドキュメントが不必要に読み込まれる可能性があります。これにより、Visual Studio のメモリフットプリント全体が増加する可能性があります。

## <a name="document-loading"></a>ドキュメントの読み込み

スタブフレームとドキュメントは、ユーザーがドキュメントにアクセスしたときに完全に初期化されます。たとえば、ウィンドウフレームのタブを選択します。 ドキュメントは、ドキュメントデータを取得するために RDT に直接アクセスするか、次のいずれかの呼び出しを行うことによって間接的に RDT にアクセスすることによって、ドキュメントのデータを要求する拡張機能によって初期化することもできます。

- ウィンドウフレーム <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.Show%2A> メソッド。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A>次のいずれかのプロパティのウィンドウフレームメソッド。

  - [__VSFPROPID。VSFPROPID_DocView](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_DocView>)

  - [__VSFPROPID。VSFPROPID_ViewHelper](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_ViewHelper>)

  - [__VSFPROPID。VSFPROPID_DocData](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_DocData>)

  - [__VSFPROPID。VSFPROPID_AltDocData](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_AltDocData>)

  - [__VSFPROPID。VSFPROPID_RDTDocData](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_RDTDocData>)

  - [__VSFPROPID。VSFPROPID_SPProjContext](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_SPProjContext>)

- 拡張機能でマネージコードを使用する場合は、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.GetDocumentInfo%2A> ドキュメントが保留中の初期化状態でないことがわかっているか、ドキュメントを完全に初期化する必要がある場合を除き、を呼び出さないでください。 その理由は、メソッドが常に doc データオブジェクトを返し、必要に応じて作成するためです。 代わりに、インターフェイスのメソッドのいずれかを呼び出す必要があり `IVsRunningDocumentTable4` ます。

- 拡張機能で C++ が使用されている場合は、 `null` 必要のないパラメーターにを渡すことができます。

- 他のプロパティを確認する前に、関連するプロパティを要求する前に、次のいずれかのメソッドを呼び出すことによって、不要なドキュメントの読み込みを回避できます。

  - <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> __VSFPROPID6 を使用し [ます。VSFPROPID_PendingInitialization](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID6.VSFPROPID_PendingInitialization>)。

  - <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentFlags%2A>. このメソッドは、 <xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4> _VSRDTFLAGS4 の値を含むオブジェクトを返し [ます。](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4.RDT_PendingInitialization>) ドキュメントがまだ初期化されていない場合は RDT_PendingInitialization します。

ドキュメントが読み込まれたタイミングは、ドキュメントが完全に初期化されたときに発生する RDT イベントをサブスクライブすることによって確認できます。 次の2つの可能性があります。

- イベントシンクがを実装している場合は、を <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents2> サブスクライブできます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents2.OnAfterAttributeChangeEx%2A>

- それ以外の場合は、にサブスクライブでき <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents.OnAfterAttributeChange%2A> ます。

次の例は、架空のドキュメントアクセスシナリオです。たとえば、Visual Studio の拡張機能では、開いているドキュメントに関する情報を表示したい場合があります。たとえば、編集ロック数やドキュメントデータに関する情報が表示されます。 を使用して RDT 内のドキュメントを列挙し <xref:Microsoft.VisualStudio.Shell.Interop.IEnumRunningDocuments> 、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.GetDocumentInfo%2A> 各ドキュメントを呼び出して、編集ロック数とドキュメントデータを取得します。 ドキュメントが保留中の初期化状態にある場合、ドキュメントデータを要求すると、不要に初期化されます。

ドキュメントにアクセスするより効率的な方法は、を使用して <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentEditLockCount%2A> 編集ロック数を取得し、を使用して <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentFlags%2A> ドキュメントが初期化されているかどうかを判断することです。 フラグに _VSRDTFLAGS4 が含まれていない場合は [。RDT_PendingInitialization](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4.RDT_PendingInitialization>)、ドキュメントは既に初期化されており、を使用してドキュメントデータを要求して <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentData%2A> も、不要な初期化は行われません。 フラグに _VSRDTFLAGS4 が含まれている場合は [。RDT_PendingInitialization](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4.RDT_PendingInitialization>)、ドキュメントが初期化されるまで、拡張機能はドキュメントデータを要求しないようにする必要があります。 この初期化は、イベントハンドラーで検出でき `OnAfterAttributeChange(Ex)` ます。

## <a name="test-extensions-to-see-if-they-force-initialization"></a>拡張機能をテストして、初期化を強制的に実行するかどうかを確認します

ドキュメントが初期化されているかどうかを示す手掛かりはありません。そのため、拡張機能が強制的に初期化されているかどうかを確認するのが困難な場合があります。 完全に初期化されていないすべてのドキュメントのタイトルがタイトルに *[スタブ]* として表示されるようにするため、検証を簡単にするレジストリキーを設定できます。

**HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\14.0\BackgroundSolutionLoad** で、 **StubTabTitleFormatString** を *{0} [スタブ]* に設定します。
