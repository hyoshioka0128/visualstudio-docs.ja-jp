---
title: オブジェクト |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- VSTextBuffer
helpviewer_keywords:
- VSTextBuffer object, reference
- views [Visual Studio SDK], VSTextBuffer object
ms.assetid: c5f94b45-7249-4e1f-a53d-1d2a1c61e0ef
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a5ea44d2b22c96d49f334f2ea33f9db8d69b5eb0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697722"
---
# <a name="vstextbuffer-object"></a>オブジェクト
テキスト バッファー オブジェクトは、通常、ファイルに関連付けられている Unicode テキストのストリームを表します。 オブジェクト<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer>は、コア エディターのコンテキストの外部で使用できます ( ウィザードなど) 。

 次の表に、 の`VSTextBuffer`インターフェイスを示します。

|Method|説明|
|------------|-----------------|
|[Iolecommandtarget](/windows/desktop/api/docobj/nn-docobj-iolecommandtarget)|標準 OLE インターフェイス。 バッファ内の元に戻す/やり直し処理に使用します。|
|[ファイルを保存します。](/windows/desktop/api/objidl/nn-objidl-ipersistfile)|標準 OLE インターフェイス。|
|[I永続ストリーム](/windows/desktop/api/objidl/nn-objidl-ipersiststream)|標準 OLE インターフェイス。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompoundAction>|複合アクション (単一の取り消し/やり直し単位にグループ化されたアクション) の作成を有効にします。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData>|テキスト バッファーによって管理されるドキュメント データの永続化を有効にします。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>|基本的なサービスを提供します。多くのクライアントで使用されます。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextFind>|バッファの検索に使用します。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines>|2 次元座標を使用して読み取りおよび書き込み機能を提供します。 `IVsTextBuffer` から継承されます。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStream>|1 次元座標を使用して読み取りおよび書き込み機能を提供します。 `IVsTextBuffer` から継承されます。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextScanner>|バッファー内のテキストに高速でストリーム指向のシーケンシャル アクセスを提供します。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsUserData>|プロパティのジェネリック コレクションへのアクセスを提供します。 最も重要なプロパティは、バッファーの名前またはモニカーです。 GUID を作成し、キーとして使用することで、このインターフェイスを使用して、独自のランダム データをバッファーに格納できます。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer>|イベントのコネクション ポイントをサポートします。|

## <a name="remarks"></a>Remarks
 `VSTextBuffer`通常は、 の`QueryInterface``IVsTextBuffer`呼び出しによって見つかります。 詳細については、「テキスト[バッファー](/visualstudio/extensibility/accessing-the-text-buffer-by-using-the-legacy-api?view=vs-2015)」を参照してください。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>
- <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView>
- [フィギュア編集](https://www.microsoft.com/download/details.aspx?id=55984)
