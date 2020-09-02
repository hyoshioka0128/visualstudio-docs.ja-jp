---
title: 従来の API を使用したコードウィンドウのカスタマイズ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - code windows
ms.assetid: 5328ab2f-55cb-4680-9744-ec79f55acd1b
caps.latest.revision: 20
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f15c649b8d857d2e920bb957e5975d296749cb86
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62556135"
---
# <a name="customizing-code-windows-by-using-the-legacy-api"></a>レガシ API を使用するコード ウィンドウのカスタマイズ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

コードウィンドウは、1つまたは複数のテキストビューをサポートするドキュメントウィンドウオブジェクトです。 コードウィンドウの正確な機能は、関連付けられている言語サービスによって異なります。 マルチドキュメントインターフェイス (MDI) モードでは、コードウィンドウは MDI 子フレームです。  
  
 コードウィンドウは言語サービスによって制御され、各言語サービスは独自のコードウィンドウマネージャーを提供できます。 これにより、言語サービスは、波線や色付けなど、独自の修飾要素をコードウィンドウに追加できます。 コアウィンドウを作成する方法の詳細については、「 [レガシ API を使用したコアエディターのインスタンス](../extensibility/instantiating-the-core-editor-by-using-the-legacy-api.md)化」を参照してください。  
  
 コードウィンドウは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> テキストビューと、オブジェクト内に配置されたすべての修飾を持つオブジェクトです。 コアエディターのインスタンス化中にコードウィンドウを作成すると、次の図に示すように、言語サービスから <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager> コードウィンドウにをアタッチできます。  
  
 ![CodeWindow グラフィック](../extensibility/media/vscodewindow.gif "vscodewindow")  
[コード ウィンドウ]  
  
 言語サービスはコードウィンドウマネージャーを実装し、ドロップダウンバーなどの表示要素の管理を担当します。 コードウィンドウは、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager.AddAdornments%2A> コードウィンドウの初期化中にメソッドを呼び出します。 この呼び出しが行われると、言語サービスは、ドロップダウンバーまたはボタンバー () を <xref:Microsoft.VisualStudio.TextManager.Interop.IVsButtonBarClient> コードウィンドウに追加できます。  
  
## <a name="in-this-section"></a>このセクションの内容  
 `Customizing Code Windows by Using the Legacy API`  
 レガシ API を使用してコードウィンドウをカスタマイズする方法について説明します。  
  
 [方法: エディターを別のエディターでホストする](../extensibility/how-to-host-an-editor-in-another-editor.md)  
 エディターウィンドウ内で2つ目のエディターをホストする方法について説明します。  
  
 [方法: エディターでフォーカスが失われたときにイベントを発生させる](../extensibility/how-to-fire-events-when-the-editor-loses-focus.md)  
 ドキュメントビューをドキュメントデータオブジェクトにアタッチする方法について説明します。  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.VisualStudio.TextManager.Interop.VsCodeWindow>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView>   
 [レガシ API を使用したコアエディターのインスタンス化](../extensibility/instantiating-the-core-editor-by-using-the-legacy-api.md)   
 [レガシ API を使用するテキスト ビューへのアクセス](../extensibility/accessing-thetext-view-by-using-the-legacy-api.md)
