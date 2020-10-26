---
title: ドロップダウンバー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - drop-down bar
ms.assetid: 4bb621bd-72f5-43d5-916f-9f66617da049
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7db4296a8fa4146a52d167bce3d8b051aa3ca073
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204656"
---
# <a name="drop-down-bar"></a>ドロップダウン バー
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ドロップダウンバーは、コードウィンドウの上部に表示され、2つのドロップダウンリストが含まれています。  
  
## <a name="drop-down-bar-interfaces"></a>ドロップダウンバーインターフェイス  
 [!INCLUDE[vcprvc](../includes/vcprvc-md.md)]たとえば、ドロップダウンバーには、次の [!INCLUDE[vcprvc](../includes/vcprvc-md.md)] 図に示すように、項目と項目のメンバー関数のリストが表示され [!INCLUDE[vcprvc](../includes/vcprvc-md.md)] ます。  
  
 ![ドロップダウン&#45;バー](../extensibility/media/vsdropdown-bar.gif "vsDropdown_bar")  
ドロップダウンバー  
  
 ドロップダウンバーを実装する場合は、主に重要な4つのインターフェイスがあります。  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBarClient>  
  
     ドロップダウンバーの内容を挿入するには、このインターフェイスを実装します。 各ドロップダウンの組み合わせには、プレーンテキストまたは装飾的なテキスト (太字、下線、斜体) を含めることができます。また、ウィンドウテキストのフォントの色を設定したり、フォントの色をグレー表示したりすることができます。また、必要に応じて、ドロップダウン項目の横に小さいビットマップを指定できます。 インターフェイスと同様に <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet> 、イメージリストにはビットマップイメージが用意されています。 各ドロップダウンの組み合わせには、異なるイメージリストを含めることができます。ただし、各イメージリストには、同じ高さのイメージが含まれている必要があります。 また、メソッドを使用して、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBarClient.GetComboTipText%2A> 各組み合わせのツールヒントを指定することもできます。  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBarManager>  
  
     コードウィンドウのドロップダウンバーを作成または破棄するには、このインターフェイスを呼び出します。 このインターフェイスは、メソッドを呼び出すことによって、ドロップダウンバーが既にコードウィンドウにアタッチされているかどうかを判断するためにも使用でき <xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBarManager.GetDropdownBar%2A> ます。 <xref:System.Runtime.InteropServices.Marshal.QueryInterface%2A>からを <xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBarManager> 呼び出し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow> ます。  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBar>  
  
     ドロップダウンバーと直接通信するには、このインターフェイスを呼び出します。 このインターフェイスを使用すると、ドロップダウンバーの内容を強制的に更新したり、いずれかのリストボックスで選択を変更したりできます。  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManagerEvents>  
  
     `ShowDropdownBarOption`言語サービスのレジストリキーにを登録している場合、コードウィンドウマネージャーは、このイベントを監視して、ドロップダウンバーを表示するかどうかに関するユーザー設定と同期する必要があります。 このオプションを言語サービスキーに登録しない場合、ドロップダウンバーの表示と非表示を切り替えるオプションは、[ **オプション** ] メニューでは無効になります。  
  
## <a name="attaching-a-drop-down-bar-to-a-code-window"></a>コードウィンドウへのドロップダウンバーのアタッチ  
 ドロップダウンバーを作成時にコードウィンドウにアタッチするには、メソッドが呼び出されたときに、言語サービスをドロップダウンバーにアタッチする必要があり <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager.AddAdornments%2A> ます。 メソッドの呼び出しによって <xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBarManager.GetDropdownBar%2A> ドロップダウンバーがまだ存在しないことが示された場合は、を呼び出し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBarManager.AddDropdownBar%2A> ます。 インターフェイスにアクセスするには <xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBarManager> 、 <xref:System.Runtime.InteropServices.Marshal.QueryInterface%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow> 実装がアタッチされたときに、返されたポインターからを呼び出し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager> ます。  
  
## <a name="see-also"></a>参照  
 [レガシ API を使用したコードウィンドウのカスタマイズ](../extensibility/customizing-code-windows-by-using-the-legacy-api.md)   
 [従来の言語サービスでのナビゲーション バーのサポート](../extensibility/internals/support-for-the-navigation-bar-in-a-legacy-language-service.md)
