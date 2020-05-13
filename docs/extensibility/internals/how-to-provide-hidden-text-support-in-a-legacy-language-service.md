---
title: 従来の言語サービスで隠しテキストのサポートを提供する
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- hidden text, supporting
- editors [Visual Studio SDK], hidden text
- language services, implementing hidden text regions
ms.assetid: 1c1dce9f-bbe2-4fc3-a736-5f78a237f4cc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8a9d5fe85932f87eb68b6b5a0f5868ebbf8f2b5f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707926"
---
# <a name="how-to-provide-hidden-text-support-in-a-legacy-language-service"></a>方法: 従来の言語サービスで隠しテキストのサポートを提供する
アウトライン領域に加えて、隠し文字領域を作成できます。 隠しテキスト領域は、クライアント制御またはエディター制御が可能で、テキストの領域を完全に非表示にするために使用されます。 エディタは、非表示の領域を水平線で表示します。 この例として、HTML エディタの **[スクリプトのみ]** ビューがあります。

## <a name="to-implement-a-hidden-text-region"></a>隠しテキスト領域を実装するには

1. の`QueryService`呼<xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager>び出し.

     へのポインターが返<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager>されます。

2. 指定<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.GetHiddenTextSession%2A>したテキスト バッファーのポインターを渡すを呼び出します。 これにより、バッファに対して隠しテキスト セッションが既に存在するかどうかが決定されます。

3. 1 つが既に存在する場合は、作成する必要はありませんし、既存<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession>のオブジェクトへのポインターが返されます。 このポインターを使用して、非表示テキスト領域を列挙および作成します。 それ以外の<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.CreateHiddenTextSession%2A>場合は、バッファーの隠しテキスト セッションを作成する呼び出し。

     オブジェクトへのポインターが<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession>返されます。

    > [!NOTE]
    > を呼び`CreateHiddenTextSession`出すときに、隠しテキスト クライアント (<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextClient>つまり、 ) を指定できます。 隠しテキスト クライアントは、ユーザーが非表示のテキストまたはアウトラインを展開または折りたたんだときに通知します。

4. 呼<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession.AddHiddenRegions%2A>び出しを呼び出して、1 つまたは複数の新しいアウトライン領域を一`reHidReg`度<xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion>に追加し、次の情報を ( ) パラメーターに指定します。

    1. アウトライン領域ではなく非表示`hrtConcealed`領域を`iType`<xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion>作成することを示す場合は、構造体のメンバーに の値を指定します。

        > [!NOTE]
        > 隠し領域が非表示になっている場合、エディタは非表示の領域の周囲に自動的に線を表示してその存在を示します。

    2. 領域が、構造体の`dwBehavior`メンバーでクライアント制御か、エディター制御のどちらであるかを指定<xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion>します。 スマート アウトラインの実装には、エディターとクライアント制御のアウトライン領域と非表示テキスト領域の組み合わせを含めることができます。
