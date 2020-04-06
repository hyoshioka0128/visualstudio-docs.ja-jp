---
title: 言語サービスでのアウトラインサポートの提供 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], outlining support
- language services, supporting outlining
- outlining, supporting
ms.assetid: df759e89-8193-418c-8038-6626304d387b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 37deafa92477289a2124ecee101dd254e68ef01d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707969"
---
# <a name="how-to-provide-expanded-outlining-support-in-a-legacy-language-service"></a>方法: 従来の言語サービスで拡張アウトライン サポートを提供する
言語のアウトラインサポートを拡張するには、[**定義に折りたたむ**] コマンドをサポートする以外に 2 つのオプションがあります。 エディター制御のアウトライン領域を追加したり、クライアント制御のアウトライン領域を追加したりできます。

## <a name="adding-editor-controlled-outline-regions"></a>エディター制御のアウトライン領域の追加
 この方法を使用して、アウトライン領域を作成し、領域が展開、折りたたまれているなどのかどうかをエディターで処理できるようにします。 アウトラインサポートを提供する 2 つのオプションのうち、このオプションは最も堅牢性が低いオプションです。 このオプションでは、 を使用して、指定した範囲のテキストに新しい<xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession.AddOutlineRegions%2A>アウトライン領域を作成します。 この領域が作成されると、その動作はエディターによって制御されます。 エディター制御のアウトライン領域を実装するには、次の手順に従います。

### <a name="to-implement-an-editor-controlled-outline-region"></a>エディター制御アウトライン領域を実装するには

1. への`QueryService`呼び出し<xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager>

     へのポインターが返<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager>されます。

2. 指定<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.GetHiddenTextSession%2A>したテキスト バッファーのポインターを渡すを呼び出します。 バッファーの<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession>オブジェクトへのポインターを返します。

3. への<xref:System.Runtime.InteropServices.Marshal.QueryInterface%2A>ポインタ<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession>を呼び出<xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession>します。

4. 一<xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession.AddOutlineRegions%2A>度に 1 つ以上の新しいアウトライン領域を追加する呼び出し。

     このメソッドを使用すると、アウトラインするテキストの範囲、既存のアウトライン領域を削除するか保持するか、アウトライン領域を既定で展開するか折りたたむかを指定できます。

## <a name="add-client-controlled-outline-regions"></a>クライアント制御のアウトライン領域を追加する
 この方法を使用して、 および[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)][!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]言語サービスで使用されるようなクライアント制御 (またはスマート) アウトラインを実装します。 独自のアウトラインを管理する言語サービスは、テキスト バッファの内容を監視して、古いアウトライン領域が無効になったときに破棄し、必要に応じて新しいアウトライン領域を作成します。

### <a name="to-implement-a-client-controlled-outline-region"></a>クライアント制御のアウトライン領域を実装するには

1. の`QueryService`呼<xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager>び出し. へのポインターが返<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager>されます。

2. 指定<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.GetHiddenTextSession%2A>したテキスト バッファーのポインターを渡すを呼び出します。 これにより、バッファに対して隠しテキスト セッションが既に存在するかどうかが決定されます。

3. テキスト セッションが既に存在する場合は、作成する<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession>必要はありません。 このポインターを使用して、アウトライン領域を列挙および作成します。 それ以外の<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.CreateHiddenTextSession%2A>場合は、バッファーの隠しテキスト セッションを作成する呼び出し。 オブジェクトへのポインターが<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession>返されます。

    > [!NOTE]
    > を呼び<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.CreateHiddenTextSession%2A>出すときに、隠しテキスト クライアント (つまり、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextClient>オブジェクト) を指定できます。 このクライアントは、隠し文字またはアウトライン領域がユーザーによって展開または折りたたまれたときに通知します。

4. [<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession.AddHiddenRegions%2A>呼び出し構造])パラメータ<xref:Microsoft.VisualStudio.TextManager.Interop.HIDDEN_REGION_TYPE>:`iType`隠し領域<xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion>ではなく、アウトライン領域を作成することを示す場合は、構造体のメンバーの値を指定します。 領域が、構造体の`dwBehavior`メンバー内でクライアント制御か、エディター制御のどちらであるかを<xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion>指定します。 スマート アウトラインの実装には、エディターとクライアント制御のアウトライン領域が混在して含まれる場合があります。 構造のメンバーでアウトライン領域が折りたたまれたときに表示されるバナーテキスト ("..." など`pszBanner`) を<xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion>指定します。 非表示領域のエディターの既定のバナー テキストは "..
