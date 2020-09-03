---
title: ドキュメントの読み込みの遅延 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: fb07b8e2-a4e3-4cb0-b04f-8eb11c491f35
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5565749a21614bb0b882beab8c83ed63bc839229
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68196871"
---
# <a name="delayed-document-loading"></a>ドキュメントの読み込みの遅延
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

ユーザーが Visual Studio ソリューションを再び開くと、関連付けられているドキュメントのほとんどはすぐに読み込まれません。 ドキュメントウィンドウフレームは、保留中の初期化状態で作成され、プレースホルダードキュメント (スタブフレームと呼ばれます) が実行中のドキュメントテーブル (RDT) に配置されます。  
  
 ドキュメント内の要素を読み込んだ後にクエリを実行することで、拡張機能によってプロジェクトドキュメントが不必要に読み込まれる場合があります。 これにより、Visual Studio の総メモリ使用量が増加します。  
  
## <a name="document-loading"></a>ドキュメントの読み込み  
 スタブフレームとドキュメントは、ユーザーがドキュメントにアクセスしたときに完全に初期化されます。たとえば、ウィンドウフレームのタブを選択します。 ドキュメントは、ドキュメントデータを取得するために RDT に直接アクセスするか、次のいずれかの呼び出しを行うことによって間接的に RDT にアクセスすることによって、ドキュメントのデータを要求する拡張機能によって初期化することもできます。  
  
- ウィンドウフレーム表示メソッド: <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.Show%2A> 。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A>次のいずれかのプロパティのウィンドウフレーム GetProperty メソッド。  
  
  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>  
  
  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>  
  
  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>  
  
  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>  
  
  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>  
  
  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>  
  
  拡張機能でマネージコードを使用する場合は、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.GetDocumentInfo%2A> ドキュメントが保留中の初期化状態でないことがわかっているか、ドキュメントを完全に初期化する必要がある場合を除き、を呼び出さないでください。 これは、このメソッドは常に doc データオブジェクトを返し、必要に応じて作成するためです。 代わりに、IVsRunningDocumentTable4 インターフェイスのメソッドのいずれかを呼び出す必要があります。  
  
  拡張機能で C++ が使用されている場合は、 `null` 必要のないパラメーターにを渡すことができます。  
  
  関連するプロパティを要求する前に、次のいずれかのメソッドを呼び出すことによって、不要なドキュメントの読み込みを回避できます。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> を使用し <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID6> ます。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentFlags%2A>. このメソッドは、 <xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4> <xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4> ドキュメントがまだ初期化されていない場合は、の値を含むオブジェクトを返します。  
  
  ドキュメントが読み込まれたタイミングは、ドキュメントが完全に初期化されたときに発生する RDT イベントをサブスクライブすることによって確認できます。 次の2つの可能性があります。  
  
- イベントシンクがを実装している場合は、を <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents2> サブスクライブできます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents2.OnAfterAttributeChangeEx%2A>  
  
- それ以外の場合は、にサブスクライブでき <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents.OnAfterAttributeChange%2A> ます。  
  
  次に示すのは、架空のドキュメントアクセスシナリオです。 Visual Studio 拡張機能では、開いているドキュメントに関する情報を表示する必要があります。たとえば、編集ロック数やドキュメントデータに関する情報が表示されます。 を使用して RDT 内のドキュメントを列挙し <xref:Microsoft.VisualStudio.Shell.Interop.IEnumRunningDocuments> 、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.GetDocumentInfo%2A> 各ドキュメントを呼び出して、編集ロック数とドキュメントデータを取得します。 ドキュメントが保留中の初期化状態にある場合、ドキュメントデータを要求すると、不要に初期化されます。  
  
  これをより効率的に行うには、を使用して <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentEditLockCount%2A> 編集ロック数を取得し、を使用して <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentFlags%2A> ドキュメントが初期化されているかどうかを確認します。 フラグにが含まれていない場合 <xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4> 、ドキュメントは既に初期化されており、を使用してドキュメントデータを要求して <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentData%2A> も、不要な初期化は行われません。 フラグにが含ま <xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4> れる場合、ドキュメントが初期化されるまで、拡張子はドキュメントデータを要求しないようにする必要があります。 これは、OnAfterAttributeChange (Ex) イベントハンドラーで検出できます。  
  
## <a name="testing-extensions-to-see-if-they-force-initialization"></a>拡張機能をテストして、初期化を強制的に実行するかどうかを確認する  
 ドキュメントが初期化されているかどうかを示す手掛かりはありません。そのため、拡張機能が強制的に初期化されているかどうかを確認するのが困難な場合があります。 完全に初期化されていないすべてのドキュメントのタイトルにタイトルのテキストが含まれるようにするため、検証を簡単にするレジストリキーを設定でき `[Stub]` ます。  
  
 **HKEY_CURRENT_USER \software\microsoft\visualstudio\14.0\backgroundsolutionload]** で、 **StubTabTitleFormatString**を** {0} [スタブ]** に設定します。
