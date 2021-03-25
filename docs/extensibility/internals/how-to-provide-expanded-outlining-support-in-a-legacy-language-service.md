---
title: 言語サービスでアウトラインサポートを提供する |Microsoft Docs
description: エディターで制御されるアウトライン領域とクライアントコントロールのアウトライン領域を追加することによって、従来の言語サービスで拡張されたアウトラインサポートを提供する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], outlining support
- language services, supporting outlining
- outlining, supporting
ms.assetid: df759e89-8193-418c-8038-6626304d387b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 11d04af2afac04d4ec9ab197c3d3f7b5a15ad28c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105078787"
---
# <a name="how-to-provide-expanded-outlining-support-in-a-legacy-language-service"></a>方法: 従来の言語サービスで拡張されたアウトラインサポートを提供する
[ **定義に折りたたむ** ] コマンドをサポートしていないと、言語のアウトラインサポートを拡張するためのオプションが2つあります。 エディターによって制御されるアウトライン領域を追加し、クライアントによって制御されるアウトライン領域を追加できます。

## <a name="adding-editor-controlled-outline-regions"></a>エディターで制御されるアウトライン領域の追加
 この方法を使用してアウトライン領域を作成し、その領域が展開されているか折りたたまれているかをエディターが処理できるようにします。 アウトラインサポートを提供する2つのオプションのうち、このオプションは最も堅牢なものです。 このオプションでは、を使用して、指定したテキスト範囲で新しいアウトライン領域を作成し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession.AddOutlineRegions%2A> ます。 この領域が作成されると、その動作はエディターによって制御されます。 エディターで制御されるアウトライン領域を実装するには、次の手順に従います。

### <a name="to-implement-an-editor-controlled-outline-region"></a>エディターで制御されるアウトライン領域を実装するには

1. `QueryService`の呼び出し<xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager>

     これにより、へのポインターが返さ <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager> れます。

2. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.GetHiddenTextSession%2A>を呼び出し、特定のテキストバッファーへのポインターを渡します。 これにより、バッファーのオブジェクトへのポインターが返さ <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> れます。

3. <xref:System.Runtime.InteropServices.Marshal.QueryInterface%2A>へのポインターに対してを呼び出し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession> ます。

4. を呼び出して <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession.AddOutlineRegions%2A> 、一度に1つまたは複数の新しいアウトライン領域を追加します。

     この方法では、アウトラインに使用するテキストの範囲、既存のアウトライン領域を削除するか保存するか、アウトライン領域を既定で展開するか折りたたむかを指定できます。

## <a name="add-client-controlled-outline-regions"></a>クライアントによって制御されるアウトライン領域の追加
 この方法を使用して、および言語サービスで使用されているような、クライアント制御 (またはスマート) のアウトラインを実装し [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] ます。 独自のアウトラインを管理する言語サービスは、古いアウトライン領域が無効になったときに破棄し、必要に応じて新しいアウトライン領域を作成するために、テキストバッファーの内容を監視します。

### <a name="to-implement-a-client-controlled-outline-region"></a>クライアントによって制御されるアウトライン領域を実装するには

1. `QueryService`を呼び出し <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager> ます。 これにより、へのポインターが返さ <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager> れます。

2. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.GetHiddenTextSession%2A>を呼び出し、特定のテキストバッファーへのポインターを渡します。 これにより、バッファーに対して非表示のテキストセッションが既に存在するかどうかが判断されます。

3. テキストセッションが既に存在する場合は、作成する必要はなく、既存のオブジェクトへのポインター <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> が返されます。 このポインターを使用して、アウトライン領域を列挙および作成します。 それ以外の場合は、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.CreateHiddenTextSession%2A> を呼び出して、バッファーの非表示テキストセッションを作成します。 オブジェクトへのポインター <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> が返されます。

    > [!NOTE]
    > を呼び出すと <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.CreateHiddenTextSession%2A> 、非表示のテキストクライアント (つまり、オブジェクト) を指定でき <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextClient> ます。 このクライアントは、非表示のテキストまたはアウトライン領域がユーザーによって展開または折りたたまれたときに通知します。

4. 呼び出し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession.AddHiddenRegions%2A> 構造) パラメーター: <xref:Microsoft.VisualStudio.TextManager.Interop.HIDDEN_REGION_TYPE> `iType` <xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion> 非表示領域ではなくアウトライン領域を作成することを示すために、構造体のメンバーにの値を指定します。 構造体のメンバーで、領域がクライアントによって制御されるか、またはエディターで制御されるかを指定し `dwBehavior` <xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion> ます。 スマートアウトラインの実装には、エディターとクライアントが制御するアウトライン領域を混在させることができます。 `pszBanner`構造体のメンバーに、アウトライン領域が折りたたまれているときに表示されるバナーテキスト ("..." など) を指定し <xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion> ます。 非表示領域のエディターの既定のバナーテキストは "..." です。
