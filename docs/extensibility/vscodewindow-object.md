---
title: VSCodeWindow オブジェクト |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- VSCodeWindow
helpviewer_keywords:
- views [Visual Studio SDK], VSCodeWindow object
- VsCodeWindow object
ms.assetid: cf5fe926-e784-4098-bc01-cac49c7c55c6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d319dfd0f44646f911a01a157a92fc2e5596e492
ms.sourcegitcommit: 4b29efeb3a5f05888422417c4ee236e07197fb94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2020
ms.locfileid: "90012400"
---
# <a name="vscodewindow-object"></a>VSCodeWindow オブジェクト
コードウィンドウは、1つまたは複数のテキストビュー (通常はオブジェクト) を含むことができる特殊なドキュメントウィンドウです <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView> 。

 アーキテクチャ上、コードウィンドウはウィンドウフレーム内のドキュメントウィンドウです。 機能的には、コードウィンドウは単なるドキュメントウィンドウであり、追加機能があります。 マルチドキュメントインターフェイス (MDI) モードでは、コードウィンドウは MDI 子フレームです。 詳細については、「 [従来の API を使用してコードウィンドウをカスタマイズする](../vs-2015/extensibility/customizing-code-windows-by-using-the-legacy-api.md?view=vs-2015)」を参照してください。

 次の表は、オブジェクト内のインターフェイスを示してい <xref:Microsoft.VisualStudio.TextManager.Interop.VsCodeWindow> ます。

|Method|説明|
|------------|-----------------|
|<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>|グローバル一意識別子 (GUID) によって識別されるサービスを検索するための汎用アクセス機構を提供します。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow>|1つ以上のコードビューを含むマルチドキュメントインターフェイス (MDI) 子を表します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>|ウィンドウフレームを塗りつぶします。|

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>
- [図形の編集](https://www.microsoft.com/download/details.aspx?id=55984)