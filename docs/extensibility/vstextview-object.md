---
title: オブジェクト |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- VSTextView
helpviewer_keywords:
- VSTextView object, reference
- views [Visual Studio SDK], reference
ms.assetid: 78272ddc-9718-4c65-a94e-a44a2e8d54f4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 81d5e02d6ec18f8561a83b414532a4b78def5c09
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697712"
---
# <a name="vstextview-object"></a>オブジェクト

テキスト ビューは、ユーザーがテキスト バッファーの Unicode テキストを表示および編集できるウィンドウです。 基本的に、ビューはほとんどのユーザーがエディターと呼ぶものです。 ビューはさまざまなテキスト レイヤー (ワード ラップ、アウトライン テキストなど) によってバッファーから分離されているため、ビューがバッファー内のテキストの正確な表現であるとは保証されません。 テキスト ビューの詳細については、「[従来の API を使用してテキスト ビューにアクセスする](/visualstudio/extensibility/accessing-thetext-view-by-using-the-legacy-api?view=vs-2015)」を参照してください。

次の表に、オブジェクト内の<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView>インターフェイスを示します。

|インターフェイス|説明|
|---------------|-----------------|
|[アイドロップソース](/windows/desktop/api/oleidl/nn-oleidl-idropsource)|標準 OLE インターフェイス。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IDropTarget>|標準 OLE インターフェイス。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IObjectWithSite>|標準 OLE インターフェイス。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>|標準 OLE インターフェイス。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompoundAction>|複合アクション (単一の取り消し/やり直し単位でグループ化されたアクション) の作成を有効にします。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>|ビューを管理およびアクセスするための基本的な方法を提供します。 `IVsTextView`スレッド セーフではありません。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>|ウィンドウ ペインを作成および管理します。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLayeredTextView>|テキストレイヤーを操作します。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsThreadSafeTextView>|別のスレッドからビューに対する操作を実行します。|

## <a name="see-also"></a>関連項目

- [フィギュア編集](https://www.microsoft.com/download/details.aspx?id=55984)
- [オブジェクト](../extensibility/vstextbuffer-object.md)
