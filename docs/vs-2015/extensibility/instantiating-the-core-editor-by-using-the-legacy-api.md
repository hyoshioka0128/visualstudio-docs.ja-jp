---
title: レガシ API を使用したコアエディターのインスタンス化 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - instantiating editor
ms.assetid: dda23b18-96ef-43c6-b0dc-06d15cbe5cbb
caps.latest.revision: 30
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 29306a16390039c8ee6e424b81a5ff617e533ab4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68203909"
---
# <a name="instantiating-the-core-editor-by-using-the-legacy-api"></a>レガシ API を使用するコア エディターのインスタンス化
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

エディターは、挿入、削除、コピー、貼り付けなどのテキスト編集機能を担当します。 これらの関数は、テキストの色分け、インデント、IntelliSense のステートメント入力候補など、言語サービスによって提供される関数と組み合わせて使用されます。  
  
 コアエディターのインスタンスをインスタンス化するには、次の3つの方法があります。  
  
- コアエディターのインスタンスをウィンドウに明示的に作成します。  
  
- コアエディターのインスタンスを返すエディターファクトリを指定する  
  
- プロジェクト階層からファイルを開きます。  
  
  以降のセクションでは、従来の API を使用してエディターをインスタンス化する方法について説明します。  
  
## <a name="explicitly-opening-a-core-editor-instance"></a>コアエディターインスタンスを明示的に開く  
 コアエディターのインスタンスを明示的に取得する場合:  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>編集中のドキュメントデータオブジェクトを保持するを取得します。  
  
- インターフェイスからインターフェイスを作成して、ドキュメントデータオブジェクトの行指向表現を作成し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> ます。  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines>メソッドを使用して、インターフェイスの既定の実装のインスタンスのドキュメントデータオブジェクトとして設定し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow.SetBuffer%2A> ます。  
  
   <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow>メソッドを使用して、インターフェイスでインスタンスをホストし <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.CreateToolWindow%2A> ます。  
  
  この時点で、インターフェイスを表示すると、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> コアエディターのインスタンスを含むウィンドウが表示されます。  
  
  ただし、これは非常に便利なインスタンスではありません。これは、ショートカットキーがないため、または高度な機能へのアクセスがないためです。 ショートカットキーと高度な機能へのアクセスを取得するには:  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer.SetLanguageServiceID%2A>言語サービスと、エディターが使用するドキュメントデータオブジェクトを関連付けるには、メソッドを使用します。  
  
- 独自のショートカットキーを作成するか、オブジェクトの表示プロパティを設定してシステムの既定値を使用し <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> ます。 これを行うには、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.SetGuidProperty%2A> プロパティを使用してメソッドを呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID> ます。  
  
   標準以外のショートカットキーを取得して使用するには、vsct ファイルを使用して生成します。 詳細については、「 [Visual Studio Command Table (.Vsct) Files](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)」を参照してください。  
  
## <a name="how-to-use-an-editor-factory-to-obtain-the-core-editor"></a>エディターファクトリを使用してコアエディターを取得する方法  
 メソッドを使用してエディターファクトリでコアエディターを実装する場合は <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> 、前のセクションで説明したすべての手順に従っ <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow> て、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> オブジェクト内のドキュメントデータオブジェクトを使用してを明示的にホストし <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> ます。  
  
 テキストを表示するには、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> オブジェクトからインターフェイスを取得 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow> し、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> メソッドを呼び出します。  
  
 言語サービスをエディターに提供するには、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer.SetLanguageServiceID%2A> メソッド内でメソッドを呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> ます。  
  
 前のセクションとは異なり、既定のショートカットキーを取得するには、メソッド <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> からコアエディターを取得するときに、メソッドによって返されるコマンドコンテキストを使用し <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> ます。  
  
 メソッドが <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> テキストエディターと同じコマンド GUID を返す場合、コアエディターのインスタンスによって既定のショートカットキーが自動的に取得されます。  
  
 一般的な情報については、「 [チュートリアル: コアエディターの作成」および「エディターファイルの種類の登録](../extensibility/walkthrough-creating-a-core-editor-and-registering-an-editor-file-type.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [コアエディター内](../extensibility/inside-the-core-editor.md)   
 [プロジェクト項目を開いて保存する](../extensibility/internals/opening-and-saving-project-items.md)   
 [チュートリアル: コア エディターの作成とエディター ファイルの種類の登録](../extensibility/walkthrough-creating-a-core-editor-and-registering-an-editor-file-type.md)
