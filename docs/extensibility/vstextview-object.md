---
title: VSTextView オブジェクト |Microsoft Docs
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
ms.openlocfilehash: 06e1ba7c10912f23fedc09892e03e2105ff2bab4
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "91583607"
---
# <a name="vstextview-object"></a>VSTextView オブジェクト

テキストビューは、テキストバッファーの Unicode テキストをユーザーが表示および編集できるウィンドウです。 基本的に、ビューは、ほとんどのユーザーがエディターとして参照します。 ビューは、さまざまなテキストレイヤー (右端での折り返し、アウトラインテキストなど) によってバッファーから分離されているため、ビューはバッファー内のテキストを正確に表現するとは限りません。 テキストビューの詳細については、「 [従来の API を使用したテキストビューへのアクセス](../vs-2015/extensibility/accessing-thetext-view-by-using-the-legacy-api.md?view=vs-2015&preserve-view=true)」を参照してください。

次の表は、オブジェクト内のインターフェイスを示して <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView> います。

|インターフェイス|説明|
|---------------|-----------------|
|[IDropSource](/windows/desktop/api/oleidl/nn-oleidl-idropsource)|標準 OLE インターフェイス。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IDropTarget>|標準 OLE インターフェイス。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IObjectWithSite>|標準 OLE インターフェイス。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>|標準 OLE インターフェイス。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompoundAction>|複合アクション (つまり、1つの元に戻す/やり直し単位でグループ化されたアクション) の作成を有効にします。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>|ビューを管理およびアクセスするための基本的なメソッドを提供します。 `IVsTextView` はスレッドセーフではありません。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>|ウィンドウペインを作成および管理します。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLayeredTextView>|テキストレイヤーと対話します。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsThreadSafeTextView>|別のスレッドからビューに対して操作を実行します。|

## <a name="see-also"></a>関連項目

- [図形の編集](https://www.microsoft.com/download/details.aspx?id=55984)
- [VSTextBuffer オブジェクト](../extensibility/vstextbuffer-object.md)