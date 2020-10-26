---
title: VSCodeWindow オブジェクト |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- VSCodeWindow
helpviewer_keywords:
- views [Visual Studio SDK], VSCodeWindow object
- VsCodeWindow object
ms.assetid: cf5fe926-e784-4098-bc01-cac49c7c55c6
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 511c730ec3a11b02d46f5e9c9271c028bb4fa325
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65690770"
---
# <a name="vscodewindow-object"></a>VSCodeWindow オブジェクト
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

コードウィンドウは、1つまたは複数のテキストビュー (通常はオブジェクト) を含むことができる特殊なドキュメントウィンドウです <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView> 。  
  
 アーキテクチャ上、コードウィンドウはウィンドウフレーム内のドキュメントウィンドウです。 機能的には、コードウィンドウは単なるドキュメントウィンドウであり、追加機能があります。 マルチドキュメントインターフェイス (MDI) モードでは、コードウィンドウは MDI 子フレームです。 詳細については、「 [従来の API を使用してコードウィンドウをカスタマイズする](../extensibility/customizing-code-windows-by-using-the-legacy-api.md)」を参照してください。  
  
 次の表は、オブジェクト内のインターフェイスを示してい <xref:Microsoft.VisualStudio.TextManager.Interop.VsCodeWindow> ます。  
  
|メソッド|説明|  
|------------|-----------------|  
|<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>|グローバル一意識別子 (GUID) によって識別されるサービスを検索するための汎用アクセス機構を提供します。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow>|1つ以上のコードビューを含むマルチドキュメントインターフェイス (MDI) 子を表します。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>|ウィンドウフレームを塗りつぶします。|  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>   
 [図形の編集](https://msdn.microsoft.com/f08872bd-fd9c-4e36-8cf2-a2a2622ef986)
