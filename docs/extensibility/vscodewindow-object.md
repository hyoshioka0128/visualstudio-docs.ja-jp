---
title: オブジェクト |マイクロソフトドキュメント
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
ms.openlocfilehash: 55739b1ef577123ac0395b4c5cfb1e3c5dbc779f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697955"
---
# <a name="vscodewindow-object"></a>オブジェクト
コード ウィンドウは、1 つ以上のテキスト ビュー (通常はオブジェクト)<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView>を含めることができる特殊なドキュメント ウィンドウです。

 アーキテクチャ上、コード ウィンドウは、ウィンドウ フレーム内にあるドキュメント ウィンドウです。 機能的には、コード ウィンドウは、単に追加機能を備えたドキュメント ウィンドウです。 マルチ ドキュメント インターフェイス (MDI) モードでは、コード ウィンドウは、MDI 子フレームです。 詳細については、「[レガシ API を使用したコード ウィンドウのカスタマイズ」](/visualstudio/extensibility/customizing-code-windows-by-using-the-legacy-api?view=vs-2015)を参照してください。

 次の表に、オブジェクト内の<xref:Microsoft.VisualStudio.TextManager.Interop.VsCodeWindow>インターフェイスを示します。

|Method|説明|
|------------|-----------------|
|<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>|グローバル一意識別子 (GUID) が識別するサービスを検索するための汎用アクセス機構を提供します。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow>|1 つ以上のコード ビューを含むマルチ ドキュメント インターフェイス (MDI) 子を表します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>|ウィンドウフレームを塗りつぶします。|

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>
- [フィギュア編集](https://www.microsoft.com/download/details.aspx?id=55984)
